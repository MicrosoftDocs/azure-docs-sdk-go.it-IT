---
title: Installare Azure SDK per Go
description: Come installare, eseguire il vendoring e configurare Azure SDK per Go.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 03/14/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 3388359bba791c87025b6ffd0e6b476f95589f73
ms.sourcegitcommit: 81e97407e6139375bf7357045e818c87a17dcde1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2018
ms.locfileid: "36262981"
---
# <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="18308-103">Installare Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="18308-103">Install the Azure SDK for Go</span></span>

<span data-ttu-id="18308-104">Introduzione ad Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="18308-104">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="18308-105">L'SDK consente di gestire i servizi di Azure dalle applicazioni Go e interagire con essi.</span><span class="sxs-lookup"><span data-stu-id="18308-105">The SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="18308-106">Ottenere Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="18308-106">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="18308-107">Alcuni servizi di Azure includono un proprio SDK per Go e non sono compresi nel pacchetto Azure SDK per Go di base.</span><span class="sxs-lookup"><span data-stu-id="18308-107">Some Azure services have their own Go SDK and aren't included in the core Azure SDK for Go package.</span></span> <span data-ttu-id="18308-108">La tabella seguente elenca i servizi con SDK propri e i relativi nomi di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="18308-108">The following table lists the services with their own SDKs and their package names.</span></span> <span data-ttu-id="18308-109">Questi pacchetti vengono tutti considerati in anteprima.</span><span class="sxs-lookup"><span data-stu-id="18308-109">These packages are all considered to be in preview.</span></span>

