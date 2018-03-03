---
title: Installazione di Azure SDK per Go
description: Come installare, eseguire il vendoring e configurare Azure SDK per Go.
keywords: azure, sdk, go, golang, azure sdk
author: sptramer
ms.author: sttramer
ms.date: 01/30/2018
ms.topic: article
ms.devlang: go
manager: routlaw
ms.openlocfilehash: 7fc0a3ff71b0b06f616ae43cff311352fe873345
ms.sourcegitcommit: 890f5f01a70e7e376e6bb98a2030afbfc016f538
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2018
---
# <a name="installing-the-azure-sdk-for-go"></a><span data-ttu-id="b1977-104">Installazione di Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="b1977-104">Installing the Azure SDK for Go</span></span>

<span data-ttu-id="b1977-105">Introduzione ad Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="b1977-105">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="b1977-106">Questo SDK consente di gestire e interagire con i servizi di Azure dalle applicazioni Go.</span><span class="sxs-lookup"><span data-stu-id="b1977-106">This SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="b1977-107">Ottenere Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="b1977-107">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="b1977-108">Per usare i BLOB del servizio di archiviazione di Azure è necessario un SDK distinto.</span><span class="sxs-lookup"><span data-stu-id="b1977-108">Working with Azure Storage Blobs requires a separate SDK.</span></span>

```bash
go get -u -d github.com/Azure/azure-storage-blob-go/...
```

## <a name="vendoring-the-azure-sdk-for-go"></a><span data-ttu-id="b1977-109">Eseguire il vendoring di Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="b1977-109">Vendoring the Azure SDK for Go</span></span>

