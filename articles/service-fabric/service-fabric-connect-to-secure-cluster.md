---
title: "aaaConnect безопасно кластера Azure Service Fabric tooan | Документы Microsoft"
description: "Описываются процедуры tooauthenticate клиента доступ к кластеру Service Fabric tooa и toosecure связи между клиентами и кластера."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="a132f-103">Подключите кластер безопасного tooa</span><span class="sxs-lookup"><span data-stu-id="a132f-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="a132f-104">Когда клиент подключается tooa узла кластера Service Fabric, hello клиент может быть проверку подлинности и безопасность обмена данными с помощью сертификата безопасности или Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="a132f-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="a132f-105">Эта проверка подлинности обеспечивает только авторизованные пользователи могут получать доступ к кластеру hello и развертывать приложения и выполнять задачи управления.</span><span class="sxs-lookup"><span data-stu-id="a132f-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="a132f-106">Сертификат или AAD безопасности должна быть ранее включена в кластере hello при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="a132f-107">Дополнительные сведения о сценариях обеспечения безопасности кластеров см. в разделе [Безопасность кластера](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="a132f-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="a132f-108">При подключении tooa кластеров, защищенных с помощью сертификатов, [настроить сертификат клиента hello](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) на компьютере hello, который подключается toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="a132f-109">Подключите tooa безопасного кластер с помощью Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="a132f-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="a132f-110">Существует несколько способов tooconnect tooa безопасного кластера с помощью hello службы структуры CLI (sfctl).</span><span class="sxs-lookup"><span data-stu-id="a132f-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="a132f-111">При использовании сертификата клиента для проверки подлинности, сертификат hello сведения должны соответствовать сертификат развернут toohello узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="a132f-112">Если сертификат имеет центров сертификации (ЦС), необходимо tooadditionally указать hello доверенного ЦС.</span><span class="sxs-lookup"><span data-stu-id="a132f-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="a132f-113">Можно подключить tooa кластер, использующий hello `sfctl cluster select` команды.</span><span class="sxs-lookup"><span data-stu-id="a132f-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="a132f-114">Сертификаты клиента можно указать как сертификат и пару ключей или как отдельный PEM-файл.</span><span class="sxs-lookup"><span data-stu-id="a132f-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="a132f-115">Для защищенных паролем `pem` файлы, будет автоматически предложено tooenter hello пароль.</span><span class="sxs-lookup"><span data-stu-id="a132f-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="a132f-116">сертификат клиента hello toospecify как pem-файла, укажите путь к файлу hello в hello `--pem` аргумент.</span><span class="sxs-lookup"><span data-stu-id="a132f-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="a132f-117">Например:</span><span class="sxs-lookup"><span data-stu-id="a132f-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="a132f-118">Файлы, защищенные паролем pem запросит toorunning предыдущий пароль любую команду.</span><span class="sxs-lookup"><span data-stu-id="a132f-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="a132f-119">toospecify cert пары ключей используйте hello `--cert` и `--key` toospecify hello соответствующего файла пути tooeach аргументы.</span><span class="sxs-lookup"><span data-stu-id="a132f-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="a132f-120">Иногда использовать сертификаты toosecure тестирования или разработки кластеров не проходят проверку сертификата.</span><span class="sxs-lookup"><span data-stu-id="a132f-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="a132f-121">toobypass сертификата проверки, укажите hello `--no-verify` параметр.</span><span class="sxs-lookup"><span data-stu-id="a132f-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="a132f-122">Например:</span><span class="sxs-lookup"><span data-stu-id="a132f-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="a132f-123">Не используйте hello `no-verify` параметр при соединении tooproduction кластеров Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a132f-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="a132f-124">Кроме того можно указать пути toodirectories доверенных сертификатов ЦС или отдельные сертификаты.</span><span class="sxs-lookup"><span data-stu-id="a132f-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="a132f-125">toospecify использовать эти пути hello `--ca` аргумент.</span><span class="sxs-lookup"><span data-stu-id="a132f-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="a132f-126">Например:</span><span class="sxs-lookup"><span data-stu-id="a132f-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="a132f-127">После подключения можно будет слишком[выполнять другие команды sfctl](service-fabric-cli.md) toointeract с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="a132f-128">Подключите кластер tooa с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a132f-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="a132f-129">Прежде чем выполнять операции с кластера с помощью PowerShell, сначала следует установите toohello подключения кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="a132f-130">Hello подключения кластера используется для всех последующих команд в hello заданного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a132f-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="a132f-131">Подключите кластер небезопасные tooan</span><span class="sxs-lookup"><span data-stu-id="a132f-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="a132f-132">небезопасные tooan tooconnect кластера, укажите toohello адрес конечной точки кластера hello **Connect-ServiceFabricCluster** команды:</span><span class="sxs-lookup"><span data-stu-id="a132f-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="a132f-133">Подключите tooa безопасного кластер с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a132f-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="a132f-134">безопасный кластере tooa tooconnect, который использует доступа администратора кластера tooauthorize Azure Active Directory, укажите отпечаток сертификата hello кластера и использовать hello *azureactivedirectory возникла ошибка* флаг.</span><span class="sxs-lookup"><span data-stu-id="a132f-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a132f-135">Подключите tooa безопасного кластер с помощью сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="a132f-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="a132f-136">Выполнения hello следующую команду PowerShell безопасного tooa tooconnect кластер, который использует доступ администратора tooauthorize сертификаты клиентов.</span><span class="sxs-lookup"><span data-stu-id="a132f-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="a132f-137">Укажите отпечаток сертификата кластера hello и hello отпечаток сертификата клиента hello, которому предоставлены разрешения для управления кластером.</span><span class="sxs-lookup"><span data-stu-id="a132f-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="a132f-138">сведения о сертификате Hello должно соответствовать сертификат на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="a132f-139">*ServerCertThumbprint* — отпечаток сертификата сервера hello, установленных на узлах кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="a132f-140">*FindValue* — hello отпечаток сертификата клиента администратора hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="a132f-141">При заполнении параметры hello hello команда выглядит следующим образом hello в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="a132f-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="a132f-142">Подключите tooa безопасного кластер с помощью Active Directory для Windows</span><span class="sxs-lookup"><span data-stu-id="a132f-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="a132f-143">При развертывании автономного кластера с помощью средств безопасности AD подключитесь toohello кластер, добавив коммутатор hello «WindowsCredential».</span><span class="sxs-lookup"><span data-stu-id="a132f-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="a132f-144">Подключите кластер tooa, с помощью API-интерфейсов FabricClient hello</span><span class="sxs-lookup"><span data-stu-id="a132f-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="a132f-145">Hello Service Fabric SDK предоставляет hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) класса для управления кластером.</span><span class="sxs-lookup"><span data-stu-id="a132f-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="a132f-146">hello toouse FabricClient API, получить пакет Microsoft.ServiceFabric NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="a132f-147">Подключите кластер небезопасные tooan</span><span class="sxs-lookup"><span data-stu-id="a132f-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="a132f-148">tooconnect tooa удаленного небезопасную кластера, создайте экземпляр FabricClient и укажите адрес кластера hello:</span><span class="sxs-lookup"><span data-stu-id="a132f-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="a132f-149">Код, выполняемый в кластере, например, в надежной службы, создайте FabricClient *без* указание hello адрес кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="a132f-150">Локальное управление toohello подключается FabricClient шлюз на код hello hello узла сейчас выполняется, как избежать дополнительный сетевой прыжок.</span><span class="sxs-lookup"><span data-stu-id="a132f-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a132f-151">Подключите tooa безопасного кластер с помощью сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="a132f-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="a132f-152">Hello узлов в кластере hello, должны иметь допустимые сертификаты, общее имя или DNS-имя в сети хранения данных отображается в hello [свойство RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) на [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="a132f-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="a132f-153">Эта процедура позволяет взаимной проверки подлинности клиента hello и hello узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="a132f-154">Подключите tooa безопасного кластер интерактивно с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a132f-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="a132f-155">Следующий пример использует Azure Active Directory для сертификата клиента удостоверение и сервера для идентификации сервера Hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="a132f-156">Диалоговое окно автоматически появится окно для интерактивного входа в систему при подключении toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="a132f-157">Подключите tooa безопасного кластер не в интерактивном режиме с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a132f-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="a132f-158">Hello следующий пример использует Microsoft.IdentityModel.Clients.ActiveDirectory, версия: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="a132f-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="a132f-159">Дополнительные сведения о получении маркеров AAD см. в описании [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="a132f-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="a132f-160">Подключите кластер безопасного tooa без ведома предыдущих метаданных с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a132f-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="a132f-161">Hello следующий пример использует неинтерактивной приобретения токена, но hello же подход может быть используется toobuild качества пользовательских интерактивный приобретения токена.</span><span class="sxs-lookup"><span data-stu-id="a132f-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="a132f-162">Hello Azure Active Directory метаданных, необходимых для получения маркера считывается из конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="a132f-163">Подключите tooa безопасного кластер с помощью Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="a132f-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="a132f-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) для данного кластера, укажите в браузере для:</span><span class="sxs-lookup"><span data-stu-id="a132f-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a132f-165">полный URL-адрес Hello доступен также в панели essentials кластера hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a132f-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="a132f-166">Подключите tooa безопасного кластер с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a132f-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="a132f-167">tooconnect tooa кластера, защищенного с помощью AAD, точка веб-браузера:</span><span class="sxs-lookup"><span data-stu-id="a132f-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a132f-168">Будут автоматически осуществлять запрос toolog вход с помощью AAD.</span><span class="sxs-lookup"><span data-stu-id="a132f-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a132f-169">Подключите tooa безопасного кластер с помощью сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="a132f-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="a132f-170">tooconnect tooa кластера, защищенного с помощью сертификатов, точка веб-браузера:</span><span class="sxs-lookup"><span data-stu-id="a132f-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a132f-171">Будут автоматически осуществлять запрос tooselect сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="a132f-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="a132f-172">Настроить сертификат клиента на удаленном компьютере hello</span><span class="sxs-lookup"><span data-stu-id="a132f-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="a132f-173">По крайней мере два сертификата можно использовать для обеспечения безопасности кластера hello, один для hello кластером и сервером сертификатов и другой для клиентского доступа.</span><span class="sxs-lookup"><span data-stu-id="a132f-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="a132f-174">Рекомендуется также использовать дополнительные сертификаты и сертификаты клиентского доступа.</span><span class="sxs-lookup"><span data-stu-id="a132f-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="a132f-175">toosecure hello взаимодействия между клиентом и узла кластера с помощью сертификатов безопасности, требуется tooobtain и установите сертификат клиента hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="a132f-176">Hello сертификат можно установить в hello личных () хранилище My hello локального компьютера или текущего пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="a132f-177">Необходимо также hello отпечаток сертификата сервера hello hello клиента для проверки подлинности hello кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="a132f-178">Запустите следующие tooset командлет PowerShell hello сертификата клиента на компьютере hello, на котором будет доступен кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="a132f-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="a132f-179">Если самозаверяющий сертификат, необходимо tooimport он машины tooyour «доверенные лица» хранить перед использованием этого tooconnect сертификат tooa безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="a132f-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="a132f-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a132f-180">Next steps</span></span>

* [<span data-ttu-id="a132f-181">Обновление кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a132f-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="a132f-182">Управление приложениями Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a132f-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="a132f-183">Общие сведения о модели работоспособности в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a132f-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="a132f-184">Безопасность приложений и запуск от имени</span><span class="sxs-lookup"><span data-stu-id="a132f-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="a132f-185">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a132f-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
