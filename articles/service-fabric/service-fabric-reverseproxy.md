---
title: "aaaAzure Service Fabric обратный прокси-сервер | Документы Microsoft"
description: "Используйте toomicroservices связи с внутренней и внешней hello кластера Service Fabric обратного прокси-сервера."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Обратный прокси-сервер в Azure Service Fabric
Hello обратного прокси-сервера, встроенный в Azure Service Fabric адреса микрослужбами в кластере Service Fabric hello, который предоставляет конечные точки HTTP.

## <a name="microservices-communication-model"></a>Модель взаимодействия с микрослужбами
Как правило, Микрослужбами в Service Fabric работы на подмножестве виртуальных машин в кластере hello и можно перемещать из одного tooanother виртуальной машины по различным причинам. Таким образом hello конечных точек для микрослужбами можно изменять динамически. Hello стандартным шаблоном toocommunicate toohello микрослужбу — hello следующие решения цикла:

1. Разрешить размещение службы hello изначально через службу имен hello.
2. Подключения toohello службы.
3. Определить причину сбоев подключения hello и устраните расположение службы hello еще раз, при необходимости.

Этот процесс обычно включает упаковки связи клиентских библиотек в цикле повтора, который реализует hello политики службы разрешения и повторите попытку.
Дополнительные сведения см. в разделе [Подключение к службам в Service Fabric и взаимодействие с ними](service-fabric-connect-and-communicate-with-services.md).

### <a name="communicating-by-using-hello-reverse-proxy"></a>Связь с использованием hello обратного прокси-сервера
Hello обратного прокси-сервера в Service Fabric запускается на всех узлах кластера hello hello. Она выполняет процесс разрешения hello всей службы от имени клиента и затем перенаправляет запрос клиента hello. Таким образом клиенты, работающие в кластере hello можно использовать любую клиентские HTTP связи библиотеки tootalk toohello целевую службу с помощью hello обратного прокси-сервера hello, выполняется локально на одном узле.

