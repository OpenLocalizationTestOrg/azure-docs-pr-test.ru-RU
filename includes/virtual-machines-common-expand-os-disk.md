## <a name="overview"></a>Обзор
При создании новой виртуальной машины (VM) в группе ресурсов путем развертывания образа с [Azure Marketplace](https://azure.microsoft.com/marketplace/), диск операционной системы по умолчанию hello составляет 127 ГБ. Хотя это toohello диски данных возможно tooadd виртуальной Машины (сколько зависимости hello SKU вы выбрали) и более того, это рекомендуемые tooinstall приложений и рабочих нагрузок интенсивных ЦП на этих дисках приложение, зачастую пользователи должны hello tooexpand ОС диск toosupport некоторых сценариев, таких как следующие:

1. Поддержка старых приложений, устанавливающих свои компоненты на диске с ОС.
2. Перенос локального физического компьютера или виртуальной машины с диском операционной системы большого размера.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: модель Resource Manager и классическая модель. В этой статье описан с помощью модели hello диспетчера ресурсов. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.
> 
> 

## <a name="resize-hello-os-drive"></a>Изменение размера диска hello ОС
В этой статье мы выполнить задачу hello изменения размера диска hello операционной системы, с помощью модулей диспетчера ресурсов [Azure Powershell](/powershell/azureps-cmdlets-docs). Откройте интегрированную среду Сценариев Powershell или в окне Powershell в режиме администрирования и выполните следующие шаги hello:

1. Tooyour входа в Microsoft Azure учетной записи в режиме управления ресурсов и выберите подписку, следующим образом:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Задайте имя группы ресурсов и имя виртуальной машины следующим образом:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Получите ссылку tooyour виртуальной Машины следующим образом:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Остановите hello виртуальной Машины перед изменением размера диска hello следующим образом:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. И здесь мы ждать для момента hello! Задать размер hello toohello требуемого значения hello ОС диска и обновить hello виртуальной Машины следующим образом:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > новый размер Hello должен быть больше, чем размер существующего диска hello. Максимальное допустимое Hello — 1023 ГБ.
   > 
   > 
6. Обновление hello виртуальной Машины может занять несколько секунд. После завершения выполнения команды hello перезапустите hello виртуальной Машины следующим образом:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

Вот и все! Теперь RDP в hello виртуальной Машины, откройте Управление компьютером (или «Управление дисками») и разверните hello диска, с помощью hello вновь выделенный размер.

## <a name="summary"></a>Сводка
В этой статье мы использовали модулей Powershell tooexpand hello диска операционной системы виртуальной машины IaaS Azure Resource Manager. Воспроизвести ниже приведен hello полный скрипт в качестве справочной информации.

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Дальнейшие действия
Хотя в этой статье мы уделять расширяемый hello ОС диск из виртуальной Машины hello, hello разработаны скрипт может также использоваться для расширения hello данных дисков вложенного toohello ВМ путем изменения одной строки кода. Например, сначала данные tooexpand hello диск toohello подключенных виртуальных Машин, замените hello ```OSDisk``` объект ```StorageProfile``` с ```DataDisks``` массива и использовать числовой индекс tooobtain ссылки toofirst подключенный диск данных, как показано ниже:

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Аналогичным образом можно ссылаться на вложенное toohello каталога диски других данных виртуальной Машины, либо с помощью индекса, как показано выше или hello ```Name``` свойства hello диска, как показано ниже:

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Если вы хотите toofind out как tooattach диски tooan виртуальной Машины диспетчера ресурсов Azure, установите этот флажок, [статьи](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

