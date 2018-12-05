---
title: Echtzeitbewertung von Python scikit-learn- und Deep Learning-Modellen in Azure
description: Diese Referenzarchitektur zeigt, wie Sie Python-Modelle als Webdienste in Azure bereitstellen, um in Echtzeit Vorhersagen zu treffen.
author: njray
ms.date: 11/09/2018
ms.author: njray
ms.openlocfilehash: 860eb83f248c2a9f2a96065c6c4cdd02715e7ce1
ms.sourcegitcommit: cc234a522b7fc35af3bcacdc044c2e2b529e54ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2018
ms.locfileid: "51347756"
---
# <a name="real-time-scoring-of-python-scikit-learn-and-deep-learning-models-on-azure"></a><span data-ttu-id="9b382-103">Echtzeitbewertung von Python scikit-learn- und Deep Learning-Modellen in Azure</span><span class="sxs-lookup"><span data-stu-id="9b382-103">Real-time scoring of Python Scikit-Learn and Deep Learning Models on Azure</span></span>

<span data-ttu-id="9b382-104">Diese Referenzarchitektur zeigt, wie Sie Python-Modelle als Webdienste bereitstellen, um in Echtzeit Vorhersagen zu treffen.</span><span class="sxs-lookup"><span data-stu-id="9b382-104">This reference architecture shows how to deploy Python models as web services to make real-time predictions.</span></span> <span data-ttu-id="9b382-105">In diesem Artikel werden zwei Szenarien behandelt: die Bereitstellung von regulären Python-Modellen und die spezifischen Anforderungen der Bereitstellung von Deep Learning-Modellen.</span><span class="sxs-lookup"><span data-stu-id="9b382-105">Two scenarios are covered: deploying regular Python models, and the specific requirements of deploying deep learning models.</span></span> <span data-ttu-id="9b382-106">Für beide Szenarien wird die hier dargestellte Architektur verwendet.</span><span class="sxs-lookup"><span data-stu-id="9b382-106">Both scenarios use the architecture shown.</span></span>

<span data-ttu-id="9b382-107">Auf GitHub sind zwei Referenzimplementierungen für diese Architektur verfügbar – eine für [reguläre Python-Modelle][github-python] und eine für [Deep Learning-Modelle][github-dl].</span><span class="sxs-lookup"><span data-stu-id="9b382-107">Two reference implementations for this architecture are available on GitHub, one for [regular Python models][github-python] and one for [deep learning models][github-dl].</span></span>

![](./_images/python-model-architecture.png)

## <a name="scenarios"></a><span data-ttu-id="9b382-108">Szenarien</span><span class="sxs-lookup"><span data-stu-id="9b382-108">Scenarios</span></span>

<span data-ttu-id="9b382-109">Die Referenzimplementierungen veranschaulichen zwei Szenarien, in denen diese Architektur verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="9b382-109">The reference implementations demonstrate two scenarios using this architecture.</span></span>

<span data-ttu-id="9b382-110">**Szenario 1: Abgleich von häufig gestellten Fragen (FAQ)**.</span><span class="sxs-lookup"><span data-stu-id="9b382-110">**Scenario 1: FAQ matching**.</span></span> <span data-ttu-id="9b382-111">Dieses Szenario zeigt, wie Sie ein Modell zum Abgleichen von häufig gestellten Fragen (FAQ) als Webdienst bereitstellen, um die Fragen von Benutzern vorherzusagen.</span><span class="sxs-lookup"><span data-stu-id="9b382-111">This scenario shows how to deploy a frequently asked questions (FAQ) matching model as a web service to provide predictions for user questions.</span></span> <span data-ttu-id="9b382-112">In diesem Szenario bezieht sich der Begriff „Eingabedaten“ im Architekturdiagramm auf Textzeichenfolgen mit Fragen von Benutzern, die mit einer Liste von häufig gestellten Fragen abgeglichen werden.</span><span class="sxs-lookup"><span data-stu-id="9b382-112">For this scenario, "Input Data" in the architecture diagram refers to text strings containing user questions to match with a list of FAQs.</span></span> <span data-ttu-id="9b382-113">Dieses Szenario ist für die [scikit-learn][scikit]-Bibliothek für maschinelles Lernen für Python konzipiert, es kann jedoch für beliebige Szenarien mit Python-Modellen generalisiert werden, um in Echtzeit Vorhersagen zu treffen.</span><span class="sxs-lookup"><span data-stu-id="9b382-113">This scenario is designed for the [scikit-learn][scikit] machine learning library for Python, but can be generalized to any scenario that uses Python models to make real-time predictions.</span></span>

