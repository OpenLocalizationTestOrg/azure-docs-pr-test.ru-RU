---
title: "Общие сведения о безопасности в Центре Интернета вещей Azure | Документация Майкрософт"
description: "Руководство разработчика. Управление доступом к Центру Интернета вещей для внутренних приложений или приложений для устройств. Содержит сведения о маркерах безопасности и поддержке сертификатов X.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e4fe5400ffcf4446392015aada031dd4dfbf238a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="control-access-to-iot-hub"></a><span data-ttu-id="6212a-104">Управление доступом к Центру Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="6212a-104">Control access to IoT Hub</span></span>

<span data-ttu-id="6212a-105">В этой статье описаны возможности защиты Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-105">This article describes the options for securing your IoT hub.</span></span> <span data-ttu-id="6212a-106">Центр Интернета вещей использует *разрешения* для предоставления доступа к каждой из своих конечных точек.</span><span class="sxs-lookup"><span data-stu-id="6212a-106">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span></span> <span data-ttu-id="6212a-107">Разрешения ограничивают доступ к Центру Интернета вещей на основе функций.</span><span class="sxs-lookup"><span data-stu-id="6212a-107">Permissions limit the access to an IoT hub based on functionality.</span></span>

<span data-ttu-id="6212a-108">Содержание статьи</span><span class="sxs-lookup"><span data-stu-id="6212a-108">This article describes:</span></span>

* <span data-ttu-id="6212a-109">Различные разрешения, которые можно предоставить устройству или серверному приложению для доступа к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-109">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span></span>
* <span data-ttu-id="6212a-110">Процесс аутентификации и маркеры, используемые для проверки разрешений.</span><span class="sxs-lookup"><span data-stu-id="6212a-110">The authentication process and the tokens it uses to verify permissions.</span></span>
* <span data-ttu-id="6212a-111">Определение области действия учетных данных для ограничения доступа к определенным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="6212a-111">How to scope credentials to limit access to specific resources.</span></span>
* <span data-ttu-id="6212a-112">Поддержка сертификатов X.509 в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="6212a-113">Механизмы настраиваемой аутентификации устройства, использующие существующие реестры удостоверений устройств или схемы аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6212a-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="6212a-114">Сценарии использования</span><span class="sxs-lookup"><span data-stu-id="6212a-114">When to use</span></span>

<span data-ttu-id="6212a-115">Для доступа к любой конечной точке Центра Интернета вещей необходимы соответствующие разрешения.</span><span class="sxs-lookup"><span data-stu-id="6212a-115">You must have appropriate permissions to access any of the IoT Hub endpoints.</span></span> <span data-ttu-id="6212a-116">Например, устройство должно содержать маркер с учетными данными безопасности, а также все сообщения, отправленные в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-116">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="6212a-117">Контроль доступа и разрешений</span><span class="sxs-lookup"><span data-stu-id="6212a-117">Access control and permissions</span></span>

