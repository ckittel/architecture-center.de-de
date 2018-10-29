---
title: Dezentralisierte Vertrauensstellung zwischen Banken in Azure
description: Richten Sie eine vertrauenswürdige Umgebung für die Kommunikation und gemeinsame Nutzung von Informationen ein, ohne auf eine zentrale Datenbank zurückzugreifen.
author: vitoc
ms.date: 09/09/2018
ms.openlocfilehash: fe27f885635ce5ae4ce368992affa1a85d7af416
ms.sourcegitcommit: 62945777e519d650159f0f963a2489b6bb6ce094
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2018
ms.locfileid: "48876755"
---
# <a name="decentralized-trust-between-banks-on-azure"></a><span data-ttu-id="04e50-103">Dezentralisierte Vertrauensstellung zwischen Banken in Azure</span><span class="sxs-lookup"><span data-stu-id="04e50-103">Decentralized trust between banks on Azure</span></span>

<span data-ttu-id="04e50-104">Dieses Beispielszenario ist hilfreich für Banken und andere Einrichtungen, die eine vertrauenswürdige Umgebung für die Informationsweitergabe einrichten möchten, ohne auf eine zentralisierte Datenbank zurückzugreifen.</span><span class="sxs-lookup"><span data-stu-id="04e50-104">This example scenario is useful for banks or any other institutions that want to establish a trusted environment for information sharing without resorting to a centralized database.</span></span> <span data-ttu-id="04e50-105">Das Szenario in diesem Beispiel wird zwar im Kontext der Verwaltung von Informationen zur Kreditwürdigkeit zwischen Banken beschrieben, die Architektur eignet sich jedoch für jedes Szenario, in dem eine Gruppe von Organisationen überprüfte Informationen untereinander austauschen möchte, ohne auf ein zentrales, von einem einzelnen Anbieter betriebenes System zurückgreifen zu müssen.</span><span class="sxs-lookup"><span data-stu-id="04e50-105">For the purpose of this example, we will describe the scenario in the context of maintaining credit score information between banks, but the architecture can be applied to any scenario where a consortium of organizations want to share validated information with one another without resorting to the use of a central system ran by one single party.</span></span>

<span data-ttu-id="04e50-106">Die Banken innerhalb eines Finanzsystems beziehen Informationen zur Kreditwürdigkeit und Bonität einer Person traditionell aus zentralisierten Quellen (etwa von einer Wirtschaftsauskunftei).</span><span class="sxs-lookup"><span data-stu-id="04e50-106">Traditionally, banks within a financial system rely on centralized sources such as credit bureaus for information on an individual's credit score and history.</span></span> <span data-ttu-id="04e50-107">Ein zentralisierter Ansatz führt zu einer Konzentration des Betriebsrisikos sowie zu einer mitunter überflüssigen dritten Partei.</span><span class="sxs-lookup"><span data-stu-id="04e50-107">A centralized approach presents a concentration of operational risk and sometimes an unnecessary third party.</span></span>

<span data-ttu-id="04e50-108">Mit DLTs (Distributed Ledger-Technologie) kann ein Bankenkonsortium ein dezentrales System aufbauen, das effizienter arbeitet, besser vor Angriffen geschützt ist und als neue Plattform fungiert, auf der innovative Strukturen implementiert werden können, um traditionelle Herausforderungen in den Bereichen Datenschutz, Geschwindigkeit und Kosten zu lösen.</span><span class="sxs-lookup"><span data-stu-id="04e50-108">With DLTs (distributed ledger technology), a consortium of banks can establish a decentralized system that can be more efficient, less susceptible to attack, and serve as a new platform where innovative structures can be implemented to solve traditional challenges with privacy, speed, and cost.</span></span>

