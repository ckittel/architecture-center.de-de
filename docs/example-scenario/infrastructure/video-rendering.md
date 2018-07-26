---
title: 3D-Videorendering in Azure
description: Ausführen von nativen HPC-Workloads in Azure mit dem Azure Batch-Dienst
author: adamboeglin
ms.date: 07/13/2018
ms.openlocfilehash: b3af0641642d7ec4b022e8c96f51693eeb0adee4
ms.sourcegitcommit: 71cbef121c40ef36e2d6e3a088cb85c4260599b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/14/2018
ms.locfileid: "39061001"
---
# <a name="3d-video-rendering-on-azure"></a>3D-Videorendering in Azure

Das 3D-Rendering ist ein zeitaufwändiger Prozess, für dessen Durchführung eine erhebliche Menge an CPU-Zeit erforderlich ist.  Auf einem einzelnen Computer kann das Generieren einer Videodatei aus statischen Medienobjekten Stunden oder sogar Tage dauern – je nach Länge und Komplexität des produzierten Videos.  Viele Unternehmen erwerben entweder teure Highend-Computer für diese Aufgaben oder investieren in große Renderfarmen, an die Aufträge übermittelt werden können.  Bei Nutzung von Azure Batch ist diese hohe Leistung aber für Sie verfügbar, wenn Sie sie benötigen, und wird heruntergefahren, wenn Sie sie nicht benötigen – ohne jegliche Kapitalinvestitionen.

Mit Batch erhalten Sie unabhängig davon, ob Sie Windows Server- oder Linux-Computeknoten wählen, eine einheitliche Verwaltungsoberfläche und Auftragsplanung. Für Batch können Sie Ihre vorhandenen Windows- oder Linux-Anwendungen nutzen, z.B. AutoDesk Maya und Blender, um in Azure umfangreiche Renderaufträge auszuführen.

## <a name="related-use-cases"></a>Verwandte Anwendungsfälle

Erwägen Sie dieses Szenario für ähnliche Anwendungsfälle:

* 3D-Modellierung
* VFX-Rendering (Visual FX)
* Videotranscodierung
* Bildverarbeitung, Farbkorrektur und Größenänderung

## <a name="architecture"></a>Architektur

![Architekturübersicht über die Komponenten einer cloudbasierten HPC-Lösung mit Azure Batch][architecture]

In diesem Beispielszenario wird der Workflow bei Verwendung von Azure Batch beschrieben, und die Daten fließen wie folgt:

1. Hochladen der Eingabedateien und der Anwendungen, mit denen diese Dateien verarbeitet werden, in Ihr Azure Storage-Konto
2. Erstellen eines Batch-Pools mit Computeknoten in Ihrem Batch-Konto, eines Auftrags zum Ausführen der Workload im Pool und von Aufgaben im Auftrag
3. Herunterladen von Eingabedateien und der Anwendungen in Batch
4. Überwachen der Aufgabenausführung
5. Hochladen der Aufgabenausgabe
6. Herunterladen von Ausgabedateien

Zur Vereinfachung dieses Prozesses können Sie auch die [Batch-Plug-Ins für Maya & 3ds Max][batch-plugins] verwenden.

### <a name="components"></a>Komponenten

Azure Batch basiert auf der folgenden Azure-Technologie:

* [Ressourcengruppen][resource-groups] sind logische Container für Azure-Ressourcen.
* [Virtuelle Netzwerke][vnet] werden sowohl für den Hauptknoten als auch für die Computeressourcen verwendet.
* [Storage][storage]-Konten werden für die Synchronisierung und Datenaufbewahrung verwendet.
* [Virtual Machine Scale Sets][vmss] (VM-Skalierungsgruppen) werden von CycleCloud für Computeressourcen genutzt.

## <a name="considerations"></a>Überlegungen

### <a name="machine-sizes-available-for-azure-batch"></a>Verfügbare Computergrößen für Azure Batch
Die meisten Renderingkunden entscheiden sich zwar für Ressourcen mit einer hohen CPU-Leistung, aber für andere Workloads mit Verwendung von VM Scale Sets werden virtuelle Computer ggf. anders ausgewählt und sind von verschiedenen Faktoren abhängig:
  - Ist die ausgeführte Anwendung speichergebunden?
  - Müssen für die Anwendung GPUs verwendet werden? 
  - Gilt für die Auftragstypen eine hohe Parallelität, oder ist für eng gekoppelte Aufträge eine Infiniband-Konnektivität erforderlich?
  - Erzwingen einer hohen E/A-Geschwindigkeit für die Speicherung auf den Computeknoten