<span data-ttu-id="6212a-118">Предоставить [разрешения](#iot-hub-permissions) можно следующими способами:</span><span class="sxs-lookup"><span data-stu-id="6212a-118">You can grant [permissions](#iot-hub-permissions) in the following ways:</span></span>

* <span data-ttu-id="6212a-119">**Политики общего доступа на уровне Центра Интернета вещей**.</span><span class="sxs-lookup"><span data-stu-id="6212a-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="6212a-120">Политики общего доступа могут предоставлять любое сочетание [разрешений](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="6212a-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="6212a-121">Политики можно задавать на [портале Azure][lnk-management-portal] или программно, используя [интерфейсы REST API поставщика ресурсов Центра Интернета вещей][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="6212a-121">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="6212a-122">По умолчанию для только что созданного Центра Интернета вещей заданы такие политики:</span><span class="sxs-lookup"><span data-stu-id="6212a-122">A newly created IoT hub has the following default policies:</span></span>

  * <span data-ttu-id="6212a-123">**iothubowner**: политика со всеми разрешениями;</span><span class="sxs-lookup"><span data-stu-id="6212a-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="6212a-124">**service**: политика с разрешением **ServiceConnect**;</span><span class="sxs-lookup"><span data-stu-id="6212a-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="6212a-125">**device**: политика с разрешением **DeviceConnect**;</span><span class="sxs-lookup"><span data-stu-id="6212a-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="6212a-126">**registryRead**: политика с разрешением **RegistryRead**;</span><span class="sxs-lookup"><span data-stu-id="6212a-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="6212a-127">**registryReadWrite**: политика с разрешениями **RegistryRead** и RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="6212a-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="6212a-128">**Учетные данные безопасности на уровне отдельного устройства**.</span><span class="sxs-lookup"><span data-stu-id="6212a-128">**Per-device security credentials**.</span></span> <span data-ttu-id="6212a-129">Каждый Центр Интернета вещей содержит [реестр удостоверений][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="6212a-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="6212a-130">Для каждого устройства в этом реестре удостоверений вы можете задать учетные данные безопасности, дающие вам разрешения **DeviceConnect**, которые соответствуют конечным точкам устройств.</span><span class="sxs-lookup"><span data-stu-id="6212a-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span></span>

<span data-ttu-id="6212a-131">Например, в стандартном решении IoT:</span><span class="sxs-lookup"><span data-stu-id="6212a-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="6212a-132">Компонент управления устройством использует политику *registryReadWrite* .</span><span class="sxs-lookup"><span data-stu-id="6212a-132">The device management component uses the *registryReadWrite* policy.</span></span>
* <span data-ttu-id="6212a-133">Компонент обработчика событий использует политику *service* .</span><span class="sxs-lookup"><span data-stu-id="6212a-133">The event processor component uses the *service* policy.</span></span>
* <span data-ttu-id="6212a-134">Компонент бизнес-логики устройства среды выполнения использует политику *service*.</span><span class="sxs-lookup"><span data-stu-id="6212a-134">The run-time device business logic component uses the *service* policy.</span></span>
* <span data-ttu-id="6212a-135">Отдельные устройства подключаются с помощью учетных данных, которые хранятся в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-135">Individual devices connect using credentials stored in the IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="6212a-136">Дополнительные сведения см. в статье о [разрешениях](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="6212a-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="6212a-137">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="6212a-137">Authentication</span></span>

<span data-ttu-id="6212a-138">Центр Интернета вещей Azure предоставляет доступ к конечным точкам, проверяя маркер на соответствие политикам общего доступа и учетным данным безопасности в реестре удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6212a-138">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="6212a-139">Учетные данные безопасности, например симметричные ключи, никогда не отправляются по сети.</span><span class="sxs-lookup"><span data-stu-id="6212a-139">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="6212a-140">Безопасность для поставщика ресурсов Центра Интернета вещей Azure обеспечивается с помощью подписки Azure (это касается всех поставщиков в [Azure Resource Manager][lnk-azure-resource-manager]).</span><span class="sxs-lookup"><span data-stu-id="6212a-140">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="6212a-141">Дополнительные сведения о способах создания и использования маркеров безопасности см. в разделе [Маркеры безопасности Центра Интернета вещей][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="6212a-141">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="6212a-142">Особенности протокола</span><span class="sxs-lookup"><span data-stu-id="6212a-142">Protocol specifics</span></span>

<span data-ttu-id="6212a-143">Каждый поддерживаемый протокол, например MQTT, AMQP и HTTP, передает маркеры разными способами.</span><span class="sxs-lookup"><span data-stu-id="6212a-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="6212a-144">При использовании протокола MQTT пакет CONNECT содержит код deviceId как значение ClientId, {iothubhostname}/{deviceId} в поле "Имя пользователя", а маркер SAS — в поле "Пароль".</span><span class="sxs-lookup"><span data-stu-id="6212a-144">When using MQTT, the CONNECT packet has the deviceId as the ClientId, {iothubhostname}/{deviceId} in the Username field, and a SAS token in the Password field.</span></span> <span data-ttu-id="6212a-145">{iothubhostname} — это полная запись CName Центра Интернета вещей (например, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="6212a-145">{iothubhostname} should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="6212a-146">При использовании [AMQP][lnk-amqp] Центр Интернета вещей поддерживает механизм [SASL PLAIN][lnk-sasl-plain] и стандарт [защиты AMQP на основе утверждений][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="6212a-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="6212a-147">Стандарт защиты AMQP на основе утверждений определяет, как следует передавать эти маркеры.</span><span class="sxs-lookup"><span data-stu-id="6212a-147">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span></span>

<span data-ttu-id="6212a-148">Для SASL PLAIN **имя пользователя** может быть следующим:</span><span class="sxs-lookup"><span data-stu-id="6212a-148">For SASL PLAIN, the **username** can be:</span></span>

* <span data-ttu-id="6212a-149">`{policyName}@sas.root.{iothubName}` — при использовании маркеров уровня Центра Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="6212a-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="6212a-150">`{deviceId}@sas.{iothubname}` — при использовании маркеров уровня устройства.</span><span class="sxs-lookup"><span data-stu-id="6212a-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="6212a-151">В обоих случаях поле пароля содержит маркер, как описано в разделе [Маркеры безопасности Центра Интернета вещей][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="6212a-151">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="6212a-152">Протокол HTTP реализует аутентификацию посредством включения допустимого маркера в заголовок запроса **авторизации** .</span><span class="sxs-lookup"><span data-stu-id="6212a-152">HTTP implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="6212a-153">Пример</span><span class="sxs-lookup"><span data-stu-id="6212a-153">Example</span></span>

<span data-ttu-id="6212a-154">Имя пользователя (значение DeviceId следует вводить с учетом регистра): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="6212a-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="6212a-155">Пароль (создайте маркер SAS с помощью [обозревателя устройств][lnk-device-explorer]): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="6212a-155">Password (Generate SAS token with the [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="6212a-156">[Пакеты SDK для Azure IoT][lnk-sdks] автоматически создают маркеры при подключении к службе.</span><span class="sxs-lookup"><span data-stu-id="6212a-156">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span> <span data-ttu-id="6212a-157">В некоторых случаях пакеты SDK для Azure IoT поддерживают не все протоколы или не все методы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6212a-157">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="6212a-158">Специальные рекомендации для SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="6212a-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="6212a-159">При использовании SASL PLAIN с протоколом AMQP клиент, подключающийся к Центру Интернета вещей, может использовать по одному маркеру для каждого TCP-подключения.</span><span class="sxs-lookup"><span data-stu-id="6212a-159">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="6212a-160">Когда срок действия маркера истекает, TCP-подключение к службе прерывается и выполняется попытка повторного подключения.</span><span class="sxs-lookup"><span data-stu-id="6212a-160">When the token expires, the TCP connection disconnects from the service and triggers a reconnect.</span></span> <span data-ttu-id="6212a-161">Хотя это поведение и не является проблематичным для внутреннего приложения, оно может навредить приложению для устройства по следующим причинам:</span><span class="sxs-lookup"><span data-stu-id="6212a-161">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span></span>

* <span data-ttu-id="6212a-162">Шлюзы обычно подключаются от имени многих устройств.</span><span class="sxs-lookup"><span data-stu-id="6212a-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="6212a-163">Если используется SASL PLAIN, шлюзам нужно создать отдельное TCP-подключение для каждого устройства, подключающегося к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-163">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span></span> <span data-ttu-id="6212a-164">Этот сценарий значительно повышает потребление электроэнергии и сетевых ресурсов и увеличивает задержку подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="6212a-164">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span></span>
* <span data-ttu-id="6212a-165">Если потребление ресурсов увеличится, устройства с ограниченными ресурсами должны будут выполнять повторное подключение после истечения срока действия маркера.</span><span class="sxs-lookup"><span data-stu-id="6212a-165">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="6212a-166">Определение области действия учетных данных на уровне Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="6212a-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="6212a-167">Чтобы определить область действия для политик безопасности на уровне Центра Интернета вещей, создайте маркеры с помощью универсального кода (URI) ограниченного ресурса.</span><span class="sxs-lookup"><span data-stu-id="6212a-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="6212a-168">Например, конечная точка для отправки сообщений с устройства в облако — **/devices/{deviceId}/messages/events**.</span><span class="sxs-lookup"><span data-stu-id="6212a-168">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="6212a-169">Кроме того, вы можете использовать политику общего доступа на уровне Центра Интернета вещей с разрешениями **DeviceConnect**. С ее помощью можно подписать маркер, значение resourceURI которого — **/devices/{deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="6212a-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="6212a-170">В результате такого подхода создается маркер, который можно использовать только для отправки сообщений от имени устройства с кодом **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="6212a-170">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="6212a-171">Этот механизм похож на [политику издателя концентраторов событий][lnk-event-hubs-publisher-policy]. Он позволяет реализовывать методы настраиваемой проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6212a-171">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="6212a-172">Маркеры безопасности Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="6212a-172">Security tokens</span></span>

<span data-ttu-id="6212a-173">Центр Интернета вещей использует маркеры безопасности для проверки подлинности устройств и служб, чтобы избежать отправки ключей по сети.</span><span class="sxs-lookup"><span data-stu-id="6212a-173">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span></span> <span data-ttu-id="6212a-174">Кроме того, маркеры безопасности ограничены по времени и области действия.</span><span class="sxs-lookup"><span data-stu-id="6212a-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="6212a-175">[Пакеты SDK для Azure IoT][lnk-sdks] автоматически создают маркеры без специальной настройки.</span><span class="sxs-lookup"><span data-stu-id="6212a-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="6212a-176">В некоторых случаях требуется напрямую создать и использовать маркеры безопасности.</span><span class="sxs-lookup"><span data-stu-id="6212a-176">Some scenarios do require you to generate and use security tokens directly.</span></span> <span data-ttu-id="6212a-177">Ниже приведены соответствующие сценарии.</span><span class="sxs-lookup"><span data-stu-id="6212a-177">Such scenarios include:</span></span>

* <span data-ttu-id="6212a-178">Непосредственное использование поверхностей MQTT, AMQP или HTTP.</span><span class="sxs-lookup"><span data-stu-id="6212a-178">The direct use of the MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="6212a-179">Реализация схемы службы маркеров, как описано в разделе [Настраиваемая проверка подлинности устройства][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="6212a-179">The implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="6212a-180">Центр Интернета вещей также позволяет устройствам использовать [сертификаты X.509][lnk-x509] для аутентификации в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-180">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="6212a-181">Структура маркера безопасности</span><span class="sxs-lookup"><span data-stu-id="6212a-181">Security token structure</span></span>

<span data-ttu-id="6212a-182">Маркеры безопасности используются для предоставления устройствам и службам ограниченного по времени доступа к определенным функциям в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-182">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span></span> <span data-ttu-id="6212a-183">Чтобы получить авторизацию для подключения к Центру Интернета вещей, устройства и службы должны отправить маркеры безопасности, подписанные с помощью общего ключа доступа или симметричного ключа,</span><span class="sxs-lookup"><span data-stu-id="6212a-183">To get authorization to connect to IoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="6212a-184">сохраненного с удостоверением устройства в реестре удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6212a-184">These keys are stored with a device identity in the identity registry.</span></span>

<span data-ttu-id="6212a-185">Маркер, подписанный с помощью ключа общего доступа, предоставляет доступа ко всем функциям, связанным с разрешениями политики общего доступа.</span><span class="sxs-lookup"><span data-stu-id="6212a-185">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> <span data-ttu-id="6212a-186">Маркер, подписанный с помощью симметричного ключа удостоверения устройства, предоставляет только разрешение **DeviceConnect** для связанного удостоверения устройства.</span><span class="sxs-lookup"><span data-stu-id="6212a-186">A token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span></span>

<span data-ttu-id="6212a-187">Маркер безопасности имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="6212a-187">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="6212a-188">Это ожидаемые значения:</span><span class="sxs-lookup"><span data-stu-id="6212a-188">Here are the expected values:</span></span>

| <span data-ttu-id="6212a-189">Значение</span><span class="sxs-lookup"><span data-stu-id="6212a-189">Value</span></span> | <span data-ttu-id="6212a-190">Описание</span><span class="sxs-lookup"><span data-stu-id="6212a-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6212a-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="6212a-191">{signature}</span></span> |<span data-ttu-id="6212a-192">Строка подписи HMAC-SHA256 формата `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="6212a-192">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="6212a-193">**Важно!**Ключ шифруется в кодировке base64 и используется для вычислений HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="6212a-193">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="6212a-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="6212a-194">{resourceURI}</span></span> |<span data-ttu-id="6212a-195">Начинающийся с имени узла Центра Интернета вещей (без протокола) префикс URI (по сегменту) для конечных точек, доступ к которым можно получить с помощью этого маркера.</span><span class="sxs-lookup"><span data-stu-id="6212a-195">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span></span> <span data-ttu-id="6212a-196">Например, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="6212a-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="6212a-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="6212a-197">{expiry}</span></span> |<span data-ttu-id="6212a-198">Строки в формате UTF8, отображающие количество секунд с начала эры 00:00:00 (в формате UTC) 1 января 1970 г.</span><span class="sxs-lookup"><span data-stu-id="6212a-198">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="6212a-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="6212a-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="6212a-200">Строчное URL-кодирование строчного URL ресурса</span><span class="sxs-lookup"><span data-stu-id="6212a-200">Lower case URL-encoding of the lower case resource URI</span></span> |
| <span data-ttu-id="6212a-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="6212a-201">{policyName}</span></span> |<span data-ttu-id="6212a-202">Имя политики общего доступа, к которой относится этот маркер.</span><span class="sxs-lookup"><span data-stu-id="6212a-202">The name of the shared access policy to which this token refers.</span></span> <span data-ttu-id="6212a-203">Отсутствует, если маркер относится к учетным данным реестра устройства.</span><span class="sxs-lookup"><span data-stu-id="6212a-203">Absent if the token refers to device-registry credentials.</span></span> |

<span data-ttu-id="6212a-204">**Обратите внимание**, что префикс универсального кода ресурса (URI) вычисляется по сегменту, а не по символу.</span><span class="sxs-lookup"><span data-stu-id="6212a-204">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="6212a-205">Например, `/a/b` — это префикс для `/a/b/c`, а не для `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="6212a-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="6212a-206">В следующем фрагменте кода Node.js показан функция **generateSasToken**, которая вычисляет маркер, используя входные данные`resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="6212a-206">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="6212a-207">В следующих разделах показано, как инициализировать различные входные данные для различных сценариев использования маркеров.</span><span class="sxs-lookup"><span data-stu-id="6212a-207">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="6212a-208">Для сравнения приведен эквивалентный код Python для создания маркера безопасности.</span><span class="sxs-lookup"><span data-stu-id="6212a-208">As a comparison, the equivalent Python code to generate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="6212a-209">Так как срок действия маркера проверяется на компьютерах Центра Интернета вещей, нужно обеспечить минимальное смещение на часах компьютера, где создается маркер.</span><span class="sxs-lookup"><span data-stu-id="6212a-209">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="6212a-210">Использование маркеров SAS в приложении для устройства</span><span class="sxs-lookup"><span data-stu-id="6212a-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="6212a-211">Существует два способа получения разрешений **DeviceConnect** для Центра Интернета вещей с маркерами безопасности: с помощью [симметричного ключа устройства из реестра удостоверений](#use-a-symmetric-key-in-the-identity-registry) или [ключа общего доступа](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="6212a-211">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="6212a-212">Помните, что все функциональные возможности, доступные с устройств, намеренно предоставляются в конечных точках с префиксом `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="6212a-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6212a-213">Единственный способ проверки подлинности конкретного устройства в Центре Интернета вещей предполагает использование симметричного ключа удостоверения устройства.</span><span class="sxs-lookup"><span data-stu-id="6212a-213">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span></span> <span data-ttu-id="6212a-214">В случаях, когда для доступа к функциям устройства применяется политика общего доступа, решение должно считать компонент, который выдает маркер безопасности, доверенным компонентом.</span><span class="sxs-lookup"><span data-stu-id="6212a-214">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span></span>

<span data-ttu-id="6212a-215">Далее указаны конечные точки, доступные с устройства (вне зависимости от протокола).</span><span class="sxs-lookup"><span data-stu-id="6212a-215">The device-facing endpoints are (irrespective of the protocol):</span></span>

| <span data-ttu-id="6212a-216">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="6212a-216">Endpoint</span></span> | <span data-ttu-id="6212a-217">Функции</span><span class="sxs-lookup"><span data-stu-id="6212a-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="6212a-218">Отправка сообщений с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="6212a-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="6212a-219">Получение сообщений из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="6212a-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-the-identity-registry"></a><span data-ttu-id="6212a-220">Использование симметричного ключа в реестре удостоверений</span><span class="sxs-lookup"><span data-stu-id="6212a-220">Use a symmetric key in the identity registry</span></span>

<span data-ttu-id="6212a-221">Если для создания маркера используется симметричный ключ удостоверения устройства, то элемент policyName (`skn`) пропускается.</span><span class="sxs-lookup"><span data-stu-id="6212a-221">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span></span>

<span data-ttu-id="6212a-222">Например, маркер, созданный для доступа ко всем функциям устройства, должен иметь следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="6212a-222">For example, a token created to access all device functionality should have the following parameters:</span></span>

* <span data-ttu-id="6212a-223">универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices/{device id}`;</span><span class="sxs-lookup"><span data-stu-id="6212a-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="6212a-224">ключ подписывания: любой симметричный ключ для удостоверения `{device id}` ;</span><span class="sxs-lookup"><span data-stu-id="6212a-224">signing key: any symmetric key for the `{device id}` identity,</span></span>
* <span data-ttu-id="6212a-225">имя политики не требуется;</span><span class="sxs-lookup"><span data-stu-id="6212a-225">no policy name,</span></span>
* <span data-ttu-id="6212a-226">время окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="6212a-226">any expiration time.</span></span>

<span data-ttu-id="6212a-227">Далее приведен пример использования предыдущей функции Node.js:</span><span class="sxs-lookup"><span data-stu-id="6212a-227">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="6212a-228">Результат, предоставляющий доступ ко всем возможностям устройства device1, будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="6212a-228">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="6212a-229">Маркер SAS можно создать с помощью инструмента [обозреватель устройств][lnk-device-explorer] на основе .NET или с помощью кроссплатформенной служебной программы командной строки [iothub-explorer][lnk-iothub-explorer] на основе Node.</span><span class="sxs-lookup"><span data-stu-id="6212a-229">It is possible to generate a SAS token using the .NET [device explorer][lnk-device-explorer] tool or the cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="6212a-230">Использование политики общего доступа</span><span class="sxs-lookup"><span data-stu-id="6212a-230">Use a shared access policy</span></span>

<span data-ttu-id="6212a-231">При создании маркера из политики общего доступа в поле `skn` укажите имя политики.</span><span class="sxs-lookup"><span data-stu-id="6212a-231">When you create a token from a shared access policy, set the `skn` field to the name of the policy.</span></span> <span data-ttu-id="6212a-232">Эта политика должна предоставить разрешение **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="6212a-232">This policy must grant the **DeviceConnect** permission.</span></span>

<span data-ttu-id="6212a-233">Существует два основных сценария использования политик общего доступа для доступа к возможностям устройств:</span><span class="sxs-lookup"><span data-stu-id="6212a-233">The two main scenarios for using shared access policies to access device functionality are:</span></span>

* <span data-ttu-id="6212a-234">[облачные шлюзы протоколов][lnk-endpoints];</span><span class="sxs-lookup"><span data-stu-id="6212a-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="6212a-235">[службы маркеров][lnk-custom-auth], используемые для реализации настраиваемых схем аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6212a-235">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span></span>

<span data-ttu-id="6212a-236">Так как политика общего доступа может предоставлять доступ для подключения в качестве любого устройства, при создании маркеров безопасности важно использовать правильный URI ресурса.</span><span class="sxs-lookup"><span data-stu-id="6212a-236">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span></span> <span data-ttu-id="6212a-237">Этот параметр имеет особое значение для служб маркеров, которые должны определять область действия маркера для конкретного устройства с помощью URI ресурса.</span><span class="sxs-lookup"><span data-stu-id="6212a-237">This setting is especially important for token services, which have to scope the token to a specific device using the resource URI.</span></span> <span data-ttu-id="6212a-238">Он менее критичен для шлюзов протоколов, так как они уже обрабатывают трафик для всех устройств.</span><span class="sxs-lookup"><span data-stu-id="6212a-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="6212a-239">Например, служба маркеров, использующая предварительно созданную политику общего доступа с именем **device** , создаст маркер со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="6212a-239">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span></span>

* <span data-ttu-id="6212a-240">универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices/{device id}`;</span><span class="sxs-lookup"><span data-stu-id="6212a-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="6212a-241">ключ подписывания: один из ключей политики `device` ;</span><span class="sxs-lookup"><span data-stu-id="6212a-241">signing key: one of the keys of the `device` policy,</span></span>
* <span data-ttu-id="6212a-242">имя политики: `device`;</span><span class="sxs-lookup"><span data-stu-id="6212a-242">policy name: `device`,</span></span>
* <span data-ttu-id="6212a-243">время окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="6212a-243">any expiration time.</span></span>

<span data-ttu-id="6212a-244">Далее приведен пример использования предыдущей функции Node.js:</span><span class="sxs-lookup"><span data-stu-id="6212a-244">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="6212a-245">Результат, предоставляющий доступ ко всем возможностям устройства device1, будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="6212a-245">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="6212a-246">Шлюз протокола может использовать этот же маркер для всех устройств, задав `myhub.azure-devices.net/devices`в качестве универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="6212a-246">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="6212a-247">Использование маркеров безопасности из компонентов службы</span><span class="sxs-lookup"><span data-stu-id="6212a-247">Use security tokens from service components</span></span>

<span data-ttu-id="6212a-248">Компоненты службы могут создавать маркеры безопасности только с помощью политик общего доступа, предоставляющих соответствующие разрешения, как описано ранее.</span><span class="sxs-lookup"><span data-stu-id="6212a-248">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="6212a-249">Ниже приведены функции службы, предоставляемые в конечных точках.</span><span class="sxs-lookup"><span data-stu-id="6212a-249">Here is the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="6212a-250">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="6212a-250">Endpoint</span></span> | <span data-ttu-id="6212a-251">Функции</span><span class="sxs-lookup"><span data-stu-id="6212a-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="6212a-252">Создание, обновление, извлечение и удаление удостоверений устройств.</span><span class="sxs-lookup"><span data-stu-id="6212a-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="6212a-253">Получение сообщений с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="6212a-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="6212a-254">Получение ответа на сообщения, отправляемые из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="6212a-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="6212a-255">Отправка сообщений из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="6212a-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="6212a-256">Например, служба, использующая предварительно созданную политику общего доступа с именем **registryRead** , создаст маркер со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="6212a-256">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span></span>

* <span data-ttu-id="6212a-257">универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices`;</span><span class="sxs-lookup"><span data-stu-id="6212a-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="6212a-258">ключ подписывания: один из ключей политики `registryRead` ;</span><span class="sxs-lookup"><span data-stu-id="6212a-258">signing key: one of the keys of the `registryRead` policy,</span></span>
* <span data-ttu-id="6212a-259">имя политики: `registryRead`;</span><span class="sxs-lookup"><span data-stu-id="6212a-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="6212a-260">время окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="6212a-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="6212a-261">Результат, предоставляющий доступ для чтения всех идентификаторов устройств, будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="6212a-261">The result, which would grant access to read all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="6212a-262">Поддерживаемые сертификаты X.509</span><span class="sxs-lookup"><span data-stu-id="6212a-262">Supported X.509 certificates</span></span>

<span data-ttu-id="6212a-263">Вы можете использовать любой сертификат X.509 для проверки подлинности устройства с помощью Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-263">You can use any X.509 certificate to authenticate a device with IoT Hub.</span></span> <span data-ttu-id="6212a-264">Сертификаты включают в себя:</span><span class="sxs-lookup"><span data-stu-id="6212a-264">Certificates include:</span></span>

* <span data-ttu-id="6212a-265">**Существующий сертификат X.509**.</span><span class="sxs-lookup"><span data-stu-id="6212a-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="6212a-266">Возможно, устройство уже имеет связанный сертификат X.509.</span><span class="sxs-lookup"><span data-stu-id="6212a-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="6212a-267">Устройство может использовать этот сертификат для проверки подлинности с помощью Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-267">The device can use this certificate to authenticate with IoT Hub.</span></span>
* <span data-ttu-id="6212a-268">**Самостоятельно сформированный и самозаверяющий сертификат X-509**.</span><span class="sxs-lookup"><span data-stu-id="6212a-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="6212a-269">Производитель устройства или внутренний специалист по развертыванию может создать эти сертификаты и сохранить соответствующий закрытый ключ (и сертификат) на устройстве.</span><span class="sxs-lookup"><span data-stu-id="6212a-269">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span></span> <span data-ttu-id="6212a-270">Для этого вы можете использовать такие инструменты, как [OpenSSL][lnk-openssl] и служебная программа [Windows SelfSignedCertificate][lnk-selfsigned].</span><span class="sxs-lookup"><span data-stu-id="6212a-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="6212a-271">**Сертификат X.509, подписанный центром сертификации**.</span><span class="sxs-lookup"><span data-stu-id="6212a-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="6212a-272">Для идентификации устройства и его аутентификации с помощью Центра Интернета вещей можно использовать сертификат X.509, созданный и подписанный центром сертификации (ЦС).</span><span class="sxs-lookup"><span data-stu-id="6212a-272">To identify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="6212a-273">Центр Интернета вещей только проверяет, чтобы представленный отпечаток соответствовал настроенному отпечатку.</span><span class="sxs-lookup"><span data-stu-id="6212a-273">IoT Hub only verifies that the thumbprint presented matches the configured thumbprint.</span></span> <span data-ttu-id="6212a-274">Центр Интернета вещей не проверяет цепочку сертификатов.</span><span class="sxs-lookup"><span data-stu-id="6212a-274">IotHub does not validate the certificate chain.</span></span>

<span data-ttu-id="6212a-275">Для аутентификации устройство может использовать только один из вариантов: либо сертификат X.509, либо маркер безопасности.</span><span class="sxs-lookup"><span data-stu-id="6212a-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="6212a-276">Регистрация сертификата X.509 для устройства</span><span class="sxs-lookup"><span data-stu-id="6212a-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="6212a-277">[Пакет SDK службы Интенета вещей Azure для C#][lnk-service-sdk] (версия 1.0.8+) поддерживает регистрацию устройства, которое использует сертификат X.509 для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="6212a-277">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="6212a-278">Другие интерфейсы API (например, импорт и экспорт устройств) также поддерживают сертификаты X.509.</span><span class="sxs-lookup"><span data-stu-id="6212a-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="6212a-279">Поддержка C\#</span><span class="sxs-lookup"><span data-stu-id="6212a-279">C\# Support</span></span>

<span data-ttu-id="6212a-280">Класс **RegistryManager** предоставляет программный способ регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="6212a-280">The **RegistryManager** class provides a programmatic way to register a device.</span></span> <span data-ttu-id="6212a-281">В частности, методы **AddDeviceAsync** и **UpdateDeviceAsync** позволяют регистрировать и обновлять устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-281">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span></span> <span data-ttu-id="6212a-282">Эти два метода используют экземпляр **устройства** в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="6212a-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="6212a-283">Класс **Device** включает свойство **Authentication**, которое позволяет указывать основной и дополнительный отпечатки сертификата X.509.</span><span class="sxs-lookup"><span data-stu-id="6212a-283">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="6212a-284">Отпечаток представляет хэш SHA-1 сертификата X.509 (сохраненного с помощью двоичного кодирования DER).</span><span class="sxs-lookup"><span data-stu-id="6212a-284">The thumbprint represents a SHA-1 hash of the X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="6212a-285">Вы можете указать основной или вторичный отпечаток или оба отпечатка сразу.</span><span class="sxs-lookup"><span data-stu-id="6212a-285">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="6212a-286">Основной и вторичный отпечатки поддерживаются для обработки сценариев переключения сертификатов.</span><span class="sxs-lookup"><span data-stu-id="6212a-286">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="6212a-287">Центр Интернета вещей не требует и не хранит весь сертификат X.509, а только его отпечаток.</span><span class="sxs-lookup"><span data-stu-id="6212a-287">IoT Hub does not require or store the entire X.509 certificate, only the thumbprint.</span></span>

<span data-ttu-id="6212a-288">Ниже приведен пример фрагмента кода C\# для регистрации устройства с использованием сертификата X.509:</span><span class="sxs-lookup"><span data-stu-id="6212a-288">Here is a sample C\# code snippet to register a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="6212a-289">Использование сертификата X.509 во время выполнения операций среды выполнения</span><span class="sxs-lookup"><span data-stu-id="6212a-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="6212a-290">[Пакет SDK для устройств Azure IoT для .NET][lnk-client-sdk] (версия 1.0.11+) поддерживает использование сертификатов X.509.</span><span class="sxs-lookup"><span data-stu-id="6212a-290">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="6212a-291">Поддержка C\#</span><span class="sxs-lookup"><span data-stu-id="6212a-291">C\# Support</span></span>

<span data-ttu-id="6212a-292">Класс **DeviceAuthenticationWithX509Certificate** поддерживает создание экземпляров **DeviceClient** с помощью сертификата X.509.</span><span class="sxs-lookup"><span data-stu-id="6212a-292">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="6212a-293">Сертификат X.509 должен быть в формате PFX (также называется PKCS № 12), который содержит закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="6212a-293">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span></span>

<span data-ttu-id="6212a-294">Ниже приведен образец фрагмента кода:</span><span class="sxs-lookup"><span data-stu-id="6212a-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="6212a-295">Настраиваемая проверка подлинности устройства</span><span class="sxs-lookup"><span data-stu-id="6212a-295">Custom device authentication</span></span>

<span data-ttu-id="6212a-296">[Реестр удостоверений][lnk-identity-registry] Центра Интернета вещей позволяет настроить контроль доступа и учетные данные безопасности для каждого устройства с помощью [маркеров][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="6212a-296">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="6212a-297">Если в решении Интернета вещей уже есть настраиваемый реестр удостоверений и (или) схема аутентификации, то рекомендуем создать *службу маркеров*, чтобы интегрировать эту инфраструктуру с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* to integrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="6212a-298">Таким образом можно использовать и другие функции IoT в решении.</span><span class="sxs-lookup"><span data-stu-id="6212a-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="6212a-299">Служба маркеров — это пользовательская облачная служба.</span><span class="sxs-lookup"><span data-stu-id="6212a-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="6212a-300">Она использует *политику общего доступа* Центра Интернета вещей с разрешениями **DeviceConnect** для создания маркеров *уровня устройства*.</span><span class="sxs-lookup"><span data-stu-id="6212a-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions to create *device-scoped* tokens.</span></span> <span data-ttu-id="6212a-301">Эти маркеры позволяют устройству подключиться к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-301">These tokens enable a device to connect to your IoT hub.</span></span>

![Этапы для схемы службы маркеров.][img-tokenservice]

<span data-ttu-id="6212a-303">Ниже приведены основные этапы для схемы службы маркеров.</span><span class="sxs-lookup"><span data-stu-id="6212a-303">Here are the main steps of the token service pattern:</span></span>

1. <span data-ttu-id="6212a-304">Создание политики общего доступа Центра Интернета вещей с разрешениями **DeviceConnect** для вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="6212a-305">Эту политику можно создать на [портале Azure][lnk-management-portal] или программным способом.</span><span class="sxs-lookup"><span data-stu-id="6212a-305">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="6212a-306">Эту политику служба маркеров будет использовать для подписания создаваемых маркеров.</span><span class="sxs-lookup"><span data-stu-id="6212a-306">The token service uses this policy to sign the tokens it creates.</span></span>
1. <span data-ttu-id="6212a-307">Когда устройству требуется доступ к Центру Интернета вещей, оно запрашивает у службы маркеров подписанный маркер.</span><span class="sxs-lookup"><span data-stu-id="6212a-307">When a device needs to access your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="6212a-308">Для определения удостоверения устройства, используемого службой маркеров для создания маркера, устройство может использовать настраиваемую схему аутентификации или реестр удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6212a-308">The device can authenticate with your custom identity registry/authentication scheme to determine the device identity that the token service uses to create the token.</span></span>
1. <span data-ttu-id="6212a-309">Служба маркеров возвращает маркер.</span><span class="sxs-lookup"><span data-stu-id="6212a-309">The token service returns a token.</span></span> <span data-ttu-id="6212a-310">Чтобы создать маркер, используйте `/devices/{deviceId}` в качестве значения `resourceURI`, где `deviceId` — это аутентифицируемое устройство.</span><span class="sxs-lookup"><span data-stu-id="6212a-310">The token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as the device being authenticated.</span></span> <span data-ttu-id="6212a-311">Служба маркеров использует политики общего доступа для создания маркера.</span><span class="sxs-lookup"><span data-stu-id="6212a-311">The token service uses the shared access policy to construct the token.</span></span>
1. <span data-ttu-id="6212a-312">Устройство использует маркер для подключения к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-312">The device uses the token directly with the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="6212a-313">Для создания маркера в службе маркеров можно использовать класс .NET [SharedAccessSignatureBuilder][lnk-dotnet-sas] или класс Java [IotHubServiceSasToken][lnk-java-sas].</span><span class="sxs-lookup"><span data-stu-id="6212a-313">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span></span>

<span data-ttu-id="6212a-314">При необходимости служба маркеров может задать срок действия маркера.</span><span class="sxs-lookup"><span data-stu-id="6212a-314">The token service can set the token expiration as desired.</span></span> <span data-ttu-id="6212a-315">По истечении срока действия маркера Центр Интернета вещей разрывает подключение к устройству.</span><span class="sxs-lookup"><span data-stu-id="6212a-315">When the token expires, the IoT hub severs the device connection.</span></span> <span data-ttu-id="6212a-316">После этого устройство должно запросить новый маркер у службы маркеров.</span><span class="sxs-lookup"><span data-stu-id="6212a-316">Then, the device must request a new token from the token service.</span></span> <span data-ttu-id="6212a-317">Короткий срок действия увеличит нагрузку как на устройство, так и на службу маркеров.</span><span class="sxs-lookup"><span data-stu-id="6212a-317">A short expiry time increases the load on both the device and the token service.</span></span>

<span data-ttu-id="6212a-318">Кроме того, чтобы устройство могло подключаться к вашему центру, его необходимо добавить в реестр удостоверений Центра Интернета вещей, даже если для подключения устройство использует маркер, а не ключ.</span><span class="sxs-lookup"><span data-stu-id="6212a-318">For a device to connect to your hub, you must still add it to the IoT Hub identity registry — even though the device is using a token and not a device key to connect.</span></span> <span data-ttu-id="6212a-319">Поэтому контроль доступа на уровне отдельных устройств путем включения или отключения удостоверений устройств в [реестре удостоверений][lnk-identity-registry] продолжает работать.</span><span class="sxs-lookup"><span data-stu-id="6212a-319">Therefore, you can continue to use per-device access control by enabling or disabling device identities in the [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="6212a-320">Это уменьшает риск существования маркеров с длительным сроком действия.</span><span class="sxs-lookup"><span data-stu-id="6212a-320">This approach mitigates the risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="6212a-321">Сравнение с настраиваемым шлюзом</span><span class="sxs-lookup"><span data-stu-id="6212a-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="6212a-322">Вариант со службой маркеров является рекомендованным способом внедрения настраиваемого реестра удостоверений или схемы проверки подлинности с использованием Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-322">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="6212a-323">Этот вариант рекомендуется, так как Центр Интернета вещей продолжает обрабатывать большую часть трафика решения.</span><span class="sxs-lookup"><span data-stu-id="6212a-323">This pattern is recommended because IoT Hub continues to handle most of the solution traffic.</span></span> <span data-ttu-id="6212a-324">Однако, если настраиваемая схема аутентификации настолько тесно переплетена с протоколом, то для обработки всего трафика может потребоваться *настраиваемый шлюз*.</span><span class="sxs-lookup"><span data-stu-id="6212a-324">However, if the custom authentication scheme is so intertwined with the protocol, you may require a *custom gateway* to process all the traffic.</span></span> <span data-ttu-id="6212a-325">В качестве примера сценария можно привести использование [протокола TLS и общих ключей][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="6212a-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="6212a-326">Дополнительные сведения см. в разделе о [шлюзе протокола][lnk-protocols].</span><span class="sxs-lookup"><span data-stu-id="6212a-326">For more information, see the [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="6212a-327">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="6212a-327">Reference topics:</span></span>

<span data-ttu-id="6212a-328">В следующих материалах предоставлены дополнительные сведения об управлении доступом к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-328">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="6212a-329">Разрешения Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="6212a-329">IoT Hub permissions</span></span>

<span data-ttu-id="6212a-330">В следующей таблице указаны разрешения, с помощью которых можно управлять доступом к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-330">The following table lists the permissions you can use to control access to your IoT hub.</span></span>

| <span data-ttu-id="6212a-331">Разрешение</span><span class="sxs-lookup"><span data-stu-id="6212a-331">Permission</span></span> | <span data-ttu-id="6212a-332">Примечания</span><span class="sxs-lookup"><span data-stu-id="6212a-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="6212a-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="6212a-333">**RegistryRead**</span></span> |<span data-ttu-id="6212a-334">Предоставляет доступ на чтение к реестру удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6212a-334">Grants read access to the identity registry.</span></span> <span data-ttu-id="6212a-335">Дополнительные сведения см. в разделе о [реестре удостоверений][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="6212a-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="6212a-336">Это разрешение используется серверными облачными службами.</span><span class="sxs-lookup"><span data-stu-id="6212a-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="6212a-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="6212a-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="6212a-338">Предоставляет доступ на чтение и запись к реестру удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6212a-338">Grants read and write access to the identity registry.</span></span> <span data-ttu-id="6212a-339">Дополнительные сведения см. в разделе о [реестре удостоверений][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="6212a-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="6212a-340">Это разрешение используется серверными облачными службами.</span><span class="sxs-lookup"><span data-stu-id="6212a-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="6212a-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="6212a-341">**ServiceConnect**</span></span> |<span data-ttu-id="6212a-342">Предоставляет доступ к конечным точкам обмена данными и мониторинга, обращенным к облачной службе.</span><span class="sxs-lookup"><span data-stu-id="6212a-342">Grants access to cloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="6212a-343">Предоставляет разрешение облачным службам получать сообщения с устройств, отправлять сообщения на устройства и получать соответствующие уведомления о доставке.</span><span class="sxs-lookup"><span data-stu-id="6212a-343">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="6212a-344">Предоставляет разрешение на получение подтверждения передачи файлов.</span><span class="sxs-lookup"><span data-stu-id="6212a-344">Grants permission to retrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="6212a-345">Предоставляет разрешение на доступ к двойникам устройств для обновления тегов и требуемых свойств, извлечения сообщаемых свойств и выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="6212a-345">Grants permission to access device twins to update tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="6212a-346">Это разрешение используется серверными облачными службами.</span><span class="sxs-lookup"><span data-stu-id="6212a-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="6212a-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="6212a-347">**DeviceConnect**</span></span> |<span data-ttu-id="6212a-348">Предоставляет доступ к конечным точкам для устройств.</span><span class="sxs-lookup"><span data-stu-id="6212a-348">Grants access to device-facing endpoints.</span></span> <br/><span data-ttu-id="6212a-349">Позволяет отправлять сообщения с устройства в облако и получать сообщения, отправленные из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="6212a-349">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="6212a-350">Предоставляет разрешение на передачу файлов с устройства.</span><span class="sxs-lookup"><span data-stu-id="6212a-350">Grants permission to perform file upload from a device.</span></span> <br/><span data-ttu-id="6212a-351">Предоставляет разрешение на получение уведомлений о требуемых свойствах для двойников устройств и на обновление сообщенных свойств двойных устройств.</span><span class="sxs-lookup"><span data-stu-id="6212a-351">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="6212a-352">Предоставляет разрешение на передачу файлов.</span><span class="sxs-lookup"><span data-stu-id="6212a-352">Grants permission to perform file uploads.</span></span> <br/><span data-ttu-id="6212a-353">Это разрешение используют устройства.</span><span class="sxs-lookup"><span data-stu-id="6212a-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="6212a-354">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="6212a-354">Additional reference material</span></span>

<span data-ttu-id="6212a-355">Другие справочные статьи в руководстве разработчика для Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="6212a-355">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="6212a-356">Статья [IoT Hub endpoints][lnk-endpoints] (Конечные точки Центра Интернета вещей) содержит сведения о конечных точках, которые каждый Центр Интернета вещей предоставляет для операций управления и среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="6212a-356">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="6212a-357">Статья [Квоты и регулирование в Центре Интернета вещей][lnk-quotas] содержит сведения о квотах, применимых к службе Центра Интернета вещей, и поведении регулирования.</span><span class="sxs-lookup"><span data-stu-id="6212a-357">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="6212a-358">В статье [Пакеты SDK для устройств и служб Интернета вещей Azure][lnk-sdks] указаны различные языковые пакеты SDK, которые можно использовать при разработке приложений для устройств и служб, взаимодействующих с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-358">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="6212a-359">В статье [Справочник — язык запросов Центра Интернета вещей для двойников устройств, заданий и маршрутизации сообщений][lnk-query] описывается язык запросов, который можно использовать для получения сведений о двойниках устройств и заданиях из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-359">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="6212a-360">Статья [Поддержка MQTT в Центре Интернета вещей][lnk-devguide-mqtt] содержит дополнительные сведения о поддержке протокола MQTT в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6212a-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6212a-361">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6212a-361">Next steps</span></span>

<span data-ttu-id="6212a-362">Теперь, когда вы узнали, как управлять доступом к Центру Интернета вещей, вас могут заинтересовать следующие статьи в руководстве разработчика для Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="6212a-362">Now you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="6212a-363">[Основные сведения о двойниках устройств (предварительная версия)][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="6212a-363">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="6212a-364">[Вызов прямого метода на устройстве (предварительная версия)][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="6212a-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="6212a-365">[Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="6212a-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="6212a-366">Если вы хотели бы применить на практике некоторые основные понятия, описанные в этой статье, можно просмотреть следующие руководства по Центру Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="6212a-366">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="6212a-367">[Приступая к работе с Центром Интернета вещей Azure][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="6212a-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="6212a-368">[Учебник: как отправлять сообщения из облака на устройства с помощью центра IoT и .Net][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="6212a-368">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="6212a-369">[Учебник: как обрабатывать сообщения, отправляемые с устройства центра IoT в облако, с помощью .Net][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="6212a-369">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
