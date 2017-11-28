# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="17533-101">Использование управляемых дисков в шаблонах Resource Manager</span><span class="sxs-lookup"><span data-stu-id="17533-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="17533-102">В этом документе рассматриваются различия между управляемым и неуправляемыми дисками при использовании шаблонов Azure Resource Manager для подготовки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="17533-102">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="17533-103">Эти знания помогут вам обновить существующие шаблоны, в которых используются неуправляемые диски, заменив их управляемыми дисками.</span><span class="sxs-lookup"><span data-stu-id="17533-103">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="17533-104">В качестве примера мы используем шаблон [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows).</span><span class="sxs-lookup"><span data-stu-id="17533-104">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="17533-105">Вы можете просмотреть шаблон, использующий [управляемые диски](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json), и его предыдущую версию, использующую [неуправляемые диски](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json), если вы хотите непосредственно сравнить их.</span><span class="sxs-lookup"><span data-stu-id="17533-105">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="17533-106">Формат шаблона с неуправляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="17533-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="17533-107">Сначала рассмотрим, как развертываются неуправляемые диски.</span><span class="sxs-lookup"><span data-stu-id="17533-107">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="17533-108">При создании неуправляемых дисков необходима учетная запись хранения для хранения файлов VHD-файлов.</span><span class="sxs-lookup"><span data-stu-id="17533-108">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="17533-109">Можно создать новую учетную запись хранения или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="17533-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="17533-110">В этой статье показано, как создать новую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="17533-110">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="17533-111">Для этого требуется ресурс учетной записи хранения в блоке ресурсов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="17533-111">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

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

<span data-ttu-id="17533-112">В объекте виртуальной машины необходима зависимость от учетной записи хранения, чтобы гарантировать, что она будет создана до виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="17533-112">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="17533-113">В разделе `storageProfile` мы укажем полный универсальный код ресурса (URI) расположения VHD, который ссылается на учетную запись хранения и требуется для диска ОС и дисков данных.</span><span class="sxs-lookup"><span data-stu-id="17533-113">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="17533-114">Формат шаблона с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="17533-114">Managed disks template formatting</span></span>

<span data-ttu-id="17533-115">При использовании службы "Управляемые диски Azure" диск становится ресурсом верхнего уровня и для него больше не требуется учетная запись хранения, созданная пользователем.</span><span class="sxs-lookup"><span data-stu-id="17533-115">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="17533-116">Управляемые диски впервые были представлены в версии API `2016-04-30-preview`. Они доступны во всех последующих версиях API и теперь являются типом диска по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="17533-116">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="17533-117">В следующих разделах рассматриваются параметры по умолчанию и описывается дальнейшая настройка дисков.</span><span class="sxs-lookup"><span data-stu-id="17533-117">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="17533-118">Рекомендуем использовать более позднюю версию API, чем `2016-04-30-preview`, так как между версиями `2016-04-30-preview` и `2017-03-30` были внесены критически важные изменения.</span><span class="sxs-lookup"><span data-stu-id="17533-118">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="17533-119">Параметры управляемого диска по умолчанию</span><span class="sxs-lookup"><span data-stu-id="17533-119">Default managed disk settings</span></span>

