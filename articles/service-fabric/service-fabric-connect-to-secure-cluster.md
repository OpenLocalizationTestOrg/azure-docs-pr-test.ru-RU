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
# <a name="connect-tooa-secure-cluster"></a>Подключите кластер безопасного tooa

Когда клиент подключается tooa узла кластера Service Fabric, hello клиент может быть проверку подлинности и безопасность обмена данными с помощью сертификата безопасности или Azure Active Directory (AAD). Эта проверка подлинности обеспечивает только авторизованные пользователи могут получать доступ к кластеру hello и развертывать приложения и выполнять задачи управления.  Сертификат или AAD безопасности должна быть ранее включена в кластере hello при создании кластера hello.  Дополнительные сведения о сценариях обеспечения безопасности кластеров см. в разделе [Безопасность кластера](service-fabric-cluster-security.md). При подключении tooa кластеров, защищенных с помощью сертификатов, [настроить сертификат клиента hello](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) на компьютере hello, который подключается toohello кластера. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>Подключите tooa безопасного кластер с помощью Azure Service Fabric CLI (sfctl)

Существует несколько способов tooconnect tooa безопасного кластера с помощью hello службы структуры CLI (sfctl). При использовании сертификата клиента для проверки подлинности, сертификат hello сведения должны соответствовать сертификат развернут toohello узлов кластера. Если сертификат имеет центров сертификации (ЦС), необходимо tooadditionally указать hello доверенного ЦС.

Можно подключить tooa кластер, использующий hello `sfctl cluster select` команды.

Сертификаты клиента можно указать как сертификат и пару ключей или как отдельный PEM-файл. Для защищенных паролем `pem` файлы, будет автоматически предложено tooenter hello пароль.

сертификат клиента hello toospecify как pem-файла, укажите путь к файлу hello в hello `--pem` аргумент. Например:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Файлы, защищенные паролем pem запросит toorunning предыдущий пароль любую команду.

toospecify cert пары ключей используйте hello `--cert` и `--key` toospecify hello соответствующего файла пути tooeach аргументы.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

Иногда использовать сертификаты toosecure тестирования или разработки кластеров не проходят проверку сертификата. toobypass сертификата проверки, укажите hello `--no-verify` параметр. Например:

> [!WARNING]
> Не используйте hello `no-verify` параметр при соединении tooproduction кластеров Service Fabric.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

Кроме того можно указать пути toodirectories доверенных сертификатов ЦС или отдельные сертификаты. toospecify использовать эти пути hello `--ca` аргумент. Например:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

После подключения можно будет слишком[выполнять другие команды sfctl](service-fabric-cli.md) toointeract с кластером hello.

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>Подключите кластер tooa с помощью PowerShell
Прежде чем выполнять операции с кластера с помощью PowerShell, сначала следует установите toohello подключения кластера. Hello подключения кластера используется для всех последующих команд в hello заданного сеанса PowerShell.

### <a name="connect-tooan-unsecure-cluster"></a>Подключите кластер небезопасные tooan

небезопасные tooan tooconnect кластера, укажите toohello адрес конечной точки кластера hello **Connect-ServiceFabricCluster** команды:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Подключите tooa безопасного кластер с помощью Azure Active Directory

безопасный кластере tooa tooconnect, который использует доступа администратора кластера tooauthorize Azure Active Directory, укажите отпечаток сертификата hello кластера и использовать hello *azureactivedirectory возникла ошибка* флаг.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Подключите tooa безопасного кластер с помощью сертификата клиента
Выполнения hello следующую команду PowerShell безопасного tooa tooconnect кластер, который использует доступ администратора tooauthorize сертификаты клиентов. Укажите отпечаток сертификата кластера hello и hello отпечаток сертификата клиента hello, которому предоставлены разрешения для управления кластером. сведения о сертификате Hello должно соответствовать сертификат на узлах кластера hello.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* — отпечаток сертификата сервера hello, установленных на узлах кластера hello hello. *FindValue* — hello отпечаток сертификата клиента администратора hello.
При заполнении параметры hello hello команда выглядит следующим образом hello в следующем примере. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>Подключите tooa безопасного кластер с помощью Active Directory для Windows
При развертывании автономного кластера с помощью средств безопасности AD подключитесь toohello кластер, добавив коммутатор hello «WindowsCredential».

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>Подключите кластер tooa, с помощью API-интерфейсов FabricClient hello
Hello Service Fabric SDK предоставляет hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) класса для управления кластером. hello toouse FabricClient API, получить пакет Microsoft.ServiceFabric NuGet hello.

