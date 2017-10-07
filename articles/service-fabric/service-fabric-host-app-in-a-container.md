---
title: "приложения .NET в контейнер tooAzure Service Fabric aaaDeploy | Документы Microsoft"
description: "Объясняется, как toopackage приложения .NET в Visual Studio в контейнер Docker. Затем развертывается новое приложение «контейнер» tooa кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Развертывание приложения .NET в tooAzure контейнера Windows Service Fabric

В этом учебнике показано как toodeploy существующего приложения ASP.NET в контейнере Windows Azure.

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание проекта Docker в Visual Studio
> * Помещение имеющегося приложения в контейнер
> * Настройка непрерывной интеграции с Visual Studio и VSTS

## <a name="prerequisites"></a>Предварительные требования

1. Установите [Docker CE для Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description), чтобы иметь возможность запускать контейнеры в Windows 10.
2. Ознакомьтесь с hello [начало работы с контейнерами Windows 10][link-container-quickstart].
3. Загрузите hello [Fabrikam Fiber CallCenter] [ link-fabrikam-github] образец приложения.
4. Установите [Azure PowerShell][link-azure-powershell-install].
5. Установка hello [непрерывной поставки средств расширения для Visual Studio 2017 г.][link-visualstudio-cd-extension]
6. Создайте [подписку Azure][link-azure-subscription] и [учетную запись Visual Studio Team Services][link-vsts-account]. 
7. [Создайте кластер в Azure](service-fabric-tutorial-create-cluster-azure-ps.md).

## <a name="containerize-hello-application"></a>Упаковываете приложение hello

Теперь, когда [кластер Service Fabric работает в Azure](service-fabric-tutorial-create-cluster-azure-ps.md) вы готовы toocreate и развертывание контейнерного приложения. toostart запустить приложение в контейнере, нам нужно tooadd **Docker поддержки** toohello проекта в Visual Studio. При добавлении **Docker поддержки** toohello приложения, выполняются две операции. Во-первых, _Dockerfile_ добавляется toohello проекта. Этот новый файл описывает, как образ контейнера hello toobe построения. Затем второй, новый _составления docker_ toohello решение будет добавлен проект. Hello новый проект содержит несколько файлов составления docker. Составить docker файлы могут быть используется toodescribe способ запуска контейнера hello.

См. дополнительные сведения о работе с [инструментами для контейнера Visual Studio][link-visualstudio-container-tools].

>[!NOTE]
>Если это hello при первом запуске образы контейнеров Windows на компьютере, Docker CE должно открыть hello базовые образы для вашего контейнеров. Hello изображений, используемых в этом учебнике, 14 ГБ. Продолжим и выполните следующие базовые образы команда терминала toopull hello hello:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Добавление поддержки Docker

Откройте hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] файл в Visual Studio.

Щелкните правой кнопкой мыши hello **FabrikamFiber.Web** проекта > **добавить** > **Docker поддержки**.

### <a name="add-support-for-sql"></a>Добавление поддержки SQL

Поэтому приложения hello toorun требуется SQL server в данном приложении используется SQL в качестве поставщика данных hello. Сошлитесь на образ контейнера SQL Server в файле docker-compose.override.ym.

В Visual Studio откройте **обозревателе решений**, найти **составления docker**и Привет открыть файл **docker compose.override.yml**.

Перейдите toohello `services:` узла, добавить узел с именем `db:` , определяющий hello входа SQL Server для контейнера hello.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>Вы можете использовать любой SQL Server для локальной отладки, который доступен с вашего узла. Тем не менее **localdb** не поддерживает взаимодействие типа `container -> host`.

>[!WARNING]
>Выполнение SQL Server в контейнере не поддерживает сохранение данных. При остановке hello контейнера, данные будут удалены. Не используйте эту конфигурацию для рабочей среды.

Перейдите toohello `fabrikamfiber.web:` узел и добавить дочерний узел с именем `depends_on:`. Это гарантирует, что hello `db` (SQL Server hello контейнер) будет запущена до наш веб-приложения (fabrikamfiber.web).

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Обновить hello веб-конфигурации

Вернитесь на hello **FabrikamFiber.Web** проекта обновления строки подключения hello в hello **web.config** файл toopoint toohello SQL Server в контейнере hello.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Toouse другой SQL Server при создании выпуска построения веб-приложения, добавьте другой файл web.release.config tooyour строку соединения.

### <a name="test-your-container"></a>Тестирование контейнера

Нажмите клавишу **F5** toorun и отладки приложения hello в контейнере.

Край открывается страница запуска определенного приложения с помощью IP-адрес контейнера hello hello hello внутренней сети NAT (обычно 172.x.x.x). toolearn Дополнительные сведения об отладке приложений в контейнерах, с помощью Visual Studio 2017 г. в разделе [в этой статье][link-debug-container].

![пример fabrikam в контейнере][image-web-preview]

