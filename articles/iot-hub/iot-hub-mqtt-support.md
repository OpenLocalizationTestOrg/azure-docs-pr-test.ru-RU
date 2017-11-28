---
title: "Поддержка Azure IoT Hub MQTT aaaUnderstand | Документы Microsoft"
description: "Разработчик руководства — поддержка для устройств, подключающихся с помощью конечной точки центра IoT устройств с выходом tooan hello MQTT протокола. Содержит сведения о встроенной поддержке MQTT в hello Azure IoT пакеты SDK."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="be098-104">Взаимодействовать с помощью протокола MQTT hello концентратор IoT</span><span class="sxs-lookup"><span data-stu-id="be098-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="be098-105">Центр IoT позволяет toocommunicate устройств с hello центра IoT устройства конечные точки, использующие hello [MQTT v3.1.1] [ lnk-mqtt-org] протокола на порт 8883 или v3.1.1 MQTT по протоколу WebSocket на порте 443.</span><span class="sxs-lookup"><span data-stu-id="be098-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="be098-106">Центр IoT требует связи toobe все устройства, защищены с помощью TLS/SSL (таким образом, центр IoT не поддерживает небезопасные подключения через порт 1883).</span><span class="sxs-lookup"><span data-stu-id="be098-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="be098-107">Подключение tooIoT концентратора</span><span class="sxs-lookup"><span data-stu-id="be098-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="be098-108">Устройства можно использовать центр IoT tooan tooconnect протокола hello MQTT либо с помощью библиотек hello в hello [пакеты SDK Azure IoT] [ lnk-device-sdks] или напрямую с помощью протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="be098-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="be098-109">С помощью устройства hello пакеты SDK</span><span class="sxs-lookup"><span data-stu-id="be098-109">Using hello device SDKs</span></span>

