# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Использование управляемых дисков в шаблонах Resource Manager

В этом документе рассматриваются различия hello между управляемым и неуправляемым диски при использовании диспетчера ресурсов Azure шаблоны tooprovision виртуальных машин. Это поможет вам tooupdate существующих шаблонов, используются неуправляемые диски toomanaged дисков. Для справки, мы используем hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) шаблон в качестве руководства. Вы можете видеть шаблон hello использование обеих [управляемых дисках](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) и в предыдущей версии с помощью [неуправляемого дисков](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) при желании toodirectly сравнить их.

## <a name="unmanaged-disks-template-formatting"></a>Формат шаблона с неуправляемыми дисками

toobegin, мы посмотрим на диски, как неуправляемый развертываются. При создании неуправляемой дисков, необходимо VHD-файлы toohold hello хранилища учетной записи. Можно создать новую учетную запись хранения или использовать существующую. В этой статье будет показано, как toocreate новой учетной записи хранения. tooaccomplish, требуется ресурс учетной записи хранения в блоке hello ресурсы, как показано ниже.

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

В рамках hello объекта виртуальной машины нам нужна зависимость от tooensure учетной записи хранилища hello, он создан до hello виртуальной машины. В рамках hello `storageProfile` статьи, затем укажите hello полный URI hello расположение виртуального жесткого диска, которое ссылается на учетную запись хранения hello и необходим для диска hello ОС и дисков данных. 

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

## <a name="managed-disks-template-formatting"></a>Формат шаблона с управляемыми дисками

С дисками управляемых Azure hello диска становится ресурс верхнего уровня и больше не требуется toobe учетной записи хранилища, созданных пользователем hello. Управляемый диски сначала были видны в hello `2016-04-30-preview` версия API, они доступны во всех последующих версиях API и теперь тип диска по умолчанию hello. Hello следующих разделах Пройдите по умолчанию hello и подробно описывается настройка toofurther дисков.

> [!NOTE]
> Рекомендуется версия toouse API-Интерфейс, более поздней, чем `2016-04-30-preview` как критические изменения между `2016-04-30-preview` и `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Параметры управляемого диска по умолчанию

toocreate виртуальную Машину с управляемых диски, вы больше не требуется ресурс учетной записи хранения toocreate hello и обновить ресурс виртуальной машины следующим образом. В частности Обратите внимание, что hello `apiVersion` отражает `2017-03-30` и hello `osDisk` и `dataDisks` больше не ссылаются tooa указанного URI для hello виртуального жесткого диска. При развертывании без указания дополнительных свойств, будет использовать диск hello [хранения Standard-LRS](../articles/storage/common/storage-redundancy.md). Если имя не указано, оно имеет формат hello `<VMName>_OsDisk_1_<randomstring>` для диска ОС hello и `<VMName>_disk<#>_<randomstring>` для каждого диска данных. По умолчанию шифрование диска Azure отключено; кэширование — чтение и запись для диска ОС hello, а не для дисков данных. Можно заметить в приведенном ниже примере hello, что по-прежнему зависимость учетной записи хранилища, хотя это только для хранения диагностических данных, не требуется для хранения на диске.

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

### <a name="using-a-top-level-managed-disk-resource"></a>Использование ресурса управляемого диска верхнего уровня

Настройки конфигурации диска hello альтернативных toospecifying hello объекта виртуальной машины можно создать ресурс верхнего уровня диска и присоединить ее как часть создания виртуальной машины hello. Например можно создать дисковый ресурс toouse в качестве диска данных следующим образом.

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

В рамках hello объекта виртуальной Машины можно затем сослаться присоединенного объекта toobe этот диск система. Указав идентификатор ресурса hello hello управляемого диска, мы создали hello `managedDisk` свойство позволяет hello вложения hello диска в качестве виртуальной Машины создается hello. Обратите внимание, что hello `apiVersion` для hello ресурса виртуальной Машины установлен слишком`2017-03-30`. Также Обратите внимание, что мы создали зависимость на tooensure ресурсов диска hello, которую он успешно создан, прежде чем создание виртуальной Машины. 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Создание управляемых групп доступности с виртуальными машинами, использующими управляемые диски

toocreate управляемых доступности наборы с виртуальными машинами с помощью управляемых дисков добавить hello `sku` доступности toohello объекта набора ресурсов и набора hello `name` свойство слишком`Aligned`. Это гарантирует, что hello дисков для каждой виртуальной Машины достаточно изолированы от друг с другом tooavoid единых точек отказа. Также Обратите внимание, что hello `apiVersion` ресурсу набора hello доступности задается слишком`2017-03-30`.

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

### <a name="additional-scenarios-and-customizations"></a>Дополнительные сценарии и настройки

toofind полные сведения о спецификациях API-интерфейса REST hello, см. в статье hello [создания управляемой дисковой документация по REST API](/rest/api/manageddisks/disks/disks-create-or-update). Вы найдете дополнительные сценарии, а также по умолчанию и допустимые значения, которые могут быть отправлено toohello API с помощью шаблонов-развертываний. 

## <a name="next-steps"></a>Дальнейшие действия

* Для полного шаблонов, использующие управляемые диски посетите hello ссылкам репозитория быстрый запуск Azure.
    * [Виртуальная машина Windows с управляемыми дисками](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [Виртуальная машина Linux с управляемыми дисками](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Полный список шаблонов с управляемыми дисками](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Посетите hello [Обзор управляемых дисков Azure](../articles/virtual-machines/windows/managed-disks-overview.md) управляемых документа toolearn Дополнительные сведения о дисках.
* Просмотрите hello шаблона справочную документацию для ресурсов виртуальных машин, перейдя по адресу hello [ссылка на шаблон Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) документа.
* Просмотрите hello шаблона справочную документацию по дисковых ресурсов, перейдя по адресу hello [ссылка на шаблон Microsoft.Compute/disks](/templates/microsoft.compute/disks) документа.
 
