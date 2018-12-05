---
title: ETL-Hybridvorgänge mit vorhandenen lokalen SSIS-Bereitstellungen und Azure Data Factory
description: ETL-Hybridvorgänge mit vorhandenen lokalen SSIS-Bereitstellungen (SQL Server Integration Services) und Azure Data Factory
author: alhieng
ms.date: 9/20/2018
ms.openlocfilehash: c4c0cfd63ef1d6c620eb36e16622ad9ffb7b5d80
ms.sourcegitcommit: 16bc6a91b6b9565ca3bcc72d6eb27c2c4ae935e4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52579462"
---
# <a name="hybrid-etl-with-existing-on-premises-ssis-and-azure-data-factory"></a><span data-ttu-id="bb9f5-103">ETL-Hybridvorgänge mit vorhandenen lokalen SSIS-Bereitstellungen und Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bb9f5-103">Hybrid ETL with existing on-premises SSIS and Azure Data Factory</span></span>

<span data-ttu-id="bb9f5-104">Organisationen, die ihre SQL Server-Datenbanken in die Cloud migrieren, können von erheblichen Kosteneinsparungen und Leistungszuwächsen sowie von einer höheren Flexibilität und einer besseren Skalierbarkeit profitieren.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-104">Organizations that migrate their SQL Server databases to the cloud can realize tremendous cost savings, performance gains, added flexibility, and greater scalability.</span></span> <span data-ttu-id="bb9f5-105">Die Überarbeitung bereits vorhandener ETL-Prozesse (Extrahieren, Transformieren und Laden), die mit SQL Server Integration Services (SSIS) erstellt wurden, kann sich jedoch als Migrationshindernis erweisen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-105">However, reworking existing extract, transform, and load (ETL) processes built with SQL Server Integration Services (SSIS) can be a migration roadblock.</span></span> <span data-ttu-id="bb9f5-106">In anderen Fällen erfordert der Prozess zum Laden von Daten eine komplexe Logik und/oder bestimmte Datentoolkomponenten, die noch nicht von Azure Data Factory v2 (ADF) unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-106">In other cases, the data load process requires complex logic and/or specific data tool components that are not yet supported by Azure Data Factory v2 (ADF).</span></span> <span data-ttu-id="bb9f5-107">Häufig werden SSIS-Funktionen wie Transformationen für Fuzzysuche und Fuzzygruppierung, CDC (Change Data Capture), SCD (Slowly Changing Dimensions) und DQS (Data Quality Services) verwendet.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-107">Commonly used SSIS capabilities include Fuzzy Lookup and Fuzzy Grouping transformations, Change Data Capture (CDC), Slowly Changing Dimensions (SCD), and Data Quality Services (DQS).</span></span>

<span data-ttu-id="bb9f5-108">Für die Lift & Shift-Migration einer vorhandenen SQL-Datenbank empfiehlt sich unter Umständen die Verwendung eines ETL-Hybridansatzes.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-108">To facilitate a lift-and-shift migration of an existing SQL database, a hybrid ETL approach may be the most suitable option.</span></span> <span data-ttu-id="bb9f5-109">Ein Hybridansatz verwendet zwar ADF als primäre Orchestrierungsengine, nutzt aber weiterhin vorhandene SSIS-Pakete für die Bereinigung von Daten und die Verwendung lokaler Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-109">A hybrid approach uses ADF as the primary orchestration engine, but continues to leverage existing SSIS packages to clean data and work with on-premise resources.</span></span> <span data-ttu-id="bb9f5-110">Dieser Ansatz verwendet die ADF-basierte SQL Server-IR (Integration Runtime), um eine Lift & Shift-Migration vorhandener Datenbanken in die Cloud zu ermöglichen, und nutzt dabei bereits vorhandenen Code und vorhandene SSIS-Pakete.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-110">This approach uses the ADF SQL Server Integrated Runtime (IR) to enable a lift-and-shift of existing databases into the cloud, while using existing code and SSIS packages.</span></span>

