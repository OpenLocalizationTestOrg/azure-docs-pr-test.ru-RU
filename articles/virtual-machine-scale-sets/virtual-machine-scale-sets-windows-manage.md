---
title: "виртуальные машины в наборе масштабирования виртуальных машин aaaManage | Документы Microsoft"
description: "Узнайте, как управлять виртуальными машинами в наборе масштабирования виртуальных машин с помощью Azure PowerShell."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Управление виртуальными машинами в масштабируемом наборе виртуальных машин
Использование задач hello в этой статье toomanage виртуальных машин в ваш набор масштабирования виртуальной машины.

Большинство задач hello, которые включают управление виртуальной машины в наборе масштабирования требуют знания hello идентификатор экземпляра, которые должны toomanage машины hello. Можно использовать [обозревателя ресурсов Azure](https://resources.azure.com) toofind hello идентификатор экземпляра виртуальной машины в наборе масштабирования. Вы также использовать обозреватель ресурсов tooverify hello состояние завершения задач hello.

В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в учетную запись tooyour.

## <a name="display-information-about-a-scale-set"></a>Отображение информации о масштабируемом наборе
Можно получить общие сведения о наборе масштабирования, который также является tooas, который ссылается представление экземпляра hello. Также можно получить более подробные сведения, такие как сведения о ресурсах hello в наборе масштабирования hello.

Замените значения с именем hello или группа ресурсов и масштабирования, установите и запустите команду hello hello:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Результат буде выглядеть примерно так:

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

Замените значения с именем hello набора ресурсов группы и масштаб hello. Замените  *#*  с идентификатором hello экземпляр виртуальной машины hello интересующий tooget и запустите его:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Результат будет выглядеть примерно так:

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Запуск виртуальной машины в наборе масштабирования
Замените значения с именем hello набора ресурсов группы и масштаб hello. Замените  *#*  с идентификатором hello hello виртуальной машины требуется toostart и запустите его:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

В обозревателе ресурсов, мы видим, что находится в состоянии hello hello экземпляра **под управлением**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

Можно запустить все виртуальные машины hello в наборе с помощью параметра - InstanceId hello не масштабирования hello.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Остановка виртуальной машины в наборе масштабирования
Замените значения с именем hello набора ресурсов группы и масштаб hello. Замените  *#*  с идентификатором hello hello виртуальной машины требуется toostop и запустите его:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

В обозревателе ресурсов, мы видим, что находится в состоянии hello hello экземпляра **освобождена**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

toostop виртуальной машины и не освободить его, используйте параметр - StayProvisioned hello. Вы можете остановить все виртуальные машины hello в устанавливается с помощью параметра - InstanceId hello не hello.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Перезапуск виртуальной машины в наборе масштабирования
Замените значения с именем hello набора ресурсов группы и hello шкалы hello. Замените  *#*  с идентификатором hello hello виртуальной машины требуется toorestart и запустите его:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Можно перезапустить все виртуальные машины hello в устанавливается с помощью параметра - InstanceId hello не hello.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Удаление виртуальной машины из набора масштабирования
Замените значения с именем hello набора ресурсов группы и hello шкалы hello. Замените  *#*  с идентификатором hello hello виртуальной машины требуется tooremove и запустите его:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

Hello масштабный набор виртуальных машин за один раз можно удалить, не с помощью параметра - InstanceId hello.

## <a name="change-hello-capacity-of-a-scale-set"></a>Изменить hello емкость набора масштабирования
Можно добавить или убрать, изменив hello емкость hello набор виртуальных машин. Получите необходимый toochange набор hello емкость toowhat нужно toobe, а затем обновить набор масштабирования hello с новой емкости hello набор масштабирования hello. В этих команд замените значения с именем hello набора ресурсов группы и hello шкалы hello.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

При удалении из hello масштабный набор виртуальных машин сначала удаляются hello виртуальных машин с высоким идентификаторы hello.

