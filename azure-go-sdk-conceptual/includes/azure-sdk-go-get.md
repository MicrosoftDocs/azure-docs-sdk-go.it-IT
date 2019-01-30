---
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: include
ms.prod: azure
ms.technology: azure-cli
ms.openlocfilehash: 5df14f939efdd0550b49261c88c8dc6518ada459
ms.sourcegitcommit: 3d26b464f196f8675c636ae792637d4c882fb92c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "55145550"
---
<span data-ttu-id="00191-101">[Azure SDK per Go](https://github.com/Azure/azure-sdk-for-go) è compatibile con Go 1.8 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="00191-101">The [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) is compatible with Go versions 1.8 and higher.</span></span> <span data-ttu-id="00191-102">Per gli ambienti che usano [profili di Azure Stack](/azure/azure-stack/user/azure-stack-version-profiles-go) il requisito minimo è Go versione 1.9.</span><span class="sxs-lookup"><span data-stu-id="00191-102">For environments using [Azure Stack Profiles](/azure/azure-stack/user/azure-stack-version-profiles-go), Go version 1.9 is the minimum requirement.</span></span>
<span data-ttu-id="00191-103">Se è necessario installare Go, seguire le [istruzioni di installazione di Go](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="00191-103">If you need to install Go, follow [the Go installation instructions](https://golang.org/doc/install).</span></span>

<span data-ttu-id="00191-104">È possibile scaricare Azure SDK per Go e le rispettive dipendenze tramite `go get`.</span><span class="sxs-lookup"><span data-stu-id="00191-104">You can download the Azure SDK for Go and its dependencies via `go get`.</span></span>

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> <span data-ttu-id="00191-105">Assicurarsi di scrivere `Azure` in lettere maiuscole nell'URL.</span><span class="sxs-lookup"><span data-stu-id="00191-105">Make sure that you capitalize `Azure` in the URL.</span></span> <span data-ttu-id="00191-106">In caso contrario, è possibile che si verifichino problemi di importazione correlati alla distinzione tra maiuscole/minuscole durante l'uso dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="00191-106">Doing otherwise can cause case-related import problems when working with the SDK.</span></span> <span data-ttu-id="00191-107">È anche necessario scrivere `Azure` in lettere maiuscole nelle istruzioni di importazione.</span><span class="sxs-lookup"><span data-stu-id="00191-107">You also need to capitalize `Azure` in your import statements.</span></span>
