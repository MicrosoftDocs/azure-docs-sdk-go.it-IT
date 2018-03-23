---
title: Distribuire una macchina virtuale di Azure da Go
description: Distribuire una macchina virtuale tramite Azure SDK per Go.
author: sptramer
ms.author: sttramer
ms.date: 02/08/2018
ms.topic: quickstart
ms.devlang: go
manager: carmonm
ms.openlocfilehash: 46a1243ff2ff6bfcf3831e2cea3137c1f6051c78
ms.sourcegitcommit: fcc1786d59d2e32c97a9a8e0748e06f564a961bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a><span data-ttu-id="b5706-103">Guida introduttiva: Distribuire una macchina virtuale da un modello con Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="b5706-103">Quickstart: Deploy an Azure virtual machine from a template with the Azure SDK for Go</span></span>

<span data-ttu-id="b5706-104">Questa guida introduttiva è incentrata sulla distribuzione di risorse da un modello con Azure SDK per Go.</span><span class="sxs-lookup"><span data-stu-id="b5706-104">This quickstart focuses on deploying resources from a template with the Azure SDK for Go.</span></span> <span data-ttu-id="b5706-105">I modelli sono snapshot di tutte le risorse incluse in un [gruppo di risorse di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="b5706-105">Templates are snapshots of all of the resources contained within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span> <span data-ttu-id="b5706-106">Sarà possibile acquisire familiarità con la funzionalità e le convenzioni dell'SDK durante l'esecuzione di un'attività utile.</span><span class="sxs-lookup"><span data-stu-id="b5706-106">Along the way, you'll become familiar with the functionality and conventions of the SDK while performing a useful task.</span></span>

<span data-ttu-id="b5706-107">Al termine della guida introduttiva sarà disponibile una VM in esecuzione a cui si accede con un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="b5706-107">At the end of this quickstart, you have a running VM that you log into with a username and password.</span></span>

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

<span data-ttu-id="b5706-108">Se si usa un'installazione locale dell'interfaccia della riga di comando di Azure, questa guida introduttiva richiede l'interfaccia della riga di comando versione 2.0.24 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b5706-108">If you use a local install of the Azure CLI, this quickstart requires CLI version 2.0.24 or later.</span></span> <span data-ttu-id="b5706-109">Eseguire `az --version` per assicurarsi che l'installazione dell'interfaccia della riga di comando rispetti questo requisito.</span><span class="sxs-lookup"><span data-stu-id="b5706-109">Run `az --version` to make sure your CLI install meets this requirement.</span></span> <span data-ttu-id="b5706-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b5706-110">If you need to install or upgrade, see [Install the Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="b5706-111">Installare Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="b5706-111">Install the Azure SDK for Go</span></span> 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a><span data-ttu-id="b5706-112">Creare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="b5706-112">Create a service principal</span></span>

<span data-ttu-id="b5706-113">Per accedere in modalità non interattiva con un'applicazione, è necessaria un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b5706-113">To log in non-interactively with an application, you need a service principal.</span></span> <span data-ttu-id="b5706-114">Le entità servizio rientrano nel controllo degli accessi in base al ruolo, che crea un'identità univoca per l'utente.</span><span class="sxs-lookup"><span data-stu-id="b5706-114">Service principals are part of role-based access control (RBAC), which creates a unique user identity.</span></span> <span data-ttu-id="b5706-115">Per creare una nuova entità servizio con l'interfaccia della riga di comando, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="b5706-115">To create a new service principal with the CLI, run the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart
```

<span data-ttu-id="b5706-116">__Assicurarsi__ di registrare i valori `appId`, `password` e `tenant` nell'output.</span><span class="sxs-lookup"><span data-stu-id="b5706-116">__Make sure__ to record the `appId`, `password`, and `tenant` values in the output.</span></span> <span data-ttu-id="b5706-117">Questi valori vengono usati dall'applicazione per l'autenticazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="b5706-117">These values are used by the application to authenticate with Azure.</span></span>

<span data-ttu-id="b5706-118">Per altre informazioni sulla creazione e sulla gestione delle entità servizio con l'interfaccia della riga di comando di Azure 2.0, vedere [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b5706-118">For more information on creating and managing service principals with the Azure CLI 2.0, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>

## <a name="get-the-code"></a><span data-ttu-id="b5706-119">Ottenere il codice</span><span class="sxs-lookup"><span data-stu-id="b5706-119">Get the code</span></span>

<span data-ttu-id="b5706-120">Ottenere il codice della guida introduttiva e tutte le rispettive dipendenze con `go get`.</span><span class="sxs-lookup"><span data-stu-id="b5706-120">Get the quickstart code and all of its dependencies with `go get`.</span></span>

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm/...
```

<span data-ttu-id="b5706-121">È possibile compilare questo codice, ma per eseguirlo correttamente è necessario specificare informazioni sull'account Azure e sull'entità servizio creata.</span><span class="sxs-lookup"><span data-stu-id="b5706-121">This code compiles, but doesn't run correctly until you provide it information about your Azure account and the created service principal.</span></span> <span data-ttu-id="b5706-122">In `main.go` è disponibile una variabile, `config`, che include uno struct `authInfo`.</span><span class="sxs-lookup"><span data-stu-id="b5706-122">In `main.go` there is a variable, `config`, which contains an `authInfo` struct.</span></span> <span data-ttu-id="b5706-123">Per un'autenticazione corretta è necessario che i valori dei campi dello struct vengano sostituiti.</span><span class="sxs-lookup"><span data-stu-id="b5706-123">This struct needs to have its field values replaced in order to authenticate correctly.</span></span>

```go
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }
```

* <span data-ttu-id="b5706-124">`SubscriptionID`: ID sottoscrizione, che può essere ottenuto dal comando dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="b5706-124">`SubscriptionID`: Your subscription ID, which can be obtained from the CLI command</span></span>

  ```azurecli-interactive
  az account show --query id -o tsv
  ```

* <span data-ttu-id="b5706-125">`TenantID`: ID del tenant, corrispondente al valore `tenant` registrato durante la creazione dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="b5706-125">`TenantID`: Your tenant ID, the `tenant` value recorded when creating the service principal</span></span>
* <span data-ttu-id="b5706-126">`ServicePrincipalID`: valore `appId` registrato durante la creazione dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="b5706-126">`ServicePrincipalID`: The `appId` value recorded when creating the service principal</span></span>
* <span data-ttu-id="b5706-127">`ServicePrincipalSecret`: valore `password` registrato durante la creazione dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="b5706-127">`ServicePrincipalSecret`: The `password` value recorded when creating the service principal</span></span>

<span data-ttu-id="b5706-128">È anche necessario modificare un valore nel file `vm-quickstart-params.json`.</span><span class="sxs-lookup"><span data-stu-id="b5706-128">You also need to edit a value in the `vm-quickstart-params.json` file.</span></span>

```json
    "vm_password": {
        "value": "_"
    }
```

* <span data-ttu-id="b5706-129">`vm_password`: password per l'account utente della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b5706-129">`vm_password`: The password for the VM user account.</span></span> <span data-ttu-id="b5706-130">Deve comprendere tra 12 e 72 caratteri e includere 3 dei caratteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5706-130">It must be 12-72 characters in length and contain 3 of the following characters:</span></span>
  * <span data-ttu-id="b5706-131">Una lettera minuscola</span><span class="sxs-lookup"><span data-stu-id="b5706-131">A lowercase letter</span></span>
  * <span data-ttu-id="b5706-132">Una lettera maiuscola</span><span class="sxs-lookup"><span data-stu-id="b5706-132">An uppercase letter</span></span>
  * <span data-ttu-id="b5706-133">Un numero</span><span class="sxs-lookup"><span data-stu-id="b5706-133">A number</span></span>
  * <span data-ttu-id="b5706-134">Un simbolo</span><span class="sxs-lookup"><span data-stu-id="b5706-134">A symbol</span></span>

## <a name="running-the-code"></a><span data-ttu-id="b5706-135">Esecuzione del codice</span><span class="sxs-lookup"><span data-stu-id="b5706-135">Running the code</span></span>

<span data-ttu-id="b5706-136">Eseguire la guida introduttiva con il comando `go run`.</span><span class="sxs-lookup"><span data-stu-id="b5706-136">Run the quickstart with the `go run` command.</span></span>

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm
go run main.go
```

<span data-ttu-id="b5706-137">In caso di errore nella distribuzione, viene visualizzato un messaggio che indica che si è verificato un problema, ma senza dettagli specifici.</span><span class="sxs-lookup"><span data-stu-id="b5706-137">If there is a failure in the deployment, you get a message indicating that there was an issue, but without any specific details.</span></span> <span data-ttu-id="b5706-138">Tramite l'interfaccia della riga di comando di Azure, ottenere i dettagli dell'errore di distribuzione con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b5706-138">Using the Azure CLI, get the details of the deployment failure with the following command:</span></span>

```azurecli-interactive
az group deployment show -g GoVMQuickstart -n VMDeployQuickstart
```

<span data-ttu-id="b5706-139">Se la distribuzione ha esito positivo, viene visualizzato un messaggio che indica nome utente, indirizzo IP e password per l'accesso alla macchina virtuale appena creata.</span><span class="sxs-lookup"><span data-stu-id="b5706-139">If the deployment is successful, you see a message giving the username, IP address, and password for logging into the newly created virtual machine.</span></span> <span data-ttu-id="b5706-140">Accedere tramite SSH alla macchina virtuale per verificare che sia attiva e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b5706-140">SSH into this machine to confirm that it is up and running.</span></span>

## <a name="cleaning-up"></a><span data-ttu-id="b5706-141">Cleaning up</span><span class="sxs-lookup"><span data-stu-id="b5706-141">Cleaning up</span></span>

<span data-ttu-id="b5706-142">Pulire le risorse create durante la guida introduttiva eliminando il gruppo di risorse con l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b5706-142">Clean up the resources created during this quickstart by deleting the resource group with the CLI.</span></span>

```azurecli-interactive
az group delete -n GoVMQuickstart
```

## <a name="code-in-depth"></a><span data-ttu-id="b5706-143">Informazioni dettagliate sul codice</span><span class="sxs-lookup"><span data-stu-id="b5706-143">Code in depth</span></span>

<span data-ttu-id="b5706-144">Le operazioni eseguite dal codice della guida introduttiva vengono suddivise in un blocco di variabili e di alcune piccole funzioni, ognuna delle quali viene illustrata in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b5706-144">What the quickstart code does is broken down into a block of variables and several small functions, each of which are discussed here.</span></span>

### <a name="variable-assignments-and-structs"></a><span data-ttu-id="b5706-145">Assegnazioni e struct delle variabili</span><span class="sxs-lookup"><span data-stu-id="b5706-145">Variable assignments and structs</span></span>

<span data-ttu-id="b5706-146">Poiché il codice della guida introduttiva è autonomo, usa variabili globali invece delle opzioni da riga di comando o delle variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="b5706-146">Since quickstart is self-contained, it uses global variables rather than command-line options or environment variables.</span></span>

```go
type authInfo struct {
        TenantID               string
        SubscriptionID         string
        ServicePrincipalID     string
        ServicePrincipalSecret string
}
```

<span data-ttu-id="b5706-147">Lo struct `authInfo` viene dichiarato per incapsulare tutte le informazioni necessarie per l'autorizzazione nei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5706-147">The `authInfo` struct is declared to encapsulate all of the information needed for authorization with Azure services.</span></span>

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

<span data-ttu-id="b5706-148">Vengono dichiarati i valori che specificano i nomi delle risorse create.</span><span class="sxs-lookup"><span data-stu-id="b5706-148">Values are declared which give the names of created resources.</span></span> <span data-ttu-id="b5706-149">Viene specificata anche la posizione, che può essere modificata per verificare il comportamento delle distribuzioni in altri data center.</span><span class="sxs-lookup"><span data-stu-id="b5706-149">The location is also specified here, which you can change to see how deployments behave in other datacenters.</span></span> <span data-ttu-id="b5706-150">Non tutte le risorse necessarie sono disponibili in tutti i data center.</span><span class="sxs-lookup"><span data-stu-id="b5706-150">Not every datacenter has all of the required resources available.</span></span>

<span data-ttu-id="b5706-151">Le costanti `templateFile` e `parametersFile` fanno riferimento ai file necessari per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b5706-151">The `templateFile` and `parametersFile` constants point to the files needed for deployment.</span></span> <span data-ttu-id="b5706-152">Il token dell'entità servizio viene illustrato più avanti e la variabile `ctx` è un [contesto di Go](https://blog.golang.org/context) per le operazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="b5706-152">The service principal token is covered later, and the `ctx` variable is a [Go context](https://blog.golang.org/context) for the network operations.</span></span>

### <a name="init-and-authorization"></a><span data-ttu-id="b5706-153">Metodo init() e autorizzazione</span><span class="sxs-lookup"><span data-stu-id="b5706-153">init() and authorization</span></span>

<span data-ttu-id="b5706-154">Il metodo `init()` per il codice configura l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="b5706-154">The `init()` method for the code sets up authorization.</span></span> <span data-ttu-id="b5706-155">Poiché l'autorizzazione è una precondizione per qualsiasi operazione nella guida introduttiva, è consigliabile includerla nell'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="b5706-155">Since authorization is a precondition for everything in the quickstart, it makes sense to have it as part of initialization.</span></span> 

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

<span data-ttu-id="b5706-156">Questo codice completa due passaggi per l'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="b5706-156">This code completes two steps for authorization:</span></span>

* <span data-ttu-id="b5706-157">Le informazioni di configurazione OAuth per `TenantID` vengono recuperate tramite l'interazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5706-157">OAuth configuration information for the `TenantID` is retrieved by interfacing with Azure Active Directory.</span></span> <span data-ttu-id="b5706-158">L'oggetto [`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) contiene gli endpoint usati nella configurazione Standard di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5706-158">The [`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) object contains endpoints used in the standard Azure configuration.</span></span>
* <span data-ttu-id="b5706-159">Viene chiamata la funzione [`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken).</span><span class="sxs-lookup"><span data-stu-id="b5706-159">The [`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken) function is called.</span></span> <span data-ttu-id="b5706-160">Questa funzione accetta le informazioni OAuth insieme alle credenziali di accesso dell'entità servizio, oltre a indicazioni sulla modalità di gestione usata per Azure.</span><span class="sxs-lookup"><span data-stu-id="b5706-160">This function takes the OAuth information along with the service principal login, as well as which style of Azure management is being used.</span></span> <span data-ttu-id="b5706-161">A meno che non siano necessari requisiti specifici e non si sia esperti, questo valore deve essere sempre `.ResourceManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="b5706-161">Unless you have specific requirements and know what you're doing, this value should always be `.ResourceManagerEndpoint`.</span></span>

