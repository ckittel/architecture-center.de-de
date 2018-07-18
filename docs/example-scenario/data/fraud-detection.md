---
title: Erweiterte Analysen und Betrugserkennung in Echtzeit
description: Bewährte Lösung zur Erkennung betrügerischer Aktivitäten in Echtzeit mithilfe von Azure Event Hubs und Stream Analytics.
author: alexbuckgit
ms.date: 07/05/2018
ms.openlocfilehash: cf375445b38b0ff7d6fbc400902d5e97b34b4fed
ms.sourcegitcommit: 5d99b195388b7cabba383c49a81390ac48f86e8a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/06/2018
ms.locfileid: "37891327"
---
# <a name="real-time-fraud-detection-on-azure"></a><span data-ttu-id="ac73d-103">Betrugserkennung in Echtzeit in Azure</span><span class="sxs-lookup"><span data-stu-id="ac73d-103">Real-time fraud detection on Azure</span></span>

<span data-ttu-id="ac73d-104">Dieses Beispielszenario ist relevant für Organisationen, die Daten in Echtzeit analysieren müssen, um betrügerische Transaktionen oder andere anomale Aktivitäten zu erkennen.</span><span class="sxs-lookup"><span data-stu-id="ac73d-104">This example scenario is relevant to organizations that need to analyze data in real-time to detect fraudulent transactions or other anomalous activity.</span></span>

<span data-ttu-id="ac73d-105">Ein mögliches Anwendungsgebiet ist etwa die Erkennung betrügerischer Kreditkartenaktivitäten oder Mobiltelefonanrufe.</span><span class="sxs-lookup"><span data-stu-id="ac73d-105">Potential applications include identifying fraudulent credit card activity or mobile phone calls.</span></span> <span data-ttu-id="ac73d-106">Bei herkömmlichen onlinebasierten Analysesystemen kann es mehrere Stunden dauern, bis die Daten transformiert und analysiert wurden, um anomale Aktivitäten zu erkennen.</span><span class="sxs-lookup"><span data-stu-id="ac73d-106">Traditional online analytical systems might take hours to transform and analyze the data to identify anomalous activity.</span></span>

<span data-ttu-id="ac73d-107">Mit den vollständig verwalteten Azure-Diensten wie Event Hubs und Stream Analytics müssen Unternehmen keine einzelnen Server verwalten und können gleichzeitig ihre Kosten senken und von der Erfahrung profitieren, über die Microsoft bei der cloudbasierten Datenerfassung sowie bei Analysen in Echtzeit verfügt.</span><span class="sxs-lookup"><span data-stu-id="ac73d-107">By using fully managed Azure services such as Event Hubs and Stream Analytics, companies can eliminate the need to manage individual servers, while reducing costs and leveraging Microsoft's expertise in cloud-scale data ingestion and real-time analytics.</span></span> <span data-ttu-id="ac73d-108">In diesem Szenario geht es speziell um die Erkennung betrügerischer Aktivitäten.</span><span class="sxs-lookup"><span data-stu-id="ac73d-108">This scenario specifically addresses the detection of fraudulent activity.</span></span> <span data-ttu-id="ac73d-109">Informationen zu anderen Datenanalysen finden Sie bei Bedarf in der Liste verfügbarer [Azure Analytics-Dienste][product-category].</span><span class="sxs-lookup"><span data-stu-id="ac73d-109">If you have other needs for data analytics, you should review the list of available [Azure Analytics services][product-category].</span></span>

<span data-ttu-id="ac73d-110">Dieses Beispiel ist Teil einer umfassenderen Datenverarbeitungsarchitektur und -strategie.</span><span class="sxs-lookup"><span data-stu-id="ac73d-110">This sample represents one part of a broader data processing architecture and strategy.</span></span> <span data-ttu-id="ac73d-111">Weitere Optionen für diesen Aspekt einer Gesamtarchitektur werden weiter unten in diesem Artikel erläutert.</span><span class="sxs-lookup"><span data-stu-id="ac73d-111">Other options for this aspect of an overall architecture are discussed later in this article.</span></span>
 
## <a name="potential-use-cases"></a><span data-ttu-id="ac73d-112">Mögliche Anwendungsfälle</span><span class="sxs-lookup"><span data-stu-id="ac73d-112">Potential use cases</span></span>

