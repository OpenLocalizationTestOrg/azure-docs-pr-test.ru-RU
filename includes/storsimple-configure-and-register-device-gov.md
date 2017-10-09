<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure и зарегистрировать устройство hello
1. Доступ к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple. В разделе [последовательной консоли устройства toohello использование PuTTY tooconnect](#use-putty-to-connect-to-the-device-serial-console) инструкции. **Полностью toofollow убедиться, что процедура hello или не будет возможности tooaccess hello консоли.**
2. В сеансе hello, открывающемся нажмите клавишу ВВОД один раз tooget командную строку. 
3. Появится запрос toochoose hello язык, что tooset для вашего устройства. Укажите язык hello и нажмите клавишу ВВОД. 
   
    ![Настройка и регистрация StorSimple: устройство 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. В меню последовательной консоли hello, представленные выберите вариант 1 toolog на с полным доступом. 
   
    ![Регистрация StorSimple: устройство 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. Выполните следующие шаги tooconfigure hello минимальные необходимые параметры сети для устройства hello.
   
   > [!IMPORTANT]
   > Эти шаги по настройке должны toobe блокировкой hello активного контроллера устройства hello. меню последовательной консоли Hello указывает состояние контроллера hello в текст заголовка hello. Если не являются подключиться toohello активный контроллер, отключитесь и подключитесь toohello активного контроллера.
   > 
   > 
   
   1. Hello командной строки введите пароль. пароль устройства по умолчанию Hello **Password1**.
   2. Введите следующую команду hello:
      
        `Invoke-HcsSetupWizard`
   3. Мастер установки появится toohelp, настроить параметры сети hello hello устройства. Ввести hello следующую информацию: 
      
      * IP-адрес для сетевого интерфейса DATA 0
      * Маска подсети
      * Шлюз
      * IP-адрес основного DNS-сервера
      * IP-адрес основного NTP-сервера
      
      > [!NOTE]
      > Toowait может иметь несколько минут для маски подсети hello и применения toobe параметры DNS. 
      > 
      > 
   4. (Необязательно.) Настройте прокси-сервер доступа в Интернет.
      
      > [!IMPORTANT]
      > Хотя использовать прокси-сервер доступа в Интернет не обязательно, следует знать, что, если в вашей сети он имеется, настройку для работы с ним можно выполнить только в этом разделе. Дополнительные сведения см. слишком[Настройка веб-прокси для устройства](../articles/storsimple/storsimple-configure-web-proxy.md). 
      > 
      > 
6. Нажмите клавиши Ctrl + C мастер установки tooexit hello.
7. Установите обновления hello следующим образом:
   
   1. Используйте следующий командлет tooset IP-адресов на обоих контроллерах hello hello.
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. Hello командной строки, выполнив `Get-HcsUpdateAvailability`. Вы должны получить уведомление о доступности обновлений.
   3. Запустите `Start-HcsUpdate`. Эту команду можно выполнить на любом узле. Обновления будут применяться на первом контроллере hello, выполнит переход контроллера hello и затем hello обновления будут применяться на hello другой контроллер.
      
      Можно следить за ходом hello hello обновления, запустив `Get-HcsUpdateStatus`.    
      
      Hello следующий образец вывода показывает hello обновление выполняется.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      Следующий пример выходных данных Hello указывает, что завершения обновления hello.
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      Это может потребоваться до too11 часы Здравствуйте, tooapply все hello обновлений, включая обновления Windows.

8. После того как все hello обновления можно успешно установлена, запустите hello следующий командлет tooconfirm, Здравствуйте, правильно ли были применены обновления программного обеспечения:
   
     `Get-HcsSystem`
   
    Вы должны увидеть следующие версии hello.
   
   * HcsSoftwareVersion: 6.3.9600.17491
   * CisAgentVersion: 1.0.9037.0
   * MdsAgentVersion: 26.0.4696.1433
9. Верно ли был применен выполнения hello, выполнив командлет tooconfirm, hello обновление встроенного по:
   
    `Start-HcsFirmwareCheck`.
   
     состояние Hello встроенное по должно быть **: UpToDate**.
10. Запустите hello, следуя портал Microsoft Azure для государственных toohello устройств hello командлет toopoint (так как он указывает toohello открытый классического портала Azure по умолчанию). Оба контроллера будут перезапущены. Рекомендуется использовать два сеанса PuTTY, toosimultaneously подключения tooboth контроллеров, чтобы вы могли видеть при перезапуске каждого контроллера.
    
     `Set-CloudPlatform -AzureGovt_US`
    
    Появится сообщение подтверждения. Примите значение по умолчанию hello (**Y**).
11. Выполните командлет tooresume установке hello.
    
     `Invoke-HcsSetupWizard`
    
     ![Продолжение работы мастера установки](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    При возобновлении работы программы установки, мастер hello будет hello с обновлением 1 версии (соответствует tooversion 17469). 
12. Примите параметры сети hello. Вы увидите сообщение проверки после принятия каждого параметра.
13. В целях безопасности пароль администратора устройства hello срок действия истекает через hello первого сеанса, и нужно будет toochange теперь ИТ. При выводе запроса задайте пароль администратора устройства. Требуемая длина пароля администратора устройства от 8 до 15 символов. Hello пароль должен содержать символы трех из следующих hello: нижнем регистре, верхнем регистре, цифры и специальные символы.
    
    <br/>![Регистрация StorSimple: устройство 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. Последний шаг мастера установки hello Hello регистрирует устройство hello в службе StorSimple Manager. Для этого вам будет необходимо hello регистрационный ключ службы, полученный в [шаг 2: ключ регистрации службы hello Get](#step-2-get-the-service-registration-key). После ввода ключа регистрации hello, может понадобиться toowait 2-3 минуты до регистрации устройства hello.
    
    > [!NOTE]
    > В любое время мастер установки hello tooexit можно нажать клавиши Ctrl + C. Если введено все параметры сети hello (IP-адрес Data 0, маску подсети и шлюз) записей будут сохранены.
    > 
    > 
    
    ![Ход выполнения регистрации StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. После регистрации устройства hello отображается ключ шифрования данных службы. Скопируйте этот ключ и сохраните его в безопасном месте. **Этот ключ потребуется с hello службы регистрации ключа tooregister дополнительных устройств с hello в службе StorSimple Manager.** См. слишком[безопасность StorSimple](../articles/storsimple/storsimple-security.md) Дополнительные сведения об этом ключе.
    
    ![Регистрация StorSimple: устройство 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > текст hello toocopy из окна последовательной консоли hello, просто выделите текст hello. Затем можно будет toopaste его в буфер обмена hello или любой текстовый редактор. 
    > 
    > НЕ используйте сочетание клавиш Ctrl + C toocopy hello ключа шифрования. С помощью клавиши Ctrl + C вызовет вы tooexit приветствия мастера установки. В результате пароль администратора устройства hello не будут изменены и hello устройство вернется toohello пароль по умолчанию.
    > 
    > 
16. Выход hello последовательной консоли.
17. Вернитесь toohello государственных портал Azure и завершите hello следующие шаги:
    
    1. Дважды щелкните вашей hello tooaccess службы диспетчера StorSimple **быстрый запуск** страницы.
    2. Щелкните **Просмотр подключенных устройств**.
    3. На hello **устройств** проверьте hello устройства успешно подключен toohello службы путем поиска информации о состоянии hello. Состояние устройства Hello должно быть **Online**.
       
        ![Страница устройств StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        Если состояние устройства hello **Offline**, подождите несколько минут для hello toocome устройства через Интернет. 
       
        Если устройство hello еще в автономном режиме, через несколько минут, то необходимо убедиться, что брандмауэр сети была настроена, как описано в toomake [требования к сети для устройства StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Убедитесь, что порт 9354 открыт для исходящей связи используется hello служебной шины для диспетчера StorSimple устройство службы связи.

