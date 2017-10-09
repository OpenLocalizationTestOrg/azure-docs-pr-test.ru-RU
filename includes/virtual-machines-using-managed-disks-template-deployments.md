# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="22714-101">Использование управляемых дисков в шаблонах Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22714-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="22714-102">В этом документе рассматриваются различия hello между управляемым и неуправляемым диски при использовании диспетчера ресурсов Azure шаблоны tooprovision виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="22714-102">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="22714-103">Это поможет вам tooupdate существующих шаблонов, используются неуправляемые диски toomanaged дисков.</span><span class="sxs-lookup"><span data-stu-id="22714-103">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="22714-104">Для справки, мы используем hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) шаблон в качестве руководства.</span><span class="sxs-lookup"><span data-stu-id="22714-104">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="22714-105">Вы можете видеть шаблон hello использование обеих [управляемых дисках](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) и в предыдущей версии с помощью [неуправляемого дисков](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) при желании toodirectly сравнить их.</span><span class="sxs-lookup"><span data-stu-id="22714-105">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="22714-106">Формат шаблона с неуправляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="22714-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="22714-107">toobegin, мы посмотрим на диски, как неуправляемый развертываются.</span><span class="sxs-lookup"><span data-stu-id="22714-107">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="22714-108">При создании неуправляемой дисков, необходимо VHD-файлы toohold hello хранилища учетной записи.</span><span class="sxs-lookup"><span data-stu-id="22714-108">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="22714-109">Можно создать новую учетную запись хранения или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="22714-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="22714-110">В этой статье будет показано, как toocreate новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="22714-110">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="22714-111">tooaccomplish, требуется ресурс учетной записи хранения в блоке hello ресурсы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="22714-111">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="22714-112">В рамках hello объекта виртуальной машины нам нужна зависимость от tooensure учетной записи хранилища hello, он создан до hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="22714-112">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="22714-113">В рамках hello `storageProfile` статьи, затем укажите hello полный URI hello расположение виртуального жесткого диска, которое ссылается на учетную запись хранения hello и необходим для диска hello ОС и дисков данных.</span><span class="sxs-lookup"><span data-stu-id="22714-113">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="22714-114">Формат шаблона с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="22714-114">Managed disks template formatting</span></span>

