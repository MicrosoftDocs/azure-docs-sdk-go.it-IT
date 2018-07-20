---
title: Strumenti per gli sviluppatori Go
description: Strumenti per l'uso di Azure SDK per Go e dei servizi di Azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 07/13/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: dfa3912ac13e6f6d52d607f9dcc150f3a5b57602
ms.sourcegitcommit: d1790b317a8fcb4d672c654dac2a925a976589d4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2018
ms.locfileid: "39039506"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a>Strumenti per gli sviluppatori che usano Azure SDK per Go

Per scrivere in modo efficiente codice di Go e assicurarsi che funzioni correttamente con i servizi di Azure sono disponibili alcuni strumenti consigliati.

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

L'interfaccia della riga di comando di Azure permette la creazione e la configurazione delle risorse di Azure nelle sottoscrizioni. L'interfaccia della riga di comando può semplificare le operazioni iniziali per la creazione rapida di risorse comuni e condivise di Azure, per consentire agli sviluppatori di concentrarsi sull'utilizzo più complesso dei servizi. L'interfaccia della riga di comando è multipiattaforma e include funzionalità per query e filtri, che consentono di inviare tramite pipe l'output direttamente agli strumenti preferiti della riga di comando. L'interfaccia della riga di comando è disponibile per l'installazione nel sistema locale, come immagine Docker, o tramite [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).

> [!div class="nextstepaction"]
> [Installare l'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a>Visual Studio Code

Visual Studio Code è un editor leggero che include il supporto completo per il linguaggio Go tramite le estensioni. Queste estensioni includono il supporto per funzionalità quali il completamento automatico, i modelli di `impl`, il refactoring e il debug. Visual Studio Code offre anche molte estensioni per gli strumenti comuni per gli sviluppatori, ad esempio il controllo del codice sorgente, e offre anche estensioni per interazioni dirette con i servizi di Azure. Microsoft gestisce una metaestensione ufficiale che include queste estensioni di Azure, tra cui un'interfaccia interattiva per l'interfaccia della riga di comando di Azure.

* [Installare Visual Studio Code](https://code.visualstudio.com/Download)
* [Ottenere l'estensione di Visual Studio Code per Go](https://code.visualstudio.com/docs/languages/go)
* [Ottenere l'estensione Strumenti di Azure](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="cicd-with-azure-devops-project"></a>CI/CD con il progetto DevOps di Azure

Con la pipeline del progetto DevOps di Azure, è possibile configurare una compilazione e una distribuzione continue per le applicazioni Go. Tutto quello che serve è un repository git disponibile e sarà possibile configurare per distribuire ed eseguire test direttamente sulle risorse di Azure. La pipeline di configurazione è semplice da creare e gestire e, poiché ne viene effettuato il provisioning direttamente su Azure, è possibile controllarla nello stesso modo con cui si gestiscono le altre risorse di Azure.

> [!div class="nextstepaction"]
> [Informazioni su come creare una pipeline CI/CD con i progetti DevOps di Azure](/devops-project/azure-devops-project-go)

## <a name="dependency-management-with-dep"></a>Gestione delle dipendenze con dep

È possibile gestire le dipendenze dei pacchetti ed eseguire il vendoring con Go in molti modi, poiché non è ancora disponibile una soluzione ufficiale. Per eseguire questa gestione è consigliabile usare la gestione dipendenze di `dep`. Azure SDK per Go usa dep per il rispettivo vendoring ed è garantita la ricezione corretta delle dipendenze per qualsiasi altro progetto che usa dep.

> [!div class="nextstepaction"]
> [Ottenere la gestione dipendenze di dep](https://github.com/golang/dep)
