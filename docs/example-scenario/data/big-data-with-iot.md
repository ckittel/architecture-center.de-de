---
title: IoT und Datenanalyse in der Bauindustrie
description: Verwenden Sie IoT-Geräte und Datenanalysen für eine umfassende Verwaltung und den Betrieb bei Bauprojekten.
author: alexbuckgit
ms.date: 08/29/2018
ms.openlocfilehash: 7ab0de50b0eba1ab420e450f3408fe5dc45f04ac
ms.sourcegitcommit: b2a4eb132857afa70201e28d662f18458865a48e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2018
ms.locfileid: "48818495"
---
# <a name="iot-and-data-analytics-in-the-construction-industry"></a><span data-ttu-id="327eb-103">IoT und Datenanalyse in der Bauindustrie</span><span class="sxs-lookup"><span data-stu-id="327eb-103">IoT and data analytics in the construction industry</span></span>

<span data-ttu-id="327eb-104">Dieses Beispielszenario ist für Entwickler von Lösungen relevant, die Daten zahlreicher IoT-Geräte in eine umfassende Datenanalysearchitektur integrieren, um Entscheidungsprozesse zu verbessern und zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="327eb-104">This example scenario is relevant to organizations building solutions that integrate data from many IoT devices into a comprehensive data analysis architecture to improve and automate decision making.</span></span> <span data-ttu-id="327eb-105">Zu den möglichen Anwendungsbereichen zählen unter anderem die Baubranche, Bergbau und die Fertigungsbranche sowie andere Branchen, in denen große Datenmengen aus zahlreichen IoT-basierten Dateneingaben anfallen.</span><span class="sxs-lookup"><span data-stu-id="327eb-105">Potential applications include construction, mining, manufacturing, or other industry solutions involving large volumes of data from many IoT-based data inputs.</span></span>

<span data-ttu-id="327eb-106">In diesem Szenario stellt ein Baugerätehersteller Fahrzeuge, Messgeräte und Drohnen her, die mit IoT- und GPS-Technologien ausgestattet sind und Telemetriedaten generieren.</span><span class="sxs-lookup"><span data-stu-id="327eb-106">In this scenario, a construction equipment manufacturer builds vehicles, meters, and drones that use IoT and GPS technologies to emit telemetry data.</span></span> <span data-ttu-id="327eb-107">Das Unternehmen möchte seine Datenarchitektur modernisieren, um die Betriebsumgebung und den Zustand der Geräte besser überwachen zu können.</span><span class="sxs-lookup"><span data-stu-id="327eb-107">The company wants to modernize their data architecture to better monitor operating conditions and equipment health.</span></span> <span data-ttu-id="327eb-108">Eine Möglichkeit wäre, die alte Lösung des Unternehmens durch eine lokale Infrastruktur zu ersetzen. Dies wäre jedoch sehr aufwendig, und die neue Lösung wäre nicht ausreichend skalierbar, um das erwartete Datenvolumen zu bewältigen.</span><span class="sxs-lookup"><span data-stu-id="327eb-108">Replacing the company's legacy solution using on-premises infrastructure would be both time and labor intensive, and would not be able to scale sufficiently to handle the anticipated data volume.</span></span>

<span data-ttu-id="327eb-109">Das Unternehmen möchte eine cloudbasierte intelligente Lösung für die Baubranche aufbauen.</span><span class="sxs-lookup"><span data-stu-id="327eb-109">The company wants to build a cloud-based "smart construction" solution.</span></span> <span data-ttu-id="327eb-110">Diese Lösung soll umfassende Daten für eine Baustelle sammeln sowie den Betrieb und die Wartung der verschiedenen Baustellenkomponenten automatisieren.</span><span class="sxs-lookup"><span data-stu-id="327eb-110">It should gather a comprehensive set of data for a construction site and automate the operation and maintenance of the various elements of the site.</span></span> <span data-ttu-id="327eb-111">Das Unternehmen hat folgende Ziele:</span><span class="sxs-lookup"><span data-stu-id="327eb-111">The company's goals include:</span></span>

