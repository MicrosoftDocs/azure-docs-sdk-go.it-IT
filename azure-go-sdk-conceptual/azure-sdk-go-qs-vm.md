---
title: Distribuire una macchina virtuale di Azure da Go
description: Distribuire una macchina virtuale tramite Azure SDK per Go.
keywords: azure, macchina virtuale, vm, go, golang, azure sdk
author: sptramer
ms.author: sttramer
ms.date: 02/08/2018
ms.topic: quickstart
ms.devlang: go
manager: routlaw
ms.openlocfilehash: ae460dbf21b13c40f3d564274f8b790afe005aae
ms.sourcegitcommit: af3473779cd7c2978f290fbdc51ee15eb1130840
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2018
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a>Guida introduttiva: Distribuire una macchina virtuale da un modello con Azure SDK per Go

Questa guida introduttiva è incentrata sulla distribuzione di risorse da un modello con Azure SDK per Go. I modelli sono snapshot di tutte le risorse incluse in un [gruppo di risorse di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview). Sarà possibile acquisire familiarità con la funzionalità e le convenzioni dell'SDK durante l'esecuzione di un'attività utile.

Al termine della guida introduttiva sarà disponibile una VM in esecuzione a cui si accede con un nome utente e una password.

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

Se si usa un'installazione locale dell'interfaccia della riga di comando di Azure, questa guida introduttiva richiede l'interfaccia della riga di comando versione 2.0.24 o successiva. Eseguire `az --version` per assicurarsi che l'installazione dell'interfaccia della riga di comando rispetti questo requisito. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli).

## <a name="install-the-azure-sdk-for-go"></a>Installare Azure SDK per Go 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a>Creare un'entità servizio

Per accedere in modalità non interattiva con un'applicazione, è necessaria un'entità servizio. Le entità servizio rientrano nel controllo degli accessi in base al ruolo, che crea un'identità univoca per l'utente. Per creare una nuova entità servizio con l'interfaccia della riga di comando, eseguire questo comando:

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart
```

__Assicurarsi__ di registrare i valori `appId`, `password` e `tenant` nell'output. Questi valori vengono usati dall'applicazione per l'autenticazione in Azure.

Per altre informazioni sulla creazione e sulla gestione delle entità servizio con l'interfaccia della riga di comando di Azure 2.0, vedere [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).

## <a name="get-the-code"></a>Ottenere il codice

Ottenere il codice della guida introduttiva e tutte le rispettive dipendenze con `go get`.

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm/...
```

È possibile compilare questo codice, ma per eseguirlo correttamente è necessario specificare informazioni sull'account Azure e sull'entità servizio creata. In `main.go` è disponibile una variabile, `config`, che include uno struct `authInfo`. Per un'autenticazione corretta è necessario che i valori dei campi dello struct vengano sostituiti.

```go
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }
```

* `SubscriptionID`: ID sottoscrizione, che può essere ottenuto dal comando dell'interfaccia della riga di comando

  ```azurecli-interactive
  az account show --query id -o tsv
  ```

* `TenantID`: ID del tenant, corrispondente al valore `tenant` registrato durante la creazione dell'entità servizio
* `ServicePrincipalID`: valore `appId` registrato durante la creazione dell'entità servizio
* `ServicePrincipalSecret`: valore `password` registrato durante la creazione dell'entità servizio

È anche necessario modificare un valore nel file `vm-quickstart-params.json`.

```json
    "vm_password": {
        "value": "_"
    }
```

* `vm_password`: password per l'account utente della macchina virtuale. Deve comprendere tra 12 e 72 caratteri e includere 3 dei caratteri seguenti:
  * Una lettera minuscola
  * Una lettera maiuscola
  * Un numero
  * Un simbolo

## <a name="running-the-code"></a>Esecuzione del codice

