---
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 02/14/2018
ms.topic: include
ms.prod: azure
ms.technology: azure-cli
ms.openlocfilehash: ddd58efdbc0c2d3ded068a9bebf2466db702566f
ms.sourcegitcommit: f08abf902b48f8173aa6e261084ff2cfc9043305
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
[Azure SDK per Go](https://github.com/Azure/azure-sdk-for-go) è compatibile con Go 1.8 e versioni successive. Per gli ambienti che usano [profili di Azure Stack](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles) il requisito minimo è Go versione 1.9.
Se Go non è disponibile nel sistema, seguire le [istruzioni di installazione di Go](https://golang.org/doc/install).

È possibile ottenere Azure SDK per Go e le rispettive dipendenze tramite `go get`.

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> Assicurarsi di scrivere `Azure` in lettere maiuscole nell'URL. In caso contrario, è possibile che si verifichino problemi di importazione correlati alla distinzione tra maiuscole/minuscole durante l'uso dell'SDK. È anche necessario scrivere `Azure` in lettere maiuscole nelle istruzioni di importazione.