* <span data-ttu-id="327eb-112">Integrieren und Analysieren sämtlicher Baugeräte und Daten, um Standzeiten zu minimieren und Diebstählen vorzubeugen</span><span class="sxs-lookup"><span data-stu-id="327eb-112">Integrating and analyzing all construction site equipment and data to minimize equipment downtime and reduce theft.</span></span>
* <span data-ttu-id="327eb-113">Ermöglichen der Remotesteuerung und Automatisierung von Baugeräten, um die Auswirkungen des Arbeitskräftemangels zu kompensieren und langfristig die Anzahl der benötigten Arbeiter zu senken sowie schlechter ausgebildeten Arbeitern eine Chance zu geben</span><span class="sxs-lookup"><span data-stu-id="327eb-113">Remotely and automatically controlling construction equipment to mitigate the effects of a labor shortage, ultimately requiring fewer workers and enabling lower-skilled workers to succeed.</span></span>
* <span data-ttu-id="327eb-114">Senken der Betriebskosten und Arbeitsanforderungen für die zugrunde liegende Infrastruktur bei gleichzeitiger Erhöhung der Produktivität und Sicherheit</span><span class="sxs-lookup"><span data-stu-id="327eb-114">Minimizing the operating costs and labor requirements for the supporting infrastructure, while increasing productivity and safety.</span></span>
* <span data-ttu-id="327eb-115">Problemloses Skalieren der Infrastruktur zur Bewältigung eines höheren Telemetriedatenaufkommens</span><span class="sxs-lookup"><span data-stu-id="327eb-115">Easily scaling the infrastructure to support increases in telemetry data.</span></span>
* <span data-ttu-id="327eb-116">Einhalten aller relevanten gesetzlichen Vorgaben durch Bereitstellung von Ressourcen innerhalb des Landes, ohne die Verfügbarkeit des Systems zu beeinträchtigen</span><span class="sxs-lookup"><span data-stu-id="327eb-116">Complying with all relevant legal requirements by provisioning resources in-country without compromising system availability.</span></span>
* <span data-ttu-id="327eb-117">Verwenden von Open-Source-Software zur Maximierung der Investition in die aktuellen Kenntnisse der Arbeiter</span><span class="sxs-lookup"><span data-stu-id="327eb-117">Using open-source software to maximize the investment in workers' current skills.</span></span>

<span data-ttu-id="327eb-118">Durch die Verwendung verwalteter Azure-Dienste wie IoT Hub und HDInsight kann der Kunde schnell eine umfassende Lösung mit geringeren Betriebskosten aufbauen und bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="327eb-118">Using managed Azure services such as IoT Hub and HDInsight will allow the customer to rapidly build and deploy a comprehensive solution with a lower operating cost.</span></span> <span data-ttu-id="327eb-119">Sollten Sie noch weitere Datenanalyseanforderungen haben, sehen Sie sich die Liste mit den verfügbaren [vollständig verwalteten Datenanalysediensten in Azure][product-category] an.</span><span class="sxs-lookup"><span data-stu-id="327eb-119">If you have additional data analytics needs, you should review the list of available [fully managed data analytics services in Azure][product-category].</span></span>

## <a name="relevant-use-cases"></a><span data-ttu-id="327eb-120">Relevante Anwendungsfälle</span><span class="sxs-lookup"><span data-stu-id="327eb-120">Relevant use cases</span></span>

<span data-ttu-id="327eb-121">Diese Lösung eignet sich für Folgendes:</span><span class="sxs-lookup"><span data-stu-id="327eb-121">Consider this solution for the following use cases:</span></span>

