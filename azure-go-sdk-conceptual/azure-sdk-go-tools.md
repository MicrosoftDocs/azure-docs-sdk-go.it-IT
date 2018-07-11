---
title: Strumenti per gli sviluppatori Go
description: Strumenti per l'uso di Azure SDK per Go e dei servizi di Azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 006d140bffb66fdd769a14511232d4ea5081811d
ms.sourcegitcommit: 181d4e0b164cf39b3feac346f559596bd19c94db
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2018
ms.locfileid: "38066983"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="421e9-103">Strumenti per gli sviluppatori che usano Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="421e9-103">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="421e9-104">Per scrivere in modo efficiente codice di Go e assicurarsi che funzioni correttamente con i servizi di Azure sono disponibili alcuni strumenti consigliati.</span><span class="sxs-lookup"><span data-stu-id="421e9-104">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli-20"></a><span data-ttu-id="421e9-105">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="421e9-105">Azure CLI 2.0</span></span>

<span data-ttu-id="421e9-106">L'interfaccia della riga di comando di Azure 2.0 fornisce un'interfaccia della riga di comando per la creazione e la configurazione delle risorse di Azure nelle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="421e9-106">The Azure 2.0 CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="421e9-107">L'interfaccia della riga di comando può semplificare le operazioni iniziali per la creazione rapida di risorse comuni e condivise di Azure, per consentire agli sviluppatori di concentrarsi sull'utilizzo più complesso dei servizi.</span><span class="sxs-lookup"><span data-stu-id="421e9-107">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="421e9-108">L'interfaccia della riga di comando è multipiattaforma e include funzionalità per query e filtri, che consentono di inviare tramite pipe l'output direttamente agli strumenti preferiti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="421e9-108">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="421e9-109">L'interfaccia della riga di comando è disponibile per l'installazione nel sistema locale, come immagine Docker, o tramite [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="421e9-109">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="421e9-110">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="421e9-110">Install the Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="421e9-111">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="421e9-111">Visual Studio Code</span></span>

<span data-ttu-id="421e9-112">Visual Studio Code è un editor leggero che include il supporto completo per il linguaggio Go tramite le estensioni.</span><span class="sxs-lookup"><span data-stu-id="421e9-112">Visual Studio Code is a lightweight editor that has comprehensive support for the Go language through extensions.</span></span> <span data-ttu-id="421e9-113">Queste estensioni includono il supporto per funzionalità quali il completamento automatico, i modelli di `impl`, il refactoring e il debug.</span><span class="sxs-lookup"><span data-stu-id="421e9-113">These extensions include support for features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="421e9-114">Visual Studio Code offre anche molte estensioni per gli strumenti comuni per gli sviluppatori, ad esempio il controllo del codice sorgente, e offre anche estensioni per interazioni dirette con i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="421e9-114">Visual Studio Code also offers many extensions for common developer tools such as source control, and even offers extensions for direct interactions with Azure services.</span></span> <span data-ttu-id="421e9-115">Microsoft gestisce una metaestensione ufficiale che include queste estensioni di Azure, tra cui un'interfaccia interattiva per l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="421e9-115">Microsoft maintains an official meta-extension including these Azure extensions, including an interactive interface for the Azure CLI.</span></span>

* [<span data-ttu-id="421e9-116">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="421e9-116">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="421e9-117">Ottenere l'estensione di Visual Studio Code per Go</span><span class="sxs-lookup"><span data-stu-id="421e9-117">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="421e9-118">Ottenere l'estensione Strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="421e9-118">Get the Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="421e9-119">Gestione delle dipendenze con dep</span><span class="sxs-lookup"><span data-stu-id="421e9-119">Dependency management with dep</span></span>

<span data-ttu-id="421e9-120">È possibile gestire le dipendenze dei pacchetti ed eseguire il vendoring con Go in molti modi, poiché non è ancora disponibile una soluzione ufficiale.</span><span class="sxs-lookup"><span data-stu-id="421e9-120">There are many ways to manage your package dependencies and do vendoring with Go, since there is no official solution yet.</span></span> <span data-ttu-id="421e9-121">Per eseguire questa gestione è consigliabile usare la gestione dipendenze di `dep`.</span><span class="sxs-lookup"><span data-stu-id="421e9-121">The recommended way to perform this management is with the `dep` dependency manager.</span></span> <span data-ttu-id="421e9-122">Azure SDK per Go usa dep per il rispettivo vendoring ed è garantita la ricezione corretta delle dipendenze per qualsiasi altro progetto che usa dep.</span><span class="sxs-lookup"><span data-stu-id="421e9-122">The Azure SDK for Go uses dep for its vendoring, and is guaranteed to correctly get dependencies for any other project using dep.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="421e9-123">Ottenere la gestione dipendenze di dep</span><span class="sxs-lookup"><span data-stu-id="421e9-123">Get the dep dependency manager</span></span>](https://github.com/golang/dep)