<span data-ttu-id="04e50-109">In diesem Beispiel erfahren Sie, wie Azure-Dienste wie VM-Skalierungsgruppe, Virtual Network, Key Vault, Storage, Load Balancer und Monitor für die schnelle Bereitstellung einer effizienten privaten Ethereum-PoA-Blockchain bereitgestellt werden können, die es den teilnehmenden Banken ermöglicht, ihre eigenen Knoten zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="04e50-109">This example will show you how Azure services such as virtual machine scale set, Virtual Network, Key Vault, Storage, Load Balancer, and Monitor can be quickly provisioned for the deployment of an efficient private Ethereum PoA blockchain where member banks can establish their own nodes.</span></span>

## <a name="relevant-use-cases"></a><span data-ttu-id="04e50-110">Relevante Anwendungsfälle</span><span class="sxs-lookup"><span data-stu-id="04e50-110">Relevant use cases</span></span>

<span data-ttu-id="04e50-111">Folgende Anwendungsfälle verfügen über ähnliche Entwurfsmuster:</span><span class="sxs-lookup"><span data-stu-id="04e50-111">These other uses cases have similar design patterns:</span></span>

* <span data-ttu-id="04e50-112">Verschieben zugeteilter Budgets zwischen verschiedenen Unternehmenseinheiten eines multinationalen Konzerns</span><span class="sxs-lookup"><span data-stu-id="04e50-112">Movement of allocated budgets between different business units of a multinational corporation</span></span>
* <span data-ttu-id="04e50-113">Grenzüberschreitende Zahlungen</span><span class="sxs-lookup"><span data-stu-id="04e50-113">Cross-border payments</span></span>
* <span data-ttu-id="04e50-114">Handelsfinanzierungsszenarien</span><span class="sxs-lookup"><span data-stu-id="04e50-114">Trade finance scenarios</span></span>
* <span data-ttu-id="04e50-115">Treuesysteme mit verschiedenen Unternehmen</span><span class="sxs-lookup"><span data-stu-id="04e50-115">Loyalty systems involving different companies</span></span>
* <span data-ttu-id="04e50-116">Lieferkettensysteme und vieles mehr</span><span class="sxs-lookup"><span data-stu-id="04e50-116">Supply chain ecosystems and many more</span></span>

## <a name="architecture"></a><span data-ttu-id="04e50-117">Architektur</span><span class="sxs-lookup"><span data-stu-id="04e50-117">Architecture</span></span>

![Diagramm einer dezentralisierten Architektur von Vertrauensstellungen für Banken](./media/architecture-decentralized-trust.png)

<span data-ttu-id="04e50-119">In diesem Szenario werden die Back-End-Komponenten behandelt, die erforderlich sind, um ein skalierbares, sicheres und überwachtes privates Blockchainnetzwerk für Unternehmen innerhalb eines Konsortiums mit mindestens zwei Mitgliedern zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="04e50-119">This scenario covers the back-end components that are necessary to create a scalable, secure, and monitored private, enterprise blockchain network within a consortium of two or more members.</span></span> <span data-ttu-id="04e50-120">Über die Details der Bereitstellung dieser Komponenten (in verschiedenen Abonnements und Ressourcengruppen) sowie über die Konnektivitätsanforderungen (VPN oder ExpressRoute) können Sie auf der Grundlage der Richtlinienanforderungen Ihrer Organisation selbst entscheiden.</span><span class="sxs-lookup"><span data-stu-id="04e50-120">Details of how these components are provisioned (that is, within different subscriptions and resource groups) as well as the connectivity requirements (that is, VPN or ExpressRoute) are left for your consideration based on your organization's policy requirements.</span></span> <span data-ttu-id="04e50-121">Der Datenfluss gestaltet sich wie folgt:</span><span class="sxs-lookup"><span data-stu-id="04e50-121">Here's how data flows:</span></span>

