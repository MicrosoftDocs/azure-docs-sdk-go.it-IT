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
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a>Strumenti per gli sviluppatori che usano Azure SDK per Go

Per scrivere in modo efficiente codice di Go e assicurarsi che funzioni correttamente con i servizi di Azure sono disponibili alcuni strumenti consigliati.

## <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

L'interfaccia della riga di comando di Azure 2.0 fornisce un'interfaccia della riga di comando per la creazione e la configurazione delle risorse di Azure nelle sottoscrizioni. L'interfaccia della riga di comando può semplificare le operazioni iniziali per la creazione rapida di risorse comuni e condivise di Azure, per consentire agli sviluppatori di concentrarsi sull'utilizzo più complesso dei servizi. L'interfaccia della riga di comando è multipiattaforma e include funzionalità per query e filtri, che consentono di inviare tramite pipe l'output direttamente agli strumenti preferiti della riga di comando. L'interfaccia della riga di comando è disponibile per l'installazione nel sistema locale, come immagine Docker, o tramite [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).

> [!div class="nextstepaction"]
> [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a>Visual Studio Code

Visual Studio Code è un editor leggero che include il supporto completo per il linguaggio Go tramite le estensioni. Queste estensioni includono il supporto per funzionalità quali il completamento automatico, i modelli di `impl`, il refactoring e il debug. Visual Studio Code offre anche molte estensioni per gli strumenti comuni per gli sviluppatori, ad esempio il controllo del codice sorgente, e offre anche estensioni per interazioni dirette con i servizi di Azure. Microsoft gestisce una metaestensione ufficiale che include queste estensioni di Azure, tra cui un'interfaccia interattiva per l'interfaccia della riga di comando di Azure.

* [Installare Visual Studio Code](https://code.visualstudio.com/Download)
* [Ottenere l'estensione di Visual Studio Code per Go](https://code.visualstudio.com/docs/languages/go)
* [Ottenere l'estensione Strumenti di Azure](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="dependency-management-with-dep"></a>Gestione delle dipendenze con dep

È possibile gestire le dipendenze dei pacchetti ed eseguire il vendoring con Go in molti modi, poiché non è ancora disponibile una soluzione ufficiale. Per eseguire questa gestione è consigliabile usare la gestione dipendenze di `dep`. Azure SDK per Go usa dep per il rispettivo vendoring ed è garantita la ricezione corretta delle dipendenze per qualsiasi altro progetto che usa dep.

> [!div class="nextstepaction"]
> [Ottenere la gestione dipendenze di dep](https://github.com/tools/godep)

## <a name="telemetry-with-application-insights"></a>Telemetria con Application Insights

[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) è un prodotto di analisi che consente di raccogliere con facilità informazioni di telemetria dalle applicazioni ed è integrato con l'ecosistema di Azure, con Visual Studio Team Services e con GitHub. Può essere usato in molte applicazioni e Microsoft offre Go SDK per Application Insights.

> [!div class="nextstepaction"]
> [Ottenere Go SDK per Application Insights](https://github.com/Microsoft/ApplicationInsights-Go) 
