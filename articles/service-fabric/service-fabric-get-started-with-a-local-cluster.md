---
title: "aaaDeploy и обновления Azure микрослужбами локально | Документы Microsoft"
description: "Узнайте, как tooset локального кластера Service Fabric, развернуть существующий tooit приложения, а затем обновите приложение."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Начало развертывания и обновления приложений в локальном кластере
Hello Azure Service Fabric SDK включает полной локальной среде разработки, можно использовать tooquickly Приступая к работе с развертывания и управления приложениями на локальном кластере. В этой статье создания локального кластера, развернуть существующий tooit приложения, а затем обновите данной приложения tooa новой версии, все из Windows PowerShell.

> [!NOTE]
> В этой статье предполагается, что вы уже [настроили среду разработки](service-fabric-get-started.md).
> 
> 

## <a name="create-a-local-cluster"></a>Создание локального кластера
Кластер Service Fabric представляет собой набор аппаратных ресурсов, на которых можно развернуть приложение. Как правило кластер состоит из в любом из пяти toomany тысяч машин. Однако hello Service Fabric SDK включает конфигурации кластера, который может выполняться на одном компьютере.

Очень важно, что toounderstand, hello локального кластера Service Fabric не эмуляторе или симуляторе. Он запускает hello того же кода платформы, который находится на кластеры с несколькими компьютерами. Hello единственное отличие заключается в том, что он выполняется hello платформы процессы, которые обычно распределены по пяти машин на одном компьютере.

Hello SDK предоставляет два способа tooset локального кластера: Windows PowerShell скрипт и hello локального кластера диспетчера системы значок приложения. В этом учебнике мы используем скрипт PowerShell hello.

> [!NOTE]
> Если вы уже создали локальный кластер путем развертывания приложения из Visual Studio, можете пропустить этот раздел.
> 
> 

1. Откройте новое окно PowerShell от имени администратора.
2. Запустите сценарий установки кластера hello из папки hello SDK:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    Настройка кластера занимает несколько минут. После завершения установки вы увидите примерно такой результат:
   
    ![Результат установки кластера][cluster-setup-success]
   
    Теперь вы находитесь готов tootry развертывание кластера tooyour приложения.

## <a name="deploy-an-application"></a>Развертывание приложения
Hello Service Fabric SDK включает широкий набор платформ и средства для создания приложений разработки. Если вы заинтересованы в обучении toocreate приложений в Visual Studio. в статье [создание первого приложения Service Fabric в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).

В этом учебнике, что можно сосредоточиться на аспекты управления hello hello платформы, использование существующего приложения образец для (называемые WordCount): развертывания, наблюдения и обновления.

