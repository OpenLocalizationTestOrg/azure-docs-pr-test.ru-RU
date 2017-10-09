### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Определите DNS-имя виртуальной машины hello hello
tooconnect toohello SQL Server Database Engine с другого компьютера, необходимо знать hello доменных имен (DNS) имя виртуальной машины hello. (Это имя hello hello Интернет использует tooidentify hello виртуальной машины. Можно использовать hello IP-адрес, но hello IP-адреса могут измениться, если Azure переместит ресурсы для обеспечения избыточности или обслуживания. имя DNS Hello будет стабильным, поскольку может быть перенаправлено tooa новый IP-адрес.)  

1. В портале Azure hello (или предыдущем шаге hello) выберите **виртуальные машины (классические)**.
2. Выберите виртуальную машину SQL.
3. На hello **виртуальной машины** колонки, hello копирования **DNS-имя** для hello виртуальной машины.
   
    ![DNS-имя](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Подключения toohello компонент Database Engine с другого компьютера
1. На компьютере подключен toohello Интернета, откройте SQL Server Management Studio.
2. В hello **подключения tooServer** или **подключения tooDatabase ядра** диалогового окна hello **имя сервера** введите DNS-имя виртуальной машины hello (определенный в hello hello предыдущая задача) и номер порта общедоступную конечную точку в формате hello *Dnsимя, номерПорта* например **mysqlvm.cloudapp.net,57500**.
   
    ![Connect using SSMS](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Если вы не помните номер порта hello общедоступную конечную точку созданного ранее, его можно найти в hello **конечные точки** область hello **виртуальной машины** колонку.
   
    ![Общий порт](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. В hello **проверки подлинности** выберите **проверки подлинности SQL Server**.
4. В hello **входа** введите hello имя входа, который был создан в предыдущей задаче.
5. В hello **пароль** поле, тип hello пароль имени входа hello, созданный в предыдущей задаче.
6. Щелкните **Подключить**.