1. <span data-ttu-id="04e50-122">Bank A erstellt/aktualisiert den Bonitätsdatensatz, indem sie per JSON-RPC eine Transaktion an das Blockchainnetzwerk sendet.</span><span class="sxs-lookup"><span data-stu-id="04e50-122">Bank A creates/updates an individual's credit record by sending a transaction to the blockchain network via JSON-RPC.</span></span>
2. <span data-ttu-id="04e50-123">Daten fließen vom privaten Anwendungsserver von Bank A an den Azure Load Balancer und anschließend zur Überprüfung an einen virtuellen Knotencomputer der VM-Skalierungsgruppe.</span><span class="sxs-lookup"><span data-stu-id="04e50-123">Data flows from Bank A's private application server to the Azure load balancer and subsequently to a validating node VM on the virtual machine scale set.</span></span>
3. <span data-ttu-id="04e50-124">Das Ethereum-PoA-Netzwerk erstellt zu einem vorgegebenen Zeitpunkt (in diesem Szenario: zwei Sekunden) einen Block.</span><span class="sxs-lookup"><span data-stu-id="04e50-124">The Ethereum PoA network creates a block at a preset time (2 seconds for this scenario).</span></span>
4. <span data-ttu-id="04e50-125">Die Transaktion wird in dem erstellten Block gebündelt und über das Blockchainnetzwerk überprüft.</span><span class="sxs-lookup"><span data-stu-id="04e50-125">The transaction is bundled into the created block and validated across the blockchain network.</span></span>
5. <span data-ttu-id="04e50-126">Bank B kann den von Bank A erstellten Bonitätsdatensatz lesen, indem sie auf ähnliche Weise über JSON-RPC mit ihrem eigenen Knoten kommuniziert.</span><span class="sxs-lookup"><span data-stu-id="04e50-126">Bank B can read the credit record created by bank A by communicating with its own node similarly via JSON-RPC.</span></span>

### <a name="components"></a><span data-ttu-id="04e50-127">Komponenten</span><span class="sxs-lookup"><span data-stu-id="04e50-127">Components</span></span>

* <span data-ttu-id="04e50-128">Virtual Machines in VM-Skalierungsgruppen stellt bedarfsgerechte Computeressourcen zum Hosten der Überprüfungsprozesse für die Blockchain bereit.</span><span class="sxs-lookup"><span data-stu-id="04e50-128">Virtual Machines within Virtual Machine Scale Sets provides the on-demand compute facility to host the validator processes for the blockchain</span></span>
* <span data-ttu-id="04e50-129">Key Vault wird als sicherer Speicher für die privaten Schlüssel der einzelnen Überprüfungen verwendet.</span><span class="sxs-lookup"><span data-stu-id="04e50-129">Key Vault is used as the secure storage facility for the private keys of each validator</span></span>
* <span data-ttu-id="04e50-130">Load Balancer verteilt die RPC-, Peering- und Governance-DApp-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="04e50-130">Load Balancer spreads the RPC, peering, and Governance DApp requests</span></span>
* <span data-ttu-id="04e50-131">Storage hostet persistente Netzwerkinformationen und koordiniert das Leasing.</span><span class="sxs-lookup"><span data-stu-id="04e50-131">Storage hosting persistent network information and coordinating leasing</span></span>
* <span data-ttu-id="04e50-132">Operations Management Suite (eine Sammlung mehrerer Azure-Dienste) liefert Informationen zu verfügbaren Knoten, zu Transaktionen pro Minute und zu Konsortiumsmitgliedern.</span><span class="sxs-lookup"><span data-stu-id="04e50-132">Operations Management Suite (a bundling of a few Azure services) provides insight into available nodes, transactions per minute and consortium members</span></span>

### <a name="alternatives"></a><span data-ttu-id="04e50-133">Alternativen</span><span class="sxs-lookup"><span data-stu-id="04e50-133">Alternatives</span></span>

