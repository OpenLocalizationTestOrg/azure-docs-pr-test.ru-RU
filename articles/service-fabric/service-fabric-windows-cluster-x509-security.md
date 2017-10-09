---
title: "aaaSecure Azure Service Fabric кластера в Windows с использованием сертификатов | Документы Microsoft"
description: "В этой статье описывается, как связи toosecure в автономный hello или закрытый кластера также между клиентами и hello кластера."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>Защита автономного кластера под управлением Windows с помощью сертификатов X.509
В этой статье описывается, как toosecure hello взаимодействия hello различные узлы кластера Windows, автономные также тем tooauthenticate клиенты подключения кластера toothis с использованием сертификатов X.509. Это гарантирует, что только авторизованные пользователи могут получить доступ к кластера hello hello развернутых приложений и выполнять задачи управления.  При создании кластера hello на hello кластера должна быть включена защита с помощью сертификата.  

Дополнительные сведения о безопасности кластера, в том числе безопасности обмена данными между узлами, между клиентом и узлом, и об управлении доступом на основе ролей см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>Необходимые сертификаты
toostart, [загрузить hello изолированный пакет кластера](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone hello узлов в кластере. В hello загружен пакет, вы найдете **ClusterConfig.X509.MultiMachine.json** файла. Откройте файл hello и просмотрите раздел hello для **безопасности** под hello **свойства** раздела:

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

В этом разделе описываются hello сертификаты, необходимые для обеспечения безопасности автономный кластера Windows. При указании сертификата кластера значение hello **ClusterCredentialType** too_**X509**_. При указании сертификата сервера для внешних соединений, задайте hello **ServerCredentialType** слишком_**X509**_. Не обязательно, однако рекомендуется toohave оба эти сертификаты надлежащим образом защищенным кластера. Если эти значения заданы слишком*X509* то необходимо также указать hello соответствующие сертификаты или Service Fabric вызовет исключение. В некоторых сценариях может требуется только toospecify hello _ClientCertificateThumbprints_ или _ReverseProxyCertificate_. В этих сценариях, не требуется задать _ClusterCredentialType_ или _ServerCredentialType_ too_X509_.


> [!NOTE]
> Объект [отпечаток](https://en.wikipedia.org/wiki/Public_key_fingerprint) является первичным идентификатором hello сертификата. Чтение [как tooretrieve отпечаток сертификата](https://msdn.microsoft.com/library/ms734695.aspx) toofind out отпечаток hello hello сертификатов, которые вы создаете.
> 
> 

Hello следующей таблице перечислены hello сертификаты, необходимые для настройки кластера.

| **Параметры CertificateInformation** | **Описание** |
| --- | --- |
| ClusterCertificate |Рекомендуется использовать в тестовой среде. Этот сертификат является обязательным toosecure hello взаимодействия между hello узлы в кластере. Для обновления можно использовать два разных сертификата — основной и дополнительный. Задайте отпечаток hello основной сертификат hello в hello **отпечаток** разделе, а также получателей в hello hello **ThumbprintSecondary** переменных. |
| ClusterCertificateCommonNames |Рекомендуется использовать в рабочей среде. Этот сертификат является обязательным toosecure hello взаимодействия между hello узлы в кластере. Можно использовать одно или два общих имени сертификата для кластера. |
| ServerCertificate |Рекомендуется использовать в тестовой среде. Этот сертификат представлены toohello клиента, она попытается tooconnect toothis кластера. Для удобства можно toouse же сертификата для hello *ClusterCertificate* и *ServerCertificate*. Для обновления можно использовать два разных сертификата сервера — основной и дополнительный. Задайте отпечаток hello основной сертификат hello в hello **отпечаток** разделе, а также получателей в hello hello **ThumbprintSecondary** переменных. |
| ServerCertificateCommonNames |Рекомендуется использовать в рабочей среде. Этот сертификат представлены toohello клиента, она попытается tooconnect toothis кластера. Для удобства можно toouse же сертификата для hello *ClusterCertificateCommonNames* и *ServerCertificateCommonNames*. Можно использовать одно или два общих имени сертификата для сервера. |
| ClientCertificateThumbprints |Это набор сертификатов, которые должны tooinstall на клиентах hello с проверкой подлинности. Имеется несколько различных клиентских сертификатов, установленных на компьютерах hello, что требуется кластера toohello tooallow доступа. Задать hello отпечаток каждого сертификата в hello **CertificateThumbprint** переменной. Если значение hello **IsAdmin** слишком*true*, hello клиента с помощью этого сертификата, установленными на нем можно сделать администратору действия управления на кластере hello. Если hello **IsAdmin** — *false*, hello клиента с помощью этого сертификата можно выполнить только hello действия, разрешенные для права доступа, обычно доступные только для чтения. Дополнительные сведения о ролях см. в статье [Контроль доступа на основе ролей](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Набор hello общее имя hello первый сертификат клиента для hello **CertificateCommonName**. Hello **CertificateIssuerThumbprint** является отпечатком hello hello издателя сертификата. Чтение [работа с сертификатами](https://msdn.microsoft.com/library/ms731899.aspx) tooknow Дополнительные сведения об общих имен и hello издателя. |
| ReverseProxyCertificate |Рекомендуется использовать в тестовой среде. Это необязательный сертификат, который может быть указан, если необходимо, чтобы toosecure вашей [обратного прокси-сервера](service-fabric-reverseproxy.md). Если вы используете этот сертификат, обязательно укажите для параметра nodeTypes значение reverseProxyEndpointPort. |
| ReverseProxyCertificateCommonNames |Рекомендуется использовать в рабочей среде. Это необязательный сертификат, который может быть указан, если необходимо, чтобы toosecure вашей [обратного прокси-сервера](service-fabric-reverseproxy.md). Если вы используете этот сертификат, обязательно укажите для параметра nodeTypes значение reverseProxyEndpointPort. |

Ниже приведен пример конфигурации кластера, где предоставляется hello сертификаты кластера, сервера и клиента. Учтите, что для кластера / server / reverseProxy сертификаты, отпечаток и общее имя не допускается toobe совместно настроенных для hello же тип сертификата.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>Смена сертификатов
Если используется общее имя сертификата вместо отпечатка, чтобы сменить сертификат, не нужно обновлять конфигурацию кластера.
Если изменение сертификата включает в себя издателя, наведите курсор на, пожалуйста, не hello старого сертификата издателя в хранилище сертификатов hello по крайней мере 2 часа после установки hello новый издателя сертификата.

## <a name="acquire-hello-x509-certificates"></a>Получить сертификаты X.509 hello
toosecure взаимодействия внутри кластера hello, необходимо сначала tooobtain сертификаты X.509 для узлов кластера. Кроме того toothis toolimit подключения кластера tooauthorized компьютеров и пользователей, может потребоваться tooobtain и установка сертификатов для hello клиентских компьютеров.

Для кластеров под управлением рабочих нагрузок, следует использовать [центра сертификации (ЦС)](https://en.wikipedia.org/wiki/Certificate_authority) подписан кластера hello toosecure сертификата X.509. Дополнительные сведения о получении этих сертификатов перейдите слишком[как: получите сертификат](http://msdn.microsoft.com/library/aa702761.aspx).

Для кластеров, используемых для целей тестирования вы можете toouse самозаверяющий сертификат.

## <a name="optional-create-a-self-signed-certificate"></a>Создание самозаверяющего сертификата (необязательно)
Одним из способов toocreate самозаверяющего сертификата, которая может быть защищена правильно — toouse hello *CertSetup.ps1* скрипта в папке Service Fabric SDK hello в каталоге hello *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Изменить это имя файла toochange hello по умолчанию hello сертификата (искать значение hello *CN = ServiceFabricDevClusterCert*). Выполните этот сценарий следующим образом: `.\CertSetup.ps1 -Install`.

Теперь можно экспортируйте hello tooa сертификата PFX-файл защищенного паролем. Сначала нужно получите hello отпечаток сертификата hello. Из hello *запустить* меню запуска hello *Управление сертификатами компьютера*. Перейдите toohello **Local Computer\Personal** папки и найти hello сертификата вы только что создан. Дважды щелкните сертификат tooopen hello его, выберите hello *сведения* вкладку и прокрутите вниз toohello *отпечаток* поля. Скопируйте значение отпечатка hello в hello PowerShell указанную ниже команду, после удаления пробелов hello.  Изменение hello `String` значение tooprotect tooa подходящий защищенный пароль, он и выполнения hello следующую команду в PowerShell:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

toosee hello сведения о сертификате, установленном на hello компьютера можно выполнять hello следующую команду PowerShell:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

Кроме того, если у вас есть подписка Azure, выполните раздел hello [добавить сертификаты tooKey хранилище](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Установка сертификатов hello
Как только сертификаты, их можно установить на узлах кластера hello. Узлы должны toohave hello последней версии Windows PowerShell на них установлен 3.x. Необходимо будет toorepeat эти действия на каждом узле кластера и сервер сертификатов и все вторичные сертификаты.

1. Скопируйте файлы toohello hello PFX-файл узла.
2. Откройте окно PowerShell с правами администратора и введите следующие команды hello. Замените hello *$pswd* с паролем hello используется toocreate этот сертификат. Замените hello *$PfxFilePath* с указанием полного пути hello узла копируются toothis hello PFX-файл.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Теперь можно задайте hello контроля доступа на этот сертификат, чтобы hello Service Fabric процесс, который выполняется под hello учетной записи сетевой службы, можно использовать его, выполнив следующий скрипт hello. Укажите hello отпечаток сертификата hello и «Сетевая служба» для учетной записи службы hello. Можно проверить, hello списки управления доступом в сертификате hello верны, открыв сертификат hello в *запустить* > *Управление сертификатами компьютера* и просмотрев *все задачи*  >  *Управление закрытыми ключами*.
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. Повторите приведенные выше действия hello для каждого сертификата сервера. Также можно использовать эти действия tooinstall hello сертификаты клиента на компьютерах hello нужных кластера toohello tooallow доступа.

## <a name="create-hello-secure-cluster"></a>Создание безопасного кластера hello
После настройки hello **безопасности** раздел hello **ClusterConfig.X509.MultiMachine.json** , вы можете продолжить файла слишком[создать кластер](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure раздела Здравствуйте, узлов и создание кластера автономный hello. Запомнить toouse hello **ClusterConfig.X509.MultiMachine.json** файла при создании кластера hello. Например команда может выглядеть hello следующее:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

После создания безопасного hello Windows автономный кластер успешно и программа установки Здравствуйте tooit tooconnect авторизованных клиентов, выполните раздел hello [Connect tooa безопасного кластера с помощью PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. Например:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

Другие toowork команд PowerShell можно выполнять с кластером. Например [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow список узлов в этом кластере безопасной.


кластер tooremove hello, подключить toohello узел в кластере hello, куда был загружен пакет Service Fabric hello, откройте командную строку и перейдите в папку toohello пакета. Теперь выполните hello следующую команду:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Неправильный сертификат конфигурации может помешать кластера hello возникающие во время развертывания. tooself-Диагностика проблем безопасности, см. в группе просмотра событий *журналы приложений и служб* > *Microsoft Service Fabric*.
> 
> 

