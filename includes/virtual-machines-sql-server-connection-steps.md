### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Откройте TCP-порты в брандмауэре Windows hello для экземпляра по умолчанию hello hello компонент Database Engine
1. Подключите toohello виртуальную машину с помощью удаленного рабочего стола. Подробные инструкции по подключению toohello виртуальной Машины в разделе [открыть SQL виртуальной Машины с помощью удаленного рабочего стола](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. После входа на начальный экран приветствия, введите **WF.msc**и нажмите клавишу ВВОД.
   
    ![Запуск программы брандмауэра hello](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. В hello **брандмауэр Windows в режиме повышенной безопасности**в hello левой панели, щелкните правой кнопкой мыши **правила для входящих подключений**, а затем нажмите кнопку **новое правило** в области действий hello.
   
    ![Создать правило](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. В hello **правило мастера** диалогового **тип правила**выберите **порт**, а затем нажмите кнопку **Далее**.
5. В hello **протокол и порты** диалоговое окно, по умолчанию hello **TCP**. В hello **определенные локальные порты** поле, а затем тип hello номер_порта hello экземпляр компонента Database Engine hello (**1433** для экземпляра по умолчанию hello или выбор для hello частный порт конечной точки шаге hello).
   
    ![TCP-порт 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. Щелкните **Далее**.
7. В hello **действия** установите флажок **разрешить подключение hello**, а затем нажмите кнопку **Далее**.
   
    **Примечание по безопасности:** при выборе **разрешить подключение hello безопасное** позволяет повысить уровень безопасности. Выберите этот параметр, если требуется tooconfigure другие параметры безопасности в вашей среде.
   
    ![Разрешить подключения](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. В hello **профиль** выберите **открытый**, **закрытый**, и **домена**. Нажмите кнопку **Далее**.
   
    **Примечание по безопасности:** при выборе **открытый** разрешает доступ через Интернет hello. Во всех возможных случаях выбирайте более строгий профиль.
   
    ![Открытый профиль](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. В hello **имя** диалоговое окно, введите имя и описание для этого правила и нажмите кнопку **Готово**.
   
    ![Имя правила](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

При необходимости откройте дополнительные порты для других компонентов. Дополнительные сведения см. в разделе [Настройка брандмауэра Windows hello tooAllow доступа к SQL Server](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>Настройка SQL Server toolisten на hello протокола TCP

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>Настройка SQL Server на проверку подлинности в смешанном режиме
без среды домена Hello SQL Server Database Engine не может использовать проверку подлинности Windows. toohello tooconnect компонент Database Engine с другого компьютера настройте SQL Server для смешанного режима проверки подлинности. Смешанный режим позволяет выполнять проверку подлинности SQL Server и проверку подлинности Windows.

> [!NOTE]
> Настройка аутентификации в смешанном режиме может быть необязательна, если вы настроили виртуальную сеть Azure с помощью настроенной доменной среды.
> 
> 

1. При подключенном toohello виртуальной машины на начальной странице hello, типа **SQL Server Management Studio** и щелкните значок выбранного hello.
   
    Здравствуйте, первый раз при открытии среды Management Studio, его необходимо создать среду Management Studio hello пользователей. Это может занять несколько минут.
2. Среда Management Studio предоставляет hello **подключения tooServer** диалоговое окно. В hello **имя сервера** введите имя hello из виртуальной машины hello tooconnect toohello компонент Database Engine с hello обозревателя объектов (вместо hello имя виртуальной машины, можно также использовать **(local)** или один период как hello **имя сервера**). Выберите **проверки подлинности Windows**и оставить  ***your_VM_name*\your_local_administrator** в hello **имя пользователя** поле. Щелкните **Подключить**.
   
    ![Подключение tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. В SQL Server Management Studio обозревателе объектов щелкните правой кнопкой мыши имя hello hello экземпляра SQL Server (имя виртуальной машины hello) и нажмите кнопку **свойства**.
   
    ![Свойства сервера](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. На hello **безопасности** в разделе **проверки подлинности сервера**выберите **режим SQL Server и проверка подлинности Windows**, а затем нажмите кнопку **ОК** .
   
    ![Выберите режим проверки подлинности](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. В SQL Server Management Studio диалоговое окно «hello», щелкните **ОК** tooacknowledge hello требование toorestart SQL Server.
6. В обозревателе объектов щелкните сервер правой кнопкой мыши и выберите **Перезагрузить**. (Если выполняется агент SQL Server, его также нужно перезапустить).
   
    ![Перезагрузить](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. В SQL Server Management Studio диалоговое окно «hello», щелкните **Да** tooagree, что требуется toorestart SQL Server.

### <a name="create-sql-server-authentication-logins"></a>Создание учетных записей проверки подлинности SQL Server
tooconnect toohello компонент Database Engine с другого компьютера, необходимо создать по крайней мере одно имя входа проверки подлинности SQL Server.

1. В SQL Server Management Studio обозревателе объектов разверните папку hello hello экземпляра сервера, в котором нужно создать имя входа hello toocreate.
2. Щелкните правой кнопкой мыши hello **безопасности** папки, точки слишком**New**и выберите **входа...** .
   
    ![Новая учетная запись](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. В hello **Создание имени входа** диалоговом на hello **Общие** введите имя нового пользователя hello hello в hello **имя входа** поле.
4. Выберите **Проверка подлинности SQL Server**.
5. В hello **пароль** введите пароль для нового пользователя hello. Введите пароль еще раз в hello **подтверждение пароля** поле.
6. Выберите параметры применения пароля hello, необходимые (**требовать использование политики паролей**, **срока действия паролей**, и **потребовать смену пароля при следующем входе**). При использовании этого имени входа для себя toorequire изменения пароля при следующем входе hello не обязательно.
7. Из hello **база данных по умолчанию** выберите базу данных по умолчанию для имени входа hello. **Главный** hello по умолчанию для этого параметра. Если вы еще не создали пользовательскую базу данных, оставьте выбранным слишком**master**.
   
    ![Свойства учетной записи](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Если это hello первого входа в систему создаваемого можно toodesignate это имя входа от имени администратора SQL Server. В этом случае на hello **ролей сервера** установите флажок **sysadmin**.
   
   > [!NOTE]
   > Члены фиксированной серверной роли sysadmin hello имеют полный контроль над hello компонента Database Engine. Количество представителей этой роли нужно ограничить.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Нажмите кнопку ОК.

Более подробные сведения об учетных записях SQL Server см. в статье [Создание имени входа](http://msdn.microsoft.com/library/aa337562.aspx).