### <a name="flow-of-operations-in-main"></a><span data-ttu-id="b5706-162">Flusso di operazioni in main()</span><span class="sxs-lookup"><span data-stu-id="b5706-162">Flow of operations in main()</span></span>

<span data-ttu-id="b5706-163">La funzione `main()` è semplice e indica solo il flusso di operazioni e l'esecuzione del controllo degli errori.</span><span class="sxs-lookup"><span data-stu-id="b5706-163">The `main()` function is simple, only indicating the flow of operations and performing error-checking.</span></span>

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

<span data-ttu-id="b5706-164">Il codice esegue questi passaggi nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="b5706-164">The steps that the code runs through are, in order:</span></span>

* <span data-ttu-id="b5706-165">Creare il gruppo di risorse in cui eseguire la distribuzione (`createGroup()`)</span><span class="sxs-lookup"><span data-stu-id="b5706-165">Create the resource group to deploy to (`createGroup()`)</span></span>
* <span data-ttu-id="b5706-166">Creare la distribuzione all'interno del gruppo (`createDeployment()`)</span><span class="sxs-lookup"><span data-stu-id="b5706-166">Create the deployment within this group (`createDeployment()`)</span></span>
* <span data-ttu-id="b5706-167">Ottenere e visualizzare le informazioni di accesso per la VM distribuita (`getLogin()`)</span><span class="sxs-lookup"><span data-stu-id="b5706-167">Obtain and display login information for the deployed VM (`getLogin()`)</span></span>

