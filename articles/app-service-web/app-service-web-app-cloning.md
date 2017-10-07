---
title: "aaaWeb приложения клонирование, с помощью PowerShell"
description: "Узнайте, как tooclone веб-приложения toonew веб-приложений с помощью PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>Клонирование приложений службы приложений Azure с помощью PowerShell
С выпуском Microsoft Azure PowerShell hello версии 1.1.0 был добавлен новый параметр добавлен tooNew AzureRMWebApp, который предоставит hello пользователя hello возможность tooclone существующего приложения tooa только что созданный веб-приложения в другой регион или hello одного региона. Это позволит клиентам toodeploy количество приложений в разных регионах быстро и легко.

В настоящее время клонирование приложений поддерживается только в планах службы приложений уровня Premium. новый компонент использует Hello hello же ограничения, как средство резервного копирования приложений Web, в разделе [резервное копирование веб-приложения в службе приложений Azure](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn об использовании диспетчера ресурсов Azure на основе toomanage командлеты Azure PowerShell возврат веб-приложений [диспетчера ресурсов Azure на основе команд PowerShell для веб-приложения Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>Клонирование существующего приложения
Сценарий: Существующий веб-приложение в регионе США, hello пользователь предпочитает tooclone hello содержимое tooa новое веб-приложение в Центре области. Это можно сделать с помощью версии диспетчера ресурсов Azure hello toocreate командлет PowerShell hello новое веб-приложение с параметром - SourceWebApp hello.

Зная ресурсов hello имя группы, которое содержит hello исходного веб-приложения, можно использовать следующую информацию PowerShell команды tooget hello источника веб-приложения (в данном случае с именем источника webapp) hello:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

toocreate новый план служб приложений, можно использовать команду New-AzureRmAppServicePlan как следующий пример hello

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

С помощью команды New-AzureRmWebApp hello, мы можно создать новое веб-приложение hello в регионе hello North Central US и привязать tooan план служб приложений существующего уровня premium, кроме того, мы используем hello того же ресурса группу, что hello исходного веб-приложения, или определить новую группу ресурсов , hello ниже показано, что:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

tooclone существующего веб-приложения, включая все слоты развертывания связанных, hello пользователю будет необходимо toouse Здравствуйте параметр IncludeSourceWebAppSlots, hello следующую команду PowerShell показано использование этого параметра с помощью команды New-AzureRmWebApp hello hello:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

tooclone существующего веб-приложения, в пределах hello же регионе hello пользователю будет необходимо toocreate план новую группу ресурсов и новую службу приложения hello же регионе, а затем с помощью hello следующие PowerShell команды tooclone hello веб-приложения

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Клонирование существующих приложений tooan среды службы приложений
Сценарий: Существующий веб-приложение в регионе США, hello пользователь предпочитает tooclone hello содержимое tooa новый web app tooan существующие среды службы приложений (ASE).

Зная ресурсов hello имя группы, которое содержит hello исходного веб-приложения, можно использовать следующую информацию PowerShell команды tooget hello источника веб-приложения (в данном случае с именем источника webapp) hello:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

Необходимо знать имя hello ASE и имя группы ресурсов hello, к которой принадлежит hello ASE, hello пользователя можно использовать команду New AzureRmWebApp hello что toocreate hello новое веб-приложение в существующий ASE hello, следуя hello демонстрирует, что:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

Параметр расположения Hello требуется из-за причин toolegacy, однако в случае hello при создании приложения в ASE оно будет игнорироваться. 

## <a name="cloning-an-existing-app-slot"></a>Клонирование существующего слота приложения
Сценарий: hello пользователь предпочитает tooclone существующих приложений гнездо Web tooeither новое веб-приложение или новая область веб-приложения. новое веб-приложение может быть в hello Hello же регионе, как исходный слот веб-приложения hello, или в другом регионе.

Зная ресурсов hello имя группы, которое содержит hello исходного веб-приложения, можно использовать следующую команду PowerShell tooget hello источника web app слота сведения (в данном случае с именем источника webappslot) привязан tooWeb приложения источника-веб-приложение hello:

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

Hello следующий код демонстрирует создание клона hello исходного web app tooa нового веб-приложения:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>Настройка диспетчера трафика при клонировании приложения
Создание нескольких регионах веб-приложений и настройки диспетчера трафика Azure tooroute трафика tooall этих веб-приложений, tooinsure n важные сценарии, заказчиков приложений высокой надежности при клонировании существующего веб-приложения, которым у вас есть hello tooconnect параметр обоих веб tooeither приложений нового профиля диспетчера трафика или уже существующей - Обратите внимание, что только версия диспетчера ресурсов Azure поддерживается диспетчера трафика.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>Создание нового профиля диспетчера трафика при клонировании приложения
Сценарий: hello пользователь предпочитает tooclone область tooanother web app, при настройке профиля диспетчера трафика Azure Resource Manager, среди оба веб-приложения. Hello следующий код демонстрирует создание клона hello источника web app tooa новое веб-приложение при настройке профиля диспетчера трафика:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>Добавление нового клонированного веб-приложения tooan существующего профиля диспетчера трафика
Сценарий: hello пользователя уже есть профиль диспетчера трафика Azure Resource Manager, он хотел tooadd веб-приложения в качестве конечных точек. toodo таким образом, необходимо сначала tooassemble Здравствуйте, существующий код профиля диспетчера трафика, нам нужно будет hello идентификатор подписки, имя группы ресурсов и hello трафика manager имени существующего профиля.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

После того, идентификатор диспетчера трафика hello, hello следующий код демонстрирует создание клона hello исходного web app tooa нового веб-приложения во время добавления их tooan существующего профиля диспетчера трафика:

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>Существующие ограничения
Эта функция в настоящее время находится в предварительной версии, со временем мы работаем tooadd новые возможности, hello после списка являются hello известные ограничения в текущей версии hello клонирования приложения:

* Параметры автоматического масштабирования не клонируются
* Параметры расписания резервного копирования не клонируются
* Параметры виртуальных сетей не клонируются
* Подробные сведения о приложении не настраиваются автоматически на веб-приложения hello назначения
* Параметры простой авторизации не клонируются
* Расширение Kudu не клонируется
* Правила TiP не клонируются
* Содержимое базы данных не клонируется.

### <a name="references"></a>Ссылки
* [Команды Azure PowerShell на основе Azure Resource Manager для веб-приложений Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Клонирование веб-приложения с помощью портала Azure](app-service-web-app-cloning-portal.md)
* [Резервное копирование веб-приложений в службе приложений Azure](web-sites-backup.md)
* [Предварительная поддержка диспетчера трафика Azure в диспетчере ресурсов Azure](../traffic-manager/traffic-manager-powershell-arm.md)
* [Введение tooApp среды службы](app-service-app-service-environment-intro.md)
* [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md)