Hello контейнера больше не готов toobe построен и создания пакетов приложения Service Fabric. Получив hello образ контейнера, построенный на компьютере, можно принудительно отправить его tooany контейнер реестра и подтягивают toorun tooany узла.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Подготовка приложения hello для облака hello

приложение hello tooget готова к работе в Service Fabric в Azure, мы должны toocomplete два шага.

1. Предоставить порт hello, где нам это нужно будет tooreach toobe наш веб-приложения в кластере Service Fabric hello.
2. Указать готовую к работе базу данных SQL для приложения.

### <a name="expose-hello-port-for-hello-app"></a>Предоставить hello порт для приложения hello
мы настроили кластер Service Fabric Hello имеет порт *80* открыт по умолчанию в hello подсистемы балансировки нагрузки Azure, распределяет кластера toohello входящего трафика. Мы можем предоставить наш контейнер по этому порту с помощью файла docker-compose.yml.

В Visual Studio откройте **обозревателе решений**, найти **составления docker**и Привет открыть файл **docker compose.override.yml**.

Изменение hello `fabrikamfiber.web:` узел, добавьте дочерний узел с именем `ports:`.

Добавьте запись строки `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Использование рабочей базы данных SQL
При выполнении в рабочей среде данные требуется сохранять в базе данных. В контейнере в настоящее время нет данных постоянно tooguarantee способом, поэтому не удается сохранить рабочих данных в SQL Server в контейнере.

Рекомендуется использовать базу данных SQL Azure. tooset вверх и выполнения управляемого SQL Server в Azure, посетите hello [примеры использования базы данных SQL Azure] [ link-azure-sql] статьи.

>[!NOTE]
>Запомнить toochange hello соединения строки toohello SQL server в hello **web.release.config** файла в hello **FabrikamFiber.Web** проекта.
>
>Это приложение корректно завершает работу, если база данных SQL недоступна. Можно выбрать toogo вперед и развертывание приложения hello без сервера SQL.

## <a name="deploy-with-visual-studio-team-services"></a>Развертывание с помощью Visual Studio Team Services

tooset развертывания с помощью Visual Studio Team Services требуется tooinstall hello [непрерывной поставки средств расширения для Visual Studio 2017 г][link-visualstudio-cd-extension]. Это расширение позволяет легко toodeploy tooAzure путем настройки Visual Studio Team Services и получить кластера Service Fabric tooyour приложение, развернутое.

tooget работы, код должен быть размещен в системе управления версиями. Hello оставшейся части этого раздела предполагается **git** уже используется.

### <a name="set-up-a-vsts-repo"></a>Настройка репозитория VSTS
В нижнем правом углу hello Visual Studio, нажмите кнопку **добавить tooSource управления** > **Git** (или какой бы параметр ни вы предпочитаете).

![Нажмите кнопку элемента управления источника hello][image-source-control]

В hello _Team Explorer_ панели, нажмите клавишу **публикации репозитория Git**.

Выберите имя репозитория VSTS и нажмите кнопку **Опубликовать репозиторий**.

![Публикация tooVSTS репозитория][image-publish-repo]

Теперь, когда ваш код синхронизируется с исходным репозиторием VSTS, можно настроить непрерывную интеграцию и непрерывную поставку.

### <a name="setup-continuous-delivery"></a>Настройка непрерывной доставки

В _обозревателе решений_, щелкните правой кнопкой мыши hello **решения** > **Настройка непрерывной поставки**.

Здравствуйте, выберите подписку Azure.

Задать **тип узла** слишком**кластера Service Fabric**.

Задать **целевой узел** кластера service fabric toohello, созданный в предыдущем разделе hello.

Выберите **контейнер реестра** toopublish для контейнера.

>[!TIP]
>Используйте hello **изменить** toocreate кнопка реестра контейнера.

Нажмите кнопку **ОК**.

![настройка непрерывной интеграции Service Fabric][image-setup-ci]
   
   После завершения настройки hello контейнера — развернутой tooService структуры. Каждый раз, когда push репозитория toohello обновления выполняется нового построения и выпуска.
   
   >[!NOTE]
   >Создание образов контейнеров hello занять около 15 минут.
   >Hello первого развертывания кластера Service Fabric для toohello вызывает hello базовый Windows Server Core контейнера изображений toobe загружены. Hello занимает toocomplete дополнительных 5 – 10 минут.

Обзор toohello Fabrikam Call Center приложения с помощью hello URL-адрес кластера: например, *http://mycluster.westeurope.cloudapp.azure.com*

Теперь, когда контейнерных и развертывания решений Fabrikam Call Center hello можно открыть hello [портал Azure] [ link-azure-portal] и просмотреть приложения hello в Service Fabric. приложение hello tootry, откройте веб-браузер и перейдите toohello URL-адрес кластера Service Fabric.

## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание проекта Docker в Visual Studio
> * Помещение имеющегося приложения в контейнер
> * Настройка непрерывной интеграции с Visual Studio и VSTS

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