<span data-ttu-id="9b382-114">In diesem Szenario wird eine Teilmenge der Stack Overflow-Fragedaten verwendet, die die ursprünglichen Fragen (als JavaScript markiert), die zugehörigen doppelten Fragen und Antworten umfasst.</span><span class="sxs-lookup"><span data-stu-id="9b382-114">This scenario uses a subset of Stack Overflow question data that includes original questions tagged as JavaScript, their duplicate questions, and their answers.</span></span> <span data-ttu-id="9b382-115">Das Szenario trainiert eine scikit-learn-Pipeline zum Vorhersagen der Übereinstimmungswahrscheinlichkeit einer doppelten Frage mit den einzelnen ursprünglichen Fragen.</span><span class="sxs-lookup"><span data-stu-id="9b382-115">It trains a scikit-learn pipeline to predict the match probability of a duplicate question with each of the original questions.</span></span> <span data-ttu-id="9b382-116">Diese Vorhersagen werden in Echtzeit mithilfe eines REST-API-Endpunkts getroffen.</span><span class="sxs-lookup"><span data-stu-id="9b382-116">These predictions are made in real time using a REST API  endpoint.</span></span>

<span data-ttu-id="9b382-117">Der Anwendungsfluss für diese Architektur sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="9b382-117">The application flow for this architecture is as follows:</span></span>

1.  <span data-ttu-id="9b382-118">Der Client sendet eine HTTP-POST-Anforderung mit den codierten Fragedaten.</span><span class="sxs-lookup"><span data-stu-id="9b382-118">The client sends an HTTP POST request with the encoded question data.</span></span>

2.  <span data-ttu-id="9b382-119">Die Flask-App extrahiert die Frage aus der Anforderung.</span><span class="sxs-lookup"><span data-stu-id="9b382-119">The Flask app extracts the question from the request.</span></span>

3.  <span data-ttu-id="9b382-120">Die Frage wird zur Featurebereitstellung und Bewertung an das scikit-learn-Pipelinemodell gesendet.</span><span class="sxs-lookup"><span data-stu-id="9b382-120">The question is sent to the scikit-learn pipeline model for featurization and scoring.</span></span>

4.  <span data-ttu-id="9b382-121">Die übereinstimmenden häufig gestellten Fragen werden mit ihren Bewertungen an ein JSON-Objekt weitergeleitet und an den Client zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="9b382-121">The matching FAQ questions with their scores are piped into a JSON object and returned to the client.</span></span>

<span data-ttu-id="9b382-122">Hier sehen Sie einen Screenshot der Beispiel-App, die die Ergebnisse nutzt:</span><span class="sxs-lookup"><span data-stu-id="9b382-122">Here is a screenshot of the example app that consumes the results:</span></span>

![](./_images/python-faq-matches.png)

<span data-ttu-id="9b382-123">**Szenario 2: Bildklassifizierung.**</span><span class="sxs-lookup"><span data-stu-id="9b382-123">**Scenario 2: Image classification.**</span></span> <span data-ttu-id="9b382-124">Dieses Szenario zeigt, wie Sie ein Modell für ein künstliches neuronales Netzwerk (Convolutional Neural Network, CNN) als Webdienst bereitstellen, um Vorhersagen für Bilder zu generieren.</span><span class="sxs-lookup"><span data-stu-id="9b382-124">This scenario shows how to deploy a Convolutional Neural Network (CNN) model as a web service to provide predictions on images.</span></span> <span data-ttu-id="9b382-125">In diesem Szenario bezieht sich der Begriff „Eingabedaten“ im Architekturdiagramm auf Bilddateien.</span><span class="sxs-lookup"><span data-stu-id="9b382-125">For this scenario, "Input Data" in the architecture diagram refers to image files.</span></span> <span data-ttu-id="9b382-126">Für Aufgaben wie die Bildklassifizierung und Erkennung von Objekten sind CNNs eine äußerst effektive Lösung für maschinelles Sehen.</span><span class="sxs-lookup"><span data-stu-id="9b382-126">CNNs are very effective in computer vision for tasks such as image classification and object detection.</span></span> <span data-ttu-id="9b382-127">Dieses Szenario ist für die Frameworks TensorFlow, Keras (mit dem TensorFlow-Back-End) und PyTorch konzipiert.</span><span class="sxs-lookup"><span data-stu-id="9b382-127">This scenario is designed for the frameworks TensorFlow, Keras (with the TensorFlow back end), and PyTorch.</span></span> <span data-ttu-id="9b382-128">Es kann jedoch für beliebige Szenarien generalisiert werden, die mithilfe von Deep Learning-Modellen in Echtzeit Vorhersagen treffen.</span><span class="sxs-lookup"><span data-stu-id="9b382-128">However, it can be generalized to any scenario that uses deep learning models to make real-time predictions.</span></span>

