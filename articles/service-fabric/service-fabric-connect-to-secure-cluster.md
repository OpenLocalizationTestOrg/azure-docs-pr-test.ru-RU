---
title: "Безопасное подключение к кластеру Azure Service Fabric | Документация Майкрософт"
description: "Сведения о способах проверки подлинности клиентского доступа к кластеру Service Fabric, а также об обеспечении безопасного обмена данными между клиентами и кластером."
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
ms.openlocfilehash: d6a13ceb8ccd9207ecacc166247535d496d5dec7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="918f2-103">Безопасное подключение к кластеру</span><span class="sxs-lookup"><span data-stu-id="918f2-103">Connect to a secure cluster</span></span>

<span data-ttu-id="918f2-104">Когда клиент подключается к узлу кластера Service Fabric, он может пройти проверку подлинности и установить безопасную связь на основе сертификатов или с помощью Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="918f2-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="918f2-105">Такая проверка подлинности гарантирует, что только авторизованные пользователи могут получить доступ к кластеру и развернутым приложениям для выполнения задач управления.</span><span class="sxs-lookup"><span data-stu-id="918f2-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="918f2-106">Конфигурацию обеспечения безопасности на основе сертификатов или AAD необходимо предварительно включить в кластере при его создании.</span><span class="sxs-lookup"><span data-stu-id="918f2-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="918f2-107">Дополнительные сведения о сценариях обеспечения безопасности кластеров см. в разделе [Безопасность кластера](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="918f2-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="918f2-108">Если безопасность в кластере обеспечивается сертификатами, то на компьютере, который подключается к нему, необходимо [настроить сертификат клиента](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert).</span><span class="sxs-lookup"><span data-stu-id="918f2-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="918f2-109">Подключение к защищенному кластеру с помощью интерфейса командной строки Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="918f2-109">Connect to a secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="918f2-110">К защищенному кластеру можно подключиться с помощью интерфейса командной строки Service Fabric CLI (sfctl) несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="918f2-110">There are a few different ways to connect to a secure cluster using the Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="918f2-111">При использовании сертификата клиента для проверки подлинности сведения о сертификате должны соответствовать сертификату, развернутому в узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="918f2-111">When using a client certificate for authentication, the certificate details must match a certificate deployed to the cluster nodes.</span></span> <span data-ttu-id="918f2-112">Если сертификат выдан центром сертификации (ЦС), необходимо дополнительно указать доверенные ЦС.</span><span class="sxs-lookup"><span data-stu-id="918f2-112">If your certificate has Certificate Authorities (CAs), you need to additionally specify the trusted CAs.</span></span>