<span data-ttu-id="04e50-134">In diesem Beispiel wird der Ethereum-PoA-Ansatz verwendet, da er sich gut als Einstiegspunkt für ein Konsortium von Organisationen eignet, das eine vertrauenswürdige, dezentralisierte und transparente Umgebung erstellen möchte, in der die Mitglieder Informationen untereinander austauschen und gemeinsam nutzen können.</span><span class="sxs-lookup"><span data-stu-id="04e50-134">The Ethereum PoA approach is chosen for this example because it is a good entry point for a consortium of organizations that want to create an environment where information can be exchanged and shared with one another easily in a trusted, decentralized, and easy to understand way.</span></span> <span data-ttu-id="04e50-135">Mit den verfügbaren Azure-Lösungsvorlagen kann ein Konsortiumsleiter schnell und bequem eine Ethereum-PoA-Blockchain starten. Darüber hinaus können die Mitgliedsorganisationen des Konsortiums ihre eigenen Azure-Ressourcen innerhalb ihrer eigenen Ressourcengruppe und ihres Abonnements starten, um einem vorhandenen Netzwerk beizutreten.</span><span class="sxs-lookup"><span data-stu-id="04e50-135">The available Azure solution templates also provide a fast and convenient way not just for a consortium leader to start an Ethereum PoA blockchain, but also for member organizations in the consortium to spin up their own Azure resources within their own resource group and subscription to join an existing network.</span></span>

<span data-ttu-id="04e50-136">Bei erweiterten oder anderen Szenarien spielen möglicherweise Aspekte wie der Datenschutz bei Transaktionen eine Rolle.</span><span class="sxs-lookup"><span data-stu-id="04e50-136">For other extended or different scenarios, concerns such as transaction privacy may arise.</span></span> <span data-ttu-id="04e50-137">Ein Beispiel: In einem Szenario mit Wertpapierübertragung sollen die Transaktionen der jeweiligen Konsortiumsmitglieder möglicherweise nicht für die anderen Mitglieder sichtbar sein.</span><span class="sxs-lookup"><span data-stu-id="04e50-137">For example, in a securities transfer scenario, members in a consortium may not want their transactions to be visible even to other members.</span></span> <span data-ttu-id="04e50-138">Es gibt Alternativen zu Ethereum-PoA, die diese Probleme auf eigene Weise lösen:</span><span class="sxs-lookup"><span data-stu-id="04e50-138">Other alternatives to Ethereum PoA exist that addresses these concerns in their own way:</span></span>

* <span data-ttu-id="04e50-139">Corda</span><span class="sxs-lookup"><span data-stu-id="04e50-139">Corda</span></span>
* <span data-ttu-id="04e50-140">Quorum</span><span class="sxs-lookup"><span data-stu-id="04e50-140">Quorum</span></span>
* <span data-ttu-id="04e50-141">Hyperledger</span><span class="sxs-lookup"><span data-stu-id="04e50-141">Hyperledger</span></span>

## <a name="considerations"></a><span data-ttu-id="04e50-142">Überlegungen</span><span class="sxs-lookup"><span data-stu-id="04e50-142">Considerations</span></span>

### <a name="availability"></a><span data-ttu-id="04e50-143">Verfügbarkeit</span><span class="sxs-lookup"><span data-stu-id="04e50-143">Availability</span></span>

<span data-ttu-id="04e50-144">[Azure Monitor][monitor] überwacht das Blockchainnetzwerk kontinuierlich auf Probleme, um die Verfügbarkeit zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="04e50-144">[Azure Monitor][monitor] is used to continuously monitor the blockchain network for issues to ensure availability.</span></span> <span data-ttu-id="04e50-145">Nach erfolgreicher Bereitstellung der Blockchainlösungsvorlage aus diesem Szenario erhalten Sie einen Link zu einem benutzerdefinierten Azure Monitor-basierten Überwachungsdashboard.</span><span class="sxs-lookup"><span data-stu-id="04e50-145">A link to a custom monitoring dashboard based on Azure Monitor will be sent to you upon successful deployment of the blockchain solution template used in this scenario.</span></span> <span data-ttu-id="04e50-146">Das Dashboard zeigt Knoten, die in den letzten 30 Minuten Heartbeats gemeldet haben, sowie weitere hilfreiche Statistiken.</span><span class="sxs-lookup"><span data-stu-id="04e50-146">The dashboard shows nodes that are reporting heartbeats in the past 30 minutes as well as other useful statistics.</span></span> 