### <a name="creating-the-resource-group"></a><span data-ttu-id="b5706-168">Creazione del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="b5706-168">Creating the resource group</span></span>

<span data-ttu-id="b5706-169">La funzione `createGroup()` crea il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b5706-169">The `createGroup()` function creates the resource group.</span></span> <span data-ttu-id="b5706-170">È possibile esaminare il flusso di chiamate e di argomenti per verificare la struttura delle interazioni tra i servizi nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="b5706-170">Looking at the call flow and arguments demonstrates the way that service interactions are structured in the SDK.</span></span>

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

<span data-ttu-id="b5706-171">Questo è il flusso generale dell'interazione con un servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="b5706-171">The general flow of interacting with an Azure service is:</span></span>

* <span data-ttu-id="b5706-172">Creare il client con il metodo `service.NewXClient()`, dove `X` è il tipo di risorsa di `service` con cui si vuole interagire.</span><span class="sxs-lookup"><span data-stu-id="b5706-172">Create the client using the `service.NewXClient()` method, where `X` is the resource type of the `service` that you want to interact with.</span></span> <span data-ttu-id="b5706-173">Questa funzione accetta sempre un ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b5706-173">This function always takes a subscription ID.</span></span>
* <span data-ttu-id="b5706-174">Impostare il metodo di autorizzazione per il client, consentendo l'interazione con l'API remota.</span><span class="sxs-lookup"><span data-stu-id="b5706-174">Set the authorization method for the client, allowing it to interact with the remote API.</span></span>
* <span data-ttu-id="b5706-175">Effettuare la chiamata al metodo sul client corrispondente all'API remota.</span><span class="sxs-lookup"><span data-stu-id="b5706-175">Make the method call on the client corresponding to the remote API.</span></span> <span data-ttu-id="b5706-176">I metodi del client del servizio accettano in genere il nome della risorsa e un oggetto di metadati.</span><span class="sxs-lookup"><span data-stu-id="b5706-176">Service client methods usually take the name of the resource and a metadata object.</span></span>

