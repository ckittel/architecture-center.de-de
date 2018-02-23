---
title: "Auswählen einer Technologie für die Echtzeiterfassung von Nachrichten"
description: 
author: zoinerTejada
ms:date: 02/12/2018
ms.openlocfilehash: 2e6578b779950b5ef11bda7b8ba1fb2e45e09f4e
ms.sourcegitcommit: 3d9ee03e2dda23753661a80c7106d1789f5223bb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="choosing-a-real-time-message-ingestion-technology-in-azure"></a><span data-ttu-id="d0406-102">Auswählen einer Technologie für die Echtzeiterfassung von Nachrichten in Azure</span><span class="sxs-lookup"><span data-stu-id="d0406-102">Choosing a real-time message ingestion technology in Azure</span></span>

<span data-ttu-id="d0406-103">Bei der Echtzeitverarbeitung werden Datenströme in Echtzeit erfasst und mit minimaler Wartezeit verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="d0406-103">Real time processing deals with streams of data that are captured in real-time and processed with minimal latency.</span></span> <span data-ttu-id="d0406-104">Viele Lösungen für die Echtzeitverarbeitung erfordern jedoch einen Speicher für die Erfassung von Nachrichten, der als Puffer für Nachrichten fungiert. Der Speicher muss zudem die Verarbeitung mit horizontaler Skalierung, eine zuverlässige Übermittlung sowie weitere Semantik für das Nachrichtenqueuing unterstützen.</span><span class="sxs-lookup"><span data-stu-id="d0406-104">Many real-time processing solutions need a message ingestion store to act as a buffer for messages, and to support scale-out processing, reliable delivery, and other message queuing semantics.</span></span> 

## <a name="what-are-your-options-for-real-time-message-ingestion"></a><span data-ttu-id="d0406-105">Welche Optionen stehen Ihnen bei der Auswahl einer Technologie für die Echtzeiterfassung von Nachrichten zur Verfügung?</span><span class="sxs-lookup"><span data-stu-id="d0406-105">What are your options for real-time message ingestion?</span></span>

