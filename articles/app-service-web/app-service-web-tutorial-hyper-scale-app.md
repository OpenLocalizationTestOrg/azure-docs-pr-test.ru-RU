---
title: "aaaBuild крупномасштабных приложений в Azure | Документы Microsoft"
description: "Узнайте, как toomaximize toouse различных служб Azure hello производительности приложения ASP.NET в Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Создание гипермасштабируемого веб-приложения в Azure

Этот учебник показывает, как tooscale ожидания веб-приложение ASP.NET в Azure toomaximize пользователь запросов.

Перед запуском этого учебника, убедитесь, что [hello Azure CLI устанавливается](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) на компьютере. Кроме того, [Visual Studio](https://www.visualstudio.com/vs/) в пример приложения hello toorun локального компьютера.

## <a name="step-1---get-sample-application"></a>Шаг 1. Получение примера приложения
На этом шаге настраивается hello локального проекта ASP.NET.

### <a name="clone-hello-application-repository"></a>Репозиторий приложения hello клонирования

Откройте hello командной строки терминалов по своему усмотрению и `CD` tooa рабочий каталог. Затем hello выполнения следующих команд tooclone hello образца приложения. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Запустить образец приложения hello в Visual Studio

Откройте решение hello в Visual Studio.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Тип `F5` toorun приложения hello.

Этот образец веб-приложения ASP.NET поступают из шаблона по умолчанию hello и сохраняет пользователя сеансов и использует hello кэша вывода. Просмотрите `HighScaleApp\Controllers\HomeController.cs`. Hello `Index()` метод добавляет часть данных toohello сеанса.

```csharp
Session.Add("visited", "true"); 
```

И hello `About()` и `Contact()` методы кэшировать свои выходные данные.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>Шаг 2 - развертывание tooAzure
На этом шаге создания веб-приложение Azure и развертывания вашего tooit приложения ASP.NET образца.

### <a name="create-a-resource-group"></a>Создание группы ресурсов   
Используйте [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) toocreate [группы ресурсов](../azure-resource-manager/resource-group-overview.md) в Западной Европе hello. Группа ресурсов представляет размещения всех hello вместе, требуется toomanage ресурсы Azure, такие как серверный веб-приложения hello и любой базы данных SQL.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee какие возможные значения следует использовать для `---location`, использовать hello [список расположений az appservice](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) команды.

### <a name="create-an-app-service-plan"></a>Создание плана службы приложений
Используйте [создать план служб приложений az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate «B1» [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

План службы приложений — это единица масштабирования, которая может включать любое количество приложений должны tooscale вверх или out вместе over hello же инфраструктуры службы приложений. Каждый план также имеет свою [ценовую категорию](https://azure.microsoft.com/en-us/pricing/details/app-service/). На более высоких уровнях используется лучшее оборудование и доступны дополнительные функции (например, дополнительные экземпляры масштабирования).

В этом учебнике B1 — hello минимального уровня, который позволяет масштабировать toothree экземпляров. Приложения всегда можно переместить вверх или вниз hello ценовой категории позже, запустив [обновление плана служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Создание веб-приложения
Используйте [создать az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate веб-приложения с уникальным именем в `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Сброс учетных данных развертывания
Используйте [web az appservice пользователь развертывание задан](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset учетные данные развертывания уровня учетной записи для приложения службы.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Настройка развертывания Git
Используйте [web системы управления версиями az appservice config локальной git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure локальное развертывание Git.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Эта команда предоставляет выход, который выглядит как следующий hello:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Используйте hello вернул tooconfigure URL-адрес вашего Git удаленной. Hello следующая команда использует hello предшествующий пример выходных данных.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Развертывание примера приложения hello
Вы являются toodeploy теперь готовы к примеру приложения. Запустите `git push`.

```powershell
git push azure master
```

При запросе пароля следует использовать hello пароль, указанный вами при запуске `az appservice web deployment user set`.

### <a name="browse-tooazure-web-app"></a>Обзор tooAzure веб-приложения
Используйте [обзора web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee своего приложения, работающего в режиме реального времени в Azure, выполните следующую команду.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>Шаг 3 — подключить tooRedis
На этом шаге настраивается кэша Redis для Azure как внешних, размещение кэша tooyour веб-приложение Azure. Быстро, можно воспользоваться Redis toocache выходные данные страницы. Кроме того, при дальнейшем масштабировании веб-приложения Redis поможет надежно сохранить пользовательские сеансы в нескольких экземплярах.

### <a name="create-an-azure-redis-cache"></a>Создание кэша Redis для Azure
Используйте [az redis создать](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate кэша Redis для Azure и сохраните hello выходных данных JSON. Укажите уникальное имя в `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Настройка приложения hello toouse Redis
Формат hello строку подключения для вашего кэша.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

Вторая строка Hello следует предоставить выход, выглядит следующим образом:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

В Visual Studio, создайте файл веб-конфигурации в корневом каталоге проекта, который называется `redis.config` и hello вставить следующий код в него. В `value`, используйте строку подключения hello из hello выходные данные PowerShell.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Если взглянуть на hello `.gitignore` файла в репозиторий Git, вы увидите, что этот файл исключен из системы управления версиями. Таким образом ваша конфиденциальная информация находится в безопасности. 

Откройте `Web.config`. Обратите внимание hello `<appSettings file="redis.config">` элемент, который получает приветствия, созданный в `redis.config`. 

Найти комментарий hello раздел, содержащий `<sessionState>` и `<caching>`. Раскомментируйте его.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Этот код осуществляет поиск строки подключения Redis hello вы определили в `RedisConnection`. 

Теперь приложение использует сеансы toomanage Redis и кэширование. Тип `F5` toorun приложения hello. При желании вы можете загрузить Redis управления toovisualize hello данные клиента, сохраняется toohello кэша.

### <a name="configure-hello-connection-string-in-azure"></a>Настройка строки подключения hello в Azure

Для toowork вашего приложения в Azure, необходимо tooconfigure hello же строка подключения Redis в Azure веб-приложения. Поскольку `redis.config` не сохраняется в системе управления версиями, не является развернутой tooAzure при выполнении развертывания Git.

Используйте [обновление az appservice web конфигурации appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) строка соединения hello tooadd с hello же имя (`RedisConnection`).

az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup

Следует помнить, что `$connstring` содержит строку подключения в формате hello.

### <a name="redeploy-hello-application-tooazure"></a>Повторное развертывание tooAzure приложения hello
Использовать ваш tooAzure изменения toopush команды Git

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

При запросе пароля следует использовать hello пароль, указанный вами при запуске `az appservice web deployment user set`.

### <a name="browse-toohello-azure-web-app"></a>Обзор toohello веб-приложение Azure
Используйте [обзора web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) live toosee hello изменения в Azure.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>Шаг 4 экземпляров toomultiple шкалы.
Hello план служб приложений является hello единица масштабирования для вашего веб-приложениях Azure. tooscale ожидания веб-приложения, масштабирование hello план служб приложений.

Используйте [обновление плана служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale экземпляров toothree план службы приложений hello, который является hello максимально допустимое hello B1 ценовой категории. Помните, что B1 hello ценовой категории, выбранные при создании hello ранее план служб приложений. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Шаг 5. Развертывание приложения в нескольких регионах
При масштабировании географически, приложение работает в нескольких регионах hello облако Azure. Эта программа установки балансировку нагрузки приложения дальнейшей основанной на географических объектах и сокращает время отклика hello, поместив ближе браузера tooclient приложения.

На этом шаге масштабировать ваш ASP.NET web app tooa второй области с [диспетчера трафика Azure](https://docs.microsoft.com/en-us/azure/traffic-manager/). В конце шага hello hello будет запущен в Западной Европе (уже создан) веб-приложения и веб-приложение работает в Юго-Восточная Азия (еще не создан). Оба приложения будут обслуживаться из hello же URL-адрес диспетчера трафика.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Вертикальное масштабирование hello Europe приложения tooStandard уровня
В службе приложений интеграция с диспетчером трафика Azure требует hello ценовой категории Standard. Используйте [обновление плана служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale копирование вашего tooS1 плана служб приложений. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Создание профиля диспетчера трафика 
Используйте [создать профиль диспетчера трафика сети az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate диспетчера трафика профиль и добавить его tooyour группы ресурсов. В параметре $dnsName укажите уникальное DNS-имя.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Указывает, что этот профиль [направляет трафик пользователя toohello ближайшей конечной точкой](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Получить идентификатор ресурса hello приложение hello Европа
Используйте [Показать web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello идентификатор ресурса веб-приложения.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Добавить конечную точку диспетчера трафика для Европы приложение hello
Используйте [создать конечную точку диспетчера трафика сети az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd tooyour конечной точки профиля диспетчера трафика и используйте идентификатор ресурса hello веб-приложения как hello целевой.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Получить URL-адрес конечной точки диспетчера трафика hello
Профиль диспетчера трафика теперь есть конечная точка, точки tooyour существующего веб-приложения. Используйте [Показать профиль диспетчера трафика сети az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget его URL-адрес. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Копировать выходные данные hello в адресную строку браузера. Вы должны снова увидеть свое веб-приложение.

### <a name="create-an-azure-redis-cache-in-asia"></a>Создание кэша Redis для Azure в Азии
Теперь можно реплицировать региона Azure web app toohello Юго-Восточная Азия. toostart, используйте [az redis создать](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate второй кэш Azure Redis в Юго-Восточная Азия. Этот кэш должен toobe совместного размещения вместе с приложением в Азии.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`Имя кэша hello hello кэша Западной Европе с hello hello дает `-asia` суффикс.

### <a name="create-an-app-service-plan-in-asia"></a>Создание плана службы приложений в Азии
Используйте [создать план служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate план вторую службу приложения hello юго-восток Азиатско-Тихоокеанский регион, с помощью hello S1 того же уровня как план Западной Европе hello.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Создание веб-приложения в Азии
Используйте [создать az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate второй веб-приложения.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`содержит имя приложения hello приложения hello Западной Европе, hello с hello `-asia` суффикс.

### <a name="configure-hello-connection-string-for-redis"></a>Настройка строки подключения hello для Redis
Используйте [обновление az appservice web конфигурации appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello веб-приложение hello строки подключения для hello кэша Юго-Восточная Азия.

az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>Настройка Git развертывания для приложения hello Азии.
Используйте [web системы управления версиями az appservice config локальной git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure локальное развертывание Git для hello второй веб-приложения.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Эта команда предоставляет выход, который выглядит как следующий hello:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Используйте hello вернул tooconfigure URL-адрес второй Git, удаленный для локального хранилища. Hello следующая команда использует hello предшествующий пример выходных данных.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Развертывание примера приложения
Запустите `git push` toodeploy второй дистанционного Git образец приложения toohello. 

```bash
git push azure-asia master
```

При запросе пароля следует использовать hello пароль, указанный вами при запуске `az appservice web deployment user set`.

### <a name="browse-toohello-asia-app"></a>Обзор приложения toohello Азии
Используйте [обзора web az appservice](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify, динамическая работы вашего приложения в Azure.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Получить идентификатор ресурса hello приложение hello Азии
Используйте [Показать web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello идентификатор ресурса веб-приложения в Юго-Восточная Азия.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Добавить конечную точку диспетчера трафика для приложения hello Азии
Используйте [создать конечную точку диспетчера трафика сети az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd второй toohello конечной точки профиля диспетчера трафика.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>Добавление приложений tooweb идентификатор региона
Используйте [обновление az appservice web конфигурации appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd переменной среды для конкретного региона.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Код приложения уже использует этот параметр приложения. Просмотрите `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Готово!

Попробуйте URL-адрес hello tooaccess вашего профиля диспетчера трафика с помощью браузеров в разных географических регионах. В клиентских браузерах в Европе должно отображаться ASP.NET West Europe (ASP.NET, Западная Европа), а в браузерах клиентов из Азии — ASP.NET Southeast Asia (ASP.NET, Юго-Восточная Азия).

## <a name="more-resources"></a>Дополнительные ресурсы