<span data-ttu-id="9b382-129">In diesem Szenario wird ein für ein ImageNet-1K-Dataset (1.000 Klassen) vortrainiertes ResNet-152-Modell verwendet, um die Kategorie vorherzusagen, zu der ein Bild gehört (siehe unten stehende Abbildung).</span><span class="sxs-lookup"><span data-stu-id="9b382-129">This scenario uses a pre-trained ResNet-152 model trained on ImageNet-1K (1,000 classes) dataset to predict which category (see figure below) an image belongs to.</span></span> <span data-ttu-id="9b382-130">Diese Vorhersagen werden in Echtzeit mithilfe eines REST-API-Endpunkts getroffen.</span><span class="sxs-lookup"><span data-stu-id="9b382-130">These predictions are made in real time using a REST API endpoint.</span></span>

![](./_images/python-example-predictions.png)

<span data-ttu-id="9b382-131">Der Anwendungsfluss für das Deep Learning-Modell sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="9b382-131">The application flow for the deep learning model is as follows:</span></span>

1.  <span data-ttu-id="9b382-132">Der Client sendet eine HTTP-POST-Anforderung mit den codierten Bilddaten.</span><span class="sxs-lookup"><span data-stu-id="9b382-132">The client sends an HTTP POST request with the encoded image data.</span></span>

2.  <span data-ttu-id="9b382-133">Die Flask-App extrahiert das Bild aus der Anforderung.</span><span class="sxs-lookup"><span data-stu-id="9b382-133">The Flask app extracts the image from the request.</span></span>

3.  <span data-ttu-id="9b382-134">Das Bild wird vorverarbeitet und zur Bewertung an das Modell gesendet.</span><span class="sxs-lookup"><span data-stu-id="9b382-134">The image is preprocessed and sent to the model for scoring.</span></span>

4.  <span data-ttu-id="9b382-135">Das Bewertungsergebnis wird an ein JSON-Objekt weitergeleitet und an den Client zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="9b382-135">The scoring result is piped into a JSON object and returned to the client.</span></span>

## <a name="architecture"></a><span data-ttu-id="9b382-136">Architecture</span><span class="sxs-lookup"><span data-stu-id="9b382-136">Architecture</span></span>

<span data-ttu-id="9b382-137">Diese Architektur umfasst die folgenden Komponenten.</span><span class="sxs-lookup"><span data-stu-id="9b382-137">This architecture consists of the following components.</span></span>

<span data-ttu-id="9b382-138">**[VM][vm]**.</span><span class="sxs-lookup"><span data-stu-id="9b382-138">**[Virtual machine][vm]** (VM).</span></span> <span data-ttu-id="9b382-139">Die VM dient als Beispiel für ein Gerät (lokal oder in der Cloud), das eine HTTP-Anforderung senden kann.</span><span class="sxs-lookup"><span data-stu-id="9b382-139">The VM is shown as an example of a device &mdash; local or in the cloud &mdash; that can send an HTTP request.</span></span>

<span data-ttu-id="9b382-140">**[Azure Kubernetes Service][aks]** (AKS) wird verwendet, um die Anwendung in einem Kubernetes-Cluster bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="9b382-140">**[Azure Kubernetes Service][aks]** (AKS) is used to deploy the application on a Kubernetes cluster.</span></span> <span data-ttu-id="9b382-141">AKS vereinfacht die Bereitstellung und den Betrieb von Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9b382-141">AKS simplifies the deployment and operations of Kubernetes.</span></span> <span data-ttu-id="9b382-142">Der Cluster kann für reguläre Python-Modelle mit reinen CPU-VMs oder für Deep Learning-Modelle mit GPU-fähigen VMs konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="9b382-142">The cluster can be configured using CPU-only VMs for regular Python models or GPU-enabled VMs for deep learning models.</span></span>

<span data-ttu-id="9b382-143">**[Lastenausgleich][lb]**.</span><span class="sxs-lookup"><span data-stu-id="9b382-143">**[Load balancer][lb]**.</span></span> <span data-ttu-id="9b382-144">Ein von AKS bereitgestellter Lastenausgleich wird verwendet, um den Dienst extern verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="9b382-144">A load balancer, provisioned by AKS, is used to expose the service externally.</span></span> <span data-ttu-id="9b382-145">Datenverkehr vom Lastenausgleich wird an die Back-End-Pods geleitet.</span><span class="sxs-lookup"><span data-stu-id="9b382-145">Traffic from the load balancer is directed to the back-end pods.</span></span>

