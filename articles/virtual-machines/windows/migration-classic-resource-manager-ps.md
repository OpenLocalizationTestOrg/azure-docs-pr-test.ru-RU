---
title: "aaaMigrate tooResource диспетчера с помощью PowerShell | Документы Microsoft"
description: "Этой статье рассматриваются hello поддерживается платформой миграции ресурсов IaaS, например виртуальные машины (VM), виртуальных сетей (Vnet) и учетные записи хранения из классического tooAzure диспетчера ресурсов (ARM) с помощью команд Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Перенос ресурсов IaaS в классическом tooAzure диспетчера ресурсов с помощью Azure PowerShell
Следующие шаги показывают, как toouse Azure PowerShell команды toomigrate инфраструктуры как услуги (IaaS) ресурсы из hello классической модели toohello диспетчера ресурсов Azure развертывания модели развертывания.

Если требуется, можно переносить ресурсы с помощью hello [интерфейс командной строки Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).

* Основные сведения о поддерживаемых сценариев миграции см. в разделе [поддерживаемые платформой миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-overview.md).
* Подробные инструкции и пошаговое руководство по миграции см. в разделе [технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов](migration-classic-resource-manager-deep-dive.md).
* [Распространенные ошибки миграции](migration-classic-resource-manager-errors.md)

<br>
Ниже приведен порядок hello tooidentify блок-схемы, в котором действия требуется toobe выполнен во время процесса миграции

