---
title: "образы aaaSelect виртуальной Машины Windows в Azure | Документы Microsoft"
description: "Узнайте, как Azure PowerSHell toodetermine toouse hello издателя, предложение, SKU и версия для образов виртуальных Машин Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Как образы toofind виртуальной Машины Windows в Azure Marketplace с помощью Azure PowerShell hello

В этом разделе описывается, как образы Azure PowerShell toouse toofind виртуальной Машины в Azure Marketplace hello. Используйте этот сведения toospecify образа Marketplace при создании виртуальной Машины Windows.

Убедитесь, что установлен и настроен hello последней [модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Таблица часто используемых образов Windows
| PublisherName | ПРЕДЛОЖЕНИЕ | Sku |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-Server-Core |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-with-Containers |
| MicrosoftWindowsServer |WindowsServer |2016-Nano-Server |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008-R2-SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016-WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2-WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Поиск определенных образов


При создании новой виртуальной машины с помощью диспетчера ресурсов Azure, в некоторых случаях требуется toospecify изображения с сочетанием hello hello следующие свойства изображения:

* Издатель
* ПРЕДЛОЖЕНИЕ
* SKU

Например, использовать эти значения с hello [AzureRMVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage) командлета PowerShell или с помощью шаблона группы ресурсов, в котором необходимо указать тип hello toobe виртуальная машина создана.

Если вам требуется toodetermine эти значения, можно запустить hello [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), и [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) командлетов toonavigate hello изображения. Определите эти значения:

1. Список hello изображения издателей.
2. Получить список предложений нужного издателя.
3. Получить список номеров SKU для требуемого предложения.

Во-первых список издателей hello с hello, следующие команды:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Введите свое имя выбранного издателя и выполните hello, следующие команды:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Введите свое имя выбранного предложения и выполните следующие команды hello:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Из вывода hello hello `Get-AzureRMVMImageSku` команды, у вас есть все hello сведения toospecify hello изображения для новой виртуальной машины.

Hello ниже приведен полный пример:

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Выходные данные:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Для издателя «MicrosoftWindowsServer» hello:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Выходные данные:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Для предложения «WindowsServer» hello:

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Выходные данные:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

Из этого списка, скопируйте hello выбранный номер SKU, и у вас есть все сведения о hello для hello `Set-AzureRMVMSourceImage` командлета PowerShell или для шаблона группы ресурсов.

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы можете точно hello образа необходимо toouse. . в разделе виртуальной машины быстро с помощью информации об изображении hello, который только что найден toocreate [Создание виртуальной машины Windows с помощью PowerShell](quick-create-powershell.md).
