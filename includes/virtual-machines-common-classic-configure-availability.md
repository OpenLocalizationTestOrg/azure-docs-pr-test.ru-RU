


Группа доступности позволяет поддерживать доступность виртуальных машин во время простоев, например связанных с обслуживанием. Помещение двух или более аналогичным образом настроенные виртуальные машины в наборе доступности создает hello доступность toomaintain дублирования hello приложения или службы, выполняемые на виртуальной машине. Дополнительные сведения о том, как это работает. в разделе [Управление доступностью виртуальных машин hello][Manage hello availability of virtual machines].

Это наиболее toouse рекомендаций группы доступности и балансировки нагрузки toohelp конечные точки убедитесь, что приложение будет всегда доступен и работает эффективно. См. дополнительные сведения о [балансировке нагрузки для служб инфраструктуры Azure][Load balancing for Azure infrastructure services].

Добавлять классические виртуальные машины в группы доступности можно одним из двух способов.

* [Вариант 1: Создание виртуальной машины и набор доступности в hello же время][Option 1: Create a virtual machine and an availability set at hello same time]. Затем можно добавьте новые виртуальные машины toohello, при создании этих виртуальных машин.
* [Вариант 2: Добавить существующую группу доступности виртуальной машины tooan][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> В классической модели hello, виртуальные машины, которые нужно tooput в hello же группу доступности должен принадлежать toohello же облачной службе.
> 
> 

## <a id="createset"></a>Вариант 1: создайте виртуальную машину и набор доступности в hello же времени
Можно использовать либо hello портал Azure или Azure PowerShell команды toodo это.

hello toouse портала Azure:

1. Если это еще не сделано, войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **+ создать**, а затем нажмите кнопку **виртуальной машины**.
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Выберите образ виртуальной машины Marketplace hello, нужно toouse. Вы можете toocreate виртуальной машины Windows или Linux.
4. Для виртуальной машины, выбранного hello, убедитесь, эту модель развертывания hello слишком**классический** и нажмите кнопку **создать**
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Введите имя виртуальной машины, имя пользователя и пароль (для компьютеров Windows) или открытый ключ SSH (для компьютеров Linux). 
6. Выберите размер виртуальной Машины hello и нажмите кнопку **выберите** toocontinue.
7. Выберите **необязательная конфигурация > Группа доступности**и выберите набор доступности hello нужно tooadd hello виртуальной машины.
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Проверьте настройки конфигурации. Когда все будет готово, нажмите **Создать**.
9. Пока Azure создает виртуальную машину, вы можете отслеживать ход выполнения hello в **виртуальные машины** в главном меню hello.

toouse Azure PowerShell команды toocreate виртуальной машине Azure и добавьте его tooa новый или существующую группу доступности см. в разделе [toocreate использование Azure PowerShell и предварительной настройки виртуальных машин под управлением Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Вариант 2: добавить существующую группу доступности виртуальной машины tooan
В hello портал Azure можно добавить существующие tooan классических виртуальных машин в существующей группе доступности или создайте новую для них. (Помните, hello, hello виртуальных машин в одной группе доступности должны принадлежать toohello же облачной службе.) Hello действия являются почти hello же. С помощью Azure PowerShell можно добавить существующую группу доступности hello виртуальной машины tooan.

1. Если вы еще не сделали, войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **виртуальные машины (классические)**.
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. Hello список виртуальных машин выберите имя hello hello виртуальной машины, что требуется, чтобы набор toohello tooadd.
4. Выберите **набор доступности** из виртуальной машины hello **параметры**.
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Выберите набор доступности hello которых надо tooadd hello виртуальной машины. Hello виртуальной машины должны принадлежать toohello же облачную службу как набор доступности hello.
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. Щелкните **Сохранить**.

toouse команд Azure PowerShell, откройте сеанс Azure PowerShell правами администратора и запустите следующую команду hello. Местозаполнители hello (такие как &lt;VmCloudServiceName&gt;), замените весь код внутри кавычек hello, включая hello < и > символы, с hello исправления имен.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> Hello виртуальной машине может быть toofinish toobe перезапуска, добавив его в группу доступности toohello.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

