---
title: "aaaAzure Service Fabric обратного прокси-сервера безопасного взаимодействия | Документы Microsoft"
description: "Настройка обратного прокси-сервера tooenable безопасного взаимодействия конца в конец."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Служба безопасного tooa соединены hello обратного прокси-сервера

В этой статье объясняется, как tooestablish безопасное подключение между hello обратного прокси-сервера и служб, позволяя окончания tooend безопасного канала.

Соединение toosecure службы поддерживается только в том случае, если обратный прокси-сервер является toolisten, настроенных на HTTPS. Hello документе предполагается, что это случай hello.
См. слишком[обратный прокси-сервер в Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello обратного прокси-сервера в Service Fabric.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Установление безопасного соединения между hello обратного прокси-сервера и служб 

### <a name="reverse-proxy-authenticating-tooservices"></a>Обратный прокси-сервер проверки подлинности tooservices:
Hello обратный прокси-сервер должен идентифицировать себя с использованием его сертификата, заданного с tooservices ***reverseProxyCertificate*** свойство в hello **кластера** [разделе типа ресурсов](../azure-resource-manager/resource-group-authoring-templates.md). Службы могут реализовывать hello логику tooverify hello сертификат hello обратного прокси-сервера. Hello службы могут указывать сведения о сертификате клиента hello принимается как параметры конфигурации в пакете конфигурации hello. Это могут быть прочитаны во время выполнения и использовать toovalidate hello сертификат hello обратного прокси-сервера. См. слишком[Управление параметрами приложения](service-fabric-manage-multiple-environment-app-configuration.md) параметры конфигурации tooadd hello. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>Обратный прокси-сервер, проверка удостоверения службы hello через hello сертификата, предоставленного службой hello:
Проверка сертификата сервера tooperform представленных hello служб сертификатов hello, обратного прокси-сервера поддерживает один из следующих вариантов hello: None, ServiceCommonNameAndIssuer и ServiceCertificateThumbprints.
один из этих трех параметров tooselect укажите hello **ApplicationCertificateValidationPolicy** в разделе параметров hello элемента шлюза приложения/Http в [fabricSettings](service-fabric-cluster-fabric-settings.md).

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

См. в следующем разделе toohello подробные сведения о дополнительной настройке для каждого из этих параметров.

### <a name="service-certificate-validation-options"></a>Параметры проверки сертификата службы 

- **Нет**: обратного прокси-сервера пропускает проверку сертификатов прокси службы hello и устанавливает безопасное соединение hello. Это поведение по умолчанию hello.
Укажите hello **ApplicationCertificateValidationPolicy** со значением **нет** в разделе параметров hello элемента шлюза приложения/Http.

- **ServiceCommonNameAndIssuer**: обратный прокси-сервер проверяет hello сертификат, представленный hello службы на основании общее имя сертификата и отпечаток немедленно издателя: укажите hello **ApplicationCertificateValidationPolicy**  со значением **ServiceCommonNameAndIssuer** в разделе параметров hello элемента шлюза приложения/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

Список toospecify hello общее имя службы и отпечатки издателя, добавьте **шлюза приложения, Http или ServiceCommonNameAndIssuer** элемента под fabricSettings, как показано ниже. В элементе массива параметров hello можно добавить несколько пар отпечаток издателя и общее имя сертификата. 

Если обратный прокси-сервер hello конечной точки подключается toopresents сертификат, который обычно имя и издатель отпечаток соответствует любому из hello значения, указанные здесь, устанавливается канал SSL. После toomatch hello сертификат подробные сведения об ошибках обратного прокси-сервера не выполняется hello клиентский запрос с кодом состояния 502 (Неверный шлюз). Строка состояния HTTP Hello также будет содержать hello фразу «Недопустимый сертификат SSL». 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- **ServiceCertificateThumbprints**: обратный прокси-сервер будет проверять hello прокси службы сертификат, основанный на его отпечаток. Вы можете выбрать toogo этот маршрут при hello службы должны быть настроены самозаверяющие сертификаты: укажите hello **ApplicationCertificateValidationPolicy** со значением **ServiceCertificateThumbprints**в разделе параметров hello элемента шлюза приложения/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

Также укажите отпечатки hello с **ServiceCertificateThumbprints** параметры в разделе элемента шлюза приложения/Http. Несколько отпечатки можно указать как список разделенных запятыми, в поле значение hello, как показано ниже:

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

Если отпечаток сертификата сервера hello hello указан в этой записи конфигурации, обратного прокси-сервера успешно hello SSL-подключение. В противном случае он завершает соединение hello и происходит сбой hello запрос клиента с 502 (Неверный шлюз). Строка состояния HTTP Hello также будет содержать hello фразу «Недопустимый сертификат SSL».

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>Логика выбора конечной точки, когда службы предоставляют защищенные и незащищенные конечные точки
Service Fabric поддерживает настройку нескольких конечных точек для службы. См. [Указание ресурсов в манифесте службы](service-fabric-service-manifest-resources.md).

Обратный прокси-сервер выбирает одну из hello hello конечные точки tooforward запрос в зависимости от hello **ListenerName** параметр запроса. Если этот параметр не указан, его можно выбрать любой конечной точки из списка конечных точек hello. Это может быть конечная точка HTTP или HTTPS. Возможно, сценариев и требований место toooperate hello обратного прокси-сервера в «только режиме безопасности», т. е. Вы не хотите hello безопасного обратного прокси-сервера tooforward запросов toounsecured конечных точек. Это можно сделать, указав hello **SecureOnlyMode** запись конфигурации со значением **true** в разделе параметров hello элемента шлюза приложения/Http.   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> При работе в **SecureOnlyMode**, если клиент указал **ListenerName** соответствующая конечная точка HTTP(unsecured) tooan, hello запрос с кодом состояния 404 (не найдено) HTTP завершается ошибкой обратного прокси-сервера.

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>Настройка проверки подлинности сертификата клиента через обратный прокси-сервер hello
Завершение запросов SSL осуществляется по hello обратный прокси-сервер и все данные сертификата клиента hello будут потеряны. Для hello служб tooperform сертификат проверки подлинности клиента, задайте hello **ForwardClientCertificate** в разделе параметров hello элемента шлюза приложения/Http.

1. При **ForwardClientCertificate** задано слишком**false**, обратного прокси-сервера не будет запрашиваться для сертификата клиента hello во время SSL-подтверждения с клиентом hello.
Это поведение по умолчанию hello.

2. Когда **ForwardClientCertificate** задано слишком**true**, обратный прокси-сервер запрашивает сертификат клиента hello во время SSL-подтверждения с клиентом hello.
Он затем пересылает hello клиента данные сертификата в заголовок HTTP с именем **сертификат клиента X**. значение заголовка Hello является строка формата PEM hello в кодировке base64 сертификата клиента hello. Hello службы может завершиться успешно или неудача hello запрос на соответствующий код состояния после проверки данных сертификата hello.
Если hello клиента нет сертификата, обратный прокси-сервер пересылает пустой заголовок и позволить случай hello дескриптор службы hello.

> Обратный прокси-сервер является простым сервером пересылки. Он не будет выполнять проверку сертификата клиента hello.


## <a name="next-steps"></a>Дальнейшие действия
* См. слишком[настроить службы toosecure tooconnect обратного прокси-сервера](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) для диспетчера ресурсов Azure шаблона образцы tooconfigure безопасного обратного прокси-сервера с параметрами проверки сертификата другую службу hello.
* Пример обмена данными по протоколу HTTP между службами представлен в [примере проекта на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Удаленное взаимодействие службы с Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [Начало работы со службами веб-API Microsoft Azure Service Fabric с саморазмещением OWIN](service-fabric-reliable-services-communication-webapi.md)
* [Управление сертификатами кластера](service-fabric-cluster-security-update-certs-azure.md)