<span data-ttu-id="04e50-147">Weitere Verfügbarkeitsthemen finden Sie im Azure Architecture Center in der [Checkliste für die Verfügbarkeit][availability].</span><span class="sxs-lookup"><span data-stu-id="04e50-147">For other availability topics, see the [availability checklist][availability] in the Azure Architecture Center.</span></span>

### <a name="scalability"></a><span data-ttu-id="04e50-148">Skalierbarkeit</span><span class="sxs-lookup"><span data-stu-id="04e50-148">Scalability</span></span>

<span data-ttu-id="04e50-149">Eine verbreitete Sorge bei Blockchains ist häufig die Anzahl von Transaktionen, die eine Blockchain in einem vordefinierten Zeitraum enthalten kann.</span><span class="sxs-lookup"><span data-stu-id="04e50-149">A popular concern for blockchain is the number of transactions that a blockchain can include within a preset amount of time.</span></span> <span data-ttu-id="04e50-150">In diesem Szenario wird Proof-of-Authority verwendet, um im Vergleich zu Proof-of-Work eine bessere Verwaltung der Skalierbarkeit zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="04e50-150">This scenario uses Proof-of-Authority where such scalability can be better managed than Proof-of-Work.</span></span> <span data-ttu-id="04e50-151">In Proof-of-Authority-basierten Netzwerken sind die Konsensteilnehmer bekannt und werden verwaltet. Dadurch eignen sie sich besser für private Blockchains eines Konsortiums von Organisationen, die sich untereinander kennen.</span><span class="sxs-lookup"><span data-stu-id="04e50-151">In Proof-of-Authority based networks, consensus participants are known and managed, making it more suitable for private blockchain for a consortium of organization that knows one another.</span></span> <span data-ttu-id="04e50-152">Parameter wie durchschnittliche Blockzeit, Transaktionen pro Minute und Auslastung von Computeressourcen lassen sich komfortabel über das benutzerdefinierte Dashboard überwachen.</span><span class="sxs-lookup"><span data-stu-id="04e50-152">Parameters such as average block time, transactions per minute and compute resource consumption can be easily monitored via the custom dashboard.</span></span> <span data-ttu-id="04e50-153">Ressourcen können dann auf der Grundlage der Skalierungsanforderungen angepasst werden.</span><span class="sxs-lookup"><span data-stu-id="04e50-153">Resources can then be adjusted accordingly based on scale requirements.</span></span>

<span data-ttu-id="04e50-154">Allgemeine Informationen zur Entwicklung skalierbarer Szenarien finden Sie im Azure Architecture Center in der [Checkliste für die Skalierbarkeit][scalability].</span><span class="sxs-lookup"><span data-stu-id="04e50-154">For general guidance on designing scalable scenario, see the [scalability checklist][scalability] in the Azure Architecture Center.</span></span>

### <a name="security"></a><span data-ttu-id="04e50-155">Sicherheit</span><span class="sxs-lookup"><span data-stu-id="04e50-155">Security</span></span>

<span data-ttu-id="04e50-156">[Azure Key Vault][vault] dient zum komfortablen Speichern und Verwalten der privaten Schlüssel von Überprüfungen.</span><span class="sxs-lookup"><span data-stu-id="04e50-156">[Azure Key Vault][vault] is used to easily store and manage the private keys of validators.</span></span> <span data-ttu-id="04e50-157">Die Standardbereitstellung in diesem Beispiel erstellt ein Blockchainnetzwerk, auf das über das Internet zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="04e50-157">The default deployment in this example creates a blockchain network that is accessible via the internet.</span></span> <span data-ttu-id="04e50-158">In einem Produktionsszenario, in dem ein privates Netzwerk benötigt wird, können die Mitglieder über VNET-zu-VNET-VPN-Gatewayverbindungen miteinander verbunden werden.</span><span class="sxs-lookup"><span data-stu-id="04e50-158">For production scenario where a private network is desired, members can be connected to each other via VNet-to-VNet VPN gateway connections.</span></span> <span data-ttu-id="04e50-159">Die Schritte zum Konfigurieren eines VPN finden Sie weiter unten im Abschnitt mit den zugehörigen Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="04e50-159">The steps for configuring a VPN are included in the related resources section below.</span></span>

