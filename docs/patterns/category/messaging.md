---
title: Nachrichtenmuster
titleSuffix: Cloud Design Patterns
description: Die verteilte Struktur von Cloudanwendungen erfordert eine Messaginginfrastruktur, die die Komponenten und Dienste – idealerweise lose gekoppelt – miteinander verbindet, um die Skalierbarkeit zu maximieren. Asynchrones Messaging ist weit verbreitet und bietet viele Vorteile, beinhaltet aber auch Herausforderungen, beispielsweise die Reihenfolge von Nachrichten, die Verwaltung von nicht verarbeitbaren Nachrichten, Idempotenz und vieles mehr.
keywords: Entwurfsmuster
author: dragon119
ms.date: 03/01/2018
ms.topic: design-pattern
ms.service: architecture-center
ms.subservice: cloud-fundamentals
ms.custom: seodec18
ms.openlocfilehash: f838288e10acf9af5776c93972028b6b878bd7b0
ms.sourcegitcommit: 579c39ff4b776704ead17a006bf24cd4cdc65edd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59640667"
---
# <a name="messaging-patterns"></a>Nachrichtenmuster

Die verteilte Struktur von Cloudanwendungen erfordert eine Messaginginfrastruktur, die die Komponenten und Dienste – idealerweise lose gekoppelt – miteinander verbindet, um die Skalierbarkeit zu maximieren. Asynchrones Messaging ist weit verbreitet und bietet viele Vorteile, beinhaltet aber auch Herausforderungen, beispielsweise die Reihenfolge von Nachrichten, die Verwaltung von nicht verarbeitbaren Nachrichten, Idempotenz und vieles mehr.

| Muster | Zusammenfassung |
| ------- | ------- |
| [Anspruchsprüfung](../claim-check.md) | Teilen Sie eine große Nachricht in eine Anspruchsprüfung und eine Nutzlast auf, um die Überlastung eines Nachrichtenbusses zu vermeiden. |
| [Konkurrierende Consumer](../competing-consumers.md) | Mehreren gleichzeitigen Consumern die Verarbeitung von Nachrichten ermöglichen, die auf dem gleichen Messagingkanal empfangen werden |
| [Pipes und Filter](../pipes-and-filters.md) | Unterteilen einer Aufgabe, die komplexe Verarbeitungsvorgänge ausführt, in eine Reihe wiederverwendbarer separater Elemente |
| [Prioritätswarteschlange](../priority-queue.md) | Priorisieren Sie an Dienste gesendete Anforderungen, sodass Anforderungen mit einer höheren Priorität schneller empfangen und verarbeitet werden als Anforderungen mit einer niedrigeren Priorität. |
| [Publisher-Subscriber](../publisher-subscriber.md) | Ermöglichen Sie einer Anwendung die asynchrone Ankündigung von Ereignissen für mehrere interessierte Consumer, ohne die Absender mit den Empfängern zu koppeln. |
| [Warteschlangenbasierter Lastenausgleich](../queue-based-load-leveling.md) | Verwenden Sie eine Warteschlange, die als Puffer zwischen einem Task und einem von diesem aufgerufenen Dienst fungiert, um unregelmäßig auftretende hohe Lasten aufzufangen. |
| [Scheduler-Agent-Supervisor](../scheduler-agent-supervisor.md) | Koordinieren Sie eine Reihe von Aktionen in einer verteilten Gruppe von Diensten und anderen Remoteressourcen. |