<span data-ttu-id="bb9f5-111">Dieses Beispielszenario ist für Organisationen relevant, die Datenbanken in die Cloud verschieben und die Verwendung von ADF als primäre cloudbasierte ETL-Engine in Betracht ziehen, während sie vorhandene SSIS-Pakete in ihren neuen Clouddatenworkflow integrieren.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-111">This example scenario is relevant to organizations that are moving databases to the cloud and are considering using ADF as their primary cloud-based ETL engine while incorporating existing SSIS packages into their new cloud data workflow.</span></span> <span data-ttu-id="bb9f5-112">Viele Organisationen haben stark in die Entwicklung von SSIS-ETL-Paketen für bestimmte Datenaufgaben investiert.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-112">Many organizations have significant invested in developing SSIS ETL packages for specific data tasks.</span></span> <span data-ttu-id="bb9f5-113">Die Vorstellung, diese Pakete umschreiben zu müssen, kann durchaus abschreckend sein.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-113">Rewriting these packages can be daunting.</span></span> <span data-ttu-id="bb9f5-114">Darüber hinaus sind viele vorhandene Codepakete von lokalen Ressourcen abhängig, was eine Migration in die Cloud verhindert.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-114">Also, many existing code packages have dependencies on local resources, preventing migration to the cloud.</span></span>

<span data-ttu-id="bb9f5-115">Mit ADF können Kunden ihre bereits vorhandenen ETL-Pakete nutzen und weitere Investitionen in die lokale ETL-Entwicklung zurückfahren.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-115">ADF lets customers take advantage of their existing ETL packages while limiting further investment in on-premises ETL development.</span></span> <span data-ttu-id="bb9f5-116">In diesem Beispiel werden mögliche Anwendungsfälle für die Nutzung vorhandener SSIS-Pakete im Rahmen eines neuen Clouddatenworkflows mit Azure Data Factory v2 erläutert.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-116">This example discusses potential use cases for leveraging existing SSIS packages as part of a new cloud data workflow using Azure Data Factory v2.</span></span>

## <a name="potential-use-cases"></a><span data-ttu-id="bb9f5-117">Mögliche Anwendungsfälle</span><span class="sxs-lookup"><span data-stu-id="bb9f5-117">Potential use cases</span></span>

<span data-ttu-id="bb9f5-118">In der Vergangenheit war SSIS für viele SQL Server-Datenexperten das bevorzugte ETL-Tool für Datentransformationen und -ladevorgänge.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-118">Traditionally, SSIS has been the ETL tool of choice for many SQL Server data professionals for data transformation and loading.</span></span> <span data-ttu-id="bb9f5-119">Gelegentlich wurden bestimmte SSIS-Features oder Plug-In-Komponenten von Drittanbietern verwendet, um die Entwicklung voranzutreiben.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-119">Sometimes, specific SSIS features or third-party plugging components have been used to accelerate the development effort.</span></span> <span data-ttu-id="bb9f5-120">Kommt ein Austausch oder eine Neuentwicklung dieser Pakete nicht in Frage, können Kunden ihre Datenbanken nicht in die Cloud migrieren.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-120">Replacement or redevelopment of these packages may not be an option, which prevents customers from migrating their databases to the cloud.</span></span> <span data-ttu-id="bb9f5-121">Kunden suchen daher nach Möglichkeiten, wie sie ihre vorhandenen Datenbanken möglichst effizient in die Cloud migrieren und ihre vorhandenen SSIS-Pakete weiter verwenden können.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-121">Customers are looking for low impact approaches to migrating their existing databases to the cloud and taking advantage of their existing SSIS packages.</span></span>

<span data-ttu-id="bb9f5-122">Im Anschluss finden Sie einige potenzielle lokale Anwendungsfälle:</span><span class="sxs-lookup"><span data-stu-id="bb9f5-122">Several potential on-premises use cases are listed below:</span></span>

