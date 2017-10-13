1. При подключении к виртуальной машине с помощью удаленного рабочего стола найдите **диспетчер конфигурации**:

    ![Откройте SSCM](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. В диспетчере конфигурации SQL Server в области консоли разверните пункт **Сетевая конфигурация SQL Server**.

1. В области консоли щелкните **Протоколы для MSSQLSERVER** (имя экземпляра по умолчанию). В области сведений щелкните правой кнопкой мыши **TCP** и выберите пункт **Включить** (если этот тип протокола еще не включен).

    ![Включение TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. В области консоли выберите **Службы SQL Server**. В области сведений щелкните правой кнопкой мыши **SQL Server (*имя экземпляра*)** (экземпляр по умолчанию — **SQL Server (MSSQLSERVER)**) и выберите **Перезагрузить**, чтобы остановить и перезапустить экземпляр SQL Server.

    ![Перезапустите ядро СУБД](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Закройте диспетчер конфигурации SQL Server.

Дополнительные сведения о включении протоколов для компонента Ядро СУБД SQL Server см. в статье [Включение или отключение сетевого протокола сервера](http://msdn.microsoft.com/library/ms191294.aspx).