- [<span data-ttu-id="d0406-106">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0406-106">Azure Event Hubs</span></span>](/azure/event-hubs/)
- [<span data-ttu-id="d0406-107">Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d0406-107">Azure IoT Hub</span></span>](/azure/iot-hub/)
- [<span data-ttu-id="d0406-108">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0406-108">Kafka on HDInsight</span></span>](/azure/hdinsight/kafka/apache-kafka-get-started)

## <a name="azure-event-hubs"></a><span data-ttu-id="d0406-109">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0406-109">Azure Event Hubs</span></span>

<span data-ttu-id="d0406-110">[Azure Event Hubs](/azure/event-hubs/) ist eine hochgradig skalierbare Datenstreamingplattform und ein Dienst zur Erfassung von Ereignissen, der pro Sekunde Millionen von Ereignissen empfangen und verarbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="d0406-110">[Azure Event Hubs](/azure/event-hubs/) is a highly scalable data streaming platform and event ingestion service, capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="d0406-111">Event Hubs kann Ereignisse, Daten oder Telemetriedaten, die von verteilter Software und verteilten Geräten erzeugt wurden, verarbeiten und speichern.</span><span class="sxs-lookup"><span data-stu-id="d0406-111">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="d0406-112">An einen Event Hub gesendete Daten können transformiert und mit einem beliebigen Echtzeitanalyse-Anbieter oder Batchverarbeitungs-/Speicheradapter gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="d0406-112">Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="d0406-113">Event Hubs bietet Funktionen für das Veröffentlichen/Abonnieren in großem Umfang mit geringer Wartezeit und eignet sich daher für Big Data-Szenarien.</span><span class="sxs-lookup"><span data-stu-id="d0406-113">Event Hubs provides publish-subscribe capabilities with low latency at massive scale, which makes it appropriate for big data scenarios.</span></span>

## <a name="azure-iot-hub"></a><span data-ttu-id="d0406-114">Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d0406-114">Azure IoT Hub</span></span>

<span data-ttu-id="d0406-115">[Azure IoT Hub](/azure/iot-hub/) ist ein verwalteter Dienst, der eine zuverlässige und sichere bidirektionale Kommunikation zwischen Millionen von IoT-Geräten und einem cloudbasierten Back-End ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="d0406-115">[Azure IoT Hub](/azure/iot-hub/) is a managed service that enables reliable and secure bidirectional communications between millions of IoT devices and a cloud-based back end.</span></span>

<span data-ttu-id="d0406-116">IoT Hub bietet folgende Features:</span><span class="sxs-lookup"><span data-stu-id="d0406-116">Feature of IoT Hub include:</span></span>

* <span data-ttu-id="d0406-117">Mehrere Optionen für die Kommunikation zwischen Geräten und Cloud (Device-to-Cloud, D2C) sowie zwischen Cloud und Geräten (Cloud-to-Device, C2D).</span><span class="sxs-lookup"><span data-stu-id="d0406-117">Multiple options for device-to-cloud and cloud-to-device communication.</span></span> <span data-ttu-id="d0406-118">Dazu zählen unter anderem unidirektionales Messaging, Dateiübertragungen und Anforderung-Antwort-Methoden.</span><span class="sxs-lookup"><span data-stu-id="d0406-118">These options include one-way messaging, file transfer, and request-reply methods.</span></span>
* <span data-ttu-id="d0406-119">Nachrichtenrouting zu anderen Azure-Diensten.</span><span class="sxs-lookup"><span data-stu-id="d0406-119">Message routing to other Azure services.</span></span>
* <span data-ttu-id="d0406-120">Abfragbarer Speicher für Gerätemetadaten und synchronisierte Zustandsinformationen.</span><span class="sxs-lookup"><span data-stu-id="d0406-120">Queryable store for device metadata and synchronized state information.</span></span>
* <span data-ttu-id="d0406-121">Sichere Kommunikation und Zugriffssteuerung mithilfe von geräteabhängigen Sicherheitsschlüsseln oder X.509-Zertifikaten.</span><span class="sxs-lookup"><span data-stu-id="d0406-121">Scure communications and access control using per-device security keys or X.509 certificates.</span></span>
* <span data-ttu-id="d0406-122">Überwachung der Ereignisse zur Verwaltung der Gerätekonnektivität und -identität.</span><span class="sxs-lookup"><span data-stu-id="d0406-122">Monitoring of device connectivity and device identity management events.</span></span>

<span data-ttu-id="d0406-123">Im Hinblick auf die Erfassung von Nachrichten ist IoT Hub von der Funktion her mit Event Hubs vergleichbar.</span><span class="sxs-lookup"><span data-stu-id="d0406-123">In terms of message ingestion, IoT Hub is similar to Event Hubs.</span></span> <span data-ttu-id="d0406-124">IoT Hub wurde jedoch speziell für die Verwaltung der IoT-Gerätekonnektivität konzipiert und nicht nur für die Erfassung von Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="d0406-124">However, it was specifically designed for managing IoT device connectivity, not just message ingestion.</span></span> <span data-ttu-id="d0406-125">Weitere Informationen finden Sie unter [Vergleich zwischen Azure IoT Hub und Azure Event Hubs](/azure/iot-hub/iot-hub-compare-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="d0406-125">For more information, see [Comparison of Azure IoT Hub and Azure Event Hubs](/azure/iot-hub/iot-hub-compare-event-hubs).</span></span> 

## <a name="kafka-on-hdinsight"></a><span data-ttu-id="d0406-126">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0406-126">Kafka on HDInsight</span></span>

<span data-ttu-id="d0406-127">[Apache Kafka](https://kafka.apache.org/) ist eine verteilte Open Source-Streamingplattform, die zum Erstellen von Echtzeit-Datenpipelines und Streaminganwendungen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="d0406-127">[Apache Kafka](https://kafka.apache.org/) is an open-source distributed streaming platform that can be used to build real-time data pipelines and streaming applications.</span></span> <span data-ttu-id="d0406-128">Kafka verfügt auch über Nachrichtenbrokerfunktionen, die einer Nachrichtenwarteschlange ähneln, über die Sie benannte Datenströme veröffentlichen und diese abonnieren können.</span><span class="sxs-lookup"><span data-stu-id="d0406-128">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> <span data-ttu-id="d0406-129">Apache Kafka ist horizontal skalierbar, fehlertolerant und extrem schnell.</span><span class="sxs-lookup"><span data-stu-id="d0406-129">It is horizontally scalable, fault-tolerant, and extremely fast.</span></span> <span data-ttu-id="d0406-130">[Kafka in HDInsight](/azure/hdinsight/kafka/apache-kafka-get-started) stellt Kafka als verwalteten, hoch skalierbaren und hoch verfügbaren Dienst in Azure bereit.</span><span class="sxs-lookup"><span data-stu-id="d0406-130">[Kafka on HDInsight](/azure/hdinsight/kafka/apache-kafka-get-started) provides a Kafka as a managed, highly scalable, and highly available service in Azure.</span></span> 

<span data-ttu-id="d0406-131">Gängige Anwendungsfälle für Kafka sind beispielsweise:</span><span class="sxs-lookup"><span data-stu-id="d0406-131">Some common use cases for Kafka are:</span></span>

* <span data-ttu-id="d0406-132">**Messaging**:</span><span class="sxs-lookup"><span data-stu-id="d0406-132">**Messaging**.</span></span> <span data-ttu-id="d0406-133">Da das Veröffentlichen/Abonnieren-Nachrichtenmuster unterstützt wird, wird Kafka häufig als Nachrichtenbroker genutzt.</span><span class="sxs-lookup"><span data-stu-id="d0406-133">Because it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>
* <span data-ttu-id="d0406-134">**Aktivitätsüberwachung**.</span><span class="sxs-lookup"><span data-stu-id="d0406-134">**Activity tracking**.</span></span> <span data-ttu-id="d0406-135">Da Kafka die geordnete Protokollierung von Datensätzen unterstützt, kann die Anwendung zum Nachverfolgen und Neuerstellen von Aktivitäten verwendet werden (beispielsweise Benutzeraktionen auf einer Website).</span><span class="sxs-lookup"><span data-stu-id="d0406-135">Because Kafka provides in-order logging of records, it can be used to track and re-create activities, such as user actions on a web site.</span></span>
* <span data-ttu-id="d0406-136">**Aggregation**.</span><span class="sxs-lookup"><span data-stu-id="d0406-136">**Aggregation**.</span></span> <span data-ttu-id="d0406-137">Mit der Datenstromverarbeitung können Sie Informationen aus unterschiedlichen Datenströmen aggregieren, um die Informationen zu operativen Daten zu kombinieren und zu zentralisieren.</span><span class="sxs-lookup"><span data-stu-id="d0406-137">Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>
* <span data-ttu-id="d0406-138">**Transformation**.</span><span class="sxs-lookup"><span data-stu-id="d0406-138">**Transformation**.</span></span> <span data-ttu-id="d0406-139">Mit der Datenstromverarbeitung können Sie Daten aus mehreren Eingabethemen zu einem oder mehreren Ausgabethemen kombinieren und erweitern.</span><span class="sxs-lookup"><span data-stu-id="d0406-139">Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="key-selection-criteria"></a><span data-ttu-id="d0406-140">Wichtige Auswahlkriterien</span><span class="sxs-lookup"><span data-stu-id="d0406-140">Key selection criteria</span></span>

<span data-ttu-id="d0406-141">Beantworten Sie die folgenden Fragen, um die Auswahl einzuschränken:</span><span class="sxs-lookup"><span data-stu-id="d0406-141">To narrow the choices, start by answering these questions:</span></span>

- <span data-ttu-id="d0406-142">Benötigen Sie eine bidirektionale Kommunikation zwischen Ihren IoT-Geräten und Azure?</span><span class="sxs-lookup"><span data-stu-id="d0406-142">Do you need two-way communication between your IoT devices and Azure?</span></span> <span data-ttu-id="d0406-143">Wenn dies der Fall ist, ist IoT Hub für Sie die richtige Wahl.</span><span class="sxs-lookup"><span data-stu-id="d0406-143">If so, choose IoT Hub.</span></span>

- <span data-ttu-id="d0406-144">Müssen Sie den Zugriff für einzelne Geräte verwalten und in der Lage sein, den Zugriff auf ein bestimmtes Gerät zu widerrufen?</span><span class="sxs-lookup"><span data-stu-id="d0406-144">Do you need to manage access for individual devices and be able to revoke access to a specific device?</span></span> <span data-ttu-id="d0406-145">Wenn dies der Fall ist, ist IoT Hub für Sie die richtige Wahl.</span><span class="sxs-lookup"><span data-stu-id="d0406-145">If yes, choose IoT Hub.</span></span>

## <a name="capability-matrix"></a><span data-ttu-id="d0406-146">Funktionsmatrix</span><span class="sxs-lookup"><span data-stu-id="d0406-146">Capability matrix</span></span>

<span data-ttu-id="d0406-147">In den folgenden Tabellen sind die Hauptunterschiede der Funktionen zusammengefasst:</span><span class="sxs-lookup"><span data-stu-id="d0406-147">The following tables summarize the key differences in capabilities.</span></span> 

| | <span data-ttu-id="d0406-148">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d0406-148">IoT Hub</span></span> | <span data-ttu-id="d0406-149">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0406-149">Event Hubs</span></span> | <span data-ttu-id="d0406-150">Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0406-150">Kafka on HDInsight</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d0406-151">Cloud-zu-Gerät-Kommunikation</span><span class="sxs-lookup"><span data-stu-id="d0406-151">Cloud-to-device communications</span></span> | <span data-ttu-id="d0406-152">Ja</span><span class="sxs-lookup"><span data-stu-id="d0406-152">Yes</span></span> | <span data-ttu-id="d0406-153">Nein </span><span class="sxs-lookup"><span data-stu-id="d0406-153">No</span></span> | <span data-ttu-id="d0406-154">Nein </span><span class="sxs-lookup"><span data-stu-id="d0406-154">No</span></span> |
| <span data-ttu-id="d0406-155">Vom Gerät initiierter Dateiupload</span><span class="sxs-lookup"><span data-stu-id="d0406-155">Device-initiated file upload</span></span> | <span data-ttu-id="d0406-156">Ja</span><span class="sxs-lookup"><span data-stu-id="d0406-156">Yes</span></span> | <span data-ttu-id="d0406-157">Nein </span><span class="sxs-lookup"><span data-stu-id="d0406-157">No</span></span> | <span data-ttu-id="d0406-158">Nein </span><span class="sxs-lookup"><span data-stu-id="d0406-158">No</span></span> |
| <span data-ttu-id="d0406-159">Gerätestatusinformationen</span><span class="sxs-lookup"><span data-stu-id="d0406-159">Device state information</span></span> | [<span data-ttu-id="d0406-160">Gerätezwillinge</span><span class="sxs-lookup"><span data-stu-id="d0406-160">Device twins</span></span>](/azure/iot-hub/iot-hub-devguide-device-twins) | <span data-ttu-id="d0406-161">Nein </span><span class="sxs-lookup"><span data-stu-id="d0406-161">No</span></span> | <span data-ttu-id="d0406-162">Nein </span><span class="sxs-lookup"><span data-stu-id="d0406-162">No</span></span> |
| <span data-ttu-id="d0406-163">Protokollunterstützung</span><span class="sxs-lookup"><span data-stu-id="d0406-163">Protocol support</span></span> | <span data-ttu-id="d0406-164">MQTT, AMQP, HTTPS<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d0406-164">MQTT, AMQP, HTTPS <sup>1</sup></span></span> | <span data-ttu-id="d0406-165">AMQP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="d0406-165">AMQP, HTTPS</span></span> | [<span data-ttu-id="d0406-166">Kafka-Protokoll</span><span class="sxs-lookup"><span data-stu-id="d0406-166">Kafka Protocol</span></span>](https://cwiki.apache.org/confluence/display/KAFKA/A+Guide+To+The+Kafka+Protocol) |
| <span data-ttu-id="d0406-167">Sicherheit</span><span class="sxs-lookup"><span data-stu-id="d0406-167">Security</span></span> | <span data-ttu-id="d0406-168">Geräteabhängige Identität, widerrufbare Zugriffssteuerung</span><span class="sxs-lookup"><span data-stu-id="d0406-168">Per-device identity; revocable access control.</span></span> | <span data-ttu-id="d0406-169">Freigegebene Zugriffsrichtlinien, begrenzte Sperrung über Herausgeberrichtlinien</span><span class="sxs-lookup"><span data-stu-id="d0406-169">Shared access policies; limited revocation through publisher policies.</span></span> | <span data-ttu-id="d0406-170">Authentifizierung mit SASL, austauschbare Autorisierung, Unterstützung der Integration in externe Authentifizierungsdienste</span><span class="sxs-lookup"><span data-stu-id="d0406-170">Authentication using SASL; pluggable authorization; integration with external authentication services supported.</span></span> |

<span data-ttu-id="d0406-171">[1] Sie können auch das [Azure IoT-Protokollgateway](/azure/iot-hub/iot-hub-protocol-gateway) als benutzerdefiniertes Gateway verwenden, um die Protokollanpassung für IoT Hub zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="d0406-171">[1] You can also use [Azure IoT protocol gateway](/azure/iot-hub/iot-hub-protocol-gateway) as a custom gateway to enable protocol adaptation for IoT Hub.</span></span>

<span data-ttu-id="d0406-172">Weitere Informationen finden Sie unter [Vergleich zwischen Azure IoT Hub und Azure Event Hubs](/azure/iot-hub/iot-hub-compare-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="d0406-172">For more information, see [Comparison of Azure IoT Hub and Azure Event Hubs](/azure/iot-hub/iot-hub-compare-event-hubs).</span></span>