<span data-ttu-id="ac73d-113">Diese Lösung eignet sich für Folgendes:</span><span class="sxs-lookup"><span data-stu-id="ac73d-113">Consider this solution for the following use cases:</span></span>

* <span data-ttu-id="ac73d-114">Erkennen betrügerischer Mobiltelefonanrufe in Telekommunikationsszenarien</span><span class="sxs-lookup"><span data-stu-id="ac73d-114">Detecting fraudulent mobile-phone calls in telecommunications scenarios.</span></span>
* <span data-ttu-id="ac73d-115">Identifizieren betrügerischer Kreditkartentransaktionen für Banken</span><span class="sxs-lookup"><span data-stu-id="ac73d-115">Identifying fraudulent credit card transactions for banking institutions.</span></span>
* <span data-ttu-id="ac73d-116">Identifizieren betrügerischer Einkäufe in Einzelhandels- oder E-Commerce-Szenarien</span><span class="sxs-lookup"><span data-stu-id="ac73d-116">Identifying fraudulent purchases in retail or e-commerce scenarios.</span></span>

## <a name="architecture"></a><span data-ttu-id="ac73d-117">Architektur</span><span class="sxs-lookup"><span data-stu-id="ac73d-117">Architecture</span></span>

![Übersicht über die Architektur der Azure-Komponenten für eine Lösung zur Betrugserkennung in Echtzeit][architecture-diagram]

<span data-ttu-id="ac73d-119">Diese Lösung umfasst die Back-End-Komponenten einer Pipeline für Echtzeitanalysen.</span><span class="sxs-lookup"><span data-stu-id="ac73d-119">This solution covers the back-end components of a real-time analytics pipeline.</span></span> <span data-ttu-id="ac73d-120">Daten durchlaufen die Lösung wie folgt:</span><span class="sxs-lookup"><span data-stu-id="ac73d-120">Data flows through the solution as follows:</span></span>

1. <span data-ttu-id="ac73d-121">Metadaten von Mobiltelefonanrufen werden aus dem Quellsystem an eine Azure Event Hubs-Instanz gesendet.</span><span class="sxs-lookup"><span data-stu-id="ac73d-121">Mobile phone call metadata is sent from the source system to an Azure Event Hubs instance.</span></span> 
2. <span data-ttu-id="ac73d-122">Ein Stream Analytics-Auftrag wird gestartet, der Daten über die Event Hub-Quelle empfängt.</span><span class="sxs-lookup"><span data-stu-id="ac73d-122">A Stream Analytics job is started, which receives data via the event hub source.</span></span>
3. <span data-ttu-id="ac73d-123">Der Stream Analytics-Auftrag führt eine vordefinierte Abfrage aus, um den Eingabedatenstrom zu transformieren und auf der Grundlage eines Algorithmus für betrügerische Transaktionen zu analysieren.</span><span class="sxs-lookup"><span data-stu-id="ac73d-123">The Stream Analytics job runs a predefined query to transform the input stream and analyze it based on a fraudulent-transaction algorithm.</span></span> <span data-ttu-id="ac73d-124">Diese Abfrage verwendet ein rollierendes Fenster, um den Datenstrom in unterschiedliche Zeiteinheiten zu unterteilen.</span><span class="sxs-lookup"><span data-stu-id="ac73d-124">This query uses a tumbling window to segment the stream into distinct temporal units.</span></span>
4. <span data-ttu-id="ac73d-125">Der Stream Analytics-Auftrag schreibt den transformierten Datenstrom, der erkannte betrügerische Anrufe darstellt, in eine Ausgabesenke in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ac73d-125">The Stream Analytics job writes the transformed stream representing detected fraudulent calls to an output sink in Azure Blob storage.</span></span>

### <a name="components"></a><span data-ttu-id="ac73d-126">Komponenten</span><span class="sxs-lookup"><span data-stu-id="ac73d-126">Components</span></span>