Eseguire la guida introduttiva con il comando `go run`.

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm
go run main.go
```

In caso di errore nella distribuzione, viene visualizzato un messaggio che indica che si è verificato un problema, ma senza dettagli specifici. Tramite l'interfaccia della riga di comando di Azure, ottenere i dettagli dell'errore di distribuzione con il comando seguente:

```azurecli-interactive
az group deployment show -g GoVMQuickstart -n VMDeployQuickstart
```

Se la distribuzione ha esito positivo, viene visualizzato un messaggio che indica nome utente, indirizzo IP e password per l'accesso alla macchina virtuale appena creata. Accedere tramite SSH alla macchina virtuale per verificare che sia attiva e in esecuzione.

## <a name="cleaning-up"></a>Cleaning up

Pulire le risorse create durante la guida introduttiva eliminando il gruppo di risorse con l'interfaccia della riga di comando.

```azurecli-interactive
az group delete -n GoVMQuickstart
```

## <a name="code-in-depth"></a>Informazioni dettagliate sul codice

Le operazioni eseguite dal codice della guida introduttiva vengono suddivise in un blocco di variabili e di alcune piccole funzioni, ognuna delle quali viene illustrata in questo articolo.

### <a name="variable-assignments-and-structs"></a>Assegnazioni e struct delle variabili

Poiché il codice della guida introduttiva è autonomo, usa variabili globali invece delle opzioni da riga di comando o delle variabili di ambiente.

```go
type authInfo struct {
        TenantID               string
        SubscriptionID         string
        ServicePrincipalID     string
        ServicePrincipalSecret string
}
```

Lo struct `authInfo` viene dichiarato per incapsulare tutte le informazioni necessarie per l'autorizzazione nei servizi di Azure.

```go
const (
    resourceGroupName     = "GoVMQuickstart"
    resourceGroupLocation = "eastus"

    deploymentName = "VMDeployQuickstart"
    templateFile   = "vm-quickstart-template.json"
    parametersFile = "vm-quickstart-params.json"
)