![Взаимодействие изнутри][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Достижение микрослужбами из вне кластера hello
модель внешней связи по умолчанию Hello для микрослужбами представляет собой модель согласиться на использование, где каждая служба нельзя обращаться непосредственно из внешних клиентов. [Подсистема балансировки нагрузки Azure](../load-balancer/load-balancer-overview.md), являющееся границы сети между микрослужбами и внешними клиентами выполняет преобразование сетевых адресов и пересылает внешние запросы конечных точек toointernal IP: Port. toomake клиентов доступны непосредственно tooexternal микрослужбу конечной точки, необходимо сначала настроить использует порт tooeach tooforward трафика, который hello службы балансировки нагрузки в кластере hello. Кроме того большинство микрослужбами, особенно с отслеживанием состояния микрослужбами не live на всех узлах кластера hello. Hello микрослужбами можно перемещать между узлами при отработке отказа. В таких случаях подсистема балансировки нагрузки не может определить эффективно hello расположение целевого узла hello toowhich реплик hello пересылать трафик.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Достижение микрослужбами через hello обратного прокси-сервера из кластера вне hello
Вместо настройки порта hello отдельных службы в подсистему балансировки нагрузки, можно настроить только hello порт hello обратного прокси-сервера в подсистему балансировки нагрузки. Эта конфигурация позволяет клиентам за пределами кластера hello достичь служб внутри hello кластера с помощью hello обратный прокси-сервер без дополнительной настройки.

![Взаимодействие извне][0]

> [!WARNING]
> При настройке обратных прокси hello порт в подсистему балансировки нагрузки все микрослужбами hello кластера, которые предоставляют конечную точку HTTP адресуемых за пределами кластера hello.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>Формат URI для адресации служб с помощью hello обратного прокси-сервера
Здравствуйте, использующая обратного прокси-сервера следует перенаправить конкретных универсальный код ресурса идентификатора (URI) формат tooidentify hello секции toowhich hello входящих запрос службы:

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **HTTP (s):** hello обратного прокси-сервера может быть настроенный tooaccept HTTP или HTTPS-трафика. Пересылка HTTPS можно найти слишком[подключения служба безопасного tooa обратного прокси-сервера hello](service-fabric-reverseproxy-configure-secure-communication.md) после установки toolisten обратный прокси-сервер HTTPS.
* **Кластер полное доменное имя (FQDN) | внутренний IP-адрес:** для внешних клиентов можно настроить hello обратного прокси-сервера, чтобы он будет доступен через домен кластера hello, например mycluster.eastus.cloudapp.azure.com. По умолчанию hello обратный прокси-сервер работает на каждом узле. Для внутреннего трафика hello обратного прокси-сервера можно получить на localhost или на любой внутренний узел IP-адрес, например 10.0.0.1.
* **Порт:** порт hello, например 19081, который был задан для hello обратного прокси-сервера.
* **ServiceInstanceName:** hello полное имя экземпляра службы hello развернуты, что вы пытаетесь tooreach без hello «fabric: / «схемы. Например, hello tooreach *fabric: / myapp/myservice/* службы, следует использовать *myapp/myservice*.

    Имя экземпляра службы Hello учитывается регистр. С помощью другой регистр символов для имени экземпляра службы hello в URL-АДРЕСЕ hello вызывает toofail hello запросы с 404 (не найдено).
* **Суффикс пути:** это фактический URL-путь hello *myapi/значения/добавить/3*, для нужной tooconnect для службы hello.
* **PartitionKey:** для секционированных службы, это ключ вычисляемую секцию hello hello секции, которые должны tooreach. Обратите внимание, что это *не* hello идентификатор GUID раздела. Этот параметр не является обязательным для служб, использующих hello одноэлементную схему секционирования.
* **PartitionKind:** это hello схемы секционирования службы. Это может иметь значение "Int64Range" (Диапазон Int64) или "Named" (Именованная). Этот параметр не является обязательным для служб, использующих hello одноэлементную схему секционирования.
* **ListenerName** hello конечные точки из службы hello имеют форму hello {«Конечные точки»: {«Listener1»: «Endpoint1», «Listener2»: «Endpoint2»...}}. Когда hello служба предоставляет несколько конечных точек, определяет конечную точку hello, запрос клиента hello должен быть передан. Это можно опустить, если служба hello имеется только один прослушиватель.
* **TargetReplicaSelector** указывает, каким образом должен быть выбран hello целевая реплика или экземпляр.
  * Когда hello целевой службы с отслеживанием состояния, hello TargetReplicaSelector может принимать одно из следующих hello: «PrimaryReplica», «RandomSecondaryReplica» или «RandomReplica». Если этот параметр не указан, по умолчанию hello — «PrimaryReplica».
  * При hello целевой службы без сохранения состояния, обратный прокси-сервер принимает экземпляр случайных hello секции tooforward hello запрос службы.
* **Время ожидания:** указывает hello время ожидания для запроса hello HTTP, созданные службы toohello hello обратный прокси-сервер от имени hello клиентского запроса. значение по умолчанию Hello составляет 60 секунд. Данный параметр является необязательным.

### <a name="example-usage"></a>Пример использования
В качестве примера рассмотрим hello *fabric: / MyApp/MyService* службу, которая открывает прослушиватель HTTP на hello URL-адреса:

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

Ниже приведены ресурсы hello hello службы:

* `/index.html`
* `/api/users/<userId>`

Если служба hello использует схему секционирования singleton hello, hello *PartitionKey* и *PartitionKind* параметры строки запроса не являются обязательными, а hello службы можно получить с помощью шлюза hello как:

* Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* Изнутри: `http://localhost:19081/MyApp/MyService`

Если служба hello использует hello универсальный Int64 схему секционирования, hello *PartitionKey* и *PartitionKind* параметры строки запроса должен быть используется tooreach секции hello службы:

* Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* Изнутри: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

tooreach hello ресурсов, предоставляемых службой hello, просто поместите hello пути к ресурсу после имени службы hello в hello URL-адрес:

* Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* Изнутри: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

шлюз Hello затем будет пересылать toohello службы эти запросы на URL-адрес:

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>Специальные действия для служб с общим доступом к портам
Шлюз Azure приложение пытается tooresolve службы адрес еще раз и повторите запрос hello в том случае, когда службы невозможен. Это Главное преимущество шлюза приложения, так как клиентский код не требуется tooimplement свои собственные разрешения для службы и разрешать цикла.

Как правило когда службы невозможен, экземпляр службы hello или реплики перемещено tooa другой узел в рамках своего обычного жизненного цикла. В этом случае шлюз приложений может получать сети подключения ошибки указывает, что конечной точки, что нет открытых больше времени на hello изначально разрешить адрес.

Тем не менее реплики или экземпляры службы могут совместно использовать хост-процесс и даже порт при размещении на веб-сервере на основе http.sys, включая:

* [System.Net.HttpListener;](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [ASP.NET Core WebListener;](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana.](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

В этом случае вполне вероятно, hello веб-сервер доступен в хост-процесса hello и отвечать на запросы toorequests, но hello разрешении экземпляр службы или реплика больше не доступен на узле hello. В этом случае шлюз hello получать ответы HTTP 404 hello веб-сервера. Следовательно, ошибка "HTTP 404" может иметь два разных значения.

- #1: адрес службы hello имеют правильный регистр, но ресурс hello, hello запрошенного пользователя не существует.
- Случай #2: неверный адрес службы hello и ресурса hello, hello запрошенного пользователя могут существовать на другом узле.

Hello первый случай — обычный HTTP 404, который считается пользовательской ошибки. Однако в случае второй hello hello пользователь запросил ресурс, который существует. Шлюз приложений было невозможно toolocate, он перемещен, так как hello самой службы. Приложения требованиям tooresolve hello адрес шлюза снова и повторите попытку hello запрос.

Таким образом, использование шлюза приложений должна toodistinguish способом между этих двух случаях. toomake, что различие, подсказку с сервера hello необходим.

* По умолчанию шлюз приложений предполагает случай #2 и пытается tooresolve и проблемы hello запрос еще раз.
* tooApplication вариант #1 tooindicate шлюза, hello службы должна возвращать hello, выполнив HTTP-заголовок ответа:

  `X-ServiceFabric : ResourceNotFound`

Этот заголовок ответа HTTP указывает на обычный HTTP 404 ситуацию, в которой hello запрошенный ресурс не существует, а шлюз приложений не будет адрес службы hello tooresolve еще раз.

## <a name="setup-and-configuration"></a>Установка и настройка

### <a name="enable-reverse-proxy-via-azure-portal"></a>Включение обратного прокси-сервера на портале Azure

Портал Azure предоставляет параметр tooenable обратного прокси-сервера при создании нового кластера Service Fabric.
В разделе **кластера Service Fabric создать**, шаг 2: конфигурация кластера, конфигурация типа узла, установите флажок hello слишком «Enable обратного прокси».
Для настройки безопасного обратного прокси-сервера, SSL-сертификат может быть указано в шаге 3: слишком безопасности, Настройка параметров безопасности кластера, а также hello, установите флажок «Включить SSL-сертификат для обратного прокси-сервера» и введите сведения о сертификате hello.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Включение обратного прокси-сервера с помощью шаблонов Azure Resource Manager

Можно использовать hello [шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable hello обратного прокси-сервера в Service Fabric для hello кластера.

См. слишком[Настройка HTTPS обратного прокси-сервера в кластере безопасного](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) для диспетчера ресурсов Azure шаблона образцы tooconfigure безопасного обратного прокси-сервера с помощью сертификата и обработка смены сертификата.

Во-первых вы получаете шаблона hello hello кластера, которые должны toodeploy. Можно использовать шаблоны образец hello или создать настраиваемый шаблон диспетчера ресурсов. Затем можно включить hello обратного прокси-сервера с помощью hello следующие шаги:

1. Определить порт для hello обратного прокси-сервера в hello [раздела параметров](../azure-resource-manager/resource-group-authoring-templates.md) hello шаблона.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. Укажите порт hello для каждого из объектов nodetype hello в hello **кластера** [разделе типа ресурсов](../azure-resource-manager/resource-group-authoring-templates.md).

    порт Hello определяется по имени параметра hello, reverseProxyEndpointPort.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. tooaddress hello обратного прокси-сервера из внешней hello Azure кластера задавать правила балансировки нагрузки Azure hello hello порт, указанный на шаге 1.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. tooconfigure сертификаты SSL для порта hello для обратного прокси hello, добавьте hello сертификат toohello ***reverseProxyCertificate*** свойство в hello **кластера** [разделе типа ресурсов](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Поддержка сертификат обратного прокси-сервера, который не совпадает с сертификатом hello кластера
 Если сертификат hello обратного прокси-сервера не совпадает с hello сертификата, который защищает hello кластера, затем hello ранее указанный сертификат должен быть установлен на виртуальной машине hello и добавлены toohello список управления доступом (ACL), позволяющую Service Fabric доступ к нему. Это можно сделать в hello **virtualMachineScaleSets** [разделе типа ресурсов](../resource-group-authoring-templates.md). Для установки добавьте osProfile toohello этого сертификата. раздел расширения Hello hello шаблона можно обновить сертификат hello в hello ACL.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> При использовании сертификатов, которые отличаются от hello кластера сертификат tooenable hello обратного прокси-сервера в существующем кластере, установить сертификат hello обратного прокси-сервера и обновить hello ACL в кластере hello, перед включением hello обратного прокси-сервера. Полный hello [шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) развертывания с помощью параметров hello, описанных ранее перед началом развертывания tooenable hello обратного прокси-сервера в шагах 1 – 4.

## <a name="next-steps"></a>Дальнейшие действия
* Пример обмена данными по протоколу HTTP между службами представлен в [примере проекта на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Служба HTTP toosecure перенаправления с hello обратного прокси-сервера](service-fabric-reverseproxy-configure-secure-communication.md)
* [Удаленное взаимодействие службы с Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [Начало работы со службами веб-API Microsoft Azure Service Fabric с саморазмещением OWIN](service-fabric-reliable-services-communication-webapi.md)
* [Коммуникационный стек WCF для надежных служб](service-fabric-reliable-services-communication-wcf.md)
* Дополнительные параметры конфигурации обратного прокси-сервера описаны в разделе о ApplicationGateway/Http статьи [Настройка параметров кластера Service Fabric и политики обновления структур](service-fabric-cluster-fabric-settings.md).

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
