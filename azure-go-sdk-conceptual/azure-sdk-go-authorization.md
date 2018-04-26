---
title: Autenticazione con Azure SDK per Go
description: Informazioni sui metodi di autenticazione disponibili in Azure SDK per Go e su come usarli.
services: azure
author: sptramer
ms.author: sttramer
ms.date: 04/03/2018
ms.topic: article
ms.service: azure
ms.devlang: go
manager: carmonm
ms.openlocfilehash: 39f9dc5a7cdf9ab84cfd9264446bacb31392ca80
ms.sourcegitcommit: 59d2b4c9d8da15fbbd15e36551093219fdaf256e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2018
---
# <a name="authentication-methods-in-the-azure-sdk-for-go"></a>Metodi di autenticazione in Azure SDK per Go

Azure SDK per Go offre una varietà di tipi e metodi di autenticazione utilizzabili dall'applicazione. I metodi di autenticazione supportati variano dal pull di informazioni da variabili di ambiente all'autenticazione interattiva basata su Web. Questo articolo illustra i tipi di autenticazione disponibili nell'SDK e i metodi per usarli, oltre a presentare le procedure consigliate per la selezione del tipo di autenticazione adatto all'applicazione.

## <a name="available-authentication-types-and-methods"></a>Metodi e tipi di autenticazione disponibili

Azure SDK per Go offre diversi tipi di autenticazione che usano set di credenziali diversi. Ognuno di questi tipi di autenticazione è disponibile tramite metodi di autenticazione diversi, ovvero secondo il modo in cui l'SDK riceve le credenziali come input. La tabella seguente descrive i tipi di autenticazione e le situazioni in cui sono consigliati per l'uso da parte dell'applicazione.