<span data-ttu-id="9b382-146">Der **[Docker-Hub][docker]** dient zum Speichern des im Kubernetes-Cluster bereitgestellten Docker-Images.</span><span class="sxs-lookup"><span data-stu-id="9b382-146">**[Docker Hub][docker]** is used to store the Docker image that is deployed on Kubernetes cluster.</span></span> <span data-ttu-id="9b382-147">Der Docker-Hub wurde für diese Architektur ausgewählt, weil er benutzerfreundlich und das Standardimagerepository für Docker-Benutzer ist.</span><span class="sxs-lookup"><span data-stu-id="9b382-147">Docker Hub was chosen for this architecture because it's easy to use and is the default image repository for Docker users.</span></span> <span data-ttu-id="9b382-148">[Azure Container Registry][acr] kann ebenfalls verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9b382-148">[Azure Container Registry][acr] can also be used for this architecture.</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="9b382-149">Überlegungen zur Leistung</span><span class="sxs-lookup"><span data-stu-id="9b382-149">Performance considerations</span></span>

<span data-ttu-id="9b382-150">Für Architekturen zur Echtzeitbewertung ist die Durchsatzleistung ein entscheidender Faktor.</span><span class="sxs-lookup"><span data-stu-id="9b382-150">For real-time scoring architectures, throughput performance becomes a dominant consideration.</span></span> <span data-ttu-id="9b382-151">Für reguläre Python-Modelle sind CPUs, die zum Bewältigen der Workload ausreichen, in der Regel akzeptabel.</span><span class="sxs-lookup"><span data-stu-id="9b382-151">For regular Python models, it's generally accepted that CPUs are sufficient to handle the workload.</span></span> 

<span data-ttu-id="9b382-152">Für Deep Learning-Workloads, bei denen sich die Geschwindigkeit als Engpass erweisen kann, bieten GPUs im Allgemeinen jedoch eine bessere [Leistung][gpus-vs-cpus] als CPUs.</span><span class="sxs-lookup"><span data-stu-id="9b382-152">However for deep learning workloads, when speed is a bottleneck, GPUs generally provide better [performance][gpus-vs-cpus] compared to CPUs.</span></span> <span data-ttu-id="9b382-153">Um die GPU-Leistung mit CPUs zu erreichen, ist normalerweise ein Cluster mit einer großen Anzahl von CPUs erforderlich.</span><span class="sxs-lookup"><span data-stu-id="9b382-153">To match GPU performance using CPUs, a cluster with large number of CPUs is usually needed.</span></span>

<span data-ttu-id="9b382-154">Sie können in beiden Szenarien CPUs für diese Architektur verwenden. Für Deep Learning-Modelle bieten GPUs jedoch deutlich höhere Durchsatzwerte als ein CPU-Cluster mit vergleichbaren Kosten.</span><span class="sxs-lookup"><span data-stu-id="9b382-154">You can use CPUs for this architecture in either scenario, but for deep learning models, GPUs provide significantly higher throughput values compared to a CPU cluster of similar cost.</span></span> <span data-ttu-id="9b382-155">AKS unterstützt die Verwendung von GPUs. Dies ist einer der Vorteile, die die Verwendung von AKS für diese Architektur bietet.</span><span class="sxs-lookup"><span data-stu-id="9b382-155">AKS supports the use of GPUs, which is one advantage of using AKS for this architecture.</span></span> <span data-ttu-id="9b382-156">Zudem werden bei Deep Learning-Bereitstellungen in der Regel Modelle mit einer hohen Anzahl von Parametern verwendet.</span><span class="sxs-lookup"><span data-stu-id="9b382-156">Also, deep learning deployments typically use models with a high number of parameters.</span></span> <span data-ttu-id="9b382-157">Durch die Verwendung von GPUs werden Ressourcenkonflikte zwischen dem Modell und dem Webdienst vermieden, die bei reinen CPU-Bereitstellungen ein Problem darstellen.</span><span class="sxs-lookup"><span data-stu-id="9b382-157">Using GPUs prevents contention for resources between the model and the web service, which is an issue in CPU-only deployments.</span></span>

## <a name="scalability-considerations"></a><span data-ttu-id="9b382-158">Überlegungen zur Skalierbarkeit</span><span class="sxs-lookup"><span data-stu-id="9b382-158">Scalability considerations</span></span>

