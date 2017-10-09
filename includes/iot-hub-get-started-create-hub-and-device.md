## <a name="create-an-iot-hub"></a>Создание центра IoT

1. В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **Интернета вещей** > **центр IoT**.

   ![Создать центр IoT в hello портал Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. В hello **центр IoT** области введите следующие сведения для вашего центра IoT hello:

     **Имя**: Введите имя вашего центра IoT hello. Если вы вводите имя hello допустим, отображается зеленая галочка.

     **Ценах и масштабировании уровня**: выберите hello **F1 - свободного** уровня. Этот вариант подойдет для этой демонстрационной версии. Дополнительные сведения см. в разделе hello [Ценовая категория и категория масштабирования](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Группа ресурсов**: создание концентратора IoT hello toohost группы ресурсов или используйте существующую. Дополнительные сведения см. в разделе [toomanage группы на использование ресурсов, ресурсов Azure](../articles/azure-resource-manager/resource-group-portal.md).

     **Расположение**: выберите hello ближайший tooyou расположение, где создается центра IoT hello.

     **ПИН-код toodashboard**: выберите этот параметр для облегчения доступа центра IoT tooyour из панели мониторинга hello.

   ![Введите сведения toocreate ваш центр IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. Щелкните **Создать**. Концентратор IoT может занять несколько минут toocreate. Вы увидите ход выполнения в hello **уведомления** области.

   ![Просмотр уведомлений о ходе создания Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. После создания вашего центра IoT, щелкните его на панели мониторинга hello. Запишите hello **Hostname**, а затем нажмите кнопку **политики общего доступа**.

   ![Получение имени узла hello из вашего центра IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. В hello **политики общего доступа** панели щелкните hello **iothubowner** политики и затем копировать и запишите hello **строка подключения** из вашего центра IoT. Дополнительные сведения см. в разделе [tooIoT управления доступом концентратора](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
Строка подключения iothubowner в этом руководстве по установке не понадобится. Тем не менее может потребоваться его для некоторых учебников hello в различных сценариях IoT после завершения этой установки.

   ![Получение строки подключения Центра Интернета вещей](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Регистрация устройства в центр IoT hello для устройства

1. В hello [портал Azure](https://portal.azure.com/), откройте ваш центр IoT.

2. Щелкните **Обозреватель устройств**.
3. В панели проводника устройства hello, щелкните **добавить** tooadd концентратор IoT tooyour устройства. Затем hello следующие:

   **Идентификатор устройства**: Введите идентификатор hello hello новое устройство. Идентификаторы устройств чувствительны к регистру.

   **Тип проверки подлинности.** Выберите **Симметричный ключ**.

   **Auto Generate Keys** (Автоматическое создание ключей). Установите флажок.

   **Подключение устройства tooIoT концентратора**: щелкните **включить**.

   ![Добавление устройства в hello обозреватель устройств из вашего центра IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Щелкните **Сохранить**.
5. После создания устройства Привет открыть устройство hello в hello **обозреватель устройств** области.
6. Запишите первичный ключ hello hello строки соединения.

   ![Получить строку подключения устройства hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
