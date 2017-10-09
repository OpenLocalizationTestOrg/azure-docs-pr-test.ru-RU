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
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="44337-103">Защита автономного кластера под управлением Windows с помощью сертификатов X.509</span><span class="sxs-lookup"><span data-stu-id="44337-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="44337-104">В этой статье описывается, как toosecure hello взаимодействия hello различные узлы кластера Windows, автономные также тем tooauthenticate клиенты подключения кластера toothis с использованием сертификатов X.509.</span><span class="sxs-lookup"><span data-stu-id="44337-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="44337-105">Это гарантирует, что только авторизованные пользователи могут получить доступ к кластера hello hello развернутых приложений и выполнять задачи управления.</span><span class="sxs-lookup"><span data-stu-id="44337-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="44337-106">При создании кластера hello на hello кластера должна быть включена защита с помощью сертификата.</span><span class="sxs-lookup"><span data-stu-id="44337-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="44337-107">Дополнительные сведения о безопасности кластера, в том числе безопасности обмена данными между узлами, между клиентом и узлом, и об управлении доступом на основе ролей см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="44337-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="44337-108">Необходимые сертификаты</span><span class="sxs-lookup"><span data-stu-id="44337-108">Which certificates will you need?</span></span>
<span data-ttu-id="44337-109">toostart, [загрузить hello изолированный пакет кластера](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone hello узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="44337-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="44337-110">В hello загружен пакет, вы найдете **ClusterConfig.X509.MultiMachine.json** файла.</span><span class="sxs-lookup"><span data-stu-id="44337-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="44337-111">Откройте файл hello и просмотрите раздел hello для **безопасности** под hello **свойства** раздела:</span><span class="sxs-lookup"><span data-stu-id="44337-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

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

<span data-ttu-id="44337-112">В этом разделе описываются hello сертификаты, необходимые для обеспечения безопасности автономный кластера Windows.</span><span class="sxs-lookup"><span data-stu-id="44337-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="44337-113">При указании сертификата кластера значение hello **ClusterCredentialType** too_**X509**_. При указании сертификата сервера для внешних соединений, задайте hello **ServerCredentialType** слишком_**X509**_. Не обязательно, однако рекомендуется toohave оба эти сертификаты надлежащим образом защищенным кластера. Если эти значения заданы слишком*X509* то необходимо также указать hello соответствующие сертификаты или Service Fabric вызовет исключение. В некоторых сценариях может требуется только toospecify hello _ClientCertificateThumbprints_ или _ReverseProxyCertificate_. В этих сценариях, не требуется задать _ClusterCredentialType_ или _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="44337-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="44337-114">Объект [отпечаток](https://en.wikipedia.org/wiki/Public_key_fingerprint) является первичным идентификатором hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="44337-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="44337-115">Чтение [как tooretrieve отпечаток сертификата](https://msdn.microsoft.com/library/ms734695.aspx) toofind out отпечаток hello hello сертификатов, которые вы создаете.</span><span class="sxs-lookup"><span data-stu-id="44337-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="44337-116">Hello следующей таблице перечислены hello сертификаты, необходимые для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="44337-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="44337-117">**Параметры CertificateInformation**</span><span class="sxs-lookup"><span data-stu-id="44337-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="44337-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="44337-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="44337-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="44337-119">ClusterCertificate</span></span> |<span data-ttu-id="44337-120">Рекомендуется использовать в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="44337-120">Recommended for test environment.</span></span> <span data-ttu-id="44337-121">Этот сертификат является обязательным toosecure hello взаимодействия между hello узлы в кластере.</span><span class="sxs-lookup"><span data-stu-id="44337-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="44337-122">Для обновления можно использовать два разных сертификата — основной и дополнительный.</span><span class="sxs-lookup"><span data-stu-id="44337-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="44337-123">Задайте отпечаток hello основной сертификат hello в hello **отпечаток** разделе, а также получателей в hello hello **ThumbprintSecondary** переменных.</span><span class="sxs-lookup"><span data-stu-id="44337-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="44337-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="44337-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="44337-125">Рекомендуется использовать в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="44337-125">Recommended for production environment.</span></span> <span data-ttu-id="44337-126">Этот сертификат является обязательным toosecure hello взаимодействия между hello узлы в кластере.</span><span class="sxs-lookup"><span data-stu-id="44337-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="44337-127">Можно использовать одно или два общих имени сертификата для кластера.</span><span class="sxs-lookup"><span data-stu-id="44337-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="44337-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="44337-128">ServerCertificate</span></span> |<span data-ttu-id="44337-129">Рекомендуется использовать в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="44337-129">Recommended for test environment.</span></span> <span data-ttu-id="44337-130">Этот сертификат представлены toohello клиента, она попытается tooconnect toothis кластера.</span><span class="sxs-lookup"><span data-stu-id="44337-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="44337-131">Для удобства можно toouse же сертификата для hello *ClusterCertificate* и *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="44337-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="44337-132">Для обновления можно использовать два разных сертификата сервера — основной и дополнительный.</span><span class="sxs-lookup"><span data-stu-id="44337-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="44337-133">Задайте отпечаток hello основной сертификат hello в hello **отпечаток** разделе, а также получателей в hello hello **ThumbprintSecondary** переменных.</span><span class="sxs-lookup"><span data-stu-id="44337-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="44337-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="44337-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="44337-135">Рекомендуется использовать в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="44337-135">Recommended for production environment.</span></span> <span data-ttu-id="44337-136">Этот сертификат представлены toohello клиента, она попытается tooconnect toothis кластера.</span><span class="sxs-lookup"><span data-stu-id="44337-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="44337-137">Для удобства можно toouse же сертификата для hello *ClusterCertificateCommonNames* и *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="44337-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="44337-138">Можно использовать одно или два общих имени сертификата для сервера.</span><span class="sxs-lookup"><span data-stu-id="44337-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="44337-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="44337-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="44337-140">Это набор сертификатов, которые должны tooinstall на клиентах hello с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="44337-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="44337-141">Имеется несколько различных клиентских сертификатов, установленных на компьютерах hello, что требуется кластера toohello tooallow доступа.</span><span class="sxs-lookup"><span data-stu-id="44337-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="44337-142">Задать hello отпечаток каждого сертификата в hello **CertificateThumbprint** переменной.</span><span class="sxs-lookup"><span data-stu-id="44337-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="44337-143">Если значение hello **IsAdmin** слишком*true*, hello клиента с помощью этого сертификата, установленными на нем можно сделать администратору действия управления на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="44337-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="44337-144">Если hello **IsAdmin** — *false*, hello клиента с помощью этого сертификата можно выполнить только hello действия, разрешенные для права доступа, обычно доступные только для чтения.</span><span class="sxs-lookup"><span data-stu-id="44337-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="44337-145">Дополнительные сведения о ролях см. в статье [Контроль доступа на основе ролей](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="44337-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="44337-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="44337-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="44337-147">Набор hello общее имя hello первый сертификат клиента для hello **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="44337-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="44337-148">Hello **CertificateIssuerThumbprint** является отпечатком hello hello издателя сертификата.</span><span class="sxs-lookup"><span data-stu-id="44337-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="44337-149">Чтение [работа с сертификатами](https://msdn.microsoft.com/library/ms731899.aspx) tooknow Дополнительные сведения об общих имен и hello издателя.</span><span class="sxs-lookup"><span data-stu-id="44337-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="44337-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="44337-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="44337-151">Рекомендуется использовать в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="44337-151">Recommended for test environment.</span></span> <span data-ttu-id="44337-152">Это необязательный сертификат, который может быть указан, если необходимо, чтобы toosecure вашей [обратного прокси-сервера](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="44337-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="44337-153">Если вы используете этот сертификат, обязательно укажите для параметра nodeTypes значение reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="44337-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="44337-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="44337-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="44337-155">Рекомендуется использовать в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="44337-155">Recommended for production environment.</span></span> <span data-ttu-id="44337-156">Это необязательный сертификат, который может быть указан, если необходимо, чтобы toosecure вашей [обратного прокси-сервера](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="44337-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="44337-157">Если вы используете этот сертификат, обязательно укажите для параметра nodeTypes значение reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="44337-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="44337-158">Ниже приведен пример конфигурации кластера, где предоставляется hello сертификаты кластера, сервера и клиента.</span><span class="sxs-lookup"><span data-stu-id="44337-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="44337-159">Учтите, что для кластера / server / reverseProxy сертификаты, отпечаток и общее имя не допускается toobe совместно настроенных для hello же тип сертификата.</span><span class="sxs-lookup"><span data-stu-id="44337-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

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

## <a name="certificate-roll-over"></a><span data-ttu-id="44337-160">Смена сертификатов</span><span class="sxs-lookup"><span data-stu-id="44337-160">Certificate roll over</span></span>
<span data-ttu-id="44337-161">Если используется общее имя сертификата вместо отпечатка, чтобы сменить сертификат, не нужно обновлять конфигурацию кластера.</span><span class="sxs-lookup"><span data-stu-id="44337-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="44337-162">Если изменение сертификата включает в себя издателя, наведите курсор на, пожалуйста, не hello старого сертификата издателя в хранилище сертификатов hello по крайней мере 2 часа после установки hello новый издателя сертификата.</span><span class="sxs-lookup"><span data-stu-id="44337-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="44337-163">Получить сертификаты X.509 hello</span><span class="sxs-lookup"><span data-stu-id="44337-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="44337-164">toosecure взаимодействия внутри кластера hello, необходимо сначала tooobtain сертификаты X.509 для узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="44337-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="44337-165">Кроме того toothis toolimit подключения кластера tooauthorized компьютеров и пользователей, может потребоваться tooobtain и установка сертификатов для hello клиентских компьютеров.</span><span class="sxs-lookup"><span data-stu-id="44337-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="44337-166">Для кластеров под управлением рабочих нагрузок, следует использовать [центра сертификации (ЦС)](https://en.wikipedia.org/wiki/Certificate_authority) подписан кластера hello toosecure сертификата X.509.</span><span class="sxs-lookup"><span data-stu-id="44337-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="44337-167">Дополнительные сведения о получении этих сертификатов перейдите слишком[как: получите сертификат](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="44337-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="44337-168">Для кластеров, используемых для целей тестирования вы можете toouse самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="44337-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="44337-169">Создание самозаверяющего сертификата (необязательно)</span><span class="sxs-lookup"><span data-stu-id="44337-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="44337-170">Одним из способов toocreate самозаверяющего сертификата, которая может быть защищена правильно — toouse hello *CertSetup.ps1* скрипта в папке Service Fabric SDK hello в каталоге hello *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="44337-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="44337-171">Изменить это имя файла toochange hello по умолчанию hello сертификата (искать значение hello *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="44337-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="44337-172">Выполните этот сценарий следующим образом: `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="44337-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="44337-173">Теперь можно экспортируйте hello tooa сертификата PFX-файл защищенного паролем.</span><span class="sxs-lookup"><span data-stu-id="44337-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="44337-174">Сначала нужно получите hello отпечаток сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="44337-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="44337-175">Из hello *запустить* меню запуска hello *Управление сертификатами компьютера*.</span><span class="sxs-lookup"><span data-stu-id="44337-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="44337-176">Перейдите toohello **Local Computer\Personal** папки и найти hello сертификата вы только что создан.</span><span class="sxs-lookup"><span data-stu-id="44337-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="44337-177">Дважды щелкните сертификат tooopen hello его, выберите hello *сведения* вкладку и прокрутите вниз toohello *отпечаток* поля.</span><span class="sxs-lookup"><span data-stu-id="44337-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="44337-178">Скопируйте значение отпечатка hello в hello PowerShell указанную ниже команду, после удаления пробелов hello.</span><span class="sxs-lookup"><span data-stu-id="44337-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="44337-179">Изменение hello `String` значение tooprotect tooa подходящий защищенный пароль, он и выполнения hello следующую команду в PowerShell:</span><span class="sxs-lookup"><span data-stu-id="44337-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="44337-180">toosee hello сведения о сертификате, установленном на hello компьютера можно выполнять hello следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="44337-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="44337-181">Кроме того, если у вас есть подписка Azure, выполните раздел hello [добавить сертификаты tooKey хранилище](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="44337-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="44337-182">Установка сертификатов hello</span><span class="sxs-lookup"><span data-stu-id="44337-182">Install hello certificates</span></span>
<span data-ttu-id="44337-183">Как только сертификаты, их можно установить на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="44337-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="44337-184">Узлы должны toohave hello последней версии Windows PowerShell на них установлен 3.x.</span><span class="sxs-lookup"><span data-stu-id="44337-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="44337-185">Необходимо будет toorepeat эти действия на каждом узле кластера и сервер сертификатов и все вторичные сертификаты.</span><span class="sxs-lookup"><span data-stu-id="44337-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="44337-186">Скопируйте файлы toohello hello PFX-файл узла.</span><span class="sxs-lookup"><span data-stu-id="44337-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="44337-187">Откройте окно PowerShell с правами администратора и введите следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="44337-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="44337-188">Замените hello *$pswd* с паролем hello используется toocreate этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="44337-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="44337-189">Замените hello *$PfxFilePath* с указанием полного пути hello узла копируются toothis hello PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="44337-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="44337-190">Теперь можно задайте hello контроля доступа на этот сертификат, чтобы hello Service Fabric процесс, который выполняется под hello учетной записи сетевой службы, можно использовать его, выполнив следующий скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="44337-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="44337-191">Укажите hello отпечаток сертификата hello и «Сетевая служба» для учетной записи службы hello.</span><span class="sxs-lookup"><span data-stu-id="44337-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="44337-192">Можно проверить, hello списки управления доступом в сертификате hello верны, открыв сертификат hello в *запустить* > *Управление сертификатами компьютера* и просмотрев *все задачи*  >  *Управление закрытыми ключами*.</span><span class="sxs-lookup"><span data-stu-id="44337-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
4. <span data-ttu-id="44337-193">Повторите приведенные выше действия hello для каждого сертификата сервера.</span><span class="sxs-lookup"><span data-stu-id="44337-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="44337-194">Также можно использовать эти действия tooinstall hello сертификаты клиента на компьютерах hello нужных кластера toohello tooallow доступа.</span><span class="sxs-lookup"><span data-stu-id="44337-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="44337-195">Создание безопасного кластера hello</span><span class="sxs-lookup"><span data-stu-id="44337-195">Create hello secure cluster</span></span>
<span data-ttu-id="44337-196">После настройки hello **безопасности** раздел hello **ClusterConfig.X509.MultiMachine.json** , вы можете продолжить файла слишком[создать кластер](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure раздела Здравствуйте, узлов и создание кластера автономный hello.</span><span class="sxs-lookup"><span data-stu-id="44337-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="44337-197">Запомнить toouse hello **ClusterConfig.X509.MultiMachine.json** файла при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="44337-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="44337-198">Например команда может выглядеть hello следующее:</span><span class="sxs-lookup"><span data-stu-id="44337-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="44337-199">После создания безопасного hello Windows автономный кластер успешно и программа установки Здравствуйте tooit tooconnect авторизованных клиентов, выполните раздел hello [Connect tooa безопасного кластера с помощью PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="44337-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="44337-200">Например:</span><span class="sxs-lookup"><span data-stu-id="44337-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="44337-201">Другие toowork команд PowerShell можно выполнять с кластером.</span><span class="sxs-lookup"><span data-stu-id="44337-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="44337-202">Например [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow список узлов в этом кластере безопасной.</span><span class="sxs-lookup"><span data-stu-id="44337-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="44337-203">кластер tooremove hello, подключить toohello узел в кластере hello, куда был загружен пакет Service Fabric hello, откройте командную строку и перейдите в папку toohello пакета.</span><span class="sxs-lookup"><span data-stu-id="44337-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="44337-204">Теперь выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="44337-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="44337-205">Неправильный сертификат конфигурации может помешать кластера hello возникающие во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="44337-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="44337-206">tooself-Диагностика проблем безопасности, см. в группе просмотра событий *журналы приложений и служб* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="44337-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