* <span data-ttu-id="ac73d-127">[Azure Event Hubs][docs-event-hubs] ist eine Echtzeitstreaming-Plattform und ein Ereigniserfassungsdienst, der pro Sekunde Millionen von Ereignissen empfangen und verarbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="ac73d-127">[Azure Event Hubs][docs-event-hubs] is a real-time streaming platform and event ingestion service, capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="ac73d-128">Event Hubs kann Ereignisse, Daten oder Telemetriedaten, die von verteilter Software und verteilten Geräten erzeugt wurden, verarbeiten und speichern.</span><span class="sxs-lookup"><span data-stu-id="ac73d-128">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="ac73d-129">In dieser Lösung empfängt Event Hubs alle Anrufmetadaten, die auf betrügerische Aktivitäten analysiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="ac73d-129">In this solution, Event Hubs receives all phone call metadata to be analyzed for fraudulent activity.</span></span>
* <span data-ttu-id="ac73d-130">[Azure Stream Analytics][docs-stream-analytics] ist eine Ereignisverarbeitungsengine, die große Datenmengen analysieren kann, die von Geräten und anderen Quellen gestreamt werden.</span><span class="sxs-lookup"><span data-stu-id="ac73d-130">[Azure Stream Analytics][docs-stream-analytics] is an event-processing engine that can analyze high volumes of data streaming from devices and other data sources.</span></span> <span data-ttu-id="ac73d-131">Zur Identifizierung von Mustern und Beziehungen wird zudem das Extrahieren von Informationen aus Datenströmen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ac73d-131">It also supports extracting information from data streams to identify patterns and relationships.</span></span> <span data-ttu-id="ac73d-132">Diese Muster können weitere Downstreamaktionen auslösen.</span><span class="sxs-lookup"><span data-stu-id="ac73d-132">These patterns can trigger other downstream actions.</span></span> <span data-ttu-id="ac73d-133">In dieser Lösung transformiert Stream Analytics den Eingabedatenstrom aus Event Hubs, um betrügerische Anrufe zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="ac73d-133">In this solution, Stream Analytics transforms the input stream from Event Hubs to identify fraudulent calls.</span></span>
* <span data-ttu-id="ac73d-134">[Blob Storage][docs-blob-storage] wird in dieser Lösung zum Speichern der Ergebnisse des Stream Analytics-Auftrags verwendet.</span><span class="sxs-lookup"><span data-stu-id="ac73d-134">[Blob storage][docs-blob-storage] is used in this solution to store the results of the Stream Analytics job.</span></span>

## <a name="considerations"></a><span data-ttu-id="ac73d-135">Überlegungen</span><span class="sxs-lookup"><span data-stu-id="ac73d-135">Considerations</span></span>

### <a name="alternatives"></a><span data-ttu-id="ac73d-136">Alternativen</span><span class="sxs-lookup"><span data-stu-id="ac73d-136">Alternatives</span></span>

<span data-ttu-id="ac73d-137">Für Echtzeiterfassung von Nachrichten, Datenspeicherung, Datenstromverarbeitung und die Speicherung von Analysedaten sowie für Analysen und Berichte stehen zahlreiche Technologieoptionen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="ac73d-137">Many technology choices are available for real-time message ingestion, data storage, stream processing, storage of analytical data, and analytics and reporting.</span></span> <span data-ttu-id="ac73d-138">Eine Übersicht über diese Optionen, ihre Funktionen und wichtige Auswahlkriterien finden Sie im Azure-Datenarchitekturleitfaden unter [Auswählen einer Technologie für die Echtzeiterfassung von Nachrichten in Azure](/azure/architecture/data-guide/technology-choices/real-time-ingestion).</span><span class="sxs-lookup"><span data-stu-id="ac73d-138">For an overview of these options, their capabilities, and key selection criteria, see [Big data architectures: Real-time processing](/azure/architecture/data-guide/technology-choices/real-time-ingestion) in the Azure Data Architecture Guide.</span></span>

<span data-ttu-id="ac73d-139">Von verschiedenen Machine Learning-Diensten in Azure können zudem komplexere Algorithmen für die Betrugserkennung generiert werden.</span><span class="sxs-lookup"><span data-stu-id="ac73d-139">Additionally, more complex algorithms for fraud detection can be produced by various machine learning services in Azure.</span></span> <span data-ttu-id="ac73d-140">Eine Übersicht über diese Optionen finden Sie im [Azure-Datenarchitekturleitfaden](../../data-guide/index.md) unter [Auswählen einer Machine Learning-Technologie in Azure](/azure/architecture/data-guide/technology-choices/data-science-and-machine-learning).</span><span class="sxs-lookup"><span data-stu-id="ac73d-140">For an overview of these options, see [Technology choices for machine learning](/azure/architecture/data-guide/technology-choices/data-science-and-machine-learning) in the [Azure Data Architecture Guide](../../data-guide/index.md).</span></span>