<span data-ttu-id="b5706-177">La funzione [`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) viene usata qui per eseguire un tipo di conversione.</span><span class="sxs-lookup"><span data-stu-id="b5706-177">The [`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) function is used to perform a type conversion here.</span></span> <span data-ttu-id="b5706-178">Gli struct dei parametri per i metodi dell'SDK accettano quasi esclusivamente puntatori, quindi questi metodi vengono forniti per semplificare le conversioni dei tipi.</span><span class="sxs-lookup"><span data-stu-id="b5706-178">The parameters structs for methods of the SDK almost exclusively take pointers, so these methods are provided to make the type conversions easy.</span></span> <span data-ttu-id="b5706-179">Per un elenco completo e informazioni sul comportamento dei convertitori utili, vedere la documentazione per il modulo [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to).</span><span class="sxs-lookup"><span data-stu-id="b5706-179">See the documentation for the [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) module for the complete list and behavior of convenience converters.</span></span>

<span data-ttu-id="b5706-180">L'operazione `groupsClient.CreateOrUpdate()` restituisce un puntatore a uno struct di dati che rappresenta il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b5706-180">The `groupsClient.CreateOrUpdate()` operation returns a pointer to a data struct representing the resource group.</span></span> <span data-ttu-id="b5706-181">Un valore restituito diretto di questo tipo indica un'operazione a esecuzione ridotta che deve essere asincrona.</span><span class="sxs-lookup"><span data-stu-id="b5706-181">A direct return value of this kind indicates a short-running operation that is meant to be synchronous.</span></span> <span data-ttu-id="b5706-182">Nella sezione successiva è disponibile un esempio di operazione a esecuzione prolungata e viene illustrato come interagire con tali operazioni.</span><span class="sxs-lookup"><span data-stu-id="b5706-182">In the next section, you'll see an example of a long-running operation and how to interact with them.</span></span>

