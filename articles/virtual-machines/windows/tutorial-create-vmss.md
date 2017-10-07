---
title: "aaaCreate виртуальной машины шкалы наборов для Windows в Azure | Документы Microsoft"
description: "Создание и развертывание высокодоступного приложения на виртуальных машинах Windows с помощью масштабируемого набора виртуальных машин."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Создание масштабируемого набора виртуальных машин и развертывание высокодоступного приложения в Windows
Набор масштабирования виртуальной машины дает toodeploy и управление набором идентичными, автоматического масштабирования виртуальных машин. Можно вручную масштабировать hello число виртуальных машин в наборе масштабирования hello, или определить tooautoscale правила на основе использования ЦП, объем памяти или сетевой трафик. В рамках этого руководства вы развернете масштабируемый набор виртуальных машин в Azure. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Использовать настраиваемое расширение скриптов hello toodefine tooscale узла IIS
> * Создание балансировщика нагрузки для масштабируемого набора
> * создавать масштабируемый набор виртуальных машин;
> * Увеличение или уменьшение числа hello экземпляров в наборе масштабирования
> * Создание правил автомасштабирования

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Обзор масштабируемого набора
Наборы масштабирования используются одинаковые принципы, как вы узнали о в предыдущем учебнике hello слишком[создать высокодоступные виртуальные машины](tutorial-availability-sets.md). Виртуальные машины в масштабируемом наборе распределяются по доменам сбоя и доменам обновления, как и виртуальные машины в группе доступности.

Виртуальные машины создаются в масштабируемом наборе по мере необходимости. Определение правила toocontrol автомасштабирования как и когда добавляются или удаляются из hello масштабный набор виртуальных машин. Эти правила могут активироваться на основе метрик, таких как использование ЦП, использование памяти или сетевой трафик.

Масштаб задает поддержки вверх too1 000 виртуальных машин при использовании образа платформы Azure. Для рабочих нагрузок с значительные установки или настройки требования виртуальной Машины, вы можете слишком[создать образ виртуальной Машины](tutorial-custom-images.md). Можно создать too100 виртуальных машин в наборе, при использовании настраиваемого образа масштабирования.


## <a name="create-an-app-tooscale"></a>Создание приложения tooscale
Прежде чем создать масштабируемый набор, выполните команду [az group create](/powershell/module/azurerm.resources/new-azurermresourcegroup) для создания группы ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupAutomate* в hello *EastUS* расположение:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

В более ранних учебника вы узнали, каким образом слишком[конфигурацию виртуальной Машины автоматизировать](tutorial-automate-vm-deployment.md) с использованием настраиваемого расширения скриптов "hello". Создание конфигурации набор масштабирования и применить tooinstall настраиваемое расширение скриптов и настроить службы IIS:

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a>Создание подсистемы балансировки нагрузки для масштабируемого набора
Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами. Отслеживает данный порт на каждой виртуальной Машине зонда работоспособности подсистемы балансировки нагрузки и только распределяет трафик tooan оперативной виртуальной Машины. Дополнительные сведения см. Далее учебнике hello на [как tooload сбалансировать виртуальных машин Windows](tutorial-load-balancer.md).

Создайте подсистему балансировки нагрузки с общедоступным IP-адресом, которая распределяет веб-трафик через порт 80.

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a>Создание масштабируемого набора
Теперь создайте масштабируемый набор виртуальных машин с помощью командлета [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm). Hello следующий пример создает именованный наборе масштабирования *myScaleSet*:

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

Он занимает несколько минут toocreate и настроить все hello масштабирования набор ресурсов виртуальных машин.


## <a name="test-your-app"></a>Тестирование приложения
toosee веб-сайта IIS в действии, получить hello общедоступный IP-адрес балансировки нагрузки, с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello следующий пример извлекает hello IP-адрес для *myPublicIP* создана как часть набора масштабирования hello:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Введите hello общедоступный IP-адрес в tooa веб-браузера. будут отображены приложение Hello, включая имя узла виртуальной Машины, hello нагрузки трафика балансировки распределенных для hello hello:

![Выполнение сайта IIS](./media/tutorial-create-vmss/running-iis-site.png)

набор в действии масштабирования hello toosee, вы может принудительное обновление вашего веб-браузера toosee hello нагрузку балансировки распределения трафика между все виртуальные машины hello, запускающий ваше приложение.


## <a name="management-tasks"></a>Задачи управления
На протяжении жизненного цикла hello набора масштабирования hello, может потребоваться toorun одну или несколько задач управления. Кроме того вы можете toocreate скрипты, автоматизирующие различные жизненного цикла задачи. Azure PowerShell предоставляет toodo быстро этих задач. Ниже приведено несколько распространенных задач.

### <a name="view-vms-in-a-scale-set"></a>Просмотр виртуальных машин в масштабируемом наборе
Список виртуальных машин, работающих в шкалу tooview набора, используйте [Get AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) следующим образом:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a>Увеличение или уменьшение числа экземпляров виртуальной машины
число экземпляров hello toosee в настоящее время на шкале установки, используйте [Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) и запросов на *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

Можно затем вручную увеличить или уменьшить hello количество виртуальных машин в наборе с масштабирования hello [AzureRmVmss обновление](/powershell/module/azurerm.compute/update-azurermvmss). Hello следующий пример задает hello число виртуальных машин в ваш набор слишком масштабирования*5*:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

Если несколько минут tooupdate hello указанного числа экземпляров в наборе масштабирования.


### <a name="configure-autoscale-rules"></a>Настройка правил автомасштабирования
Вместо установки вручную масштабирование hello число экземпляров в на шкале, можно определить правила автомасштабирования. Эти правила отслеживать hello экземпляры в шкалу задать и реагировать соответствующим образом на основе метрик и порогов, определенных пользователем. Следующий пример Hello масштабируемостью hello число экземпляров на единицу при hello среднюю нагрузку ЦП больше, чем на 60% в течение 5 минут. Если затем нагрузки Средняя нагрузка на ЦП hello падает ниже 30% в течение 5 минут, экземпляры hello масштабируются в одним экземпляром:

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a>Дальнейшие действия
В рамках этого руководства вы создали набор масштабирования виртуальных машин. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Использовать настраиваемое расширение скриптов hello toodefine tooscale узла IIS
> * Создание балансировщика нагрузки для масштабируемого набора
> * создавать масштабируемый набор виртуальных машин;
> * Увеличение или уменьшение числа hello экземпляров в наборе масштабирования
> * Создание правил автомасштабирования

Дополнительные сведения о понятиях и принципах работы виртуальных машин балансировки нагрузки передвинута Далее учебника toolearn toohello.

> [!div class="nextstepaction"]
> [Балансировка нагрузки между виртуальными машинами](tutorial-load-balancer.md)