### <a name="availability"></a><span data-ttu-id="ac73d-141">Verfügbarkeit</span><span class="sxs-lookup"><span data-stu-id="ac73d-141">Availability</span></span>

<span data-ttu-id="ac73d-142">Azure Monitor bietet einheitliche Benutzeroberflächen für die übergreifende Überwachung verschiedener Azure-Dienste.</span><span class="sxs-lookup"><span data-stu-id="ac73d-142">Azure Monitor provides unified user interfaces for monitoring across various Azure services.</span></span> <span data-ttu-id="ac73d-143">Weitere Informationen finden Sie unter [Überwachen von Azure-Anwendungen und -Ressourcen](/azure/monitoring-and-diagnostics/monitoring-overview).</span><span class="sxs-lookup"><span data-stu-id="ac73d-143">For more information, see [Monitoring in Microsoft Azure](/azure/monitoring-and-diagnostics/monitoring-overview).</span></span> <span data-ttu-id="ac73d-144">Event Hubs und Stream Analytics sind jeweils mit Azure Monitor verknüpft.</span><span class="sxs-lookup"><span data-stu-id="ac73d-144">Event Hubs and Stream Analytics are both integrated with Azure Monitor.</span></span> 

<span data-ttu-id="ac73d-145">Weitere Überlegungen zur Verfügbarkeit finden Sie im Azure Architecture Center in der [Checkliste für die Verfügbarkeit][availability].</span><span class="sxs-lookup"><span data-stu-id="ac73d-145">For other availability considerations, see the [availability checklist][availability] in the Azure Architecture Center.</span></span>

### <a name="scalability"></a><span data-ttu-id="ac73d-146">Skalierbarkeit</span><span class="sxs-lookup"><span data-stu-id="ac73d-146">Scalability</span></span>

<span data-ttu-id="ac73d-147">Die Komponenten dieser Lösung sind für die Erfassung mit Hyperskalierung sowie für hochgradig parallelisierte Echtzeitanalysen konzipiert.</span><span class="sxs-lookup"><span data-stu-id="ac73d-147">The components of this solution are designed for hyper-scale ingestion and massively parallel real-time analytics.</span></span> <span data-ttu-id="ac73d-148">Azure Event Hubs ist hochgradig skalierbar und kann pro Sekunde Millionen von Ereignissen mit geringer Wartezeit empfangen und verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="ac73d-148">Azure Event Hubs is highly scalable, capable of receiving and processing millions of events per second with low latency.</span></span>  <span data-ttu-id="ac73d-149">Event Hubs kann die Anzahl von Durchsatzeinheiten bei Bedarf [automatisch zentral hochskalieren](/azure/event-hubs/event-hubs-auto-inflate).</span><span class="sxs-lookup"><span data-stu-id="ac73d-149">Event Hubs can [automatically scale up](/azure/event-hubs/event-hubs-auto-inflate) the number of throughput units to meet usage needs.</span></span> <span data-ttu-id="ac73d-150">Azure Stream Analytics kann große Mengen von Streamingdaten aus zahlreichen Quellen analysieren.</span><span class="sxs-lookup"><span data-stu-id="ac73d-150">Azure Stream Analytics is capable of analyzing high volumes of streaming data from many sources.</span></span> <span data-ttu-id="ac73d-151">Sie können Stream Analytics zentral hochskalieren, indem Sie die Anzahl von [Streamingeinheiten](/azure/stream-analytics/stream-analytics-streaming-unit-consumption) erhöhen, die für die Ausführung Ihres Streamingauftrags zugeteilt sind.</span><span class="sxs-lookup"><span data-stu-id="ac73d-151">You can scale up Stream Analytics by increasing the number of [streaming units](/azure/stream-analytics/stream-analytics-streaming-unit-consumption) allocated to execute your streaming job.</span></span>

<span data-ttu-id="ac73d-152">Allgemeine Informationen zur Entwicklung skalierbarer Lösungen finden Sie im Azure Architecture Center in der [Checkliste für die Skalierbarkeit][scalability].</span><span class="sxs-lookup"><span data-stu-id="ac73d-152">For general guidance on designing scalable solutions, see the [scalability checklist][scalability] in the Azure Architecture Center.</span></span>

