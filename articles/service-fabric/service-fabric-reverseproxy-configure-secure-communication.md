---
title: "Защищенное взаимодействие с обратным прокси-сервером Azure Service Fabric | Документы Майкрософт"
description: "Настройка обратного прокси-сервера для обеспечения безопасного сквозного взаимодействия."
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
ms.openlocfilehash: 568f9638c59282bcd7d3fae058a1588a889c22dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a><span data-ttu-id="fc826-103">Подключение к защищенной службе с помощью обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="fc826-103">Connect to a secure service with the reverse proxy</span></span>

<span data-ttu-id="fc826-104">В этой статье объясняется, как установить безопасное подключение между обратным прокси-сервером и службами, которое будет использоваться в качестве защищенного сквозного канала.</span><span class="sxs-lookup"><span data-stu-id="fc826-104">This article explains how to establish secure connection between the reverse proxy and services, thus enabling an end to end secure channel.</span></span>

<span data-ttu-id="fc826-105">Подключение к защищенным службам поддерживается, только если обратный прокси-сервер настроен для прослушивания по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fc826-105">Connecting to secure services is supported only when reverse proxy is configured to listen on HTTPS.</span></span> <span data-ttu-id="fc826-106">В остальной части документа предполагается, что это так.</span><span class="sxs-lookup"><span data-stu-id="fc826-106">Rest of the document assumes this is the case.</span></span>
<span data-ttu-id="fc826-107">Сведения о настройке обратного прокси-сервера Service Fabric см. в статье [Обратный прокси-сервер в Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="fc826-107">Refer to [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) to configure the reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a><span data-ttu-id="fc826-108">Установление безопасного подключения между обратным прокси-сервером и службами</span><span class="sxs-lookup"><span data-stu-id="fc826-108">Secure connection establishment between the reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-to-services"></a><span data-ttu-id="fc826-109">Обратный прокси-сервер проходит аутентификацию в службах</span><span class="sxs-lookup"><span data-stu-id="fc826-109">Reverse proxy authenticating to services:</span></span>
<span data-ttu-id="fc826-110">Обратный прокси-сервер должен идентифицировать себя в службах с помощью сертификата, заданного свойством ***reverseProxyCertificate*** в [разделе "Тип ресурса"](../azure-resource-manager/resource-group-authoring-templates.md) **кластера**.</span><span class="sxs-lookup"><span data-stu-id="fc826-110">The reverse proxy identifies itself to services using its certificate, specified with ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="fc826-111">Службы могут реализовать логику для проверки сертификата, представленного обратным прокси-сервером.</span><span class="sxs-lookup"><span data-stu-id="fc826-111">Services can implement the logic to verify the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="fc826-112">Службы могут указывать сведения о принятом сертификате клиента как параметры конфигурации в пакете конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fc826-112">The services can specify the accepted client certificate details as configuration settings in the configuration package.</span></span> <span data-ttu-id="fc826-113">Их можно считывать во время выполнения и использовать для проверки сертификата, представленного обратным прокси-сервером.</span><span class="sxs-lookup"><span data-stu-id="fc826-113">This can be read at runtime and used to validate the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="fc826-114">Сведения о добавлении параметров конфигурации см. в статье [Управление параметрами приложения](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="fc826-114">Refer to [Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) to add the configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a><span data-ttu-id="fc826-115">Проверка обратным прокси-сервером удостоверения службы с помощью сертификата, предоставленного службой</span><span class="sxs-lookup"><span data-stu-id="fc826-115">Reverse proxy verifying the service's identity via the certificate presented by the service:</span></span>
<span data-ttu-id="fc826-116">Для выполнения проверки сертификатов, представленных службами, обратный прокси-сервер поддерживает один из следующих параметров: None, ServiceCommonNameAndIssuer и ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="fc826-116">To perform server certificate validation of the certificates presented by the services, reverse proxy supports one of the following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="fc826-117">Чтобы выбрать один из этих трех параметров, задайте свойство **ApplicationCertificateValidationPolicy** в разделе параметров элемента ApplicationGateway/Http в [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="fc826-117">To select one of these three options, specify the **ApplicationCertificateValidationPolicy** in the parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="fc826-118">Сведения о дополнительной настройке для каждого из этих параметров см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="fc826-118">Refer to the next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="fc826-119">Параметры проверки сертификата службы</span><span class="sxs-lookup"><span data-stu-id="fc826-119">Service certificate validation options</span></span> 

- <span data-ttu-id="fc826-120">**None**: обратный прокси-сервер пропускает проверку сертификата службы, подключаемой через прокси-сервер, и устанавливает безопасное подключение.</span><span class="sxs-lookup"><span data-stu-id="fc826-120">**None**: Reverse proxy skips verification of the proxied service certificate and establishes the secure connection.</span></span> <span data-ttu-id="fc826-121">Это поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fc826-121">This is the default behavior.</span></span>
<span data-ttu-id="fc826-122">Задайте для свойства **ApplicationCertificateValidationPolicy** значение **None** в разделе параметров элемента ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="fc826-122">Specify the **ApplicationCertificateValidationPolicy** with value **None** in the parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="fc826-123">**ServiceCommonNameAndIssuer**: обратный прокси-сервер проверяет сертификат, представленный службой, на основании общего имени сертификата и отпечатка непосредственного издателя. Задайте для свойства **ApplicationCertificateValidationPolicy** значение **ServiceCommonNameAndIssuer** в разделе параметров элемента ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="fc826-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies the certificate presented by the service based on certificate's common name and immediate issuer's thumbprint: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="fc826-124">Чтобы указать список общих имен служб и отпечатков издателей, добавьте элемент **ApplicationGateway/Http/ServiceCommonNameAndIssuer** в раздел fabricSettings, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fc826-124">To specify the list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="fc826-125">В элемент массива параметров можно добавить несколько пар общих имен сертификатов и отпечатков издателей.</span><span class="sxs-lookup"><span data-stu-id="fc826-125">Multiple certificate common name and issuer thumbprint pairs can be added in the parameters array element.</span></span> 

<span data-ttu-id="fc826-126">Если обратный прокси-сервер конечной точки подключается для представления сертификата, общее имя и отпечаток издателя которого соответствуют любому из указанных в элементе значений, устанавливается SSL-канал.</span><span class="sxs-lookup"><span data-stu-id="fc826-126">If the endpoint reverse proxy is connecting to presents a certificate who's common name and  issuer thumbprint matches any of the values specified here, SSL channel is established.</span></span> <span data-ttu-id="fc826-127">Если соответствие для сведений о сертификате не найдено, обратный прокси-сервер не выполняет запрос клиента с кодом состояния 502 (неверный шлюз).</span><span class="sxs-lookup"><span data-stu-id="fc826-127">Upon failure to match the certificate details, reverse proxy fails the client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="fc826-128">В строке состояния HTTP также будет содержаться фраза "Недопустимый сертификат SSL".</span><span class="sxs-lookup"><span data-stu-id="fc826-128">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="fc826-129">**ServiceCertificateThumbprints**: обратный прокси-сервер будет проверять сертификат службы на основе отпечатка.</span><span class="sxs-lookup"><span data-stu-id="fc826-129">**ServiceCertificateThumbprints**: Reverse proxy will verify the proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="fc826-130">Вы можете выбрать этот вариант, если для служб настроены самозаверяющие сертификаты: задайте для свойства **ApplicationCertificateValidationPolicy** значение **ServiceCertificateThumbprints** в разделе параметров элемента ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="fc826-130">You can choose to go this route when the services are configured with self signed certificates: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="fc826-131">Также укажите отпечатки с помощью записи **ServiceCertificateThumbprints** в разделе параметров элемента ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="fc826-131">Also specify the thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="fc826-132">Можно указать несколько отпечатков в виде списка с разделителями-запятыми в поле значения, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="fc826-132">Multiple thumbprints can be specified as a comma-separated list in the value field, as shown below:</span></span>

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

<span data-ttu-id="fc826-133">Если отпечаток сертификата сервера содержится в этой записи конфигурации, обратный прокси-сервер успешно устанавливает SSL-подключение.</span><span class="sxs-lookup"><span data-stu-id="fc826-133">If the thumbprint of the server certificate is listed in this config entry, reverse proxy succeeds the SSL connection.</span></span> <span data-ttu-id="fc826-134">В противном случае — он завершает подключение и не выполняет запроса клиента с ошибкой 502 (неверный шлюз).</span><span class="sxs-lookup"><span data-stu-id="fc826-134">Otherwise, it terminates the connection and fails the client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="fc826-135">В строке состояния HTTP также будет содержаться фраза "Недопустимый сертификат SSL".</span><span class="sxs-lookup"><span data-stu-id="fc826-135">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="fc826-136">Логика выбора конечной точки, когда службы предоставляют защищенные и незащищенные конечные точки</span><span class="sxs-lookup"><span data-stu-id="fc826-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="fc826-137">Service Fabric поддерживает настройку нескольких конечных точек для службы.</span><span class="sxs-lookup"><span data-stu-id="fc826-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="fc826-138">См. [Указание ресурсов в манифесте службы](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fc826-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="fc826-139">Обратный прокси-сервер выбирает одну из конечных точек для пересылки запросов в зависимости от значения параметра запроса **ListenerName**.</span><span class="sxs-lookup"><span data-stu-id="fc826-139">Reverse proxy selects one of the endpoints to forward the request based on the  **ListenerName** query parameter.</span></span> <span data-ttu-id="fc826-140">Если этот параметр не указан, сервер может выбрать любую конечную точку из списка конечных точек.</span><span class="sxs-lookup"><span data-stu-id="fc826-140">If this is not specified, it can pick any endpoint from the endpoints list.</span></span> <span data-ttu-id="fc826-141">Это может быть конечная точка HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fc826-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="fc826-142">Существует ряд сценариев и требований, когда обратный прокси-сервер должен работать "только в безопасном режиме", т. е.</span><span class="sxs-lookup"><span data-stu-id="fc826-142">There might be scenarios/requirements where you want the reverse proxy to operate in a "secure only mode", i.e</span></span> <span data-ttu-id="fc826-143">защищенный обратный прокси-сервер не должен пересылать запросы в незащищенные конечные точки.</span><span class="sxs-lookup"><span data-stu-id="fc826-143">you don't want the secure reverse proxy to forward requests to unsecured endpoints.</span></span> <span data-ttu-id="fc826-144">Это можно сделать, указав запись конфигурации **SecureOnlyMode** со значением **true** в разделе параметров элемента ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="fc826-144">This can be achieved by specifying the **SecureOnlyMode** configuration entry with value **true** in the parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="fc826-145">При работе в режиме **SecureOnlyMode**, если клиент указал значение **ListenerName**, соответствующее конечной точке HTTP (незащищенной), обратный прокси-сервер не выполняет запрос с кодом состояния HTTP 404 (не найдено).</span><span class="sxs-lookup"><span data-stu-id="fc826-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding to an HTTP(unsecured) endpoint, reverse proxy fails the request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a><span data-ttu-id="fc826-146">Настройка проверки подлинности сертификата клиента через обратный прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="fc826-146">Setting up client certificate authentication through the reverse proxy</span></span>
<span data-ttu-id="fc826-147">Разрыв SSL-подключения выполняется на обратном прокси-сервере, и все данные сертификата клиента утрачиваются.</span><span class="sxs-lookup"><span data-stu-id="fc826-147">SSL termination happens at the reverse proxy and all the client certificate data is lost.</span></span> <span data-ttu-id="fc826-148">Чтобы службы могли выполнять проверку подлинности сертификата клиента, задайте параметр **ForwardClientCertificate** в разделе параметров элемента ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="fc826-148">For the services to perform client certificate authentication, set the **ForwardClientCertificate** setting in the parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="fc826-149">Если для параметра **ForwardClientCertificate** задано значение **false**, обратный прокси-сервер не будет запрашивать сертификат клиента во время подтверждения SSL.</span><span class="sxs-lookup"><span data-stu-id="fc826-149">When **ForwardClientCertificate** is set to **false**, reverse proxy will not request for the client certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="fc826-150">Это поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fc826-150">This is the default behavior.</span></span>

2. <span data-ttu-id="fc826-151">Если для параметра **ForwardClientCertificate** задано значение **true**, обратный прокси-сервер запрашивает сертификат клиента во время подтверждения SSL.</span><span class="sxs-lookup"><span data-stu-id="fc826-151">When **ForwardClientCertificate** is set to **true**, reverse proxy requests for the client's certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="fc826-152">Затем он пересылает данные сертификата клиента в пользовательский заголовок HTTP с именем **X-Client-Certificate**.</span><span class="sxs-lookup"><span data-stu-id="fc826-152">It will then forward the client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="fc826-153">Значение заголовка является строкой формата PEM в кодировке base64 сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="fc826-153">The header value is the base64 encoded PEM format string of the client's certificate.</span></span> <span data-ttu-id="fc826-154">Служба может успешно или неудачно выполнить запрос с соответствующим кодом состояния после проверки данных сертификата.</span><span class="sxs-lookup"><span data-stu-id="fc826-154">The service can succeed/fail the request with appropriate status code after inspecting the certificate data.</span></span>
<span data-ttu-id="fc826-155">Если клиент не представляет сертификат, обратный прокси-сервер пересылает пустой заголовок и передает принятие решения службе.</span><span class="sxs-lookup"><span data-stu-id="fc826-155">If the client does not present a certificate, reverse proxy forwards an empty header and let the service handle the case.</span></span>

> <span data-ttu-id="fc826-156">Обратный прокси-сервер является простым сервером пересылки.</span><span class="sxs-lookup"><span data-stu-id="fc826-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="fc826-157">Он не выполняет проверку сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="fc826-157">It will not perform any validation of the client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fc826-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc826-158">Next steps</span></span>
* <span data-ttu-id="fc826-159">Примеры шаблонов Azure Resource Manager для настройки разных параметров проверки сертификата службы для защищенного обратного прокси-сервера см. в разделе [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services).</span><span class="sxs-lookup"><span data-stu-id="fc826-159">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="fc826-160">Пример обмена данными по протоколу HTTP между службами представлен в [примере проекта на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="fc826-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="fc826-161">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="fc826-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="fc826-162">Начало работы со службами веб-API Microsoft Azure Service Fabric с саморазмещением OWIN</span><span class="sxs-lookup"><span data-stu-id="fc826-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="fc826-163">Управление сертификатами кластера</span><span class="sxs-lookup"><span data-stu-id="fc826-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
