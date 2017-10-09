## <a name="create-a-device-identity"></a>Создание удостоверения устройства

В этом разделе используется hello [портал Azure] [ lnk-azure-portal] toocreate удостоверение устройства в реестре hello identity в вашего центра IoT. Устройство не удается подключиться tooIoT концентратора, если оно не имеет запись в реестре удостоверений hello. Дополнительные сведения см. в разделе hello раздел «Удостоверение реестра» hello [руководстве для разработчиков центра IoT][lnk-devguide-identity]. Hello **обозреватель устройств** hello портал помогает создать уникальный идентификатор устройства и ключ, что устройство может использовать tooidentify себя при соединении tooIoT концентратора. Идентификаторы устройств чувствительны к регистру.

1. Убедитесь, что вы вошли в toohello [портал Azure][lnk-azure-portal].

1. В hello Jumpbar щелкните **все ресурсы** и ресурс концентратора IoT.

    ![Перейдите в центр Iot tooyour][img-find-iothub]

1. При открытии ресурса концентратора IoT щелкните hello **обозреватель устройств** инструмент, а затем нажмите кнопку **добавить** вверху hello. Укажите имя hello для нового устройства, например **myDeviceId**и нажмите кнопку **Сохранить**.

    ![Создание удостоверения устройства на портале][img-create-device]

   После этого будет создано удостоверение устройства для вашего Центра Интернета вещей.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. В hello **обозреватель устройств**в список устройств, выберите только что созданный hello устройство и запишите hello **строка подключения---первичный ключ**. 

    ![Строка подключения к устройству.][img-connection-string]

> [!NOTE]
> Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT. Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности, а также включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств. Если приложению toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения. Дополнительные сведения см. в [руководстве разработчика по Центру Интернета вещей][lnk-devguide-identity].

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

