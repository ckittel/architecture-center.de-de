---
title: "Checkliste für die Skalierbarkeit"
description: "Checkliste für die Skalierbarkeit für Entwurfsprobleme bei automatischer Azure-Skalierung."
author: dragon119
ms.date: 03/24/2017
ms.custom: checklist
ms.openlocfilehash: 250fa2d56720c476bb604c5dba684e938088b6a0
ms.sourcegitcommit: b0482d49aab0526be386837702e7724c61232c60
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2017
---
# <a name="scalability-checklist"></a>Checkliste für die Skalierbarkeit
[!INCLUDE [header](../_includes/header.md)]

## <a name="service-design"></a>Dienstentwurf
* **Partitionieren der Workload**. Entwickeln Sie Teile des Prozesses als diskret und zerlegbar. Minimieren Sie die Größe der einzelnen Teile, während Sie die üblichen Regeln für die Trennung von Belangen und das Single-Responsibility-Prinzip befolgen. Dadurch können Komponententeile auf eine Weise verteilt werden, die die Verwendung jeder Recheneinheit (beispielsweise eine Rolle oder ein Datenbankserver) maximiert. Es erleichtert auch die Skalierung der Anwendung, indem Sie Instanzen bestimmter Ressourcen hinzufügen. Weitere Informationen finden Sie unter [Leitfaden Partitionierungsberechnung](https://msdn.microsoft.com/library/dn589773.aspx).
* **Entwurf für die Skalierung**. Skalierung ermöglicht es Anwendungen, auf veränderbare Last zu reagieren, indem sie die Anzahl der Instanzen der Rollen, Warteschlangen und andere Dienste, die sie verwenden, erhöhen und verringern. Die Anwendung muss jedoch zu diesem Zweck entworfen werden. Die Anwendung und die verwendeten Dienste müssen z. B. statusfrei sein, damit Anforderungen an eine beliebige Instanz weitergeleitet werden können. Dies verhindert die Beeinträchtigung der aktuellen Benutzer durch das Hinzufügen oder Entfernen von bestimmten Instanzen. Sie sollten auch die Konfiguration oder automatische Erkennung von Instanzen implementieren, während diese hinzugefügt und entfernt werden, sodass der Code in der Anwendung das notwendige Routing durchführen kann. Eine Webanwendung kann z. B. eine Reihe von Warteschlangen in einem Roundrobin-Ansatz verwenden, um Anforderungen an Hintergrunddienste weiterzuleiten, die in Workerrollen ausgeführt werden. Die Webanwendung muss Änderungen hinsichtlich der Anzahl der Warteschlangen erkennen können, um Anforderungen erfolgreich weiterleiten und den Lastenausgleich der Anwendung durchführen zu können.
* **Als Einheit skalieren**. Planen Sie zusätzliche Ressourcen ein, um ein Wachstum zu ermöglichen. Sie sollten für jede Ressource die oberen Skalierungsgrenzen kennen und Sharding oder Zerlegung verwenden, um über diese Grenzen hinausgehen. Bestimmen der Skalierungseinheiten für das System im Hinblick auf klar definierte Ressourcensätze. Dadurch ist die Anwendung der horizontalen Hochskalierung einfacher und weniger anfällig für negative Auswirkungen auf die Anwendung aufgrund von Einschränkungen, die durch den Mangel an Ressourcen in einem Teil des gesamten Systems verursacht werden. Zum Beispiel kann das Hinzufügen von x Web- und Workerrollen möglicherweise y zusätzliche Warteschlangen und z Speicherkonten erforderlich machen, um die durch die Rollen generierte Workload zu bewältigen. Eine Skalierungseinheit kann somit aus x Web- und Workerrollen, *y* Warteschlangen und *z* Speicherkonten bestehen. Entwerfen Sie die Anwendung so, dass sie einfach skaliert wird, indem Sie eine oder mehrere Skalierungseinheiten hinzufügen.
* **Vermeiden von Clientaffinität**. Stellen Sie wenn möglich sicher, dass für die Anwendung keine Affinität erforderlich ist. Anfragen können dadurch an eine beliebige Instanz weitergeleitet werden, und die Anzahl der Instanzen ist irrelevant. Dies verhindert auch den Aufwand für das Speichern, Abrufen und Verwalten von Zustandsinformationen für jeden einzelnen Benutzer.
* **Nutzung von Funktionen der automatischen Plattformskalierung**. Wenn die Hostingplattform eine Funktion für die automatische Skalierung unterstützt, z. B. Azure Autoscale, bevorzugen Sie diese vor benutzerdefinierten Mechanismen oder Drittanbietermechanismen, es sei denn der integrierte Mechanismus kann Ihre Anforderungen nicht erfüllen. Verwenden Sie wo möglich geplante Skalierungsregeln, um sicherzustellen, dass die Ressourcen ohne Startverzögerung zur Verfügung stehen. Fügen Sie jedoch automatische reaktive Skalierungsregeln hinzu, um gegebenenfalls unerwartete Änderungen der Nachfrage zu bewältigen. Sie können die Vorgänge der automatischen Skalierung in der Dienstverwaltungs-API verwenden, um die automatische Skalierung anzupassen und um Regeln benutzerdefinierte Leistungsindikatoren hinzufügen. Weitere Informationen finden Sie unter [Anleitungen für die automatische Skalierung](../best-practices/auto-scaling.md).
* **Offload-intensive CPU/IO-Vorgänge als Hintergrundaufgaben**. Lagern Sie die Verarbeitung für diese Anforderung in einer separaten Aufgabe aus, wenn erwartet wird, dass eine Anforderung an einen Dienst lange Zeit für die Ausführung benötigt oder beträchtliche Ressourcen absorbiert. Verwenden Sie zum Ausführen dieser Aufgaben Workerrollen oder Hintergrundaufträge (abhängig von der Hostingplattform). Dadurch kann den Dienst weiterhin Anforderungen erhalten und reaktionsfähig bleiben.  Weitere Informationen finden Sie unter [Leitfaden für Hintergrundaufträge](../best-practices/background-jobs.md).
* **Verteilen Sie die Workload für Hintergrundaufgaben**. Wenn es viele Hintergrundaufgaben gibt oder die Aufgaben beträchtliche Zeit oder Ressourcen erfordern, können Sie die Arbeit auf mehrere Recheneinheiten (z. B. Workerrollen oder Hintergrundaufträge) verteilen. Eine mögliche Lösung ist das [Muster „Konkurrierende Consumer“](https://msdn.microsoft.com/library/dn568101.aspx).
* **Erwägen Sie den Übergang zu einer *Shared-Nothing*-Architektur**. Eine Architektur ohne gemeinsam genutzte Inhalte verwendet unabhängige, eigenständige Knoten, die keine einzelnen Konfliktpunkt haben (z. B. gemeinsame Dienste oder Speicher). Theoretisch kann ein solches System fast unbegrenzt skaliert werden. Während ein vollständiger Ansatz ohne gemeinsam genutzte Inhalte im Allgemeinen für die meisten Anwendungen nicht geeignet ist, bietet er Möglichkeiten für Entwürfe mit besserer Skalierbarkeit. Die Vermeidung der Verwendung von serverseitigem Sitzungsstatus, Clientaffinität und Datenpartitionierung sind gute Beispiele für den Übergang zu einer Architektur ohne gemeinsam genutzte Inhalte.

## <a name="data-management"></a>Datenverwaltung
* **Verwenden Sie Datenpartitionierung**. Teilen Sie die Daten auf mehrere Datenbanken und Datenbankserver auf, oder entwerfen Sie die Anwendung zur Verwendung von Datenspeicherdiensten, die diese Partitionierung transparent gewährleisten (z. B. Elastische Datenbank für Azure SQL-Datenbank und Azure-Tabellenspeicher). Dieser Ansatz hilft bei der Leistungsmaximierung und ermöglicht einfachere Skalierung. Es gibt verschiedene Partitionierungsverfahren wie horizontale, vertikale und funktionale Partitionierung. Sie können eine Kombination dieser Verfahren nutzen, um optimalen Nutzen aus verbesserter Abfrageleistung, einfacherer Skalierbarkeit, flexiblerer Verwaltung, besserer Verfügbarkeit und eine Übereinstimmung des Speichertyps und der darin enthaltenen Daten zu erreichen. Berücksichtigen Sie außerdem die verschiedenen Arten von Datenspeichern für verschiedene Arten von Daten. Wählen Sie die Typen basierend darauf aus, wie gut sie für den spezifischen Datentyp optimiert sind. Dazu zählt beispielsweise die Verwendung von Tabellenspeicher, einer Dokumentendatenbank oder eines Spalte-Familien-Datenspeichers anstelle von oder zusätzlich zu einer relationalen Datenbank. Weitere Informationen finden Sie unter [Leitfaden Datenpartitionierung](../best-practices/data-partitioning.md).
* **Design für letztendliche Konsistenz**. Letztendliche Konsistenz verbessert die Skalierbarkeit durch das Reduzieren oder Entfernen des Zeitaufwands für die Synchronisierung verknüpfter Daten, die über mehrere Speicher aufgeteilt sind. Der Preis ist, dass Daten beim Lesen nicht immer konsistent sind und einige Schreibvorgänge möglicherweise Konflikte verursachen. Letztendliche Konsistenz ist ideal für Situationen, in denen die gleichen Daten oft gelesen jedoch selten geschrieben werden. Weitere Informationen finden Sie unter [Data Consistency Primer](https://msdn.microsoft.com/library/dn589800.aspx)(Grundlagen der Datenkonsistenz).
* **Reduzieren Sie viele Einzelaufrufinteraktionen zwischen Komponenten und Diensten**. Vermeiden Sie das Entwerfen von Interaktionen, bei denen eine Anwendung mehrere Aufrufe an einen Dienst machen muss (von denen jeder eine kleine Menge Daten zurückgibt), statt einem einzigen Aufruf, der alle Daten zurückgeben kann. Kombinieren Sie wenn möglich mehrere verwandte Vorgänge in einer einzigen Anforderung, wenn der Aufruf eines Dienstes oder einer Komponente mit spürbarer Latenz erfolgt. Dies vereinfacht die Überwachung der Leistung und Optimierung komplexer Vorgänge. Verwenden Sie z. B. gespeicherte Prozeduren in Datenbanken, um komplexe Logik einzukapseln, und reduzieren Sie die Anzahl der Roundtrips und Sperren für Ressourcen.
* **Verwenden Sie Warteschlangen, um die Last für Schreibvorgänge mit hoher Geschwindigkeit auszugleichen**. Nachfrageschübe für einen Dienst können diesen Dienst überlasten und eskalierende Fehler verursachen. Um dies zu verhindern, empfiehlt sich die  Implementieren des [Warteschlangenbasierten Lastenausgleichsmusters](https://msdn.microsoft.com/library/dn589783.aspx). Verwenden Sie eine Warteschlange, die als Puffer zwischen einer Aufgabe und einem Dienst, den sie aufruft, fungiert. Dies kann eine vorübergehend starke Auslastung ausgleichen, die andernfalls zu einem Ausfall des Diensts oder zu einem Timeout der Aufgabe führen kann.
* **Minimieren Sie die Belastung des Datenspeichers**. Der Datenspeicher ist in der Regel ein Verarbeitungsengpass, eine teure Ressource, und er lässt sich oft nicht einfach horizontal hochskalieren. Entfernen Sie nach Möglichkeit Logik (z. B. die Verarbeitung von XML-Dokumenten oder JSON-Objekten) aus dem Datenspeicher, und führen Sie die Verarbeitung in der Anwendung durch. Serialisieren oder deserialisieren Sie beispielsweise den XML-Code in der Anwendungsschicht, und übergeben Sie ihn an ein datenspeichereigenes Format, anstatt XML an die Datenbank zu übergeben (außer als nicht transparente Zeichenfolge für den Speicher). In der Regel ist es einfacher, die Anwendung horizontal hochzuskalieren als den Datenspeicher. Sie sollten also versuchen, den größtmöglichen Teil der rechenintensiven Verarbeitung innerhalb der Anwendung auszuführen.
* **Minimieren der abgerufenen Datenmenge**. Rufen Sie nur die Daten ab, die Sie benötigen, indem Sie Spalten und Kriterien zum Auswählen von Zeilen angeben. Verwenden Sie Tabellenwertparameter und die entsprechenden Isolationsgrade. Verwenden Sie Mechanismen wie Entitätstags, um ein unnötiges Abrufen von Daten zu vermeiden.
* **Verwenden Sie Zwischenspeichern aggressiv**. Verwenden Sie nach Möglichkeit Zwischenspeicherung, um die Ressourcen und Dienste zu verringern, die Daten generieren oder übermitteln. Zwischenspeichern ist in der Regel für Daten geeignet, die relativ statisch sind oder für deren Erhalt beträchtliche Verarbeitung notwendig ist. Eine Zwischenspeicherung sollte gegebenenfalls auf allen Ebenen der Anwendung erfolgen, einschließlich bei Datenzugriff und Generierung der Benutzeroberfläche. Weitere Informationen finden Sie unter [Leitfaden Zwischenspeichern](../best-practices/caching.md).
* **Umgang mit Datenzuwachs und -aufbewahrung**. Die Datenmenge, die von einer Anwendung gespeichert wird, wächst mit der Zeit. Dieses Wachstum erhöht die Speicherkosten und die Latenz beim Zugriff auf die Daten, was wiederum den Anwendungsdurchsatz und die Leistung beeinflusst. Es ist möglich, regelmäßig einige der alten Daten zu archivieren, auf die nicht mehr zugegriffen wird, oder Daten, auf die selten zugegriffen wird, in den langfristigen Speicher zu verschieben, der kostengünstiger ist, aber eine höhere Zugriffslatenz hat.
* **Optimieren von Data Transfer Objects (DTOs) mit einem effizienten Binärformat**. DTOs werden viele Male zwischen den Ebenen einer Anwendung übergeben. Wenn Sie die Größe minimieren, wird die Belastung von Ressourcen und dem Netzwerk reduziert. Wägen Sie jedoch die Ersparnisse gegen den Aufwand für das Konvertieren der Daten in das erforderliche Format an jedem Einsatzort ab. Übernehmen Sie ein Format, das maximale Interoperabilität bietet, um eine einfache Wiederverwendung einer Komponente zu ermöglichen.
* **Cachesteuerung einstellen**. Entwerfen und konfigurieren Sie die Anwendung derart, dass wenn möglich eine Ausgabezwischenspeicherung oder Fragmentzwischenspeicherung verwendet wird, um die Verarbeitungslast zu minimieren.
* **Aktivieren Sie clientseitiges Zwischenspeichern**. Webanwendungen sollten Cacheeinstellungen für Inhalte aktivieren, die zwischengespeichert werden können. Dies ist häufig standardmäßig deaktiviert. Konfigurieren Sie den Server für die Lieferung entsprechender Cache-Control-Header, um die Zwischenspeicherung von Inhalten auf Proxyservern und Clients zu aktivieren.
* **Verwenden Sie Azure Blob Storage und Azure Content Delivery Network zur Reduzierung der Auslastung der Anwendung**. Erwägen Sie die Speicherung von statischen oder relativ statischen öffentlichen Inhalten wie Bildern, Ressourcen, Skripten und Stylesheets im Blobspeicher. Dieser Ansatz befreit die Anwendung von der Arbeitsbelastung, die durch die dynamische Generierung dieser Inhalte für jede Anforderung  entsteht. Darüber hinaus sollten Sie die Verwendung des Content Delivery Network zum Zwischenspeichern dieser Inhalte und für die Lieferung an Clients in Betracht ziehen. Die Verwendung des Content Delivery Network kann die Leistung auf dem Client verbessern, da Inhalte aus dem geografisch am nächsten liegenden Rechenzentrum mit Content Delivery Network-Cache übermittelt werden. Weitere Informationen finden Sie unter der [Anleitungen zum Content Delivery Network (CDN)](../best-practices/cdn.md).
* **Optimieren und rationalisieren Sie SQL-Abfragen und Indizes**. Einige T-SQL-Anweisungen oder Konstrukte haben möglicherweise Auswirkungen auf die Leistung, die durch die Optimierung eines Codes in einer gespeicherten Prozedur reduziert werden können. Vermeiden Sie z.B. die Konvertierung von **datetime**-Typen in einen **varchar** vor dem Vergleich mit einem **datetime**-Literalwert. Verwenden Sie stattdessen die Datum/Uhrzeit-Vergleichsfunktionen. Das Fehlen geeigneter Indizes kann die Ausführung der Abfrage auch verlangsamen. Wenn Sie ein Framework für objekt-relationale Zuordnung verwenden, stellen Sie sicher, dass Sie verstehen, wie es funktioniert und wie es sich auf die Leistung der Datenzugriffsschicht auswirkt. Weitere Informationen finden Sie unter [Abfrageoptimierung](https://technet.microsoft.com/library/ms176005.aspx).
* **Erwägen Sie die Denormalisierung von Daten**. Datennormalisierung hilft, Duplizierung und Inkonsistenzen zu vermeiden. Die Verwaltung mehrerer Indizes, Prüfung auf referenzielle Integrität, Durchführung mehrerer Zugriffe auf kleine Datenblöcke und Verknüpfung von Tabellen, um die Daten wieder zusammenzusetzen, führt zu einem Aufwand, der sich auf die Leistung auswirken kann. Überlegen Sie, ob etwas zusätzliches Speichervolumen und Duplizierung akzeptabel ist, um die Last auf den Datenspeicher zu reduzieren. Berücksichtigen Sie auch, ob auf die Anwendung selbst (die in der Regel leichter zu skalieren ist) zurückgegriffen werden kann, um Aufgaben wie das Verwalten von referenzieller Integrität zu übernehmen, damit die Last für den Datenspeicher verringert wird. Weitere Informationen finden Sie unter [Leitfaden Datenpartitionierung](../best-practices/data-partitioning.md).

## <a name="service-implementation"></a>Dienstimplementierung
* **Verwenden Sie asynchrone Aufrufe**. Verwenden Sie wenn möglich asynchronen Code beim Zugriff auf Ressourcen oder Dienste, die durch E/A oder Netzwerkbandbreite beschränkt sein können oder die eine merkliche Latenz haben, um eine Sperrung des aufrufenden Threads zu vermeiden. Verwenden Sie zum Implementieren von asynchronen Vorgängen das [aufgabenbasierte asynchrone Muster](https://msdn.microsoft.com/library/hh873175.aspx).
* **Vermeiden Sie das Sperren von Ressourcen, und verwenden Sie stattdessen einen optimistischen Ansatz**. Sperren Sie nie den Zugriff auf Ressourcen wie z. B. Speicher oder andere Dienste, die merkliche Latenz haben, da es sich dabei um eine primäre Ursache von Leistungseinbußen handelt. Verwenden Sie immer optimistische Ansätze, um gleichzeitige Vorgänge wie z. B. das Schreiben in den Speicher zu verwalten. Verwenden Sie die Funktionen der Speicherschicht, um Konflikte zu verwalten. In verteilten Anwendungen können Daten nur letztendlich konsistent sein.
* **Komprimieren Sie sehr stark komprimierbare Daten über Netzwerke mit hohen Wartezeiten und geringer Bandbreite**. In den meisten Fällen stellen in einer Webanwendung HTTP-Antworten auf Clientanforderungen die größte von der Anwendung generierte und über das Netzwerk übertragene Datenmenge. HTTP-Komprimierung kann dies besonders für statische Inhalte erheblich reduzieren. Dies kann Kosteneinsparungen und Lastverringerung für das Netzwerk bieten, obwohl die Komprimierung dynamischer Inhalte zu einer minimal höheren Auslastung auf dem Server führt. In anderen allgemeinen Umgebungen kann die Datenkomprimierung die übertragene Datenmenge reduzieren und den Zeit- und Kostenaufwand minimieren, jedoch führen die Komprimierungs- und Dekomprimierungsprozesse zu einem Mehraufwand. Daher sollte die Komprimierung nur verwendet werden, wenn ein nachweisbarer Leistungsgewinn besteht. Andere Serialisierungsmethoden, z. B. JSON oder binäre Codierungen, können die Nutzlastgröße bei geringerer Auswirkung auf die Leistung senken, wobei sie sich bei XML wahrscheinlich vergrößert.
* **Verkürzen Sie die Zeit, die Verbindungen und Ressourcen verwendet werden**. Verwalten Sie Verbindungen und Ressourcen nur, solange Sie sie verwenden müssen. Öffnen Sie z. B. Verbindungen so spät wie möglich, und ermöglichen Sie die baldmöglichste Rückgabe an den Verbindungspool. Greifen Sie auf die Ressourcen so spät wie möglich zu, und entsorgen Sie sie so schnell wie möglich.
* **Minimieren Sie die Anzahl der benötigten Verbindungen**. Dienstverbindungen absorbieren Ressourcen. Begrenzen Sie die erforderliche Anzahl, und stellen Sie sicher, dass vorhandene Verbindungen möglichst wiederverwendet werden. Verwenden Sie z. B. nach dem Ausführen der Authentifizierung gegebenenfalls den Identitätswechsel, um einen Code als bestimmte Identität auszuführen. Dies kann dabei helfen, den Verbindungspool durch die Wiederverwendung von Verbindungen optimal zu nutzen.
  
  > [!NOTE]
  > : APIs verwenden Verbindungen für einige Dienste automatisch wieder, sofern dienstspezifische Richtlinien eingehalten werden. Es ist wichtig, dass Sie die Umstände verstehen, unter denen eine Verbindung für jeden Dienst, die die Anwendung nutzt, erneut verwendet werden kann.
  > 
  > 
* **Senden Sie zur Optimierung der Netzwerknutzung Anforderungen in Batches**. Senden Sie z. B. Nachrichten stapelweise, wenn Sie auf eine Warteschlange zugreifen und führen Sie beim Zugriff auf Speicher oder einen Cache mehrere Lese- oder Schreibvorgänge als Batch aus. Dies kann helfen, die Effizienz der Dienste und Datenspeicher zu maximieren, indem die Anzahl der Aufrufe über das Netzwerk verringert wird.
* **Vermeiden Sie eine Anforderung zum Speichern des serverseitigen Sitzungsstatus** wenn möglich. Serverseitige Sitzungsstatusverwaltung erfordert in der Regel Clientaffinität (sprich das Routing jeder Anforderung zur gleichen Serverinstanz), wodurch die Skalierungsfähigkeit des Systems beeinflusst wird. Im Idealfall sollten Sie die Clients in Bezug auf die Server, die sie verwenden, statusfrei entwerfen. Speichern Sie jedoch vertrauliche Daten oder große Mengen von Client-Daten in einem verteilten serverseitigen Cache, auf den alle Instanzen der Anwendung zugreifen können, wenn die Anwendung den Sitzungszustand beibehalten muss.
* **Optimieren Sie Tabellenspeicherschemas**. Erwägen Sie bei der Verwendung von Tabellenspeichern, bei denen die Tabellen- und Spaltennamen übergeben und mit jeder Abfrage verarbeitet werden müssen, wie z. B. Azure-Tabellenspeicher, die Nutzung von kürzeren Namen, um diesen zusätzlichen Aufwand zu reduzieren. Gehen Sie keine Kompromisse hinsichtlich der Lesbarkeit und Verwaltbarkeit ein, indem Sie übermäßig kompakte Namen verwenden.
* **Verwenden Sie die Task Parallel Library (TPL) zum Durchführen asynchroner Vorgänge**. Die TPL erleichtert das Schreiben von asynchronem Code, der E/A-Vorgänge ausführt. Verwenden Sie *ConfigureAwait(false)* so oft wie möglich, um die Abhängigkeit von einer Fortsetzung von einem bestimmten Synchronisierungskontext zu beseitigen. Damit reduzieren Sie auch die Wahrscheinlichkeit für einen Thread-Deadlock.
* **Stellen Sie Ressourcenabhängigkeiten während der Bereitstellung oder beim Anwendungsstart her**. Vermeiden Sie den wiederholten Aufruf von Methoden, die das Vorhandensein einer Ressource testen und dann die Ressource erstellen, wenn sie nicht vorhanden ist. (Methoden wie *CloudTable.CreateIfNotExists* und *CloudQueue.CreateIfNotExists* in der Azure Storage-Clientbibliothek folgen diesem Muster.) Diese Methoden können einen beträchtlichen Aufwand nötig machen, wenn sie vor jedem Zugriff auf einen Tabellenspeicher oder eine Speicherwarteschlange aufgerufen werden. Alternative:
  * Erstellen Sie die erforderlichen Ressourcen beim Bereitstellen der Anwendung oder beim ersten Start. (Ein einzelner Aufruf von *CreateIfNotExists* für jede Ressource im Startcode für eine Web- oder Workerrolle ist zulässig.) Achten Sie jedoch darauf, Ausnahmen zu behandeln, die auftreten können, wenn der Code versucht, auf eine Ressource zuzugreifen, die nicht vorhanden ist. In diesen Fällen sollten Sie die Ausnahme protokollieren und möglicherweise einen Operator darüber benachrichtigen, dass eine Ressource fehlt.
  * Unter bestimmten Umständen ist es angebracht, die fehlende Ressource als Teil des Ausnahmebehandlungscodes zu erstellen. Sie sollten diesen Ansatz jedoch mit Vorsicht anwenden, da das Nichtvorhandensein der Ressource auf einen Programmierfehler (z. B. einen falsch geschriebenen Ressourcennamen) oder auf ein anderes Problem auf Infrastrukturebene hinweisen könnte.
* **Verwenden Sie einfache Frameworks**. Wählen Sie die APIs und Frameworks die Sie verwenden sorgfältig, um die Ressourcennutzung und Ausführungszeit sowie die Gesamtlast auf die Anwendung zu minimieren. Die Verwendung von Web-API zur Behandlung von Dienstanforderungen kann den Platzbedarf der Anwendung reduzieren und die Ausführungsgeschwindigkeit erhöhen, ist aber möglicherweise nicht für komplexere Szenarien geeignet, in denen die zusätzlichen Funktionen von Windows Communication Foundation erforderlich sind.
* **Erwägen Sie, die Anzahl der Dienstkonten zu minimieren**. Verwenden Sie z. B. ein spezielles Konto für den Zugriff auf Ressourcen oder Dienste, die Verbindungen beschränken oder bessere Leistung bringen, wenn weniger Verbindungen verwaltet werden. Dieser Ansatz wird häufig für Dienste wie z. B. Datenbanken verwendet, kann aber die Möglichkeit zur genauen Überwachung der Vorgänge aufgrund der Identitätswechsel des ursprünglichen Benutzers beeinflussen.
* **führen Sie Leistungsprofilerstellung und Auslastungstests durch** und stellen vor der endgültigen Version sicher, dass die Anwendung ausführt und nach Bedarf skaliert wird. Diese Tests sollten auf der gleichen Art von Hardware stattfinden, wie die Produktionsplattform, mit den gleichen Datentypen und -mengen sowie der Benutzerauslastung, die in der Produktion auftreten. Weitere Informationen finden Sie unter [Testen der Leistung eines Clouddiensts](/azure/vs-azure-tools-performance-profiling-cloud-services/).
