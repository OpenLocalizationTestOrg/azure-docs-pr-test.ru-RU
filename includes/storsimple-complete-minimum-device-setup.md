<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>Установка минимального устройства StorSimple toocomplete hello
1. В hello **устройств** устройства выберите hello нажмите hello стрелку рядом с страница hello устройства имя toogo toohello конкретного устройства. 
   
    ![Страница "Устройства": устройство подключено](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. Щелкните значок быстрого запуска ![значок быстрого запуска](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) tooaccess hello страницу быстрого запуска устройства. Нажмите кнопку **выполните настройку** toostart hello **настройки устройства** мастера.
   
    ![Страница быстрого запуска устройства](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. На hello **основные параметры** страницы, hello следующие:
   
   1. Укажите **понятное имя** для устройства. Имя устройства по умолчанию Hello отражает сведения, такие как модель устройства hello и серийный номер. Понятное имя копии toomanage too64 символов можно назначить устройства.
   2. Набор hello **часовой пояс** на основе географического расположения hello в какой hello развертывается устройство. Устройство будет использовать заданный часовой пояс для всех запланированных операций.
   3. В разделе **Параметры DNS** укажите адрес для **дополнительного DNS-сервера**. При использовании IPv6 hello поле заполняется на основе префикса IPv6 hello, предоставленных в интерфейсе Windows PowerShell hello. 
      Если hello дополнительный DNS-сервер не настроен, будут разрешены toosave конфигурацию устройства.
   4. В списке интерфейсов iSCSI включите по крайней мере одну сеть для iSCSI. По крайней мере один сетевой интерфейс должен toobe облаком и один toobe поддержкой iSCSI. Интерфейс DATA 0 по умолчанию поддерживает облако.
      
      ![Базовые параметры минимальной настройки StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. Щелкните значок со стрелкой hello. ![Значок стрелки StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. На hello **сетевых интерфейсов** укажите hello фиксированных IP-адреса для контроллера 0 и контроллера 1. Если hello DATA 0 интерфейс был настроен для IPv4, hello фиксированных toobe необходимость адреса IP, представленные в hello формате IPv4. При указании префикса для конфигурации IPv6 hello фиксированные IP-адреса будут заполнены автоматически в этих полях.

    > [!NOTE] 
    > - фиксированные IP-адреса контроллера Hello toobe свободное IP-адресов в подсети hello, доступной по IP-адрес устройства hello.
    > - фиксированные IP-адреса для контроллера hello Hello используются для обслуживания устройств toohello обновления hello и таким образом hello фиксированные IP-адреса должен быть toohello tooconnect маршрутизацию и Интернет.

    ![Сетевые интерфейсы для минимальной настройки устройства StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. Щелкните значок галочки hello ![StorSimple галочка](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Возвратит устройство toohello **быстрый запуск** страницы.
   
   > [!NOTE]
   > Можно изменить все hello другие параметры устройства в любое время, обратившись к hello **Настройка** страницы.
   > 
   > 

![Доступно видео](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **Доступно видео**

Нажмите кнопку toowatch видео, в котором показано, как toocomplete hello минимальной настройки устройства, [здесь](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).

