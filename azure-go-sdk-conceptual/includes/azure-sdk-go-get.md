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
<span data-ttu-id="58d5f-101">[Azure SDK per Go](https://github.com/Azure/azure-sdk-for-go) è compatibile con Go 1.8 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="58d5f-101">The [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) is compatible with Go versions 1.8 and later.</span></span> <span data-ttu-id="58d5f-102">Per gli ambienti che usano [profili di Azure Stack](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles) il requisito minimo è Go versione 1.9.</span><span class="sxs-lookup"><span data-stu-id="58d5f-102">For environments using [Azure Stack Profiles](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles), Go version 1.9 is the minimum requirement.</span></span>
<span data-ttu-id="58d5f-103">Se Go non è disponibile nel sistema, seguire le [istruzioni di installazione di Go](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="58d5f-103">If you do not have Go available on your system, follow [the Go installation instructions](https://golang.org/doc/install).</span></span>

<span data-ttu-id="58d5f-104">È possibile ottenere Azure SDK per Go e le rispettive dipendenze tramite `go get`.</span><span class="sxs-lookup"><span data-stu-id="58d5f-104">You can obtain the Azure SDK for Go and its dependencies via `go get`.</span></span>

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> <span data-ttu-id="58d5f-105">Assicurarsi di scrivere `Azure` in lettere maiuscole nell'URL.</span><span class="sxs-lookup"><span data-stu-id="58d5f-105">Make sure that you capitalize `Azure` in the URL.</span></span> <span data-ttu-id="58d5f-106">In caso contrario, è possibile che si verifichino problemi di importazione correlati alla distinzione tra maiuscole/minuscole durante l'uso dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="58d5f-106">Doing otherwise can cause case-related import problems when working with the SDK.</span></span> <span data-ttu-id="58d5f-107">È anche necessario scrivere `Azure` in lettere maiuscole nelle istruzioni di importazione.</span><span class="sxs-lookup"><span data-stu-id="58d5f-107">You also need to capitalize `Azure` in your import statements.</span></span>

