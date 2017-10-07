---
title: "набор масштабирования виртуальной машины Azure aaaUpgrade | Документы Microsoft"
description: "Обновление масштабируемого набора виртуальных машин Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Обновление набора масштабирования виртуальных машин
В этой статье описывается, как развертывание операционной системы обновления tooan Azure набор масштабирования виртуальных машин без простоев. В этом контексте обновление операционной системы включает в себя изменение версии hello или номера SKU hello ОС или hello URI пользовательского изображения. Обновление без простоя означает обновление виртуальных машин по одной или группами (например, по одному домену сбоя), а не всех сразу. В этом случае виртуальные машины, которые не обновляются, могут продолжать работу.

tooavoid неоднозначности, давайте отличить четыре типа обновления ОС, может потребоваться tooperform:

* Изменение версии hello или номера SKU образа платформы. Например, изменение Ubuntu версии 14.04.2-LTS из 14.04.201506100 too14.04.201507060 или изменение too16.04.0-LTS/latest SKU 15.10 или последний Ubuntu hello. Этот сценарий описан в данной статье.
* Изменение hello URI, указывающий tooa новую версию пользовательского образа сборки (**свойства** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **изображения** > **uri**). Этот сценарий описан в данной статье.
* Изменяется ссылка на изображение hello набора масштабирования, созданную с помощью управляемых дисков Azure.
* Установка исправлений hello ОС из виртуальной машине (в качестве примера описывается установка исправления безопасности и запуска центра обновления Windows). Этот сценарий поддерживается, но не описан в данной статье.

В этой статье не рассматриваются наборы масштабирования виртуальных машин, которые развернуты как часть кластера [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) . Дополнительные сведения об исправлении Service Fabric см. в разделе [Исправление ОС Windows в кластере Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application).

Hello основные версии ОС или SKU образа платформы hello последовательности для изменения или hello URI пользовательского изображения выглядит следующим образом:

1. Получение модели набор масштабирования виртуальной машины hello.
2. Изменить версию hello, SKU, ссылка на изображение или значение URI в модели hello.
3. Обновление модели hello.
4. Сделать *manualUpgrade* вызова на виртуальных машинах hello в наборе масштабирования hello. Этот шаг применяется только если *upgradePolicy* задано слишком**ручной** в шкалу. Если задано слишком**автоматического**, все виртуальные машины hello будут обновлены одновременно, тем самым вызывая время простоя.

С этой информацией в виду давайте посмотрим, как удалось обновить версию hello наборе в PowerShell, а также с помощью API-интерфейса REST hello масштабирования. Эти примеры охватывают hello регистр образ платформы, но в этой статье предоставляет достаточно сведений, чтобы вы tooadapt tooa пользовательского образа этот процесс.

## <a name="powershell"></a>PowerShell
В этом примере обновляется набора масштабирования виртуальных машин Windows (Создание toohello новая версия 4.0.20160229. После обновления модели hello, это происходит во время обновления один экземпляр виртуальной машины.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

При обновлении hello URI для пользовательского изображения вместо изменения указана версия образа платформы, замените hello «набор hello новую версию» строки с помощью команды, которое будет обновлять hello URI источника изображения. Например если без использования управляемых дисков Azure был создан набор масштабирования hello, hello обновления будет выглядеть так:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Если пользовательский образ на основе набора масштабирования был создан с помощью управляемых дисков Azure hello ссылка на изображение будет обновляться. Например:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Hello REST API
Ниже приведено несколько примеров Python, использующих tooroll Azure REST API hello ожидания обновления версии ОС. Оба используют облегченного hello [azurerm](https://pypi.python.org/pypi/azurerm) библиотеку toodo функции оболочки Azure REST API GET на шкале hello установить модель, следуют PUT с обновленной модели. Они также рассмотрим представления экземпляров виртуальных машин tooidentify hello виртуальных машин, домен обновления.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) сценарий Python, который использовал tooroll out ОС обновления tooa масштабирования виртуальных машин под управлением набор в одном домене обновления за раз.

![Сценарий Vmssupgrade для выбора виртуальных машин или домена обновления](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Этот сценарий позволяет выбрать tooupdate виртуальными машинами или указать домен обновления. Он поддерживает изменение указана версия образа платформы или hello URI пользовательского изображения.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) — это универсальный редактор наборов масштабирования виртуальных машин, отображающий состояние виртуальных машин в виде тепловой карты, в которой каждая строка представляет один домен обновления. Помимо прочего можно обновить модель hello для набора масштабирования с новой версией, SKU или пользовательского образа URI, а затем выбрать tooupgrade домены сбоя. После этого, все виртуальные машины hello в этом домене обновления, обновленного toohello новой модели. Кроме того можно выполнить последовательное обновление на основе размера пакета hello по своему усмотрению.  

Hello следующем снимке экрана показана модель наборе для Ubuntu 14.04-2LTS версии 14.04.201507060 масштабирования. Многие другие параметры были добавлены средства toothis со времени на этом снимке экрана.

![Модель Vmsseditor для домена обновления с ОС Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

После нажатия кнопки **обновление** и затем **получение сведений о**, tooupdate запуск виртуальных машин в UD 0.

![Отображение процесса обновления в Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