### <a name="performing-the-deployment"></a><span data-ttu-id="b5706-183">Esecuzione della distribuzione</span><span class="sxs-lookup"><span data-stu-id="b5706-183">Performing the deployment</span></span>

<span data-ttu-id="b5706-184">Dopo la creazione del gruppo che include le risorse, è possibile eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b5706-184">Once the group to contain its resources is created, it's time to run the deployment.</span></span> <span data-ttu-id="b5706-185">Il codice viene suddiviso in sezioni di dimensioni minori per evidenziare le diverse parti della logica.</span><span class="sxs-lookup"><span data-stu-id="b5706-185">This code is broken up into smaller sections to emphasize different parts of its logic.</span></span>


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

<span data-ttu-id="b5706-186">I file della distribuzione vengono caricati da `readJSON`, per cui non vengono forniti dettagli.</span><span class="sxs-lookup"><span data-stu-id="b5706-186">The deployment files are loaded by `readJSON`, the details of which are skipped here.</span></span> <span data-ttu-id="b5706-187">Questa funzione restituisce `*map[string]interface{}`, il tipo usato nella creazione dei metadati per la chiamata alla distribuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="b5706-187">This function returns a `*map[string]interface{}`, the type used in constructing the metadata for the resource deployment call.</span></span>

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