<span data-ttu-id="be098-110">[Пакеты SDK] [ lnk-device-sdks] hello, поддержка протокола MQTT доступны для Java, Node.js, C, C# и Python.</span><span class="sxs-lookup"><span data-stu-id="be098-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="be098-111">устройство Hello SDK использовать hello Стандартная центра IoT соединения строки tooestablish концентратор IoT tooan соединения.</span><span class="sxs-lookup"><span data-stu-id="be098-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="be098-112">протокол MQTT toouse hello, hello клиентского протокола параметра должно быть установлено слишком**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="be098-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="be098-113">По умолчанию hello устройство пакеты SDK, подключить к hello tooan центр IoT **CleanSession** слишком установлен флаг**0** и использовать **QoS 1** для обмена сообщениями с центром IoT hello.</span><span class="sxs-lookup"><span data-stu-id="be098-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="be098-114">После перехода устройства подключенных tooan центра IoT, устройство hello SDK предоставлять методы, которые включить toosend сообщений hello устройства, tooand получать сообщения от центра IoT.</span><span class="sxs-lookup"><span data-stu-id="be098-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="be098-115">Hello Следующая таблица содержит примеры toocode ссылки для каждого поддерживаемого языка и указывает hello параметр toouse tooestablish tooIoT подключение концентратора с помощью протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="be098-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="be098-116">Язык</span><span class="sxs-lookup"><span data-stu-id="be098-116">Language</span></span> | <span data-ttu-id="be098-117">Параметр протокола</span><span class="sxs-lookup"><span data-stu-id="be098-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="be098-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="be098-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="be098-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="be098-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="be098-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="be098-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="be098-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="be098-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="be098-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="be098-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="be098-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="be098-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="be098-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="be098-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="be098-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="be098-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="be098-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="be098-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="be098-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="be098-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="be098-128">Миграция приложения для устройств с AMQP tooMQTT</span><span class="sxs-lookup"><span data-stu-id="be098-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="be098-129">Если вы используете hello [устройства SDK][lnk-device-sdks], переключение с помощью AMQP tooMQTT, необходимо изменить параметр протокола hello в инициализации клиента hello как уже говорилось ранее.</span><span class="sxs-lookup"><span data-stu-id="be098-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="be098-130">При этом убедитесь, что hello toocheck следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="be098-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="be098-131">AMQP возвращает ошибки для многих условий во время MQTT разрывает подключение hello.</span><span class="sxs-lookup"><span data-stu-id="be098-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="be098-132">В результате может потребоваться изменить логику обработки исключений.</span><span class="sxs-lookup"><span data-stu-id="be098-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="be098-133">MQTT не поддерживает hello *Отклонить* операции при получении [сообщений облака на устройство][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="be098-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="be098-134">Если ваше приложение серверной части должно tooreceive ответа от устройства приложение hello, рассмотрите возможность использования [прямой методы][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="be098-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="be098-135">Непосредственно с помощью протокола MQTT hello</span><span class="sxs-lookup"><span data-stu-id="be098-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="be098-136">Если устройство не может использовать устройство hello пакеты SDK, он по-прежнему подключиться toohello конечных точек открытый устройства на порт 8883 с использованием протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="be098-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="be098-137">В hello **CONNECT** пакетов hello устройство должно использовать hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="be098-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="be098-138">Для hello **ClientId** воспользуйтесь hello **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="be098-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="be098-139">Для hello **Username** поле `{iothubhostname}/{device_id}/api-version=2016-11-14`, где {iothubhostname} hello полный CName центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="be098-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="be098-140">Например, если hello концентратор IoT называется **contoso.azure devices.net** и hello имя устройства — **MyDevice01**, hello полный **Username** поле должно содержать `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="be098-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="be098-141">Для hello **пароль** поля, используйте маркер SAS.</span><span class="sxs-lookup"><span data-stu-id="be098-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="be098-142">Формат маркера SAS является приветствия Hello hello таким же как для hello HTTP и AMQP протоколы:</span><span class="sxs-lookup"><span data-stu-id="be098-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="be098-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="be098-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="be098-144">Дополнительные сведения о маркерах SAS toogenerate см в разделе hello устройства [маркеров безопасности с помощью центра IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="be098-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="be098-145">При тестировании, можно также использовать hello [обозреватель устройств] [ lnk-device-explorer] tooquickly средство создать токен SAS, который можно скопировать и вставить в собственный код:</span><span class="sxs-lookup"><span data-stu-id="be098-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="be098-146">Go toohello **управления** вкладке **обозреватель устройств**.</span><span class="sxs-lookup"><span data-stu-id="be098-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="be098-147">Щелкните **Маркер SAS** (вверху справа).</span><span class="sxs-lookup"><span data-stu-id="be098-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="be098-148">На **SASTokenForm**, выберите устройство в hello **DeviceID** раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="be098-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="be098-149">Задайте значение **срока жизни**.</span><span class="sxs-lookup"><span data-stu-id="be098-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="be098-150">Нажмите кнопку **формирования** toocreate срок действия токена.</span><span class="sxs-lookup"><span data-stu-id="be098-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="be098-151">Hello маркер SAS, которое создается, имеет следующую структуру: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="be098-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="be098-152">Здравствуйте, часть этого маркера toouse как hello **пароль** — с помощью MQTT tooconnect поля: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="be098-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="be098-153">MQTT подключение и отключение пакетов, центр IoT выдает событие hello **мониторинг операций** канала с дополнительной информацией, которые могут помочь tootroubleshoot проблемы с подключением.</span><span class="sxs-lookup"><span data-stu-id="be098-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="be098-154">Отправка сообщений из устройства в облако</span><span class="sxs-lookup"><span data-stu-id="be098-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="be098-155">После успешного подключения, устройство может отправлять сообщения tooIoT концентратора с помощью `devices/{device_id}/messages/events/` или `devices/{device_id}/messages/events/{property_bag}` как **имя раздела**.</span><span class="sxs-lookup"><span data-stu-id="be098-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="be098-156">Hello `{property_bag}` элемент включает сообщений toosend hello устройства с дополнительными свойствами в формате URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="be098-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="be098-157">Например:</span><span class="sxs-lookup"><span data-stu-id="be098-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="be098-158">Это `{property_bag}` элемент использует hello кодировкой как для строк запросов в протоколе hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="be098-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="be098-159">приложение Hello устройства можно также использовать `devices/{device_id}/messages/events/{property_bag}` как hello **название раздела будет** toodefine *будет сообщения* toobe пересланный телеметрии сообщение.</span><span class="sxs-lookup"><span data-stu-id="be098-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="be098-160">Центр Интернета вещей не поддерживает сообщения со вторым уровнем качества обслуживания.</span><span class="sxs-lookup"><span data-stu-id="be098-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="be098-161">Если приложение для устройства публикует сообщение с **QoS 2**, центр IoT закрывает hello сетевое подключение.</span><span class="sxs-lookup"><span data-stu-id="be098-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="be098-162">Центр Интернета вещей не сохраняет сообщения retain.</span><span class="sxs-lookup"><span data-stu-id="be098-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="be098-163">Если устройство отправляет сообщение hello **Сохранить** too1 установлен флаг, центр IoT добавляет hello **x-opt Сохранить** сообщение toohello свойств приложения.</span><span class="sxs-lookup"><span data-stu-id="be098-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="be098-164">В этом случае вместо сохранения hello сохранить сообщение, центр IoT передает toohello серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="be098-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="be098-165">Центр Интернета вещей поддерживает только одно активное подключение MQTT на устройство.</span><span class="sxs-lookup"><span data-stu-id="be098-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="be098-166">Любое новое соединение MQTT от имени hello таким же Идентификатором устройства вызывает центра IoT toodrop hello существующее подключение.</span><span class="sxs-lookup"><span data-stu-id="be098-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="be098-167">Дополнительные сведения см. в статье [Отправка и получение сообщений в Центре Интернета вещей][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="be098-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="be098-168">Получение сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="be098-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="be098-169">tooreceive сообщения из центра IoT, устройство необходимо подписаться с помощью `devices/{device_id}/messages/devicebound/#` как **фильтра разделов**.</span><span class="sxs-lookup"><span data-stu-id="be098-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="be098-170">Здравствуйте многоуровневого подстановочные  **#**  в hello фильтра разделов используется только tooallow hello устройства tooreceive дополнительные свойства в разделе имени hello.</span><span class="sxs-lookup"><span data-stu-id="be098-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="be098-171">Центр IoT не допускает использование hello hello  **#**  или **?**</span><span class="sxs-lookup"><span data-stu-id="be098-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="be098-172">для фильтрации вложенных разделов.</span><span class="sxs-lookup"><span data-stu-id="be098-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="be098-173">Поскольку центр IoT не брокера обмена сообщениями pub-sub общего назначения, он поддерживает только имена разделе документированы hello и фильтры разделов.</span><span class="sxs-lookup"><span data-stu-id="be098-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="be098-174">Hello устройства сообщения получены не из центра IoT, пока не будет успешно подписана конкретного устройства tooits конечной точки, представленный hello `devices/{device_id}/messages/devicebound/#` фильтра статьи.</span><span class="sxs-lookup"><span data-stu-id="be098-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="be098-175">После установления успешная подписка hello устройства начинается получение сообщений только облака на устройство, которые были отправлены tooit после hello срока действия подписки hello.</span><span class="sxs-lookup"><span data-stu-id="be098-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="be098-176">Если устройство hello подключается с **CleanSession** слишком установлен флаг**0**, hello подписки сохраняется в разных сеансах.</span><span class="sxs-lookup"><span data-stu-id="be098-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="be098-177">В этом случае hello в следующий раз, он соединяется с **CleanSession 0** hello устройство получает ожидающих сообщений, которые были отправлены tooit пока он был отключен.</span><span class="sxs-lookup"><span data-stu-id="be098-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="be098-178">Если устройство hello использует **CleanSession** слишком установлен флаг**1** , не получает сообщения из центра IoT пока она подписывается устройства tooits конечной точки.</span><span class="sxs-lookup"><span data-stu-id="be098-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="be098-179">Центр IoT доставляет сообщения с hello **имя раздела** `devices/{device_id}/messages/devicebound/`, или `devices/{device_id}/messages/devicebound/{property_bag}` при наличии любого свойства сообщения.</span><span class="sxs-lookup"><span data-stu-id="be098-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="be098-180">`{property_bag}` содержит закодированные в формате URL-адреса пары "ключ-значение" свойств сообщения.</span><span class="sxs-lookup"><span data-stu-id="be098-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="be098-181">Только для свойств приложения и задаваемое пользователем системные свойства (такие как **messageId** или **correlationId**) включаются в контейнере свойств hello.</span><span class="sxs-lookup"><span data-stu-id="be098-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="be098-182">Имена системных свойств имеют префикс hello  **$** , свойства приложения использование исходного имени свойства и hello без префикса.</span><span class="sxs-lookup"><span data-stu-id="be098-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="be098-183">Когда приложение устройства подписывается tooa раздела с **QoS 2**, центр IoT предоставляет максимальный уровень качества обслуживания 1 в hello **SUBACK** пакетов.</span><span class="sxs-lookup"><span data-stu-id="be098-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="be098-184">После этого центр IoT доставляет сообщения toohello устройства с помощью QoS 1.</span><span class="sxs-lookup"><span data-stu-id="be098-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="be098-185">Получение свойств двойника устройства</span><span class="sxs-lookup"><span data-stu-id="be098-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="be098-186">Во-первых, устройство подписывается слишком`$iothub/twin/res/#`, ответов tooreceive hello операции.</span><span class="sxs-lookup"><span data-stu-id="be098-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="be098-187">Затем он отправляет пустое сообщение tootopic `$iothub/twin/GET/?$rid={request id}`, заполненных значением **идентификатор запроса**. hello service отправляет ответное сообщение, содержащее данные двойных hello устройства в разделе `$iothub/twin/res/{status}/?$rid={request id}`, используя же hello  **Идентификатор запроса** как запрос hello.</span><span class="sxs-lookup"><span data-stu-id="be098-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="be098-188">Идентификатором запроса может быть любое допустимое значение свойства сообщения, как указано в статье [Отправка и получение сообщений в Центре Интернета вещей][lnk-messaging], а состояние проверяется как целое число.</span><span class="sxs-lookup"><span data-stu-id="be098-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="be098-189">текст ответа Hello содержит hello в разделе свойств двойных hello устройства:</span><span class="sxs-lookup"><span data-stu-id="be098-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="be098-190">текст Hello запись реестра идентификаторов hello ограничения toohello элемент «свойства», например:</span><span class="sxs-lookup"><span data-stu-id="be098-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="be098-191">приведены коды возможных состояний Hello.</span><span class="sxs-lookup"><span data-stu-id="be098-191">hello possible status codes are:</span></span>