<span data-ttu-id="918f2-113">Можно подключиться к кластеру с помощью команды `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="918f2-113">You can connect to a cluster using the `sfctl cluster select` command.</span></span>

<span data-ttu-id="918f2-114">Сертификаты клиента можно указать как сертификат и пару ключей или как отдельный PEM-файл.</span><span class="sxs-lookup"><span data-stu-id="918f2-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="918f2-115">Вам автоматически будет предложено ввести пароль для защищенных файлов формата `pem`.</span><span class="sxs-lookup"><span data-stu-id="918f2-115">For password protected `pem` files, you will be prompted automatically to enter the password.</span></span>

<span data-ttu-id="918f2-116">Чтобы указать сертификат клиента как PEM-файл, укажите путь к файлу в аргументе `--pem`.</span><span class="sxs-lookup"><span data-stu-id="918f2-116">To specify the client certificate as a pem file, specify the file path in the `--pem` argument.</span></span> <span data-ttu-id="918f2-117">Например:</span><span class="sxs-lookup"><span data-stu-id="918f2-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="918f2-118">Прежде чем выполнять любые команды, для защищенных паролем PEM-файлов необходимо будет ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="918f2-118">Password protected pem files will prompt for password prior to running any command.</span></span>

<span data-ttu-id="918f2-119">Чтобы указать сертификат, пара ключей использует аргументы `--cert` и `--key`, чтобы указать пути для каждого соответствующего файла.</span><span class="sxs-lookup"><span data-stu-id="918f2-119">To specify a cert, key pair use the `--cert` and `--key` arguments to specify the file paths to each respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="918f2-120">Иногда сертификаты, используемые для защиты тестового кластера и кластера для разработки не проходят проверку сертификата.</span><span class="sxs-lookup"><span data-stu-id="918f2-120">Sometimes certificates used to secure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="918f2-121">Чтобы не выполнять проверку сертификата, укажите параметр `--no-verify`.</span><span class="sxs-lookup"><span data-stu-id="918f2-121">To bypass certificate verification, specify the `--no-verify` option.</span></span> <span data-ttu-id="918f2-122">Например:</span><span class="sxs-lookup"><span data-stu-id="918f2-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="918f2-123">При подключении к производственным кластерам Service Fabric не используйте параметр `no-verify`.</span><span class="sxs-lookup"><span data-stu-id="918f2-123">Do not use the `no-verify` option when connecting to production Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="918f2-124">Кроме того, вы можете указать пути к каталогам доверенных сертификатов ЦС или отдельных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="918f2-124">In addition, you can specify paths to directories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="918f2-125">Чтобы указать эти пути, используйте аргумент `--ca`.</span><span class="sxs-lookup"><span data-stu-id="918f2-125">To specify these paths, use the `--ca` argument.</span></span> <span data-ttu-id="918f2-126">Например:</span><span class="sxs-lookup"><span data-stu-id="918f2-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="918f2-127">После подключения вы сможете взаимодействовать с кластером с помощью [других команд sfctl](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="918f2-127">After you connect, you should be able to [run other sfctl commands](service-fabric-cli.md) to interact with the cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="918f2-128">Подключение к кластеру с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="918f2-128">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="918f2-129">Перед выполнением операций в кластере с помощью PowerShell к этому кластеру сначала нужно подключиться.</span><span class="sxs-lookup"><span data-stu-id="918f2-129">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="918f2-130">Это подключение используется для выполнения всех последующих команд в течение определенного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="918f2-130">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="918f2-131">Подключение к незащищенному кластеру</span><span class="sxs-lookup"><span data-stu-id="918f2-131">Connect to an unsecure cluster</span></span>

<span data-ttu-id="918f2-132">Чтобы подключиться к незащищенному кластеру, добавьте в следующую команду **Connect-ServiceFabricCluster** адрес конечной точки кластера.</span><span class="sxs-lookup"><span data-stu-id="918f2-132">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="918f2-133">Подключение к защищенному кластеру с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="918f2-133">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="918f2-134">Чтобы подключиться к защищенному кластеру, использующему Azure Active Directory для проверки подлинности административного доступа, предоставьте отпечаток сертификата кластера и используйте флаг *AzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="918f2-134">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="918f2-135">Подключение к защищенному кластеру с использованием сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="918f2-135">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="918f2-136">Чтобы подключиться к защищенному кластеру, использующему сертификаты клиента для проверки подлинности административного доступа, выполните следующую команду PowerShell.</span><span class="sxs-lookup"><span data-stu-id="918f2-136">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="918f2-137">Предоставьте отпечаток сертификата кластера, а также отпечаток сертификата клиента с разрешениями на управление кластером.</span><span class="sxs-lookup"><span data-stu-id="918f2-137">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="918f2-138">Сведения о сертификате должны соответствовать сертификату на узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="918f2-138">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="918f2-139">*ServerCertThumbprint* — отпечаток сертификата сервера, установленного на узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="918f2-139">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="918f2-140">*FindValue* — отпечаток сертификата клиента администрирования.</span><span class="sxs-lookup"><span data-stu-id="918f2-140">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="918f2-141">Когда все параметры указаны, команда выглядит так:</span><span class="sxs-lookup"><span data-stu-id="918f2-141">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="918f2-142">Подключение к защищенному кластеру с помощью Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="918f2-142">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="918f2-143">При развертывании автономного кластера с помощью группы безопасности Active Directory подключитесь к кластеру, добавив параметр "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="918f2-143">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="918f2-144">Подключение к кластеру с помощью интерфейсов API FabricClient</span><span class="sxs-lookup"><span data-stu-id="918f2-144">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="918f2-145">В пакете SDK для Service Fabric предусмотрен класс [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) для управления кластером.</span><span class="sxs-lookup"><span data-stu-id="918f2-145">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="918f2-146">Чтобы использовать интерфейсы API FabricClient, получите пакет NuGet Microsoft.ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="918f2-146">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="918f2-147">Подключение к незащищенному кластеру</span><span class="sxs-lookup"><span data-stu-id="918f2-147">Connect to an unsecure cluster</span></span>

<span data-ttu-id="918f2-148">Чтобы подключиться к удаленному незащищенному кластеру, создайте экземпляр FabricClient и укажите адрес кластера.</span><span class="sxs-lookup"><span data-stu-id="918f2-148">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="918f2-149">В коде, выполняемом в кластере (например, в надежной службе), создайте класс FabricClient, *не* указывая адрес кластера.</span><span class="sxs-lookup"><span data-stu-id="918f2-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="918f2-150">Класс FabricClient подключается к локальному шлюзу управления на узле, где в настоящее время выполняется код, без дополнительного перехода по сети.</span><span class="sxs-lookup"><span data-stu-id="918f2-150">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="918f2-151">Подключение к защищенному кластеру с использованием сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="918f2-151">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="918f2-152">У узлов в кластере должны быть действительные сертификаты, общее имя или DNS-имя которых в сети SAN отображается в [свойстве RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames), заданном для [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="918f2-152">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="918f2-153">Это обеспечивает взаимную проверку подлинности между клиентом и узлами кластера.</span><span class="sxs-lookup"><span data-stu-id="918f2-153">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

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

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="918f2-154">Интерактивное подключение к защищенному кластеру с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="918f2-154">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="918f2-155">В следующем примере в качестве удостоверения клиента используется Azure Active Directory, а сертификат сервера — в качестве удостоверения сервера.</span><span class="sxs-lookup"><span data-stu-id="918f2-155">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="918f2-156">При подключении к кластеру автоматически появляется всплывающее окно интерактивного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="918f2-156">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

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

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="918f2-157">Неинтерактивное подключение к защищенному кластеру с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="918f2-157">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="918f2-158">Приведенный ниже пример основан на пространстве имен Microsoft.IdentityModel.Clients.ActiveDirectory версии 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="918f2-158">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="918f2-159">Дополнительные сведения о получении маркеров AAD см. в описании [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="918f2-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="918f2-160">Подключение к защищенному кластеру без предварительного получения метаданных с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="918f2-160">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="918f2-161">В следующем примере используется неинтерактивное получение маркера, но используемый подход пригоден и для реализации интерактивного получения маркера.</span><span class="sxs-lookup"><span data-stu-id="918f2-161">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="918f2-162">Метаданные Azure Active Directory, необходимые для получения маркера, считываются из конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="918f2-162">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="918f2-163">Подключение к защищенному кластеру с помощью Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="918f2-163">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="918f2-164">Чтобы подключиться к [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) для заданного кластера, просто перейдите в браузере по адресу:</span><span class="sxs-lookup"><span data-stu-id="918f2-164">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="918f2-165">Полный URL-адрес доступен также на панели основных компонентов кластера портала Azure.</span><span class="sxs-lookup"><span data-stu-id="918f2-165">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="918f2-166">Подключение к защищенному кластеру с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="918f2-166">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="918f2-167">Чтобы подключиться к кластеру, защищенному с помощью AAD, перейдите в браузере по адресу:</span><span class="sxs-lookup"><span data-stu-id="918f2-167">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="918f2-168">После этого автоматически запрос на ввод учетных данных AAD.</span><span class="sxs-lookup"><span data-stu-id="918f2-168">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="918f2-169">Подключение к защищенному кластеру с использованием сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="918f2-169">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="918f2-170">Чтобы подключиться к кластеру, защищенному с использованием сертификатов, перейдите в браузере по адресу:</span><span class="sxs-lookup"><span data-stu-id="918f2-170">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="918f2-171">После этого автоматически появится запрос на выбор сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="918f2-171">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="918f2-172">Настройка сертификата клиента на удаленном компьютере</span><span class="sxs-lookup"><span data-stu-id="918f2-172">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="918f2-173">Для обеспечения безопасности кластера следует использовать по крайней мере два сертификата: один для кластера и сервера, а второй для клиентского доступа.</span><span class="sxs-lookup"><span data-stu-id="918f2-173">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="918f2-174">Рекомендуется также использовать дополнительные сертификаты и сертификаты клиентского доступа.</span><span class="sxs-lookup"><span data-stu-id="918f2-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="918f2-175">Чтобы защитить обмен данными между клиентом и узлом кластера с помощью сертификатов, сначала необходимо получить и установить сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="918f2-175">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="918f2-176">Его можно установить в личное хранилище на локальном компьютере или в личное хранилище текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="918f2-176">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="918f2-177">Отпечаток в сертификате сервера также нужен, чтобы клиент мог аутентифицировать кластер.</span><span class="sxs-lookup"><span data-stu-id="918f2-177">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="918f2-178">Выполните следующий командлет PowerShell, чтобы установить сертификат клиента на компьютер, который используется для доступа к кластеру.</span><span class="sxs-lookup"><span data-stu-id="918f2-178">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="918f2-179">Если это самозаверяющий сертификат, то перед использованием для подключения к безопасному кластеру его необходимо импортировать в хранилище "Доверенные лица" на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="918f2-179">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="918f2-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="918f2-180">Next steps</span></span>

* [<span data-ttu-id="918f2-181">Обновление кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="918f2-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="918f2-182">Управление приложениями Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="918f2-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="918f2-183">Общие сведения о модели работоспособности в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="918f2-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="918f2-184">Безопасность приложений и запуск от имени</span><span class="sxs-lookup"><span data-stu-id="918f2-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="918f2-185">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="918f2-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
