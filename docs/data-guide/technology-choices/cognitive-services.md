---
title: "Auswählen einer Cognitive Services-Technologie"
description: 
author: zoinerTejada
ms:date: 02/12/2018
ms.openlocfilehash: d97e166abed4670e4bdc797cc8075be3314e677a
ms.sourcegitcommit: 90cf2de795e50571d597cfcb9b302e48933e7f18
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="choosing-a-microsoft-cognitive-services-technology"></a><span data-ttu-id="a64e5-102">Auswählen einer Cognitive Services-Technologie von Microsoft</span><span class="sxs-lookup"><span data-stu-id="a64e5-102">Choosing a Microsoft cognitive services technology</span></span>

<span data-ttu-id="a64e5-103">Microsoft Cognitive Services sind cloudbasierte APIs, die Sie in KI-Anwendungen und -Datenflüssen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="a64e5-103">Microsoft cognitive services are cloud-based APIs that you can use in artificial intelligence (AI) applications and data flows.</span></span> <span data-ttu-id="a64e5-104">Sie umfassen vortrainierte Modelle, die für die Nutzung in Ihrer Anwendung bereit sind und für die Sie keine Daten und kein Modelltraining bereitstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-104">They provide you with pretrained models that are ready to use in your application, requiring no data and no model training on your part.</span></span> <span data-ttu-id="a64e5-105">Cognitive Services werden vom KI- und Forschungsteam von Microsoft entwickelt und umfassen die neuesten Deep Learning-Algorithmen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-105">The cognitive services are developed by Microsoft's AI and Research team and leverage the latest deep learning algorithms.</span></span> <span data-ttu-id="a64e5-106">Sie werden über HTTP-REST-Schnittstellen genutzt.</span><span class="sxs-lookup"><span data-stu-id="a64e5-106">They are consumed over HTTP REST interfaces.</span></span> <span data-ttu-id="a64e5-107">Außerdem sind SDKs für viele gängige Frameworks für die Anwendungsentwicklung verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a64e5-107">In addition, SDKs are available for many common application development frameworks.</span></span>

<span data-ttu-id="a64e5-108">Cognitive Services umfassen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a64e5-108">The cognitive services include:</span></span>

* <span data-ttu-id="a64e5-109">Textanalyse</span><span class="sxs-lookup"><span data-stu-id="a64e5-109">Text analysis</span></span>
* <span data-ttu-id="a64e5-110">Maschinelles Sehen</span><span class="sxs-lookup"><span data-stu-id="a64e5-110">Computer vision</span></span>
* <span data-ttu-id="a64e5-111">Videoanalyse</span><span class="sxs-lookup"><span data-stu-id="a64e5-111">Video analytics</span></span>
* <span data-ttu-id="a64e5-112">Spracherkennung und -generierung</span><span class="sxs-lookup"><span data-stu-id="a64e5-112">Speech recognition and generation</span></span>
* <span data-ttu-id="a64e5-113">Verstehen natürlicher Sprache</span><span class="sxs-lookup"><span data-stu-id="a64e5-113">Natural language understanding</span></span>
* <span data-ttu-id="a64e5-114">Intelligente Suche</span><span class="sxs-lookup"><span data-stu-id="a64e5-114">Intelligent search</span></span>

<span data-ttu-id="a64e5-115">Hauptvorteile:</span><span class="sxs-lookup"><span data-stu-id="a64e5-115">Key benefits:</span></span>

* <span data-ttu-id="a64e5-116">Minimaler Entwicklungsaufwand für modernste KI-Dienste</span><span class="sxs-lookup"><span data-stu-id="a64e5-116">Minimal development effort for state-of-the-art AI services.</span></span>
* <span data-ttu-id="a64e5-117">Einfache Integration in Apps über HTTP-REST-Schnittstellen</span><span class="sxs-lookup"><span data-stu-id="a64e5-117">Easy integration into apps via HTTP REST interfaces.</span></span>
* <span data-ttu-id="a64e5-118">Integrierte Unterstützung der Nutzung von Cognitive Services in Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a64e5-118">Built-in support for consuming cognitive services in Azure Data Lake Analytics.</span></span>

<span data-ttu-id="a64e5-119">Zu berücksichtigende Aspekte:</span><span class="sxs-lookup"><span data-stu-id="a64e5-119">Considerations:</span></span>

