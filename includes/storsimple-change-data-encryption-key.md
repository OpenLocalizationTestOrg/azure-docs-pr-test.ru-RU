<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>Шаг 1: Авторизуйте устройство toochange hello ключ шифрования данных службы в hello классический портал Azure
Как правило Здравствуйте, администратор устройства отправит запрос, администратор службы hello авторизовать ключи шифрования устройства toochange службы данных. Здравствуйте, администратор службы, затем авторизует ключ hello toochange hello устройства.

Этот шаг выполняется в hello классический портал Azure. Здравствуйте, администратор службы можно выбрать устройство из отображаемого списка устройств hello подходящих toobe авторизован. Hello устройство является затем процесс изменения ключа шифрования данных службы авторизованным toostart hello.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Устройства, которые можно авторизовать ключи шифрования данных службы toochange?
Устройства должны удовлетворять следующие критерии перед изменений ключа шифрования данных службы авторизованным tooinitiate hello.

* Hello устройство должно быть online toobe, подходящих для авторизации изменения ключа шифрования данных службы.
* Вы можете разрешить одно устройство еще раз через 30 минут, если изменения ключа hello не было инициировано приветствия.
* Можно авторизовать другое устройство, при условии, что изменение ключа hello не было инициировано ранее авторизованным устройством hello. После авторизации нового устройства hello hello старое устройство не может инициировать изменение hello.
* Не удается авторизовать устройство hello смену ключей шифрования данных службы hello во время выполнения.
* Можно авторизовать устройство, если некоторые hello устройства, зарегистрированные в службе hello отменены hello шифрования, а другие — нет. В таких случаях hello устройства являются те, которые выполнены изменения ключа шифрования данных службы hello hello.

> [!NOTE]
> В hello классический портал Azure StorSimple, виртуальные устройства не отображаются в списке hello устройств, которые могут быть авторизован изменение ключа toostart hello.
> 
> 

Выполните следующие шаги tooselect hello и авторизуйте устройство tooinitiate hello службы изменения ключа шифрования данных.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize ключ hello toochange устройства
1. На странице панели мониторинга службы hello щелкните **изменение ключа шифрования данных службы**.
   
    ![Изменение ключа шифрования службы](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. В hello **изменение ключа шифрования данных службы** диалогового окна выберите и авторизуйте устройство tooinitiate hello службы изменения ключа шифрования данных. Hello раскрывающегося списка имеет все hello доступных устройств, которым можно авторизовать.
3. Щелкните значок галочки hello ![значок галочки](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Шаг 2: Использование Windows PowerShell для StorSimple tooinitiate hello службы изменения ключа шифрования данных
Этот шаг выполняется в hello Windows PowerShell для StorSimple интерфейс hello авторизации устройства StorSimple.

> [!NOTE]
> Нет операции могут выполняться в hello классический портал Azure службе StorSimple Manager до завершения hello смены ключей.
> 
> 

При использовании hello устройство последовательной консоли tooconnect toohello в интерфейсе Windows PowerShell выполните следующие шаги hello.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>изменить ключ шифрования данных службы tooinitiate hello
1. Выберите вариант 1 toolog с полным доступом.
2. Hello командной строки введите следующую команду:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. После успешного завершения hello командлета вы получите новый ключ шифрования данных службы. Скопируйте и сохраните этот ключ для использования на шаге 3. Этот ключ будет использовать tooupdate все hello оставшихся устройства, зарегистрированные в службе StorSimple Manager hello.
   
   > [!NOTE]
   > Этот процесс должен быть запущен в течение четырех часов авторизации устройства StorSimple.
   > 
   > 
   
   Затем этот новый ключ отправляется toohello службы toobe помещается tooall hello устройств, зарегистрированных в службе hello. Предупреждение появится на панели мониторинга службы hello. Hello службы приведет к отключению всех операций hello на устройствах, зарегистрированных hello и администратора устройства hello затем потребуется ключ шифрования данных службы hello tooupdate на hello других устройств. Однако hello операций ввода-вывода (компьютеры, отправляющие облако toohello данных) не будут прерваны.
   
   При наличии одного устройства зарегистрированные службы tooyour, hello процесс смены завершен, hello следующий шаг можно пропустить. При наличии нескольких устройств зарегистрированных tooyour службы продолжить toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Шаг 3: Обновите ключ шифрования данных службы hello на других устройствах StorSimple
Эти действия должны выполняться в hello в интерфейсе Windows PowerShell устройства StorSimple, при наличии нескольких tooyour зарегистрированных устройств в службе StorSimple Manager. Hello ключ, полученный на шаге 2: с помощью Windows PowerShell для StorSimple tooinitiate hello службы изменения ключа шифрования данных должен быть используется tooupdate все hello оставшихся зарегистрированы в службе StorSimple Manager hello устройства StorSimple.

Выполните hello после шифрования данных службы hello tooupdate действия на устройстве.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>ключ шифрования данных службы tooupdate hello
1. С помощью Windows PowerShell для StorSimple tooconnect toohello консоли. Выберите вариант 1 toolog с полным доступом.
2. Hello командной строки введите следующую команду:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Укажите ключ шифрования данных службы hello, полученный в [шаг 2: с помощью Windows PowerShell для StorSimple tooinitiate hello службы изменения ключа шифрования данных](#to-initiate-the-service-data-encryption-key-change).

