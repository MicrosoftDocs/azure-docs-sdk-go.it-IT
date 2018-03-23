---
title: Installazione di Azure SDK per Go
description: Come installare, eseguire il vendoring e configurare Azure SDK per Go.
author: sptramer
ms.author: sttramer
ms.date: 01/30/2018
ms.topic: article
ms.devlang: go
manager: carmonm
ms.openlocfilehash: 580daf4f2e91eabf97e3acd21bda183c559b57da
ms.sourcegitcommit: fcc1786d59d2e32c97a9a8e0748e06f564a961bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="installing-the-azure-sdk-for-go"></a><span data-ttu-id="cd83e-103">Installazione di Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="cd83e-103">Installing the Azure SDK for Go</span></span>

<span data-ttu-id="cd83e-104">Introduzione ad Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="cd83e-104">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="cd83e-105">Questo SDK consente di gestire e interagire con i servizi di Azure dalle applicazioni Go.</span><span class="sxs-lookup"><span data-stu-id="cd83e-105">This SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="cd83e-106">Ottenere Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="cd83e-106">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="cd83e-107">Per usare i BLOB del servizio di archiviazione di Azure è necessario un SDK distinto.</span><span class="sxs-lookup"><span data-stu-id="cd83e-107">Working with Azure Storage Blobs requires a separate SDK.</span></span>

```bash
go get -u -d github.com/Azure/azure-storage-blob-go/...
```

## <a name="vendoring-the-azure-sdk-for-go"></a><span data-ttu-id="cd83e-108">Eseguire il vendoring di Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="cd83e-108">Vendoring the Azure SDK for Go</span></span>

