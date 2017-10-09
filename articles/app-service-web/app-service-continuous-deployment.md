---
title: "aaaContinuous tooAzure развертывания службы приложений | Документы Microsoft"
description: "Узнайте, как tooAzure tooenable непрерывного развертывания служб приложений."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>TooAzure непрерывного развертывания служб приложений
В этом учебнике показано как tooconfigure рабочего процесса непрерывного развертывания для вашего [службе приложений Azure] приложения. Интеграция служб приложений с BitBucket, GitHub, и [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) позволяет непрерывной рабочий процесс развертывания, где Azure извлекает hello самые последние обновления из проекта опубликованных tooone из этих служб. Непрерывное развертывание очень удобно для проектов, которые часто обновляются несколькими участниками.

toofind out как tooconfigure непрерывного развертывания вручную из репозитория облака, не перечислен в hello портал Azure (такие как [GitLab](https://gitlab.com/)), в разделе [Настройка непрерывного развертывания, с помощью действий вручную](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Включение непрерывного развертывания
tooenable непрерывного развертывания,

1. Опубликуйте репозиторий содержимого toohello приложения, который будет использоваться для непрерывного развертывания.  
    Дополнительные сведения о публикации служб toothese проекта см. в разделе [создания репозитория (GitHub)], [создания репозитория (BitBucket)], и [Приступая к работе с VSTS].
2. В колонке меню приложения в hello [портал Azure], нажмите кнопку **развертывание Приложений > варианты развертывания**. Нажмите кнопку **Выбор источника**, а затем выберите источник развертывания hello.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > tooconfigure учетную запись VSTS для развертывания службы приложений см. в разделе это [учебника](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Полный рабочий процесс авторизации hello.
4. В hello **источник развертывания** колонке выберите проект hello и ветвление toodeploy из. Закончив, нажмите кнопку **OK**.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > При включении непрерывного развертывания с использованием GitHub или BitBucket будут отображаться и открытые, и закрытые проекты.
   > 
   > 
   
    Службы приложений создает связь с выбранном репозитории hello, запрашивающий hello файлы из указанной ветви hello и сохраняет копию репозиторий для своего приложения службы приложений. При настройке VSTS непрерывного развертывания из hello портал Azure, интеграция hello использует службы приложения hello [подсистема развертывания Kudu](https://github.com/projectkudu/kudu/wiki), который уже автоматизирует задачи построения и развертывания с каждой `git push`. Нет необходимости tooseparately непрерывное развертывание в VSTS. После завершения этого процесса hello **варианты развертывания** колонка приложения будет отображаться активное развертывание, указывающее развертывания завершилась успешно.
5. приложение hello tooverify успешно развернут, нажмите кнопку hello **URL-адрес** hello верхней части колонки приложение hello в hello портал Azure.
6. tooverify, возникающей непрерывного развертывания из репозитория hello по своему усмотрению push репозиторий toohello изменений. Приложение следует обновить изменения hello tooreflect вскоре после завершения hello принудительной toohello репозитория. Убедитесь, что он извлечены обновления hello в hello **варианты развертывания** колонке приложения.

## <a name="VSsolution"></a>Непрерывное развертывание решения Visual Studio
Помещает tooAzure решения Visual Studio приложения службы — так же просто, как отправить файл index.html простой. процесс развертывания службы приложения Hello упрощает все сведения о hello, включая восстановление NuGet зависимостей и построения двоичные файлы приложения hello. Рекомендации по hello источника управления поддержания кода только в репозиторий Git и позволить позаботиться о hello rest развертывания службы приложений.

Hello шаги для принудительной отправки вашего tooApp решения Visual Studio, службы, hello же, как и hello [предыдущего раздела](#overview), предоставленном настройке решения и репозитория следующим образом:

* Используйте hello Visual Studio исходный элемент управления параметр toogenerate `.gitignore` файла, например hello образ ниже или добавьте вручную `.gitignore` файл в корневом каталоге репозитория с содержимым аналогичные toothis [.gitignore пример](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Добавьте репозиторий tooyour дерева каталогов hello всего решения, с hello SLN-файл в корневом хранилище hello.

После настройки вашего хранилища, как описано и настроить приложение в Azure для непрерывной публикации из одного hello online репозиториев Git, можно разрабатывать приложения ASP.NET локально в Visual Studio и постоянно путем простого развертывания вашего кода нажать online репозиторий Git изменения tooyour.

## <a name="disableCD"></a>Отключение непрерывного развертывания
toodisable непрерывного развертывания,

1. В колонке меню приложения в hello [портал Azure], нажмите кнопку **развертывание Приложений > варианты развертывания**. Нажмите кнопку **Disconnect** в hello **варианты развертывания** колонку.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. После ответа на **Да** toohello сообщение с подтверждением, можно возвращать колонка tooyour приложения и нажмите кнопку **развертывание Приложений > варианты развертывания** при желании tooset вверх публикации из другого источника.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Как tooinvestigate распространенные проблемы с непрерывным развертыванием](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [Как toouse PowerShell для Azure]
* [Как toouse hello средства командной строки Azure для Mac и Linux]
* [Документация по Git]
* [Project Kudu](https://github.com/projectkudu/kudu/wiki)
* [Использовать Azure tooautomatically создания приложении CI/CD конвейера toodeploy ASP.NET 4](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

[службе приложений Azure]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[портал Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Как toouse PowerShell для Azure]: /powershell/azureps-cmdlets-docs
[Как toouse hello средства командной строки Azure для Mac и Linux]:../cli-install-nodejs.md
[Документация по Git]: http://git-scm.com/documentation

[создания репозитория (GitHub)]: https://help.github.com/articles/create-a-repo (Создание репозитория GitHub)
[создания репозитория (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo (Создание репозитория BitBucket)
[Приступая к работе с VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview (Приступая к работе с VSTS)
