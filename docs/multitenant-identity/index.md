---
title: Identitätsverwaltung für mehrinstanzenfähige Anwendungen
description: Bewährte Methoden für die Authentifizierung, Autorisierung und Identitätsverwaltung mehrmandantenfähiger Apps.
author: MikeWasson
ms.date: 07/21/2017
ms.topic: guide
ms.service: architecture-center
ms.subservice: reference-architecture
ms.openlocfilehash: be906106fb12c381d57ad40ae22e748dcff9722f
ms.sourcegitcommit: c053e6edb429299a0ad9b327888d596c48859d4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58346075"
---
# <a name="manage-identity-in-multitenant-applications"></a>Verwalten der Identität in mehrinstanzenfähigen Anwendungen

In dieser Artikelreihe werden bewährte Methoden für Mehrmandantenfähigkeit bei Verwendung von Azure AD für die Authentifizierung und Identitätsverwaltung beschrieben.

[![GitHub](../_images/github.png)-Beispielcode][sample-application]

Beim Erstellen einer mehrmandantenfähigen Anwendung besteht eine der ersten Herausforderungen in der Verwaltung der Benutzeridentitäten, da jeder Benutzer nun zu einem Mandanten gehört. Beispiel: 

- Benutzer melden sich bei der App mit den Anmeldeinformationen ihrer Organisation an.
- Benutzer sollten Zugriff auf Daten der eigenen Organisation haben, dürfen jedoch nicht auf Daten anderer Mandanten zugreifen.
- Eine Organisation kann sich für eine Anwendung anmelden und Organisationsmitgliedern dann Anwendungsrollen zuweisen.

Azure Active Directory (Azure AD) verfügt über einige hervorragende Funktionen, die alle diese Szenarios unterstützen.

Wir haben begleitend für diese Artikelreihe eine vollständige [End-to-End-Implementierung][sample-application] einer mehrmandantenfähigen Anwendung erstellt. Die Artikel fassen zusammen, was wir im Verlauf der Erstellung dieser Anwendung gelernt haben. Informationen zu den ersten Schritten mit der Anwendung finden Sie unter [Run the Surveys application][running-the-app] (Ausführen der Surveys-Anwendung).

## <a name="introduction"></a>Einführung

Angenommen, Sie schreiben eine SaaS-Unternehmensanwendung, die in der Cloud gehostet werden soll. Selbstredend hat die Anwendung Benutzer:

![Benutzer](./images/users.png)

Doch diese Benutzer gehören zu Organisationen:

![Organisationsbenutzer](./images/org-users.png)

Beispiel: Tailspin verkauft Abonnements für seine SaaS-Anwendung. Contoso und Fabrikam registrieren Sie sich für die App. Wenn Alice (`alice@contoso`) sich anmeldet, sollte die Anwendung wissen, dass Alice zu Contoso gehört.

- Alice *muss* Zugriff auf Contoso-Daten haben.
- Alice *darf keinen* Zugriff auf Fabrikam-Daten haben.

In dieser Anleitung wird gezeigt, wie Sie Benutzeridentitäten in einer mehrmandantenfähigen Anwendung verwalten und dabei [Azure Active Directory](/azure/active-directory) (Azure AD) für die Anmeldung und Authentifizierung verwenden.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-multitenancy"></a>Was bedeutet Mehrmandantenfähigkeit?

<!-- markdownlint-enable MD026 -->

Ein *Mandant* ist eine Gruppe von Benutzern. Bei einer SaaS-Anwendung ist der Mandant ein Abonnent oder Kunde der Anwendung. *Mehrmandantenfähigkeit* ist eine Architektur, in der mehrere Mandanten gemeinsam die gleiche physische Instanz der App nutzen. Obwohl Mandanten physische Ressourcen (z. B. VMs oder Speicher) gemeinsam nutzen, erhält jeder Mandant eine eigene logische Instanz der App.

In der Regel werde Anwendungsdaten von den Benutzern innerhalb eines Mandanten, jedoch nicht mit anderen Mandanten gemeinsam genutzt.

![Mehrere Mandanten](./images/multitenant.png)

Vergleichen Sie diese Architektur mit einer Architektur mit nur einem Mandanten, bei der jeder Mandant über eine dedizierte physische Instanz verfügt. Bei einer Architektur mit nur einem Mandanten fügen Sie Mandanten hinzu, indem Sie neue Instanzen der App in Betrieb nehmen.

![Einzelner Mandant](./images/single-tenant.png)