Azure verfügt über einen weiten Bereich von VM-Größen, mit denen alle oben beschriebenen Anwendungsanforderungen erfüllt werden können. Einige gelten speziell für HPC, aber auch die kleinsten Größen können genutzt werden, um für eine effektive Rasterimplementierung zu sorgen:

  - [HPC-VM-Größen][compute-hpc] Aufgrund der CPU-Bindung des Renderns empfiehlt Microsoft normalerweise die Verwendung von Azure-VMs der H-Serie.  Diese VMs sind speziell auf Highend-Computeranforderungen ausgelegt und verfügen über vCPU-Größen mit 8 oder 16 Kernen sowie DDR4-Arbeitsspeicher, temporären SSD-Speicher und Haswell E5 Intel-Technologie.
  - [GPU-VM-Größen][compute-gpu] GPU-optimierte VM-Größen sind für spezialisierte virtuelle Computer mit einzelnen oder mehreren NVIDIA-GPUs verfügbar. Diese Größen sind für rechenintensive, grafikintensive und visualisierungsorientierte Workloads vorgesehen.
    - Die Größen NC, NCv2, NCv3 und ND sind für rechen- und netzwerkintensive Anwendungen und Algorithmen wie CUDA- und OpenCL-basierte Anwendungen und Simulationen sowie für KI und Deep Learning optimiert. NV-Größen sind für Remotevisualisierung, Streaming, Spiele, Codierung und VDI-Szenarien mit Frameworks wie OpenGL und DirectX optimiert und konzipiert.
  - [Arbeitsspeicheroptimierte VM-Größen][compute-memory] Wenn mehr Arbeitsspeicher erforderlich ist, ermöglichen die arbeitsspeicheroptimierten VM-Größen ein höheres Arbeitsspeicher/CPU-Verhältnis.
  - [Universelle VM-Größen][compute-general] Es sind auch universelle VM-Größen mit einem ausgewogenen Verhältnis von CPU zu Arbeitsspeicher verfügbar.

### <a name="alternatives"></a>Alternativen

Falls Sie eine bessere Kontrolle über Ihre Renderingumgebung in Azure oder eine Hybridimplementierung benötigen, kann CycleCloud-Computing die Orchestrierung eines IaaS-Rasters in der Cloud unterstützen. Indem die gleiche zugrunde liegende Azure-Technologie wie für Azure Batch verwendet wird, wird das Erstellen und Warten eines IaaS-Rasters zu einem effizienten Prozess. Unter dem folgenden Link finden Sie weitere Informationen zu den Entwurfsprinzipien:

Eine vollständige Übersicht über alle HPC-Lösungen, die für Sie in Azure verfügbar sind, finden Sie im Artikel [HPC-, Batch- und Big Compute-Lösungen mit Azure-VMs][hpc-alt-solutions].

### <a name="availability"></a>Verfügbarkeit

Die Überwachung der Azure Batch-Komponenten ist über unterschiedliche Dienste, Tools und APIs verfügbar. Weitere Informationen hierzu finden Sie im Artikel [Überwachen von Batch-Lösungen][batch-monitor].

### <a name="scalability"></a>Skalierbarkeit

Pools eines Azure Batch-Kontos können entweder per manuellem Eingriff oder mit einer Formel basierend auf Azure Batch-Metriken automatisch skaliert werden. Weitere Informationen hierzu finden Sie im Artikel [Create an automatic scaling formula for scaling nodes in a Batch pool][batch-scaling] (Erstellen einer Formel für die automatische Skalierung zum Skalieren von Knoten in einem Batch-Pool).

### <a name="security"></a>Sicherheit

Allgemeine Informationen zur Entwicklung sicherer Lösungen finden Sie in der [Dokumentation zur Azure-Sicherheit][security].

### <a name="resiliency"></a>Resilienz

Da in Azure Batch derzeit keine Failoverfunktion verfügbar ist, empfehlen wir die folgenden Schritte, um sicherzustellen, dass bei einem ungeplanten Ausfall für Verfügbarkeit gesorgt ist:

* Erstellen eines Azure Batch-Kontos an einem anderen Azure-Standort mit einem anderen Speicherkonto
* Erstellen der gleichen Knotenpools mit dem gleichen Namen und null zugeordneten Knoten
* Sicherstellen, dass Anwendungen erstellt und auf das alternative Speicherkonto aktualisiert werden
* Hochladen von Eingabedateien und Übermitteln von Aufträgen an das andere Azure Batch-Konto

## <a name="deploy-this-scenario"></a>Bereitstellen dieses Szenarios

### <a name="creating-an-azure-batch-account-and-pools-manually"></a>Manuelles Erstellen eines Azure Batch-Kontos und der Pools

In diesem Beispielszenario wird veranschaulicht, wie Azure Batch funktioniert, und Azure Batch Labs wird als SaaS-Beispiellösung verwendet, die für Ihre eigenen Kunden entwickelt werden kann:

[Azure Batch – Masterclass][batch-labs-masterclass]

### <a name="deploying-the-sample-scenario-using-an-azure-resource-manager-arm-template"></a>Bereitstellen des Beispielszenarios mit einer ARM-Vorlage (Azure Resource Manager)

Über die Vorlage wird Folgendes bereitgestellt:
  - Ein neues Azure Batch-Konto
  - Ein Speicherkonto
  - Einen Knotenpool, der dem Batch-Konto zugeordnet ist
  - Knotenpool wird für die Verwendung von A2 v2-VMs mit Canonical Ubuntu-Images konfiguriert
  - Knotenpool enthält anfänglich 0 VMs, und zum Hinzufügen von VMs ist eine manuelle Skalierung erforderlich

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Fsolution-architectures%2Fmaster%2Fhpc%2Fbatchcreatewithpools.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