<span data-ttu-id="04e50-160">Allgemeine Informationen zur Entwicklung sicherer Lösungen finden Sie in der [Dokumentation zur Azure-Sicherheit][security].</span><span class="sxs-lookup"><span data-stu-id="04e50-160">For general guidance on designing secure solutions, see the [Azure Security Documentation][security].</span></span>

### <a name="resiliency"></a><span data-ttu-id="04e50-161">Resilienz</span><span class="sxs-lookup"><span data-stu-id="04e50-161">Resiliency</span></span>

<span data-ttu-id="04e50-162">Die Ethereum-PoA-Blockchain bietet selbst ein gewisses Maß an Resilienz, da die Überprüfungsknoten in unterschiedlichen Regionen bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="04e50-162">The Ethereum PoA blockchain can itself provide some degree of resilience as the validator nodes can be deployed in different regions.</span></span> <span data-ttu-id="04e50-163">In Azure stehen Optionen für Bereitstellungen in mehr als 54 Regionen auf der ganzen Welt bereit.</span><span class="sxs-lookup"><span data-stu-id="04e50-163">Azure has options for deployments in over 54 regions worldwide.</span></span> <span data-ttu-id="04e50-164">Eine Blockchain wie in diesem Szenario bietet einzigartige und innovative Möglichkeiten der Zusammenarbeit, um die Resilienz zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="04e50-164">A blockchain such as the one in this scenario provides unique and refreshing possibilities of cooperation to increase resilience.</span></span> <span data-ttu-id="04e50-165">Die Resilienz des Netzwerks wird nicht nur durch eine einzelne zentrale Partei gewährleistet, sondern durch alle Mitglieder des Konsortiums.</span><span class="sxs-lookup"><span data-stu-id="04e50-165">The resilience of the network is not just provided for by a single centralized party but all members of the consortium.</span></span> <span data-ttu-id="04e50-166">Bei einer Proof-of-Authority-basierten Blockchain ist die Netzwerkresilienz noch besser planbar.</span><span class="sxs-lookup"><span data-stu-id="04e50-166">A Proof-of-Authority based blockchain allows network resilience to be even more planned and deliberate.</span></span>

<span data-ttu-id="04e50-167">Allgemeine Informationen zur Entwicklung robuster Lösungen finden Sie unter [Entwerfen robuster Anwendungen für Azure][resiliency].</span><span class="sxs-lookup"><span data-stu-id="04e50-167">For general guidance on designing resilient solutions, see [Designing resilient applications for Azure][resiliency].</span></span>

## <a name="pricing"></a><span data-ttu-id="04e50-168">Preise</span><span class="sxs-lookup"><span data-stu-id="04e50-168">Pricing</span></span>

<span data-ttu-id="04e50-169">Zur Ermittlung der Betriebskosten für dieses Szenario sind alle Dienste im Kostenrechner vorkonfiguriert.</span><span class="sxs-lookup"><span data-stu-id="04e50-169">To explore the cost of running this scenario, all of the services are pre-configured in the cost calculator.</span></span> <span data-ttu-id="04e50-170">Wenn Sie wissen möchten, welche Kosten für Ihren spezifischen Anwendungsfall entstehen, passen Sie die entsprechenden Variablen an Ihre voraussichtlichen Leistungs- und Verfügbarkeitsanforderungen an.</span><span class="sxs-lookup"><span data-stu-id="04e50-170">To see how the pricing would change for your particular use case, change the appropriate variables to match your expected performance and availability requirements.</span></span>

<span data-ttu-id="04e50-171">Wir haben basierend auf der Anzahl von VM-Instanzen, über die Ihre Anwendungen ausgeführt werden, drei Beispielkostenprofile bereitgestellt. (Die Instanzen können sich in unterschiedlichen Regionen befinden.)</span><span class="sxs-lookup"><span data-stu-id="04e50-171">We have provided three sample cost profiles based on the number of scale set VM instances that run your applications (the instances can reside in different regions).</span></span>