<span data-ttu-id="9b382-159">Bei regulären Python-Modellen mit einer AKS-Clusterbereitstellung mit reinen CPU-VMs ist beim [Erhöhen der Anzahl von Pods][manually-scale-pods] Vorsicht geboten.</span><span class="sxs-lookup"><span data-stu-id="9b382-159">For regular Python models, where AKS cluster is provisioned with CPU-only VMs, take care when [scaling out the number of pods][manually-scale-pods].</span></span> <span data-ttu-id="9b382-160">Das Ziel ist es, den Cluster vollständig zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="9b382-160">The goal is to fully utilize the cluster.</span></span> <span data-ttu-id="9b382-161">Die Skalierung ist von den CPU-Anforderungen und den für die Pods definierten Grenzwerten abhängig.</span><span class="sxs-lookup"><span data-stu-id="9b382-161">Scaling depends on the CPU requests and limits defined for the pods.</span></span> <span data-ttu-id="9b382-162">Kubernetes unterstützt auch die [automatische Skalierung][autoscale-pods] der Pods, um die Anzahl von Pods in einer Bereitstellung basierend auf der CPU-Nutzung oder anderen ausgewählten Metriken anzupassen.</span><span class="sxs-lookup"><span data-stu-id="9b382-162">Kubernetes also supports [autoscaling][autoscale-pods] of the pods to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> <span data-ttu-id="9b382-163">Die [automatische Clusterskalierung][autoscaler] (Vorschauversion) kann Agent-Knoten basierend auf ausstehenden Pods skalieren.</span><span class="sxs-lookup"><span data-stu-id="9b382-163">The [cluster autoscaler][autoscaler] (in preview) can scale agent nodes based on pending pods.</span></span>

<span data-ttu-id="9b382-164">Für Deep Learning-Szenarien mit GPU-fähigen VMs sind die Ressourceneinschränkungen für Pods so ausgelegt, dass eine GPU einem Pod zugewiesen wird.</span><span class="sxs-lookup"><span data-stu-id="9b382-164">For deep learning scenarios, using GPU-enabled VMs, resource limits on pods are such that one GPU is assigned to one pod.</span></span> <span data-ttu-id="9b382-165">Je nach verwendetem VM-Typ müssen Sie die [Knoten des Clusters skalieren][scale-cluster], um die Anforderungen für den Dienst zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="9b382-165">Depending on the type of VM used, you must [scale the nodes of the cluster][scale-cluster] to meet the demand for the service.</span></span> <span data-ttu-id="9b382-166">Dies ist mithilfe der Azure-Befehlszeilenschnittstelle (Azure CLI) und Kubectl ganz einfach möglich.</span><span class="sxs-lookup"><span data-stu-id="9b382-166">You can do this easily using the Azure CLI and kubectl.</span></span>

## <a name="monitoring-and-logging-considerations"></a><span data-ttu-id="9b382-167">Überlegungen zur Überwachung und Protokollierung</span><span class="sxs-lookup"><span data-stu-id="9b382-167">Monitoring and logging considerations</span></span>

### <a name="aks-monitoring"></a><span data-ttu-id="9b382-168">AKS-Überwachung</span><span class="sxs-lookup"><span data-stu-id="9b382-168">AKS monitoring</span></span>

<span data-ttu-id="9b382-169">Verwenden Sie das Feature [Azure Monitor für Container][monitor-containers], um Einblick in die AKS-Leistung zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="9b382-169">For visibility into AKS performance, use the [Azure Monitor for containers][monitor-containers] feature.</span></span> <span data-ttu-id="9b382-170">Das Feature erfasst anhand der Metrik-API die in Kubernetes verfügbaren Speicher- und Prozessormetriken von Controllern, Knoten und Containern.</span><span class="sxs-lookup"><span data-stu-id="9b382-170">It collects memory and processor metrics from controllers, nodes, and containers that are available in Kubernetes through the Metrics API.</span></span>

<span data-ttu-id="9b382-171">Überwachen Sie während der Bereitstellung Ihrer Anwendung den AKS-Cluster, um sicherzustellen, dass er wie erwartet funktioniert, alle Knoten funktionsfähig sind und alle Pods ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="9b382-171">While deploying your application, monitor the AKS cluster to make sure it's working as expected, all the nodes are operational, and all pods are running.</span></span> <span data-ttu-id="9b382-172">Sie können den Podstatus mit dem Befehlszeilentool [Kubectl][kubectl] abrufen, Kubernetes enthält jedoch auch ein Webdashboard für die grundlegende Überwachung des Clusterstatus und Verwaltung.</span><span class="sxs-lookup"><span data-stu-id="9b382-172">Although you can use the [kubectl][kubectl] command-line tool to retrieve pod status, Kubernetes also includes a web dashboard for basic monitoring of the cluster status and management.</span></span>

![](./_images/python-kubernetes-dashboard.png)

