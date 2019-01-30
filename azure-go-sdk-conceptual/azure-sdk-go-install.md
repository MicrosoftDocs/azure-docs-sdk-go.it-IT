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
ms.openlocfilehash: 2799e3a6c637036eeaf7b20adf8aa55a8a4ab400
ms.sourcegitcommit: 4db332f5e43a5b43032ff9017805d5fd5a650d86
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/28/2019
ms.locfileid: "55145533"
---
# <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="37612-103">Installare Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="37612-103">Install the Azure SDK for Go</span></span>

<span data-ttu-id="37612-104">Introduzione ad Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="37612-104">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="37612-105">L'SDK consente di gestire i servizi di Azure dalle applicazioni Go e interagire con essi.</span><span class="sxs-lookup"><span data-stu-id="37612-105">The SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="37612-106">Ottenere Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="37612-106">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="37612-107">Alcuni servizi di Azure includono un proprio SDK per Go e non sono compresi nel pacchetto Azure SDK per Go di base.</span><span class="sxs-lookup"><span data-stu-id="37612-107">Some Azure services have their own Go SDK and aren't included in the core Azure SDK for Go package.</span></span> <span data-ttu-id="37612-108">La tabella seguente elenca i servizi con SDK propri e i relativi nomi di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="37612-108">The following table lists the services with their own SDKs and their package names.</span></span> <span data-ttu-id="37612-109">Questi pacchetti vengono tutti considerati in anteprima.</span><span class="sxs-lookup"><span data-stu-id="37612-109">These packages are all considered to be in preview.</span></span>