<span data-ttu-id="22714-115">С дисками управляемых Azure hello диска становится ресурс верхнего уровня и больше не требуется toobe учетной записи хранилища, созданных пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="22714-115">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="22714-116">Управляемый диски сначала были видны в hello `2016-04-30-preview` версия API, они доступны во всех последующих версиях API и теперь тип диска по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="22714-116">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="22714-117">Hello следующих разделах Пройдите по умолчанию hello и подробно описывается настройка toofurther дисков.</span><span class="sxs-lookup"><span data-stu-id="22714-117">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="22714-118">Рекомендуется версия toouse API-Интерфейс, более поздней, чем `2016-04-30-preview` как критические изменения между `2016-04-30-preview` и `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="22714-118">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="22714-119">Параметры управляемого диска по умолчанию</span><span class="sxs-lookup"><span data-stu-id="22714-119">Default managed disk settings</span></span>

<span data-ttu-id="22714-120">toocreate виртуальную Машину с управляемых диски, вы больше не требуется ресурс учетной записи хранения toocreate hello и обновить ресурс виртуальной машины следующим образом.</span><span class="sxs-lookup"><span data-stu-id="22714-120">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="22714-121">В частности Обратите внимание, что hello `apiVersion` отражает `2017-03-30` и hello `osDisk` и `dataDisks` больше не ссылаются tooa указанного URI для hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="22714-121">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="22714-122">При развертывании без указания дополнительных свойств, будет использовать диск hello [хранения Standard-LRS](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="22714-122">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="22714-123">Если имя не указано, оно имеет формат hello `<VMName>_OsDisk_1_<randomstring>` для диска ОС hello и `<VMName>_disk<#>_<randomstring>` для каждого диска данных.</span><span class="sxs-lookup"><span data-stu-id="22714-123">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="22714-124">По умолчанию шифрование диска Azure отключено; кэширование — чтение и запись для диска ОС hello, а не для дисков данных.</span><span class="sxs-lookup"><span data-stu-id="22714-124">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="22714-125">Можно заметить в приведенном ниже примере hello, что по-прежнему зависимость учетной записи хранилища, хотя это только для хранения диагностических данных, не требуется для хранения на диске.</span><span class="sxs-lookup"><span data-stu-id="22714-125">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="22714-126">Использование ресурса управляемого диска верхнего уровня</span><span class="sxs-lookup"><span data-stu-id="22714-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="22714-127">Настройки конфигурации диска hello альтернативных toospecifying hello объекта виртуальной машины можно создать ресурс верхнего уровня диска и присоединить ее как часть создания виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="22714-127">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="22714-128">Например можно создать дисковый ресурс toouse в качестве диска данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="22714-128">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="22714-129">В рамках hello объекта виртуальной Машины можно затем сослаться присоединенного объекта toobe этот диск система.</span><span class="sxs-lookup"><span data-stu-id="22714-129">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="22714-130">Указав идентификатор ресурса hello hello управляемого диска, мы создали hello `managedDisk` свойство позволяет hello вложения hello диска в качестве виртуальной Машины создается hello.</span><span class="sxs-lookup"><span data-stu-id="22714-130">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="22714-131">Обратите внимание, что hello `apiVersion` для hello ресурса виртуальной Машины установлен слишком`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="22714-131">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="22714-132">Также Обратите внимание, что мы создали зависимость на tooensure ресурсов диска hello, которую он успешно создан, прежде чем создание виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="22714-132">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="22714-133">Создание управляемых групп доступности с виртуальными машинами, использующими управляемые диски</span><span class="sxs-lookup"><span data-stu-id="22714-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="22714-134">toocreate управляемых доступности наборы с виртуальными машинами с помощью управляемых дисков добавить hello `sku` доступности toohello объекта набора ресурсов и набора hello `name` свойство слишком`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="22714-134">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="22714-135">Это гарантирует, что hello дисков для каждой виртуальной Машины достаточно изолированы от друг с другом tooavoid единых точек отказа.</span><span class="sxs-lookup"><span data-stu-id="22714-135">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="22714-136">Также Обратите внимание, что hello `apiVersion` ресурсу набора hello доступности задается слишком`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="22714-136">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="22714-137">Дополнительные сценарии и настройки</span><span class="sxs-lookup"><span data-stu-id="22714-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="22714-138">toofind полные сведения о спецификациях API-интерфейса REST hello, см. в статье hello [создания управляемой дисковой документация по REST API](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="22714-138">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="22714-139">Вы найдете дополнительные сценарии, а также по умолчанию и допустимые значения, которые могут быть отправлено toohello API с помощью шаблонов-развертываний.</span><span class="sxs-lookup"><span data-stu-id="22714-139">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="22714-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22714-140">Next steps</span></span>

* <span data-ttu-id="22714-141">Для полного шаблонов, использующие управляемые диски посетите hello ссылкам репозитория быстрый запуск Azure.</span><span class="sxs-lookup"><span data-stu-id="22714-141">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="22714-142">Виртуальная машина Windows с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="22714-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="22714-143">Виртуальная машина Linux с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="22714-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="22714-144">Полный список шаблонов с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="22714-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="22714-145">Посетите hello [Обзор управляемых дисков Azure](../articles/virtual-machines/windows/managed-disks-overview.md) управляемых документа toolearn Дополнительные сведения о дисках.</span><span class="sxs-lookup"><span data-stu-id="22714-145">Visit hello [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="22714-146">Просмотрите hello шаблона справочную документацию для ресурсов виртуальных машин, перейдя по адресу hello [ссылка на шаблон Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) документа.</span><span class="sxs-lookup"><span data-stu-id="22714-146">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="22714-147">Просмотрите hello шаблона справочную документацию по дисковых ресурсов, перейдя по адресу hello [ссылка на шаблон Microsoft.Compute/disks](/templates/microsoft.compute/disks) документа.</span><span class="sxs-lookup"><span data-stu-id="22714-147">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