<span data-ttu-id="9b382-173">Den Gesamtzustand des Clusters und der Knoten können Sie im Abschnitt **Knoten** des Kubernetes-Dashboards einsehen.</span><span class="sxs-lookup"><span data-stu-id="9b382-173">To see the overall state of the cluster and nodes, go to the **Nodes** section of the Kubernetes dashboard.</span></span> <span data-ttu-id="9b382-174">Wenn ein Knoten inaktiv oder ausgefallen ist, können Sie die Fehlerprotokolle auf dieser Seite anzeigen.</span><span class="sxs-lookup"><span data-stu-id="9b382-174">If a node is inactive or has failed, you can display the error logs from that page.</span></span> <span data-ttu-id="9b382-175">Informationen zur Anzahl von Pods und zum Status Ihrer Bereitstellung finden Sie in den Abschnitten **Pods** und **Bereitstellungen**.</span><span class="sxs-lookup"><span data-stu-id="9b382-175">Similarly, go to the **Pods** and **Deployments** sections for information about the number of pods and status of your deployment.</span></span>

### <a name="aks-logs"></a><span data-ttu-id="9b382-176">AKS-Protokolle</span><span class="sxs-lookup"><span data-stu-id="9b382-176">AKS logs</span></span> 

<span data-ttu-id="9b382-177">AKS protokolliert automatisch alle stdout-/stderr-Meldungen in den Protokollen der Pods im Cluster.</span><span class="sxs-lookup"><span data-stu-id="9b382-177">AKS automatically logs all stdout/stderr to the logs of the pods in the cluster.</span></span> <span data-ttu-id="9b382-178">Verwenden Sie Kubectl, um diese Meldungen und auch Ereignisse sowie Protokolle auf Knotenebene anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="9b382-178">Use kubectl to see these and also node-level events and logs.</span></span> <span data-ttu-id="9b382-179">Ausführliche Informationen finden Sie in den Bereitstellungsschritten.</span><span class="sxs-lookup"><span data-stu-id="9b382-179">For details, see the deployment steps.</span></span>

<span data-ttu-id="9b382-180">Verwenden Sie [Azure Monitor für Container][monitor-containers], um Metriken und Protokolle über eine Containerversion des Log Analytics-Agents für Linux zu erfassen, die in Ihrem Log Analytics-Arbeitsbereich gespeichert wird.</span><span class="sxs-lookup"><span data-stu-id="9b382-180">Use [Azure Monitor for containers][monitor-containers] to collect metrics and logs through a containerized version of the Log Analytics agent for Linux, which is stored in your Log Analytics workspace.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="9b382-181">Sicherheitshinweise</span><span class="sxs-lookup"><span data-stu-id="9b382-181">Security considerations</span></span>

<span data-ttu-id="9b382-182">Verwenden Sie [Azure Security Center][security-center], um sich eine zentrale Übersicht über den Sicherheitszustand Ihrer Azure-Ressourcen zu verschaffen.</span><span class="sxs-lookup"><span data-stu-id="9b382-182">Use [Azure Security Center][security-center] to get a central view of the security state of your Azure resources.</span></span> <span data-ttu-id="9b382-183">Das Azure Security Center überwacht potenzielle Sicherheitsprobleme und bietet eine umfassende Darstellung der Sicherheitsintegrität Ihrer Bereitstellung, überwacht jedoch keine AKS-Agent-Knoten.</span><span class="sxs-lookup"><span data-stu-id="9b382-183">Security Center monitors potential security issues and provides a comprehensive picture of the security health of your deployment, although it doesn't monitor AKS agent nodes.</span></span> <span data-ttu-id="9b382-184">Security Center wird für jedes Azure-Abonnement individuell konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="9b382-184">Security Center is configured per Azure subscription.</span></span> <span data-ttu-id="9b382-185">Aktivieren Sie die Erfassung von Sicherheitsdaten wie unter [Einbinden Ihres Azure-Abonnements in Security Center Standard][get-started] beschrieben.</span><span class="sxs-lookup"><span data-stu-id="9b382-185">Enable security data collection as described in [Onboard your Azure subscription to Security Center Standard][get-started].</span></span> <span data-ttu-id="9b382-186">Nachdem die Datensammlung aktiviert wurde, durchsucht Security Center VMs automatisch, die unter diesem Abonnement erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="9b382-186">When data collection is enabled, Security Center automatically scans any VMs created under that subscription.</span></span>

