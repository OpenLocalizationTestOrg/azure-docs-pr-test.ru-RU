---
title: "Центр IoT Azure безопасности aaaUnderstand | Документы Microsoft"
description: "Руководство разработчика - как toocontrol доступ к tooIoT концентратора для приложений устройств и серверной части. Содержит сведения о маркерах безопасности и поддержке сертификатов X.509."
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
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a><span data-ttu-id="f7715-104">Элемент управления доступом tooIoT концентратора</span><span class="sxs-lookup"><span data-stu-id="f7715-104">Control access tooIoT Hub</span></span>

<span data-ttu-id="f7715-105">В этой статье описываются hello механизмы защиты вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-105">This article describes hello options for securing your IoT hub.</span></span> <span data-ttu-id="f7715-106">Центр IoT использует *разрешений* конечной точки центра IoT tooeach toogrant доступа.</span><span class="sxs-lookup"><span data-stu-id="f7715-106">IoT Hub uses *permissions* toogrant access tooeach IoT hub endpoint.</span></span> <span data-ttu-id="f7715-107">Разрешения ограничивают hello доступа tooan IoT hub на основе функциональности.</span><span class="sxs-lookup"><span data-stu-id="f7715-107">Permissions limit hello access tooan IoT hub based on functionality.</span></span>

<span data-ttu-id="f7715-108">Содержание статьи</span><span class="sxs-lookup"><span data-stu-id="f7715-108">This article describes:</span></span>

* <span data-ttu-id="f7715-109">Hello различные разрешения, можно предоставить tooaccess серверной части приложения или устройства tooa ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-109">hello different permissions that you can grant tooa device or back-end app tooaccess your IoT hub.</span></span>
* <span data-ttu-id="f7715-110">Здравствуйте, токены проверки подлинности процесса и hello используется tooverify разрешения.</span><span class="sxs-lookup"><span data-stu-id="f7715-110">hello authentication process and hello tokens it uses tooverify permissions.</span></span>
* <span data-ttu-id="f7715-111">Как tooscope учетные данные toolimit доступ к ресурсам toospecific.</span><span class="sxs-lookup"><span data-stu-id="f7715-111">How tooscope credentials toolimit access toospecific resources.</span></span>
* <span data-ttu-id="f7715-112">Поддержка сертификатов X.509 в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7715-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="f7715-113">Механизмы настраиваемой аутентификации устройства, использующие существующие реестры удостоверений устройств или схемы аутентификации.</span><span class="sxs-lookup"><span data-stu-id="f7715-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="f7715-114">Когда toouse</span><span class="sxs-lookup"><span data-stu-id="f7715-114">When toouse</span></span>

<span data-ttu-id="f7715-115">Необходимо иметь соответствующие разрешения tooaccess все конечные точки центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-115">You must have appropriate permissions tooaccess any of hello IoT Hub endpoints.</span></span> <span data-ttu-id="f7715-116">Например устройство необходимо включить токен, содержащий учетные данные безопасности вместе с каждое сообщение, что он отправляет tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="f7715-116">For example, a device must include a token containing security credentials along with every message it sends tooIoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="f7715-117">Контроль доступа и разрешений</span><span class="sxs-lookup"><span data-stu-id="f7715-117">Access control and permissions</span></span>

