прослушиватель группы доступности Hello — IP-адресом и сетевым имя, hello SQL Server прослушивает группы доступности. прослушиватель группы доступности hello toocreate hello следующие:

1. <a name="getnet"></a>Получите имя сетевого ресурса кластера hello hello.

    а. С помощью протокола удаленного рабочего СТОЛА tooconnect toohello виртуальную машину Azure, на котором размещена первичная реплика hello. 

    b. Откройте диспетчер отказоустойчивости кластеров.

    c. Выберите hello **сетей** узла и сетевое имя кластера Примечание hello. Используйте это имя в hello `$ClusterNetworkName` переменной в hello сценарий PowerShell. В hello за сетевое имя кластера hello изображения следует **сети кластера 1**:

   ![Сетевое имя кластера](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Добавление клиентской точки доступа hello.  
    точка доступа клиента Hello — hello сетевого имени, который используется приложениями баз данных toohello tooconnect в группе доступности. Создайте точку доступа клиента hello в диспетчере отказоустойчивости кластеров.

    а. Разверните имя кластера hello и щелкните **ролей**.

    b. В hello **ролей** панели, щелкните правой кнопкой мыши группу доступности hello имя, а затем выберите **добавить ресурс** > **точки доступа клиента**.

   ![Точка доступа клиента](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. В hello **имя** Создайте имя для этого нового прослушивателя. 
   Hello для hello новый прослушиватель имеет имя hello сетевого имени, который используется приложениями tooconnect toodatabases в группе доступности SQL Server hello.
   
    d. toofinish при создании прослушивателя hello, нажмите кнопку **Далее** дважды, а затем нажмите кнопку **Готово**. Не следует переводить прослушиватель hello или ресурс в оперативный режим на этом этапе.

3. <a name="congroup"></a>Настройте hello IP-ресурс для группы доступности hello.

    а. Нажмите кнопку hello **ресурсов** вкладку, а затем раскройте точку доступа клиента hello, вы создали.  
    точка доступа клиента Hello находится в автономном режиме.

   ![Точка доступа клиента](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Щелкните правой кнопкой мыши hello IP-ресурс и выберите пункт Свойства. Запишите имя hello hello IP-адрес и использовать его в hello `$IPResourceName` переменной в hello сценарий PowerShell.

    c. В разделе **IP-адрес** выберите параметр **Статический IP-адрес**. Задать hello IP-адрес как hello же адрес используется при установке hello адрес подсистемы балансировки нагрузки для hello портал Azure.

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Зависеть ресурс группы доступности SQL Server hello hello клиентской точки доступа.

    а. В диспетчере отказоустойчивости кластеров щелкните **Роли** и выберите группу доступности.

    b. На hello **ресурсов** в разделе **другие ресурсы**, щелкните правой кнопкой мыши группу ресурсов доступности hello и нажмите кнопку **свойства**. 

    c. На вкладке зависимости hello добавьте имя hello ресурса точек (прослушиватель hello) hello клиентского доступа.

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    г) Нажмите кнопку **ОК**.

5. <a name="listname"></a>Сделать hello клиентского доступа точки ресурса, зависящее от hello IP-адрес.

    а. В диспетчере отказоустойчивости кластеров щелкните **Роли** и выберите группу доступности. 

    b. На hello **ресурсов** щелкните правой кнопкой мыши ресурс точки доступа клиента hello в **имя сервера**, а затем нажмите кнопку **свойства**. 

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Нажмите кнопку hello **зависимости** вкладки. Убедитесь, что IP-адрес hello зависимость. Если это не так, задайте зависимость hello IP-адрес. Если перечислено несколько ресурсов, убедитесь, что hello IP-адреса имеют или не зависимости. Нажмите кнопку **ОК**. 

   ![Ресурс IP-адреса](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **перевести в оперативный режим**. 

    >[!TIP]
    >Можно проверить правильность настройки зависимостей, приветствия. TooRoles перейдите в Диспетчер отказоустойчивости кластеров, щелкните правой кнопкой мыши группу доступности hello, нажмите кнопку **дополнительные действия**, а затем нажмите кнопку **Показать отчет о зависимостях**. Если зависимости hello правильно настроены, hello группы доступности определяется hello сетевое имя и hello сетевого имени зависит от hello IP-адрес. 


6. <a name="setparam"></a>Настроить параметры кластера hello в PowerShell.
    
    а. Скопируйте hello, следуя tooone сценария PowerShell в экземплярах SQL Server. Обновите hello переменные среды.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Задайте параметры кластера hello, выполнив hello сценарий PowerShell на одном из узлов кластера hello.  

    > [!NOTE]
    > Если экземпляры SQL Server находятся в отдельных регионах, требуется сценарий PowerShell toorun hello дважды. Здравствуйте, первый раз, использовать hello `$ILBIP` и `$ProbePort` из первой области hello. Здравствуйте, второй раз, использовать hello `$ILBIP` и `$ProbePort` из второй области hello. сетевое имя кластера Hello и имя ресурса IP кластера hello hello же. 