<span data-ttu-id="b5706-188">Il codice segue lo stesso modello della creazione del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b5706-188">This code follows the same pattern as with creating the resource group.</span></span> <span data-ttu-id="b5706-189">Viene creato un nuovo client, a cui viene consentita l'autenticazione in Azure, e quindi viene chiamato un metodo.</span><span class="sxs-lookup"><span data-stu-id="b5706-189">A new client is created, given the ability to authenticate with Azure, and then a method is called.</span></span> <span data-ttu-id="b5706-190">Il metodo ha addirittura lo stesso nome (`CreateOrUpdate`) del metodo corrispondente per i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="b5706-190">The method even has the same name (`CreateOrUpdate`) as the corresponding method for resource groups.</span></span> <span data-ttu-id="b5706-191">Questo modello si ripete nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="b5706-191">This pattern is seen again and again in the SDK.</span></span> <span data-ttu-id="b5706-192">I metodi che eseguono operazioni simili hanno in genere lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="b5706-192">Methods that perform similar work normally have the same name.</span></span>

<span data-ttu-id="b5706-193">La differenza principale è costituita dal valore restituito del metodo `deploymentsClient.CreateOrUpdate()`.</span><span class="sxs-lookup"><span data-stu-id="b5706-193">The biggest difference comes in the return value of the `deploymentsClient.CreateOrUpdate()` method.</span></span> <span data-ttu-id="b5706-194">Questo valore è un oggetto `Future`, che segue lo [schema progettuale degli oggetti Future](https://en.wikipedia.org/wiki/Futures_and_promises).</span><span class="sxs-lookup"><span data-stu-id="b5706-194">This value is a `Future` object, which follows the [future design pattern](https://en.wikipedia.org/wiki/Futures_and_promises).</span></span> <span data-ttu-id="b5706-195">Gli oggetti Future rappresentano un'operazione a esecuzione prolungata in Azure di cui è possibile che si voglia eseguire occasionalmente il polling durante l'esecuzione di altre attività.</span><span class="sxs-lookup"><span data-stu-id="b5706-195">Futures represent a long-running operation in Azure that you may want to occasionally poll while performing other work.</span></span>

```go
        //...
        err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
        if err != nil {
                log.Fatalf("Error while waiting for deployment creation: %v", err)
        }
        return deploymentFuture.Result(deploymentsClient)
}
```

<span data-ttu-id="b5706-196">Per questo esempio è consigliabile attendere il completamento dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="b5706-196">For this example, the best thing to do is to wait for the operation to complete.</span></span> <span data-ttu-id="b5706-197">Per rimanere in attesa di un oggetto Future sono necessari un [oggetto context](https://blog.golang.org/context) e il client che ha creato l'oggetto Future.</span><span class="sxs-lookup"><span data-stu-id="b5706-197">Waiting on a future requires both a [context object](https://blog.golang.org/context) and the client that created the Future object.</span></span> <span data-ttu-id="b5706-198">È possibile che si verifichino due tipi di errore, ovvero un errore provocato sul lato client durante il tentativo di chiamata del metodo e una risposta di errore dal server.</span><span class="sxs-lookup"><span data-stu-id="b5706-198">There are two possible error sources here: An error caused on the client side when trying to invoke the method, and an error response from the server.</span></span> <span data-ttu-id="b5706-199">Quest'ultimo tipo di errore viene restituito come parte della chiamata `deploymentFuture.Result()`.</span><span class="sxs-lookup"><span data-stu-id="b5706-199">The latter is returned as part of the `deploymentFuture.Result()` call.</span></span>

### <a name="obtaining-the-assigned-ip-address"></a><span data-ttu-id="b5706-200">Ottenere l'indirizzo IP assegnato</span><span class="sxs-lookup"><span data-stu-id="b5706-200">Obtaining the assigned IP address</span></span>

<span data-ttu-id="b5706-201">Per eseguire qualsiasi operazione con la macchina virtuale appena creata, è necessario l'indirizzo IP assegnato.</span><span class="sxs-lookup"><span data-stu-id="b5706-201">To do anything with the newly created VM, you need the assigned IP address.</span></span> <span data-ttu-id="b5706-202">Gli indirizzi IP sono risorse di Azure distinte, associate a risorse della scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="b5706-202">IP addresses are their own separate Azure resource, bound to Network Interface Controller (NIC) resources.</span></span>

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

<span data-ttu-id="b5706-203">Questo metodo si basa su informazioni archiviate nel file dei parametri.</span><span class="sxs-lookup"><span data-stu-id="b5706-203">This method relies on information that is stored in the parameters file.</span></span> <span data-ttu-id="b5706-204">Il codice può eseguire query direttamente sulla macchina virtuale per ottenere la rispettiva scheda di interfaccia di rete, può eseguire query sulla scheda di interfaccia di rete per ottenere la rispettiva risorsa IP e quindi può eseguire query direttamente sulla risorsa IP.</span><span class="sxs-lookup"><span data-stu-id="b5706-204">The code could query the VM directly to get its NIC, query the NIC to get its IP resource, and then query the IP resource directly.</span></span> <span data-ttu-id="b5706-205">È prevista una lunga catena di dipendenze e operazioni da risolvere, che risulta costosa.</span><span class="sxs-lookup"><span data-stu-id="b5706-205">That's a long chain of dependencies and operations to resolve, making it expensive.</span></span> <span data-ttu-id="b5706-206">Poiché le informazioni JSON sono locali, è anche possibile caricarle.</span><span class="sxs-lookup"><span data-stu-id="b5706-206">Since the JSON information is local, it can be loaded instead.</span></span>

<span data-ttu-id="b5706-207">Anche i valori per l'utente e la password della macchina virtuale vengono caricati da the JSON.</span><span class="sxs-lookup"><span data-stu-id="b5706-207">The values for the VM user and password are likewise loaded from the JSON.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5706-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5706-208">Next steps</span></span>

<span data-ttu-id="b5706-209">In questa guida introduttiva è stato selezionato un modello esistente e il modello è stato distribuito tramite Go.</span><span class="sxs-lookup"><span data-stu-id="b5706-209">In this quickstart, you took an existing template and deployed it through Go.</span></span> <span data-ttu-id="b5706-210">È stata quindi stabilita la connessione alla macchina virtuale appena creata tramite SSH per verificarne l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b5706-210">Then you connected to the newly created VM via SSH to ensure that it's running.</span></span>

<span data-ttu-id="b5706-211">Per continuare a ottenere informazioni sull'uso delle macchine virtuali nell'ambiente di Azure con Go, vedere gli [esempi di calcolo di Azure per Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) o gli [esempi di gestione delle risorse di Azure per Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span><span class="sxs-lookup"><span data-stu-id="b5706-211">To continue learning about working with virtual machines in the Azure environment with Go, take a look at the [Azure compute samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) or [Azure resource management samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span></span>