| <span data-ttu-id="18308-110">Service</span><span class="sxs-lookup"><span data-stu-id="18308-110">Service</span></span> | <span data-ttu-id="18308-111">Pacchetto</span><span class="sxs-lookup"><span data-stu-id="18308-111">Package</span></span> |
|---------|---------|
| <span data-ttu-id="18308-112">Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="18308-112">Blob Storage</span></span> | [<span data-ttu-id="18308-113">github.com/Azure/azure-storage-blob-go</span><span class="sxs-lookup"><span data-stu-id="18308-113">github.com/Azure/azure-storage-blob-go</span></span>](https://github.com/Azure/azure-storage-blob-go) |
| <span data-ttu-id="18308-114">Archiviazione file</span><span class="sxs-lookup"><span data-stu-id="18308-114">File Storage</span></span> | [<span data-ttu-id="18308-115">github.com/Azure/azure-storage-file-go</span><span class="sxs-lookup"><span data-stu-id="18308-115">github.com/Azure/azure-storage-file-go</span></span>](https://github.com/Azure/azure-storage-file-go) |
| <span data-ttu-id="18308-116">Coda di archiviazione</span><span class="sxs-lookup"><span data-stu-id="18308-116">Storage Queue</span></span> | [<span data-ttu-id="18308-117">github.com/Azure/azure-storage-queue-go</span><span class="sxs-lookup"><span data-stu-id="18308-117">github.com/Azure/azure-storage-queue-go</span></span>](https://github.com/Azure/azure-storage-queue-go) |
| <span data-ttu-id="18308-118">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="18308-118">Event Hub</span></span> | [<span data-ttu-id="18308-119">github.com/Azure/azure-event-hubs-go</span><span class="sxs-lookup"><span data-stu-id="18308-119">github.com/Azure/azure-event-hubs-go</span></span>](https://github.com/Azure/azure-event-hubs-go) |
| <span data-ttu-id="18308-120">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="18308-120">Service Bus</span></span> | [<span data-ttu-id="18308-121">github.com/Azure/azure-service-bus-go</span><span class="sxs-lookup"><span data-stu-id="18308-121">github.com/Azure/azure-service-bus-go</span></span>](https://github.com/Azure/azure-service-bus-go) |
| <span data-ttu-id="18308-122">Application Insights</span><span class="sxs-lookup"><span data-stu-id="18308-122">Application Insights</span></span> | [<span data-ttu-id="18308-123">github.com/Microsoft/ApplicationInsights-go</span><span class="sxs-lookup"><span data-stu-id="18308-123">github.com/Microsoft/ApplicationInsights-go</span></span>](https://github.com/Microsoft/ApplicationInsights-go) |

## <a name="vendor-the-azure-sdk-for-go"></a><span data-ttu-id="18308-124">Eseguire il vendoring di Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="18308-124">Vendor the Azure SDK for Go</span></span>

<span data-ttu-id="18308-125">È possibile eseguire il vendoring di Azure SDK per Go tramite [dep](https://github.com/golang/dep).</span><span class="sxs-lookup"><span data-stu-id="18308-125">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="18308-126">Per motivi di stabilità è consigliabile eseguire il vendoring.</span><span class="sxs-lookup"><span data-stu-id="18308-126">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="18308-127">Per usare il supporto per `dep`, aggiungere `github.com/Azure/azure-sdk-for-go` a una sezione di `[[constraint]]` del file `Gopkg.toml`.</span><span class="sxs-lookup"><span data-stu-id="18308-127">In order to use `dep` support, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="18308-128">Per eseguire ad esempio il vendoring sulla versione `14.0.0`, aggiungere la voce seguente:</span><span class="sxs-lookup"><span data-stu-id="18308-128">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="include-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="18308-129">Includere Azure SDK per Go nel progetto</span><span class="sxs-lookup"><span data-stu-id="18308-129">Include the Azure SDK for Go in your project</span></span>

<span data-ttu-id="18308-130">Per usare i servizi di Azure dal codice di Go, importare eventuali servizi con cui si interagisce e i moduli `autorest` necessari.</span><span class="sxs-lookup"><span data-stu-id="18308-130">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="18308-131">Si ottiene un elenco completo dei moduli disponibili da GoDoc per i [servizi disponibili](https://godoc.org/github.com/Azure/azure-sdk-for-go) e per i [pacchetti AutoRest](https://godoc.org/github.com/Azure/go-autorest).</span><span class="sxs-lookup"><span data-stu-id="18308-131">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="18308-132">I pacchetti più comuni necessari da `go-autorest` sono:</span><span class="sxs-lookup"><span data-stu-id="18308-132">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="18308-133">Pacchetto</span><span class="sxs-lookup"><span data-stu-id="18308-133">Package</span></span> | <span data-ttu-id="18308-134">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="18308-134">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="18308-135">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="18308-135">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="18308-136">Oggetti per la gestione dell'autenticazione del client del servizio</span><span class="sxs-lookup"><span data-stu-id="18308-136">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="18308-137">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="18308-137">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="18308-138">Costanti per le interazioni con i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="18308-138">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="18308-139">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="18308-139">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="18308-140">Meccanismi di autenticazione per l'accesso ai servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="18308-140">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="18308-141">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="18308-141">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="18308-142">Helper di asserzione tipi per l'uso di strutture dei dati di Azure SDK</span><span class="sxs-lookup"><span data-stu-id="18308-142">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="18308-143">Il controllo delle versioni dei moduli per i servizi di Azure viene eseguito indipendentemente dalle rispettive API dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="18308-143">Modules for Azure services are versioned independently from the SDK APIs for them.</span></span> <span data-ttu-id="18308-144">Queste versioni sono parte del percorso di importazione del modulo e derivano da una _versione del servizio_ o da un _profilo_.</span><span class="sxs-lookup"><span data-stu-id="18308-144">These versions are part of the module import path, and are from either a _service version_ or a _profile_.</span></span> <span data-ttu-id="18308-145">È attualmente consigliabile usare una versione specifica del servizio per lo sviluppo e il rilascio.</span><span class="sxs-lookup"><span data-stu-id="18308-145">Currently, it is recommended that you use a specific service version for both development and release.</span></span> <span data-ttu-id="18308-146">I servizi si trovano nel modulo `services`.</span><span class="sxs-lookup"><span data-stu-id="18308-146">Services are located under the `services` module.</span></span> <span data-ttu-id="18308-147">Il percorso completo per l'importazione è il nome del servizio, seguito dalla versione in formato `YYYY-MM-DD` e quindi seguito nuovamente dal nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="18308-147">The full path for the import is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="18308-148">Per includere ad esempio la versione `2017-03-30` del servizio di calcolo:</span><span class="sxs-lookup"><span data-stu-id="18308-148">For example, to include the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="18308-149">È attualmente consigliabile usare la versione più recente di un servizio, a meno che non esistano motivi specifici per procedere diversamente.</span><span class="sxs-lookup"><span data-stu-id="18308-149">Right now it is recommended that you use the latest version of a service, unless you have a reason to do otherwise.</span></span>

<span data-ttu-id="18308-150">Se è necessario uno snapshot collettivo dei servizi, è anche possibile selezionare una singola versione del profilo.</span><span class="sxs-lookup"><span data-stu-id="18308-150">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="18308-151">La versione dell'unico profilo bloccato è ora `2017-03-09`, che potrebbe non includere le funzionalità più recenti dei servizi.</span><span class="sxs-lookup"><span data-stu-id="18308-151">Right now, the only locked profile is version `2017-03-09`, which may not have the latest features of services.</span></span> <span data-ttu-id="18308-152">I profili sono disponibili nel modulo `profiles`, con la rispettiva versione in formato `YYYY-MM-DD`.</span><span class="sxs-lookup"><span data-stu-id="18308-152">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="18308-153">I servizi vengono raggruppati sotto la rispettiva versione del profilo.</span><span class="sxs-lookup"><span data-stu-id="18308-153">Services are grouped under their profile version.</span></span> <span data-ttu-id="18308-154">Per importare ad esempio il modulo di gestione delle risorse di Azure dal profilo `2017-03-09`:</span><span class="sxs-lookup"><span data-stu-id="18308-154">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="18308-155">Sono disponibili anche profili `preview` e `latest`.</span><span class="sxs-lookup"><span data-stu-id="18308-155">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="18308-156">L'uso di questi profili non è consigliato.</span><span class="sxs-lookup"><span data-stu-id="18308-156">Using them is not recommended.</span></span> <span data-ttu-id="18308-157">Questi profili sono versioni incrementali ed è possibile che il comportamento dei servizi cambi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="18308-157">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18308-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18308-158">Next steps</span></span>

<span data-ttu-id="18308-159">Per iniziare a usare Azure SDK per Go, provare a seguire una guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="18308-159">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="18308-160">Distribuire una macchina virtuale da un modello</span><span class="sxs-lookup"><span data-stu-id="18308-160">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="18308-161">Trasferire oggetti nell'archivio BLOB di Azure con Azure Blob SDK per Go</span><span class="sxs-lookup"><span data-stu-id="18308-161">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="18308-162">Connettersi a Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="18308-162">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="18308-163">Per iniziare immediatamente a usare altri servizi in Go SDK, vedere il codice di esempio disponibile.</span><span class="sxs-lookup"><span data-stu-id="18308-163">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="18308-164">Eseguire l'autenticazione con i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="18308-164">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [<span data-ttu-id="18308-165">Distribuire nuove macchine virtuali con l'autenticazione SSH</span><span class="sxs-lookup"><span data-stu-id="18308-165">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="18308-166">Distribuire un'immagine del contenitore in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="18308-166">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="18308-167">Creare un cluster nel servizio Kubernetes di Azure</span><span class="sxs-lookup"><span data-stu-id="18308-167">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="18308-168">Usare i servizi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="18308-168">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="18308-169">Tutti gli esempi per Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="18308-169">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