<span data-ttu-id="9b382-187">**Vorgänge**.</span><span class="sxs-lookup"><span data-stu-id="9b382-187">**Operations**.</span></span> <span data-ttu-id="9b382-188">Wenn Sie sich mit Ihrem Azure Active Directory-Authentifizierungstoken (Azure AD) bei einem AKS-Cluster anmelden möchten, konfigurieren Sie AKS zur Verwendung von Azure AD für die [Benutzerauthentifizierung][aad-auth].</span><span class="sxs-lookup"><span data-stu-id="9b382-188">To sign in to an AKS cluster using your Azure Active Directory (Azure AD) authentication token, configure AKS to use Azure AD for [user authentication][aad-auth].</span></span> <span data-ttu-id="9b382-189">Clusteradministratoren können auch die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) von Kubernetes auf der Grundlage einer Benutzeridentität oder Verzeichnisgruppenmitgliedschaft konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="9b382-189">Cluster administrators can also configure Kubernetes role-based access control (RBAC) based on a user's identity or directory group membership.</span></span>

<span data-ttu-id="9b382-190">Steuern Sie den Zugriff auf die von Ihnen bereitgestellten Azure-Ressourcen mit [RBAC][rbac].</span><span class="sxs-lookup"><span data-stu-id="9b382-190">Use [RBAC][rbac] to control access to the Azure resources that you deploy.</span></span> <span data-ttu-id="9b382-191">Mithilfe der RBAC können Sie Mitglieder Ihres DevOps-Teams Autorisierungsrollen zuweisen.</span><span class="sxs-lookup"><span data-stu-id="9b382-191">RBAC lets you assign authorization roles to members of your DevOps team.</span></span> <span data-ttu-id="9b382-192">Ein Benutzer kann mehreren Rollen zugewiesen werden. Außerdem können Sie für noch präzisere [Berechtigungen] benutzerdefinierte Rollen erstellen.</span><span class="sxs-lookup"><span data-stu-id="9b382-192">A user can be assigned to multiple roles, and you can create custom roles for even more fine-grained [permissions].</span></span>

<span data-ttu-id="9b382-193">**HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="9b382-193">**HTTPS**.</span></span> <span data-ttu-id="9b382-194">Als bewährte Sicherheitsmethode sollte die Anwendung HTTPS erzwingen und HTTP-Anforderungen umleiten.</span><span class="sxs-lookup"><span data-stu-id="9b382-194">As a security best practice, the application should enforce HTTPS and redirect HTTP requests.</span></span> <span data-ttu-id="9b382-195">Verwenden Sie einen [Eingangscontroller][ingress-controller], um einen Reverseproxy bereitzustellen, der SSL beendet und HTTP-Anforderungen umleitet.</span><span class="sxs-lookup"><span data-stu-id="9b382-195">Use an [ingress controller][ingress-controller] to deploy a reverse proxy that terminates SSL and redirects HTTP requests.</span></span> <span data-ttu-id="9b382-196">Weitere Informationen finden Sie unter [Erstellen eines HTTPS-Eingangscontrollers in Azure Kubernetes Service (AKS)][https-ingress].</span><span class="sxs-lookup"><span data-stu-id="9b382-196">For more information, see [Create an HTTPS ingress controller on Azure Kubernetes Service (AKS)][https-ingress].</span></span>

<span data-ttu-id="9b382-197">**Authentifizierung**.</span><span class="sxs-lookup"><span data-stu-id="9b382-197">**Authentication**.</span></span> <span data-ttu-id="9b382-198">Diese Lösung beschränkt den Zugriff auf die Endpunkte nicht.</span><span class="sxs-lookup"><span data-stu-id="9b382-198">This solution doesn't restrict access to the endpoints.</span></span> <span data-ttu-id="9b382-199">Wenn Sie die Architektur in einer Unternehmensumgebung bereitstellen, sichern Sie die Endpunkte über API-Schlüssel, und fügen Sie der Clientanwendung eine Benutzerauthentifizierung hinzu.</span><span class="sxs-lookup"><span data-stu-id="9b382-199">To deploy the architecture in an enterprise setting, secure the endpoints through API keys and add some form of user authentication to the client application.</span></span>

<span data-ttu-id="9b382-200">**Containerregistrierung**.</span><span class="sxs-lookup"><span data-stu-id="9b382-200">**Container registry**.</span></span> <span data-ttu-id="9b382-201">Diese Lösung verwendet eine öffentliche Registrierung zum Speichern des Docker-Images.</span><span class="sxs-lookup"><span data-stu-id="9b382-201">This solution uses a public registry to store the Docker image.</span></span> <span data-ttu-id="9b382-202">Der Code, von dem die Anwendung abhängig ist, und das Modell sind in diesem Image enthalten.</span><span class="sxs-lookup"><span data-stu-id="9b382-202">The code that the application depends on, and the model, are contained within this image.</span></span> <span data-ttu-id="9b382-203">Unternehmensanwendungen sollten eine private Registrierung verwenden, um Schutz vor Schadsoftware bereitzustellen und zu verhindern, dass die Informationen im Container kompromittiert werden.</span><span class="sxs-lookup"><span data-stu-id="9b382-203">Enterprise applications should use a private registry to help guard against running malicious code and to help keep the information inside the container from being compromised.</span></span>

