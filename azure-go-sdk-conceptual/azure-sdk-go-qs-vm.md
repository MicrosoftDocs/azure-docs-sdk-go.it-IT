---
title: Distribuire una macchina virtuale di Azure da Go
description: Distribuire una macchina virtuale tramite Azure SDK per Go.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 04/03/2018
ms.topic: quickstart
ms.prod: azure
ms.technology: azure-sdk-go
ms.service: virtual-machines
ms.devlang: go
ms.openlocfilehash: 1fbcc54df2a2aebce56c5a5800361f3d3aed1ccc
ms.sourcegitcommit: f08abf902b48f8173aa6e261084ff2cfc9043305
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a><span data-ttu-id="74910-103">Guida introduttiva: Distribuire una macchina virtuale da un modello con Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="74910-103">Quickstart: Deploy an Azure virtual machine from a template with the Azure SDK for Go</span></span>

<span data-ttu-id="74910-104">Questa guida introduttiva è incentrata sulla distribuzione di risorse da un modello con Azure SDK per Go.</span><span class="sxs-lookup"><span data-stu-id="74910-104">This quickstart focuses on deploying resources from a template with the Azure SDK for Go.</span></span> <span data-ttu-id="74910-105">I modelli sono snapshot di tutte le risorse incluse in un [gruppo di risorse di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="74910-105">Templates are snapshots of all of the resources contained within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span> <span data-ttu-id="74910-106">Sarà possibile acquisire familiarità con la funzionalità e le convenzioni dell'SDK durante l'esecuzione di un'attività utile.</span><span class="sxs-lookup"><span data-stu-id="74910-106">Along the way, you'll become familiar with the functionality and conventions of the SDK while performing a useful task.</span></span>

<span data-ttu-id="74910-107">Al termine della guida introduttiva sarà disponibile una VM in esecuzione a cui si accede con un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="74910-107">At the end of this quickstart, you have a running VM that you log into with a username and password.</span></span>

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

<span data-ttu-id="74910-108">Se si usa un'installazione locale dell'interfaccia della riga di comando di Azure, questa guida introduttiva richiede l'interfaccia della riga di comando versione __2.0.28__ o successiva.</span><span class="sxs-lookup"><span data-stu-id="74910-108">If you use a local install of the Azure CLI, this quickstart requires CLI version __2.0.28__ or later.</span></span> <span data-ttu-id="74910-109">Eseguire `az --version` per assicurarsi che l'installazione dell'interfaccia della riga di comando rispetti questo requisito.</span><span class="sxs-lookup"><span data-stu-id="74910-109">Run `az --version` to make sure your CLI install meets this requirement.</span></span> <span data-ttu-id="74910-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="74910-110">If you need to install or upgrade, see [Install the Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="74910-111">Installare Azure SDK per Go</span><span class="sxs-lookup"><span data-stu-id="74910-111">Install the Azure SDK for Go</span></span> 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a><span data-ttu-id="74910-112">Creare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="74910-112">Create a service principal</span></span>


<span data-ttu-id="74910-113">Per accedere in modalità non interattiva con un'applicazione, è necessaria un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="74910-113">To log in non-interactively with an application, you need a service principal.</span></span> <span data-ttu-id="74910-114">Le entità servizio rientrano nel controllo degli accessi in base al ruolo, che crea un'identità univoca per l'utente.</span><span class="sxs-lookup"><span data-stu-id="74910-114">Service principals are part of role-based access control (RBAC), which creates a unique user identity.</span></span> <span data-ttu-id="74910-115">Per creare una nuova entità servizio con l'interfaccia della riga di comando, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="74910-115">To create a new service principal with the CLI, run the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart --sdk-auth > quickstart.auth
```

<span data-ttu-id="74910-116">Impostare la variabile di ambiente `AZURE_AUTH_LOCATION` come percorso completo al file.</span><span class="sxs-lookup"><span data-stu-id="74910-116">Set the environment variable `AZURE_AUTH_LOCATION` to be the full path to this file.</span></span> <span data-ttu-id="74910-117">L'SDK individua e legge le credenziali direttamente da questo file, senza che sia necessario apportare modifiche o registrare informazioni dall'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="74910-117">Then the SDK locates and reads the credentials directly from this file, without you having to make any changes or record information from the service principal.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="74910-118">Ottenere il codice</span><span class="sxs-lookup"><span data-stu-id="74910-118">Get the code</span></span>

<span data-ttu-id="74910-119">Ottenere il codice della guida introduttiva e tutte le rispettive dipendenze con `go get`.</span><span class="sxs-lookup"><span data-stu-id="74910-119">Get the quickstart code and all of its dependencies with `go get`.</span></span>

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstarts/deploy-vm/...
```

<span data-ttu-id="74910-120">Se la variabile `AZURE_AUTH_LOCATION` è impostata correttamente, non è necessario apportare modifiche al codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="74910-120">You don't need to make any source code modifications if the `AZURE_AUTH_LOCATION` variable is properly set.</span></span> <span data-ttu-id="74910-121">Quando viene eseguito il programma, tutte le informazioni di autenticazione necessarie vengono caricati da esso.</span><span class="sxs-lookup"><span data-stu-id="74910-121">When the program runs, it loads all the necessary authentication information from there.</span></span>

## <a name="running-the-code"></a><span data-ttu-id="74910-122">Esecuzione del codice</span><span class="sxs-lookup"><span data-stu-id="74910-122">Running the code</span></span>

<span data-ttu-id="74910-123">Eseguire la guida introduttiva con il comando `go run`.</span><span class="sxs-lookup"><span data-stu-id="74910-123">Run the quickstart with the `go run` command.</span></span>

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstarts/deploy-vm
go run main.go
```

<span data-ttu-id="74910-124">In caso di errore nella distribuzione viene visualizzato un messaggio che indica il verificarsi di un problema, ma senza dettagli esaustivi.</span><span class="sxs-lookup"><span data-stu-id="74910-124">If there is a failure in the deployment, you get a message indicating that there was an issue, but it may not include enough detail.</span></span> <span data-ttu-id="74910-125">Tramite l'interfaccia della riga di comando di Azure, ottenere i dettagli completi dell'errore di distribuzione con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="74910-125">Using the Azure CLI, get the full details of the deployment failure with the following command:</span></span>

```azurecli-interactive
az group deployment show -g GoVMQuickstart -n VMDeployQuickstart
```

<span data-ttu-id="74910-126">Se la distribuzione ha esito positivo, viene visualizzato un messaggio che indica nome utente, indirizzo IP e password per l'accesso alla macchina virtuale appena creata.</span><span class="sxs-lookup"><span data-stu-id="74910-126">If the deployment is successful, you see a message giving the username, IP address, and password for logging into the newly created virtual machine.</span></span> <span data-ttu-id="74910-127">Accedere tramite SSH alla macchina virtuale per verificare che sia attiva e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="74910-127">SSH into this machine to confirm that it is up and running.</span></span>

## <a name="cleaning-up"></a><span data-ttu-id="74910-128">Cleaning up</span><span class="sxs-lookup"><span data-stu-id="74910-128">Cleaning up</span></span>

<span data-ttu-id="74910-129">Pulire le risorse create durante la guida introduttiva eliminando il gruppo di risorse con l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="74910-129">Clean up the resources created during this quickstart by deleting the resource group with the CLI.</span></span>

```azurecli-interactive
az group delete -n GoVMQuickstart
```

## <a name="code-in-depth"></a><span data-ttu-id="74910-130">Informazioni dettagliate sul codice</span><span class="sxs-lookup"><span data-stu-id="74910-130">Code in depth</span></span>

<span data-ttu-id="74910-131">Le operazioni eseguite dal codice della guida introduttiva vengono suddivise in un blocco di variabili e di alcune piccole funzioni, ognuna delle quali viene illustrata in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="74910-131">What the quickstart code does is broken down into a block of variables and several small functions, each of which are discussed here.</span></span>

### <a name="variables-constants-and-types"></a><span data-ttu-id="74910-132">Variabili, costanti e tipi</span><span class="sxs-lookup"><span data-stu-id="74910-132">Variables, constants, and types</span></span>

<span data-ttu-id="74910-133">Essendo indipendente, la guida introduttiva usa variabili e costanti globali.</span><span class="sxs-lookup"><span data-stu-id="74910-133">Since quickstart is self-contained, it uses global constants and variables.</span></span>

```go
const (
    resourceGroupName     = "GoVMQuickstart"
    resourceGroupLocation = "eastus"

    deploymentName = "VMDeployQuickstart"
    templateFile   = "vm-quickstart-template.json"
    parametersFile = "vm-quickstart-params.json"
)

// Information loaded from the authorization file to identify the client
type clientInfo struct {
    SubscriptionID string
    VMPassword     string
}

var (
    ctx        = context.Background()
    clientData clientInfo
    authorizer autorest.Authorizer
)
```

<span data-ttu-id="74910-134">Vengono dichiarati i valori che specificano i nomi delle risorse create.</span><span class="sxs-lookup"><span data-stu-id="74910-134">Values are declared which give the names of created resources.</span></span> <span data-ttu-id="74910-135">Viene specificata anche la posizione, che può essere modificata per verificare il comportamento delle distribuzioni in altri data center.</span><span class="sxs-lookup"><span data-stu-id="74910-135">The location is also specified here, which you can change to see how deployments behave in other datacenters.</span></span> <span data-ttu-id="74910-136">Non tutte le risorse necessarie sono disponibili in tutti i data center.</span><span class="sxs-lookup"><span data-stu-id="74910-136">Not every datacenter has all of the required resources available.</span></span>

<span data-ttu-id="74910-137">Il tipo `clientInfo` viene dichiarato per incapsulare tutte le informazioni che devono essere caricate in modo indipendente dal file di autenticazione per configurare i client nell'SDK e impostare la password della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="74910-137">The `clientInfo` type is declared to encapsulate all of the information that must be independently loaded from the authentication file to set up clients in the SDK and set the VM password.</span></span>

<span data-ttu-id="74910-138">Le costanti `templateFile` e `parametersFile` fanno riferimento ai file necessari per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="74910-138">The `templateFile` and `parametersFile` constants point to the files needed for deployment.</span></span> <span data-ttu-id="74910-139">La variabile `authorizer` verrà configurata dall'SDK per Go per l'autenticazione, mentre la variabile `ctx` è un [contesto Go](https://blog.golang.org/context) per le operazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="74910-139">The `authorizer` will be configured by the Go SDK for authentication, and the `ctx` variable is a [Go context](https://blog.golang.org/context) for the network operations.</span></span>

### <a name="authentication-and-initialization"></a><span data-ttu-id="74910-140">Autenticazione e inizializzazione</span><span class="sxs-lookup"><span data-stu-id="74910-140">Authentication and initialization</span></span>

<span data-ttu-id="74910-141">La funzione `init` configura l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="74910-141">The `init` function sets up authentication.</span></span> <span data-ttu-id="74910-142">Poiché l'autenticazione è una precondizione per qualsiasi operazione nella guida introduttiva, è consigliabile includerla nell'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="74910-142">Since authentication is a precondition for everything in the quickstart, it makes sense to have it as part of initialization.</span></span> <span data-ttu-id="74910-143">Essa permette anche di caricare alcune informazioni necessarie dal file di autenticazione per configurare i client e la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="74910-143">It also loads some information needed from the authentication file to configure clients and the VM.</span></span>

```go
func init() {
    var err error
    authorizer, err = auth.NewAuthorizerFromFile(azure.PublicCloud.ResourceManagerEndpoint)
    if err != nil {
        log.Fatalf("Failed to get OAuth config: %v", err)
    }

    authInfo, err := readJSON(os.Getenv("AZURE_AUTH_LOCATION"))
    clientData.SubscriptionID = (*authInfo)["subscriptionId"].(string)
    clientData.VMPassword = (*authInfo)["clientSecret"].(string)
}
```

<span data-ttu-id="74910-144">Prima di tutto viene chiamato il comando [auth.NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile) per caricare le informazioni di autenticazione dal file che si trova in `AZURE_AUTH_LOCATION`.</span><span class="sxs-lookup"><span data-stu-id="74910-144">First, [auth.NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile) is called to load the authentication information from the file located at `AZURE_AUTH_LOCATION`.</span></span> <span data-ttu-id="74910-145">Successivamente, questo file viene caricato manualmente dalla funzione `readJSON` (qui omessa) per eseguire il pull dei due valori necessari per eseguire il resto del programma: l'ID sottoscrizione del client e il segreto dell'entità servizio, che viene usato anche per la password della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="74910-145">Next, this file is loaded manually by the `readJSON` function (omitted here) to pull the two values needed to run the rest of the program: The subscription ID of the client, and the service principal's secret, which is also used for the VM's password.</span></span>

> [!WARNING]
> <span data-ttu-id="74910-146">Per semplicità, nella guida introduttiva viene riutilizzata la password dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="74910-146">To keep the quickstart simple, the service principal password is reused.</span></span> <span data-ttu-id="74910-147">Nell'ambiente di produzione, prestare attenzione a non riutilizzare __mai__ una password che consente di accedere alle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="74910-147">In production, take care to __never__ reuse a password which gives access to your Azure resources.</span></span>

### <a name="flow-of-operations-in-main"></a><span data-ttu-id="74910-148">Flusso di operazioni in main()</span><span class="sxs-lookup"><span data-stu-id="74910-148">Flow of operations in main()</span></span>

<span data-ttu-id="74910-149">La funzione `main` è semplice e indica solo il flusso di operazioni e l'esecuzione del controllo degli errori.</span><span class="sxs-lookup"><span data-stu-id="74910-149">The `main` function is simple, only indicating the flow of operations and performing error-checking.</span></span>

```go
func main() {
    group, err := createGroup()
    if err != nil {
        log.Fatalf("failed to create group: %v", err)
    }
    log.Printf("Created group: %v", *group.Name)

    log.Printf("Starting deployment: %s", deploymentName)
    result, err := createDeployment()
    if err != nil {
        log.Fatalf("Failed to deploy: %v", err)
    }
    if result.Name != nil {
        log.Printf("Completed deployment %v: %v", deploymentName, *result.Properties.ProvisioningState)
    } else {
        log.Printf("Completed deployment %v (no data returned to SDK)", deploymentName)
    }
    getLogin()
}
```

<span data-ttu-id="74910-150">Il codice esegue questi passaggi nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="74910-150">The steps that the code runs through are, in order:</span></span>

* <span data-ttu-id="74910-151">Creare il gruppo di risorse in cui eseguire la distribuzione (`createGroup`)</span><span class="sxs-lookup"><span data-stu-id="74910-151">Create the resource group to deploy to (`createGroup`)</span></span>
* <span data-ttu-id="74910-152">Creare la distribuzione all'interno del gruppo (`createDeployment`)</span><span class="sxs-lookup"><span data-stu-id="74910-152">Create the deployment within this group (`createDeployment`)</span></span>
* <span data-ttu-id="74910-153">Ottenere e visualizzare le informazioni di accesso per la VM distribuita (`getLogin`)</span><span class="sxs-lookup"><span data-stu-id="74910-153">Obtain and display login information for the deployed VM (`getLogin`)</span></span>

### <a name="creating-the-resource-group"></a><span data-ttu-id="74910-154">Creazione del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="74910-154">Creating the resource group</span></span>

<span data-ttu-id="74910-155">La funzione `createGroup` crea il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="74910-155">The `createGroup` function creates the resource group.</span></span> <span data-ttu-id="74910-156">È possibile esaminare il flusso di chiamate e di argomenti per verificare la struttura delle interazioni tra i servizi nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="74910-156">Looking at the call flow and arguments demonstrates the way that service interactions are structured in the SDK.</span></span>

```go
func createGroup() (group resources.Group, err error) {
    groupsClient := resources.NewGroupsClient(clientData.SubscriptionID)
    groupsClient.Authorizer = authorizer

        return groupsClient.CreateOrUpdate(
                ctx,
                resourceGroupName,
                resources.Group{
                        Location: to.StringPtr(resourceGroupLocation)})
}
```

<span data-ttu-id="74910-157">Questo è il flusso generale dell'interazione con un servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="74910-157">The general flow of interacting with an Azure service is:</span></span>

* <span data-ttu-id="74910-158">Creare il client con il metodo `service.New*Client()`, dove `*` è il tipo di risorsa di `service` con cui si vuole interagire.</span><span class="sxs-lookup"><span data-stu-id="74910-158">Create the client using the `service.New*Client()` method, where `*` is the resource type of the `service` that you want to interact with.</span></span> <span data-ttu-id="74910-159">Questa funzione accetta sempre un ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="74910-159">This function always takes a subscription ID.</span></span>
* <span data-ttu-id="74910-160">Impostare il metodo di autorizzazione per il client, consentendo l'interazione con l'API remota.</span><span class="sxs-lookup"><span data-stu-id="74910-160">Set the authorization method for the client, allowing it to interact with the remote API.</span></span>
* <span data-ttu-id="74910-161">Effettuare la chiamata al metodo sul client corrispondente all'API remota.</span><span class="sxs-lookup"><span data-stu-id="74910-161">Make the method call on the client corresponding to the remote API.</span></span> <span data-ttu-id="74910-162">I metodi del client del servizio accettano in genere il nome della risorsa e un oggetto di metadati.</span><span class="sxs-lookup"><span data-stu-id="74910-162">Service client methods usually take the name of the resource and a metadata object.</span></span>

<span data-ttu-id="74910-163">La funzione [`to.StringPtr`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) viene usata qui per eseguire un tipo di conversione.</span><span class="sxs-lookup"><span data-stu-id="74910-163">The [`to.StringPtr`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) function is used to perform a type conversion here.</span></span> <span data-ttu-id="74910-164">I parametri per i metodi dell'SDK accettano quasi esclusivamente puntatori, quindi vengono forniti metodi utili per semplificare le conversioni dei tipi.</span><span class="sxs-lookup"><span data-stu-id="74910-164">The parameters for SDK methods almost exclusively take pointers, so convenience methods are provided to make the type conversions easy.</span></span> <span data-ttu-id="74910-165">Per un elenco completo e informazioni sul comportamento dei convertitori utili, vedere la documentazione per il modulo [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to).</span><span class="sxs-lookup"><span data-stu-id="74910-165">See the documentation for the [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) module for the complete list of convenience converters and their behavior.</span></span>

<span data-ttu-id="74910-166">Il metodo `groupsClient.CreateOrUpdate` ha restituito un puntatore a un tipo di dati che rappresenta il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="74910-166">The `groupsClient.CreateOrUpdate` method returns a pointer to a data type representing the resource group.</span></span> <span data-ttu-id="74910-167">Un valore restituito diretto di questo tipo indica un'operazione a esecuzione ridotta che deve essere asincrona.</span><span class="sxs-lookup"><span data-stu-id="74910-167">A direct return value of this kind indicates a short-running operation that is meant to be synchronous.</span></span> <span data-ttu-id="74910-168">Nella sezione successiva è disponibile un esempio di operazione a esecuzione prolungata e viene illustrato come interagire con essa.</span><span class="sxs-lookup"><span data-stu-id="74910-168">In the next section, you'll see an example of a long-running operation and how to interact with it.</span></span>

### <a name="performing-the-deployment"></a><span data-ttu-id="74910-169">Esecuzione della distribuzione</span><span class="sxs-lookup"><span data-stu-id="74910-169">Performing the deployment</span></span>

<span data-ttu-id="74910-170">Dopo la creazione del gruppo di risorse, è possibile eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="74910-170">Once the resource group is created, it's time to run the deployment.</span></span> <span data-ttu-id="74910-171">Il codice viene suddiviso in sezioni di dimensioni minori per evidenziare le diverse parti della logica.</span><span class="sxs-lookup"><span data-stu-id="74910-171">This code is broken up into smaller sections to emphasize different parts of its logic.</span></span>

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
    (*params)["vm_password"] = map[string]string{
        "value": clientData.VMPassword,
    }
        // ...
```

<span data-ttu-id="74910-172">I file della distribuzione vengono caricati da `readJSON`, per cui non vengono forniti dettagli.</span><span class="sxs-lookup"><span data-stu-id="74910-172">The deployment files are loaded by `readJSON`, the details of which are skipped here.</span></span> <span data-ttu-id="74910-173">Questa funzione restituisce `*map[string]interface{}`, il tipo usato nella creazione dei metadati per la chiamata alla distribuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="74910-173">This function returns a `*map[string]interface{}`, the type used in constructing the metadata for the resource deployment call.</span></span> <span data-ttu-id="74910-174">La password della macchina virtuale viene impostata manualmente anche sui parametri della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="74910-174">The VM's password is also set manually on the deployment parameters.</span></span>

```go
        // ...

    deploymentsClient := resources.NewDeploymentsClient(clientData.SubscriptionID)
    deploymentsClient.Authorizer = authorizer

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
        return
    }
```

<span data-ttu-id="74910-175">Il codice segue lo stesso criterio della creazione del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="74910-175">This code follows the same pattern as creating the resource group.</span></span> <span data-ttu-id="74910-176">Viene creato un nuovo client, a cui viene consentita l'autenticazione in Azure, e quindi viene chiamato un metodo.</span><span class="sxs-lookup"><span data-stu-id="74910-176">A new client is created, given the ability to authenticate with Azure, and then a method is called.</span></span> <span data-ttu-id="74910-177">Il metodo ha addirittura lo stesso nome (`CreateOrUpdate`) del metodo corrispondente per i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="74910-177">The method even has the same name (`CreateOrUpdate`) as the corresponding method for resource groups.</span></span> <span data-ttu-id="74910-178">Questo criterio viene visualizzato in tutto l'SDK.</span><span class="sxs-lookup"><span data-stu-id="74910-178">This pattern is seen throughout the SDK.</span></span> <span data-ttu-id="74910-179">I metodi che eseguono operazioni simili hanno in genere lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="74910-179">Methods that perform similar work normally have the same name.</span></span>

<span data-ttu-id="74910-180">La differenza principale è costituita dal valore restituito del metodo `deploymentsClient.CreateOrUpdate`.</span><span class="sxs-lookup"><span data-stu-id="74910-180">The biggest difference comes in the return value of the `deploymentsClient.CreateOrUpdate` method.</span></span> <span data-ttu-id="74910-181">Questo valore, di tipo [Future](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#Future), segue lo [schema progettuale degli oggetti Future](https://en.wikipedia.org/wiki/Futures_and_promises).</span><span class="sxs-lookup"><span data-stu-id="74910-181">This value is of the [Future](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#Future) type, which follows the [future design pattern](https://en.wikipedia.org/wiki/Futures_and_promises).</span></span> <span data-ttu-id="74910-182">Gli oggetti Future rappresentano un'operazione con esecuzione prolungata in Azure per cui è possibile eseguire il polling, annullare o bloccare il loro completamento.</span><span class="sxs-lookup"><span data-stu-id="74910-182">Futures represent a long-running operation in Azure that you can poll, cancel, or block on their completion.</span></span>

```go
        //...
    err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
    if err != nil {
        return
    }
    deployment, err = deploymentFuture.Result(deploymentsClient)

    // Work around possible bugs or late-stage failures
    if deployment.Name == nil || err != nil {
        deployment, _ = deploymentsClient.Get(ctx, resourceGroupName, deploymentName)
    }
    return
```

<span data-ttu-id="74910-183">Per questo esempio è consigliabile attendere il completamento dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="74910-183">For this example, the best thing to do is to wait for the operation to complete.</span></span> <span data-ttu-id="74910-184">Per rimanere in attesa di un oggetto Future sono necessari sia un [contesto di ambiente](https://blog.golang.org/context), sia il client che ha creato `Future`.</span><span class="sxs-lookup"><span data-stu-id="74910-184">Waiting on a future requires both a [context object](https://blog.golang.org/context) and the client that created the `Future`.</span></span> <span data-ttu-id="74910-185">È possibile che si verifichino due tipi di errore, ovvero un errore provocato sul lato client durante il tentativo di chiamata del metodo e una risposta di errore dal server.</span><span class="sxs-lookup"><span data-stu-id="74910-185">There are two possible error sources here: An error caused on the client side when trying to invoke the method, and an error response from the server.</span></span> <span data-ttu-id="74910-186">Quest'ultimo tipo di errore viene restituito come parte della chiamata `deploymentFuture.Result`.</span><span class="sxs-lookup"><span data-stu-id="74910-186">The latter is returned as part of the `deploymentFuture.Result` call.</span></span>

<span data-ttu-id="74910-187">Una volta recuperate le informazioni sulla distribuzione è disponibile una soluzione per possibili bug in cui le informazioni di distribuzione possono essere vuote con una chiamata manuale a `deploymentsClient.Get` per garantire che i dati vengano popolati.</span><span class="sxs-lookup"><span data-stu-id="74910-187">Once the deployment information is retrieved, there is a workaround for possible bugs where the deployment information may be empty with a manual call to `deploymentsClient.Get` to ensure that the data is populated.</span></span>

### <a name="obtaining-the-assigned-ip-address"></a><span data-ttu-id="74910-188">Ottenere l'indirizzo IP assegnato</span><span class="sxs-lookup"><span data-stu-id="74910-188">Obtaining the assigned IP address</span></span>

<span data-ttu-id="74910-189">Per eseguire qualsiasi operazione con la macchina virtuale appena creata, è necessario l'indirizzo IP assegnato.</span><span class="sxs-lookup"><span data-stu-id="74910-189">To do anything with the newly created VM, you need the assigned IP address.</span></span> <span data-ttu-id="74910-190">Gli indirizzi IP sono risorse di Azure distinte, associate a risorse della scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="74910-190">IP addresses are their own separate Azure resource, bound to Network Interface Controller (NIC) resources.</span></span>

```go
func getLogin() {
    params, err := readJSON(parametersFile)
    if err != nil {
        log.Fatalf("Unable to read parameters. Get login information with `az network public-ip list -g %s", resourceGroupName)
    }

    addressClient := network.NewPublicIPAddressesClient(clientData.SubscriptionID)
    addressClient.Authorizer = authorizer
    ipName := (*params)["publicIPAddresses_QuickstartVM_ip_name"].(map[string]interface{})
    ipAddress, err := addressClient.Get(ctx, resourceGroupName, ipName["value"].(string), "")
    if err != nil {
        log.Fatalf("Unable to get IP information. Try using `az network public-ip list -g %s", resourceGroupName)
    }

    vmUser := (*params)["vm_user"].(map[string]interface{})

    log.Printf("Log in with ssh: %s@%s, password: %s",
        vmUser["value"].(string),
        *ipAddress.PublicIPAddressPropertiesFormat.IPAddress,
        clientData.VMPassword)
}
```

<span data-ttu-id="74910-191">Questo metodo si basa su informazioni archiviate nel file dei parametri.</span><span class="sxs-lookup"><span data-stu-id="74910-191">This method relies on information that is stored in the parameters file.</span></span> <span data-ttu-id="74910-192">Il codice può eseguire query direttamente sulla macchina virtuale per ottenere la rispettiva scheda di interfaccia di rete, può eseguire query sulla scheda di interfaccia di rete per ottenere la rispettiva risorsa IP e quindi può eseguire query direttamente sulla risorsa IP.</span><span class="sxs-lookup"><span data-stu-id="74910-192">The code could query the VM directly to get its NIC, query the NIC to get its IP resource, and then query the IP resource directly.</span></span> <span data-ttu-id="74910-193">È prevista una lunga catena di dipendenze e operazioni da risolvere, che risulta costosa.</span><span class="sxs-lookup"><span data-stu-id="74910-193">That's a long chain of dependencies and operations to resolve, making it expensive.</span></span> <span data-ttu-id="74910-194">Poiché le informazioni JSON sono locali, è anche possibile caricarle.</span><span class="sxs-lookup"><span data-stu-id="74910-194">Since the JSON information is local, it can be loaded instead.</span></span>

<span data-ttu-id="74910-195">Anche il valore per l'utente della macchina virtuale viene caricato dalle informazioni JSON.</span><span class="sxs-lookup"><span data-stu-id="74910-195">The value for the VM user is also loaded from the JSON.</span></span> <span data-ttu-id="74910-196">La password della macchina virtuale è stata caricata in precedenza dal file di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="74910-196">The VM password was loaded earlier from the authentication file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74910-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74910-197">Next steps</span></span>

<span data-ttu-id="74910-198">In questa guida introduttiva è stato selezionato un modello esistente e il modello è stato distribuito tramite Go.</span><span class="sxs-lookup"><span data-stu-id="74910-198">In this quickstart, you took an existing template and deployed it through Go.</span></span> <span data-ttu-id="74910-199">È stata quindi stabilita la connessione alla macchina virtuale appena creata tramite SSH per verificarne l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="74910-199">Then you connected to the newly created VM via SSH to ensure that it's running.</span></span>

<span data-ttu-id="74910-200">Per continuare a ottenere informazioni sull'uso delle macchine virtuali nell'ambiente di Azure con Go, vedere gli [esempi di calcolo di Azure per Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) o gli [esempi di gestione delle risorse di Azure per Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span><span class="sxs-lookup"><span data-stu-id="74910-200">To continue learning about working with virtual machines in the Azure environment with Go, take a look at the [Azure compute samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) or [Azure resource management samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span></span>

<span data-ttu-id="74910-201">Per altre informazioni sui metodi di autenticazione disponibili nell'SDK e sui tipi di autenticazione che supportano, vedere [Autenticazione con Azure SDK per Go](azure-sdk-go-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="74910-201">To learn more about the available authentication methods in the SDK, and which authentication types they support, see [Authentication with the Azure SDK for Go](azure-sdk-go-authorization.md).</span></span>
