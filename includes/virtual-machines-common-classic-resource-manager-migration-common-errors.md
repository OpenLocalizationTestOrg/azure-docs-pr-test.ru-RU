# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Распространенные ошибки во время tooAzure классический переноса диспетчера ресурсов
Это статье каталоги hello наиболее распространенных ошибок и способы их устранения во время миграции hello IaaS ресурсов из развертывания Azure классической модели toohello диспетчера ресурсов Azure стека.

## <a name="list-of-errors"></a>Список ошибок
| Строка ошибки | Устранение |
| --- | --- |
| Внутренняя ошибка сервера |В некоторых случаях это временная ошибка, которая исчезает после повторной попытки. Если он по-прежнему toopersist, [обратитесь в службу поддержки Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) мере изучения платформы журналов. <br><br> **Примечание:** после отслеживания инцидент hello группой поддержки hello не попытайтесь любой самостоятельного устранения рисков как это может иметь непредвиденные последствия на рабочую среду. |
| Миграция не поддерживается для развертывания {deployment-name} в размещенной службе {hosted-service-name}, так как это развертывание PaaS (веб-роль или рабочая роль). |Это происходит, если развертывание содержит веб-роль или рабочую роль. Так как Миграция поддерживается только для виртуальных машин, удалите из развертывания hello hello рабочих и веб-роли и повторите попытку миграции. |
| Не удалось выполнить развертывание шаблона {template-name}. CorrelationId={guid} |В серверном hello миграции службы мы используем ресурсы toocreate шаблонов диспетчера ресурсов Azure в стеке диспетчера ресурсов Azure hello. Поскольку шаблоны являются идемпотентными, обычно можно безопасно повторить tooget операции миграции hello за этой ошибки. Если эта ошибка повторяется, toopersist, [обратитесь в службу поддержки Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) и предоставьте им hello CorrelationId. <br><br> **Примечание:** после отслеживания инцидент hello группой поддержки hello не попытайтесь любой самостоятельного устранения рисков как это может иметь непредвиденные последствия на рабочую среду. |
| Виртуальная сеть Hello {виртуального network-name} не существует. |Это может произойти, если вы создали hello виртуальной сети в новый портал Azure hello. Фактическое имя виртуальной сети Hello hello шаблону «группа * <VNET name>» |
| Виртуальная машина {vm-name} в размещенной службе {hosted-service-name} содержит расширение {extension-name}, которое не поддерживается в Azure Resource Manager. Рекомендуется toouninstall его из hello виртуальных Машин перед продолжением миграции. |Расширения XML, например BGInfo 1.*, не поддерживаются в Azure Resource Manager. Таким образом их невозможно перенести. Если эти расширения левой hello, установленной на виртуальной машине, они автоматически удаляются до завершения миграции hello. |
| Виртуальная машина {vm-name} в размещенной службе {hosted-service-name} содержит расширение VMSnapshot или VMSnapshotLinux, которое сейчас не поддерживается для миграции. Удалить из виртуальной Машины hello и добавьте его обратно с использованием диспетчера ресурсов Azure, после миграции hello завершено |Это сценарий hello, где hello виртуальная машина настроена для резервного копирования Azure. Поскольку в настоящее время это не поддерживается, следуйте инструкциям в решение hello в https://aka.ms/vmbackupmigration |
| Виртуальной Машины "{vm-name}" в размещенной службе {размещенных service-name} содержит расширение {расширения name}, состояние которого не возвращается из hello виртуальной Машины. Поэтому виртуальную машину нельзя перенести. Убедитесь, что формируется отчет, hello состояние расширения или удалить расширение hello из hello виртуальной Машины и повторите попытку миграции. <br><br> Виртуальная машина {vm-name} в размещенной службе {hosted-service-name} содержит расширение {extension-name}, сообщающее о состоянии обработчика: {handler-status}. Таким образом нельзя перенести hello виртуальной Машины. Убедитесь, что hello расширение обработчика состояния сообщаемый {обработчик status} или удалите его из hello виртуальной Машины и повторите попытку миграции. <br><br> Reporting агент виртуальной Машины для виртуальной Машины "{vm-name}" в размещенной службе {размещенных service-name} hello общее состояние агента как не готовый. Таким образом hello виртуальной Машины могут быть перенесены, если он имеет расширение переносимые. Убедитесь, что этот агент виртуальной Машины hello сообщает общее состояние агента готовой к использованию. См. в toohttps://aka.ms/classiciaasmigrationfaqs. |Гостевой агент Azure и расширения ВМ должны исходящих toopopulate учетной записи хранилища виртуальной Машины internet access toohello их состояние. Стандартные причины сбоя состояния: <li> Сетевую группу безопасности, блокирующее исходящий доступ toohello Интернета <li> Если hello виртуальной сети имеет DNS-серверы в локальной среде и не может подключиться к DNS <br><br> В случае продолжения toosee Неподдерживаемое состояние можно удалить эту проверку tooskip расширения hello и переход вперед с миграцией. |
| Миграция не поддерживается для развертывания {deployment-name} в размещенной службе {hosted-service-name}, так как она содержит несколько наборов доступности. |В настоящее время можно перенести только размещенные службы с одной и менее группами доступности. toowork этой проблемы перенесите hello дополнительные группы доступности и виртуальных машин в этих tooa наборов доступности другой размещенной службы. |
| Миграция не поддерживается для развертывания {развертывания name} в размещенной службе {размещенных service-name, так как она содержит виртуальные машины, которые не являются частью набора доступности hello, несмотря на то, что hello HostedService содержит один. |Hello решение для этого сценария — tooeither перемещения всех виртуальных машин hello в одном доступности задать или удалить все виртуальные машины из приветствия набора доступности в hello размещенной службы. |
| Учетной записи хранилища или размещенной службе или виртуальная сеть {виртуального network-name} hello процесс миграции и поэтому не может быть изменено |Эта ошибка происходит, когда завершен hello операции миграции «Подготовка» для ресурса hello и запускается операция, которая бы сделать ресурс toohello изменений. Из-за блокировку плоскости управления hello после операции «Подготовка» hello блокируются toohello любые изменения ресурса. toounlock hello управления плоскости, при выполнении операции «Фиксация» миграции hello toocomplete переноса или hello «Прервать» миграции операции tooroll обратно hello операции «Подготовка». |
| Миграция запрещена для размещенной службы {размещенных service-name}, так как она содержит виртуальную машину {vm-name} в состоянии RoleStateUnknown. Миграция разрешена только когда виртуальная машина находится в одном из следующих hello приветствия состояния — запущена, остановлена, остановки освобождения. |Hello виртуальной Машины может выполняться через переход состояния, что обычно происходит, когда во время операции обновления на hello размещенной службе, таких как перезагрузка, Установка расширения и т. д. Рекомендуется для hello toocomplete операции обновления в размещенной службе hello перед попыткой миграции. |
| Развертывание {развертывания name} в размещенной службе {размещенных service-name} содержит {vm-name} виртуальной Машины с диском данных {имя данных диска} {логический размер диска данных виртуальной Машины hello которого физического BLOB-объекта размером {size-of-the-vhd-blob-backing-the-data-disk} байт не соответствует Size-of-the-Data-Disk-specified-in-the-VM-API} байт. Миграция будет выполнена без указания размера для диска данных hello hello виртуальной Машины диспетчера ресурсов Azure. | Эта ошибка возникает, если вы изменили размер большого двоичного объекта виртуального жесткого диска hello без обновления размер hello в модель hello API виртуальной Машины. Подробное описание шагов по устранению этой ошибки приводится [ниже](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).|
| При проверке диска данных {имя диска данных} возникло исключение хранилища: ссылка на носитель {универсальный код ресурса (URI) диска данных} виртуальной машины {имя виртуальной машины} в облачной службе {имя облачной службы}. Убедитесь, что медиассылки, hello виртуальный жесткий ДИСК доступен для этой виртуальной машины | Эта ошибка может произойти, если диски hello hello виртуальной Машины была удалена или больше недоступны. Убедитесь, что диски hello для hello, виртуальная машина существует.|
| Виртуальная машина {имя_ВМ} в HostedService {имя_облачной_службы} содержит диск с MediaLink {URI_VHD} с именем BLOB-объекта {имя_объекта_VHD}, которое не поддерживается в Azure Resource Manager. | Эта ошибка возникает, когда имя hello hello большого двоичного объекта имеет «/» в нем, который в настоящее время не поддерживается в поставщике ресурсов вычислений. |
| Миграция не разрешена для развертывания {развертывания name} в {cloud-service-name} размещенной службе, он не находится в региональной областью hello. Для перемещения этой области развертывания tooregional см toohttp://aka.ms/regionalscope. | В 2014 Azure объявлено, что сетевые ресурсы будут перемещены из области tooregional области уровня кластера. Дополнительные сведения см. здесь: [http://aka.ms/regionalscope] \(http://aka.ms/regionalscope). Эта ошибка возникает при переносе развертывания hello не был автоматически перемещает региональной областью tooa операции обновления. Лучшим решением проблемы является tooeither добавить tooa конечной точки виртуальной Машины или данных на диске toohello виртуальной Машины и повторите попытку миграции. <br> В разделе [как tooset копирование конечные точки в классической виртуальной машине в Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) или [присоединения данных диска tooa Windows виртуальную машину, созданную с помощью hello классической модели развертывания](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Подробные инструкции по устранению

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>Виртуальную Машину с диска данных которого физический размер в байтах больших двоичных объектов не соответствует hello диска данных виртуальной Машины логический размер в байтах.

Это происходит, когда hello размер логического диска данных можно получить синхронизирован с hello фактический размер большого двоичного объекта виртуального жесткого диска. Это можно легко проверить с помощью hello, следующие команды:

#### <a name="verifying-hello-issue"></a>Проверка того, проблема hello

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Сдерживание проблема hello

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Перемещение виртуальной Машины tooa другую подписку после завершения миграции

После завершения процесса миграции hello, вы можете toomove hello ВМ tooanother подписки. Тем не менее при наличии секрет или сертификат на перемещение виртуальной Машины, которые ссылаются на ресурс хранилища ключей hello hello в настоящее время не поддерживается. Hello ниже инструкциям разрешить проблему tooworkaround hello. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>Azure CLI 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
