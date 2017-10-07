---
title: "aaaDeploy приложение Azure Service Fabric с непрерывной интеграции (Team Services) | Документы Microsoft"
description: "Узнайте, как tooset непрерывной интеграции и развертывания для приложения Service Fabric, с помощью Visual Studio Team Services.  Развертывание кластера Service Fabric tooa приложения в Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Развертывание приложения, указав кластер Service Fabric tooa CI или компакт-диска
Этот учебник входит в три ряда и описывает способ tooset непрерывной интеграции и развертывания для приложения Azure Service Fabric с помощью Visual Studio Team Services.  Приложение Service Fabric требуется, создать приложение hello в [построения приложения .NET](service-fabric-tutorial-create-dotnet-app.md) используется в качестве примера.

В третьей части серии hello, вы узнаете, как:

> [!div class="checklist"]
> * Добавление проекта tooyour системы управления версиями
> * Создание определения сборки в Team Services
> * Создание определения выпуска в Team Services
> * Автоматическое развертывание и обновление приложения

Из этого цикла руководств вы узнаете, как выполнять такие задачи:
> [!div class="checklist"]
> * [Создание приложения .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md).
> * [Развертывание кластера удаленного tooa приложения hello](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Настройка непрерывной интеграции и непрерывного развертывания с помощью Visual Studio Team Services.

## <a name="prerequisites"></a>Предварительные требования
Перед началом работы с этим руководством выполните следующие действия:
- Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Установка Visual Studio 2017 г](https://www.visualstudio.com/) и установить hello **разработки Azure** и **ASP.NET и веб-разработки** рабочих нагрузок.
- [Установите пакет Service Fabric SDK hello](service-fabric-get-started.md)
- Создайте приложение Service Fabric, например с помощью [этого руководства](service-fabric-tutorial-create-dotnet-app.md). 
- Создайте кластер Service Fabric с Windows, например с помощью [этого руководства](service-fabric-tutorial-create-cluster-azure-ps.md).
- Создайте [учетную запись Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Загрузите пример приложения hello голосование
Если вы не сборку пример приложения hello голосование в [часть одного из этого учебника ряда](service-fabric-tutorial-create-dotnet-app.md), вы можете загрузить ее. В окне командной строки запустите hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Подготовка профиля публикации
После запуска [приложение создано](service-fabric-tutorial-create-dotnet-app.md) и [развертывания tooAzure приложения hello](service-fabric-tutorial-deploy-app-to-party-cluster.md), вы будете готовы tooset непрерывной интеграции.  Во-первых Подготовьте профиль публикации в приложении для использования процессом развертывания hello, которая выполняется в Team Services.  Hello профиля публикации должно быть ранее созданный кластер настроенных tootarget hello.  Запустите Visual Studio и откройте существующий проект приложения Service Fabric.  В **обозревателе решений**, щелкните правой кнопкой мыши приложение hello и выберите **публикации...** .

Выберите целевой профиль в рамках вашей toouse проект приложения для непрерывной интеграции рабочего процесса, например облако.  Укажите конечную точку подключения кластера hello.  Проверьте hello **обновления hello приложения** флажок, чтобы приложение обновляет для всех развертываний в Team Services.  Нажмите кнопку hello **Сохранить** hello параметры гиперссылки toosave toohello профиль публикации, а затем нажмите кнопку **отменить** hello tooclose-диалоговое окно.  

![Принудительная отправка профиля][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Совместное использование нового репозитория Team Services Git Visual Studio решение tooa
Совместно использовать исходные файлы приложения tooa командного проекта в Team Services, поэтому можно создавать сборок.  

Создание нового локального репозитория Git для проекта, выбрав **добавить tooSource управления** -> **Git** в строке состояния hello в нижнем правом углу hello Visual Studio. 

В hello **Push** просмотра в **Team Explorer**выберите hello **публикации репозитория Git** под заголовком **Push tooVisual Studio Team Services**.

![Принудительная отправка репозитория Git][push-git-repo]

Проверить ваш адрес электронной почты и выберите свою учетную запись в hello **домена Team Services** раскрывающегося списка. Введите имя репозитория и выберите **Опубликовать репозиторий**.

![Принудительная отправка репозитория Git][publish-code]

Публикация репозитория hello создает новый командный проект в вашей учетной записи с точно такое же имя в качестве локального репозитория hello hello. репозиторий toocreate hello в существующий командный проект, нажмите кнопку **Дополнительно** Далее слишком**репозитория** имя и выберите командный проект. Код можно просматривать в Интернете hello, выбрав **его см. на веб-hello**.

## <a name="configure-continuous-delivery-with-vsts"></a>Настройка непрерывной поставки с помощью VSTS
Определение сборки Team Services описывает рабочий процесс, состоящий из набора шагов сборки, которые выполняются последовательно. Создайте определение сборки, который создает пакет приложения Service Fabric и другие артефакты, кластер Service Fabric tooa toodeploy. Дополнительные сведения об [определениях сборок Team Services](https://www.visualstudio.com/docs/build/define/create). 

Определение выпуска Team Services описывает рабочий процесс, который выполняет развертывание кластера tooa пакета приложений. При совместном использовании hello определение построения и определение выпуска выполнение hello весь рабочий процесс, начиная с источника tooending файлы с запущенным приложением в кластере. Узнайте больше об [определениях выпуска](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)Team Services.

### <a name="create-a-build-definition"></a>Создание определения сборки
Откройте веб-браузер и перейдите tooyour нового командного проекта в: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Выберите hello **построения и выпуска** вкладку, затем **строит**, затем **+ новое определение**.  В **выберите шаблон**выберите hello **приложение Azure Service Fabric** шаблона и нажмите кнопку **применить**. 

![Выбор шаблона сборки][select-build-template] 

голосование приложения Hello содержит проект .NET Core, поэтому добавьте задачу, которая восстанавливает hello зависимости. В hello **задачи** представление, выберите **+ добавить задачу** в левом нижнем hello. Поиск на задачи командной строки hello toofind «Командная строка», а затем щелкните **добавить**. 

![Добавление задачи][add-task] 

В новую задачу hello, введите «Запуск dotnet.exe» **отображаемое имя**, «dotnet.exe» в **средство**и «восстановление» в **аргументы**. 

![Создание задачи][new-task] 

В hello **триггеры** щелкните hello **включения триггера** переключиться в **непрерывной интеграции**. 

Выберите **сохранить & очередь** и введите «Размещенные VS2017» в качестве hello **очереди агента**. Выберите **очереди** toomanually начать сборку.  Сборки также активируются после принудительного запуска или возврата.

toocheck ход сборки, коммутатор toohello **строит** вкладки.  После проверки успешно выполняется построение hello, определите определения выпуска, которая развертывает приложение tooa кластера. 

### <a name="create-a-release-definition"></a>Создание определения выпуска  

Выберите hello **построения и выпуска** вкладку, затем **выпуски**, затем **+ новое определение**.  В **создать определение выпуска**выберите hello **развертывание структуры службы Azure** шаблон из списка hello и нажмите кнопку **Далее**.  Выберите hello **построения** источника, проверьте hello **непрерывного развертывания** и нажмите кнопку **создать**. 

В hello **среды** щелкните **добавить** toohello справа от **подключения кластера**.  Укажите имя подключения «mysftestcluster», конечную точку кластера «tcp://mysftestcluster.westus.cloudapp.azure.com:19000», "и" hello Azure Active Directory "или" учетные данные сертификата для кластера hello. Для учетных данных Azure Active Directory, укажите учетные данные hello, toouse tooconnect toohello кластеру в hello **Username** и **пароль** поля. Для проверки подлинности на основе сертификатов, определите кодировку hello Base64 hello файл сертификата клиента в hello **сертификат клиента** поля.  См. на этом поле, сведения о том, как всплывающее окно справки hello tooget это значение.  Если сертификат защищен паролем, определить пароль hello в hello **пароль** поля.  Нажмите кнопку **Сохранить** определение выпуска toosave hello.

![Добавление подключения к кластеру][add-cluster-connection] 

Щелкните **Запуск в агенте** и в поле **Очередь развертывания** выберите **Hosted VS2017**. Нажмите кнопку **Сохранить** определение выпуска toosave hello.

![Запуск в агенте][run-on-agent]

Выберите **+ выпуска** -> **Создание выпуска** -> **создать** toomanually создать выпуск.  Убедитесь, что сообщение hello развертывание завершено успешно, и приложение hello в кластере hello.  Откройте веб-браузер и перейдите в слишком[http://mysftestcluster.westus.cloudapp.azure.com:19080/обозреватель/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Обратите внимание, версия приложения hello, в этом примере это «1.0.0.20170616.3». 

## <a name="commit-and-push-changes-trigger-a-release"></a>Фиксация и отправка изменений, создание выпуска
tooverify, hello конвейера непрерывной интеграции работает путем возврата служб tooTeam некоторые изменения в коде.    

При написании кода в Visual Studio изменения отслеживаются автоматически. Зафиксировать изменения tooyour локального репозитория Git, выбрав hello ожидающие изменения значок)![Ожидает][pending]) из строки состояния hello в правой нижней hello.

На hello **изменения** просмотра в Team Explorer, добавить сообщение с описанием обновления и фиксация изменений.

![Фиксация всех изменений][changes]

Значок панели выберите hello неопубликованные изменения состояния (![отменена публикация изменений][unpublished-changes]) или hello синхронизации представлении в Team Explorer. Выберите **Push** tooupdate код в Team Services или TFS.

![Отправка изменений][push]

Опубликуйте изменения tooTeam hello служб автоматически триггеров построения.  При успешном выполнении hello определения построения выпуска создается автоматически и начинается обновление приложения hello в кластере hello.

toocheck ход сборки, коммутатор toohello **строит** вкладке **Team Explorer** в Visual Studio.  После проверки успешно выполняется построение hello, определите определения выпуска, которая развертывает приложение tooa кластера.

Убедитесь, что сообщение hello развертывание завершено успешно, и приложение hello в кластере hello.  Откройте веб-браузер и перейдите в слишком[http://mysftestcluster.westus.cloudapp.azure.com:19080/обозреватель/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Обратите внимание, версия приложения hello, в этом примере это «1.0.0.20170815.3».

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Обновление приложения hello
Сделать изменения в коде приложения hello.  Сохраните и фиксации изменений hello, hello предыдущих действий.

Как только обновление hello начинается приложения hello, можно отслеживать ход выполнения обновления hello в обозреватель Service Fabric:

![Service Fabric Explorer][sfx2]

обновление приложения Hello может занять несколько минут. После завершения обновления hello hello будет запущено приложение hello следующей версии.  В этом примере — 1.0.0.20170815.4.

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Дальнейшие действия
Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Добавление проекта tooyour системы управления версиями
> * Создание определения сборки
> * Создание определения выпуска
> * Автоматическое развертывание и обновление приложения

Теперь, когда развертывания приложения и настроить непрерывную интеграцию, попробуйте hello следующее:
- [Обновление приложения](service-fabric-application-upgrade.md)
- [Тестирование приложения](service-fabric-testability-overview.md) 
- [Мониторинг и диагностика](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png