* <span data-ttu-id="bb9f5-123">Laden von Netzwerkrouterprotokollen in eine Datenbank zu Analysezwecken</span><span class="sxs-lookup"><span data-stu-id="bb9f5-123">Loading network router logs to a database for analysis.</span></span>
* <span data-ttu-id="bb9f5-124">Vorbereiten von Beschäftigungsdaten der Personalabteilung für Analyseberichte</span><span class="sxs-lookup"><span data-stu-id="bb9f5-124">Preparing human resources employment data for analytical reporting.</span></span>
* <span data-ttu-id="bb9f5-125">Laden von Produkt- und Vertriebsdaten in ein Data Warehouse, um Umsatzprognosen zu erstellen</span><span class="sxs-lookup"><span data-stu-id="bb9f5-125">Loading product and sales data into a data warehouse for sales forecasting.</span></span>
* <span data-ttu-id="bb9f5-126">Automatisieren von Ladevorgängen oder betrieblichen Datenspeichern oder Data Warehouses für das Finanz- und Rechnungswesen</span><span class="sxs-lookup"><span data-stu-id="bb9f5-126">Automating loading or operational data stores or data warehouses for finance and accounting.</span></span>

## <a name="architecture"></a><span data-ttu-id="bb9f5-127">Architektur</span><span class="sxs-lookup"><span data-stu-id="bb9f5-127">Architecture</span></span>

![Übersicht über die Architektur eines ETL-Hybridprozesses mit Azure Data Factory][architecture-diagram]

1. <span data-ttu-id="bb9f5-129">Daten werden aus dem Blobspeicher in Data Factory gelesen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-129">Data is sourced from Blob storage into Data Factory.</span></span>
2. <span data-ttu-id="bb9f5-130">Die Data Factory-Pipeline ruft eine gespeicherte Prozedur auf, um einen lokal gehosteten SSIS-Auftrag über die Integrated Runtime auszuführen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-130">The Data Factory pipeline invokes a stored procedure to execute an SSIS job hosted on-premises via the Integrated Runtime.</span></span>
3. <span data-ttu-id="bb9f5-131">Die Datenbereinigungsaufträge werden ausgeführt, um die Daten für die Downstreamnutzung vorzubereiten.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-131">The data cleansing jobs are executed to prepare the data for downstream consumption.</span></span>
4. <span data-ttu-id="bb9f5-132">Nach erfolgreicher Datenbereinigung werden die bereinigten Daten mithilfe einer Kopieraufgabe in Azure geladen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-132">Once the data cleansing task completes successfully, a copy task is executed to load the clean data into Azure.</span></span>
5. <span data-ttu-id="bb9f5-133">Danach werden die bereinigten Daten in Tabellen in SQL Data Warehouse geladen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-133">The clean data is then loaded into tables in the SQL Data Warehouse.</span></span>

### <a name="components"></a><span data-ttu-id="bb9f5-134">Komponenten</span><span class="sxs-lookup"><span data-stu-id="bb9f5-134">Components</span></span>

* <span data-ttu-id="bb9f5-135">[Blobspeicher][docs-blob-storage] wird als Dateispeicher sowie als Datenquelle für Data Factory verwendet.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-135">[Blob storage][docs-blob-storage] is used to store files and as a source for Data Factory to retrieve data.</span></span>
* <span data-ttu-id="bb9f5-136">[SQL Server Integration Services][docs-ssis] enthält die lokalen ETL-Pakete für die Ausführung aufgabenspezifischer Workloads.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-136">[SQL Server Integration Services][docs-ssis] contains the on-premises ETL packages used to execute task-specific workloads.</span></span>
* <span data-ttu-id="bb9f5-137">[Azure Data Factory][docs-data-factory] ist die Cloudorchestrierungsengine, die Daten aus mehreren Quellen miteinander kombiniert, orchestriert und in ein Data Warehouse lädt.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-137">[Azure Data Factory][docs-data-factory] is the cloud orchestration engine that takes data from multiple sources and combines, orchestrates, and loads the data into a data warehouse.</span></span>
* <span data-ttu-id="bb9f5-138">[SQL Data Warehouse][docs-sql-data-warehouse] zentralisiert Daten in der Cloud, sodass über standardmäßige ANSI-SQL-Abfragen problemlos auf sie zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-138">[SQL Data Warehouse][docs-sql-data-warehouse] centralizes data in the cloud for easy access using standard ANSI SQL queries.</span></span>

