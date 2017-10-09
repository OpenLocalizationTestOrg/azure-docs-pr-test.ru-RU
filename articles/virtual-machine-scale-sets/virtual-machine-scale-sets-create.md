---
title: "набор масштабирования виртуальной машины Azure aaaCreate | Документы Microsoft"
description: "Создание и развертывание масштабируемого набора виртуальных машин Linux или Windows в Azure с помощью Azure CLI, PowerShell, шаблона или Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>Создание и развертывание масштабируемого набора виртуальных машин
Наборы масштабирования виртуальных машин упростить для вас toodeploy идентичные виртуальных машин и управление как набор. Масштабируемые наборы обеспечивают высокую степень масштабируемости и персонализацию уровня вычислений для гипермасштабируемых приложений. Кроме того, они поддерживают образы платформ Windows и Linux, а также пользовательские образы и расширения. Дополнительные сведения о масштабируемых наборах см. в разделе [Общие сведения о масштабируемых наборах виртуальных машин в Azure](virtual-machine-scale-sets-overview.md).

В этом учебнике показано, как toocreate набора масштабирования виртуальных машин **без** с помощью портала Azure "hello". Сведения о как toouse hello портала Azure см. в разделе [как toocreate набора масштабирования виртуальных машин с портала Azure hello](virtual-machine-scale-sets-portal-create.md).

>[!NOTE]
>Дополнительные сведения о ресурсах Azure Resource Manager см. в статье [Развертывание с помощью Azure Resource Manager и классическое развертывание: сведения о моделях развертывания и состоянии ресурсов](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="sign-in-tooazure"></a>Войдите в tooAzure

Если вы используете Azure CLI 2.0 или Azure PowerShell toocreate шкалу задано, необходимо сначала toosign в tooyour подписки.

Дополнительные сведения о статье tooinstall, настроить и войдите в tooAzure с помощью Azure CLI или PowerShell, [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) или [приступить к работе с помощью командлетов Azure PowerShell](/powershell/azure/overview).

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Необходимо сначала toocreate группы ресурсов, набора масштабирования виртуальных машин hello с которым связан.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Создание с помощью Azure CLI

Создать масштабируемый набор виртуальных машин с помощью Azure CLI достаточно просто. Если не указать значения по умолчанию, они будут заданы автоматически. Например, если не указать данные виртуальной сети, она будет создана автоматически. При отсутствии hello следующие элементы, они создаются: 
- подсистема балансировки нагрузки;
- виртуальную сеть;
- общедоступный IP-адрес.

При выборе hello образ виртуальной машины, которые должны toouse на hello набора масштабирования виртуальных машин, у вас есть несколько вариантов:

- URN  
Идентификатор ресурса Hello:  
**Win2012R2Datacenter**.

- Псевдоним URN  
Hello понятное имя универсального имени ресурса:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**.

- Идентификатор настраиваемого ресурса  
tooan путь Hello ресурсов Azure:  
**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**.

- Веб-ресурс  
Hello tooan пути HTTP URI:  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**.

>[!TIP]
>Список доступных образов можно получить с помощью команды `az vm image list`.

набор масштабирования виртуальных машин toocreate, необходимо указать следующие hello:

- Группа ресурсов 
- Имя
- образ операционной системы;
- данные аутентификации. 
 
Следующий пример Hello создает базовый набор масштабирования виртуальной машины (этот шаг может занять несколько минут).

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

После завершения выполнения команды hello теперь имеется шкала созданной виртуальной машины. IP-адрес tooget hello hello виртуальной машины может понадобиться, чтобы вы могли подключаться tooit. Вы можете получить множество различных сведений о виртуальной машине hello (включая hello IP-адрес) с hello следующую команду. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>Создание с помощью PowerShell

PowerShell — toouse сложнее, чем Azure CLI. Azure CLI предоставляет значения по умолчанию для сетевых ресурсов (таких как подсистемы балансировки нагрузки, IP-адреса и виртуальные сети), а PowerShell — нет. Также с помощью PowerShell немного сложнее указать образ. Изображения можно получать с hello следующие командлеты:

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

командлеты работают Hello можно направить в последовательности. Ниже приведен пример как tooget все образы для hello **Западная часть США 2** область с издателем с именем hello **microsoft** в нем.

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

Hello рабочий процесс для создания набора масштабирования виртуальных машин выглядит следующим образом:

1. Создайте объект конфигурации, который содержит сведения о наборе масштабирования hello.
2. Справочник по hello базовый образ ОС.
3. Настройте параметры операционной системы hello: проверка подлинности, префикс имени виртуальной Машины и передача/пользователя.
4. Настройте сеть.
5. Создайте набор масштабирования hello.

В этом примере создается простой масштабируемый набор с двумя экземплярами для компьютера под управлением Windows Server 2016.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>Использование образов настраиваемой виртуальной машины
При создании набора из собственного пользовательского изображения вместо ссылки на образ виртуальной машины из коллекции hello шкалы hello _AzureRmVmssStorageProfile набор_ команда будет выглядеть следующим образом:
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>Создание с помощью шаблона

Вы можете развернуть масштабируемый набор виртуальных машин с помощью шаблона Azure Resource Manager. Можно создать собственный шаблон или использовать один из hello [шаблон репозитория](https://azure.microsoft.com/resources/templates/?term=vmss). Эти шаблоны можно развернуть напрямую tooyour подписки Azure.

>[!NOTE]
>toocreate собственный шаблон, создайте файл JSON. Общие сведения о том, как toocreate и настройки шаблона см. в разделе [шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Пример шаблона доступен на [сайте GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set). Дополнительные сведения о том, как отображается toocreate и использовать этот пример, [минимальный набор реальную масштабирования](.\virtual-machine-scale-sets-mvss-start.md).

## <a name="create-from-visual-studio"></a>Создание с помощью Visual Studio

С помощью Visual Studio можно создать проект группы ресурсов Azure и добавить шаблон tooit набор масштабирования виртуальных машин. Можно выбрать, следует ли tooimport из GitHub или hello Azure коллекции веб-приложений. Кроме того, автоматически создается сценарий PowerShell для развертывания. Дополнительные сведения см. в разделе [как toocreate набора масштабирования виртуальных машин с помощью Visual Studio](virtual-machine-scale-sets-vs-create.md).

## <a name="create-from-hello-azure-portal"></a>Создать из hello портал Azure

Hello портал Azure предоставляет удобный способ tooquickly создания набора масштабирования. Дополнительные сведения см. в разделе [как toocreate набора масштабирования виртуальных машин с портала Azure hello](virtual-machine-scale-sets-portal-create.md).

## <a name="next-steps"></a>Дальнейшие действия

Узнайте больше о [дисках данных](virtual-machine-scale-sets-attached-disks.md).

Узнайте, каким образом слишком[управлять приложениями](virtual-machine-scale-sets-deploy-app.md).
