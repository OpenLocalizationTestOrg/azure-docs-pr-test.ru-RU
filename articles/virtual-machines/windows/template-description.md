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
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="a7002-103">Виртуальные машины в шаблоне Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a7002-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="a7002-104">В этой статье описываются аспекты шаблона диспетчера ресурсов Azure, применяются toovirtual машины.</span><span class="sxs-lookup"><span data-stu-id="a7002-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="a7002-105">Здесь не описывается полный шаблон для создания виртуальной машины. Для этого требуются определения ресурсов для учетных записей хранения, сетевых интерфейсов, общедоступных IP-адресов и виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="a7002-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="a7002-106">Дополнительные сведения об этих ресурсов определение вместе см. в разделе hello [Пошаговое руководство диспетчера ресурсов шаблона](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a7002-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="a7002-107">Существует много [шаблоны в галерее hello](https://azure.microsoft.com/documentation/templates/?term=VM) , содержащих hello ресурса виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a7002-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="a7002-108">Здесь описываются не все элементы, которые могут быть включены в шаблон.</span><span class="sxs-lookup"><span data-stu-id="a7002-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="a7002-109">В этом примере показан типичный раздел ресурсов шаблона для создания указанного числа виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a7002-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="a7002-110">Этот пример основан на учетной записи хранения, которая была создана ранее.</span><span class="sxs-lookup"><span data-stu-id="a7002-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="a7002-111">Можно создать учетную запись хранения hello счет ее развертывания на основе шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="a7002-112">пример Hello зависит от сетевого интерфейса и ее зависимые ресурсы, которые должны быть определены в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="a7002-113">Эти ресурсы не отображаются в примере hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="a7002-114">Версия API</span><span class="sxs-lookup"><span data-stu-id="a7002-114">API Version</span></span>

<span data-ttu-id="a7002-115">При развертывании ресурсов с помощью шаблона toospecify имеется версия hello API toouse.</span><span class="sxs-lookup"><span data-stu-id="a7002-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="a7002-116">Hello пример hello ресурса виртуальной машины, с помощью этого элемента apiVersion.</span><span class="sxs-lookup"><span data-stu-id="a7002-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="a7002-117">версия Hello hello API, указанной в шаблоне влияет на свойства, которые можно определить в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="a7002-118">В общем случае следует выбрать самую последнюю версию API hello при создании шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a7002-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="a7002-119">Для существующих шаблонов можно ли будет toocontinue используется более ранняя версия API или обновления шаблона для hello последнюю версию tootake преимуществами новых функций.</span><span class="sxs-lookup"><span data-stu-id="a7002-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="a7002-120">Используйте эти возможности для получения последней версии API hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="a7002-121">Для REST API выполните операцию [вывода списка всех поставщиков ресурсов](https://docs.microsoft.com/rest/api/resources/providers#Providers_List).</span><span class="sxs-lookup"><span data-stu-id="a7002-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="a7002-122">В PowerShell используйте командлет [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider).</span><span class="sxs-lookup"><span data-stu-id="a7002-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="a7002-123">Azure CLI 2.0: [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="a7002-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="a7002-124">Параметры и переменные</span><span class="sxs-lookup"><span data-stu-id="a7002-124">Parameters and variables</span></span>

<span data-ttu-id="a7002-125">[Параметры](../../resource-group-authoring-templates.md) упростить для вас toospecify значения для шаблона hello при его запуске.</span><span class="sxs-lookup"><span data-stu-id="a7002-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="a7002-126">Этот раздел параметров используется в примере hello:</span><span class="sxs-lookup"><span data-stu-id="a7002-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="a7002-127">При развертывании шаблона пример hello, введите значения для hello имя и пароль учетной записи администратора hello на каждой виртуальной Машине и hello число toocreate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a7002-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="a7002-128">Предусмотрена возможность hello указывать значения параметров в отдельном файле, который управляется с помощью шаблона hello, или указать значения при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="a7002-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="a7002-129">[Переменные](../../resource-group-authoring-templates.md) упростить для вас tooset значения в шаблоне hello, которые многократно используются на протяжении его или, может изменяться со временем.</span><span class="sxs-lookup"><span data-stu-id="a7002-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="a7002-130">В этом разделе переменных используется в примере hello:</span><span class="sxs-lookup"><span data-stu-id="a7002-130">This variables section is used in hello example:</span></span>

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

<span data-ttu-id="a7002-131">При развертывании шаблона пример hello, значения переменных используются для hello имя и идентификатор hello ранее созданную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a7002-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="a7002-132">Переменные также не используется tooprovide параметров hello hello диагностического расширения.</span><span class="sxs-lookup"><span data-stu-id="a7002-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="a7002-133">Используйте hello [советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](../../resource-manager-template-best-practices.md) toohelp, можно выбрать способ toostructure hello параметров и переменных в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="a7002-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="a7002-134">цикла ресурсов</span><span class="sxs-lookup"><span data-stu-id="a7002-134">Resource loops</span></span>

<span data-ttu-id="a7002-135">Если для приложения требуется несколько виртуальных машин, в шаблоне можно использовать элемент копирования.</span><span class="sxs-lookup"><span data-stu-id="a7002-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="a7002-136">Этот необязательный элемент циклически создания hello количества виртуальных машин, указанное в качестве параметра:</span><span class="sxs-lookup"><span data-stu-id="a7002-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="a7002-137">Кроме того Обратите внимание, в примере hello, hello индекс цикла используется при указании некоторых hello значений для ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="a7002-138">Например если вы ввели число экземпляров имена трех, hello hello дисков операционной системы: myOSDisk1, myOSDisk2 и myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="a7002-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="a7002-139">В этом примере используются управляемые диски для виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="a7002-140">Имейте в виду, что создание цикл для одного ресурса в шаблоне hello может потребовать вы toouse hello цикла при создании или доступ к другим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="a7002-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="a7002-141">Например несколько виртуальных машин невозможно использовать hello же сетевой интерфейс, поэтому если шаблон циклически создание трех виртуальных машин, также необходимо циклический перебор по созданию три сетевых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="a7002-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="a7002-142">При назначении tooa интерфейса сети виртуальной Машины, индекс цикла hello — используется tooidentify его:</span><span class="sxs-lookup"><span data-stu-id="a7002-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="a7002-143">Зависимости</span><span class="sxs-lookup"><span data-stu-id="a7002-143">Dependencies</span></span>

<span data-ttu-id="a7002-144">Наибольшее число ресурсов зависят другие ресурсы toowork правильно.</span><span class="sxs-lookup"><span data-stu-id="a7002-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="a7002-145">Виртуальные машины должна быть связана с виртуальной сетью и toodo, что ему требуется сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a7002-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="a7002-146">Hello [dependsOn](../../resource-group-define-dependencies.md) элемент является используется toomake, что этот сетевой интерфейс hello готов toobe используется перед созданием виртуальных машин hello:</span><span class="sxs-lookup"><span data-stu-id="a7002-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="a7002-147">Resource Manager параллельно развертывает все ресурсы, которые не зависят от развертывания других ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a7002-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="a7002-148">Будьте осторожны при установке зависимостей, так как можно случайно замедлить развертывания, указав ненужные зависимости.</span><span class="sxs-lookup"><span data-stu-id="a7002-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="a7002-149">С помощью зависимостей можно связать несколько ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a7002-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="a7002-150">Например сетевой интерфейс hello зависит hello общедоступный IP-адрес и ресурсы виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a7002-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="a7002-151">Как узнать, требуется ли зависимость?</span><span class="sxs-lookup"><span data-stu-id="a7002-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="a7002-152">Рассмотрим hello значения, заданные в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="a7002-153">Если элемент в определении ресурса виртуальной машины hello указывает tooanother ресурсу, развертываемому в hello того же шаблона необходимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="a7002-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="a7002-154">Например, в примере виртуальный машины определен профиль сети.</span><span class="sxs-lookup"><span data-stu-id="a7002-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="a7002-155">tooset это свойство hello сетевой интерфейс должен существовать.</span><span class="sxs-lookup"><span data-stu-id="a7002-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="a7002-156">Поэтому требуется зависимость.</span><span class="sxs-lookup"><span data-stu-id="a7002-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="a7002-157">Требуется также tooset зависимость для другого ресурса (родительский) определяется один ресурс (дочерний).</span><span class="sxs-lookup"><span data-stu-id="a7002-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="a7002-158">Например параметры диагностики hello и расширения пользовательского скрипта определены как дочерние ресурсы виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="a7002-159">Они не могут создаваться до hello виртуальная машина существует.</span><span class="sxs-lookup"><span data-stu-id="a7002-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="a7002-160">Таким образом оба ресурса, помечаются как зависимость от hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a7002-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="a7002-161">Профили</span><span class="sxs-lookup"><span data-stu-id="a7002-161">Profiles</span></span>

<span data-ttu-id="a7002-162">При определении ресурса виртуальной машины используются несколько элементов профиля.</span><span class="sxs-lookup"><span data-stu-id="a7002-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="a7002-163">Некоторые являются обязательными, а другие — необязательными.</span><span class="sxs-lookup"><span data-stu-id="a7002-163">Some are required and some are optional.</span></span> <span data-ttu-id="a7002-164">Например элементы hardwareProfile, osProfile, storageProfile и параметров масштабирования виртуальных hello являются обязательными, но hello diagnosticsProfile является необязательным.</span><span class="sxs-lookup"><span data-stu-id="a7002-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="a7002-165">С помощью этих профилей задаются следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a7002-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="a7002-166">размер;</span><span class="sxs-lookup"><span data-stu-id="a7002-166">size</span></span>](sizes.md)
- <span data-ttu-id="a7002-167">[имя](/architecture/best-practices/naming-conventions) и учетные данные;</span><span class="sxs-lookup"><span data-stu-id="a7002-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="a7002-168">диск и [параметры операционной системы;](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="a7002-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="a7002-169">сетевой интерфейс;</span><span class="sxs-lookup"><span data-stu-id="a7002-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="a7002-170">диагностика загрузки.</span><span class="sxs-lookup"><span data-stu-id="a7002-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="a7002-171">Диски и образы</span><span class="sxs-lookup"><span data-stu-id="a7002-171">Disks and images</span></span>
   
<span data-ttu-id="a7002-172">В Azure файлы VHD могут представлять [диски или образы](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7002-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a7002-173">При hello операционной системы в файле vhd специализированные toobe определенную виртуальную Машину, это будет ссылка tooas диска.</span><span class="sxs-lookup"><span data-stu-id="a7002-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="a7002-174">Когда обобщенный hello операционной системы в файле vhd toobe используется toocreate много виртуальных машин, ссылка tooas изображения.</span><span class="sxs-lookup"><span data-stu-id="a7002-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="a7002-175">Создание новых виртуальных машин и новых дисков с помощью образа платформы</span><span class="sxs-lookup"><span data-stu-id="a7002-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="a7002-176">При создании виртуальной Машины, необходимо решить, какие toouse операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a7002-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="a7002-177">Hello объекта imageReference элемент является используется toodefine hello операционной системы для новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a7002-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="a7002-178">пример Hello показано определение для операционной системы Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a7002-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="a7002-179">Если вы хотите toocreate операционной системы Linux, можно использовать это определение:</span><span class="sxs-lookup"><span data-stu-id="a7002-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="a7002-180">Параметры конфигурации для диска операционной системы hello назначаются с помощью элемента osDisk hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="a7002-181">Hello примере определяется новый управляемого диска с hello кэширования набора в режиме слишком**ReadWrite** и этот диск hello создается из [образа платформы](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="a7002-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="a7002-182">Создание виртуальных машин из существующих управляемых дисков</span><span class="sxs-lookup"><span data-stu-id="a7002-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="a7002-183">Если требуется toocreate виртуальных машин из существующих дисков, удалить объект imageReference hello и элементы osProfile hello и определить параметры диска:</span><span class="sxs-lookup"><span data-stu-id="a7002-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="a7002-184">Создание виртуальных машин из управляемого образа</span><span class="sxs-lookup"><span data-stu-id="a7002-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="a7002-185">Если требуется, чтобы toocreate виртуальной машины из образа управляемого измените элемент imageReference hello и определить следующие параметры диска:</span><span class="sxs-lookup"><span data-stu-id="a7002-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="a7002-186">Присоединение дисков данных</span><span class="sxs-lookup"><span data-stu-id="a7002-186">Attach data disks</span></span>

<span data-ttu-id="a7002-187">При необходимости можно добавить toohello дисков данных ВМ.</span><span class="sxs-lookup"><span data-stu-id="a7002-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="a7002-188">Hello [номера дисков](sizes.md) зависит от размера hello диска операционной системы, который используется.</span><span class="sxs-lookup"><span data-stu-id="a7002-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="a7002-189">Размер виртуальных машин hello hello установите tooStandard_DS1_v2 hello максимальное число дисков данных, которые могут быть добавлены toohello их равно двум.</span><span class="sxs-lookup"><span data-stu-id="a7002-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="a7002-190">В примере hello один диск управляемых данных добавляется tooeach виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="a7002-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="a7002-191">расширения.</span><span class="sxs-lookup"><span data-stu-id="a7002-191">Extensions</span></span>

<span data-ttu-id="a7002-192">Несмотря на то что [расширения](extensions-features.md) это отдельный ресурс, тесно связанные tooVMs.</span><span class="sxs-lookup"><span data-stu-id="a7002-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="a7002-193">Расширения можно добавить как ресурс дочерних hello виртуальной Машины или как отдельный ресурс.</span><span class="sxs-lookup"><span data-stu-id="a7002-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="a7002-194">Пример hello Hello [расширения диагностики](extensions-diagnostics-template.md) добавляемый toohello виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="a7002-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

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

<span data-ttu-id="a7002-195">Этот ресурс расширение использует hello storageName переменной и значения tooprovide диагностические переменные hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="a7002-196">Если требуется toochange hello данные, собранные этим модулем, ее можно добавить дополнительные производительности счетчики toohello wadperfcounters.</span><span class="sxs-lookup"><span data-stu-id="a7002-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="a7002-197">Вы можете выбрать tooput hello диагностические данные в другую учетную запись хранения чем хранения hello дисков виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a7002-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="a7002-198">Существует несколько модулей, которые можно установить на виртуальной Машине, но наиболее полезные hello, вероятно, является hello [настраиваемое расширение скриптов](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="a7002-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="a7002-199">В примере hello сценария PowerShell с именем start.ps1 работает на каждой виртуальной Машине при первом запуске.</span><span class="sxs-lookup"><span data-stu-id="a7002-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="a7002-200">сценарий start.ps1 Hello можно выполнять многие задачи конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a7002-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="a7002-201">Например не инициализируются hello дисков данных, которые добавляются в примере hello toohello виртуальных машин; можно использовать пользовательский сценарий tooinitialize их.</span><span class="sxs-lookup"><span data-stu-id="a7002-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="a7002-202">При наличии нескольких toodo задачи запуска, можно использовать toocall файл start.ps1 hello других сценариев PowerShell в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="a7002-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="a7002-203">пример Hello использует PowerShell, но можно использовать любой метод формирования сценариев, доступные в операционной системе hello, в которых используется.</span><span class="sxs-lookup"><span data-stu-id="a7002-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="a7002-204">Можно просмотреть состояние hello hello установлены расширения из параметров расширения hello hello портала:</span><span class="sxs-lookup"><span data-stu-id="a7002-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![Получение состояния расширения](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="a7002-206">Можно также получить сведения о моделях с помощью hello **Get AzureRmVMExtension** PowerShell команды hello **get расширения виртуальной машины** hello или Azure CLI 2.0 команды **получения сведений о расширении**  API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="a7002-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="a7002-207">Развернутые приложения</span><span class="sxs-lookup"><span data-stu-id="a7002-207">Deployments</span></span>

<span data-ttu-id="a7002-208">При развертывании шаблона ресурсов Azure отслеживает hello, развернутые в группу и автоматически назначение имени группы toothis развертывания.</span><span class="sxs-lookup"><span data-stu-id="a7002-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="a7002-209">Имя Hello hello развертывания является hello совпадает с именем hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="a7002-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="a7002-210">Если вы не хотите узнать состояние hello ресурсов в развертывании hello, можно использовать колонки hello группы ресурсов в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="a7002-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![Получение сведений о развертывании](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="a7002-212">Это не проблема toouse hello и те же ресурсы toocreate шаблона или tooupdate существующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a7002-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="a7002-213">При использовании команды toodeploy шаблонов, у вас есть возможность toosay hello которой [режим](../../resource-group-template-deploy.md) требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="a7002-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="a7002-214">Hello режима можно задать tooeither **завершить** или **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="a7002-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="a7002-215">по умолчанию Hello-toodo добавочные обновления.</span><span class="sxs-lookup"><span data-stu-id="a7002-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="a7002-216">Будьте внимательны при использовании hello **завершить** режиме, поскольку можно случайно удалить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a7002-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="a7002-217">При задании режима hello слишком**завершить**, диспетчер ресурсов удаляет все ресурсы в группе ресурсов hello, не входящие в шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="a7002-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7002-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7002-218">Next Steps</span></span>

- <span data-ttu-id="a7002-219">Сведения о создании собственного шаблона см. в статье [Создание шаблонов Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a7002-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="a7002-220">Развертывание шаблона hello, созданного с помощью [создания виртуальной машины Windows с помощью шаблона диспетчера ресурсов](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="a7002-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="a7002-221">Узнайте, как toomanage hello виртуальных машин, которые вы создали, просмотрев [Создание и управление виртуальными машинами Windows с помощью модуля Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7002-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