* <span data-ttu-id="327eb-122">Bauwesen, Bergbau oder Herstellung von Baugeräten</span><span class="sxs-lookup"><span data-stu-id="327eb-122">Construction, mining, or equipment manufacturing scenarios</span></span>
* <span data-ttu-id="327eb-123">Sammlung umfangreicher Gerätedaten zur Speicherung und Analyse</span><span class="sxs-lookup"><span data-stu-id="327eb-123">Large-scale collection of device data for storage and analysis</span></span>
* <span data-ttu-id="327eb-124">Erfassung und Analyse umfangreicher Datasets</span><span class="sxs-lookup"><span data-stu-id="327eb-124">Ingestion and analysis of large datasets</span></span>

## <a name="architecture"></a><span data-ttu-id="327eb-125">Architektur</span><span class="sxs-lookup"><span data-stu-id="327eb-125">Architecture</span></span>

![Architektur für IoT und Datenanalyse in der Bauindustrie][architecture]

<span data-ttu-id="327eb-127">Die Daten durchlaufen die Lösung wie folgt:</span><span class="sxs-lookup"><span data-stu-id="327eb-127">The data flows through the solution as follows:</span></span>

1. <span data-ttu-id="327eb-128">Baugeräte sammeln Sensordaten und senden die resultierenden Baudaten in regelmäßigen Abständen an Webdienste mit Lastenausgleich, die in einem Cluster virtueller Azure-Computer gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-128">Construction equipment collects sensor data and sends the construction results data at regular intervals to load balanced web services hosted on a cluster of Azure virtual machines.</span></span>
2. <span data-ttu-id="327eb-129">Die benutzerdefinierten Webdienste erfassen die resultierenden Baudaten und speichern Sie in einem Apache Cassandra-Cluster, der ebenfalls auf virtuellen Azure-Computern basiert.</span><span class="sxs-lookup"><span data-stu-id="327eb-129">The custom web services ingest the construction results data and store it in an Apache Cassandra cluster also running on Azure virtual machines.</span></span>
3. <span data-ttu-id="327eb-130">Ein weiteres Dataset wird von IoT-Sensoren verschiedener Baugeräte gesammelt und an IoT Hub gesendet.</span><span class="sxs-lookup"><span data-stu-id="327eb-130">Another dataset is gathered by IoT sensors on various construction equipment and sent to IoT Hub.</span></span>
4. <span data-ttu-id="327eb-131">Die gesammelten Rohdaten werden von IoT Hub direkt an Azure Blob Storage gesendet und können sofort angezeigt und analysiert werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-131">Raw data collected is sent directly from IoT Hub to Azure blob storage and is immediately available for viewing and analysis.</span></span>
5. <span data-ttu-id="327eb-132">Über IoT Hub gesammelte Daten werden nahezu in Echtzeit durch einen Azure Stream Analytics-Auftrag verarbeitet und in einer Azure SQL-Datenbank gespeichert.</span><span class="sxs-lookup"><span data-stu-id="327eb-132">Data collected via IoT Hub is processed in near real time by an Azure Stream Analytics job and stored in an Azure SQL database.</span></span>
6. <span data-ttu-id="327eb-133">Über die Webanwendung „Smart Construction Cloud“ können Analysten und Endbenutzer Sensordaten und Bilder anzeigen und analysieren.</span><span class="sxs-lookup"><span data-stu-id="327eb-133">The Smart Construction Cloud web application is available to analysts and end users to view and analyze sensor data and imagery.</span></span> 
7. <span data-ttu-id="327eb-134">Batchaufträge werden bei Bedarf von Benutzern der Webanwendung initiiert.</span><span class="sxs-lookup"><span data-stu-id="327eb-134">Batch jobs are initiated on demand by users of the web application.</span></span> <span data-ttu-id="327eb-135">Der Batchauftrag wird in Apache Spark in HDInsight ausgeführt und analysiert neue Daten, die im Cassandra-Cluster gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="327eb-135">The batch job runs in Apache Spark on HDInsight and analyzes new data stored in the Cassandra cluster.</span></span> 