### <a name="alternatives"></a><span data-ttu-id="bb9f5-139">Alternativen</span><span class="sxs-lookup"><span data-stu-id="bb9f5-139">Alternatives</span></span>

<span data-ttu-id="bb9f5-140">Data Factory kann auch Datenbereinigungsprozeduren aufrufen, die mit anderen Technologien (etwa mit einem Databricks-Notebook, einem Python-Skript oder einer auf einem virtuellen Computer ausgeführten SSIS-Instanz) implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-140">Data Factory could invoke data cleansing procedures implemented using other technologies, such as a Databricks notebook, Python script, or SSIS instance running in a virtual machine.</span></span> <span data-ttu-id="bb9f5-141">Eine mögliche Alternative zum Hybridansatz ist das [Installieren kostenpflichtiger oder lizenzierter benutzerdefinierter Komponenten für Azure-SSIS Integration Runtime](/azure/data-factory/how-to-develop-azure-ssis-ir-licensed-components).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-141">[Installing paid or licensed custom components for the Azure-SSIS integration runtime](/azure/data-factory/how-to-develop-azure-ssis-ir-licensed-components) may be a viable alternative to the hybrid approach.</span></span>

## <a name="considerations"></a><span data-ttu-id="bb9f5-142">Überlegungen</span><span class="sxs-lookup"><span data-stu-id="bb9f5-142">Considerations</span></span>