<span data-ttu-id="9b382-204">**DDoS Protection**.</span><span class="sxs-lookup"><span data-stu-id="9b382-204">**DDoS protection**.</span></span> <span data-ttu-id="9b382-205">Aktivieren Sie ggf. [Azure DDoS Protection Standard][ddos].</span><span class="sxs-lookup"><span data-stu-id="9b382-205">Consider enabling [DDoS Protection Standard][ddos].</span></span> <span data-ttu-id="9b382-206">DDoS Protection Basic wird als Teil der Azure-Plattform aktiviert. DDoS Protection Standard bietet jedoch Funktionen zur Risikominderung, die speziell für Azure Virtual Network-Ressourcen optimiert sind.</span><span class="sxs-lookup"><span data-stu-id="9b382-206">Although basic DDoS protection is enabled as part of the Azure platform, DDoS Protection Standard provides mitigation capabilities that are tuned specifically to Azure virtual network resources.</span></span>

<span data-ttu-id="9b382-207">**Protokollierung**:</span><span class="sxs-lookup"><span data-stu-id="9b382-207">**Logging**.</span></span> <span data-ttu-id="9b382-208">Wenden Sie vor dem Speichern von Protokolldaten bewährte Methoden an. Bereinigen Sie beispielsweise Benutzerkennwörter und andere Informationen, die ein potenzielles Sicherheitsrisiko darstellen und zu betrügerischen Zwecken verwendet werden könnten.</span><span class="sxs-lookup"><span data-stu-id="9b382-208">Use best practices before storing log data, such as scrubbing user passwords and other information that could be used to commit security fraud.</span></span>

## <a name="deployment"></a><span data-ttu-id="9b382-209">Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="9b382-209">Deployment</span></span>

<span data-ttu-id="9b382-210">Befolgen Sie die Schritte im GitHub-Repository, um diese Referenzarchitektur bereitzustellen:</span><span class="sxs-lookup"><span data-stu-id="9b382-210">To deploy this reference architecture, follow the steps described in the GitHub repos:</span></span> 

  - <span data-ttu-id="9b382-211">[Reguläre Python-Modelle][github-python]</span><span class="sxs-lookup"><span data-stu-id="9b382-211">[Regular Python models][github-python]</span></span>
  - <span data-ttu-id="9b382-212">[Deep Learning-Modelle][github-dl]</span><span class="sxs-lookup"><span data-stu-id="9b382-212">[Deep learning models][github-dl]</span></span>

[aad-auth]: /azure/aks/aad-integration
[acr]: /azure/container-registry/
[something]: https://kubernetes.io/docs/reference/access-authn-authz/authentication/
[aks]: /azure/aks/intro-kubernetes
[autoscaler]: /azure/aks/autoscaler
[autoscale-pods]: /azure/aks/tutorial-kubernetes-scale#autoscale-pods
[azcopy]: /azure/storage/common/storage-use-azcopy-linux
[ddos]: /azure/virtual-network/ddos-protection-overview
[docker]: https://hub.docker.com/
[get-started]: /azure/security-center/security-center-get-started
[github-python]: https://github.com/Azure/MLAKSDeployment
[github-dl]: https://github.com/Microsoft/AKSDeploymentTutorial
[gpus-vs-cpus]: https://azure.microsoft.com/en-us/blog/gpus-vs-cpus-for-deployment-of-deep-learning-models/
[https-ingress]: /azure/aks/ingress-tls
[ingress-controller]: https://kubernetes.io/docs/concepts/services-networking/ingress/
[kubectl]: https://kubernetes.io/docs/tasks/tools/install-kubectl/
[lb]: /azure/load-balancer/load-balancer-overview
[manually-scale-pods]: /azure/aks/tutorial-kubernetes-scale#manually-scale-pods
[monitor-containers]: /azure/monitoring/monitoring-container-insights-overview
[Berechtigungen]: /azure/aks/concepts-identity
[permissions]: /azure/aks/concepts-identity
[rbac]: /azure/active-directory/role-based-access-control-what-is
[scale-cluster]: /azure/aks/scale-cluster
[scikit]: https://pypi.org/project/scikit-learn/
[security-center]: /azure/security-center/security-center-intro
[vm]: /azure/virtual-machines/