var (
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }

    ctx = context.Background()

    token *adal.ServicePrincipalToken
)
```

Vengono dichiarati i valori che specificano i nomi delle risorse create. Viene specificata anche la posizione, che può essere modificata per verificare il comportamento delle distribuzioni in altri data center. Non tutte le risorse necessarie sono disponibili in tutti i data center.

Le costanti `templateFile` e `parametersFile` fanno riferimento ai file necessari per la distribuzione. Il token dell'entità servizio viene illustrato più avanti e la variabile `ctx` è un [contesto di Go](https://blog.golang.org/context) per le operazioni di rete.

### <a name="init-and-authorization"></a>Metodo init() e autorizzazione

Il metodo `init()` per il codice configura l'autorizzazione. Poiché l'autorizzazione è una precondizione per qualsiasi operazione nella guida introduttiva, è consigliabile includerla nell'inizializzazione. 

```go
// Authenticate with the Azure services over OAuth, using a service principal.
func init() {
    oauthConfig, err := adal.NewOAuthConfig(azure.PublicCloud.ActiveDirectoryEndpoint, config.TenantID)
    if err != nil {
        log.Fatalf("Failed to get OAuth config: %v\n", err)
    }
    token, err = adal.NewServicePrincipalToken(
        *oauthConfig,
        config.ServicePrincipalID,
        config.ServicePrincipalSecret,
        azure.PublicCloud.ResourceManagerEndpoint)
    if err != nil {
        log.Fatalf("faled to get token: %v\n", err)
    }
}
```

Questo codice completa due passaggi per l'autorizzazione:

* Le informazioni di configurazione OAuth per `TenantID` vengono recuperate tramite l'interazione con Azure Active Directory. L'oggetto [`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) contiene gli endpoint usati nella configurazione Standard di Azure.
* Viene chiamata la funzione [`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken). Questa funzione accetta le informazioni OAuth insieme alle credenziali di accesso dell'entità servizio, oltre a indicazioni sulla modalità di gestione usata per Azure. A meno che non siano necessari requisiti specifici e non si sia esperti, questo valore deve essere sempre `.ResourceManagerEndpoint`.

### <a name="flow-of-operations-in-main"></a>Flusso di operazioni in main()

La funzione `main()` è semplice e indica solo il flusso di operazioni e l'esecuzione del controllo degli errori.

```go
func main() {
    group, err := createGroup()
    if err != nil {
        log.Fatalf("failed to create group: %v", err)
    }
    log.Printf("created group: %v\n", *group.Name)

    log.Println("starting deployment")
    result, err := createDeployment()
    if err != nil {
        log.Fatalf("Failed to deploy correctly: %v", err)
    }
    log.Printf("Completed deployment: %v", *result.Name)
    getLogin()
}
```

Il codice esegue questi passaggi nell'ordine seguente:

* Creare il gruppo di risorse in cui eseguire la distribuzione (`createGroup()`)
* Creare la distribuzione all'interno del gruppo (`createDeployment()`)
* Ottenere e visualizzare le informazioni di accesso per la VM distribuita (`getLogin()`)

### <a name="creating-the-resource-group"></a>Creazione del gruppo di risorse

La funzione `createGroup()` crea il gruppo di risorse. È possibile esaminare il flusso di chiamate e di argomenti per verificare la struttura delle interazioni tra i servizi nell'SDK.

```go
func createGroup() (group resources.Group, err error) {
        groupsClient := resources.NewGroupsClient(config.SubscriptionID)
        groupsClient.Authorizer = autorest.NewBearerAuthorizer(token)

        return groupsClient.CreateOrUpdate(
                ctx,
                resourceGroupName,
                resources.Group{
                        Location: to.StringPtr(resourceGroupLocation)})
}
```

Questo è il flusso generale dell'interazione con un servizio di Azure:

* Creare il client con il metodo `service.NewXClient()`, dove `X` è il tipo di risorsa di `service` con cui si vuole interagire. Questa funzione accetta sempre un ID sottoscrizione.
* Impostare il metodo di autorizzazione per il client, consentendo l'interazione con l'API remota.
* Effettuare la chiamata al metodo sul client corrispondente all'API remota. I metodi del client del servizio accettano in genere il nome della risorsa e un oggetto di metadati.

La funzione [`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) viene usata qui per eseguire un tipo di conversione. Gli struct dei parametri per i metodi dell'SDK accettano quasi esclusivamente puntatori, quindi questi metodi vengono forniti per semplificare le conversioni dei tipi. Per un elenco completo e informazioni sul comportamento dei convertitori utili, vedere la documentazione per il modulo [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to).

L'operazione `groupsClient.CreateOrUpdate()` restituisce un puntatore a uno struct di dati che rappresenta il gruppo di risorse. Un valore restituito diretto di questo tipo indica un'operazione a esecuzione ridotta che deve essere asincrona. Nella sezione successiva è disponibile un esempio di operazione a esecuzione prolungata e viene illustrato come interagire con tali operazioni.

### <a name="performing-the-deployment"></a>Esecuzione della distribuzione

Dopo la creazione del gruppo che include le risorse, è possibile eseguire la distribuzione. Il codice viene suddiviso in sezioni di dimensioni minori per evidenziare le diverse parti della logica.


```go
func createDeployment() (deployment resources.DeploymentExtended, err error) {
    template, err := readJSON(templateFile)
    if err != nil {
        return
    }
    params, err := readJSON(parametersFile)
    if err != nil {
        return
    }

        // ...
```

I file della distribuzione vengono caricati da `readJSON`, per cui non vengono forniti dettagli. Questa funzione restituisce `*map[string]interface{}`, il tipo usato nella creazione dei metadati per la chiamata alla distribuzione delle risorse.

```go
        // ...
        
        deploymentsClient := resources.NewDeploymentsClient(config.SubscriptionID)
        deploymentsClient.Authorizer = autorest.NewBearerAuthorizer(token)

        deploymentFuture, err := deploymentsClient.CreateOrUpdate(
                ctx,
                resourceGroupName,
                deploymentName,
                resources.Deployment{
                        Properties: &resources.DeploymentProperties{
                                Template:   template,
                                Parameters: params,
                                Mode:       resources.Incremental,
                        },
                },
        )
        if err != nil {
                log.Fatalf("Failed to create deployment: %v", err)
        }
        //...
```