* <span data-ttu-id="a64e5-120">Nur über das Web verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a64e5-120">Only available over the web.</span></span> <span data-ttu-id="a64e5-121">Im Allgemeinen ist eine Internetverbindung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="a64e5-121">Internet connectivity is generally required.</span></span> <span data-ttu-id="a64e5-122">Eine Ausnahme ist der Custom Vision Service, dessen trainiertes Modell Sie exportieren können, um Vorhersagen auf Geräten und im IoT-Edgebereich zu treffen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-122">An exception is the Custom Vision Service, whose trained model you can export for prediction on devices and at the IoT edge.</span></span>
* <span data-ttu-id="a64e5-123">Eine umfassende Anpassung wird zwar unterstützt, aber die verfügbaren Dienste sind unter Umständen nicht für alle Predictive Analytics-Anforderungen geeignet.</span><span class="sxs-lookup"><span data-stu-id="a64e5-123">Although considerable customization is supported, the available services may not suit all predictive analytics requirements.</span></span>

## <a name="what-are-your-options-when-choosing-amongst-the-cognitive-services"></a><span data-ttu-id="a64e5-124">Welche Optionen haben Sie bei der Auswahl der Cognitive Services?</span><span class="sxs-lookup"><span data-stu-id="a64e5-124">What are your options when choosing amongst the cognitive services?</span></span>
<span data-ttu-id="a64e5-125">In Azure sind Dutzende von Cognitive Services verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a64e5-125">In Azure, there are dozens of Cognitive Services available.</span></span> <span data-ttu-id="a64e5-126">Die aktuelle Liste ist jeweils in einem Verzeichnis enthalten, das nach dem unterstützten Funktionsbereich kategorisiert ist:</span><span class="sxs-lookup"><span data-stu-id="a64e5-126">The current listing of these is available in a directory categorized by the functional area they support:</span></span>
- [<span data-ttu-id="a64e5-127">Bildanalyse</span><span class="sxs-lookup"><span data-stu-id="a64e5-127">Vision</span></span>](https://azure.microsoft.com/services/cognitive-services/directory/vision/)
- [<span data-ttu-id="a64e5-128">Spracheingabe</span><span class="sxs-lookup"><span data-stu-id="a64e5-128">Speech</span></span>](https://azure.microsoft.com/services/cognitive-services/directory/speech/)
- [<span data-ttu-id="a64e5-129">Einblicke und Wissen</span><span class="sxs-lookup"><span data-stu-id="a64e5-129">Knowledge</span></span>](https://azure.microsoft.com/services/cognitive-services/directory/know/)
- [<span data-ttu-id="a64e5-130">Search</span><span class="sxs-lookup"><span data-stu-id="a64e5-130">Search</span></span>](https://azure.microsoft.com/services/cognitive-services/directory/search/)
- [<span data-ttu-id="a64e5-131">Sprache</span><span class="sxs-lookup"><span data-stu-id="a64e5-131">Language</span></span>](https://azure.microsoft.com/services/cognitive-services/directory/lang/)

## <a name="key-selection-criteria"></a><span data-ttu-id="a64e5-132">Wichtige Auswahlkriterien</span><span class="sxs-lookup"><span data-stu-id="a64e5-132">Key Selection Criteria</span></span>

<span data-ttu-id="a64e5-133">Beantworten Sie zunächst die folgenden Fragen, um die Auswahlmöglichkeiten einzuschränken:</span><span class="sxs-lookup"><span data-stu-id="a64e5-133">To narrow the choices, start by answering these questions:</span></span>

- <span data-ttu-id="a64e5-134">Welche Art von Daten verarbeiten Sie?</span><span class="sxs-lookup"><span data-stu-id="a64e5-134">What type of data are you dealing with?</span></span> <span data-ttu-id="a64e5-135">Grenzen Sie Ihre Optionen basierend auf dem Typ der Eingabedaten ein, die Sie verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="a64e5-135">Narrow your options based on the type of input data you are working with.</span></span> <span data-ttu-id="a64e5-136">Wenn es bei Ihrer Eingabe beispielsweise um Text geht, sollten Sie einen Dienst mit dem Eingabetyp „Text“ wählen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-136">For example, if your input is text, select from the services that have an input type of text.</span></span> 

- <span data-ttu-id="a64e5-137">Verfügen Sie über die Daten zum Trainieren eines Modells?</span><span class="sxs-lookup"><span data-stu-id="a64e5-137">Do you have the data to train a model?</span></span> <span data-ttu-id="a64e5-138">Wenn ja, können Sie die Verwendung der benutzerdefinierten Dienste erwägen, die Ihnen das Trainieren der zugrunde liegenden Modelle mit von Ihnen bereitgestellten Daten ermöglichen, um die Genauigkeit und Leistung zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="a64e5-138">If yes, consider the custom services that enable you to train their underlying models with data that you provide, for improved accuracy and performance.</span></span> 

## <a name="capability-matrix"></a><span data-ttu-id="a64e5-139">Funktionsmatrix</span><span class="sxs-lookup"><span data-stu-id="a64e5-139">Capability matrix</span></span>

<span data-ttu-id="a64e5-140">In den folgenden Tabellen sind die Hauptunterschiede in Bezug auf die Funktionen zusammengefasst:</span><span class="sxs-lookup"><span data-stu-id="a64e5-140">The following tables summarize the key differences in capabilities.</span></span> 

### <a name="uses-prebuilt-models"></a><span data-ttu-id="a64e5-141">Verwendung von vordefinierten Modellen</span><span class="sxs-lookup"><span data-stu-id="a64e5-141">Uses prebuilt models</span></span>
| | <span data-ttu-id="a64e5-142">Eingabetyp</span><span class="sxs-lookup"><span data-stu-id="a64e5-142">Input type</span></span> | <span data-ttu-id="a64e5-143">Hauptvorteil</span><span class="sxs-lookup"><span data-stu-id="a64e5-143">Key benefit</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a64e5-144">Textanalyse-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-144">Text Analytics API</span></span> | <span data-ttu-id="a64e5-145">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-145">Text</span></span> | <span data-ttu-id="a64e5-146">Werten Sie Stimmungen und Themen aus, um zu verstehen, was sich Ihre Benutzer wünschen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-146">Evaluate sentiment and topics to understand what users want.</span></span> |
| <span data-ttu-id="a64e5-147">API für Entitätenverknüpfung</span><span class="sxs-lookup"><span data-stu-id="a64e5-147">Entity Linking API</span></span>| <span data-ttu-id="a64e5-148">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-148">Text</span></span> | <span data-ttu-id="a64e5-149">Erweitern Sie die Datenlinks Ihrer App um die Erkennung und Unterscheidung benannter Entitäten.</span><span class="sxs-lookup"><span data-stu-id="a64e5-149">Power your app's data links with named entity recognition and disambiguation.</span></span> |
| <span data-ttu-id="a64e5-150">Language Understanding Intelligent Service (LUIS)</span><span class="sxs-lookup"><span data-stu-id="a64e5-150">Language Understanding Intelligent Service (LUIS)</span></span>| <span data-ttu-id="a64e5-151">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-151">Text</span></span> | <span data-ttu-id="a64e5-152">Bringen Sie Ihren Apps bei, Befehle Ihrer Benutzer zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-152">Teach your apps to understand commands from your users.</span></span> |
| <span data-ttu-id="a64e5-153">QnA Maker Service</span><span class="sxs-lookup"><span data-stu-id="a64e5-153">QnA Maker Service</span></span>| <span data-ttu-id="a64e5-154">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-154">Text</span></span> | <span data-ttu-id="a64e5-155">Verwandeln Sie Informationen im FAQ-Format in einfach zu findende Antworten.</span><span class="sxs-lookup"><span data-stu-id="a64e5-155">Distill FAQ formatted information into conversational, easy-to-navigate answers.</span></span> |
| <span data-ttu-id="a64e5-156">API für linguistische Analyse</span><span class="sxs-lookup"><span data-stu-id="a64e5-156">Linguistic Analysis API</span></span> | <span data-ttu-id="a64e5-157">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-157">Text</span></span> | <span data-ttu-id="a64e5-158">Vereinfachen Sie komplexe Sprachkonzepte, und analysieren Sie Texte.</span><span class="sxs-lookup"><span data-stu-id="a64e5-158">Simplify complex language concepts and parse text.</span></span> |
| <span data-ttu-id="a64e5-159">Knowledge Exploration Service</span><span class="sxs-lookup"><span data-stu-id="a64e5-159">Knowledge Exploration Service</span></span> | <span data-ttu-id="a64e5-160">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-160">Text</span></span> | <span data-ttu-id="a64e5-161">Ermöglichen Sie die interaktive Suche in strukturierten Daten per Eingabe in natürlicher Sprache.</span><span class="sxs-lookup"><span data-stu-id="a64e5-161">Enable interactive search experiences over structured data via natural language inputs.</span></span> | 
| <span data-ttu-id="a64e5-162">Websprachmodell-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-162">Web Language Model API</span></span> | <span data-ttu-id="a64e5-163">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-163">Text</span></span> | <span data-ttu-id="a64e5-164">Nutzen Sie Vorhersagesprachmodelle, die mit Daten aus dem gesamten Web trainiert wurden.</span><span class="sxs-lookup"><span data-stu-id="a64e5-164">Use predictive language models trained on web-scale data.</span></span> | 
| <span data-ttu-id="a64e5-165">Academic Knowledge-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-165">Academic Knowledge API</span></span> | <span data-ttu-id="a64e5-166">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-166">Text</span></span> | <span data-ttu-id="a64e5-167">Greifen Sie auf die umfangreichen akademischen Inhalte von Microsoft Academic Graph mit Auffüllung per Bing zu.</span><span class="sxs-lookup"><span data-stu-id="a64e5-167">Tap into the wealth of academic content in the Microsoft Academic Graph populated by Bing.</span></span> |
| <span data-ttu-id="a64e5-168">Bing-Vorschlagssuche-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-168">Bing Autosuggest API</span></span> | <span data-ttu-id="a64e5-169">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-169">Text</span></span> | <span data-ttu-id="a64e5-170">Erweitern Sie Ihre App um intelligente Optionen für Vorschläge bei Suchvorgängen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-170">Give your app intelligent autosuggest options for searches.</span></span> |
| <span data-ttu-id="a64e5-171">Bing-Rechtschreibprüfungs-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-171">Bing Spell Check API</span></span> | <span data-ttu-id="a64e5-172">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-172">Text</span></span> | <span data-ttu-id="a64e5-173">Ermitteln und korrigieren Sie Rechtschreibfehler in Ihrer App.</span><span class="sxs-lookup"><span data-stu-id="a64e5-173">Detect and correct spelling mistakes in your app.</span></span> |
| <span data-ttu-id="a64e5-174">Textübersetzungs-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-174">Translator Text API</span></span> | <span data-ttu-id="a64e5-175">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-175">Text</span></span> | <span data-ttu-id="a64e5-176">Maschinelle Übersetzung</span><span class="sxs-lookup"><span data-stu-id="a64e5-176">Machine translation.</span></span> |
| <span data-ttu-id="a64e5-177">Empfehlungs-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-177">Recommendations API</span></span> | <span data-ttu-id="a64e5-178">Text</span><span class="sxs-lookup"><span data-stu-id="a64e5-178">Text</span></span> | <span data-ttu-id="a64e5-179">Sagen Sie vorher, für welche Artikel sich Ihre Kunden interessieren, und empfehlen Sie diese.</span><span class="sxs-lookup"><span data-stu-id="a64e5-179">Predict and recommend items your customers want.</span></span> |
| <span data-ttu-id="a64e5-180">Bing-Entitätssuche-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-180">Bing Entity Search API</span></span> | <span data-ttu-id="a64e5-181">Text (Websuchabfrage)</span><span class="sxs-lookup"><span data-stu-id="a64e5-181">Text (web search query)</span></span> | <span data-ttu-id="a64e5-182">Identifizieren und erweitern Sie Entitätsinformationen aus dem Web.</span><span class="sxs-lookup"><span data-stu-id="a64e5-182">Identify and augment entity information from the web.</span></span> |
| <span data-ttu-id="a64e5-183">Bing-Bildersuche-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-183">Bing Image Search API</span></span> | <span data-ttu-id="a64e5-184">Text (Websuchabfrage)</span><span class="sxs-lookup"><span data-stu-id="a64e5-184">Text (web search query)</span></span> | <span data-ttu-id="a64e5-185">Suchen Sie nach Bildern.</span><span class="sxs-lookup"><span data-stu-id="a64e5-185">Search for images.</span></span> |
| <span data-ttu-id="a64e5-186">Bing-News-Suche-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-186">Bing News Search API</span></span> | <span data-ttu-id="a64e5-187">Text (Websuchabfrage)</span><span class="sxs-lookup"><span data-stu-id="a64e5-187">Text (web search query)</span></span> | <span data-ttu-id="a64e5-188">Suchen Sie nach News.</span><span class="sxs-lookup"><span data-stu-id="a64e5-188">Search for news.</span></span> |
| <span data-ttu-id="a64e5-189">Bing-Videosuche-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-189">Bing Video Search API</span></span> | <span data-ttu-id="a64e5-190">Text (Websuchabfrage)</span><span class="sxs-lookup"><span data-stu-id="a64e5-190">Text (web search query)</span></span> | <span data-ttu-id="a64e5-191">Suchen Sie nach Videos.</span><span class="sxs-lookup"><span data-stu-id="a64e5-191">Search for videos.</span></span> |
| <span data-ttu-id="a64e5-192">Bing-Websuche-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-192">Bing Web Search API</span></span> | <span data-ttu-id="a64e5-193">Text (Websuchabfrage)</span><span class="sxs-lookup"><span data-stu-id="a64e5-193">Text (web search query)</span></span> | <span data-ttu-id="a64e5-194">Erhalten Sie umfassende Suchergebnisse aus Milliarden von Webdokumenten.</span><span class="sxs-lookup"><span data-stu-id="a64e5-194">Get enhanced search details from billions of web documents.</span></span> |<span data-ttu-id="a64e5-195">.</span><span class="sxs-lookup"><span data-stu-id="a64e5-195">.</span></span>
| <span data-ttu-id="a64e5-196">Bing-Spracheingabe-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-196">Bing Speech API</span></span> | <span data-ttu-id="a64e5-197">Text oder Sprache</span><span class="sxs-lookup"><span data-stu-id="a64e5-197">Text or Speech</span></span> | <span data-ttu-id="a64e5-198">Konvertieren Sie Sprache in Text und wieder zurück.</span><span class="sxs-lookup"><span data-stu-id="a64e5-198">Convert speech to text and back again.</span></span> |
| <span data-ttu-id="a64e5-199">Sprechererkennungs-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-199">Speaker Recognition API</span></span> | <span data-ttu-id="a64e5-200">Spracheingabe</span><span class="sxs-lookup"><span data-stu-id="a64e5-200">Speech</span></span> | <span data-ttu-id="a64e5-201">Identifizieren und authentifizieren Sie Sprecher anhand ihrer Stimme.</span><span class="sxs-lookup"><span data-stu-id="a64e5-201">Use speech to identify and authenticate individual speakers.</span></span> |
| <span data-ttu-id="a64e5-202">Sprachübersetzungs-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-202">Translator Speech API</span></span> | <span data-ttu-id="a64e5-203">Spracheingabe</span><span class="sxs-lookup"><span data-stu-id="a64e5-203">Speech</span></span> | <span data-ttu-id="a64e5-204">Führen Sie Sprachübersetzungen in Echtzeit durch.</span><span class="sxs-lookup"><span data-stu-id="a64e5-204">Perform real-time speech translation.</span></span> |
| <span data-ttu-id="a64e5-205">Maschinelles Sehen-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-205">Computer Vision API</span></span> | <span data-ttu-id="a64e5-206">Bilder (oder Frames aus Videos)</span><span class="sxs-lookup"><span data-stu-id="a64e5-206">Images (or frames from video)</span></span> | <span data-ttu-id="a64e5-207">Filtern Sie verwertbare Informationen aus Bildern heraus, nutzen Sie die automatische Erstellung von Fotobeschreibungen, die Ableitung von Tags und die Erkennung von berühmten Personen und die Textextraktion, und erstellen Sie präzise Miniaturansichten.</span><span class="sxs-lookup"><span data-stu-id="a64e5-207">Distill actionable information from images, automatically create description of photos, derive tags, recognize celebrities, extract text, and create accurate thumbnails.</span></span> |
| <span data-ttu-id="a64e5-208">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="a64e5-208">Content Moderator</span></span> | <span data-ttu-id="a64e5-209">Text, Bilder oder Video</span><span class="sxs-lookup"><span data-stu-id="a64e5-209">Text, Images or Video</span></span> | <span data-ttu-id="a64e5-210">Automatisierte Bild-, Text- und Videomoderation</span><span class="sxs-lookup"><span data-stu-id="a64e5-210">Automated image, text, and video moderation.</span></span> |
| <span data-ttu-id="a64e5-211">Emotionen-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-211">Emotion API</span></span> | <span data-ttu-id="a64e5-212">Bilder (Fotos mit Menschen)</span><span class="sxs-lookup"><span data-stu-id="a64e5-212">Images (photos with human subjects)</span></span> | <span data-ttu-id="a64e5-213">Identifizieren Sie den Emotionsbereich von Menschen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-213">Identify the range emotions of human subjects.</span></span> |
| <span data-ttu-id="a64e5-214">Gesichtserkennungs-API</span><span class="sxs-lookup"><span data-stu-id="a64e5-214">Face API</span></span> | <span data-ttu-id="a64e5-215">Bilder (Fotos mit Menschen)</span><span class="sxs-lookup"><span data-stu-id="a64e5-215">Images (photos with human subjects)</span></span> | <span data-ttu-id="a64e5-216">Nutzen Sie die Erkennung, Analyse, Organisation und Markierung von Gesichtern auf Fotos.</span><span class="sxs-lookup"><span data-stu-id="a64e5-216">Detect, identify, analyze, organize, and tag faces in photos.</span></span> |
| <span data-ttu-id="a64e5-217">Video-Indexer</span><span class="sxs-lookup"><span data-stu-id="a64e5-217">Video Indexer</span></span> | <span data-ttu-id="a64e5-218">Video</span><span class="sxs-lookup"><span data-stu-id="a64e5-218">Video</span></span> | <span data-ttu-id="a64e5-219">Führen Sie Videoauswertungen in Bezug auf Stimmung, Sprachtranskription, Sprachübersetzung, Gesichter- und Emotionserkennung und Extraktion von Schlüsselwörtern durch.</span><span class="sxs-lookup"><span data-stu-id="a64e5-219">Video insights such as sentiment, transcript speech, translate speech, recognize faces and emotions, and extract keywords.</span></span> | 

### <a name="trained-with-custom-data-you-provide"></a><span data-ttu-id="a64e5-220">Trainiert mit von Ihnen bereitgestellten benutzerdefinierten Daten</span><span class="sxs-lookup"><span data-stu-id="a64e5-220">Trained with custom data you provide</span></span>
| | <span data-ttu-id="a64e5-221">Eingabetyp</span><span class="sxs-lookup"><span data-stu-id="a64e5-221">Input type</span></span> | <span data-ttu-id="a64e5-222">Hauptvorteil</span><span class="sxs-lookup"><span data-stu-id="a64e5-222">Key benefit</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a64e5-223">Custom Vision Service</span><span class="sxs-lookup"><span data-stu-id="a64e5-223">Custom Vision Service</span></span> | <span data-ttu-id="a64e5-224">Bilder (oder Frames aus Videos)</span><span class="sxs-lookup"><span data-stu-id="a64e5-224">Images (or frames from video)</span></span> | <span data-ttu-id="a64e5-225">Passen Sie Ihre eigenen Modelle für maschinelles Sehen an.</span><span class="sxs-lookup"><span data-stu-id="a64e5-225">Customize your own computer vision models.</span></span> |
| <span data-ttu-id="a64e5-226">Benutzerdefinierter Spracherkennungsdienst</span><span class="sxs-lookup"><span data-stu-id="a64e5-226">Custom Speech Service</span></span> | <span data-ttu-id="a64e5-227">Spracheingabe</span><span class="sxs-lookup"><span data-stu-id="a64e5-227">Speech</span></span> | <span data-ttu-id="a64e5-228">Überwinden Sie die Grenzen der Spracherkennung, z.B. Sprachstil, Hintergrundgeräusche und Vokabular.</span><span class="sxs-lookup"><span data-stu-id="a64e5-228">Overcome speech recognition barriers like speaking style, background noise, and vocabulary.</span></span> | 
| <span data-ttu-id="a64e5-229">Custom Decision Service</span><span class="sxs-lookup"><span data-stu-id="a64e5-229">Custom Decision Service</span></span> | <span data-ttu-id="a64e5-230">Webinhalt (z.B. RSS-Feed)</span><span class="sxs-lookup"><span data-stu-id="a64e5-230">Web content (for example, RSS feed)</span></span> | <span data-ttu-id="a64e5-231">Verwenden Sie Machine Learning, um automatisch die richtigen Inhalte für Ihre Homepage auswählen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="a64e5-231">Use machine learning to automatically select the appropriate content for your home page</span></span> |
| <span data-ttu-id="a64e5-232">API für die benutzerdefinierte Bing-Suche</span><span class="sxs-lookup"><span data-stu-id="a64e5-232">Bing Custom Search API</span></span> | <span data-ttu-id="a64e5-233">Text (Websuchabfrage)</span><span class="sxs-lookup"><span data-stu-id="a64e5-233">Text (web search query)</span></span> | <span data-ttu-id="a64e5-234">Kommerziell einsetzbares Suchtool</span><span class="sxs-lookup"><span data-stu-id="a64e5-234">Commercial-grade search tool.</span></span> |