[Weitere Informationen zu ARM-Vorlagen][azure-arm-templates]

## <a name="pricing"></a>Preise

Die Kosten für die Nutzung von Azure Batch richten sich nach den VM-Größen, die für die Pools verwendet werden, und nach der Dauer der Zuordnung und Ausführung. Für die Erstellung eines Azure Batch-Kontos werden keine Kosten berechnet. Speicher und ausgehende Daten sollten ebenfalls berücksichtigt werden, da hierfür weitere Kosten anfallen.

Hier sind Beispiele für Kosten angegeben, die für einen Auftrag anfallen können, der innerhalb von acht Stunden abgeschlossen wird, indem eine andere Zahl von Servern genutzt wird:


- 100 VMs mit Hochleistungs-CPU: [Kostenschätzung][hpc-est-high]

  100 x H16m (16 Kerne, 225 GB RAM, Storage Premium 512 GB), 2 TB Blobspeicher, 1 TB ausgehender Datenverkehr

- 50 VMs mit Hochleistungs-CPU: [Kostenschätzung][hpc-est-med]

  50 x H16m (16 Kerne, 225 GB RAM, Storage Premium 512 GB), 2 TB Blobspeicher, 1 TB ausgehender Datenverkehr

- 10 VMs mit Hochleistungs-CPU: [Kostenschätzung][hpc-est-low]
  
  10 x H16m (16 Kerne, 225 GB RAM, Storage Premium 512 GB), 2 TB Blobspeicher, 1 TB ausgehender Datenverkehr

### <a name="low-priority-vm-pricing"></a>Preise für VMs mit niedriger Priorität

Azure Batch unterstützt auch die Verwendung von VMs mit niedriger Priorität* in den Knotenpools, und dies kann unter Umständen zu erheblichen Kosteneinsparungen führen. Einen Preisvergleich zwischen Standard-VMs und VMs mit niedriger Priorität sowie weitere Informationen zu VMs mit niedriger Priorität finden Sie unter [Batch – Preise][batch-pricing].

\* Beachten Sie, dass nur bestimmte Anwendungen und Workloads für die Ausführung auf VMs mit niedriger Priorität geeignet sind.

## <a name="related-resources"></a>Zugehörige Ressourcen

[Azure Batch – Übersicht][batch-overview]

[Azure Batch-Dokumentation][batch-doc]

[Verwenden von Containern in Azure Batch][batch-containers]

<!-- links -->
[architecture]: ./media/native-hpc-ref-arch.png
[resource-groups]: /azure/azure-resource-manager/resource-group-overview
[security]: /azure/security/
[resiliency]: /azure/architecture/resiliency/
[scalability]: /azure/architecture/checklist/scalability
[vmss]: /azure/virtual-machine-scale-sets/overview
[vnet]: /azure/virtual-network/virtual-networks-overview
[storage]: https://azure.microsoft.com/services/storage/
[batch]: https://azure.microsoft.com/services/batch/
[batch-arch]: https://azure.microsoft.com/solutions/architecture/big-compute-with-azure-batch/
[compute-hpc]: /azure/virtual-machines/windows/sizes-hpc
[compute-gpu]: /azure/virtual-machines/windows/sizes-gpu
[compute-compute]: /azure/virtual-machines/windows/sizes-compute
[compute-memory]: /azure/virtual-machines/windows/sizes-memory
[compute-general]: /azure/virtual-machines/windows/sizes-general
[compute-storage]: /azure/virtual-machines/windows/sizes-storage
[compute-acu]: /azure/virtual-machines/windows/acu
[compute=benchmark]: /azure/virtual-machines/windows/compute-benchmark-scores
[hpc-est-high]: https://azure.com/e/9ac25baf44ef49c3a6b156935ee9544c
[hpc-est-med]: https://azure.com/e/0286f1d6f6784310af4dcda5aec8c893
[hpc-est-low]: https://azure.com/e/e39afab4e71949f9bbabed99b428ba4a
[batch-labs-masterclass]: https://github.com/azurebigcompute/BigComputeLabs/tree/master/Azure%20Batch%20Masterclass%20Labs
[batch-scaling]: /azure/batch/batch-automatic-scaling
[hpc-alt-solutions]: /azure/virtual-machines/linux/high-performance-computing?toc=%2fazure%2fbatch%2ftoc.json
[batch-monitor]: /azure/batch/monitoring-overview
[batch-pricing]: https://azure.microsoft.com/en-gb/pricing/details/batch/
[batch-doc]: /azure/batch/
[batch-overview]: https://azure.microsoft.com/services/batch/
[batch-containers]: https://github.com/Azure/batch-shipyard
[azure-arm-templates]: /azure/azure-resource-manager/resource-group-overview#template-deployment
[batch-plugins]: /azure/batch/batch-rendering-service#options-for-submitting-a-render-job