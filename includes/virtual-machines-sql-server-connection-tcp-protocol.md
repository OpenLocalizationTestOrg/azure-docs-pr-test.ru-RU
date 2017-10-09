1. При подключенном toohello виртуальную машину с удаленного рабочего стола, поиск **Configuration Manager**:

    ![Откройте SSCM](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. В диспетчере конфигурации SQL Server в области консоли hello разверните **сетевая конфигурация SQL Server**.

1. В области консоли приветствия щелкните **протоколы для MSSQLSERVER** (имя экземпляра по умолчанию hello). Щелкните правой кнопкой мыши в области сведений hello **TCP** и нажмите кнопку **включить** , если он еще не включен.

    ![Включение TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. В области консоли приветствия щелкните **служб SQL Server**. Щелкните правой кнопкой мыши в области сведений hello,  **SQL Server (*имя экземпляра*) ** (экземпляр по умолчанию hello: **SQL Server (MSSQLSERVER)**) и нажмите кнопку **перезапустите** , hello toostop и перезапустите экземпляр SQL Server.

    ![Перезапустите ядро СУБД](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Закройте диспетчер конфигурации SQL Server.

Дополнительные сведения о включении протоколов для hello SQL Server Database Engine см. в разделе [Включение или отключение сетевого протокола сервера](http://msdn.microsoft.com/library/ms191294.aspx).