### <a name="multitenancy-and-horizontal-scaling"></a>Mehrmandantenfähigkeit und horizontale Skalierung

Zur Skalierung in der Cloud werden im Allgemeinen mehrere physische Instanzen hinzugefügt. Dies wird als *horizontale Skalierung* oder *horizontales Hochskalieren* bezeichnet. Nehmen Sie als Beispiel eine Web-App. Um mehr Datenverkehr zu bewältigen, können Sie weitere Server-VMs hinzufügen und für diese einen Lastenausgleich vornehmen. Jede VM führt eine separate physische Instanz der Web-App aus.

![Lastenausgleich für eine Website](./images/load-balancing.png)

Jede Anforderung kann an eine beliebige Instanz weitergeleitet werden. Zusammen arbeitet das System als eine einzelne logische Instanz. Sie können eine VM entfernen oder eine neue VM hinzufügen, ohne dass sich dies auf Benutzer auswirkt. In dieser Architektur ist jede physische Instanz mehrmandantenfähig, und zum Skalieren fügen Sie weitere Instanzen hinzu. Falls eine Instanz ausfällt, sollte dies keine Auswirkungen auf irgendeinen Mandanten haben.

## <a name="identity-in-a-multitenant-app"></a>Identität in einer mehrmandantenfähigen App

In einer mehrmandantenfähigen App müssen Sie Benutzer im Kontext von Mandanten berücksichtigen.

### <a name="authentication"></a>Authentication

- Benutzer melden Sie sich bei der App mit den Anmeldeinformationen für Ihre Organisation an. Sie müssen keine neuen Benutzerprofile für die App erstellen.
- Benutzer innerhalb derselben Organisation gehören zum selben Mandanten.
- Wenn sich ein Benutzer anmeldet, weiß die Anwendung, zu welchem Mandanten der Benutzer gehört.

### <a name="authorization"></a>Autorisierung

- Bei der Autorisierung der Aktionen eines Benutzers (z. B. Anzeigen einer Ressource) muss die App den Mandanten des Benutzers berücksichtigen.
- Benutzer können innerhalb der Anwendung Rollen wie „Admin“ oder „Standardbenutzer“ zugewiesen werden. Rollenzuweisungen müssen vom Kunden und nicht vom SaaS-Anbieter verwaltet werden.

**Beispiel:** Alice, eine Mitarbeiterin von Contoso, navigiert in ihrem Browser zur Anwendung und klickt auf die Schaltfläche „Anmelden“. Sie wird zu einer Anmeldeseite umgeleitet, auf der sie ihre Unternehmensanmeldeinformationen (Benutzername und Kennwort) eingibt. An dieser Stelle wird sie in der Anwendung als `alice@contoso.com`angemeldet. Die Anwendung erkennt auch, dass Alice eine Administratorbenutzerin dieser Anwendung ist. Da sie eine Administratorin ist, wird ihr eine Liste aller Ressourcen gezeigt, die zu Contoso gehören. Sie kann jedoch nicht Ressourcen von Fabrikam anzeigen, da sie nur in ihrem Mandanten Administratorin ist.

In dieser Anleitung untersuchen wir insbesondere den Einsatz von Azure AD für die Identitätsverwaltung.

- Wir setzen voraus, dass der Kunde Benutzerprofile (einschließlich Office 365- und Dynamics CRM-Mandanten) in Azure AD speichert.
- Kunden mit einer lokalen Active Directory-Instanz können [Azure AD Connect](/azure/active-directory/hybrid/whatis-hybrid-identity) verwenden, um ihre lokale Active Directory-Instanz mit Azure AD zu synchronisieren. Falls ein Kunde mit lokaler Active Directory-Instanz Azure AD Connect aufgrund von IT-Unternehmensrichtlinien oder aus einem anderen Grund nicht verwenden kann, kann der SaaS-Anbieter über Active Directory-Verbunddienste (AD FS) einen Verbund mit dem Verzeichnis des Kunden einrichten. Diese Option wird unter [Federating with a customer's AD FS](adfs.md)(Herstellen eines Verbunds mit den AD FS eines Kunden) beschrieben.

Andere Aspekte der Mehrmandantenfähigkeit (z. B. Datenpartitionierung, Einzelmandantenkonfiguration usw.) werden in dieser Anleitung nicht behandelt.

[**Weiter**](./tailspin.md)

<!-- links -->

[sample-application]: https://github.com/mspnp/multitenant-saas-guidance
[running-the-app]: ./run-the-app.md