### <a name="security"></a><span data-ttu-id="ac73d-153">Sicherheit</span><span class="sxs-lookup"><span data-stu-id="ac73d-153">Security</span></span>

<span data-ttu-id="ac73d-154">Azure Event Hubs verwendet zum Schutz der Daten ein [Authentifizierungs- und Sicherheitsmodell][docs-event-hubs-security-model], das auf einer Kombination aus SAS-Token (Shared Access Signature) und Ereignisherausgebern basiert.</span><span class="sxs-lookup"><span data-stu-id="ac73d-154">Azure Event Hubs secures data through an [authentication and security model][docs-event-hubs-security-model] based on a combination of Shared Access Signature (SAS) tokens and event publishers.</span></span> <span data-ttu-id="ac73d-155">Ein Ereignisherausgeber definiert einen virtuellen Endpunkt für einen Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ac73d-155">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="ac73d-156">Der Herausgeber kann nur zum Senden von Nachrichten an einen Event Hub verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ac73d-156">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="ac73d-157">Es ist nicht möglich, von einem Herausgeber Nachrichten zu empfangen.</span><span class="sxs-lookup"><span data-stu-id="ac73d-157">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="ac73d-158">Allgemeine Informationen zur Entwicklung sicherer Lösungen finden Sie in der [Dokumentation zur Azure-Sicherheit][security].</span><span class="sxs-lookup"><span data-stu-id="ac73d-158">For general guidance on designing secure solutions, see the [Azure Security Documentation][security].</span></span>

### <a name="resiliency"></a><span data-ttu-id="ac73d-159">Resilienz</span><span class="sxs-lookup"><span data-stu-id="ac73d-159">Resiliency</span></span>

<span data-ttu-id="ac73d-160">Allgemeine Informationen zur Entwicklung robuster Lösungen finden Sie unter [Entwerfen robuster Anwendungen für Azure][resiliency].</span><span class="sxs-lookup"><span data-stu-id="ac73d-160">For general guidance on designing resilient solutions, see [Designing resilient applications for Azure][resiliency].</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="ac73d-161">Bereitstellen der Lösung</span><span class="sxs-lookup"><span data-stu-id="ac73d-161">Deploy the solution</span></span>

<span data-ttu-id="ac73d-162">In [diesem Tutorial][tutorial] erfahren Sie Schritt für Schritt, wie Sie die einzelnen Komponenten der Lösung bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="ac73d-162">To deploy this solution, you can follow this [step-by-step tutorial][tutorial] demonstrating how to manually deploy each component of the solution.</span></span> <span data-ttu-id="ac73d-163">Das Tutorial beinhaltet auch eine .NET-Clientanwendung, mit der Sie exemplarische Anrufmetadaten generieren und an eine Event Hub-Instanz senden können.</span><span class="sxs-lookup"><span data-stu-id="ac73d-163">This tutorial also provides a .NET client application to generate sample phone call metadata and send that data to an event hub instance.</span></span> 

## <a name="pricing"></a><span data-ttu-id="ac73d-164">Preise</span><span class="sxs-lookup"><span data-stu-id="ac73d-164">Pricing</span></span>

<span data-ttu-id="ac73d-165">Zur Ermittlung der Betriebskosten für diese Lösung sind alle Dienste im Kostenrechner vorkonfiguriert.</span><span class="sxs-lookup"><span data-stu-id="ac73d-165">To explore the cost of running this solution, all of the services are pre-configured in the cost calculator.</span></span> <span data-ttu-id="ac73d-166">Wenn Sie wissen möchten, welche Kosten für Ihren spezifischen Anwendungsfall entstehen, passen Sie die entsprechenden Variablen an Ihre voraussichtliche Datenmenge an.</span><span class="sxs-lookup"><span data-stu-id="ac73d-166">To see how the pricing would change for your particular use case, change the appropriate variables to match your expected data volume.</span></span>

<span data-ttu-id="ac73d-167">Auf der Grundlage des zu erwartenden Datenverkehrsaufkommens haben wir drei exemplarische Kostenprofile erstellt:</span><span class="sxs-lookup"><span data-stu-id="ac73d-167">We have provided three sample cost profiles based on amount of traffic you expect to get:</span></span>