| <span data-ttu-id="37612-110">Service</span><span class="sxs-lookup"><span data-stu-id="37612-110">Service</span></span> | <span data-ttu-id="37612-111">Pacchetto</span><span class="sxs-lookup"><span data-stu-id="37612-111">Package</span></span> |
|---------|---------|
| <span data-ttu-id="37612-112">Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="37612-112">Blob Storage</span></span> | [<span data-ttu-id="37612-113">github.com/Azure/azure-storage-blob-go</span><span class="sxs-lookup"><span data-stu-id="37612-113">github.com/Azure/azure-storage-blob-go</span></span>](https://github.com/Azure/azure-storage-blob-go) |
| <span data-ttu-id="37612-114">Archiviazione file</span><span class="sxs-lookup"><span data-stu-id="37612-114">File Storage</span></span> | [<span data-ttu-id="37612-115">github.com/Azure/azure-storage-file-go</span><span class="sxs-lookup"><span data-stu-id="37612-115">github.com/Azure/azure-storage-file-go</span></span>](https://github.com/Azure/azure-storage-file-go) |
| <span data-ttu-id="37612-116">Coda di archiviazione</span><span class="sxs-lookup"><span data-stu-id="37612-116">Storage Queue</span></span> | [<span data-ttu-id="37612-117">github.com/Azure/azure-storage-queue-go</span><span class="sxs-lookup"><span data-stu-id="37612-117">github.com/Azure/azure-storage-queue-go</span></span>](https://github.com/Azure/azure-storage-queue-go) |
| <span data-ttu-id="37612-118">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="37612-118">Event Hub</span></span> | [<span data-ttu-id="37612-119">github.com/Azure/azure-event-hubs-go</span><span class="sxs-lookup"><span data-stu-id="37612-119">github.com/Azure/azure-event-hubs-go</span></span>](https://github.com/Azure/azure-event-hubs-go) |
| <span data-ttu-id="37612-120">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="37612-120">Service Bus</span></span> | [<span data-ttu-id="37612-121">github.com/Azure/azure-service-bus-go</span><span class="sxs-lookup"><span data-stu-id="37612-121">github.com/Azure/azure-service-bus-go</span></span>](https://github.com/Azure/azure-service-bus-go) |
| <span data-ttu-id="37612-122">Application Insights</span><span class="sxs-lookup"><span data-stu-id="37612-122">Application Insights</span></span> | [<span data-ttu-id="37612-123">github.com/Microsoft/ApplicationInsights-go</span><span class="sxs-lookup"><span data-stu-id="37612-123">github.com/Microsoft/ApplicationInsights-go</span></span>](https://github.com/Microsoft/ApplicationInsights-go) |

## <a name="vendor-the-azure-sdk-for-go"></a><span data-ttu-id="37612-124">Eseguire il vendoring di Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="37612-124">Vendor the Azure SDK for Go</span></span>

<span data-ttu-id="37612-125">È possibile eseguire il vendoring di Azure SDK per Go tramite [dep](https://github.com/golang/dep).</span><span class="sxs-lookup"><span data-stu-id="37612-125">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="37612-126">Per motivi di stabilità è consigliabile eseguire il vendoring.</span><span class="sxs-lookup"><span data-stu-id="37612-126">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="37612-127">Per usare `dep` nel proprio progetto, aggiungere `github.com/Azure/azure-sdk-for-go` a una sezione `[[constraint]]` di `Gopkg.toml`.</span><span class="sxs-lookup"><span data-stu-id="37612-127">To use `dep` in your own project, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="37612-128">Per eseguire ad esempio il vendoring sulla versione `14.0.0`, aggiungere la voce seguente:</span><span class="sxs-lookup"><span data-stu-id="37612-128">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```toml
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="include-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="37612-129">Includere Azure SDK per Go nel progetto</span><span class="sxs-lookup"><span data-stu-id="37612-129">Include the Azure SDK for Go in your project</span></span>

<span data-ttu-id="37612-130">Per usare i servizi di Azure dal codice di Go, importare eventuali servizi con cui si interagisce e i moduli `autorest` necessari.</span><span class="sxs-lookup"><span data-stu-id="37612-130">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="37612-131">Si ottiene un elenco completo dei moduli disponibili da GoDoc per i [servizi disponibili](https://godoc.org/github.com/Azure/azure-sdk-for-go) e per i [pacchetti AutoRest](https://godoc.org/github.com/Azure/go-autorest).</span><span class="sxs-lookup"><span data-stu-id="37612-131">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="37612-132">I pacchetti più comuni necessari da `go-autorest` sono:</span><span class="sxs-lookup"><span data-stu-id="37612-132">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="37612-133">Pacchetto</span><span class="sxs-lookup"><span data-stu-id="37612-133">Package</span></span> | <span data-ttu-id="37612-134">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="37612-134">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="37612-135">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="37612-135">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="37612-136">Oggetti per la gestione dell'autenticazione del client del servizio</span><span class="sxs-lookup"><span data-stu-id="37612-136">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="37612-137">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="37612-137">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="37612-138">Costanti per le interazioni con i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="37612-138">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="37612-139">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="37612-139">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="37612-140">Meccanismi di autenticazione per l'accesso ai servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="37612-140">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="37612-141">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="37612-141">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="37612-142">Helper di asserzione tipi per l'uso di strutture dei dati di Azure SDK</span><span class="sxs-lookup"><span data-stu-id="37612-142">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="37612-143">Il controllo delle versioni dei pacchetti Go e dei servizi di Azure viene eseguito in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="37612-143">Go packages and Azure services are versioned independently.</span></span> <span data-ttu-id="37612-144">Le versioni del servizio sono parte del percorso di importazione del modulo, disponibile nel modulo `services`.</span><span class="sxs-lookup"><span data-stu-id="37612-144">The service versions are part of the module import path, underneath the `services` module.</span></span> <span data-ttu-id="37612-145">Il percorso completo per il modulo è il nome del servizio, seguito dalla versione in formato `YYYY-MM-DD` e quindi seguito nuovamente dal nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="37612-145">The full path for the module is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="37612-146">Per importare ad esempio la versione `2017-03-30` del servizio di calcolo:</span><span class="sxs-lookup"><span data-stu-id="37612-146">For example, to import the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="37612-147">È consigliabile usare la versione più recente di un servizio all'inizio dello sviluppo e mantenere la coerenza a livello di versione.</span><span class="sxs-lookup"><span data-stu-id="37612-147">It's recommended that you use the latest version of a service when starting development and keep it consistent.</span></span>
<span data-ttu-id="37612-148">È possibile che le diverse versioni presentino modifiche ai requisiti del servizio che potrebbero provocare interruzioni del codice, anche se non vengono applicati aggiornamenti a Go SDK in tale intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="37612-148">Service requirements may change between versions that could break your code, even if there are no Go SDK updates during that time.</span></span>

<span data-ttu-id="37612-149">Se è necessario uno snapshot collettivo dei servizi, è anche possibile selezionare una singola versione del profilo.</span><span class="sxs-lookup"><span data-stu-id="37612-149">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="37612-150">La versione dell'unico profilo bloccato è ora `2017-03-09`, che potrebbe non includere le funzionalità più recenti dei servizi.</span><span class="sxs-lookup"><span data-stu-id="37612-150">Right now, the only locked profile is version `2017-03-09`, which may not have the latest features of services.</span></span> <span data-ttu-id="37612-151">I profili sono disponibili nel modulo `profiles`, con la rispettiva versione in formato `YYYY-MM-DD`.</span><span class="sxs-lookup"><span data-stu-id="37612-151">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="37612-152">I servizi vengono raggruppati sotto la rispettiva versione del profilo.</span><span class="sxs-lookup"><span data-stu-id="37612-152">Services are grouped under their profile version.</span></span> <span data-ttu-id="37612-153">Per importare ad esempio il modulo di gestione delle risorse di Azure dal profilo `2017-03-09`:</span><span class="sxs-lookup"><span data-stu-id="37612-153">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="37612-154">Sono disponibili anche profili `preview` e `latest`.</span><span class="sxs-lookup"><span data-stu-id="37612-154">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="37612-155">L'uso di questi profili non è consigliato.</span><span class="sxs-lookup"><span data-stu-id="37612-155">Using them is not recommended.</span></span> <span data-ttu-id="37612-156">Questi profili sono versioni incrementali ed è possibile che il comportamento dei servizi cambi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="37612-156">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37612-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37612-157">Next steps</span></span>

<span data-ttu-id="37612-158">Per iniziare a usare Azure SDK per Go, provare a seguire una guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="37612-158">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="37612-159">Distribuire una macchina virtuale da un modello</span><span class="sxs-lookup"><span data-stu-id="37612-159">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="37612-160">Trasferire oggetti nell'archivio BLOB di Azure con Azure Blob SDK per Go</span><span class="sxs-lookup"><span data-stu-id="37612-160">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="37612-161">Connettersi a Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="37612-161">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="37612-162">Per iniziare immediatamente a usare altri servizi in Go SDK, vedere il codice di esempio disponibile.</span><span class="sxs-lookup"><span data-stu-id="37612-162">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="37612-163">Eseguire l'autenticazione con i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="37612-163">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/internal/iam)
* [<span data-ttu-id="37612-164">Distribuire nuove macchine virtuali con l'autenticazione SSH</span><span class="sxs-lookup"><span data-stu-id="37612-164">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="37612-165">Distribuire un'immagine del contenitore in Istanze di Azure Container</span><span class="sxs-lookup"><span data-stu-id="37612-165">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="37612-166">Creare un cluster nel servizio Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="37612-166">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute)
* [<span data-ttu-id="37612-167">Usare i servizi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="37612-167">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="37612-168">Tutti gli esempi per Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="37612-168">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