| Tipo di autenticazione | Consigliato quando... |
|---------------------|---------------------|
| Autenticazione basata su certificati | È presente un certificato X509 configurato per un utente o un'entità servizio di Azure Active Directory (AAD). Per altre informazioni, vedere [Introduzione all'autenticazione basata su certificati di Azure Active Directory]. |
| Credenziali del client | Si dispone di un'entità servizio configurata per l'applicazione o una classe di applicazioni a cui questa appartiene. Per altre informazioni, vedere [Creare un'entità servizio con l'interfaccia della riga di comando di Azure 2.0]. |
| Identità del servizio gestito | L'applicazione viene eseguita su una risorsa di Azure che è stata configurata con l'identità del servizio gestito. Per altre informazioni, vedere [Identità del servizio gestito per le risorse di Azure]. |
| Token dispositivo | L'applicazione deve essere usata __soltanto__ in modo interattivo e disporrà di una varietà di utenti, potenzialmente da più tenant AAD. Gli utenti hanno accesso a un browser Web per eseguire l'accesso. Per altre informazioni, vedere [Uso dell'autenticazione tramite token dispositivo](#use-device-token-authentication).|
| Nome utente/password | Si dispone di un'applicazione interattiva che non può usare alcun altro metodo di autenticazione. Gli utenti non dispongono dell'autenticazione a più fattori abilitata per i relativi account di accesso ad Azure Active Directory. |

> [!IMPORTANT]
> Se si usa un tipo di autenticazione diverso dalle credenziali del client, l'applicazione deve essere registrata in Azure Active Directory. Per altri dettagli, vedere [Integrazione di applicazioni con Azure Active Directory](/azure/active-directory/develop/active-directory-integrating-applications).

> [!NOTE]
> A meno che non si abbiano esigenze particolari, evitare l'autenticazione con nome utente/password. L'autenticazione tramite token dispositivo può essere usata nelle situazioni in cui è opportuno eseguire l'accesso basato sull'utente.

[Introduzione all'autenticazione basata su certificati di Azure Active Directory]: /azure/active-directory/active-directory-certificate-based-authentication-get-started
[Creare un'entità servizio con l'interfaccia della riga di comando di Azure 2.0]: /cli/azure/create-an-azure-service-principal-azure-cli
[Identità del servizio gestito per le risorse di Azure]: /azure/active-directory/managed-service-identity/overview

Questi tipi di autenticazione sono disponibili tramite metodi diversi. L'[_autenticazione basata su ambiente_](#use-environment-based-authentication) legge le credenziali direttamente dall'ambiente del programma. L'[_autenticazione basata su file_](#use-file-based-authentication) carica un file contenente le credenziali dell'entità servizio. L'[_autenticazione basata su client_](#use-an-authentication-client) usa un oggetto nel codice Go e chiede all'utente di fornire le credenziali durante l'esecuzione del programma. Infine, [_l'autenticazione tramite token dispositivo_ ](#use-device-token-authentication) richiede agli utenti di accedere in modo interattivo con un token tramite un browser Web e non può essere usata assieme all'autenticazione basata su file o ambiente.

Tutti i tipi e le funzioni di autenticazione sono disponibili nel pacchetto `github.com/Azure/go-autorest/autorest/azure/auth`.

> [!NOTE]
> A meno che non si abbiano esigenze particolari, evitare l'autenticazione basata su client. Questo metodo di autenticazione incoraggia procedure non valide. In particolare, l'autenticazione basata su client spinge a impostare le credenziali come hardcoded. La scrittura di codici personalizzati per l'autenticazione potrà essere anche interrotta in versioni future di SDK qualora i requisiti di autenticazione cambino.

## <a name="use-environment-based-authentication"></a>Usare l'autenticazione basata su ambiente

Se si esegue l'applicazione in un ambiente rigorosamente controllato, ad esempio in un contenitore, l'autenticazione basata su ambiente è una scelta naturale. Configurare l'ambiente shell prima di eseguire l'applicazione e prima che Go SDK legga queste variabili di ambiente in fase di runtime per l'autenticazione con Azure. 

L'autenticazione basata su ambiente è supportata per tutti i metodi di autenticazione ad eccezione dei token dispositivo, valutati nell'ordine seguente: credenziali client, certificati, nome utente/password e identità del servizio gestito. Se non è impostata una variabile di ambiente necessaria o l'SDK riceve un rifiuto dal servizio di autenticazione, viene eseguito un tentativo con il tipo di autenticazione successivo. Se l'SDK non è in grado di eseguire l'autenticazione dall'ambiente, viene restituito un errore.

La tabella seguente illustra in dettaglio le variabili di ambiente che devono essere impostate per ogni tipo di autenticazione supportato dall'autenticazione basata su ambiente.

| Tipo di autenticazione | Variabile di ambiente | DESCRIZIONE |
| ------------------- | -------------------- | ----------- |
| __Credenziali del client__ | `AZURE_TENANT_ID` | ID del tenant di Active Directory a cui appartiene l'entità servizio. |
| | `AZURE_CLIENT_ID` | Nome o ID dell'entità servizio. |
| | `AZURE_CLIENT_SECRET` | Segreto associato all'entità servizio. |
| __Certificate__ | `AZURE_TENANT_ID` | ID del tenant di Active Directory che viene registrato con il certificato. |
| | `AZURE_CLIENT_ID` | ID client applicazione associato al certificato. |
| | `AZURE_CERTIFICATE_PATH` | Percorso verso il file di certificato client. |
| | `AZURE_CERTIFICATE_PASSWORD` | Password del certificato client. |
| __Nome utente/password__ | `AZURE_TENANT_ID` | ID del tenant di Active Directory a cui appartiene l'utente. |
| | `AZURE_CLIENT_ID` | ID client dell'applicazione. |
| | `AZURE_USERNAME` | Nome utente con cui accedere. |
| | `AZURE_PASSWORD` | Password con cui accedere. |
| __Identità del servizio gestito__ | | L'Identità del servizio gestito non richiede la configurazione di credenziali. L'applicazione deve essere eseguita in una risorsa di Azure configurata per l'uso dell'Identità del servizio gestito. Per informazioni dettagliate, vedere [Identità del servizio gestito per le risorse di Azure]. |

Per connettersi a un endpoint di gestione o cloud diverso dal cloud pubblico di Azure, è possibile impostare anche le seguenti variabili di ambiente. I motivi più comuni per impostarle includono l'uso di Azure Stack, un cloud in un'area geografica diversa o il modello di distribuzione di Azure classico.

| Variabile di ambiente | DESCRIZIONE  |
|----------------------|--------------|
| `AZURE_ENVIRONMENT` | Nome dell'ambiente cloud a cui connettersi. |
| `AZURE_AD_RESOURCE` | ID della risorsa di Active Directory da usare quando ci si connette. Deve trattarsi di un URI che punta all'endpoint di gestione. |

Quando si usa l'autenticazione basata su ambiente, chiamare la funzione [NewAuthorizerFromEnvironment](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromEnvironment) per ottenere l'oggetto provider di autorizzazioni. Questo oggetto viene quindi impostato sulla proprietà `Authorizer` dei client per consentire loro l'accesso ad Azure.

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"
authorizer, err := auth.NewAuthorizerFromEnvironment()
```

## <a name="use-file-based-authentication"></a>Usare l'autenticazione basata su file

L'autenticazione basata su file funziona solo con le credenziali del client quando vengono archiviate in un formato di file locale generato dall'[interfaccia della riga di comando di Azure 2.0](/cli/azure). È possibile creare facilmente questo file quando si crea una nuova entità servizio con il parametro `--sdk-auth`. Se si intende usare l'autenticazione basata su file, assicurarsi che questo argomento venga fornito quando si crea un'entità servizio. Poiché l'interfaccia della riga di comando stampa l'output in `stdout`, reindirizzare l'output verso un file.

```azurecli
az ad sp create-for-rbac --sdk-auth > azure.auth
```

Impostare la variabile di ambiente `AZURE_AUTH_LOCATION` in cui si trova il file di autorizzazione. Questa variabile di ambiente viene letta dall'applicazione e le credenziali contenute in essa vengono analizzate. Se è necessario selezionare il file di autorizzazione in fase di runtime, modificare l'ambiente del programma tramite la funzione [os.Setenv](https://golang.org/pkg/os/#Setenv).

Per caricare le informazioni di autenticazione, chiamare la funzione [NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile). A differenza dell'autorizzazione basata su ambiente, l'autorizzazione basata su file richiede un endpoint di risorse.

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"
authorizer, err := NewAuthorizerFromFile(azure.PublicCloud.ResourceManagerEndpoint)
```

Per altre informazioni sull'uso delle entità servizio e sulla gestione delle relative autorizzazioni di accesso, vedere [Creare un'entità servizio con l'interfaccia della riga di comando di Azure 2.0].

## <a name="use-device-token-authentication"></a>Uso dell'autenticazione tramite token dispositivo

Perché gli utenti accedano in modo interattivo, il modo migliore per offrire tale funzionalità è l'autenticazione tramite token dispositivo. Questo flusso di autenticazione fornisce all'utente un token da incollare in un sito di accesso di Microsoft, in cui l'utente può quindi effettuare l'accesso con un account di Azure Active Directory (AAD). Questo metodo di autenticazione supporta gli account con autenticazione a più fattori abilitata, a differenza dell'autenticazione standard tramite nome utente/password.

Per usare l'autenticazione tramite token dispositivo, creare un provider di autorizzazioni [DeviceFlowConfig](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#DeviceFlowConfig) con la funzione [NewDeviceFlowConfig](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewDeviceFlowConfig). Chiamare il [provider di autorizzazioni](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#DeviceFlowConfig.Authorizer) nell'oggetto risultante per avviare il processo di autenticazione. L'autenticazione tramite flusso del dispositivo blocca l'esecuzione del programma fino a quando non è stato completato l'intero flusso di autenticazione.

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"
deviceConfig := auth.NewDeviceFlowConfig(applicationID, tenantID)
authorizer, err := deviceConfig.Authorizer()
```

## <a name="use-an-authentication-client"></a>Usare un client di autenticazione

Se è necessario un tipo di autenticazione specifico e si è disposti a far eseguire al programma il caricamento delle informazioni di autenticazione da parte dell'utente, è possibile usare qualsiasi client conforme all'interfaccia [auth.AuthorizerConfig](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#AuthorizerConfig). Usare un tipo che implementa questa interfaccia per disporre di un programma interattivo, quando si usano file di configurazione specializzati o è presente un requisito che impedisce di usare un altro metodo di autenticazione.

> [!WARNING]
> Mai impostare come hardcoded le credenziali di Azure in un'applicazione. L'inserimento di informazioni riservate in un file binario dell'applicazione rende più semplice per un utente malintenzionato estrarle, indipendentemente dal fatto che l'applicazione sia in esecuzione o meno. In questo modo vengono messe a rischio tutte le risorse di Azure per cui sono autorizzate le credenziali!

Nella tabella seguente sono elencati i tipi conformi all'interfaccia `AuthorizerConfig` nell'SDK.

| Tipo di autenticazione | Tipo di provider di autorizzazioni |
|---------------------|-----------------------|
| Autenticazione basata su certificati | [ClientCertificateConfig] |
| Credenziali del client | [ClientCredentialsConfig] |
| Identità del servizio gestito | [MSIConfig] |
| Nome utente/password | [UsernamePasswordConfig] |

[ClientCertificateConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#ClientCertificateConfig
[ClientCredentialsConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#ClientCredentialsConfig
[MSIConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#MSIConfig
[DeviceFlowConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#DeviceFlowConfig
[UsernamePasswordConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#UsernamePasswordConfig

Creare un autenticatore con la propria funzione `New` associata e quindi chiamare `Authorize` nell'oggetto risultante per eseguire l'autenticazione. Ad esempio, per usare l'autenticazione basata su certificati:

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"
certificateAuthorizer := auth.NewClientCertificateConfig(certificatePath, certificatePassword, clientID, tenantID)
authorizerToken, err := certificateAuthorizer.Authorize()
```