* <span data-ttu-id="ac73d-168">[Klein:][small-pricing] Verarbeitung von einer Million Ereignissen über eine einzelne Standardstreamingeinheit pro Monat.</span><span class="sxs-lookup"><span data-stu-id="ac73d-168">[Small][small-pricing]: process one million events through one standard streaming unit per month.</span></span>
* <span data-ttu-id="ac73d-169">[Mittel:][medium-pricing] Verarbeitung von 100 Millionen Ereignissen über fünf Standardstreamingeinheiten pro Monat.</span><span class="sxs-lookup"><span data-stu-id="ac73d-169">[Medium][medium-pricing]: process 100M events through five standard streaming units per month.</span></span>
* <span data-ttu-id="ac73d-170">[Groß:][large-pricing] Verarbeitung von 999 Millionen Ereignissen über 20 Standardstreamingeinheiten pro Monat.</span><span class="sxs-lookup"><span data-stu-id="ac73d-170">[Large][large-pricing]: process 999 million events through 20 standard streaming units per month.</span></span>

## <a name="related-resources"></a><span data-ttu-id="ac73d-171">Zugehörige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ac73d-171">Related resources</span></span>

<span data-ttu-id="ac73d-172">Bei komplexeren Betrugserkennungsszenarien kann die Verwendung eines Machine Learning-Modells von Vorteil sein.</span><span class="sxs-lookup"><span data-stu-id="ac73d-172">More complex fraud detection scenarios can benefit from a machine learning model.</span></span> <span data-ttu-id="ac73d-173">Informationen zu Lösungen mit Machine Learning Server finden Sie unter [Fraud Detection][r-server-fraud-detection] (Betrugserkennung).</span><span class="sxs-lookup"><span data-stu-id="ac73d-173">For solutions built using Machine Learning Server, see [Fraud detection using Machine Learning Server][r-server-fraud-detection].</span></span> <span data-ttu-id="ac73d-174">Weitere Lösungsvorlagen mit Machine Learning Server finden Sie unter [Solution templates for Machine Learning Server and Microsoft R Server 9.1/9.2][docs-r-server-sample-solutions] (Lösungsvorlagen für Machine Learning Server und Microsoft R Server 9.1/9.2).</span><span class="sxs-lookup"><span data-stu-id="ac73d-174">For other solution templates using Machine Learning Server, see [Data science scenarios and solution templates][docs-r-server-sample-solutions].</span></span> <span data-ttu-id="ac73d-175">Eine Beispiellösung mit Azure Data Lake Analytics finden Sie unter [Using Azure Data Lake and R for Fraud Detection][technet-fraud-detection] (Verwenden von Azure Data Lake und R für die Betrugserkennung).</span><span class="sxs-lookup"><span data-stu-id="ac73d-175">For an example solution using Azure Data Lake Analytics, see [Using Azure Data Lake and R for Fraud Detection][technet-fraud-detection].</span></span>  

<!-- links -->
[product-category]: https://azure.microsoft.com/product-categories/analytics/
[tutorial]: /azure/stream-analytics/stream-analytics-real-time-fraud-detection
[small-pricing]: https://azure.com/e/74149ec312c049ccba79bfb3cfa67606
[medium-pricing]: https://azure.com/e/4fc94f7376de484d8ae67a6958cae60a
[large-pricing]: https://azure.com/e/7da8804396f9428a984578700003ba42
[architecture-diagram]: ./images/architecture-diagram-fraud-detection.png
[docs-event-hubs]: /azure/event-hubs/event-hubs-what-is-event-hubs
[docs-event-hubs-security-model]: /azure/event-hubs/event-hubs-authentication-and-security-model-overview
[docs-stream-analytics]: /azure/stream-analytics/stream-analytics-introduction
[docs-blob-storage]: /azure/storage/blobs/storage-blobs-introduction
[docs-r-server-sample-solutions]: /machine-learning-server/r/sample-solutions
[r-server-fraud-detection]: https://microsoft.github.io/r-server-fraud-detection/
[technet-fraud-detection]: https://blogs.technet.microsoft.com/machinelearning/2017/06/28/using-azure-data-lake-and-r-for-fraud-detection/
[availability]: /azure/architecture/checklist/availability
[scalability]: /azure/architecture/checklist/scalability
[resiliency]: ../../resiliency/index.md
[security]: /azure/security/
