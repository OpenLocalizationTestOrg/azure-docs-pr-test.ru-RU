### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Настроить метку для hello общедоступный IP-адрес DNS

toohello tooconnect SQL Server Database Engine из Интернета, hello рекомендуется создать метку DNS вашего общедоступного IP-адреса. Можно подключиться по IP-адресу, но hello метка DNS создает записи, проще tooidentify и краткие описания hello базовой общедоступный IP-адрес.

> [!NOTE]
> Метки DNS не требуются, если экземпляр плана tooonly подключения toohello SQL Server в рамках hello же виртуальной сети или только на локальном компьютере.

toocreate метка DNS, сначала выберите **виртуальные машины** hello портала. Установите на виртуальной Машине SQL Server toobring свойств.

1. В обзоре hello виртуальной машины, выберите ваш **общедоступный IP-адрес**.

    ![общедоступный IP-адрес](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. В свойствах hello на общедоступный IP-адрес, разверните **конфигурации**.

1. Введите имя DNS. Это имя является запись A, которая может быть напрямую используется tooconnect tooyour виртуальной Машине SQL Server по имени, а не по IP-адресу.

1. Нажмите кнопку hello **Сохранить** кнопки.

    ![имя DNS](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Подключения toohello компонент Database Engine с другого компьютера

1. На компьютере подключен toohello Интернета, откройте SQL Server Management Studio (SSMS). Если у вас нет SQL Server Management Studio, его можно скачать [здесь](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

1. В hello **подключения tooServer** или **подключения tooDatabase ядра** диалоговое окно, редактирование hello **имя сервера** значение. Введите hello IP-адрес или полное DNS-имя виртуальной машины hello (определенный в предыдущей задаче hello). Кроме того, можно также после запятой указать TCP-порт SQL Server. Например, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. В hello **проверки подлинности** выберите **проверки подлинности SQL Server**.

1. В hello **входа** введите hello имя входа SQL.

1. В hello **пароль** поле, тип hello пароль входа hello.

1. Щелкните **Подключить**.

    ![подключение SSMS](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)