<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure и зарегистрировать устройство hello
1. Доступ к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple. В разделе [последовательной консоли устройства toohello использование PuTTY tooconnect](#use-putty-to-connect-to-the-device-serial-console) инструкции. **Полностью toofollow убедиться, что процедура hello или не будет возможности tooaccess hello консоли.**
2. В сеансе hello, открывающемся нажмите клавишу ВВОД один раз tooget командную строку. 
3. Появится запрос toochoose hello язык, что tooset для вашего устройства. Укажите язык hello и нажмите клавишу ВВОД. 
   
    ![Настройка и регистрация StorSimple: устройство 1](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. В меню последовательной консоли hello, представленные выберите вариант 1 toolog на с полным доступом. 
   
    ![Регистрация StorSimple: устройство 2](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Выполните шаги с 5-12 tooconfigure hello минимальные необходимые параметры сети для устройства. **Эти шаги по настройке должны toobe блокировкой hello активного контроллера устройства hello.** меню последовательной консоли Hello указывает состояние контроллера hello в текст заголовка hello. Если вы не подключены toohello активный контроллер, отключите и подключите toohello активного контроллера.
5. Hello командной строки введите пароль. пароль устройства по умолчанию Hello **Password1**.
6. Введите следующую команду hello:
   
     `Invoke-HcsSetupWizard` 
7. Мастер установки появится toohelp, настроить параметры сети hello hello устройства. Ввести hello hello следующую информацию: 
   
   * IP-адрес для hello сетевого интерфейса DATA 0
   * Маска подсети
   * Шлюз
   * IP-адрес основного DNS-сервера
   * IP-адрес основного NTP-сервера
     
     > [!NOTE]
     > Toowait может иметь несколько минут для маски подсети hello и применены параметры toobe с DNS hello. Если вы получаете «hello устройство не готово.» сообщение об ошибке проверки hello физическое подключение hello сетевого интерфейса DATA 0 вашего используемого контроллера.
     > 
     > 
8. (Необязательно.) Настройте прокси-сервер доступа в Интернет. Хотя использовать веб-прокси не обязательно, **следует знать, что, если в вашей сети имеется веб-прокси, настройку для работы с ним можно выполнить только в этом разделе**. Дополнительные сведения см. слишком[Настройка веб-прокси для устройства](../articles/storsimple/storsimple-configure-web-proxy.md). Если возникли проблемы во время выполнения этого шага см. руководство tootroubleshooting для [ошибки во время настройки веб-прокси](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > В любое время мастер установки hello tooexit можно нажать клавиши Ctrl + C. Все параметры, примененные перед использованием этой команды, будут сохранены.

1. В целях безопасности пароль администратора устройства hello срок действия истекает через hello первого сеанса, и нужно будет toochange его для последующих сеансов. При выводе запроса задайте пароль администратора устройства. Требуемая длина пароля администратора устройства от 8 до 15 символов. Hello пароль должен содержать сочетание строчные буквы, прописные буквы, цифры и специальные символы.
2. пароль диспетчера моментальных снимков StorSimple Hello также задается здесь. Этот пароль используется только при проверке подлинности устройства на узле Windows, на котором запущен Диспетчер моментальных снимков StorSimple. При появлении запроса введите пароль 14 too15 символов. Hello пароль должен содержать сочетание любых трех следующих hello: нижнем регистре, верхнем регистре, цифры и специальные символы. 
   
   ![Регистрация StorSimple: устройство 4](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   Вы можете сбросить пароль диспетчера моментальных снимков StorSimple hello от интерфейса службы диспетчера StorSimple hello. Подробные инструкции см. слишком[изменения паролей hello StorSimple, с помощью службы диспетчера StorSimple hello](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot проблем на этом этапе см. руководство tootroubleshooting для [ошибок, связанных с toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. Последний шаг мастера установки hello Hello регистрирует устройство hello в службе StorSimple Manager. Для этого потребуется ключ регистрации службы hello, полученный на шаге 2. После ввода ключа регистрации hello, может понадобиться toowait 2-3 минуты до регистрации устройства hello.
   
   tootroubleshoot сбоев регистрации устройства можно ссылаться слишком[ошибки во время регистрации устройства](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Сведения о Устранение неполадок, можно также ссылаться слишком[пример с пошаговыми инструкциями по устранению неполадок](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. После регистрации устройства hello отображается ключ шифрования данных службы. Скопируйте этот ключ и сохраните его в безопасном месте.
   
   > [!WARNING]
   > Этот ключ потребуется с hello службы регистрации ключа tooregister дополнительных устройств с hello в службе StorSimple Manager. См. слишком[безопасность StorSimple](../articles/storsimple/storsimple-security.md) Дополнительные сведения об этом ключе.
   > 
   > 
   
    ![Регистрация StorSimple: устройство 6](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    текст hello toocopy из окна последовательной консоли hello, просто выделите текст hello. Затем можно будет toopaste его в буфер обмена hello или любой текстовый редактор. НЕ используйте сочетание клавиш Ctrl + C toocopy hello ключа шифрования. С помощью клавиши Ctrl + C вызовет вы tooexit приветствия мастера установки. В результате пароль администратора устройства hello и пароль диспетчера моментальных снимков StorSimple hello не будут изменены и hello устройство вернется toohello паролей по умолчанию.
5. Выход hello последовательной консоли.
6. Получите toohello классический портал Azure и выполните следующие шаги hello.
   
   1. Дважды щелкните вашей hello tooaccess службы диспетчера StorSimple **быстрый запуск** страницы.
   2. Щелкните **Просмотр подключенных устройств**.
   3. На hello **устройств** проверьте hello устройства успешно подключен toohello службы путем поиска информации о состоянии hello. Состояние устройства Hello должно быть **Online**. Если состояние устройства hello **Offline**, подождите несколько минут для hello toocome устройства через Интернет.
   
   ![Страница устройств StorSimple](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > После hello устройство находится в оперативном режиме, подключите кабели сети hello, не подключены в начале этого шага hello.
   > 
   > 

После hello устройство успешно зарегистрировано и не переходит в оперативный режим, можно запустить hello `Test-HcsmConnection -Verbose` tooensure, hello сетевое подключение находится в работоспособном состоянии. Hello подробные сведения об использовании этого командлета см. слишком[Справочник по командлетам для Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx).

![Доступно видео](./media/storsimple-configure-and-register-device/Video_icon.png) **Доступно видео**

toowatch видео, в котором показано, как tooconfigure и регистрация устройства через Windows PowerShell для StorSimple, нажмите кнопку [здесь](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).