### <a name="connect-tooan-unsecure-cluster"></a>Подключите кластер небезопасные tooan

tooconnect tooa удаленного небезопасную кластера, создайте экземпляр FabricClient и укажите адрес кластера hello:

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

Код, выполняемый в кластере, например, в надежной службы, создайте FabricClient *без* указание hello адрес кластера. Локальное управление toohello подключается FabricClient шлюз на код hello hello узла сейчас выполняется, как избежать дополнительный сетевой прыжок.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Подключите tooa безопасного кластер с помощью сертификата клиента

Hello узлов в кластере hello, должны иметь допустимые сертификаты, общее имя или DNS-имя в сети хранения данных отображается в hello [свойство RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) на [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Эта процедура позволяет взаимной проверки подлинности клиента hello и hello узлов кластера.

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>Подключите tooa безопасного кластер интерактивно с помощью Azure Active Directory

Следующий пример использует Azure Active Directory для сертификата клиента удостоверение и сервера для идентификации сервера Hello.

Диалоговое окно автоматически появится окно для интерактивного входа в систему при подключении toohello кластера.

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>Подключите tooa безопасного кластер не в интерактивном режиме с помощью Azure Active Directory

Hello следующий пример использует Microsoft.IdentityModel.Clients.ActiveDirectory, версия: 2.19.208020213.

Дополнительные сведения о получении маркеров AAD см. в описании [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Подключите кластер безопасного tooa без ведома предыдущих метаданных с помощью Azure Active Directory

Hello следующий пример использует неинтерактивной приобретения токена, но hello же подход может быть используется toobuild качества пользовательских интерактивный приобретения токена. Hello Azure Active Directory метаданных, необходимых для получения маркера считывается из конфигурации кластера.

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>Подключите tooa безопасного кластер с помощью Service Fabric Explorer
tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) для данного кластера, укажите в браузере для:

`http://<your-cluster-endpoint>:19080/Explorer`

полный URL-адрес Hello доступен также в панели essentials кластера hello hello портал Azure.

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Подключите tooa безопасного кластер с помощью Azure Active Directory

tooconnect tooa кластера, защищенного с помощью AAD, точка веб-браузера:

`https://<your-cluster-endpoint>:19080/Explorer`

Будут автоматически осуществлять запрос toolog вход с помощью AAD.

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Подключите tooa безопасного кластер с помощью сертификата клиента

tooconnect tooa кластера, защищенного с помощью сертификатов, точка веб-браузера:

`https://<your-cluster-endpoint>:19080/Explorer`

Будут автоматически осуществлять запрос tooselect сертификат клиента.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>Настроить сертификат клиента на удаленном компьютере hello
По крайней мере два сертификата можно использовать для обеспечения безопасности кластера hello, один для hello кластером и сервером сертификатов и другой для клиентского доступа.  Рекомендуется также использовать дополнительные сертификаты и сертификаты клиентского доступа.  toosecure hello взаимодействия между клиентом и узла кластера с помощью сертификатов безопасности, требуется tooobtain и установите сертификат клиента hello. Hello сертификат можно установить в hello личных () хранилище My hello локального компьютера или текущего пользователя hello.  Необходимо также hello отпечаток сертификата сервера hello hello клиента для проверки подлинности hello кластера.

Запустите следующие tooset командлет PowerShell hello сертификата клиента на компьютере hello, на котором будет доступен кластера hello hello.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

Если самозаверяющий сертификат, необходимо tooimport он машины tooyour «доверенные лица» хранить перед использованием этого tooconnect сертификат tooa безопасности кластера.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Дальнейшие действия

* [Обновление кластера Service Fabric](service-fabric-cluster-upgrade.md)
* [Управление приложениями Service Fabric в Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Общие сведения о модели работоспособности в Service Fabric](service-fabric-health-introduction.md)
* [Безопасность приложений и запуск от имени](service-fabric-application-runas-security.md)
* [Командная строка Azure Service Fabric](service-fabric-cli.md)
