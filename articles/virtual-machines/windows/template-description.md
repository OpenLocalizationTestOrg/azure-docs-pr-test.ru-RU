---
title: "aaaVirtual машины в шаблоне диспетчера ресурсов Azure | Microsoft Azure"
description: "Дополнительные сведения о том, как определяются hello ресурса виртуальной машины в шаблоне диспетчера ресурсов Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Виртуальные машины в шаблоне Azure Resource Manager

В этой статье описываются аспекты шаблона диспетчера ресурсов Azure, применяются toovirtual машины. Здесь не описывается полный шаблон для создания виртуальной машины. Для этого требуются определения ресурсов для учетных записей хранения, сетевых интерфейсов, общедоступных IP-адресов и виртуальных сетей. Дополнительные сведения об этих ресурсов определение вместе см. в разделе hello [Пошаговое руководство диспетчера ресурсов шаблона](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Существует много [шаблоны в галерее hello](https://azure.microsoft.com/documentation/templates/?term=VM) , содержащих hello ресурса виртуальной Машины. Здесь описываются не все элементы, которые могут быть включены в шаблон.

В этом примере показан типичный раздел ресурсов шаблона для создания указанного числа виртуальных машин.

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>Этот пример основан на учетной записи хранения, которая была создана ранее. Можно создать учетную запись хранения hello счет ее развертывания на основе шаблона hello. пример Hello зависит от сетевого интерфейса и ее зависимые ресурсы, которые должны быть определены в шаблоне hello. Эти ресурсы не отображаются в примере hello.
>
>

## <a name="api-version"></a>Версия API

При развертывании ресурсов с помощью шаблона toospecify имеется версия hello API toouse. Hello пример hello ресурса виртуальной машины, с помощью этого элемента apiVersion.

```
"apiVersion": "2016-04-30-preview",
```

версия Hello hello API, указанной в шаблоне влияет на свойства, которые можно определить в шаблоне hello. В общем случае следует выбрать самую последнюю версию API hello при создании шаблонов. Для существующих шаблонов можно ли будет toocontinue используется более ранняя версия API или обновления шаблона для hello последнюю версию tootake преимуществами новых функций.

Используйте эти возможности для получения последней версии API hello.

- Для REST API выполните операцию [вывода списка всех поставщиков ресурсов](https://docs.microsoft.com/rest/api/resources/providers#Providers_List).
- В PowerShell используйте командлет [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider).
- Azure CLI 2.0: [az provider show](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>Параметры и переменные

[Параметры](../../resource-group-authoring-templates.md) упростить для вас toospecify значения для шаблона hello при его запуске. Этот раздел параметров используется в примере hello:

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

При развертывании шаблона пример hello, введите значения для hello имя и пароль учетной записи администратора hello на каждой виртуальной Машине и hello число toocreate виртуальных машин. Предусмотрена возможность hello указывать значения параметров в отдельном файле, который управляется с помощью шаблона hello, или указать значения при появлении запроса.

[Переменные](../../resource-group-authoring-templates.md) упростить для вас tooset значения в шаблоне hello, которые многократно используются на протяжении его или, может изменяться со временем. В этом разделе переменных используется в примере hello:

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

При развертывании шаблона пример hello, значения переменных используются для hello имя и идентификатор hello ранее созданную учетную запись хранения. Переменные также не используется tooprovide параметров hello hello диагностического расширения. Используйте hello [советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](../../resource-manager-template-best-practices.md) toohelp, можно выбрать способ toostructure hello параметров и переменных в шаблоне.

## <a name="resource-loops"></a>цикла ресурсов

Если для приложения требуется несколько виртуальных машин, в шаблоне можно использовать элемент копирования. Этот необязательный элемент циклически создания hello количества виртуальных машин, указанное в качестве параметра:

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

Кроме того Обратите внимание, в примере hello, hello индекс цикла используется при указании некоторых hello значений для ресурса hello. Например если вы ввели число экземпляров имена трех, hello hello дисков операционной системы: myOSDisk1, myOSDisk2 и myOSDisk3:

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>В этом примере используются управляемые диски для виртуальных машин hello.
>
>

Имейте в виду, что создание цикл для одного ресурса в шаблоне hello может потребовать вы toouse hello цикла при создании или доступ к другим ресурсам. Например несколько виртуальных машин невозможно использовать hello же сетевой интерфейс, поэтому если шаблон циклически создание трех виртуальных машин, также необходимо циклический перебор по созданию три сетевых интерфейсов. При назначении tooa интерфейса сети виртуальной Машины, индекс цикла hello — используется tooidentify его:

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>Зависимости

Наибольшее число ресурсов зависят другие ресурсы toowork правильно. Виртуальные машины должна быть связана с виртуальной сетью и toodo, что ему требуется сетевого интерфейса. Hello [dependsOn](../../resource-group-define-dependencies.md) элемент является используется toomake, что этот сетевой интерфейс hello готов toobe используется перед созданием виртуальных машин hello:

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

Resource Manager параллельно развертывает все ресурсы, которые не зависят от развертывания других ресурсов. Будьте осторожны при установке зависимостей, так как можно случайно замедлить развертывания, указав ненужные зависимости. С помощью зависимостей можно связать несколько ресурсов. Например сетевой интерфейс hello зависит hello общедоступный IP-адрес и ресурсы виртуальной сети.

Как узнать, требуется ли зависимость? Рассмотрим hello значения, заданные в шаблоне hello. Если элемент в определении ресурса виртуальной машины hello указывает tooanother ресурсу, развертываемому в hello того же шаблона необходимые зависимости. Например, в примере виртуальный машины определен профиль сети.

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset это свойство hello сетевой интерфейс должен существовать. Поэтому требуется зависимость. Требуется также tooset зависимость для другого ресурса (родительский) определяется один ресурс (дочерний). Например параметры диагностики hello и расширения пользовательского скрипта определены как дочерние ресурсы виртуальной машины hello. Они не могут создаваться до hello виртуальная машина существует. Таким образом оба ресурса, помечаются как зависимость от hello виртуальной машины.

## <a name="profiles"></a>Профили

При определении ресурса виртуальной машины используются несколько элементов профиля. Некоторые являются обязательными, а другие — необязательными. Например элементы hardwareProfile, osProfile, storageProfile и параметров масштабирования виртуальных hello являются обязательными, но hello diagnosticsProfile является необязательным. С помощью этих профилей задаются следующие параметры:
   
- [размер;](sizes.md)
- [имя](/architecture/best-practices/naming-conventions) и учетные данные;
- диск и [параметры операционной системы;](cli-ps-findimage.md)
- [сетевой интерфейс;](../../virtual-network/virtual-networks-multiple-nics.md) 
- диагностика загрузки.

## <a name="disks-and-images"></a>Диски и образы
   
В Azure файлы VHD могут представлять [диски или образы](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). При hello операционной системы в файле vhd специализированные toobe определенную виртуальную Машину, это будет ссылка tooas диска. Когда обобщенный hello операционной системы в файле vhd toobe используется toocreate много виртуальных машин, ссылка tooas изображения.   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>Создание новых виртуальных машин и новых дисков с помощью образа платформы

При создании виртуальной Машины, необходимо решить, какие toouse операционной системы. Hello объекта imageReference элемент является используется toodefine hello операционной системы для новой виртуальной Машины. пример Hello показано определение для операционной системы Windows Server.

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

Если вы хотите toocreate операционной системы Linux, можно использовать это определение:

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Параметры конфигурации для диска операционной системы hello назначаются с помощью элемента osDisk hello. Hello примере определяется новый управляемого диска с hello кэширования набора в режиме слишком**ReadWrite** и этот диск hello создается из [образа платформы](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>Создание виртуальных машин из существующих управляемых дисков

Если требуется toocreate виртуальных машин из существующих дисков, удалить объект imageReference hello и элементы osProfile hello и определить параметры диска:

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>Создание виртуальных машин из управляемого образа

Если требуется, чтобы toocreate виртуальной машины из образа управляемого измените элемент imageReference hello и определить следующие параметры диска:

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>Присоединение дисков данных

При необходимости можно добавить toohello дисков данных ВМ. Hello [номера дисков](sizes.md) зависит от размера hello диска операционной системы, который используется. Размер виртуальных машин hello hello установите tooStandard_DS1_v2 hello максимальное число дисков данных, которые могут быть добавлены toohello их равно двум. В примере hello один диск управляемых данных добавляется tooeach виртуальной Машины:

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>расширения.

Несмотря на то что [расширения](extensions-features.md) это отдельный ресурс, тесно связанные tooVMs. Расширения можно добавить как ресурс дочерних hello виртуальной Машины или как отдельный ресурс. Пример hello Hello [расширения диагностики](extensions-diagnostics-template.md) добавляемый toohello виртуальных машин:

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Этот ресурс расширение использует hello storageName переменной и значения tooprovide диагностические переменные hello. Если требуется toochange hello данные, собранные этим модулем, ее можно добавить дополнительные производительности счетчики toohello wadperfcounters. Вы можете выбрать tooput hello диагностические данные в другую учетную запись хранения чем хранения hello дисков виртуальной Машины.

Существует несколько модулей, которые можно установить на виртуальной Машине, но наиболее полезные hello, вероятно, является hello [настраиваемое расширение скриптов](extensions-customscript.md). В примере hello сценария PowerShell с именем start.ps1 работает на каждой виртуальной Машине при первом запуске.

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

сценарий start.ps1 Hello можно выполнять многие задачи конфигурации. Например не инициализируются hello дисков данных, которые добавляются в примере hello toohello виртуальных машин; можно использовать пользовательский сценарий tooinitialize их. При наличии нескольких toodo задачи запуска, можно использовать toocall файл start.ps1 hello других сценариев PowerShell в хранилище Azure. пример Hello использует PowerShell, но можно использовать любой метод формирования сценариев, доступные в операционной системе hello, в которых используется.

Можно просмотреть состояние hello hello установлены расширения из параметров расширения hello hello портала:

![Получение состояния расширения](./media/template-description/virtual-machines-show-extensions.png)

Можно также получить сведения о моделях с помощью hello **Get AzureRmVMExtension** PowerShell команды hello **get расширения виртуальной машины** hello или Azure CLI 2.0 команды **получения сведений о расширении**  API-интерфейса REST.

## <a name="deployments"></a>Развернутые приложения

При развертывании шаблона ресурсов Azure отслеживает hello, развернутые в группу и автоматически назначение имени группы toothis развертывания. Имя Hello hello развертывания является hello совпадает с именем hello hello шаблона.

Если вы не хотите узнать состояние hello ресурсов в развертывании hello, можно использовать колонки hello группы ресурсов в hello портала Azure:

![Получение сведений о развертывании](./media/template-description/virtual-machines-deployment-info.png)
    
Это не проблема toouse hello и те же ресурсы toocreate шаблона или tooupdate существующие ресурсы. При использовании команды toodeploy шаблонов, у вас есть возможность toosay hello которой [режим](../../resource-group-template-deploy.md) требуется toouse. Hello режима можно задать tooeither **завершить** или **Incremental**. по умолчанию Hello-toodo добавочные обновления. Будьте внимательны при использовании hello **завершить** режиме, поскольку можно случайно удалить ресурсы. При задании режима hello слишком**завершить**, диспетчер ресурсов удаляет все ресурсы в группе ресурсов hello, не входящие в шаблон hello.

## <a name="next-steps"></a>Дальнейшие действия

- Сведения о создании собственного шаблона см. в статье [Создание шаблонов Azure Resource Manager](../../resource-group-authoring-templates.md).
- Развертывание шаблона hello, созданного с помощью [создания виртуальной машины Windows с помощью шаблона диспетчера ресурсов](ps-template.md).
- Узнайте, как toomanage hello виртуальных машин, которые вы создали, просмотрев [Создание и управление виртуальными машинами Windows с помощью модуля Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
