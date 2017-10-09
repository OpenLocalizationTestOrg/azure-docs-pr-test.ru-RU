<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>Установка минимального устройства StorSimple toocomplete hello
1. Выберите устройство hello и нажмите кнопку **быстрый запуск**. Нажмите кнопку **выполните настройку** мастера toostart hello и настройка устройств.
2. В мастере устройства Настройка hello **основные параметры** диалогового окна поле, hello следующие:
   
   1. Укажите **понятное имя** для устройства. Имя устройства по умолчанию Hello отражает сведения, такие как модель устройства hello и серийный номер. Понятное имя копии toomanage too64 символов можно назначить устройства.
   2. Набор hello **часовой пояс** на основе географического расположения hello в какой hello развертывается устройство. Устройство будет использовать заданный часовой пояс для всех запланированных операций.
   3. В разделе **Параметры DNS** укажите адрес для **дополнительного DNS-сервера**. При использовании IPv6 hello поле заполняется на основе префикса IPv6 hello, предоставленных в интерфейсе Windows PowerShell hello. 
      Если hello дополнительный DNS-сервер не настроен, будут разрешены toosave конфигурацию устройства.
   4. В списке интерфейсов iSCSI включите по крайней мере одну сеть для iSCSI. По крайней мере один сетевой интерфейс должен toobe облаком и один toobe поддержкой iSCSI. Интерфейс DATA 0 по умолчанию поддерживает облако.
      
      ![Базовые параметры минимальной настройки StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Щелкните значок со стрелкой hello. ![Значок стрелки StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. В hello **сетевых интерфейсов** диалогового окна введите hello фиксированных IP-адреса для контроллера 0 и контроллера 1. **фиксированные IP-адреса контроллера Hello toobe свободное IP-адресов в подсети hello, доступной по IP-адрес устройства hello.** Если hello DATA 0 интерфейс был настроен для IPv4, hello фиксированных toobe необходимость адреса IP, представленные в hello формате IPv4. При указании префикса для конфигурации IPv6 hello фиксированные IP-адреса будут заполнены автоматически в этих полях.

    ![Сетевые интерфейсы для минимальной настройки устройства StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    фиксированные IP-адреса для контроллера hello Hello используются для обслуживания устройств toohello обновления hello и таким образом hello фиксированные IP-адреса должен быть toohello tooconnect маршрутизацию и Интернет. Можно проверить, что контроллер фиксированный IP-адресов доступны для маршрутизации с помощью hello [Test-HcsmConnection] [ Test] командлета. Следующий пример показывает фиксированных IP-адреса контроллера являются перенаправленное toohello Интернет и доступ к Hello hello серверов центра обновления Майкрософт. 

     ![Test-HcsmConnection, показывающий маршрутизируемые IP-адреса](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Щелкните значок галочки hello ![StorSimple галочка](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Возвратит устройство toohello **быстрый запуск** страницы.
   
   > [!NOTE]
   > Можно изменить все hello другие параметры устройства в любое время, обратившись к hello **Настройка** страницы.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx