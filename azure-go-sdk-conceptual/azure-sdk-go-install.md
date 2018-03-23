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
# <a name="installing-the-azure-sdk-for-go"></a>Installazione di Azure SDK per Go

Introduzione ad Azure SDK per Go Questo SDK consente di gestire e interagire con i servizi di Azure dalle applicazioni Go.

## <a name="get-the-azure-sdk-for-go"></a>Ottenere Azure SDK per Go

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

Per usare i BLOB del servizio di archiviazione di Azure è necessario un SDK distinto.

```bash
go get -u -d github.com/Azure/azure-storage-blob-go/...
```

## <a name="vendoring-the-azure-sdk-for-go"></a>Eseguire il vendoring di Azure SDK per Go

È possibile eseguire il vendoring di Azure SDK per Go tramite [dep](https://github.com/golang/dep). Per motivi di stabilità è consigliabile eseguire il vendoring. Per usare il supporto per `dep`, aggiungere `github.com/Azure/azure-sdk-for-go` a una sezione di `[[constraint]]` del file `Gopkg.toml`. Per eseguire ad esempio il vendoring sulla versione `14.0.0`, aggiungere la voce seguente:

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="including-the-azure-sdk-for-go-in-your-project"></a>Inclusione di Azure SDK per Go nel progetto

Per usare i servizi di Azure dal codice di Go, importare eventuali servizi con cui si interagisce e i moduli `autorest` necessari.
Si ottiene un elenco completo dei moduli disponibili da GoDoc per i [servizi disponibili](https://godoc.org/github.com/Azure/azure-sdk-for-go) e per i [pacchetti AutoRest](https://godoc.org/github.com/Azure/go-autorest). I pacchetti più comuni necessari da `go-autorest` sono:

| Pacchetto | DESCRIZIONE |
|---------|-------------|
| [github.com/Azure/go-autorest/autorest][autorest] | Oggetti per la gestione dell'autenticazione del client del servizio |
| [github.com/Azure/go-autorest/autorest/azure][autorest/azure] | Costanti per le interazioni con i servizi di Azure |
| [github.com/Azure/go-autorest/autorest/adal][autorest/adal] | Meccanismi di autenticazione per l'accesso ai servizi di Azure |
| [github.com/Azure/go-autorest/autorest/to][autorest/to] | Helper di asserzione tipi per l'uso di strutture dei dati di Azure SDK |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

Il controllo delle versioni dei moduli per i servizi di Azure viene eseguito indipendentemente dalle rispettive API dell'SDK. Queste versioni sono parte del percorso di importazione del modulo e derivano da una _versione del servizio_ o da un _profilo_. È attualmente consigliabile usare una versione specifica del servizio per lo sviluppo e il rilascio. I servizi si trovano nel modulo `services`. Il percorso completo per l'importazione è il nome del servizio, seguito dalla versione in formato `YYYY-MM-DD` e quindi seguito nuovamente dal nome del servizio. Per includere ad esempio la versione `2017-03-30` del servizio di calcolo:

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

È attualmente consigliabile usare la versione più recente di un servizio, a meno che non esistano motivi specifici per procedere diversamente.

Se è necessario uno snapshot collettivo dei servizi, è anche possibile selezionare una singola versione del profilo. La versione dell'unico profilo bloccato è ora `2017-03-30`, che potrebbe non includere le funzionalità più recenti dei servizi. I profili sono disponibili nel modulo `profiles`, con la rispettiva versione in formato `YYYY-MM-DD`. I servizi vengono raggruppati sotto la rispettiva versione del profilo. Per importare ad esempio il modulo di gestione delle risorse di Azure dal profilo `2017-03-09`:

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> Sono disponibili anche profili `preview` e `latest`. L'uso di questi profili non è consigliato. Questi profili sono versioni incrementali ed è possibile che il comportamento dei servizi cambi in qualsiasi momento.

## <a name="next-steps"></a>Passaggi successivi

Per iniziare a usare Azure SDK per Go, provare a seguire una guida introduttiva.

* [Distribuire una macchina virtuale da un modello](azure-sdk-go-qs-vm.md)
* [Trasferire oggetti nell'archivio BLOB di Azure con Azure Blob SDK per Go](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [Connettersi a Database di Azure per PostgreSQL](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

Per iniziare immediatamente a usare altri servizi in Go SDK, vedere il codice di esempio disponibile.

* [Eseguire l'autenticazione con i servizi di Azure](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [Distribuire nuove macchine virtuali con l'autenticazione SSH](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [Distribuire un'immagine del contenitore in Istanze di contenitore di Azure](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [Creare un cluster nel servizio Kubernetes di Azure](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [Usare i servizi di Archiviazione di Azure](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [Tutti gli esempi per Azure SDK per Go](https://github.com/azure-samples/azure-sdk-for-go-samples)
