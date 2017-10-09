---
title: "aaaVisualizing кластер с помощью Service Fabric Explorer | Документы Microsoft"
description: "Обозреватель Service Fabric — это веб-средство для изучения облачных приложений и узлов в кластере Microsoft Azure Service Fabric и управления ими."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Визуализация кластера с помощью обозревателя Service Fabric
Обозреватель Service Fabric — это веб-средство для изучения приложений и узлов в кластере Azure Service Fabric и управления ими. Обозреватель Service Fabric размещается непосредственно в кластере hello, поэтому она доступна всегда, независимо от того, где запущен кластера.

## <a name="video-tutorial"></a>Видеоруководство

как просматривать toouse Service Fabric Explorer toolearn hello следующие видео Microsoft Virtual Academy:

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>Подключение tooService Fabric Explorer
Если вы следовали инструкциям hello слишком[подготовить среду разработки](service-fabric-get-started.md), Service Fabric Explorer можно запустить на локальном кластере, перейдя по toohttp://localhost:19080 / обозреватель.

## <a name="understand-hello-service-fabric-explorer-layout"></a>Анализа структуры Service Fabric Explorer hello
Можно перемещаться по Service Fabric Explorer с помощью дерева hello слева hello. Hello корневого элемента дерева hello панели мониторинга кластера hello Обзор кластера, в том числе сводную приложения и состояние работоспособности узла.

![Панель мониторинга кластера обозревателя Service Fabric][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Просмотр макета hello кластера
Узлы в кластере Service Fabric размещаются в двухмерной сетке доменов сбоя и обновления, Этой размещение гарантирует, что приложения остаются доступными в hello наличие сбоев оборудования и обновления приложения. Можно просмотреть спланированную hello текущего кластера с помощью схемы hello кластера.

![Схема кластера в обозревателе Service Fabric][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Просмотр приложений и услуг
кластер Hello содержит две ветви: один для приложений, а другой — для узлов.

Можно использовать toonavigate представление приложения hello через Service Fabric логической иерархии: приложений, служб, разделов и реплик.

В следующем примере hello, hello приложения **MyApp** состоит из двух служб, **MyStatefulService** и **WebService**. Так как **MyStatefulService** — служба с отслеживанием состояния, она включает раздел с одной основной и двумя вторичными репликами. Напротив, WebSvcService — служба без сохранения состояния и содержит единственный экземпляр.

![Представление приложений обозревателя Service Fabric][sfx-application-tree]

На каждом уровне дерева hello hello основной области отображаются нужные сведения об элементе hello. Например вы увидите состояние работоспособности hello и версия для конкретной службы.

![Панель основных сведений обозревателя Service Fabric][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Просмотреть узлы кластера hello
представление узла Hello отображает hello физическую структуру hello кластера. Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле и какие реплики запущены в настоящее время.

## <a name="actions"></a>Действия
Обозреватель Service Fabric предлагает tooinvoke быстро действий на узлах, приложений и служб в кластере.

Например, toodelete экземпляр приложения выберите приложение hello из дерева hello hello левой части экрана и выберите **действия** > **удалить приложение**.

![Удаление приложения в обозревателе Service Fabric][sfx-delete-application]

> [!TIP]
> Можно выполнять hello же действия, щелкнув следующий элемент tooeach hello кнопку с многоточием.
>
>

Hello следующей таблице перечислены действия hello, доступные для каждой сущности:

| **Сущность** | **Действие** | **Описание** |
| --- | --- | --- |
| Тип приложения |Отмена подготовки типа |Удаляет пакет приложения hello из хранилища образов hello кластера. Требуется все приложения, тип toobe, сначала удалить. |
| Приложение |Удалить приложение |Удаление приложения hello, включая все его службы и их состояния (если таковые имеются). |
| служба |Удаление службы |Удаление службы hello и его состояние (если таковые имеются). |
| Узел |Активировать |Активация узла hello. |
| Узел | Деактивация (пауза) | Приостановить работу узла hello в ее текущем состоянии. Служб продолжается toorun, но Service Fabric не перемещает заранее ничего на или отключить его если он не требуется tooprevent сбоя или несогласованности данных. Это действие не типовыми tooenable отладка служб на tooensure конкретный узел, что они не перемещаются во время проверки. | |
| Узел | Деактивация (перезапуск) | Безопасное перемещение всех служб в памяти за пределы узла и закрытие постоянных служб. Обычно используется при перезапуске хост-процессах hello или toobe необходимость машины. | |
| Узел | Деактивация (удаление данных) | Закройте все службы, запущенные на узле hello после построения недостаточно свободных реплик. Обычно используется, когда узел (или хотя бы его хранилище) окончательно выводится из эксплуатации. | |
| Узел | Удаление состояния узла | Удалите знаний реплики узла из кластера hello. Обычно используется, когда узел, вышедший из строя, уже нельзя восстановить. | |
| Узел | Перезагрузить | Моделирование сбоя узла, перезапустив hello узла. Дополнительные сведения см. [здесь](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps). | |

Поскольку многие действия разрушительных, могут быть ответы tooconfirm намерениям до завершения действия hello.

> [!TIP]
> Каждого действия, которое может быть выполнено с помощью Service Fabric Explorer также может выполняться с помощью PowerShell или API REST, tooenable автоматизации.
>
>

Также можно использовать экземпляры приложения Service Fabric Explorer toocreate для данного приложения типа и версии. Выберите тип приложения hello в представлении дерева hello, а затем щелкните hello **создать экземпляр приложения** Далее toohello версии связи хотелось бы hello правой панели.

![Создание экземпляра приложения в Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> В настоящее время экземпляры приложения, созданные с помощью Service Fabric Explorer, не могут быть параметризованы. При их создании используются значения параметров по умолчанию.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Подключение tooa удаленного кластера Service Fabric
Если вы знаете hello кластерную конечную точку и иметь достаточные разрешения Service Fabric Explorer доступен из любого браузера. Это так, как обозреватель Service Fabric — еще одно служба, которая работает в кластере hello.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>Обнаружить конечную точку Service Fabric Explorer hello для удаленного кластера
tooreach обозреватель Service Fabric для данного кластера, точка веб-браузера:

http://&lt;конечная_точка_кластера&gt;:19080/Explorer.

Для Azure кластеров hello полный URL-адрес доступен также в панели essentials кластера hello hello портал Azure.

### <a name="connect-tooa-secure-cluster"></a>Подключите кластер безопасного tooa
Можно управлять кластера Service Fabric доступа tooyour клиента с помощью сертификатов или с помощью Azure Active Directory (AAD).

При попытке tooService tooconnect Fabric Explorer в кластере безопасный, затем в зависимости от конфигурации кластера hello последующего быть toopresent требуется сертификат клиента либо выполнить вход с помощью AAD.

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор Testability](service-fabric-testability-overview.md)
* [Управление приложениями Service Fabric в Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Развертывание приложений Service Fabric с помощью PowerShell](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