|<span data-ttu-id="be098-192">Состояние</span><span class="sxs-lookup"><span data-stu-id="be098-192">Status</span></span> | <span data-ttu-id="be098-193">Описание</span><span class="sxs-lookup"><span data-stu-id="be098-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="be098-194">200</span><span class="sxs-lookup"><span data-stu-id="be098-194">200</span></span> | <span data-ttu-id="be098-195">Успешно</span><span class="sxs-lookup"><span data-stu-id="be098-195">Success</span></span> |
| <span data-ttu-id="be098-196">429</span><span class="sxs-lookup"><span data-stu-id="be098-196">429</span></span> | <span data-ttu-id="be098-197">Слишком много запросов (регулирование), как указано в статье [Reference - quotas and throttling][lnk-quotas] (Справочные материалы. Квоты и регулирование)</span><span class="sxs-lookup"><span data-stu-id="be098-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="be098-198">5**</span><span class="sxs-lookup"><span data-stu-id="be098-198">5**</span></span> | <span data-ttu-id="be098-199">ошибки сервера;</span><span class="sxs-lookup"><span data-stu-id="be098-199">Server errors</span></span> |

<span data-ttu-id="be098-200">Дополнительные сведения см. в статье [Двойники устройства][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="be098-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="be098-201">Обновление сообщаемых свойств двойника устройства</span><span class="sxs-lookup"><span data-stu-id="be098-201">Update device twin's reported properties</span></span>

<span data-ttu-id="be098-202">Hello Ниже описана последовательность как устройство обновляет hello сообщил свойства в двойных hello устройств в центре IoT:</span><span class="sxs-lookup"><span data-stu-id="be098-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="be098-203">Устройство, сначала необходимо подписаться toohello `$iothub/twin/res/#` ответов операции для раздела tooreceive hello из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="be098-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="be098-204">Устройство отправляет сообщение, содержащее двойных обновления hello устройства toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` раздела.</span><span class="sxs-lookup"><span data-stu-id="be098-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="be098-205">Это сообщение содержит значение **request id** (идентификатор запроса).</span><span class="sxs-lookup"><span data-stu-id="be098-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="be098-206">Здравствуйте службы, а затем отправляет ответное сообщение, содержащее hello новое значение ETag для hello коллекции свойств отчета в разделе `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="be098-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="be098-207">Это сообщение ответа, использует hello же **идентификатор запроса** как запрос hello.</span><span class="sxs-lookup"><span data-stu-id="be098-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="be098-208">текст сообщения Hello запроса содержит документ JSON, который предоставляет новые значения для отчета свойства (нет свойств или метаданных можно изменить).</span><span class="sxs-lookup"><span data-stu-id="be098-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="be098-209">Каждого элемента в документе JSON hello обновляет или добавьте соответствующий элемент hello в документе двойных устройства hello.</span><span class="sxs-lookup"><span data-stu-id="be098-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="be098-210">Набор элементов слишком`null`, удаляет hello элемент из hello, содержащий объект.</span><span class="sxs-lookup"><span data-stu-id="be098-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="be098-211">Например:</span><span class="sxs-lookup"><span data-stu-id="be098-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="be098-212">приведены коды возможных состояний Hello.</span><span class="sxs-lookup"><span data-stu-id="be098-212">hello possible status codes are:</span></span>

|<span data-ttu-id="be098-213">Состояние</span><span class="sxs-lookup"><span data-stu-id="be098-213">Status</span></span> | <span data-ttu-id="be098-214">Описание</span><span class="sxs-lookup"><span data-stu-id="be098-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="be098-215">200</span><span class="sxs-lookup"><span data-stu-id="be098-215">200</span></span> | <span data-ttu-id="be098-216">Успешно</span><span class="sxs-lookup"><span data-stu-id="be098-216">Success</span></span> |
| <span data-ttu-id="be098-217">400</span><span class="sxs-lookup"><span data-stu-id="be098-217">400</span></span> | <span data-ttu-id="be098-218">Недопустимый запрос.</span><span class="sxs-lookup"><span data-stu-id="be098-218">Bad Request.</span></span> <span data-ttu-id="be098-219">Неправильно сформированный JSON.</span><span class="sxs-lookup"><span data-stu-id="be098-219">Malformed JSON</span></span> |
| <span data-ttu-id="be098-220">429</span><span class="sxs-lookup"><span data-stu-id="be098-220">429</span></span> | <span data-ttu-id="be098-221">Слишком много запросов (регулирование), как указано в статье [Reference - quotas and throttling][lnk-quotas] (Справочные материалы. Квоты и регулирование)</span><span class="sxs-lookup"><span data-stu-id="be098-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="be098-222">5**</span><span class="sxs-lookup"><span data-stu-id="be098-222">5**</span></span> | <span data-ttu-id="be098-223">ошибки сервера;</span><span class="sxs-lookup"><span data-stu-id="be098-223">Server errors</span></span> |

<span data-ttu-id="be098-224">Дополнительные сведения см. в статье [Двойники устройства][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="be098-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="be098-225">Получение уведомлений об обновлении требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="be098-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="be098-226">Когда устройство подключено, центр IoT отправляет уведомления toohello разделе `$iothub/twin/PATCH/properties/desired/?$version={new version}`, который содержимым hello hello обновления, выполненные hello решения серверной части.</span><span class="sxs-lookup"><span data-stu-id="be098-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="be098-227">Например:</span><span class="sxs-lookup"><span data-stu-id="be098-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="be098-228">Как и для обновления свойств `null` средних значений, hello JSON объект удаляется элемент.</span><span class="sxs-lookup"><span data-stu-id="be098-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="be098-229">Центр Интернета вещей создает уведомления об изменении только в том случае, если устройства подключены.</span><span class="sxs-lookup"><span data-stu-id="be098-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="be098-230">Убедитесь, что hello tooimplement [потока повторного подключения устройства] [ lnk-devguide-twin-reconnection] tookeep hello требуемого свойства синхронизируются между центр IoT и приложение hello устройства.</span><span class="sxs-lookup"><span data-stu-id="be098-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="be098-231">Дополнительные сведения см. в статье [Двойники устройства][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="be098-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="be098-232">Ответ tooa прямой метод</span><span class="sxs-lookup"><span data-stu-id="be098-232">Respond tooa direct method</span></span>

<span data-ttu-id="be098-233">Во-первых, устройство имеет toosubscribe слишком`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="be098-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="be098-234">Центр IoT отправляет разделе toohello запросы метод `$iothub/methods/POST/{method name}/?$rid={request id}`с недопустимым JSON или пустой текст.</span><span class="sxs-lookup"><span data-stu-id="be098-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="be098-235">toorespond, hello устройство отправляет сообщение с допустимых данных JSON или разделе toohello пустым телом `$iothub/methods/res/{status}/?$rid={request id}`, где **идентификатор запроса** имеет toomatch hello в приветственное сообщение запроса, и **состояние** имеет toobe целое число .</span><span class="sxs-lookup"><span data-stu-id="be098-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="be098-236">Дополнительные сведения см. в статье [Прямые методы][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="be098-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="be098-237">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="be098-237">Additional considerations</span></span>

<span data-ttu-id="be098-238">В последнее соображение, если необходимо поведение toocustomize hello MQTT протокола со стороны hello облака, необходимо просмотреть hello [шлюз протокола Azure IoT] [ lnk-azure-protocol-gateway] , позволяющий toodeploy высокой производительности шлюз пользовательский протокол, который взаимодействует непосредственно с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="be098-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="be098-239">шлюз протокола Hello Azure IoT позволяет вы toocustomize hello протокола tooaccommodate brownfield MQTT развертывания устройств или других протоколов.</span><span class="sxs-lookup"><span data-stu-id="be098-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="be098-240">Однако при этом подходе необходимо запустить настраиваемый шлюз протокола и управлять им.</span><span class="sxs-lookup"><span data-stu-id="be098-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be098-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be098-241">Next steps</span></span>

<span data-ttu-id="be098-242">toolearn Дополнительные сведения о hello MQTT протокола, в разделе hello [документации MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="be098-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="be098-243">toolearn Дополнительные сведения о планировании развертывания центра IoT, см.:</span><span class="sxs-lookup"><span data-stu-id="be098-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="be098-244">[Каталог устройств, сертифицированных по программе Microsoft Azure Certified for IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="be098-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="be098-245">[Поддержка дополнительных протоколов для центра IoT][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="be098-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="be098-246">[Сравнение центра IoT и концентраторов событий][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="be098-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="be098-247">[Масштабирование центра IoT][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="be098-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="be098-248">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="be098-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="be098-249">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="be098-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="be098-250">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="be098-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
