---
title: "Диспетчер ресурсов на основе PowerShell aaaAzure команды для веб-приложения Azure | Документы Microsoft"
description: "Узнайте, как toouse hello новый toomanage команды PowerShell на основе диспетчера ресурсов Azure, веб-приложения Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>С помощью веб-приложениях Azure Azure Resource Manager-Based PowerShell tooManage
> [!div class="op_single_selector"]
> * [Интерфейс командной строки Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

С помощью Microsoft Azure PowerShell версии 1.0.0 новые команды будут добавлены, предоставляющее toomanage под управлением диспетчера ресурсов Azure PowerShell команды hello возможность hello пользователя toouse веб-приложений.

toolearn об управлении группами ресурсов, в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](../powershell-azure-resource-manager.md). 

toolearn о hello полный список параметров и параметров для hello командлеты PowerShell в разделе hello [полный Справочник по командлетам командлетов PowerShell на основе диспетчера ресурсов Azure Web App](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Управление планами службы приложений
### <a name="create-an-app-service-plan"></a>Создание плана службы приложений
план служб приложений toocreate использовать hello **New AzureRmAppServicePlan** командлета.

Ниже описаны различные параметры hello:

* **Имя**: имя плана обслуживания приложений hello.
* **Location**: расположение плана службы.
* **ResourceGroupName**: группа ресурсов, содержащая hello только что созданный план обслуживания приложений.
* **Уровень**: hello требуемого ценовой категории (по умолчанию — Free, есть параметры, Shared, Basic, Standard и Premium).
* **WorkerSize**: hello размер работников (по умолчанию — небольшой, если указан параметр hello уровня Basic, Standard или Premium. По умолчанию Small, если для параметра Tier указано значение Basic, Standard или Premium; также допустимы варианты Medium и Large.
* **NumberofWorkers**: hello число рабочих процессов в hello плана (значение по умолчанию — 1). 

Пример toouse этого командлета:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Создание плана службы приложений в среде служб приложений
toocreate план служб приложений в среде службы приложений, используйте hello же команда **New AzureRmAppServicePlan** команду с именем hello toospecify лишние параметры ASE и имя группы ресурсов в ASE.

Пример toouse этого командлета:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

Дополнительные сведения о среде службы приложений, проверка toolearn [tooApp введение среды службы](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Получение списка существующих планов службы приложений
использовать toolist hello существующих планах службы приложений, **Get AzureRmAppServicePlan** командлета.

toolist используйте всех планах службы приложений в вашей подписке. 

    Get-AzureRmAppServicePlan

toolist всех планах службы приложений в определенной группе ресурсов, используйте:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

Используйте tooget план обслуживания определенного приложения.

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Настройка существующего плана службы приложений
Параметры hello toochange существующего плана служб приложений, используйте hello **AzureRmAppServicePlan набор** командлета. Можно изменить уровень hello, размер рабочего потока и hello число рабочих процессов 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Масштабирование плана службы приложений
использовать существующий план служб приложений, tooscale:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Изменение размера рабочей hello план служб приложений
размер hello toochange рабочих процессов в существующий план служб приложений, используйте:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>Изменение hello уровня план служб приложений
toochange уровень hello существующий план служб приложений, используйте:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Удаление существующего плана службы приложений
toodelete существующего плана служб приложений все назначенные toobe необходимость приложения web перемещен или удален сначала. Затем с помощью hello **AzureRmAppServicePlan удаление** командлета можно удалить план служб приложений hello.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Управление веб-приложениями службы приложений
### <a name="create-a-web-app"></a>Создание веб-приложения
toocreate веб-приложения, используйте hello **New AzureRmWebApp** командлета.

Ниже описаны различные параметры hello:

* **Имя**: имя для веб-приложения hello.
* **AppServicePlan**: имя для плана обслуживания hello используется toohost hello веб-приложения.
* **ResourceGroupName**: группы ресурсов, на котором размещена hello план обслуживания приложений.
* **Расположение**: hello местоположению веб-приложения.

Пример toouse этого командлета:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Создание веб-приложения в среде службы приложений
toocreate веб-приложения в среде службы приложений (ASE). Используйте hello же **New AzureRmWebApp** команду с именем hello ASE toospecify лишние параметры и имя группы ресурсов hello, к которой принадлежит hello ASE.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

Дополнительные сведения о среде службы приложений, проверка toolearn [tooApp введение среды службы](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Удаление существующего веб-приложения
toodelete существующего веб-приложения, можно использовать hello **AzureRmWebApp удаление** командлета, требуется имя веб-приложения hello toospecify hello и имя группы ресурсов hello.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Список существующих веб-приложений
toolist hello существующего веб-приложения, используют hello **Get AzureRmWebApp** командлета.

Используйте для всех веб-приложений в вашей подписке toolist:

    Get-AzureRmWebApp

Используйте для всех веб-приложений в определенной группе ресурсов, toolist:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget определенного веб-приложения, используйте:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Настройка существующего веб-приложения
Параметры toochange hello и конфигурации для существующего веб-приложения используйте hello **AzureRmWebApp набор** командлета. Полный список параметров, проверьте hello [перехода по ссылке командлета](https://msdn.microsoft.com/library/mt652487.aspx)

Пример (1): используйте этот командлет строки подключения с toochange

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Пример 2. Добавление или изменение параметров приложения:

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


Пример (3): toorun набор hello веб приложения в 64-разрядном режиме

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Изменить состояние hello существующего веб-приложения
#### <a name="restart-a-web-app"></a>Перезапуск веб-приложения
toorestart веб-приложения, необходимо указать hello имя и группе ресурсов hello веб-приложения.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Остановка веб-приложения
toostop веб-приложения, необходимо указать hello имя и группе ресурсов hello веб-приложения.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Запуск веб-приложения
toostart веб-приложения, необходимо указать hello имя и группе ресурсов hello веб-приложения.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Управление профилями публикации веб-приложений
Каждый веб-приложения имеется профиль публикации, который можно использовать toopublish приложений, несколько операций могут выполняться в профилях публикации.

#### <a name="get-publishing-profile"></a>Получение профиля публикации
tooget hello профиль для веб-приложения, используйте публикации:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Эта команда отображает hello публикации профиль toohello командной строки также выходных данных hello публикации профиль tooa текстовый файл.

#### <a name="reset-publishing-profile"></a>Сброс профиля публикации
tooreset, оба hello пароль публикации для FTP и веб-развертывания для веб-приложения, используйте:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Управление сертификатами веб-приложения
toolearn о как toomanage веб-приложения сертификаты, в разделе [привязки SSL-сертификаты с помощью PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Дальнейшие действия
* toolearn о поддержке PowerShell диспетчера ресурсов Azure в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure.](../powershell-azure-resource-manager.md)
* toolearn о средах службы приложений, в разделе [tooApp введение среды службы.](app-service-app-service-environment-intro.md)
* в разделе toolearn об управлении сертификатами SSL службы приложения с помощью PowerShell, [привязки SSL-сертификаты с помощью PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* toolearn о hello полный список командлетов PowerShell на основе диспетчера ресурсов Azure для веб-приложения Azure в разделе [Справочник по командлетам Azure командлетов PowerShell диспетчера ресурсов Azure приложения Web.](https://msdn.microsoft.com/library/mt619237.aspx)
* * в разделе toolearn об управлении службы приложений, используя интерфейс командной строки, [XPlat-CLI Using Azure Resource Manager-Based для веб-приложения Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)

