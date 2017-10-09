<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure и зарегистрировать устройство hello

1. Доступ к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple. В разделе [последовательной консоли устройства toohello использование PuTTY tooconnect](#use-putty-to-connect-to-the-device-serial-console) инструкции. **Полностью toofollow убедиться, что процедура hello или не будет возможности tooaccess hello консоли.**

2. В сеансе hello, открывающемся, клавишу **ввод** один раз tooget командную строку.

3. Появится запрос toochoose hello язык, что tooset для вашего устройства. Указать язык hello и нажмите клавишу **ввод**.

4. В меню последовательной консоли hello, представленными в, выберите параметр 1 слишком**войти с полным доступом**.
     Выполните шаги с 5-12 tooconfigure hello минимальные необходимые параметры сети для устройства. **Эти шаги по настройке должны toobe блокировкой hello активного контроллера устройства hello.** меню последовательной консоли Hello указывает состояние контроллера hello в текст заголовка hello. Если вы не подключены toohello активный контроллер, отключите и подключите toohello активного контроллера.

5. Hello командной строки введите пароль. пароль устройства по умолчанию Hello **Password1**.

6. Тип hello следующую команду: `Invoke-HcsSetupWizard`.

7. Мастер установки появится toohelp, настроить параметры сети hello hello устройства. Ввести hello hello следующую информацию:
   
   * IP-адрес для hello сетевого интерфейса DATA 0
   * Маска подсети
   * Шлюз
   * IP-адрес основного DNS-сервера

   Ниже приведен пример выходных данных.

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    В hello предшествующий пример выходных данных вы увидите, что системы hello проверке параметров сети после каждого шага в процессе hello.

     > [!NOTE]
     > Toowait может иметь несколько минут для маски подсети hello и применены параметры toobe с DNS hello. Если появляется сообщение об ошибке «Проверка hello сетевого подключения tooData 0», проверьте hello физическое подключение hello сетевого интерфейса DATA 0 вашего используемого контроллера.

8. (Необязательно.) Настройте прокси-сервер доступа в Интернет. Хотя использовать веб-прокси не обязательно, **следует знать, что, если в вашей сети имеется веб-прокси, настройку для работы с ним можно выполнить только в этом разделе**. Дополнительные сведения см. слишком[Настройка веб-прокси для устройства](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Настройте основной NTP-сервер для своего устройства. NTP-серверы необходимы, так как ваше устройство должно синхронизироваться по времени, чтобы оно могло проверять подлинность с вашими поставщиками облачных служб. Убедитесь, что ваша сеть позволяет toopass трафик NTP из вашего центра обработки данных toohello Интернета. Если это невозможно, укажите внутренний NTP-сервер.

    Результат выполнения команды показан ниже.

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. В целях безопасности пароль администратора устройства hello срок действия истекает через hello первого сеанса, и нужно будет toochange теперь ИТ. При выводе запроса задайте пароль администратора устройства. Требуемая длина пароля администратора устройства от 8 до 15 символов. Hello пароль должен содержать символы трех из следующих hello: нижнем регистре, верхнем регистре, цифры и специальные символы.

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. Последний шаг мастера установки hello Hello регистрирует устройство hello службы диспетчера StorSimple устройство. Для этого потребуется ключ регистрации службы hello, полученный на шаге 2. После ввода ключа регистрации hello, может понадобиться toowait 2-3 минуты до регистрации устройства hello.
    
    > [!NOTE]
    > В любое время мастер установки hello tooexit можно нажать клавиши Ctrl + C. Если введено все параметры сети hello (IP-адрес Data 0, маску подсети и шлюз) записей будут сохранены.
    
    Результат выполнения команды показан ниже.

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. После регистрации устройства hello отображается ключ шифрования данных службы. Скопируйте этот ключ и сохраните его в безопасном месте. **Этот ключ потребуется с hello службы регистрации ключа tooregister дополнительных устройств с hello службы диспетчера StorSimple устройство.** См. слишком[безопасность StorSimple](../articles/storsimple/storsimple-security.md) Дополнительные сведения об этом ключе.
    
    ![Регистрация StorSimple: устройство 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > текст hello toocopy из окна последовательной консоли hello, просто выделите текст hello. Затем можно будет toopaste его в буфер обмена hello или любой текстовый редактор. НЕ используйте сочетание клавиш Ctrl + C toocopy hello ключа шифрования. С помощью клавиши Ctrl + C вызовет вы tooexit приветствия мастера установки. В результате пароль администратора устройства hello не будут изменены и hello устройство вернется toohello пароль по умолчанию.
    
13. Выход hello последовательной консоли.
14. Получите toohello портал Azure и выполните следующие шаги hello.
    
    1. Перейдите в службе диспетчера StorSimple устройство tooyour.
    2. Щелкните **Устройства**.
    3. Hello табличный список устройств убедитесь, что в это устройство hello успешно подключен toohello службы путем поиска информации о состоянии hello. Состояние устройства Hello должно быть **готов tooset копирование**.
       
        ![Страница устройств StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Может потребоваться toowait для несколько минут для toochange состояние устройства hello слишком**готов tooset копирование**.
       
        Если hello устройство не отображается в этом списке, то вы должны убедиться, что брандмауэр сети была настроена, как описано в toomake [требования к сети для устройства StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md). Убедитесь, что порт 9354 открыт для исходящей связи используется hello служебной шины для устройства StorSimple устройство службы связи.

