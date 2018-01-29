## <a name="overview"></a>Обзор
При создании новой виртуальной машины в группе ресурсов путем развертывания образа из [Azure Marketplace](https://azure.microsoft.com/marketplace/) диск операционной системы по умолчанию обычно имеет размер 127 ГБ (в некоторых образах диск ОС по умолчанию меньше). Хотя существует возможность добавлять диски данных к виртуальной машине (их число зависит от выбора номеров SKU), при этом даже рекомендуется устанавливать приложения и интенсивные по ЦП рабочие нагрузки на этих дополнительных дисках, зачастую пользователям требуется расширить диск операционной системы для поддержки некоторых сценариев, например следующих:

1. Поддержка старых приложений, устанавливающих свои компоненты на диске с ОС.
2. Перенос локального физического компьютера или виртуальной машины с диском операционной системы большого размера.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: модель Resource Manager и классическая модель. В этой статье описана модель развертывания на основе Resource Manager. Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.
> 
> 

## <a name="resize-the-os-drive"></a>Изменение размера диска операционной системы
В этой статье мы займемся задачей изменения размера для диска операционной системы с помощью модулей Resource Manager из [Azure Powershell](/powershell/azureps-cmdlets-docs). Мы рассмотрим изменение размера диска ОС для дисков Unamanged и управляемый код так, как подход, чтобы изменить размер дисков отличается от обоих типов дисков.

### <a name="for-resizing-unmanaged-disks"></a>Для изменения размеров неуправляемые дисков:

Откройте интегрированную среду сценариев Powershell или окно Powershell в режиме администратора и выполните следующие действия.

1. Войдите в учетную запись Microsoft Azure в режиме управления ресурсами и выберите подписку следующим образом:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Задайте имя группы ресурсов и имя виртуальной машины следующим образом:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Получите ссылку на виртуальную машину следующим образом:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Остановите виртуальную машину перед изменением размера диска следующим образом:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. И вот теперь долгожданный момент. Размер диска ОС неуправляемые нужное значение и обновление виртуальной Машины следующим образом:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > Новый размер должен быть больше, чем размер существующего диска. Допустимое значение составляет 2048 ГБ для дисков операционной системы. (Можно развернуть большой двоичный объект VHD сверх этого размера, но операционная система сможет работать только с первыми 2048 ГБ.)
   > 
   > 
6. Обновление виртуальной машины может занять несколько секунд. После завершения команды перезапустите виртуальную машину, как показано ниже:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

### <a name="for-resizing-managed-disks"></a>Для изменения размеров управляемых дисков:

Откройте интегрированную среду сценариев Powershell или окно Powershell в режиме администратора и выполните следующие действия.

1. Войдите в учетную запись Microsoft Azure в режиме управления ресурсами и выберите подписку следующим образом:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Задайте имя группы ресурсов и имя виртуальной машины следующим образом:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Получите ссылку на виртуальную машину следующим образом:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Остановите виртуальную машину перед изменением размера диска следующим образом:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. Получите ссылку на диск управляемых операционной системы. Задать размер диска операционной системы на управляемых нужное значение и обновления диска следующим образом:
   
   ```Powershell
   $disk= Get-AzureRmDisk -ResourceGroupName $rgName -DiskName $vm.StorageProfile.OsDisk.Name
   $disk.DiskSizeGB = 1023
   Update-AzureRmDisk -ResourceGroupName $rgName -Disk $disk -DiskName $disk.Name
   ```   
   > [!WARNING]
   > Новый размер должен быть больше, чем размер существующего диска. Допустимое значение составляет 2048 ГБ для дисков операционной системы. (Можно развернуть большой двоичный объект VHD сверх этого размера, но операционная система сможет работать только с первыми 2048 ГБ.)
   > 
   > 
6. Обновление виртуальной машины может занять несколько секунд. После завершения команды перезапустите виртуальную машину, как показано ниже:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

Вот и все! Теперь подключитесь по RDP к виртуальной машине, откройте раздел "Управление компьютером" (или "Управление дисками") и увеличьте диск, используя только что выделенное для этого место.

## <a name="summary"></a>Сводка
В этой статье мы использовали модули Resource Manager в Azure Powershell для увеличения диска операционной системы виртуальной машины IaaS. Воспроизвести ниже приведен полный скрипт в качестве справочной информации для дисков неуправляемый и управляемый код.

Unamanged диски:

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
Управляемые диски:

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRMVM -ResourceGroupName $rgName -Name $vmName
$disk= Get-AzureRmDisk -ResourceGroupName $rgName -DiskName $vm.StorageProfile.OsDisk.Name
$disk.DiskSizeGB = 1023
Update-AzureRmDisk -ResourceGroupName $rgName -Disk $disk -DiskName $disk.Name
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Следующие шаги
На то, что в этой статье мы уделять расширение виртуальной машины диска ОС Unamanged/управляемый код, разработанный скрипт может также использоваться для расширения дисков, подключенных к виртуальной машине. Например, чтобы увеличить первый диск с данными, подключенный к виртуальной машине, замените объект ```OSDisk``` в ```StorageProfile``` на массив ```DataDisks``` и используйте числовой индекс для получения ссылки на первый подключенный диск с данными, как показано ниже:

Unamanged диск:
```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Управляемый диск:
```Powershell
$disk= Get-AzureRmDisk -ResourceGroupName $rgName -DiskName $vm.StorageProfile.DataDisks[0].Name
$disk.DiskSizeGB = 1023
```

Аналогичным образом можно ссылаться на другие диски с данными, подключенные к виртуальной машине, либо с помощью индекса, как показано выше, либо с помощью свойства ```Name``` диска, как показано ниже:

Unamanged диск:
```Powershell
($vm.StorageProfile.DataDisks | Where ({$_.Name -eq 'my-second-data-disk'}).DiskSizeGB = 1023
```
Управляемые диск:
```Powershell
(Get-AzureRmDisk -ResourceGroupName $rgName -DiskName ($vm.StorageProfile.DataDisks | Where ({$_.Name -eq 'my-second-data-disk'})).Name).DiskSizeGB = 1023
```

Дополнительные сведения о подключении дисков к виртуальной машине через Azure Resource Manager см. в этой [статье](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