<span data-ttu-id="f7715-118">Вы можете предоставить [разрешений](#iot-hub-permissions) в hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="f7715-118">You can grant [permissions](#iot-hub-permissions) in hello following ways:</span></span>

* <span data-ttu-id="f7715-119">**Политики общего доступа на уровне Центра Интернета вещей**.</span><span class="sxs-lookup"><span data-stu-id="f7715-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="f7715-120">Политики общего доступа могут предоставлять любое сочетание [разрешений](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="f7715-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="f7715-121">Политики можно определить в hello [портал Azure][lnk-management-portal], или программно с помощью hello [API REST поставщика ресурсов центра IoT][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="f7715-121">You can define policies in hello [Azure portal][lnk-management-portal], or programmatically by using hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="f7715-122">Вновь созданный центр IoT состоит из следующих политик по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-122">A newly created IoT hub has hello following default policies:</span></span>

  * <span data-ttu-id="f7715-123">**iothubowner**: политика со всеми разрешениями;</span><span class="sxs-lookup"><span data-stu-id="f7715-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="f7715-124">**service**: политика с разрешением **ServiceConnect**;</span><span class="sxs-lookup"><span data-stu-id="f7715-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="f7715-125">**device**: политика с разрешением **DeviceConnect**;</span><span class="sxs-lookup"><span data-stu-id="f7715-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="f7715-126">**registryRead**: политика с разрешением **RegistryRead**;</span><span class="sxs-lookup"><span data-stu-id="f7715-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="f7715-127">**registryReadWrite**: политика с разрешениями **RegistryRead** и RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="f7715-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="f7715-128">**Учетные данные безопасности на уровне отдельного устройства**.</span><span class="sxs-lookup"><span data-stu-id="f7715-128">**Per-device security credentials**.</span></span> <span data-ttu-id="f7715-129">Каждый Центр Интернета вещей содержит [реестр удостоверений][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="f7715-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="f7715-130">Для каждого устройства в данном реестре удостоверений можно настроить учетные данные безопасности, которые предоставляют **DeviceConnect** разрешения области toohello соответствующие конечные точки устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped toohello corresponding device endpoints.</span></span>

<span data-ttu-id="f7715-131">Например, в стандартном решении IoT:</span><span class="sxs-lookup"><span data-stu-id="f7715-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="f7715-132">компонент управления Hello устройство использует hello *registryReadWrite* политики.</span><span class="sxs-lookup"><span data-stu-id="f7715-132">hello device management component uses hello *registryReadWrite* policy.</span></span>
* <span data-ttu-id="f7715-133">компонент обработчика событий Hello использует hello *службы* политики.</span><span class="sxs-lookup"><span data-stu-id="f7715-133">hello event processor component uses hello *service* policy.</span></span>
* <span data-ttu-id="f7715-134">бизнес-логики Hello устройства во время выполнения компонент использует hello *службы* политики.</span><span class="sxs-lookup"><span data-stu-id="f7715-134">hello run-time device business logic component uses hello *service* policy.</span></span>
* <span data-ttu-id="f7715-135">Отдельные устройства подключения, используя учетные данные, хранящиеся в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-135">Individual devices connect using credentials stored in hello IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="f7715-136">Дополнительные сведения см. в статье о [разрешениях](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="f7715-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="f7715-137">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="f7715-137">Authentication</span></span>

<span data-ttu-id="f7715-138">Центр IoT Azure предоставляет tooendpoints доступ, проверяя токен от hello общей политики доступа и учетные данные безопасности реестра удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f7715-138">Azure IoT Hub grants access tooendpoints by verifying a token against hello shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="f7715-139">Учетные данные безопасности, такие как симметричные ключи никогда не отправляются по сети hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-139">Security credentials, such as symmetric keys, are never sent over hello wire.</span></span>

> [!NOTE]
> <span data-ttu-id="f7715-140">Hello поставщика ресурсов Azure IoT Hub защищена с помощью подписки Azure как всех поставщиков в hello [диспетчера ресурсов Azure][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="f7715-140">hello Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in hello [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="f7715-141">Дополнительные сведения о том, как tooconstruct и используйте маркеры безопасности, в разделе [маркеры безопасности центра IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="f7715-141">For more information about how tooconstruct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="f7715-142">Особенности протокола</span><span class="sxs-lookup"><span data-stu-id="f7715-142">Protocol specifics</span></span>

<span data-ttu-id="f7715-143">Каждый поддерживаемый протокол, например MQTT, AMQP и HTTP, передает маркеры разными способами.</span><span class="sxs-lookup"><span data-stu-id="f7715-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="f7715-144">При использовании MQTT, пакет приветствия соединение имеет hello deviceId как hello ClientId, {iothubhostname} / {deviceId} в поле имени пользователя hello и маркер SAS в поле пароля hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-144">When using MQTT, hello CONNECT packet has hello deviceId as hello ClientId, {iothubhostname}/{deviceId} in hello Username field, and a SAS token in hello Password field.</span></span> <span data-ttu-id="f7715-145">{iothubhostname} должно hello полный CName hello центр IoT (например, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="f7715-145">{iothubhostname} should be hello full CName of hello IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="f7715-146">При использовании [AMQP][lnk-amqp] Центр Интернета вещей поддерживает механизм [SASL PLAIN][lnk-sasl-plain] и стандарт [защиты AMQP на основе утверждений][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="f7715-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="f7715-147">При использовании AMQP утверждений на основе безопасности, стандартные hello указывает как tootransmit эти токены.</span><span class="sxs-lookup"><span data-stu-id="f7715-147">If you use AMQP claims-based-security, hello standard specifies how tootransmit these tokens.</span></span>

<span data-ttu-id="f7715-148">ОБЫЧНЫЙ SASL hello **username** может быть:</span><span class="sxs-lookup"><span data-stu-id="f7715-148">For SASL PLAIN, hello **username** can be:</span></span>

* <span data-ttu-id="f7715-149">`{policyName}@sas.root.{iothubName}` — при использовании маркеров уровня Центра Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="f7715-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="f7715-150">`{deviceId}@sas.{iothubname}` — при использовании маркеров уровня устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="f7715-151">В обоих случаях поле пароль hello содержит токен hello, как описано в [маркеры безопасности центра IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="f7715-151">In both cases, hello password field contains hello token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="f7715-152">HTTP реализует проверку подлинности, включая действительный маркер в hello **авторизации** заголовка запроса.</span><span class="sxs-lookup"><span data-stu-id="f7715-152">HTTP implements authentication by including a valid token in hello **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="f7715-153">Пример</span><span class="sxs-lookup"><span data-stu-id="f7715-153">Example</span></span>

<span data-ttu-id="f7715-154">Имя пользователя (значение DeviceId следует вводить с учетом регистра): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="f7715-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="f7715-155">Пароль (маркер создания SAS с hello [обозреватель устройств] [ lnk-device-explorer] средство):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="f7715-155">Password (Generate SAS token with hello [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="f7715-156">Hello [пакеты SDK Azure IoT] [ lnk-sdks] автоматически создавать маркеры при подключении toohello службы.</span><span class="sxs-lookup"><span data-stu-id="f7715-156">hello [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting toohello service.</span></span> <span data-ttu-id="f7715-157">В некоторых случаях hello пакеты SDK Azure IoT не поддерживают все протоколы hello или все методы проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-157">In some cases, hello Azure IoT SDKs do not support all hello protocols or all hello authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="f7715-158">Специальные рекомендации для SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="f7715-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="f7715-159">При использовании обычного SASL с AMQP, клиент, подключающийся tooan центра IoT можно использовать один токен для каждого соединения TCP.</span><span class="sxs-lookup"><span data-stu-id="f7715-159">When using SASL PLAIN with AMQP, a client connecting tooan IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="f7715-160">По истечении срока действия маркера hello hello TCP-соединение отключается от службы hello и запускает переподключения.</span><span class="sxs-lookup"><span data-stu-id="f7715-160">When hello token expires, hello TCP connection disconnects from hello service and triggers a reconnect.</span></span> <span data-ttu-id="f7715-161">Такое поведение, пока не проблематично для серверной части приложения разорвал для приложения устройства для hello следующих причин:</span><span class="sxs-lookup"><span data-stu-id="f7715-161">This behavior, while not problematic for a back-end app, is damaging for a device app for hello following reasons:</span></span>

* <span data-ttu-id="f7715-162">Шлюзы обычно подключаются от имени многих устройств.</span><span class="sxs-lookup"><span data-stu-id="f7715-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="f7715-163">При использовании обычного SASL, они имеют toocreate distinct подключения TCP для каждого устройства, подключающегося tooan центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-163">When using SASL PLAIN, they have toocreate a distinct TCP connection for each device connecting tooan IoT hub.</span></span> <span data-ttu-id="f7715-164">Этот сценарий значительно увеличивает hello потребление мощности и сетевых ресурсов и увеличивает задержку hello каждого подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-164">This scenario considerably increases hello consumption of power and networking resources, and increases hello latency of each device connection.</span></span>
* <span data-ttu-id="f7715-165">После каждого срока действия маркера hello увеличено использование ресурсов tooreconnect нарушена устройств с ограниченными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="f7715-165">Resource-constrained devices are adversely affected by hello increased use of resources tooreconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="f7715-166">Определение области действия учетных данных на уровне Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f7715-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="f7715-167">Чтобы определить область действия для политик безопасности на уровне Центра Интернета вещей, создайте маркеры с помощью универсального кода (URI) ограниченного ресурса.</span><span class="sxs-lookup"><span data-stu-id="f7715-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="f7715-168">Например, сообщения из устройства в облако toosend hello конечной точки с устройства — **/devices/ {deviceId} / сообщений и событий**.</span><span class="sxs-lookup"><span data-stu-id="f7715-168">For example, hello endpoint toosend device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="f7715-169">Можно также использовать политику общего доступа на уровне концентратора IoT с **DeviceConnect** toosign разрешения маркер равен которого resourceURI **/devices/ {deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="f7715-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions toosign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="f7715-170">Этот подход создает маркер, который может использоваться toosend сообщения от имени устройства является только **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="f7715-170">This approach creates a token that is only usable toosend messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="f7715-171">Этот механизм — примерно toohello [политики издателя концентраторов событий][lnk-event-hubs-publisher-policy]и появится возможность tooimplement настраиваемые методы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f7715-171">This mechanism is similar toohello [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you tooimplement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="f7715-172">Маркеры безопасности Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f7715-172">Security tokens</span></span>

<span data-ttu-id="f7715-173">Центр IoT используется безопасность маркеры tooauthenticate устройств и служб tooavoid отправку ключей hello сети.</span><span class="sxs-lookup"><span data-stu-id="f7715-173">IoT Hub uses security tokens tooauthenticate devices and services tooavoid sending keys on hello wire.</span></span> <span data-ttu-id="f7715-174">Кроме того, маркеры безопасности ограничены по времени и области действия.</span><span class="sxs-lookup"><span data-stu-id="f7715-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="f7715-175">[Пакеты SDK для Azure IoT][lnk-sdks] автоматически создают маркеры без специальной настройки.</span><span class="sxs-lookup"><span data-stu-id="f7715-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="f7715-176">Некоторые сценарии требуют toogenerate и использование маркеров безопасности напрямую.</span><span class="sxs-lookup"><span data-stu-id="f7715-176">Some scenarios do require you toogenerate and use security tokens directly.</span></span> <span data-ttu-id="f7715-177">Ниже приведены соответствующие сценарии.</span><span class="sxs-lookup"><span data-stu-id="f7715-177">Such scenarios include:</span></span>

* <span data-ttu-id="f7715-178">Hello прямое использование рабочих областей hello MQTT, AMQP или HTTP.</span><span class="sxs-lookup"><span data-stu-id="f7715-178">hello direct use of hello MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="f7715-179">Здравствуйте реализацию шаблона службы маркеров hello, как описано в статье [нестандартной проверки подлинности устройства][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="f7715-179">hello implementation of hello token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="f7715-180">Центр IoT также допускает tooauthenticate устройства с центром IoT [сертификаты X.509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="f7715-180">IoT Hub also allows devices tooauthenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="f7715-181">Структура маркера безопасности</span><span class="sxs-lookup"><span data-stu-id="f7715-181">Security token structure</span></span>

<span data-ttu-id="f7715-182">Использовать безопасности маркеры toogrant привязанных ко времени доступа toodevices toospecific функциональных возможностей и служб в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-182">You use security tokens toogrant time-bounded access toodevices and services toospecific functionality in IoT Hub.</span></span> <span data-ttu-id="f7715-183">tooIoT tooconnect tooget авторизации концентратора, устройств и служб необходимо отправить безопасности маркеров, подписанных с общего доступа или симметричный ключ.</span><span class="sxs-lookup"><span data-stu-id="f7715-183">tooget authorization tooconnect tooIoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="f7715-184">Эти ключи хранятся в реестре удостоверений hello удостоверение устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-184">These keys are stored with a device identity in hello identity registry.</span></span>

<span data-ttu-id="f7715-185">Токен, подписанным с функциями общего доступа ключ предоставляет доступ tooall hello, связанные с помощью политики hello общего доступа.</span><span class="sxs-lookup"><span data-stu-id="f7715-185">A token signed with a shared access key grants access tooall hello functionality associated with hello shared access policy permissions.</span></span> <span data-ttu-id="f7715-186">Токен, подписанным с hello симметричный ключ только предоставляет удостоверение устройства **DeviceConnect** разрешение для hello связанного удостоверения устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-186">A token signed with a device identity's symmetric key only grants hello **DeviceConnect** permission for hello associated device identity.</span></span>

<span data-ttu-id="f7715-187">Hello маркер безопасности имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="f7715-187">hello security token has hello following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="f7715-188">Ниже приведены hello ожидаемые значения.</span><span class="sxs-lookup"><span data-stu-id="f7715-188">Here are hello expected values:</span></span>

| <span data-ttu-id="f7715-189">Значение</span><span class="sxs-lookup"><span data-stu-id="f7715-189">Value</span></span> | <span data-ttu-id="f7715-190">Описание</span><span class="sxs-lookup"><span data-stu-id="f7715-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f7715-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="f7715-191">{signature}</span></span> |<span data-ttu-id="f7715-192">Строки подписи HMAC-SHA256 hello формы: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="f7715-192">An HMAC-SHA256 signature string of hello form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="f7715-193">**Важные**: hello ключ декодирование из base64 и использовать в качестве ключа tooperform hello HMAC-SHA256 вычисления.</span><span class="sxs-lookup"><span data-stu-id="f7715-193">**Important**: hello key is decoded from base64 and used as key tooperform hello HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="f7715-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="f7715-194">{resourceURI}</span></span> |<span data-ttu-id="f7715-195">Префикс URI (с помощью сегмента) hello конечных точек, доступных с данным маркером, начиная с имени узла центра IoT hello (не protocol).</span><span class="sxs-lookup"><span data-stu-id="f7715-195">URI prefix (by segment) of hello endpoints that can be accessed with this token, starting with host name of hello IoT hub (no protocol).</span></span> <span data-ttu-id="f7715-196">Например, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="f7715-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="f7715-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="f7715-197">{expiry}</span></span> |<span data-ttu-id="f7715-198">Строки UTF-8 для числа секунд, прошедших с начала эпохи hello: 00:00:00 UTC 1 января 1970 года.</span><span class="sxs-lookup"><span data-stu-id="f7715-198">UTF8 strings for number of seconds since hello epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="f7715-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="f7715-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="f7715-200">Чем меньше случае кодирование URL-адресов-hello нижнего регистра ресурса (URI)</span><span class="sxs-lookup"><span data-stu-id="f7715-200">Lower case URL-encoding of hello lower case resource URI</span></span> |
| <span data-ttu-id="f7715-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="f7715-201">{policyName}</span></span> |<span data-ttu-id="f7715-202">Имя Hello hello общего toowhich политики доступа ссылается этот токен.</span><span class="sxs-lookup"><span data-stu-id="f7715-202">hello name of hello shared access policy toowhich this token refers.</span></span> <span data-ttu-id="f7715-203">Отсутствует, если токен hello ссылается реестра toodevice учетные данные.</span><span class="sxs-lookup"><span data-stu-id="f7715-203">Absent if hello token refers toodevice-registry credentials.</span></span> |

<span data-ttu-id="f7715-204">**Обратите внимание на префикс**: префикс URI hello вычисляется с помощью сегмента, а не символ.</span><span class="sxs-lookup"><span data-stu-id="f7715-204">**Note on prefix**: hello URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="f7715-205">Например, `/a/b` — это префикс для `/a/b/c`, а не для `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="f7715-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="f7715-206">Hello следующие Node.js фрагмент показывает, функция, вызываемая **generateSasToken** Здравствуйте, вычисляет токен из входных данных hello `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="f7715-206">hello following Node.js snippet shows a function called **generateSasToken** that computes hello token from hello inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="f7715-207">Hello далее разделах описано, как варианты использования tooinitialize hello различных входных данных для другой токен hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-207">hello next sections detail how tooinitialize hello different inputs for hello different token use cases.</span></span>

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

<span data-ttu-id="f7715-208">Для сравнения hello эквивалентные toogenerate кода Python, маркер безопасности является:</span><span class="sxs-lookup"><span data-stu-id="f7715-208">As a comparison, hello equivalent Python code toogenerate a security token is:</span></span>

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
> <span data-ttu-id="f7715-209">Так как срок действия маркера hello hello проверяется на компьютерах центра IoT, hello смещение на часах hello hello машины, который создает токен hello должен быть минимальным.</span><span class="sxs-lookup"><span data-stu-id="f7715-209">Since hello time validity of hello token is validated on IoT Hub machines, hello drift on hello clock of hello machine that generates hello token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="f7715-210">Использование маркеров SAS в приложении для устройства</span><span class="sxs-lookup"><span data-stu-id="f7715-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="f7715-211">Существует два способа tooobtain **DeviceConnect** разрешений с центром IoT с маркерами безопасности: используйте [ключ симметричного устройства из реестра удостоверений hello](#use-a-symmetric-key-in-the-identity-registry), или используйте [общий ключ доступа](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="f7715-211">There are two ways tooobtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from hello identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="f7715-212">Помните, что все функциональные возможности, доступные с устройств, намеренно предоставляются в конечных точках с префиксом `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="f7715-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7715-213">Hello только что центр IoT проверяет подлинность определенного устройства при использовании симметричным ключом удостоверения устройства hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-213">hello only way that IoT Hub authenticates a specific device is using hello device identity symmetric key.</span></span> <span data-ttu-id="f7715-214">В случаях если политика общего доступа используется tooaccess функциональные возможности устройства, hello решения необходимо учитывать компонент hello выдачи маркера безопасности hello доверенного компонента.</span><span class="sxs-lookup"><span data-stu-id="f7715-214">In cases when a shared access policy is used tooaccess device functionality, hello solution must consider hello component issuing hello security token as a trusted subcomponent.</span></span>

<span data-ttu-id="f7715-215">конечные точки с выходом устройства Hello являются (вне зависимости от протокола hello):</span><span class="sxs-lookup"><span data-stu-id="f7715-215">hello device-facing endpoints are (irrespective of hello protocol):</span></span>

| <span data-ttu-id="f7715-216">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="f7715-216">Endpoint</span></span> | <span data-ttu-id="f7715-217">Функции</span><span class="sxs-lookup"><span data-stu-id="f7715-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="f7715-218">Отправка сообщений с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="f7715-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="f7715-219">Получение сообщений из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="f7715-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a><span data-ttu-id="f7715-220">Использовать симметричный ключ в реестре удостоверений hello</span><span class="sxs-lookup"><span data-stu-id="f7715-220">Use a symmetric key in hello identity registry</span></span>

<span data-ttu-id="f7715-221">При использовании симметричного ключа удостоверения устройства toogenerate маркер, hello Имя_политики (`skn`) элемент маркера hello пропускается.</span><span class="sxs-lookup"><span data-stu-id="f7715-221">When using a device identity's symmetric key toogenerate a token, hello policyName (`skn`) element of hello token is omitted.</span></span>

<span data-ttu-id="f7715-222">Например маркер создания tooaccess hello все функциональные возможности устройства должны иметь следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f7715-222">For example, a token created tooaccess all device functionality should have hello following parameters:</span></span>

* <span data-ttu-id="f7715-223">универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices/{device id}`;</span><span class="sxs-lookup"><span data-stu-id="f7715-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="f7715-224">ключ подписи: любого симметричного ключа для hello `{device id}` удостоверения</span><span class="sxs-lookup"><span data-stu-id="f7715-224">signing key: any symmetric key for hello `{device id}` identity,</span></span>
* <span data-ttu-id="f7715-225">имя политики не требуется;</span><span class="sxs-lookup"><span data-stu-id="f7715-225">no policy name,</span></span>
* <span data-ttu-id="f7715-226">время окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="f7715-226">any expiration time.</span></span>

<span data-ttu-id="f7715-227">Пример использования hello, предшествующий Node.js функция будет следующим:</span><span class="sxs-lookup"><span data-stu-id="f7715-227">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="f7715-228">Hello результат, который предоставляет функциональные возможности tooall доступа для устройстве 1, будет следующим:</span><span class="sxs-lookup"><span data-stu-id="f7715-228">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="f7715-229">Он является маркер SAS, с помощью hello .NET возможных toogenerate [обозреватель устройств] [ lnk-device-explorer] инструмент либо hello кросс платформенных, основанные на узлах [explorer центром IOT] [ lnk-iothub-explorer] программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="f7715-229">It is possible toogenerate a SAS token using hello .NET [device explorer][lnk-device-explorer] tool or hello cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="f7715-230">Использование политики общего доступа</span><span class="sxs-lookup"><span data-stu-id="f7715-230">Use a shared access policy</span></span>

<span data-ttu-id="f7715-231">При создании маркера из политики общего доступа установлен hello `skn` toohello имя поля hello политики.</span><span class="sxs-lookup"><span data-stu-id="f7715-231">When you create a token from a shared access policy, set hello `skn` field toohello name of hello policy.</span></span> <span data-ttu-id="f7715-232">Эта политика необходимо предоставить hello **DeviceConnect** разрешение.</span><span class="sxs-lookup"><span data-stu-id="f7715-232">This policy must grant hello **DeviceConnect** permission.</span></span>

<span data-ttu-id="f7715-233">приведены Hello два основных сценария использования функциональные возможности устройства tooaccess политики общего доступа.</span><span class="sxs-lookup"><span data-stu-id="f7715-233">hello two main scenarios for using shared access policies tooaccess device functionality are:</span></span>

* <span data-ttu-id="f7715-234">[облачные шлюзы протоколов][lnk-endpoints];</span><span class="sxs-lookup"><span data-stu-id="f7715-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="f7715-235">[службы маркеров] [ lnk-custom-auth] используется tooimplement пользовательских схем проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f7715-235">[token services][lnk-custom-auth] used tooimplement custom authentication schemes.</span></span>

<span data-ttu-id="f7715-236">С момента hello политики общего доступа могут потенциально предоставлять доступ tooconnect любое устройство является важным toouse hello правильный URI ресурса, при создании маркеров безопасности.</span><span class="sxs-lookup"><span data-stu-id="f7715-236">Since hello shared access policy can potentially grant access tooconnect as any device, it is important toouse hello correct resource URI when creating security tokens.</span></span> <span data-ttu-id="f7715-237">Этот параметр особенно важен для служб маркеров, которые имеют tooscope hello маркера tooa определенному устройству с помощью hello ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="f7715-237">This setting is especially important for token services, which have tooscope hello token tooa specific device using hello resource URI.</span></span> <span data-ttu-id="f7715-238">Он менее критичен для шлюзов протоколов, так как они уже обрабатывают трафик для всех устройств.</span><span class="sxs-lookup"><span data-stu-id="f7715-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="f7715-239">Например, маркер службы с помощью предварительно созданного hello общих политика доступа **устройства** создать токен hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f7715-239">As an example, a token service using hello pre-created shared access policy called **device** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="f7715-240">универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices/{device id}`;</span><span class="sxs-lookup"><span data-stu-id="f7715-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="f7715-241">ключ подписи: один из ключей hello hello `device` политики,</span><span class="sxs-lookup"><span data-stu-id="f7715-241">signing key: one of hello keys of hello `device` policy,</span></span>
* <span data-ttu-id="f7715-242">имя политики: `device`;</span><span class="sxs-lookup"><span data-stu-id="f7715-242">policy name: `device`,</span></span>
* <span data-ttu-id="f7715-243">время окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="f7715-243">any expiration time.</span></span>

<span data-ttu-id="f7715-244">Пример использования hello, предшествующий Node.js функция будет следующим:</span><span class="sxs-lookup"><span data-stu-id="f7715-244">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="f7715-245">Hello результат, который предоставляет функциональные возможности tooall доступа для устройстве 1, будет следующим:</span><span class="sxs-lookup"><span data-stu-id="f7715-245">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="f7715-246">Использовать шлюз протокола hello же маркера для всех устройств, которые просто параметр hello ресурса (URI), слишком`myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="f7715-246">A protocol gateway could use hello same token for all devices simply setting hello resource URI too`myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="f7715-247">Использование маркеров безопасности из компонентов службы</span><span class="sxs-lookup"><span data-stu-id="f7715-247">Use security tokens from service components</span></span>

<span data-ttu-id="f7715-248">Компоненты службы можно создавать только маркеры безопасности, с помощью политики общего доступа, предоставление hello соответствующие разрешения, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="f7715-248">Service components can only generate security tokens using shared access policies granting hello appropriate permissions as explained previously.</span></span>

<span data-ttu-id="f7715-249">Вот hello функции службы, предоставляемые hello конечных точек.</span><span class="sxs-lookup"><span data-stu-id="f7715-249">Here is hello service functions exposed on hello endpoints:</span></span>

| <span data-ttu-id="f7715-250">Конечная точка</span><span class="sxs-lookup"><span data-stu-id="f7715-250">Endpoint</span></span> | <span data-ttu-id="f7715-251">Функции</span><span class="sxs-lookup"><span data-stu-id="f7715-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="f7715-252">Создание, обновление, извлечение и удаление удостоверений устройств.</span><span class="sxs-lookup"><span data-stu-id="f7715-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="f7715-253">Получение сообщений с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="f7715-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="f7715-254">Получение ответа на сообщения, отправляемые из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="f7715-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="f7715-255">Отправка сообщений из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="f7715-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="f7715-256">Например, службы, создание с помощью предварительно созданного hello общих политика доступа **registryRead** создать токен hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f7715-256">As an example, a service generating using hello pre-created shared access policy called **registryRead** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="f7715-257">универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices`;</span><span class="sxs-lookup"><span data-stu-id="f7715-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="f7715-258">ключ подписи: один из ключей hello hello `registryRead` политики,</span><span class="sxs-lookup"><span data-stu-id="f7715-258">signing key: one of hello keys of hello `registryRead` policy,</span></span>
* <span data-ttu-id="f7715-259">имя политики: `registryRead`;</span><span class="sxs-lookup"><span data-stu-id="f7715-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="f7715-260">время окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="f7715-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="f7715-261">результат Hello, которой предоставляется доступ tooread все удостоверения на устройстве, будет следующим:</span><span class="sxs-lookup"><span data-stu-id="f7715-261">hello result, which would grant access tooread all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="f7715-262">Поддерживаемые сертификаты X.509</span><span class="sxs-lookup"><span data-stu-id="f7715-262">Supported X.509 certificates</span></span>

<span data-ttu-id="f7715-263">Можно использовать любой tooauthenticate сертификат X.509 устройства с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-263">You can use any X.509 certificate tooauthenticate a device with IoT Hub.</span></span> <span data-ttu-id="f7715-264">Сертификаты включают в себя:</span><span class="sxs-lookup"><span data-stu-id="f7715-264">Certificates include:</span></span>

* <span data-ttu-id="f7715-265">**Существующий сертификат X.509**.</span><span class="sxs-lookup"><span data-stu-id="f7715-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="f7715-266">Возможно, устройство уже имеет связанный сертификат X.509.</span><span class="sxs-lookup"><span data-stu-id="f7715-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="f7715-267">Hello устройство может использовать этот сертификат tooauthenticate с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-267">hello device can use this certificate tooauthenticate with IoT Hub.</span></span>
* <span data-ttu-id="f7715-268">**Самостоятельно сформированный и самозаверяющий сертификат X-509**.</span><span class="sxs-lookup"><span data-stu-id="f7715-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="f7715-269">Изготовителя устройства или собственных разработчик может создать эти сертификаты и сохранить hello соответствующий закрытый ключ (и сертификата) на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-269">A device manufacturer or in-house deployer can generate these certificates and store hello corresponding private key (and certificate) on hello device.</span></span> <span data-ttu-id="f7715-270">Для этого вы можете использовать такие инструменты, как [OpenSSL][lnk-openssl] и служебная программа [Windows SelfSignedCertificate][lnk-selfsigned].</span><span class="sxs-lookup"><span data-stu-id="f7715-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="f7715-271">**Сертификат X.509, подписанный центром сертификации**.</span><span class="sxs-lookup"><span data-stu-id="f7715-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="f7715-272">tooidentify устройства и выполнять его проверку подлинности с центром IoT, можно использовать сертификат X.509 созданный и подписанный с центром сертификации (ЦС).</span><span class="sxs-lookup"><span data-stu-id="f7715-272">tooidentify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="f7715-273">Центр IoT только проверяет, что отпечаток hello представлены соответствует отпечатку hello настроен.</span><span class="sxs-lookup"><span data-stu-id="f7715-273">IoT Hub only verifies that hello thumbprint presented matches hello configured thumbprint.</span></span> <span data-ttu-id="f7715-274">Центром IOT не проверяет цепочку сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-274">IotHub does not validate hello certificate chain.</span></span>

<span data-ttu-id="f7715-275">Для аутентификации устройство может использовать только один из вариантов: либо сертификат X.509, либо маркер безопасности.</span><span class="sxs-lookup"><span data-stu-id="f7715-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="f7715-276">Регистрация сертификата X.509 для устройства</span><span class="sxs-lookup"><span data-stu-id="f7715-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="f7715-277">Hello [пакет SDK службы Azure IoT для C#] [ lnk-service-sdk] (версия 1.0.8+) поддерживает регистрации устройства, использующего сертификат X.509 для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f7715-277">hello [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="f7715-278">Другие интерфейсы API (например, импорт и экспорт устройств) также поддерживают сертификаты X.509.</span><span class="sxs-lookup"><span data-stu-id="f7715-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="f7715-279">Поддержка C\#</span><span class="sxs-lookup"><span data-stu-id="f7715-279">C\# Support</span></span>

<span data-ttu-id="f7715-280">Hello **RegistryManager** класс предоставляет tooregister программный способ устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-280">hello **RegistryManager** class provides a programmatic way tooregister a device.</span></span> <span data-ttu-id="f7715-281">В частности, hello **AddDeviceAsync** и **UpdateDeviceAsync** методы позволяют tooregister и обновить устройство в hello реестра удостоверений центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-281">In particular, hello **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you tooregister and update a device in hello IoT Hub identity registry.</span></span> <span data-ttu-id="f7715-282">Эти два метода используют экземпляр **устройства** в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="f7715-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="f7715-283">Hello **устройства** класс включает **проверки подлинности** свойство, которое позволяет вам toospecify первичного и вторичного X.509 отпечатки сертификата.</span><span class="sxs-lookup"><span data-stu-id="f7715-283">hello **Device** class includes an **Authentication** property that allows you toospecify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="f7715-284">отпечаток Hello представляет хэш SHA-1 сертификата X.509 hello (хранимая с помощью двоичной кодировке DER).</span><span class="sxs-lookup"><span data-stu-id="f7715-284">hello thumbprint represents a SHA-1 hash of hello X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="f7715-285">Предусмотрена возможность hello указания первичного отпечаток или получателей отпечаток или оба.</span><span class="sxs-lookup"><span data-stu-id="f7715-285">You have hello option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="f7715-286">Отпечатки основного и дополнительного, поддерживаемых toohandle сценариев смены сертификата.</span><span class="sxs-lookup"><span data-stu-id="f7715-286">Primary and secondary thumbprints are supported toohandle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="f7715-287">Центр IoT не требует или сохранить hello весь сертификат X.509, только отпечаток hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-287">IoT Hub does not require or store hello entire X.509 certificate, only hello thumbprint.</span></span>

<span data-ttu-id="f7715-288">Ниже приведен пример C\# кода устройства с помощью сертификата X.509 tooregister фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="f7715-288">Here is a sample C\# code snippet tooregister a device using an X.509 certificate:</span></span>

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

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="f7715-289">Использование сертификата X.509 во время выполнения операций среды выполнения</span><span class="sxs-lookup"><span data-stu-id="f7715-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="f7715-290">Hello [устройств Azure IoT SDK для .NET] [ lnk-client-sdk] (версия 1.0.11+) поддерживает использование hello сертификатов X.509.</span><span class="sxs-lookup"><span data-stu-id="f7715-290">hello [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports hello use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="f7715-291">Поддержка C\#</span><span class="sxs-lookup"><span data-stu-id="f7715-291">C\# Support</span></span>

<span data-ttu-id="f7715-292">Здравствуйте, класс **DeviceAuthenticationWithX509Certificate** поддерживает hello создание **DeviceClient** экземпляров с помощью сертификата X.509.</span><span class="sxs-lookup"><span data-stu-id="f7715-292">hello class **DeviceAuthenticationWithX509Certificate** supports hello creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="f7715-293">сертификат X.509 Hello должен быть в формате PFX (также называемый PKCS #12) hello, который содержит закрытый ключ hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-293">hello X.509 certificate must be in hello PFX (also called PKCS #12) format that includes hello private key.</span></span>

<span data-ttu-id="f7715-294">Ниже приведен образец фрагмента кода:</span><span class="sxs-lookup"><span data-stu-id="f7715-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="f7715-295">Настраиваемая проверка подлинности устройства</span><span class="sxs-lookup"><span data-stu-id="f7715-295">Custom device authentication</span></span>

<span data-ttu-id="f7715-296">Можно использовать центр IoT hello [реестра удостоверений] [ lnk-identity-registry] с помощью управление доступом и учетные данные безопасности на устройство tooconfigure [маркеры] [ lnk-sas-tokens] .</span><span class="sxs-lookup"><span data-stu-id="f7715-296">You can use hello IoT Hub [identity registry][lnk-identity-registry] tooconfigure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="f7715-297">Если решения IoT уже имеет схему пользовательское удостоверение реестра или проверку подлинности, рассмотрите возможность создания *токена службы* toointegrate эта инфраструктура с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* toointegrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="f7715-298">Таким образом можно использовать и другие функции IoT в решении.</span><span class="sxs-lookup"><span data-stu-id="f7715-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="f7715-299">Служба маркеров — это пользовательская облачная служба.</span><span class="sxs-lookup"><span data-stu-id="f7715-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="f7715-300">Она использует Центр IoT *общей политики доступа* с **DeviceConnect** toocreate разрешений *уровня устройства* маркеры.</span><span class="sxs-lookup"><span data-stu-id="f7715-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions toocreate *device-scoped* tokens.</span></span> <span data-ttu-id="f7715-301">Эти маркеры позволяют центра IoT tooyour tooconnect устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-301">These tokens enable a device tooconnect tooyour IoT hub.</span></span>

![Действия службы маркеров шаблона hello][img-tokenservice]

<span data-ttu-id="f7715-303">Ниже приведены основные этапы hello hello шаблона службы маркеров.</span><span class="sxs-lookup"><span data-stu-id="f7715-303">Here are hello main steps of hello token service pattern:</span></span>

1. <span data-ttu-id="f7715-304">Создание политики общего доступа Центра Интернета вещей с разрешениями **DeviceConnect** для вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7715-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="f7715-305">Эту политику можно создать в hello [портал Azure] [ lnk-management-portal] или программными средствами.</span><span class="sxs-lookup"><span data-stu-id="f7715-305">You can create this policy in hello [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="f7715-306">Hello маркера служба использует этот токены hello toosign политики, созданные им.</span><span class="sxs-lookup"><span data-stu-id="f7715-306">hello token service uses this policy toosign hello tokens it creates.</span></span>
1. <span data-ttu-id="f7715-307">Когда устройство должно tooaccess концентратор IoT, подписанный маркер запросов из токена службы.</span><span class="sxs-lookup"><span data-stu-id="f7715-307">When a device needs tooaccess your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="f7715-308">Hello устройства могут проходить проверку подлинности с удостоверением пользовательское удостоверение hello toodetermine проверки подлинности реестру схемы устройства, hello маркера служба использует маркер toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-308">hello device can authenticate with your custom identity registry/authentication scheme toodetermine hello device identity that hello token service uses toocreate hello token.</span></span>
1. <span data-ttu-id="f7715-309">Служба маркеров Hello возвращает маркер.</span><span class="sxs-lookup"><span data-stu-id="f7715-309">hello token service returns a token.</span></span> <span data-ttu-id="f7715-310">Hello токен создается с помощью `/devices/{deviceId}` как `resourceURI`, с `deviceId` как устройство hello, проходящего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="f7715-310">hello token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as hello device being authenticated.</span></span> <span data-ttu-id="f7715-311">Служба маркеров Hello использует hello общей политики tooconstruct hello токен доступа.</span><span class="sxs-lookup"><span data-stu-id="f7715-311">hello token service uses hello shared access policy tooconstruct hello token.</span></span>
1. <span data-ttu-id="f7715-312">Hello устройства с помощью токена hello непосредственно с центром IoT hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-312">hello device uses hello token directly with hello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="f7715-313">Можно использовать класс .NET hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] или hello класс Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate маркер в службе маркеров.</span><span class="sxs-lookup"><span data-stu-id="f7715-313">You can use hello .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or hello Java class [IotHubServiceSasToken][lnk-java-sas] toocreate a token in your token service.</span></span>

<span data-ttu-id="f7715-314">Hello службы маркеров можно задать срок действия токена hello в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="f7715-314">hello token service can set hello token expiration as desired.</span></span> <span data-ttu-id="f7715-315">По истечении срока действия маркера hello центра IoT hello разрывает подключение устройства hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-315">When hello token expires, hello IoT hub severs hello device connection.</span></span> <span data-ttu-id="f7715-316">Затем устройство hello должен запросить новый маркер от службы маркеров hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-316">Then, hello device must request a new token from hello token service.</span></span> <span data-ttu-id="f7715-317">Короткий срок увеличивает нагрузку hello на устройстве hello и службой маркеров hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-317">A short expiry time increases hello load on both hello device and hello token service.</span></span>

<span data-ttu-id="f7715-318">Концентратора tooyour tooconnect устройства, необходимо добавить его toohello реестра удостоверений центр IoT — несмотря на то, что устройство hello использует токен и не tooconnect ключа устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-318">For a device tooconnect tooyour hub, you must still add it toohello IoT Hub identity registry — even though hello device is using a token and not a device key tooconnect.</span></span> <span data-ttu-id="f7715-319">Таким образом, вы можете продолжить toouse контроля доступа на устройство, включение или отключение устройства удостоверений в hello [реестра удостоверений][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="f7715-319">Therefore, you can continue toouse per-device access control by enabling or disabling device identities in hello [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="f7715-320">Этот подход снижает риски hello использования маркеров со временем long истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="f7715-320">This approach mitigates hello risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="f7715-321">Сравнение с настраиваемым шлюзом</span><span class="sxs-lookup"><span data-stu-id="f7715-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="f7715-322">шаблон службы маркеров Hello является hello рекомендуется tooimplement способом схему проверки подлинности реестру пользовательское удостоверение с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-322">hello token service pattern is hello recommended way tooimplement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="f7715-323">Рекомендуется использовать такую схему, поскольку центр IoT будет toohandle большая часть трафика hello решения.</span><span class="sxs-lookup"><span data-stu-id="f7715-323">This pattern is recommended because IoT Hub continues toohandle most of hello solution traffic.</span></span> <span data-ttu-id="f7715-324">Однако если hello пользовательской схемы проверки подлинности Итак находящаяся между протокола hello, может потребоваться *пользовательского шлюза* tooprocess все hello трафика.</span><span class="sxs-lookup"><span data-stu-id="f7715-324">However, if hello custom authentication scheme is so intertwined with hello protocol, you may require a *custom gateway* tooprocess all hello traffic.</span></span> <span data-ttu-id="f7715-325">В качестве примера сценария можно привести использование [протокола TLS и общих ключей][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="f7715-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="f7715-326">Дополнительные сведения см. в разделе hello [шлюз протокола] [ lnk-protocols] раздела.</span><span class="sxs-lookup"><span data-stu-id="f7715-326">For more information, see hello [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="f7715-327">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="f7715-327">Reference topics:</span></span>

<span data-ttu-id="f7715-328">Hello следующие справочные разделы предоставляют дополнительные сведения о центра IoT tooyour управления доступом.</span><span class="sxs-lookup"><span data-stu-id="f7715-328">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="f7715-329">Разрешения Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f7715-329">IoT Hub permissions</span></span>

<span data-ttu-id="f7715-330">Hello следующей таблице перечислены разрешения hello, можно использовать центр IoT tooyour toocontrol доступа.</span><span class="sxs-lookup"><span data-stu-id="f7715-330">hello following table lists hello permissions you can use toocontrol access tooyour IoT hub.</span></span>

| <span data-ttu-id="f7715-331">Разрешение</span><span class="sxs-lookup"><span data-stu-id="f7715-331">Permission</span></span> | <span data-ttu-id="f7715-332">Примечания</span><span class="sxs-lookup"><span data-stu-id="f7715-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="f7715-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="f7715-333">**RegistryRead**</span></span> |<span data-ttu-id="f7715-334">Предоставляет доступ на чтение toohello удостоверение реестра.</span><span class="sxs-lookup"><span data-stu-id="f7715-334">Grants read access toohello identity registry.</span></span> <span data-ttu-id="f7715-335">Дополнительные сведения см. в разделе о [реестре удостоверений][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="f7715-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="f7715-336">Это разрешение используется серверными облачными службами.</span><span class="sxs-lookup"><span data-stu-id="f7715-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="f7715-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="f7715-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="f7715-338">Предоставление доступа чтения и записи toohello реестра удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f7715-338">Grants read and write access toohello identity registry.</span></span> <span data-ttu-id="f7715-339">Дополнительные сведения см. в разделе о [реестре удостоверений][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="f7715-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="f7715-340">Это разрешение используется серверными облачными службами.</span><span class="sxs-lookup"><span data-stu-id="f7715-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="f7715-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="f7715-341">**ServiceConnect**</span></span> |<span data-ttu-id="f7715-342">Предоставляет доступ к связи с выходом службы toocloud и мониторинг конечных точек.</span><span class="sxs-lookup"><span data-stu-id="f7715-342">Grants access toocloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="f7715-343">Предоставляет разрешение tooreceive устройства в облако сообщений, отправки сообщений облака на устройство и получить hello соответствующего подтверждения доставки.</span><span class="sxs-lookup"><span data-stu-id="f7715-343">Grants permission tooreceive device-to-cloud messages, send cloud-to-device messages, and retrieve hello corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="f7715-344">Отправка подтверждения доставки tooretrieve предоставляет разрешения для файла.</span><span class="sxs-lookup"><span data-stu-id="f7715-344">Grants permission tooretrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="f7715-345">Предоставляет разрешение tooaccess устройства близнецы tooupdate теги нужными свойствами получить свойства отчета и выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="f7715-345">Grants permission tooaccess device twins tooupdate tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="f7715-346">Это разрешение используется серверными облачными службами.</span><span class="sxs-lookup"><span data-stu-id="f7715-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="f7715-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="f7715-347">**DeviceConnect**</span></span> |<span data-ttu-id="f7715-348">Предоставляет доступ к стороне toodevice конечных точек.</span><span class="sxs-lookup"><span data-stu-id="f7715-348">Grants access toodevice-facing endpoints.</span></span> <br/><span data-ttu-id="f7715-349">Предоставляет разрешение toosend устройства в облако сообщения и получать сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="f7715-349">Grants permission toosend device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="f7715-350">Предоставляет разрешение tooperform отправки файла на устройстве.</span><span class="sxs-lookup"><span data-stu-id="f7715-350">Grants permission tooperform file upload from a device.</span></span> <br/><span data-ttu-id="f7715-351">Предоставляет разрешение tooreceive устройства двойных требуемого свойства уведомления и обновления устройств двойных отчета свойства.</span><span class="sxs-lookup"><span data-stu-id="f7715-351">Grants permission tooreceive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="f7715-352">Передает файл tooperform предоставляет разрешение.</span><span class="sxs-lookup"><span data-stu-id="f7715-352">Grants permission tooperform file uploads.</span></span> <br/><span data-ttu-id="f7715-353">Это разрешение используют устройства.</span><span class="sxs-lookup"><span data-stu-id="f7715-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="f7715-354">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="f7715-354">Additional reference material</span></span>

<span data-ttu-id="f7715-355">Другие разделы ссылку в hello центра IoT руководстве для разработчиков:</span><span class="sxs-lookup"><span data-stu-id="f7715-355">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="f7715-356">[Конечные точки центра IoT] [ lnk-endpoints] описывает hello различные конечные точки, предоставляемые каждый центр IoT для операций времени выполнения и управления.</span><span class="sxs-lookup"><span data-stu-id="f7715-356">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="f7715-357">[Регулирование и квоты] [ lnk-quotas] описывает hello квот и регулирования, применяющимся toohello службы центра IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-357">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="f7715-358">[Пакеты SDK устройств и служб Azure IoT] [ lnk-sdks] списки hello языка различных пакетов SDK, которые можно использовать при разработке приложений, устройств и служб, которые взаимодействуют с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="f7715-358">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="f7715-359">[Язык запросов центра IoT] [ lnk-query] описывает hello язык запросов, можно использовать tooretrieve сведения из центра IoT близнецы устройства и заданий.</span><span class="sxs-lookup"><span data-stu-id="f7715-359">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="f7715-360">[Поддержка MQTT концентратора IoT] [ lnk-devguide-mqtt] приведены более подробные сведения о поддержке центра IoT протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="f7715-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7715-361">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7715-361">Next steps</span></span>

<span data-ttu-id="f7715-362">Теперь вы узнали, как toocontrol доступа центра IoT, можно получить в следующие разделы руководства разработчика центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="f7715-362">Now you have learned how toocontrol access IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="f7715-363">[Конфигурации и состояния toosynchronize близнецы устройства][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="f7715-363">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="f7715-364">[Вызов прямого метода на устройстве (предварительная версия)][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="f7715-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="f7715-365">[Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="f7715-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="f7715-366">При желании tootry некоторые основные понятия hello, описанных в этой статье, могут быть интересны следующие учебники центра IoT hello параметры:</span><span class="sxs-lookup"><span data-stu-id="f7715-366">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="f7715-367">[Приступая к работе с Центром Интернета вещей Azure][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f7715-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="f7715-368">[Способ сообщений toosend облака на устройство с центром IoT][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f7715-368">[How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="f7715-369">[Как tooprocess сообщения из устройства в облако центра IoT][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f7715-369">[How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

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
