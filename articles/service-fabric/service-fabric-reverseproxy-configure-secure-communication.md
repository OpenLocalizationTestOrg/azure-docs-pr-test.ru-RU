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
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="6066a-103">Служба безопасного tooa соединены hello обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="6066a-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="6066a-104">В этой статье объясняется, как tooestablish безопасное подключение между hello обратного прокси-сервера и служб, позволяя окончания tooend безопасного канала.</span><span class="sxs-lookup"><span data-stu-id="6066a-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="6066a-105">Соединение toosecure службы поддерживается только в том случае, если обратный прокси-сервер является toolisten, настроенных на HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6066a-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="6066a-106">Hello документе предполагается, что это случай hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="6066a-107">См. слишком[обратный прокси-сервер в Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello обратного прокси-сервера в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6066a-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="6066a-108">Установление безопасного соединения между hello обратного прокси-сервера и служб</span><span class="sxs-lookup"><span data-stu-id="6066a-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="6066a-109">Обратный прокси-сервер проверки подлинности tooservices:</span><span class="sxs-lookup"><span data-stu-id="6066a-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="6066a-110">Hello обратный прокси-сервер должен идентифицировать себя с использованием его сертификата, заданного с tooservices ***reverseProxyCertificate*** свойство в hello **кластера** [разделе типа ресурсов](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6066a-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="6066a-111">Службы могут реализовывать hello логику tooverify hello сертификат hello обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6066a-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="6066a-112">Hello службы могут указывать сведения о сертификате клиента hello принимается как параметры конфигурации в пакете конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="6066a-113">Это могут быть прочитаны во время выполнения и использовать toovalidate hello сертификат hello обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6066a-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="6066a-114">См. слишком[Управление параметрами приложения](service-fabric-manage-multiple-environment-app-configuration.md) параметры конфигурации tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="6066a-115">Обратный прокси-сервер, проверка удостоверения службы hello через hello сертификата, предоставленного службой hello:</span><span class="sxs-lookup"><span data-stu-id="6066a-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="6066a-116">Проверка сертификата сервера tooperform представленных hello служб сертификатов hello, обратного прокси-сервера поддерживает один из следующих вариантов hello: None, ServiceCommonNameAndIssuer и ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="6066a-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="6066a-117">один из этих трех параметров tooselect укажите hello **ApplicationCertificateValidationPolicy** в разделе параметров hello элемента шлюза приложения/Http в [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="6066a-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="6066a-118">См. в следующем разделе toohello подробные сведения о дополнительной настройке для каждого из этих параметров.</span><span class="sxs-lookup"><span data-stu-id="6066a-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="6066a-119">Параметры проверки сертификата службы</span><span class="sxs-lookup"><span data-stu-id="6066a-119">Service certificate validation options</span></span> 

- <span data-ttu-id="6066a-120">**Нет**: обратного прокси-сервера пропускает проверку сертификатов прокси службы hello и устанавливает безопасное соединение hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="6066a-121">Это поведение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-121">This is hello default behavior.</span></span>
<span data-ttu-id="6066a-122">Укажите hello **ApplicationCertificateValidationPolicy** со значением **нет** в разделе параметров hello элемента шлюза приложения/Http.</span><span class="sxs-lookup"><span data-stu-id="6066a-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="6066a-123">**ServiceCommonNameAndIssuer**: обратный прокси-сервер проверяет hello сертификат, представленный hello службы на основании общее имя сертификата и отпечаток немедленно издателя: укажите hello **ApplicationCertificateValidationPolicy**  со значением **ServiceCommonNameAndIssuer** в разделе параметров hello элемента шлюза приложения/Http.</span><span class="sxs-lookup"><span data-stu-id="6066a-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="6066a-124">Список toospecify hello общее имя службы и отпечатки издателя, добавьте **шлюза приложения, Http или ServiceCommonNameAndIssuer** элемента под fabricSettings, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6066a-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="6066a-125">В элементе массива параметров hello можно добавить несколько пар отпечаток издателя и общее имя сертификата.</span><span class="sxs-lookup"><span data-stu-id="6066a-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="6066a-126">Если обратный прокси-сервер hello конечной точки подключается toopresents сертификат, который обычно имя и издатель отпечаток соответствует любому из hello значения, указанные здесь, устанавливается канал SSL.</span><span class="sxs-lookup"><span data-stu-id="6066a-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="6066a-127">После toomatch hello сертификат подробные сведения об ошибках обратного прокси-сервера не выполняется hello клиентский запрос с кодом состояния 502 (Неверный шлюз).</span><span class="sxs-lookup"><span data-stu-id="6066a-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="6066a-128">Строка состояния HTTP Hello также будет содержать hello фразу «Недопустимый сертификат SSL».</span><span class="sxs-lookup"><span data-stu-id="6066a-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="6066a-129">**ServiceCertificateThumbprints**: обратный прокси-сервер будет проверять hello прокси службы сертификат, основанный на его отпечаток.</span><span class="sxs-lookup"><span data-stu-id="6066a-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="6066a-130">Вы можете выбрать toogo этот маршрут при hello службы должны быть настроены самозаверяющие сертификаты: укажите hello **ApplicationCertificateValidationPolicy** со значением **ServiceCertificateThumbprints**в разделе параметров hello элемента шлюза приложения/Http.</span><span class="sxs-lookup"><span data-stu-id="6066a-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="6066a-131">Также укажите отпечатки hello с **ServiceCertificateThumbprints** параметры в разделе элемента шлюза приложения/Http.</span><span class="sxs-lookup"><span data-stu-id="6066a-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="6066a-132">Несколько отпечатки можно указать как список разделенных запятыми, в поле значение hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="6066a-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

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

<span data-ttu-id="6066a-133">Если отпечаток сертификата сервера hello hello указан в этой записи конфигурации, обратного прокси-сервера успешно hello SSL-подключение.</span><span class="sxs-lookup"><span data-stu-id="6066a-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="6066a-134">В противном случае он завершает соединение hello и происходит сбой hello запрос клиента с 502 (Неверный шлюз).</span><span class="sxs-lookup"><span data-stu-id="6066a-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="6066a-135">Строка состояния HTTP Hello также будет содержать hello фразу «Недопустимый сертификат SSL».</span><span class="sxs-lookup"><span data-stu-id="6066a-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="6066a-136">Логика выбора конечной точки, когда службы предоставляют защищенные и незащищенные конечные точки</span><span class="sxs-lookup"><span data-stu-id="6066a-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="6066a-137">Service Fabric поддерживает настройку нескольких конечных точек для службы.</span><span class="sxs-lookup"><span data-stu-id="6066a-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="6066a-138">См. [Указание ресурсов в манифесте службы](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6066a-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="6066a-139">Обратный прокси-сервер выбирает одну из hello hello конечные точки tooforward запрос в зависимости от hello **ListenerName** параметр запроса.</span><span class="sxs-lookup"><span data-stu-id="6066a-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="6066a-140">Если этот параметр не указан, его можно выбрать любой конечной точки из списка конечных точек hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="6066a-141">Это может быть конечная точка HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6066a-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="6066a-142">Возможно, сценариев и требований место toooperate hello обратного прокси-сервера в «только режиме безопасности», т. е.</span><span class="sxs-lookup"><span data-stu-id="6066a-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="6066a-143">Вы не хотите hello безопасного обратного прокси-сервера tooforward запросов toounsecured конечных точек.</span><span class="sxs-lookup"><span data-stu-id="6066a-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="6066a-144">Это можно сделать, указав hello **SecureOnlyMode** запись конфигурации со значением **true** в разделе параметров hello элемента шлюза приложения/Http.</span><span class="sxs-lookup"><span data-stu-id="6066a-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="6066a-145">При работе в **SecureOnlyMode**, если клиент указал **ListenerName** соответствующая конечная точка HTTP(unsecured) tooan, hello запрос с кодом состояния 404 (не найдено) HTTP завершается ошибкой обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6066a-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="6066a-146">Настройка проверки подлинности сертификата клиента через обратный прокси-сервер hello</span><span class="sxs-lookup"><span data-stu-id="6066a-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="6066a-147">Завершение запросов SSL осуществляется по hello обратный прокси-сервер и все данные сертификата клиента hello будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="6066a-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="6066a-148">Для hello служб tooperform сертификат проверки подлинности клиента, задайте hello **ForwardClientCertificate** в разделе параметров hello элемента шлюза приложения/Http.</span><span class="sxs-lookup"><span data-stu-id="6066a-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="6066a-149">При **ForwardClientCertificate** задано слишком**false**, обратного прокси-сервера не будет запрашиваться для сертификата клиента hello во время SSL-подтверждения с клиентом hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="6066a-150">Это поведение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="6066a-151">Когда **ForwardClientCertificate** задано слишком**true**, обратный прокси-сервер запрашивает сертификат клиента hello во время SSL-подтверждения с клиентом hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="6066a-152">Он затем пересылает hello клиента данные сертификата в заголовок HTTP с именем **сертификат клиента X**.</span><span class="sxs-lookup"><span data-stu-id="6066a-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="6066a-153">значение заголовка Hello является строка формата PEM hello в кодировке base64 сертификата клиента hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="6066a-154">Hello службы может завершиться успешно или неудача hello запрос на соответствующий код состояния после проверки данных сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="6066a-155">Если hello клиента нет сертификата, обратный прокси-сервер пересылает пустой заголовок и позволить случай hello дескриптор службы hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="6066a-156">Обратный прокси-сервер является простым сервером пересылки.</span><span class="sxs-lookup"><span data-stu-id="6066a-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="6066a-157">Он не будет выполнять проверку сертификата клиента hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6066a-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6066a-158">Next steps</span></span>
* <span data-ttu-id="6066a-159">См. слишком[настроить службы toosecure tooconnect обратного прокси-сервера](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) для диспетчера ресурсов Azure шаблона образцы tooconfigure безопасного обратного прокси-сервера с параметрами проверки сертификата другую службу hello.</span><span class="sxs-lookup"><span data-stu-id="6066a-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="6066a-160">Пример обмена данными по протоколу HTTP между службами представлен в [примере проекта на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="6066a-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="6066a-161">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6066a-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="6066a-162">Начало работы со службами веб-API Microsoft Azure Service Fabric с саморазмещением OWIN</span><span class="sxs-lookup"><span data-stu-id="6066a-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="6066a-163">Управление сертификатами кластера</span><span class="sxs-lookup"><span data-stu-id="6066a-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