<span data-ttu-id="17533-120">Для создания виртуальной машины с управляемыми дисками больше не требуется создавать ресурс учетной записи хранения, и можно обновлять ресурс виртуальной машины следующим образом.</span><span class="sxs-lookup"><span data-stu-id="17533-120">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="17533-121">В частности, обратите внимание на то, что `apiVersion` имеет значение `2017-03-30`, а `osDisk` и `dataDisks` больше не ссылаются на определенный универсальный код ресурса (URI) VHD.</span><span class="sxs-lookup"><span data-stu-id="17533-121">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="17533-122">При развертывании без указания дополнительных свойств диск будет использовать [локально избыточное хранилище уровня "Стандартный"](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="17533-122">When deploying without specifying additional properties, the disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="17533-123">Если не указать имя, то диску ОС присваивается имя `<VMName>_OsDisk_1_<randomstring>`, а каждому диску данных — `<VMName>_disk<#>_<randomstring>`.</span><span class="sxs-lookup"><span data-stu-id="17533-123">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="17533-124">По умолчанию шифрование диска Azure отключено. Кэширование чтения и записи включено для диска ОС, но не для дисков данных.</span><span class="sxs-lookup"><span data-stu-id="17533-124">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="17533-125">Можно заметить, что в приведенном ниже примере осталась зависимость от учетной записи хранения, хотя она используется только для хранения диагностических данных и не требуется для хранения дисков.</span><span class="sxs-lookup"><span data-stu-id="17533-125">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="17533-126">Использование ресурса управляемого диска верхнего уровня</span><span class="sxs-lookup"><span data-stu-id="17533-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="17533-127">В качестве альтернативы указанию конфигурации дисков в объекте виртуальной машины можно создать ресурс диска верхнего уровня и подключить его при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="17533-127">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="17533-128">Например, можно создать дисковый ресурс, как показано ниже, и использовать его в качестве диска данных.</span><span class="sxs-lookup"><span data-stu-id="17533-128">For example, we can create a disk resource as follows to use as a data disk.</span></span>

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

<span data-ttu-id="17533-129">Затем можно указать ссылку на него в объекте виртуальной машины, чтобы подключить этот объект диска.</span><span class="sxs-lookup"><span data-stu-id="17533-129">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="17533-130">Указав идентификатор ресурса созданного управляемого диска в свойстве `managedDisk`, можно подключить этот диск при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="17533-130">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="17533-131">Обратите внимание, что для параметра `apiVersion` ресурса виртуальной машины задано значение `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="17533-131">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="17533-132">Кроме того, обратите внимание, что мы создали зависимость от дискового ресурса, чтобы обеспечить его успешное создание перед созданием виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="17533-132">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="17533-133">Создание управляемых групп доступности с виртуальными машинами, использующими управляемые диски</span><span class="sxs-lookup"><span data-stu-id="17533-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="17533-134">Чтобы создать управляемые группы доступности с виртуальными машинами, использующими управляемые диски, добавьте объект `sku` в ресурс группы доступности и задайте для свойства `name` значение `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="17533-134">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="17533-135">Это гарантирует, что диски каждой виртуальной машины будут достаточно изолированы друг от друга, чтобы избежать образования единых точек отказа.</span><span class="sxs-lookup"><span data-stu-id="17533-135">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="17533-136">Также обратите внимание, что для параметра `apiVersion` ресурса группы доступности задано значение `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="17533-136">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="17533-137">Дополнительные сценарии и настройки</span><span class="sxs-lookup"><span data-stu-id="17533-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="17533-138">Полные сведения о спецификациях REST API можно найти в [документации по созданию управляемых дисков с помощью REST API](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="17533-138">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="17533-139">В ней вы найдете дополнительные сценарии, а также значения по умолчанию и допустимые значения, которые можно передавать в API при развертывании с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="17533-139">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="17533-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17533-140">Next steps</span></span>

* <span data-ttu-id="17533-141">Полные шаблоны, использующие управляемые диски, можно получить, перейдя по приведенным ниже ссылкам на репозиторий кратких руководств по Azure.</span><span class="sxs-lookup"><span data-stu-id="17533-141">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="17533-142">Виртуальная машина Windows с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="17533-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="17533-143">Виртуальная машина Linux с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="17533-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="17533-144">Полный список шаблонов с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="17533-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="17533-145">Ознакомьтесь с документом [Обзор управляемых дисков Azure](../articles/virtual-machines/windows/managed-disks-overview.md), чтобы узнать больше об управляемых дисках.</span><span class="sxs-lookup"><span data-stu-id="17533-145">Visit the [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="17533-146">Ознакомьтесь с информацией по шаблонам для ресурсов виртуальных машин, приведенной в [справочнике по шаблону Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines).</span><span class="sxs-lookup"><span data-stu-id="17533-146">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="17533-147">Ознакомьтесь с информацией по шаблонам дисковых ресурсов, приведенной в [справочнике по шаблону Microsoft.Compute/disks](/templates/microsoft.compute/disks).</span><span class="sxs-lookup"><span data-stu-id="17533-147">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
