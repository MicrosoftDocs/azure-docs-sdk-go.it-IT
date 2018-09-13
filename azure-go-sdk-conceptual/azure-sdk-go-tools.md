---
title: Strumenti per gli sviluppatori che usano Azure SDK per Go
description: Strumenti per l'uso di Azure SDK per Go e dei servizi di Azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 70cf7d645f47df29e8e42599a0acd75858144783
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059204"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="7d78b-103">Strumenti per gli sviluppatori che usano Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="7d78b-103">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="7d78b-104">Per scrivere in modo efficiente codice di Go e assicurarsi che funzioni correttamente con i servizi di Azure sono disponibili alcuni strumenti consigliati.</span><span class="sxs-lookup"><span data-stu-id="7d78b-104">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="7d78b-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7d78b-105">Azure CLI</span></span>

<span data-ttu-id="7d78b-106">L'interfaccia della riga di comando di Azure permette la creazione e la configurazione delle risorse di Azure nelle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="7d78b-106">The Azure CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="7d78b-107">L'interfaccia della riga di comando può semplificare le operazioni iniziali per la creazione rapida di risorse comuni e condivise di Azure, per consentire agli sviluppatori di concentrarsi sull'utilizzo più complesso dei servizi.</span><span class="sxs-lookup"><span data-stu-id="7d78b-107">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="7d78b-108">L'interfaccia della riga di comando è multipiattaforma e include funzionalità per query e filtri, che consentono di inviare tramite pipe l'output direttamente agli strumenti preferiti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="7d78b-108">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="7d78b-109">L'interfaccia della riga di comando è disponibile per l'installazione nel sistema locale, come immagine Docker, o tramite [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="7d78b-109">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d78b-110">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7d78b-110">Install the Azure CLI</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="7d78b-111">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7d78b-111">Visual Studio Code</span></span>

<span data-ttu-id="7d78b-112">Visual Studio Code è un editor leggero che offre supporto per Go.</span><span class="sxs-lookup"><span data-stu-id="7d78b-112">Visual Studio Code is a lightweight editor that offers Go support.</span></span> <span data-ttu-id="7d78b-113">Questa estensione offre funzionalità quali il completamento automatico, i modelli di `impl`, il refactoring e il debug.</span><span class="sxs-lookup"><span data-stu-id="7d78b-113">This extension offers features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="7d78b-114">Visual Studio Code offre anche il supporto per l'accesso nell'editor al controllo del codice sorgente ed estensioni per l'uso dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d78b-114">Visual Studio Code also offers support for in-editor access to source control, and extensions for working with Azure services.</span></span>

* [<span data-ttu-id="7d78b-115">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7d78b-115">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="7d78b-116">Ottenere l'estensione di Visual Studio Code per Go</span><span class="sxs-lookup"><span data-stu-id="7d78b-116">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="7d78b-117">Ottenere l'estensione Visual Studio Code per strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="7d78b-117">Get the Visual Studio Code Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="cicd-with-azure-devops-project"></a><span data-ttu-id="7d78b-118">CI/CD con il progetto DevOps di Azure</span><span class="sxs-lookup"><span data-stu-id="7d78b-118">CI/CD with Azure DevOps Project</span></span>

<span data-ttu-id="7d78b-119">Le pipeline del progetto Azure DevOps consentono di configurare un sistema di integrazione continua per le applicazioni Go.</span><span class="sxs-lookup"><span data-stu-id="7d78b-119">Azure DevOps Project pipelines allow you to set up a continuous integration system for your Go applications.</span></span> <span data-ttu-id="7d78b-120">Per eseguire la distribuzione e i test direttamente in Azure, è sufficiente avere un repository Git.</span><span class="sxs-lookup"><span data-stu-id="7d78b-120">All it takes is a git repo, and you can deploy and test directly on Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d78b-121">Informazioni su come creare una pipeline CI/CD con i progetti DevOps di Azure</span><span class="sxs-lookup"><span data-stu-id="7d78b-121">Learn how to create a CI/CD pipeline with Azure DevOps Project</span></span>](/azure/devops-project/azure-devops-project-go)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="7d78b-122">Gestione delle dipendenze con dep</span><span class="sxs-lookup"><span data-stu-id="7d78b-122">Dependency management with dep</span></span>

<span data-ttu-id="7d78b-123">Azure SDK per Go usa il comando dep per la gestione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="7d78b-123">The Azure SDK for Go uses dep for dependency management.</span></span> <span data-ttu-id="7d78b-124">Il comando dep consente di eseguire il pull dei requisiti del fornitore per l'applicazione Go, evitando conflitti di versione e assicurando il funzionamento corretto del progetto.</span><span class="sxs-lookup"><span data-stu-id="7d78b-124">The dep command allows you to pull and vendor requirements for your Go application, avoiding version conflicts and ensuring that your project works correctly.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d78b-125">Ottenere la gestione dipendenze di dep</span><span class="sxs-lookup"><span data-stu-id="7d78b-125">Get the dep dependency manager</span></span>](https://github.com/golang/dep)