![Снимок экрана, показывающий шагов миграции hello](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>Шаг 1. Планирование миграции
Вот несколько рекомендаций, рекомендуется при оценке миграции IaaS ресурсов от классических tooResource диспетчера.

* Прочтите hello [поддерживаемые и неподдерживаемые функции и настройки](migration-classic-resource-manager-overview.md). При наличии виртуальных машин, использующих неподдерживаемые конфигурации или компоненты, рекомендуется отложить hello конфигурации или компонент поддержки toobe было объявлено. Кроме того если он соответствует вашим потребностям, удалить эти компоненты или можно вывести из миграции tooenable этой конфигурации.
* Если у вас есть автоматизированные скрипты, которые сегодня развертывание инфраструктуры и приложений, попробуйте toocreate аналогичную программу установки теста с помощью этих скриптов для миграции. Кроме того можно настроить образец сред с помощью портала Azure hello.

> [!IMPORTANT]
> Шлюзы приложений для миграции с классической tooResource Manager в настоящее время не поддерживаются. Перед запуском сети hello toomove операции подготовки toomigrate классической виртуальной сети с шлюза приложения, удалить шлюз hello. После завершения миграции hello переподключение hello шлюза в диспетчере ресурсов Azure.
>
>Шлюзов ExpressRoute подключение tooExpressRoute цепи в другую подписку невозможно перенести автоматически. В таких случаях удалить шлюз ExpressRoute hello, миграция виртуальной сети hello и повторного создания шлюза hello. См. в разделе [перенести ExpressRoute каналов и связанные виртуальные сети из модели развертывания диспетчера ресурсов hello классический toohello](../../expressroute/expressroute-migration-classic-resource-manager.md) для получения дополнительной информации.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>Шаг 2: Установите последнюю версию Azure PowerShell hello
Существует два основных варианта tooinstall Azure PowerShell: [коллекции PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) или [установщика веб-платформы (WebPI)](http://aka.ms/webpi-azps). Обновления для установщика веб-платформы выпускаются ежемесячно. Обновления для коллекции PowerShell выпускаются на постоянной основе. В этой статье используется Azure PowerShell 2.1.0.

Инструкции по установке см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>Шаг 3: Убедитесь, что вы являетесь администратором для hello подписки на портале Azure
tooperform завершения миграции вы должны добавляться как соадминистратора подписки hello в hello [портал Azure](https://portal.azure.com).

1. Вход в hello [портал Azure](https://portal.azure.com).
2. Выберите меню концентратора hello **подписки**. Если вы не видите этот пункт, щелкните **Больше служб**.
3. Найдите запись hello нужную подписку, а затем просмотрите hello **Мои РОЛИ** поля. Для совместного администратора hello значение должно быть _администратор учетной записи_.

Если вы не могли tooadd соадминистратора, обратитесь администратором служб или соадминистратора для hello подписки tooget самостоятельно добавить.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>Шаг 4. Настройка подписки и регистрация для миграции
Сначала запустите командную строку PowerShell. Для миграции, необходимо tooset настройку среды для обоих классический и диспетчер ресурсов.

Учетная запись tooyour для диспетчера ресурсов модели hello для входа.

```powershell
    Login-AzureRmAccount
```

Получить hello доступные подписки с помощью hello следующую команду:

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

Задайте подписки Azure для hello текущего сеанса. В этом примере задает hello имя подписки по умолчанию слишком**Моя подписка Azure**. Замените имя подписки пример hello свои собственные.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> Регистрация — однократное действие, но, прежде чем выполнять миграцию, вам нужно зарегистрироваться. Без регистрации, вы видите hello следующие сообщение об ошибке:
>
> *Неправильный запрос: Подписка не зарегистрирована для миграции.*
>
>

Зарегистрируйте поставщик ресурсов hello миграции с помощью hello следующую команду:

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Подождите пять минут для регистрации toofinish hello. Можно проверить состояние hello hello утверждения с помощью hello следующую команду:

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Убедитесь, что RegistrationState имеет значение `Registered` , прежде чем продолжить.

Теперь войдите в учетную запись tooyour для hello классической модели.

```powershell
    Add-AzureAccount
```

Получить hello доступные подписки с помощью hello следующую команду:

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

Задайте подписки Azure для hello текущего сеанса. В этом примере задает подписку по умолчанию hello слишком**Моя подписка Azure**. Замените имя подписки пример hello свои собственные.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Шаг 5: Убедитесь, что недостаточно ядер виртуальная машина Azure Resource Manager hello Azure область текущего развертывания или виртуальной сети
Можно использовать следующие PowerShell команды toocheck hello текущее количество ядер, имеющегося в диспетчере ресурсов Azure hello. toolearn Дополнительные сведения об основных квоты, в разделе [ограничения и hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).

В этом примере проверяется доступность hello в hello **Запад США** области. Замените имя области пример hello свои собственные.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>Шаг 6: Проведение команды toomigrate ресурсов IaaS
> [!NOTE]
> Все операции hello, описанные здесь являются идемпотентными. Если имеются неполадки, отличные от неподдерживаемое свойство или ошибка конфигурации, рекомендуется повторить попытку hello подготовки, отмены или фиксации операции. Платформа Hello пытается hello действие еще раз.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>Шаг. 6.1. Вариант 1. Миграция виртуальных машин в облачную службу (не в виртуальную сеть)
Получение списка hello облачные службы, используя следующую команду hello и подбору hello облачной службы, которые должны toomigrate. Если hello виртуальных машин в облачной службе hello находятся в виртуальной сети или если они имеют рабочих и веб-роли, hello команда возвращает сообщение об ошибке.

```powershell
    Get-AzureService | ft Servicename
```

Получите имя hello развертывания для облачной службы hello. В этом примере — имя службы hello **Мои службы**. Замените имя службы имя службы пример hello.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

Подготовка виртуальных машин hello в облачную службу hello для миграции. У вас есть два toochoose параметры из.

* **Вариант 1. Перенос hello виртуальные машины tooa платформы созданную виртуальную сеть**

    Во-первых проверки, при переносе hello облачной службы, с помощью hello, следующие команды:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    Hello предыдущая команда отображает все предупреждения и ошибки, блокирующие миграции. Если проверка прошла успешно, то можно переместить на toohello **Подготовка** шаг:

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **Вариант 2. Перенос tooan существующую виртуальную сеть в модели развертывания диспетчера ресурсов hello**

    В этом примере задает hello имя группы ресурсов слишком**myResourceGroup**, hello имя виртуальной сети слишком**myVirtualNetwork** и hello имя подсети слишком**mySubNet**. Замените имена hello в примере hello hello имена собственные ресурсы.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    Во-первых проверки, при переносе hello виртуальной сети с помощью hello следующую команду:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    Hello предыдущая команда отображает все предупреждения и ошибки, блокирующие миграции. Если проверка прошла успешно, то вы можете перейти с hello после шага подготовки:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

После успешного завершения операции подготовки hello с любой из предыдущих параметров hello опросить состояние миграции hello hello виртуальных машин. Убедитесь, что они находятся в hello `Prepared` состояния.

В этом примере задает hello имя виртуальной Машины слишком**myVM**. Замените имя образца hello собственное имя виртуальной Машины.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

Проверьте конфигурацию hello для подготовки ресурсов с помощью PowerShell или портал Azure hello hello. Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте hello следующую команду:

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду:

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>Шаг 6.1. Вариант 2. Миграция виртуальных машин в виртуальной сети

toomigrate виртуальные машины в виртуальной сети, переносе hello виртуальной сети. с помощью виртуальной сети hello автоматически перенести Hello виртуальных машин. Подбор hello виртуальной сети, которые должны toomigrate.
> [!NOTE]
> [Миграция одной виртуальной машины для классического](migrate-single-classic-to-resource-manager.md) путем создания новой виртуальной машины диспетчера ресурсов с дисками, управляемых с помощью hello (операционной системы и данных) файлы VHD hello виртуальной машины.
<br>

> [!NOTE]
> имя виртуальной сети Hello может отличаться от приведенного в hello нового портала. Hello новый портал Azure отображает hello с названием `[vnet-name]` hello фактическое виртуального сетевого имени, то типа `Group [resource-group-name] [vnet-name]`. Перед миграцией подстановки hello фактическое виртуального сетевого имени с помощью команды hello `Get-AzureVnetSite | Select -Property Name` или просматривать его в hello старый портал Azure. 

В этом примере задает hello имя виртуальной сети слишком**myVnet**. Замените имя виртуальной сети пример hello свои собственные.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> Если hello виртуальной сети содержит веб- или рабочих ролей или виртуальных машин с неподдерживаемых конфигураций, вы получите сообщение об ошибке проверки.
>
>

Во-первых проверки, при переносе hello виртуальной сети с помощью hello следующую команду:

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

Hello предыдущая команда отображает все предупреждения и ошибки, блокирующие миграции. Если проверка прошла успешно, то вы можете перейти с hello после шага подготовки:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Проверьте конфигурацию hello для подготовки виртуальных машин с помощью Azure PowerShell или портал Azure hello hello. Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте hello следующую команду:

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду:

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>Шаг 6.2. Перенос учетной записи хранения
После завершения переноса виртуальных машин hello, мы рекомендуем перенести учетные записи хранения hello.

Прежде чем переносить hello учетной записи хранилища, выполните перед проверки предварительных требований:

* **Перенос классических виртуальных машин, чьи диски хранятся в учетной записи хранения hello**

    Предшествующий команда возвращает RoleName и DiskName свойства всех дисков виртуальной Машины классический hello в учетной записи хранения hello. RoleName — имя hello toowhich виртуальной машины hello подключенный диск. Если предшествующие команда возвращает дисков убедитесь перед миграцией переносятся, toowhich виртуальных машин, эти диски подключены hello учетной записи хранилища.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Удаление неприкрепленные классический дисков виртуальной Машины хранятся в учетной записи хранилища hello**

    Находите неприкрепленные классический дисков ВМ в хранилище hello учетной записи с помощью следующую команду:

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    Если приведенная выше команда вернула диски, удалите их, выполнив следующую команду.

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **Удаление образов виртуальных Машин, хранятся в учетной записи хранилища hello**

    Предшествующий команда возвращает все образы виртуальных Машин hello с диском ОС, хранятся в учетной записи хранилища hello.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     Предшествующий команда возвращает все образы виртуальных Машин hello с дисками данных, хранящихся в учетной записи хранилища hello.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    Удалите все образы виртуальных Машин hello, возвращаемый выше команд с помощью предыдущей команды.
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

Проверьте каждую учетную запись хранилища для миграции с помощью hello следующую команду. В этом примере — имя учетной записи хранения hello **myStorageAccount**. Замените имя пример hello hello имя учетной записи.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

Следующим шагом является tooPrepare hello учетной записи хранилища для миграции

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Проверьте конфигурацию hello для подготовки учетной записи хранилища с помощью Azure PowerShell или портал Azure hello hello. Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте hello следующую команду:

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду:

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>Дальнейшие действия
* [Общие сведения о миграции поддерживаются платформы IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Планирование миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Использовать ресурсы IaaS toomigrate CLI из классической tooAzure диспетчера ресурсов](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Средства сообщества соблюдения миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Распространенные ошибки миграции](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Просмотрите hello наиболее часто задаваемые вопросы о миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