### <a name="components"></a><span data-ttu-id="327eb-136">Komponenten</span><span class="sxs-lookup"><span data-stu-id="327eb-136">Components</span></span>

* <span data-ttu-id="327eb-137">[IoT Hub](/azure/iot-hub/about-iot-hub) fungiert als zentraler Nachrichtenhub für die sichere bidirektionale Kommunikation mit gerätespezifischer Identität zwischen Cloudplattform, Baugeräten und anderen Baustellenkomponenten.</span><span class="sxs-lookup"><span data-stu-id="327eb-137">[IoT Hub](/azure/iot-hub/about-iot-hub) acts as a central message hub for secure bi-directional communication with per-device identity between the cloud platform and the construction equipment and other site elements.</span></span> <span data-ttu-id="327eb-138">IoT Hub kann schnell Daten für jedes Gerät sammeln, die dann in der Datenanalysepipeline erfasst werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-138">IoT Hub can rapidly collect data for each device for ingestion into the data analytics pipeline.</span></span> 
* <span data-ttu-id="327eb-139">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) ist eine Ereignisverarbeitungsengine, die große Datenmengen analysieren kann, die von Geräten und anderen Quellen gestreamt werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-139">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) is an event-processing engine that can analyze high volumes of data streaming from devices and other data sources.</span></span> <span data-ttu-id="327eb-140">Zur Identifizierung von Mustern und Beziehungen wird zudem das Extrahieren von Informationen aus Datenströmen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="327eb-140">It also supports extracting information from data streams to identify patterns and relationships.</span></span> <span data-ttu-id="327eb-141">In diesem Szenario erfasst und analysiert Stream Analytics Daten von IoT-Geräten und speichert die Ergebnisse in Azure SQL-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="327eb-141">In this scenario, Stream Analytics ingests and analyzes data from IoT devices and stores the results in Azure SQL Database.</span></span> 
* <span data-ttu-id="327eb-142">[Azure SQL-Datenbank](/azure/sql-database/sql-database-technical-overview) enthält die Ergebnisse der analysierten Daten von IoT-Geräten und Messgeräten. Diese können von Analysten und Benutzern über eine Azure-basierte Webanwendung angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-142">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) contains the results of analyzed data from IoT devices and meters, which can be viewed by analysts and users via an Azure-based Web application.</span></span> 
* <span data-ttu-id="327eb-143">[Blob Storage](/azure/storage/blobs/storage-blobs-introduction) speichert Bilddaten, die von den IoT Hub-Geräten erfasst wurden.</span><span class="sxs-lookup"><span data-stu-id="327eb-143">[Blob storage](/azure/storage/blobs/storage-blobs-introduction) stores image data gathered from the IoT hub devices.</span></span> <span data-ttu-id="327eb-144">Die Bilddaten können über die Webanwendung angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-144">The image data can be viewed via the web application.</span></span>
* <span data-ttu-id="327eb-145">[Traffic Manager](/azure/traffic-manager/traffic-manager-overview) steuert die Verteilung von Benutzerdatenverkehr für Dienstendpunkte in unterschiedlichen Azure-Regionen.</span><span class="sxs-lookup"><span data-stu-id="327eb-145">[Traffic Manager](/azure/traffic-manager/traffic-manager-overview) controls the distribution of user traffic for service endpoints in different Azure regions.</span></span>
* <span data-ttu-id="327eb-146">[Load Balancer](/azure/load-balancer/load-balancer-overview) verteilt Datenübermittlungen von Baugeräten auf die VM-basierten Webdienste, um eine hohe Verfügbarkeit zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="327eb-146">[Load Balancer](/azure/load-balancer/load-balancer-overview) distributes data submissions from construction equipment devices across the VM-based web services to provide high availability.</span></span>
* <span data-ttu-id="327eb-147">[Virtuelle Azure-Computer](/azure/virtual-machines) fungieren als Host für die Webdienste, die die resultierenden Baudaten empfangen und in der Apache Cassandra-Datenbank erfassen.</span><span class="sxs-lookup"><span data-stu-id="327eb-147">[Azure Virtual Machines](/azure/virtual-machines) host the web services that receive and ingest the construction results data into the Apache Cassandra database.</span></span>
* <span data-ttu-id="327eb-148">[Apache Cassandra](https://cassandra.apache.org) ist eine verteilte NoSQL-Datenbank zum Speichern von Baudaten, die später durch Apache Spark verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-148">[Apache Cassandra](https://cassandra.apache.org) is a distributed NoSQL database used to store construction data for later processing by Apache Spark.</span></span>
* <span data-ttu-id="327eb-149">[Web-Apps](/azure/app-service/app-service-web-overview) hostet die Endbenutzer-Webanwendung, mit der Quelldaten und Bilder abgefragt und angezeigt werden können.</span><span class="sxs-lookup"><span data-stu-id="327eb-149">[Web Apps](/azure/app-service/app-service-web-overview) hosts the end-user web application, which can be used to query and view source data and images.</span></span> <span data-ttu-id="327eb-150">Über die Anwendung können Benutzer auch Batchaufträge in Apache Spark initiieren.</span><span class="sxs-lookup"><span data-stu-id="327eb-150">Users can also initiate batch jobs in Apache Spark via the application.</span></span>
* <span data-ttu-id="327eb-151">[Apache Spark in HDInsight](/azure/hdinsight/spark/apache-spark-overview) unterstützt In-Memory-Verarbeitung, um die Leistung von Anwendungen bei der Analyse großer Datenmengen zu steigern.</span><span class="sxs-lookup"><span data-stu-id="327eb-151">[Apache Spark on HDInsight](/azure/hdinsight/spark/apache-spark-overview) supports in-memory processing to boost the performance of big-data analytic applications.</span></span> <span data-ttu-id="327eb-152">In diesem Szenario wird Spark verwendet, um komplexe Algorithmen für die in Apache Cassandra gespeicherten Daten auszuführen.</span><span class="sxs-lookup"><span data-stu-id="327eb-152">In this scenario, Spark is used to run complex algorithms over the data stored in Apache Cassandra.</span></span>


### <a name="alternatives"></a><span data-ttu-id="327eb-153">Alternativen</span><span class="sxs-lookup"><span data-stu-id="327eb-153">Alternatives</span></span>

* <span data-ttu-id="327eb-154">[Cosmos DB](/azure/cosmos-db/introduction) ist eine alternative NoSQL-Datenbanktechnologie.</span><span class="sxs-lookup"><span data-stu-id="327eb-154">[Cosmos DB](/azure/cosmos-db/introduction) is an alternative NoSQL database technology.</span></span> <span data-ttu-id="327eb-155">Cosmos DB bietet [Multimasterunterstützung auf globaler Ebene](/azure/cosmos-db/multi-region-writers) mit [mehreren klar definierten Konsistenzebenen](/azure/cosmos-db/consistency-levels), um verschiedenste Kundenanforderungen zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="327eb-155">Cosmos DB provides [multi-master support at global scale](/azure/cosmos-db/multi-region-writers) with [multiple well-defined consistency levels](/azure/cosmos-db/consistency-levels) to meet various customer requirements.</span></span> <span data-ttu-id="327eb-156">Darüber hinaus unterstützt Cosmos DB auch die [Cassandra-API](/azure/cosmos-db/cassandra-introduction).</span><span class="sxs-lookup"><span data-stu-id="327eb-156">It also supports the [Cassandra API](/azure/cosmos-db/cassandra-introduction).</span></span> 
* <span data-ttu-id="327eb-157">[Azure Databricks](/azure/azure-databricks/what-is-azure-databricks) ist eine Apache Spark-basierte Analyseplattform, die für Azure optimiert ist.</span><span class="sxs-lookup"><span data-stu-id="327eb-157">[Azure Databricks](/azure/azure-databricks/what-is-azure-databricks) is an Apache Spark-based analytics platform optimized for Azure.</span></span> <span data-ttu-id="327eb-158">Dank Azure-Integration ermöglicht sie die Einrichtung mit nur einem Klick und bietet optimierte Workflows sowie einen interaktiven Arbeitsbereich für die Zusammenarbeit.</span><span class="sxs-lookup"><span data-stu-id="327eb-158">It is integrated with Azure to provide one-click setup, streamlined workflows, and an interactive collaborative workspace.</span></span>
* <span data-ttu-id="327eb-159">[Data Lake Storage](/azure/storage/data-lake-storage) ist eine Alternative zu Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="327eb-159">[Data Lake Storage](/azure/storage/data-lake-storage) is an alternative to Blob storage.</span></span> <span data-ttu-id="327eb-160">Bei diesem Szenario war Data Lake Storage in der Zielregion nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="327eb-160">For this scenario, Data Lake Storage was not available in the targeted region.</span></span>
* <span data-ttu-id="327eb-161">[Web-Apps](/azure/app-service) kann auch zum Hosten der Webdienste für die Erfassung der resultierenden Baudaten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-161">[Web Apps](/azure/app-service) could also be used to host the web services for ingesting construction results data.</span></span>
* <span data-ttu-id="327eb-162">Für die Echtzeiterfassung von Nachrichten, Datenspeicherung, Datenstromverarbeitung und Speicherung von Analysedaten sowie für Analysen und Berichte stehen zahlreiche Technologieoptionen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="327eb-162">Many technology options are available for real-time message ingestion, data storage, stream processing, storage of analytical data, and analytics and reporting.</span></span> <span data-ttu-id="327eb-163">Eine Übersicht über diese Optionen, ihre Funktionen und wichtige Auswahlkriterien finden Sie im [Azure-Datenarchitekturleitfaden](/azure/architecture/data-guide) unter [Auswählen einer Technologie für die Echtzeiterfassung von Nachrichten in Azure](/azure/architecture/data-guide/technology-choices/real-time-ingestion).</span><span class="sxs-lookup"><span data-stu-id="327eb-163">For an overview of these options, their capabilities, and key selection criteria, see [Big data architectures: Real-time processing](/azure/architecture/data-guide/technology-choices/real-time-ingestion) in the [Azure Data Architecture Guide](/azure/architecture/data-guide).</span></span>

## <a name="considerations"></a><span data-ttu-id="327eb-164">Überlegungen</span><span class="sxs-lookup"><span data-stu-id="327eb-164">Considerations</span></span>

<span data-ttu-id="327eb-165">Die breite Verfügbarkeit von Azure-Regionen ist ein wichtiger Faktor für dieses Szenario.</span><span class="sxs-lookup"><span data-stu-id="327eb-165">The broad availability of Azure regions is an important factor for this scenario.</span></span> <span data-ttu-id="327eb-166">Die Verfügbarkeit mehrerer Regionen in einem einzelnen Land kann bei der Notfallwiederherstellung genutzt werden und ermöglicht gleichzeitig die Einhaltung vertraglicher Verpflichtungen sowie der Anforderungen von Strafverfolgungsbehörden.</span><span class="sxs-lookup"><span data-stu-id="327eb-166">Having more than one region in a single country can provide disaster recovery while also enabling compliance with contractual obligations and law enforcement requirements.</span></span> <span data-ttu-id="327eb-167">Die Hochgeschwindigkeitskommunikation zwischen Azure-Regionen ist ebenfalls ein wichtiger Faktor in diesem Szenario.</span><span class="sxs-lookup"><span data-stu-id="327eb-167">Azure's high-speed communication between regions is also an important factor in this scenario.</span></span>

<span data-ttu-id="327eb-168">Dank der Unterstützung von Open Source-Technologien durch Azure konnte der Kunde auf bereits vorhandene Kenntnisse seines Personals zurückgreifen.</span><span class="sxs-lookup"><span data-stu-id="327eb-168">Azure support for open-source technologies allowed the customer to take advantage of their existing workforce skills.</span></span> <span data-ttu-id="327eb-169">Im Vergleich zu einer lokalen Lösung kann der Kunde außerdem schneller neue Technologien einführen und von geringeren Kosten und einer geringeren Arbeitsauslastung profitieren.</span><span class="sxs-lookup"><span data-stu-id="327eb-169">The customer can also accelerate the adoption of new technologies with lower costs and operating workloads compared to an on-premises solution.</span></span> 

## <a name="pricing"></a><span data-ttu-id="327eb-170">Preise</span><span class="sxs-lookup"><span data-stu-id="327eb-170">Pricing</span></span>

<span data-ttu-id="327eb-171">Folgende Aspekte haben erheblichen Einfluss auf die Kosten für diese Lösung:</span><span class="sxs-lookup"><span data-stu-id="327eb-171">The following considerations will drive a substantial portion of the costs for this solution.</span></span>

* <span data-ttu-id="327eb-172">Die Kosten für virtuelle Azure-Computer steigen linear, wenn weitere Instanzen bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-172">Azure virtual machine costs will increase linearly as additional instances are provisioned.</span></span> <span data-ttu-id="327eb-173">Für virtuelle Computer mit aufgehobener Bereitstellung fallen nur Speicherkosten und keine Computekosten an.</span><span class="sxs-lookup"><span data-stu-id="327eb-173">Virtual machines that are deallocated will only incur storage costs, and not compute costs.</span></span> <span data-ttu-id="327eb-174">Diese Computer mit aufgehobener Zuordnung können bei entsprechend hohem Bedarf neu zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="327eb-174">These deallocated machines can then be reallocated when demand is high.</span></span>
* <span data-ttu-id="327eb-175">Die Kosten für [IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub) hängen von der Anzahl bereitgestellter IoT-Einheiten sowie vom gewählten Diensttarif ab, der wiederum die Anzahl der pro Tag und Einheit zulässigen Nachrichten bestimmt.</span><span class="sxs-lookup"><span data-stu-id="327eb-175">[IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub) costs are driven by the number of IoT units provisioned as well as the service tier chosen, which determines the number of messages per day per unit allowed.</span></span> 
* <span data-ttu-id="327eb-176">Die Kosten für [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics) hängen von der Anzahl von Streamingeinheiten ab, die für die Verarbeitung der Daten im Dienst erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="327eb-176">[Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics) is priced by the number of streaming units required to process the data into the service.</span></span>

## <a name="related-resources"></a><span data-ttu-id="327eb-177">Zugehörige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="327eb-177">Related resources</span></span>

<span data-ttu-id="327eb-178">In der [Kundengeschichte von Komatsu][customer-story] können Sie sich eine Implementierung einer ähnlichen Architektur ansehen.</span><span class="sxs-lookup"><span data-stu-id="327eb-178">To see an implementation of a similar architecture, read the [Komatsu customer story][customer-story].</span></span>

<span data-ttu-id="327eb-179">Einen Leitfaden für Big Data-Architekturen finden Sie im [Azure-Datenarchitekturleitfaden](/azure/architecture/data-guide).</span><span class="sxs-lookup"><span data-stu-id="327eb-179">Guidance for big data architectures is available in the [Azure Data Architecture Guide](/azure/architecture/data-guide).</span></span>

<!-- links -->
[product-category]: https://azure.microsoft.com/product-categories/analytics/
[customer-site]: https://home.komatsu/en/
[customer-story]: https://customers.microsoft.com/story/komatsu-manufacturing-azure-iot-hub-japan
[architecture]: ./media/architecture-big-data-with-iot.png