1. Откройте новое окно PowerShell от имени администратора.
2. Импортируйте модуль Service Fabric SDK PowerShell hello.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Создание приложения hello toostore каталога, загрузить и развернуть, например C:\ServiceFabric.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Загрузка приложения WordCount hello](http://aka.ms/servicefabric-wordcountapp) расположение toohello был создан.  Примечание: hello браузера Microsoft Edge сохраняет файл hello с *.zip* расширения.  Измените расширение файла hello слишком*.sfpkg*.
5. Подключение локального кластера toohello:
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Создайте новое приложение с помощью команды развертывания hello SDK с имя и путь пакета приложения toohello.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Если все пойдет хорошо, вы увидите hello следующие выходные данные:
   
    ![Развернуть локальный кластер toohello приложения][deploy-app-to-local-cluster]
7. приложение hello toosee в действии, запустить браузер hello и перехода слишком[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html). Вы должны увидеть следующее:
   
    ![Пользовательский интерфейс развернутого приложения][deployed-app-ui]
   
    Hello приложения WordCount проста. Он включает клиентские JavaScript кода toogenerate случайных пяти символов «слов», который затем передаются приложению toohello через веб-API ASP.NET. Службы с отслеживанием состояния отслеживает количество hello подсчетом слов. Они разбиваются зависимости hello первый символ слова hello. Можно найти hello исходного кода для приложения WordCount hello в hello [классический Приступая к работе образцы](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    приложение Hello, которое мы развернуто содержит четыре секции. Поэтому слова, начинающиеся с буквы A – G хранятся в первом разделе hello, слова, начинающиеся с H до N, хранятся в второй раздел hello и т. д.

## <a name="view-application-details-and-status"></a>Просмотр сведений о приложении и его состояния
Теперь, когда мы развернуто приложение hello, давайте взглянем на некоторые сведения о приложении hello в PowerShell.

1. Запрос всех развернутых приложений в кластере hello:
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    Предположим, что только вы развернули приложение hello WordCount, появится примерно:
   
    ![Запрос всех развернутых приложений в PowerShell][ps-getsfapp]
2. Go toohello следующий уровень, запрашивая hello набор служб, которые включены в приложения WordCount hello.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Список служб для приложения hello в PowerShell][ps-getsfsvc]
   
    приложение Hello состоит из двух служб, hello фронтальный веб-сервер и службы с отслеживанием состояния hello, управляющего слова hello.
3. Наконец проверьте список секций hello WordCountService:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Просмотр разделов службы hello в PowerShell][ps-getsfpartitions]
   
    Здравствуйте, набор команд, которые вы использовали, как и все команды PowerShell структуры службы, доступные для кластера, вы можете подключиться к локальным или удаленным.
   
    Для более наглядный способ toointeract с кластером hello, средство hello веб-обозреватель Service Fabric, перейдя по слишком[http://localhost:19080/обозреватель](http://localhost:19080/Explorer) в браузере hello.
   
    ![Просмотр сведений о приложении в обозревателе Service Fabric][sfx-service-overview]
   
   > [!NOTE]
   > toolearn Дополнительные сведения о Service Fabric Explorer. в разделе [визуализация кластера с Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Обновление приложения
Service Fabric обеспечивает обновления нет простоев, мониторинг работоспособности hello приложения hello, как происходит откат кластеру hello. Выполните обновление приложения WordCount hello.

Новая версия приложения hello, теперь Hello подсчитывает только слова, начинающиеся с гласные. Как обновление hello разворачивает, мы видим два изменения в поведении приложения hello. Во-первых скорость hello увеличения размера hello count должно медленно, так как подсчитываются меньшее количество слов. Во-вторых поскольку hello первая секция содержит два гласные ("A" и "E"), а все остальные разделы содержат только один каждого, число ее со временем запустить toooutpace hello другим пользователям.

1. [Загрузить пакет версии 2 WordCount hello](http://aka.ms/servicefabric-wordcountappv2) toohello местоположения, куда вы загрузили hello версии 1 пакета.
2. Вернуть tooyour окно PowerShell и команда hello SDK обновления tooregister hello новой версии в кластере hello. Затем перейдите к обновлению hello fabric: / приложения WordCount.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    Вы увидите, что hello следующие выходные данные в PowerShell, что hello обновления начинается.
   
    ![Ход обновления в PowerShell][ps-appupgradeprogress]
3. Во время обновления hello будет продолжена, может оказаться проще toomonitor его состояние с Service Fabric Explorer. Откройте окно браузера и перейдите слишком[http://localhost:19080/обозреватель](http://localhost:19080/Explorer). Разверните **приложений** в дереве hello hello слева, затем выберите **WordCount**и, наконец, **fabric: / WordCount**. На вкладке essentials hello появится hello состояния обновления hello как проходит доменов обновления кластера hello.
   
    ![Ход обновления в обозревателе Service Fabric][sfx-upgradeprogress]
   
    Как происходит обновление hello через каждый домен, проверки работоспособности, выполненной tooensure правильно написанное приложение hello.
4. При повторном запуске hello ранее запрос для набора служб в фабрике hello hello: / приложения WordCount Обратите внимание, что hello WordCountService версии изменены, но hello WordCountWebService версии не:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Запрос служб приложений после обновления][ps-getsfsvc-postupgrade]
   
    Этот пример демонстрирует, как платформа Service Fabric управляет обновлениями: они применяются только к набору служб (либо к пакетам кода или конфигурации в этих службах), которые были изменены. Оно касается только hello набор служб (или кода и конфигурации пакетов в пределах этих служб), были ли изменены, что делает hello процесс обновления быстрее и надежнее.
5. Наконец возвращают toohello tooobserve браузера hello поведение hello новой версии приложения. Как и ожидалось, медленнее hello число по мере того и первая секция hello составляло немного более hello тома.
   
    ![Представление hello новую версию приложения hello в браузере hello][deployed-app-ui-v2]

## <a name="cleaning-up"></a>Очистка.
Перед упаковкой, очень важно, tooremember, hello локального кластера является вещественным числом. Приложения продолжают toorun в фоновом режиме hello, пока вы не удалите их.  В зависимости от характера приложения hello выполняемого приложения могут занимать значительных ресурсов на компьютере. У вас есть несколько вариантов toomanage приложений и hello кластера:

1. tooremove отдельного приложения и все его с данными, запустите hello следующую команду:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    Или удаление приложения hello из hello Service Fabric Explorer **действия** hello контекстном меню в виде списка в левой части приложения hello.
   
    ![Удаление приложения в обозревателе Service Fabric][sfe-delete-application]
2. После удаления приложения hello из кластера hello, отмените регистрацию версии 1.0.0 и 2.0.0 из типа приложения WordCount hello. При удалении пакетов приложения hello, включая кода hello и конфигурации из хранилища образов hello кластера.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    Или в обозреватель Service Fabric, выберите **наполнение типа** для приложения hello.
3. tooshut вниз hello кластера, но сохранить данные приложения hello и трассировки щелкните **остановить локальный кластер** в значок приложения hello системы.
4. кластер hello toodelete целиком, щелкните **удалить локального кластера** в значок приложения hello системы. Этот параметр приведет к другой медленной развертывания hello следующий раз при нажатии клавиши F5 в Visual Studio. Удаление локального кластера hello только в том случае, если не предполагается toouse некоторое время или если необходимо tooreclaim ресурсов.

## <a name="one-node-and-five-node-cluster-mode"></a>Режимы кластера с одним и с пятью узлами
При разработке приложений часто бывает необходимо быстро написать, изменить код или выполнить его отладку. toohelp оптимизировать этот процесс, hello локального кластера может работать в двух режимах: один узел или узел пяти. Каждый из этих режимов имеет свои преимущества. Режим пяти узел кластера позволяет toowork с реальными кластера. Вы можете тестировать сценарии отработки отказа и работать с несколькими экземплярами и репликами служб. Кластер с одним узлом режим — оптимизированный toodo быстрого развертывания и регистрации служб, toohelp быстро проверить код с помощью среды выполнения Service Fabric hello.

Режимы кластера с одним узлом и с пятью узлами не являются эмуляторами или имитаторами. Hello локальному кластеру разработки запусков hello того же кода платформы, который находится на кластеры с несколькими компьютерами.

> [!WARNING]
> При изменении режима кластера hello hello текущего кластера удаляется из системы и создается новый кластер. Hello данные, хранящиеся в кластере hello удаляется при изменении режима кластера.
> 
> 

toochange hello режим tooone узел кластера, выберите **Переключите режим кластера** в hello локального кластера Service Fabric диспетчера.

![Переключение режима кластера][switch-cluster-mode]

Или измените режим hello кластера, с помощью PowerShell:

1. Откройте новое окно PowerShell от имени администратора.
2. Запустите сценарий установки кластера hello из папки hello SDK:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    Настройка кластера занимает несколько минут. После завершения установки вы увидите примерно такой результат:
   
    ![Результат установки кластера][cluster-setup-success-1-node]

## <a name="next-steps"></a>Дальнейшие действия
* Теперь, когда вы развернули и обновили предварительно собранные приложения, вы можете [выполнить сборку своего приложения в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).
* Все hello действия, выполняемые в локальном кластере hello в этой статье может выполняться на [кластера Azure](service-fabric-cluster-creation-via-portal.md) также.
* Обновление Hello, мы выполнили в этой статье был basic. В разделе hello [документации по обновлению](service-fabric-application-upgrade.md) toolearn Дополнительные сведения о hello мощность и гибкость обновления Service Fabric.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
