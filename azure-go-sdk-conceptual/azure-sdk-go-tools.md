---
title: Strumenti per gli sviluppatori Go
description: Strumenti per l'uso di Azure SDK per Go e dei servizi di Azure
keywords: azure, go, golang, azure, visual studio, visual studio code
author: sptramer
ms.author: sttramer
ms.date: 01/30/2018
ms.topic: article
ms.devlang: go
manager: routlaw
ms.openlocfilehash: 4753775e608b39c6da43d64fd08c1532e03d5810
ms.sourcegitcommit: aaa8c37880332625f858a38f5918e6cf581bf48d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="08b13-104">Strumenti per gli sviluppatori che usano Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="08b13-104">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="08b13-105">Per scrivere in modo efficiente codice di Go e assicurarsi che funzioni correttamente con i servizi di Azure sono disponibili alcuni strumenti consigliati.</span><span class="sxs-lookup"><span data-stu-id="08b13-105">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli-20"></a><span data-ttu-id="08b13-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="08b13-106">Azure CLI 2.0</span></span>

<span data-ttu-id="08b13-107">L'interfaccia della riga di comando di Azure 2.0 fornisce un'interfaccia della riga di comando per la creazione e la configurazione delle risorse di Azure nelle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="08b13-107">The Azure 2.0 CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="08b13-108">L'interfaccia della riga di comando può semplificare le operazioni iniziali per la creazione rapida di risorse comuni e condivise di Azure, per consentire agli sviluppatori di concentrarsi sull'utilizzo più complesso dei servizi.</span><span class="sxs-lookup"><span data-stu-id="08b13-108">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="08b13-109">L'interfaccia della riga di comando è multipiattaforma e include funzionalità per query e filtri, che consentono di inviare tramite pipe l'output direttamente agli strumenti preferiti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="08b13-109">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="08b13-110">L'interfaccia della riga di comando è disponibile per l'installazione nel sistema locale, come immagine Docker, o tramite [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="08b13-110">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08b13-111">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="08b13-111">Install the Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="08b13-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="08b13-112">Visual Studio Code</span></span>

<span data-ttu-id="08b13-113">Visual Studio Code è un editor leggero che include il supporto completo per il linguaggio Go tramite le estensioni.</span><span class="sxs-lookup"><span data-stu-id="08b13-113">Visual Studio Code is a lightweight editor that has comprehensive support for the Go language through extensions.</span></span> <span data-ttu-id="08b13-114">Queste estensioni includono il supporto per funzionalità quali il completamento automatico, i modelli di `impl`, il refactoring e il debug.</span><span class="sxs-lookup"><span data-stu-id="08b13-114">These extensions include support for features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="08b13-115">Visual Studio Code offre anche molte estensioni per gli strumenti comuni per gli sviluppatori, ad esempio il controllo del codice sorgente, e offre anche estensioni per interazioni dirette con i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="08b13-115">Visual Studio Code also offers many extensions for common developer tools such as source control, and even offers extensions for direct interactions with Azure services.</span></span> <span data-ttu-id="08b13-116">Microsoft gestisce una metaestensione ufficiale che include queste estensioni di Azure, tra cui un'interfaccia interattiva per l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="08b13-116">Microsoft maintains an official meta-extension including these Azure extensions, including an interactive interface for the Azure CLI.</span></span>

* [<span data-ttu-id="08b13-117">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="08b13-117">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="08b13-118">Ottenere l'estensione di Visual Studio Code per Go</span><span class="sxs-lookup"><span data-stu-id="08b13-118">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="08b13-119">Ottenere l'estensione Strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="08b13-119">Get the Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="08b13-120">Gestione delle dipendenze con dep</span><span class="sxs-lookup"><span data-stu-id="08b13-120">Dependency management with dep</span></span>

<span data-ttu-id="08b13-121">È possibile gestire le dipendenze dei pacchetti ed eseguire il vendoring con Go in molti modi, poiché non è ancora disponibile una soluzione ufficiale.</span><span class="sxs-lookup"><span data-stu-id="08b13-121">There are many ways to manage your package dependencies and do vendoring with Go, since there is no official solution yet.</span></span> <span data-ttu-id="08b13-122">Per eseguire questa gestione è consigliabile usare la gestione dipendenze di `dep`.</span><span class="sxs-lookup"><span data-stu-id="08b13-122">The recommended way to perform this management is with the `dep` dependency manager.</span></span> <span data-ttu-id="08b13-123">Azure SDK per Go usa dep per il rispettivo vendoring ed è garantita la ricezione corretta delle dipendenze per qualsiasi altro progetto che usa dep.</span><span class="sxs-lookup"><span data-stu-id="08b13-123">The Azure SDK for Go uses dep for its vendoring, and is guaranteed to correctly get dependencies for any other project using dep.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08b13-124">Ottenere la gestione dipendenze di dep</span><span class="sxs-lookup"><span data-stu-id="08b13-124">Get the dep dependency manager</span></span>](https://github.com/tools/godep)

## <a name="telemetry-with-application-insights"></a><span data-ttu-id="08b13-125">Telemetria con Application Insights</span><span class="sxs-lookup"><span data-stu-id="08b13-125">Telemetry with Application Insights</span></span>

<span data-ttu-id="08b13-126">[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) è un prodotto di analisi che consente di raccogliere con facilità informazioni di telemetria dalle applicazioni ed è integrato con l'ecosistema di Azure, con Visual Studio Team Services e con GitHub.</span><span class="sxs-lookup"><span data-stu-id="08b13-126">[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) is an analytics product that allows you to easily collect telemetry information from your applications and integrates with the Azure ecosystem, Visual Studio Team Services, and GitHub.</span></span> <span data-ttu-id="08b13-127">Può essere usato in molte applicazioni e Microsoft offre Go SDK per Application Insights.</span><span class="sxs-lookup"><span data-stu-id="08b13-127">It can be used in many applications, and Microsoft offers a Go SDK for working with Application Insights.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08b13-128">Ottenere Go SDK per Application Insights</span><span class="sxs-lookup"><span data-stu-id="08b13-128">Get the Application Insights for Go SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Go) 