<span data-ttu-id="cd83e-109">È possibile eseguire il vendoring di Azure SDK per Go tramite [dep](https://github.com/golang/dep).</span><span class="sxs-lookup"><span data-stu-id="cd83e-109">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="cd83e-110">Per motivi di stabilità è consigliabile eseguire il vendoring.</span><span class="sxs-lookup"><span data-stu-id="cd83e-110">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="cd83e-111">Per usare il supporto per `dep`, aggiungere `github.com/Azure/azure-sdk-for-go` a una sezione di `[[constraint]]` del file `Gopkg.toml`.</span><span class="sxs-lookup"><span data-stu-id="cd83e-111">In order to use `dep` support, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="cd83e-112">Per eseguire ad esempio il vendoring sulla versione `14.0.0`, aggiungere la voce seguente:</span><span class="sxs-lookup"><span data-stu-id="cd83e-112">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="including-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="cd83e-113">Inclusione di Azure SDK per Go nel progetto</span><span class="sxs-lookup"><span data-stu-id="cd83e-113">Including the Azure SDK for Go in your project</span></span>

<span data-ttu-id="cd83e-114">Per usare i servizi di Azure dal codice di Go, importare eventuali servizi con cui si interagisce e i moduli `autorest` necessari.</span><span class="sxs-lookup"><span data-stu-id="cd83e-114">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="cd83e-115">Si ottiene un elenco completo dei moduli disponibili da GoDoc per i [servizi disponibili](https://godoc.org/github.com/Azure/azure-sdk-for-go) e per i [pacchetti AutoRest](https://godoc.org/github.com/Azure/go-autorest).</span><span class="sxs-lookup"><span data-stu-id="cd83e-115">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="cd83e-116">I pacchetti più comuni necessari da `go-autorest` sono:</span><span class="sxs-lookup"><span data-stu-id="cd83e-116">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="cd83e-117">Pacchetto</span><span class="sxs-lookup"><span data-stu-id="cd83e-117">Package</span></span> | <span data-ttu-id="cd83e-118">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="cd83e-118">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="cd83e-119">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="cd83e-119">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="cd83e-120">Oggetti per la gestione dell'autenticazione del client del servizio</span><span class="sxs-lookup"><span data-stu-id="cd83e-120">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="cd83e-121">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="cd83e-121">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="cd83e-122">Costanti per le interazioni con i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="cd83e-122">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="cd83e-123">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="cd83e-123">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="cd83e-124">Meccanismi di autenticazione per l'accesso ai servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="cd83e-124">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="cd83e-125">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="cd83e-125">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="cd83e-126">Helper di asserzione tipi per l'uso di strutture dei dati di Azure SDK</span><span class="sxs-lookup"><span data-stu-id="cd83e-126">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="cd83e-127">Il controllo delle versioni dei moduli per i servizi di Azure viene eseguito indipendentemente dalle rispettive API dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="cd83e-127">Modules for Azure services are versioned independently from the SDK APIs for them.</span></span> <span data-ttu-id="cd83e-128">Queste versioni sono parte del percorso di importazione del modulo e derivano da una _versione del servizio_ o da un _profilo_.</span><span class="sxs-lookup"><span data-stu-id="cd83e-128">These versions are part of the module import path, and are from either a _service version_ or a _profile_.</span></span> <span data-ttu-id="cd83e-129">È attualmente consigliabile usare una versione specifica del servizio per lo sviluppo e il rilascio.</span><span class="sxs-lookup"><span data-stu-id="cd83e-129">Currently, it is recommended that you use a specific service version for both development and release.</span></span> <span data-ttu-id="cd83e-130">I servizi si trovano nel modulo `services`.</span><span class="sxs-lookup"><span data-stu-id="cd83e-130">Services are located under the `services` module.</span></span> <span data-ttu-id="cd83e-131">Il percorso completo per l'importazione è il nome del servizio, seguito dalla versione in formato `YYYY-MM-DD` e quindi seguito nuovamente dal nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="cd83e-131">The full path for the import is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="cd83e-132">Per includere ad esempio la versione `2017-03-30` del servizio di calcolo:</span><span class="sxs-lookup"><span data-stu-id="cd83e-132">For example, to include the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="cd83e-133">È attualmente consigliabile usare la versione più recente di un servizio, a meno che non esistano motivi specifici per procedere diversamente.</span><span class="sxs-lookup"><span data-stu-id="cd83e-133">Right now it is recommended that you use the latest version of a service, unless you have a reason to do otherwise.</span></span>

<span data-ttu-id="cd83e-134">Se è necessario uno snapshot collettivo dei servizi, è anche possibile selezionare una singola versione del profilo.</span><span class="sxs-lookup"><span data-stu-id="cd83e-134">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="cd83e-135">La versione dell'unico profilo bloccato è ora `2017-03-30`, che potrebbe non includere le funzionalità più recenti dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cd83e-135">Right now, the only locked profile is version `2017-03-30`, which may not have the latest features of services.</span></span> <span data-ttu-id="cd83e-136">I profili sono disponibili nel modulo `profiles`, con la rispettiva versione in formato `YYYY-MM-DD`.</span><span class="sxs-lookup"><span data-stu-id="cd83e-136">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="cd83e-137">I servizi vengono raggruppati sotto la rispettiva versione del profilo.</span><span class="sxs-lookup"><span data-stu-id="cd83e-137">Services are grouped under their profile version.</span></span> <span data-ttu-id="cd83e-138">Per importare ad esempio il modulo di gestione delle risorse di Azure dal profilo `2017-03-09`:</span><span class="sxs-lookup"><span data-stu-id="cd83e-138">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="cd83e-139">Sono disponibili anche profili `preview` e `latest`.</span><span class="sxs-lookup"><span data-stu-id="cd83e-139">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="cd83e-140">L'uso di questi profili non è consigliato.</span><span class="sxs-lookup"><span data-stu-id="cd83e-140">Using them is not recommended.</span></span> <span data-ttu-id="cd83e-141">Questi profili sono versioni incrementali ed è possibile che il comportamento dei servizi cambi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="cd83e-141">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd83e-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd83e-142">Next steps</span></span>

<span data-ttu-id="cd83e-143">Per iniziare a usare Azure SDK per Go, provare a seguire una guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="cd83e-143">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="cd83e-144">Distribuire una macchina virtuale da un modello</span><span class="sxs-lookup"><span data-stu-id="cd83e-144">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="cd83e-145">Trasferire oggetti nell'archivio BLOB di Azure con Azure Blob SDK per Go</span><span class="sxs-lookup"><span data-stu-id="cd83e-145">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="cd83e-146">Connettersi a Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cd83e-146">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="cd83e-147">Per iniziare immediatamente a usare altri servizi in Go SDK, vedere il codice di esempio disponibile.</span><span class="sxs-lookup"><span data-stu-id="cd83e-147">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="cd83e-148">Eseguire l'autenticazione con i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="cd83e-148">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [<span data-ttu-id="cd83e-149">Distribuire nuove macchine virtuali con l'autenticazione SSH</span><span class="sxs-lookup"><span data-stu-id="cd83e-149">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="cd83e-150">Distribuire un'immagine del contenitore in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="cd83e-150">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="cd83e-151">Creare un cluster nel servizio Kubernetes di Azure</span><span class="sxs-lookup"><span data-stu-id="cd83e-151">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="cd83e-152">Usare i servizi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cd83e-152">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="cd83e-153">Tutti gli esempi per Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="cd83e-153">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
