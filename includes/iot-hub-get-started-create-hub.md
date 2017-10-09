## <a name="create-an-iot-hub"></a>Создание центра IoT
Создаете центр IoT для вашей tooconnect приложения имитированное устройство для. Hello следующие шаги показывают, как toocomplete это задач с помощью hello портал Azure.

1. Войдите в toohello [портал Azure][lnk-portal].
1. В hello Jumpbar щелкните **New** > **Интернета вещей** > **центр IoT**.
   
    ![Навигационная панель портала Azure][1]
1. В hello **центр IoT** колонке выберите конфигурацию hello для вашего центра IoT.
   
    ![Колонка "Центр Интернета вещей"][2]
   
   1. В hello **имя** введите имя для вашего центра IoT. Если hello **имя** действителен и доступных, отображается зеленая галочка в hello **имя** поле.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Выберите [уровень цен и масштабирования][lnk-pricing]. Для этого руководства задавать определенный уровень не нужно. В этом учебнике используется уровень free F1 hello.
   1. В разделе **Группа ресурсов** создайте новую группу ресурсов или выберите существующую. Дополнительные сведения см. в разделе [с помощью ресурса группы toomanage ресурсам Azure][lnk-resource-groups].
   1. В **расположение**, выберите hello toohost расположение вашего центра IoT. В этом руководстве следует выбрать ближайшее к вам расположение.
1. Выбрав параметры конфигурации центра IoT, нажмите кнопку **Создать**.  Он может занять несколько минут для Azure toocreate концентратор IoT. состояние toocheck hello, позволяющее наблюдать за hello на начальной панели hello или на панели уведомлений hello.
   
    ![Состояние нового центра IoT][3]
1. При успешном создании центра IoT hello, щелкните hello новая Плитка для вашего центра IoT в колонке hello Azure портала tooopen hello hello новый центр IoT. Запишите hello **Hostname**, а затем нажмите кнопку **политики общего доступа**.
   
    ![Колонка нового центра IoT][4]
1. В hello **политики общего доступа** колонка, щелкните hello **iothubowner** политики, затем скопируйте и запишите hello строка подключения концентратора IoT hello **iothubowner** колонку. Дополнительные сведения см. в разделе [управления доступом к] [ lnk-access-control] в hello «Центра IoT руководство разработчика».
   
    ![Колонка "Политики общего доступа"][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
