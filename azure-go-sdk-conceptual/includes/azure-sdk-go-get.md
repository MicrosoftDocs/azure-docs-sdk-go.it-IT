---
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 02/14/2018
ms.topic: include
ms.prod: azure
ms.technology: azure-cli
ms.openlocfilehash: 0febc2cc42ad95a1b7a5032c7987e37cc82f374e
ms.sourcegitcommit: 181d4e0b164cf39b3feac346f559596bd19c94db
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2018
ms.locfileid: "38067034"
---
[Azure SDK per Go](https://github.com/Azure/azure-sdk-for-go) è compatibile con Go 1.8 e versioni successive. Per gli ambienti che usano [profili di Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-version-profiles) il requisito minimo è Go versione 1.9.
Se Go non è disponibile nel sistema, seguire le [istruzioni di installazione di Go](https://golang.org/doc/install).

È possibile ottenere Azure SDK per Go e le rispettive dipendenze tramite `go get`.

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> Assicurarsi di scrivere `Azure` in lettere maiuscole nell'URL. In caso contrario, è possibile che si verifichino problemi di importazione correlati alla distinzione tra maiuscole/minuscole durante l'uso dell'SDK. È anche necessario scrivere `Azure` in lettere maiuscole nelle istruzioni di importazione.