* <span data-ttu-id="04e50-172">[Klein:][small-pricing] Dieses Preisbeispiel umfasst zwei virtuelle Computer pro Monat ohne Überwachung.</span><span class="sxs-lookup"><span data-stu-id="04e50-172">[Small][small-pricing]: this pricing example correlates to 2 VMs per month with monitoring turned off</span></span>
* <span data-ttu-id="04e50-173">[Mittel:][medium-pricing] Dieses Preisbeispiel umfasst sieben virtuelle Computer pro Monat mit aktivierter Überwachung.</span><span class="sxs-lookup"><span data-stu-id="04e50-173">[Medium][medium-pricing]: this pricing example correlates to 7 VMs per month with monitoring turned on</span></span>
* <span data-ttu-id="04e50-174">[Groß:][large-pricing] Dieses Preisbeispiel umfasst 15 virtuelle Computer pro Monat mit aktivierter Überwachung.</span><span class="sxs-lookup"><span data-stu-id="04e50-174">[Large][large-pricing]: this pricing example correlates to 15 VMs per month with monitoring turned on</span></span>

<span data-ttu-id="04e50-175">Die oben aufgeführten Preise gelten für ein einzelnes Konsortiumsmitglied, das ein Blockchainnetzwerk startet oder einem solchen Netzwerk beitritt.</span><span class="sxs-lookup"><span data-stu-id="04e50-175">The above pricing is for one consortium member to start or join a blockchain network.</span></span> <span data-ttu-id="04e50-176">In einem Konsortium mit mehreren Unternehmen oder Organisationen erhält für gewöhnlich jedes Mitglied ein eigenes Azure-Abonnement.</span><span class="sxs-lookup"><span data-stu-id="04e50-176">Typically in a consortium where there are multiple companies or organizations involved, each member will get their own Azure subscription.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04e50-177">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="04e50-177">Next Steps</span></span>

<span data-ttu-id="04e50-178">Wenn Sie sich ein Beispiel für dieses Szenario ansehen möchten, stellen Sie die [Demoanwendung für die Ethereum-PoA-Blockchain][deploy] in Azure bereit, und lesen Sie sich anschließend die [Infodatei des Quellcodes für das Szenario][source] durch.</span><span class="sxs-lookup"><span data-stu-id="04e50-178">To see an example of this scenario, deploy the [Ethereum PoA blockchain demo application][deploy] on Azure, then go through the [README of the scenario source code][source].</span></span>

## <a name="related-resources"></a><span data-ttu-id="04e50-179">Zugehörige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="04e50-179">Related resources</span></span>

<span data-ttu-id="04e50-180">Weitere Informationen zur Verwendung der Ethereum-Proof-of-Authority-Lösungsvorlage für Azure finden Sie in [diesem Benutzerhandbuch][guide].</span><span class="sxs-lookup"><span data-stu-id="04e50-180">For more information on using the Ethereum Proof-of-Authority solution template for Azure, review this [usage guide][guide].</span></span>

<!-- links -->
[small-pricing]: https://azure.com/e/4e429d721eb54adc9a1558fae3e67990
[medium-pricing]: https://azure.com/e/bb42cd77437744be8ed7064403bfe2ef
[large-pricing]: https://azure.com/e/e205b443de3e4adfadf4e09ffee30c56
[guide]: /azure/blockchain-workbench/ethereum-poa-deployment
[deploy]: https://portal.azure.com/?pub_source=email&pub_status=success#create/microsoft-azure-blockchain.azure-blockchain-ethereumethereum-poa-consortium
[source]: https://github.com/vitoc/creditscoreblockchain
[monitor]: /azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor
[availability]: /azure/architecture/checklist/availability
[scalability]: /azure/architecture/checklist/scalability
[resiliency]: ../../resiliency/index.md
[security]: /azure/security/
[vault]: https://azure.microsoft.com/services/key-vault/