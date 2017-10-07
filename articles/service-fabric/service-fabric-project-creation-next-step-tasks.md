---
title: "следующие шаги создания проекта aaaService структуры | Документы Microsoft"
description: "В этой статье содержатся ссылки набор основных задач разработки tooa для Service Fabric"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>Ваше приложение Service Fabric и дальнейшие действия
Ваше приложение Azure Service Fabric создано. В этой статье описывающего hello план проекта и некоторые возможные дальнейшие действия.

## <a name="your-application"></a>Ваше приложение
Каждое новое приложение включает проект приложения. Возможно, один или два дополнительных проекта, в зависимости от типа hello выбранной службы.

### <a name="hello-application-project"></a>проект приложения Hello
проект приложения Hello состоит из:

* Набор служб toohello ссылки, входящих в состав приложения.
* Три публикация профилей (узел 1 локальной, 5-узловая локальной и облачной), которые можно использовать toomaintain настройках для работы с различных сред — как конечную точку кластера tooa связанные настройки и ли tooperform обновить развертывания по умолчанию.
* Три параметра файлов приложения (то же, как описано выше), которые можно использовать конфигурации приложения для конкретной среды toomaintain, например количество hello toocreate секций для службы.
* Скрипт развертывания, можно использовать toodeploy приложения из командной строки hello, или как часть автоматических непрерывной интеграции и развертывания конвейера.
* манифест приложения Hello, описывающий приложения hello. Hello манифеста можно найти в папке ApplicationPackageRoot hello.

### <a name="stateless-service"></a>Служба без отслеживания состояния
При добавлении новой службы без сохранения состояния, Visual Studio добавляет проект решении tooyour службы, включающее тип потомками `StatelessService`. Служба Hello увеличивает значение локальной переменной в счетчике.

### <a name="stateful-service"></a>Служба с отслеживанием состояния
При добавлении новой службы с отслеживанием состояния, Visual Studio добавляет проект решении tooyour службы, включающее тип потомками `StatefulService`. Hello службы увеличивает значение счетчика в его `RunAsync` метод и сохраняет результат hello в `ReliableDictionary`.

### <a name="actor-service"></a>Служба субъекта
При добавлении нового надежного субъекта, Visual Studio добавляет два решения проектов tooyour: проект субъекта и проекте интерфейса.

проект субъекта Hello предоставляет методы задания и начало hello значение счетчика, надежно сохраняются в пределах состояния субъекта hello. Hello проекта интерфейса предоставляет интерфейс других служб можно использовать tooinvoke hello субъекта.

### <a name="stateless-web-api"></a>Веб-API без отслеживания состояния
проект без сохранения состояния веб-API Hello предоставляет простую веб-службы, которые можно использовать tooopen приложений tooexternal-клиентов. Дополнительные сведения о структуру проекта hello. в разделе [веб-API службы фабрики служб с резидентным OWIN](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>ASP.NET core
Hello Service Fabric SDK предоставляет hello же установить ASP.NET Core шаблонов, доступных для проектов ASP.NET Core автономного: пустое, [веб-API][aspnet-webapi], и [веб-приложение][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Гостевые исполняемые файлы и контейнеры

Service Fabric «guest» — это служба, который не встроен в моделях программирования платформы hello. Вы можете упаковать hello двоичные файлы для гостевой либо [непосредственно в пакет приложения hello](service-fabric-deploy-existing-app.md) или [через образ контейнера](service-fabric-deploy-container.md). В обоих случаях Visual Studio создает hello необходимые артефакты в hello **ApplicationPackageRoot** папку проекта приложения hello. Visual Studio не создаст новый проект служб, так как код hello уже существует в другом месте. Если вы хотите toomanage гостевые проекты наряду с проект приложения hello Service Fabric, их можно добавить toohello одного решения Visual Studio.

## <a name="next-steps"></a>Дальнейшие действия
### <a name="create-an-azure-cluster"></a>Создание кластера Azure
Hello Service Fabric SDK предоставляет локального кластера для разработки и тестирования. toocreate кластер в Azure, в разделе [установка кластера Service Fabric с портала Azure hello][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Публикация вашего приложения tooAzure
Можно опубликовать приложение непосредственно из Visual Studio tooan Azure кластера. toolearn, изучите раздел [публикация вашего приложения tooAzure][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Использовать обозреватель Service Fabric toovisualize кластера
Обозреватель Service Fabric предлагает простой способ toovisualize кластера, включая развернутых приложений и физическую структуру. toolearn более, в разделе [визуализация кластера с помощью Service Fabric Explorer][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Версии и обновление служб
Service Fabric обеспечивает независимое управление версиями и обновление независимых служб в приложении. toolearn более, в разделе [управления версиями и обновление служб][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Настройка непрерывной интеграции с Visual Studio Team Services
toolearn процесс непрерывной интеграции можно настроить для приложения Service Fabric разделе [настроить непрерывную интеграцию с Visual Studio Team Services][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