<span data-ttu-id="b1977-110">È possibile eseguire il vendoring di Azure SDK per Go tramite [dep](https://github.com/golang/dep).</span><span class="sxs-lookup"><span data-stu-id="b1977-110">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="b1977-111">Per motivi di stabilità è consigliabile eseguire il vendoring.</span><span class="sxs-lookup"><span data-stu-id="b1977-111">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="b1977-112">Per usare il supporto per `dep`, aggiungere `github.com/Azure/azure-sdk-for-go` a una sezione di `[[constraint]]` del file `Gopkg.toml`.</span><span class="sxs-lookup"><span data-stu-id="b1977-112">In order to use `dep` support, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="b1977-113">Per eseguire ad esempio il vendoring sulla versione `14.0.0`, aggiungere la voce seguente:</span><span class="sxs-lookup"><span data-stu-id="b1977-113">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="including-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="b1977-114">Inclusione di Azure SDK per Go nel progetto</span><span class="sxs-lookup"><span data-stu-id="b1977-114">Including the Azure SDK for Go in your project</span></span>

<span data-ttu-id="b1977-115">Per usare i servizi di Azure dal codice di Go, importare eventuali servizi con cui si interagisce e i moduli `autorest` necessari.</span><span class="sxs-lookup"><span data-stu-id="b1977-115">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="b1977-116">Si ottiene un elenco completo dei moduli disponibili da GoDoc per i [servizi disponibili](https://godoc.org/github.com/Azure/azure-sdk-for-go) e per i [pacchetti AutoRest](https://godoc.org/github.com/Azure/go-autorest).</span><span class="sxs-lookup"><span data-stu-id="b1977-116">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="b1977-117">I pacchetti più comuni necessari da `go-autorest` sono:</span><span class="sxs-lookup"><span data-stu-id="b1977-117">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="b1977-118">Pacchetto</span><span class="sxs-lookup"><span data-stu-id="b1977-118">Package</span></span> | <span data-ttu-id="b1977-119">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="b1977-119">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="b1977-120">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="b1977-120">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="b1977-121">Oggetti per la gestione dell'autenticazione del client del servizio</span><span class="sxs-lookup"><span data-stu-id="b1977-121">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="b1977-122">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="b1977-122">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="b1977-123">Costanti per le interazioni con i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="b1977-123">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="b1977-124">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="b1977-124">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="b1977-125">Meccanismi di autenticazione per l'accesso ai servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="b1977-125">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="b1977-126">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="b1977-126">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="b1977-127">Helper di asserzione tipi per l'uso di strutture dei dati di Azure SDK</span><span class="sxs-lookup"><span data-stu-id="b1977-127">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="b1977-128">Il controllo delle versioni dei moduli per i servizi di Azure viene eseguito indipendentemente dalle rispettive API dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="b1977-128">Modules for Azure services are versioned independently from the SDK APIs for them.</span></span> <span data-ttu-id="b1977-129">Queste versioni sono parte del percorso di importazione del modulo e derivano da una _versione del servizio_ o da un _profilo_.</span><span class="sxs-lookup"><span data-stu-id="b1977-129">These versions are part of the module import path, and are from either a _service version_ or a _profile_.</span></span> <span data-ttu-id="b1977-130">È attualmente consigliabile usare una versione specifica del servizio per lo sviluppo e il rilascio.</span><span class="sxs-lookup"><span data-stu-id="b1977-130">Currently, it is recommended that you use a specific service version for both development and release.</span></span> <span data-ttu-id="b1977-131">I servizi si trovano nel modulo `services`.</span><span class="sxs-lookup"><span data-stu-id="b1977-131">Services are located under the `services` module.</span></span> <span data-ttu-id="b1977-132">Il percorso completo per l'importazione è il nome del servizio, seguito dalla versione in formato `YYYY-MM-DD` e quindi seguito nuovamente dal nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="b1977-132">The full path for the import is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="b1977-133">Per includere ad esempio la versione `2017-03-30` del servizio di calcolo:</span><span class="sxs-lookup"><span data-stu-id="b1977-133">For example, to include the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="b1977-134">È attualmente consigliabile usare la versione più recente di un servizio, a meno che non esistano motivi specifici per procedere diversamente.</span><span class="sxs-lookup"><span data-stu-id="b1977-134">Right now it is recommended that you use the latest version of a service, unless you have a reason to do otherwise.</span></span>

<span data-ttu-id="b1977-135">Se è necessario uno snapshot collettivo dei servizi, è anche possibile selezionare una singola versione del profilo.</span><span class="sxs-lookup"><span data-stu-id="b1977-135">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="b1977-136">La versione dell'unico profilo bloccato è ora `2017-03-30`, che potrebbe non includere le funzionalità più recenti dei servizi.</span><span class="sxs-lookup"><span data-stu-id="b1977-136">Right now, the only locked profile is version `2017-03-30`, which may not have the latest features of services.</span></span> <span data-ttu-id="b1977-137">I profili sono disponibili nel modulo `profiles`, con la rispettiva versione in formato `YYYY-MM-DD`.</span><span class="sxs-lookup"><span data-stu-id="b1977-137">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="b1977-138">I servizi vengono raggruppati sotto la rispettiva versione del profilo.</span><span class="sxs-lookup"><span data-stu-id="b1977-138">Services are grouped under their profile version.</span></span> <span data-ttu-id="b1977-139">Per importare ad esempio il modulo di gestione delle risorse di Azure dal profilo `2017-03-09`:</span><span class="sxs-lookup"><span data-stu-id="b1977-139">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="b1977-140">Sono disponibili anche profili `preview` e `latest`.</span><span class="sxs-lookup"><span data-stu-id="b1977-140">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="b1977-141">L'uso di questi profili non è consigliato.</span><span class="sxs-lookup"><span data-stu-id="b1977-141">Using them is not recommended.</span></span> <span data-ttu-id="b1977-142">Questi profili sono versioni incrementali ed è possibile che il comportamento dei servizi cambi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="b1977-142">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1977-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1977-143">Next steps</span></span>

<span data-ttu-id="b1977-144">Per iniziare a usare Azure SDK per Go, provare a seguire una guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="b1977-144">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="b1977-145">Distribuire una macchina virtuale da un modello</span><span class="sxs-lookup"><span data-stu-id="b1977-145">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="b1977-146">Trasferire oggetti nell'archivio BLOB di Azure con Azure Blob SDK per Go</span><span class="sxs-lookup"><span data-stu-id="b1977-146">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="b1977-147">Connettersi a Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b1977-147">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="b1977-148">Per iniziare immediatamente a usare altri servizi in Go SDK, vedere il codice di esempio disponibile.</span><span class="sxs-lookup"><span data-stu-id="b1977-148">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="b1977-149">Eseguire l'autenticazione con i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="b1977-149">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [<span data-ttu-id="b1977-150">Distribuire nuove macchine virtuali con l'autenticazione SSH</span><span class="sxs-lookup"><span data-stu-id="b1977-150">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="b1977-151">Distribuire un'immagine del contenitore in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="b1977-151">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="b1977-152">Creare un cluster nel servizio Kubernetes di Azure</span><span class="sxs-lookup"><span data-stu-id="b1977-152">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="b1977-153">Usare i servizi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b1977-153">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="b1977-154">Tutti gli esempi per Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="b1977-154">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
