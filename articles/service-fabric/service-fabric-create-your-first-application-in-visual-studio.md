---
title: "aaaCreate надежной службы Azure Service Fabric с помощью C#"
description: "Создание, развертывание и отладка приложения надежной службы, созданного в Service Fabric с помощью Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>Создание первого приложения надежных служб Service Fabric с отслеживанием состояния на C#

Узнайте, как toodeploy первого приложения Service Fabric для .NET в Windows через несколько минут. По завершении у вас будет локальный кластер, выполняющийся с приложением надежной службы.

## <a name="prerequisites"></a>Предварительные требования

Перед началом работы [настройте среду разработки](service-fabric-get-started.md). Сюда входит установка hello Service Fabric SDK и Visual Studio 2017 г. или 2015.

## <a name="create-hello-application"></a>Создание приложения hello

Запустите Visual Studio от имени **администратора**.

Создайте проект, нажав клавиши `CTRL`+`SHIFT`+`N`.

В hello **новый проект** диалоговое окно, выберите **облака > приложение Service Fabric**.

Имя приложения hello **MyApplication** и нажмите клавишу **ОК**.

   
![Диалоговое окно "Новый проект" в Visual Studio][1]

В следующем диалоговом окне приветствия, можно создать любой тип приложения Service Fabric. В рамках этого краткого руководства выберите **Служба с отслеживанием состояния**.

Имя службы hello **MyStatefulService** и нажмите клавишу **ОК**.

![Диалоговое окно "Новая служба" в Visual Studio][2]


Visual Studio создает проект приложения hello и проект службы с отслеживанием состояния hello и отображает их в обозревателе решений.

![Обозреватель решений после создания приложения и службы с отслеживанием состояния][3]

проект приложения Hello (**MyApplication**) содержит код напрямую. Он только ссылается на набор проектов служб. Также он содержит данные еще трех типов.

* **Профили публикации**  
Развертывание сред toodifferent профилей.

* **Сценарии**  
Сценарий PowerShell для развертывания и обновления приложения.

* **Определение приложения**  
Включает файл ApplicationManifest.xml hello под *ApplicationPackageRoot* описывающей композиции вашего приложения. Файлы параметров связанного приложения находятся в *ApplicationParameters*, который может быть toospecify используемые параметры, относящиеся к среде. Профиль публикации Visual Studio выбирает, связанный файл параметров приложения, который указан в hello во время развертывания tooa конкретной среды.
    
Общие сведения о hello содержимое проекта службы hello. в разделе [Приступая к работе с надежного обмена](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Развернуть и отладить приложение hello

Теперь, когда вы создали приложение, запустите его.

В Visual Studio нажмите клавишу `F5` toodeploy hello приложения для отладки.

>[!NOTE]
>Hello в первый раз запустить и развернуть hello приложения локально, Visual Studio создает локального кластера для отладки. Это может занять некоторое время. Состояние создания кластера Hello отображается в окне вывода Visual Studio hello.

При hello кластера будет готово, вы получите уведомление из hello локального кластера приложения области уведомлений диспетчера входящий в состав пакета SDK для hello.
   
![Уведомление в области уведомлений локального кластера][4]

После запуска приложения hello, Visual Studio автоматически выбирает hello **средство просмотра событий диагностики**, где можно просмотреть выходные данные трассировки из служб.
   
![Средство просмотра диагностических событий][5]

Hello шаблона службы с отслеживанием состояния, мы использовали просто показывает, увеличение значения счетчика в hello `RunAsync` метод **MyStatefulService.cs**.

Разверните одну из события toosee hello сведения, включая узел hello, где выполняется код hello. В данном случае это \_Узел 2\_, хотя на вашем компьютере это может быть другой узел.
   
![Подробная информация в средстве просмотра диагностических событий][6]

локальный кластер Hello содержит пять узлов, размещенных на одном компьютере. В рабочей среде каждый узел размещается на различных физических или виртуальных машинах. отладчик потери hello toosimulate машины во время выполнения hello Visual Studio в hello же время, давайте вниз по одному из узлов hello hello локальном кластере.

В hello **обозревателе решений** откройте **MyStatefulService.cs**. 

Найти hello `RunAsync` метод и задайте точки останова на первой строке метода hello hello.

![Точка останова в методе RunAsync службы с отслеживанием состояния][7]

Запустите hello **Service Fabric Explorer** инструмент, щелкнув hello **локального кластера диспетчера** приложения области уведомлений и выберите **управление локального кластера**.

![Запустите обозреватель Service Fabric из локального кластера диспетчера hello][systray-launch-sfx]

[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) обеспечивает визуальное представление кластера. Содержит набор приложений, развернутых tooit hello и физические узлы, входящие в состав набора hello.

В левой области hello, разверните **кластера > узлы** и найти hello узел, где выполняется ваш код.

Нажмите кнопку **действия > деактивировать (перезапустите)** toosimulate перезапуска компьютера.

![Остановка узла в обозревателе Service Fabric][sfx-stop-node]

Сразу же увидите точка останова попадать в Visual Studio, как вы делали на одном узле, легко вычисление hello при сбое tooanother.


Затем возвращают toohello диагностические средства просмотра событий и просмотрите сообщения приветствия. Счетчик Hello возобновлена увеличения, несмотря на то, что фактически поступления событий hello с другого узла.

![Информация в средстве просмотра диагностических событий после аварийного переключения][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>Очистка hello локального кластера (необязательно)

Помните, что этот локальный кластер работает по-настоящему. Остановка отладчика hello удаляет экземпляр приложения и Отмена регистрации типа приложения hello. Однако hello кластер продолжает toorun в фоновом режиме hello. Когда вы будете готовы toostop hello локального кластера, существует несколько параметров.

### <a name="keep-application-and-trace-data"></a>Хранение приложения и трассировка данных

Завершите работу кластера, hello, щелкнув hello **локального кластера диспетчера** приложения области уведомлений и выберите **остановить локальный кластер**.

### <a name="delete-hello-cluster-and-all-data"></a>Удаление кластера hello и все данные

Удаление кластера hello, щелкнув hello **локального кластера диспетчера** приложения области уведомлений и выберите **удалить локальный кластер**. 

Если этот параметр выбран, Visual Studio будет повторное развертывание кластера hello hello очередном запуске hello приложения. Выберите этот параметр, если не планируется, локального кластера hello toouse некоторое время или при необходимости tooreclaim ресурсов.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о [надежных службах](service-fabric-reliable-services-introduction.md)
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