<span data-ttu-id="bb9f5-143">Die Integrated Runtime (IR) unterstützt zwei Modelle: selbstgehostet und von Azure gehostet.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-143">The Integrated Runtime (IR) supports two models: self-hosted IR or Azure-hosted IR.</span></span> <span data-ttu-id="bb9f5-144">Sie müssen sich zunächst für eine dieser beiden Optionen entscheiden.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-144">You first must decide between these two options.</span></span> <span data-ttu-id="bb9f5-145">Die selbstgehostete Variante ist kostengünstiger, aber auch mit einem höheren Wartungs- und Verwaltungsaufwand verbunden.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-145">Self-hosting is more cost effective but has more overhead for maintenance and management.</span></span> <span data-ttu-id="bb9f5-146">Weitere Informationen finden Sie unter [Selbstgehostete Integrationslaufzeit](/azure/data-factory/concepts-integration-runtime#self-hosted-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-146">For more information, see [Self-hosted IR](/azure/data-factory/concepts-integration-runtime#self-hosted-integration-runtime).</span></span> <span data-ttu-id="bb9f5-147">Eine Entscheidungshilfe für die Wahl der passenden IR finden Sie bei Bedarf unter [Ermitteln der richtigen Integrationslaufzeit](/azure/data-factory/concepts-integration-runtime#determining-which-ir-to-use).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-147">If you need help determining which IR to use, see [Determining which IR to use](/azure/data-factory/concepts-integration-runtime#determining-which-ir-to-use).</span></span>

<span data-ttu-id="bb9f5-148">Bei Verwendung der von Azure gehosteten Variante müssen Sie entscheiden, wie viel Leistung für die Verarbeitung Ihrer Daten erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-148">For the Azure-hosted approach, you should decide how much power is required to process your data.</span></span> <span data-ttu-id="bb9f5-149">Bei der von Azure gehosteten Konfiguration können Sie im Rahmen der Konfigurationsschritte die VM-Größe auswählen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-149">The Azure-hosted configuration allows you to select the VM size as part of the configuration steps.</span></span> <span data-ttu-id="bb9f5-150">Weitere Informationen zum Auswählen von VM-Größen finden Sie unter [Überlegungen zur Leistung](/azure/cloud-services/cloud-services-sizes-specs#performance-considerations).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-150">To learn more about selecting VM sizes, see [VM performance considerations](/azure/cloud-services/cloud-services-sizes-specs#performance-considerations).</span></span>

<span data-ttu-id="bb9f5-151">Die Entscheidung wird deutlich einfacher, wenn Sie bereits über SSIS-Pakete mit lokalen Abhängigkeiten verfügen (beispielsweise Datenquellen oder Dateien, auf die nicht von Azure aus zugegriffen werden kann).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-151">The decision is much easier when you already have existing SSIS packages that have on-premise dependencies such as data sources or files that are not accessible from Azure.</span></span> <span data-ttu-id="bb9f5-152">In diesem Fall kommt nur die selbstgehostete IR in Frage.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-152">In this scenario, your only option is the self-hosted IR.</span></span> <span data-ttu-id="bb9f5-153">Dieser Ansatz ist am flexibelsten und ermöglicht es, die Cloud als Orchestrierungsengine zu nutzen, ohne vorhandene Pakete umschreiben zu müssen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-153">This approach provides the most flexibility to leverage the cloud as the orchestration engine, without having to rewrite existing packages.</span></span>

<span data-ttu-id="bb9f5-154">Letztendlich geht es darum, die verarbeiteten Daten zur weiteren Optimierung in die Cloud zu laden oder mit anderen in der Cloud gespeicherten Daten zu kombinieren.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-154">Ultimately, the intent is to move the processed data into the cloud for further refinement or combining with other data stored in the cloud.</span></span> <span data-ttu-id="bb9f5-155">Achten Sie im Rahmen des Entwurfsprozesses auf die Anzahl von Aktivitäten, die in den ADF-Pipelines verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-155">As part of the design process, keep track of the number of activities used in the ADF pipelines.</span></span> <span data-ttu-id="bb9f5-156">Weitere Informationen finden Sie unter [Pipelines und Aktivitäten in Azure Data Factory](/azure/data-factory/concepts-pipelines-activities).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-156">For more information, see [Pipelines and activities in Azure Data Factory](/azure/data-factory/concepts-pipelines-activities).</span></span>

## <a name="pricing"></a><span data-ttu-id="bb9f5-157">Preise</span><span class="sxs-lookup"><span data-stu-id="bb9f5-157">Pricing</span></span>

<span data-ttu-id="bb9f5-158">Azure Data Factory ist eine kostengünstige Möglichkeit, um die Datenverschiebung in die Cloud zu orchestrieren.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-158">Azure Data Factory is a cost-effective way to orchestrate data movement in the cloud.</span></span> <span data-ttu-id="bb9f5-159">Die Kosten basieren auf verschiedenen Faktoren:</span><span class="sxs-lookup"><span data-stu-id="bb9f5-159">The cost is based on the several factors.</span></span>

* <span data-ttu-id="bb9f5-160">Anzahl von Pipelineausführungen</span><span class="sxs-lookup"><span data-stu-id="bb9f5-160">Number of pipeline executions</span></span>
* <span data-ttu-id="bb9f5-161">Anzahl verwendeter Entitäten/Aktivitäten innerhalb der Pipeline</span><span class="sxs-lookup"><span data-stu-id="bb9f5-161">Number of entities/activities used within the pipeline</span></span>
* <span data-ttu-id="bb9f5-162">Anzahl von Überwachungsvorgängen</span><span class="sxs-lookup"><span data-stu-id="bb9f5-162">Number of monitoring operations</span></span>
* <span data-ttu-id="bb9f5-163">Anzahl von Integrationsdurchläufen (in Azure gehostete IR oder selbstgehostete IR)</span><span class="sxs-lookup"><span data-stu-id="bb9f5-163">Number of Integration Runs (Azure-hosted IR or self-hosted IR)</span></span>

<span data-ttu-id="bb9f5-164">Für ADF wird eine nutzungsbasierte Abrechnung verwendet.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-164">ADF uses consumption-based billing.</span></span> <span data-ttu-id="bb9f5-165">Kosten fallen daher nur während Pipelineausführungen und während der Überwachung an.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-165">Therefore, cost is only incurred during pipeline executions and monitoring.</span></span> <span data-ttu-id="bb9f5-166">Die Ausführung einer einfachen Pipeline kostet gerade einmal 50 Cent, die Überwachung lediglich 25 Cent.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-166">The execution of a basic pipeline would cost as little as 50 cents and the monitoring as little as 25 cents.</span></span> <span data-ttu-id="bb9f5-167">Mit dem [Azure-Kostenrechner](https://azure.microsoft.com/pricing/calculator/) können Sie eine genauere Schätzung auf der Grundlage Ihrer spezifischen Workload erstellen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-167">The [Azure cost calculator](https://azure.microsoft.com/pricing/calculator/) can be used to create a more accurate estimate based on your specific workload.</span></span>

<span data-ttu-id="bb9f5-168">Wenn Sie eine ETL-Hybridworkload ausführen, müssen Sie auch die Kosten für den virtuellen Computer berücksichtigen, der als Host für Ihre SSIS-Pakete fungiert.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-168">When running a hybrid ETL workload, you must factor in the cost of the virtual machine used to host your SSIS packages.</span></span> <span data-ttu-id="bb9f5-169">Diese Kosten richten sich nach der Größe des virtuellen Computers und reichen von D1v2 (ein Kern, 3,5 GB RAM, Datenträger mit 50 GB) bis E64V3 (64 Kerne, 432 GB RAM, Datenträger mit 1.600 GB).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-169">This cost is based on the size of the VM ranging from a D1v2 (1 core, 3.5 GB RAM, 50 GB Disk) to E64V3 (64 cores, 432 GB RAM, 1600 GB disk).</span></span>  <span data-ttu-id="bb9f5-170">Weitere Informationen zur Wahl der geeigneten VM-Größe finden Sie unter [Überlegungen zur Leistung](/azure/cloud-services/cloud-services-sizes-specs#performance-considerations).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-170">If you need further guidance on selection the appropriate VM size, see [VM performance considerations](/azure/cloud-services/cloud-services-sizes-specs#performance-considerations).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb9f5-171">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="bb9f5-171">Next Steps</span></span>

* <span data-ttu-id="bb9f5-172">Informieren Sie sich ausführlicher über [Azure Data Factory](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="bb9f5-172">Learn more about [Azure Data Factory](https://azure.microsoft.com/services/data-factory/).</span></span>
* <span data-ttu-id="bb9f5-173">Absolvieren Sie das [Schritt-für-Schritt-Tutorial](/azure/data-factory/#step-by-step-tutorials), um sich mit Azure Data Factory vertraut zu machen.</span><span class="sxs-lookup"><span data-stu-id="bb9f5-173">Get started with Azure Data Factory by following the [Step-by-step tutorial](/azure/data-factory/#step-by-step-tutorials).</span></span>
* <span data-ttu-id="bb9f5-174">[Stellen Sie Azure-SSIS Integration Runtime in Azure Data Factory bereit.](/azure/data-factory/tutorial-deploy-ssis-packages-azure)</span><span class="sxs-lookup"><span data-stu-id="bb9f5-174">[Provision the Azure-SSIS Integration Runtime in Azure Data Factory](/azure/data-factory/tutorial-deploy-ssis-packages-azure).</span></span>

<!-- links -->
[architecture-diagram]: ./media/architecture-diagram-hybrid-etl-with-adf.png
[small-pricing]: https://azure.com/e/
[medium-pricing]: https://azure.com/e/
[large-pricing]: https://azure.com/e/
[availability]: /azure/architecture/checklist/availability
[resource-groups]: /azure/azure-resource-manager/resource-group-overview
[resiliency]: /azure/architecture/resiliency/
[security]: /azure/security/
[scalability]: /azure/architecture/checklist/scalability
[docs-blob-storage]: /azure/storage/blobs/
[docs-data-factory]: /azure/data-factory/introduction
[docs-resource-groups]: /azure/azure-resource-manager/resource-group-overview
[docs-ssis]: /sql/integration-services/sql-server-integration-services
[docs-sql-data-warehouse]: /azure/sql-data-warehouse/sql-data-warehouse-overview-what-is