Il codice segue lo stesso modello della creazione del gruppo di risorse. Viene creato un nuovo client, a cui viene consentita l'autenticazione in Azure, e quindi viene chiamato un metodo. Il metodo ha addirittura lo stesso nome (`CreateOrUpdate`) del metodo corrispondente per i gruppi di risorse. Questo modello si ripete nell'SDK. I metodi che eseguono operazioni simili hanno in genere lo stesso nome.

La differenza principale è costituita dal valore restituito del metodo `deploymentsClient.CreateOrUpdate()`. Questo valore è un oggetto `Future`, che segue lo [schema progettuale degli oggetti Future](https://en.wikipedia.org/wiki/Futures_and_promises). Gli oggetti Future rappresentano un'operazione a esecuzione prolungata in Azure di cui è possibile che si voglia eseguire occasionalmente il polling durante l'esecuzione di altre attività.

```go
        //...
        err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
        if err != nil {
                log.Fatalf("Error while waiting for deployment creation: %v", err)
        }
        return deploymentFuture.Result(deploymentsClient)
}
```

Per questo esempio è consigliabile attendere il completamento dell'operazione. Per rimanere in attesa di un oggetto Future sono necessari un [oggetto context](https://blog.golang.org/context) e il client che ha creato l'oggetto Future. È possibile che si verifichino due tipi di errore, ovvero un errore provocato sul lato client durante il tentativo di chiamata del metodo e una risposta di errore dal server. Quest'ultimo tipo di errore viene restituito come parte della chiamata `deploymentFuture.Result()`.

### <a name="obtaining-the-assigned-ip-address"></a>Ottenere l'indirizzo IP assegnato

Per eseguire qualsiasi operazione con la macchina virtuale appena creata, è necessario l'indirizzo IP assegnato. Gli indirizzi IP sono risorse di Azure distinte, associate a risorse della scheda di interfaccia di rete.

```go
func getLogin() {
        params, err := readJSON(parametersFile)
        if err != nil {
                log.Fatalf("Unable to read parameters. Get login information with `az network public-ip list -g %s", resourceGroupName)
        }

        addressClient := network.NewPublicIPAddressesClient(config.SubscriptionID)
        addressClient.Authorizer = autorest.NewBearerAuthorizer(token)
        ipName := (*params)["publicIPAddresses_QuickstartVM_ip_name"].(map[string]interface{})
        ipAddress, err := addressClient.Get(ctx, resourceGroupName, ipName["value"].(string), "")
        if err != nil {
                log.Fatalf("Unable to get IP information. Try using `az network public-ip list -g %s", resourceGroupName)
        }

        vmUser := (*params)["vm_user"].(map[string]interface{})
        vmPass := (*params)["vm_password"].(map[string]interface{})

        log.Printf("Log in with ssh: %s@%s, password: %s",
                vmUser["value"].(string),
                *ipAddress.PublicIPAddressPropertiesFormat.IPAddress,
                vmPass["value"].(string))
}
```

Questo metodo si basa su informazioni archiviate nel file dei parametri. Il codice può eseguire query direttamente sulla macchina virtuale per ottenere la rispettiva scheda di interfaccia di rete, può eseguire query sulla scheda di interfaccia di rete per ottenere la rispettiva risorsa IP e quindi può eseguire query direttamente sulla risorsa IP. È prevista una lunga catena di dipendenze e operazioni da risolvere, che risulta costosa. Poiché le informazioni JSON sono locali, è anche possibile caricarle.

Anche i valori per l'utente e la password della macchina virtuale vengono caricati da the JSON.

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stato selezionato un modello esistente e il modello è stato distribuito tramite Go. È stata quindi stabilita la connessione alla macchina virtuale appena creata tramite SSH per verificarne l'esecuzione.

Per continuare a ottenere informazioni sull'uso delle macchine virtuali nell'ambiente di Azure con Go, vedere gli [esempi di calcolo di Azure per Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) o gli [esempi di gestione delle risorse di Azure per Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).
