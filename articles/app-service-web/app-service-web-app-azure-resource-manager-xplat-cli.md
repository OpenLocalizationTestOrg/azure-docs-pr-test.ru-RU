---
title: "aaaAzure диспетчер ресурсов на основе кросс платформенных средства командной строки для веб-приложения Azure | Документы Microsoft"
description: "Узнайте, как toouse hello новый toomanage диспетчера ресурсов Azure кросс платформенных командной строки средства на основе веб-приложения Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Использование кроссплатформенного интерфейса командной строки на основе Azure Resource Manager для службы приложений Azure
> [!div class="op_single_selector"]
> * [Интерфейс командной строки Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

В выпуске версии средств командной строки Microsoft Azure кросс платформенных 0.10.5 hello были добавлены новые команды. Эти команды дают toomanage под управлением диспетчера ресурсов Azure PowerShell команды hello возможность hello пользователя toouse службы приложений.

toolearn об управлении группами ресурсов, в разделе [toomanage Azure CLI hello Azure использовать ресурсы и группы ресурсов](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Кроме того, попробуйте [Azure CLI 2.0](https://github.com/Azure/azure-cli), CLI следующего поколения, языке Python для модели развертывания hello ресурса управления.
>
>

## <a name="managing-app-service-plans"></a>Управление планами службы приложений
### <a name="create-an-app-service-plan"></a>Создание плана службы приложений
toocreate план служб приложений использовать hello **создания azure appserviceplan** команды.

Ниже описаны различные параметры hello:

* **--группы ресурсов**: группа ресурсов, содержащая hello только что созданный план обслуживания приложений.
* **— имя**: имя плана обслуживания приложений hello.
* **--location**: расположение плана службы.
* **--sku**: hello требуемого ценообразования sku (параметры hello: F1 (Free). Варианты: F1 (бесплатный); D1 (общедоступный); B1 (малый базовый), B2 (средний базовый) и B3 (крупный базовый); S1 (малый стандартный), S2 (средний стандартный) и S3 (крупный стандартный); P1 (малый премиум), P2 (средний премиум) и P3 (крупный премиум).
* **--экземпляров**: hello число рабочих процессов в hello плана (значение по умолчанию — 1).

Пример toouse этого командлета:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Создание плана службы приложений Linux

С помощью hello же **создания azure appserviceplan** команду с hello дополнительный параметр **true--islinux**. Обратите внимание на ограничения hello и областей, описанные в [tooApp введение службы в Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Получение списка существующих планов службы приложений
использовать toolist hello существующих планах службы приложений, **список azure appserviceplan** команды.

toolist всех планах службы приложений в определенной группе ресурсов, используйте:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

использовать tooget план обслуживания определенного приложения **Показать azure appserviceplan** команды:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Настройка существующего плана службы приложений
Параметры hello toochange существующего плана служб приложений, используйте hello **конфигурации azure appserviceplan** команды. Вы можете изменить hello sku и hello число рабочих процессов 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Масштабирование плана службы приложений
использовать существующий план служб приложений, tooscale:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>Изменение hello SKU план служб приложений
toochange sku hello существующий план служб приложений, используйте:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Удаление существующего плана службы приложений
toodelete существующего плана служб приложений все назначенные приложений необходимость toobe перемещен или удален сначала. Затем с помощью hello **удалить azure веб-приложение** команды, вы можете удалить план служб приложений hello.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Управление приложениями службы приложений
### <a name="create-a-web-app"></a>Создание веб-приложения
toocreate веб-приложения, используйте hello **azure веб-приложения создайте** команды.

Ниже описаны различные параметры hello:

* **— имя**: имя для веб-приложения hello.
* **--плана**: имя для плана обслуживания hello используется toohost hello веб-приложения.
* **--группы ресурсов**: группы ресурсов, на котором размещена hello план обслуживания приложений.
* **--расположение**: hello местоположению веб-приложения.

Пример toouse этого командлета:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Удаление существующего приложения
toodelete существующего приложения, можно использовать hello **удалить azure веб-приложение** команды. Требуется имя hello toospecify приложение hello и имя группы ресурсов hello.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Список существующих приложений
использовать существующие приложения hello toolist hello **список azure веб-приложение** команды.

все приложения в определенной группе ресурсов, toolist использовать:

    azure webapp list --resource-group ContosoAzureResourceGroup

использовать tooget определенное приложение hello **Показать azure веб-приложение** команды.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Настройка существующего приложения
Параметры toochange hello и конфигурации для существующего приложения, используйте hello **набор параметров конфигурации azure веб-приложение** команды.

Пример (1): изменение hello php версии приложения 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Пример 2. Добавление или изменение параметров приложения:

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

другие конфигурации, которые можно изменять, tooknow hello используйте **набора конфигурации azure webapp -h** команды.

### <a name="change-hello-state-of-an-existing-app"></a>Изменить состояние hello существующего приложения
#### <a name="restart-an-app"></a>Перезапуск приложения
toorestart приложения необходимо указать hello имя и группе ресурсов приложения hello.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Остановка приложения
toostop приложения необходимо указать hello имя и группе ресурсов приложения hello.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Запуск приложения
toostart приложения необходимо указать hello имя и группе ресурсов приложения hello.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Управление профилями публикации приложения
Каждое приложение имеет профиль публикации, который можно использовать toopublish кода.

#### <a name="get-publishing-profile"></a>Получение профиля публикации
tooget hello профиль приложения, используйте для публикации:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Эта команда отображает hello публикации профиль имени пользователя и пароля toohello командной строки.

### <a name="manage-app-hostnames"></a>Управление именами узлов приложения
использовать toomanage привязки имени узла для вашего приложения hello **имена узлов azure webapp config** команды  

#### <a name="list-hostname-bindings"></a>Список привязок имен узлов
tooget hello текущие имя узла привязки для приложения, используйте:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Добавление привязок имен узлов
приложение tooan привязки имени узла tooadd, использование

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Удаление привязок имен узлов
toodelete привязки имени узла, используйте:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Дальнейшие действия
* toolearn о поддержке диспетчера ресурсов Azure CLI. в разделе [toomanage Azure CLI hello Azure используйте ресурсы и группы ресурсов.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* toolearn об управлении службы приложений с помощью PowerShell, в разделе [tooManage Using Azure Resource Manager-Based PowerShell веб-приложения Azure.](app-service-web-app-azure-resource-manager-powershell.md)
* в разделе toolearn о службе приложений Azure в Linux, [tooApp введение службы в Linux](app-service-linux-intro.md)
