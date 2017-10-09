---
title: "aaaCreate веб-приложение ASP.NET Core в коде Visual Studio"
description: "Этот учебник демонстрирует, как toocreate ASP.NET Core веб-приложения с помощью кода Visual Studio."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Создание веб-приложения ASP.NET Core в Visual Studio Code
## <a name="overview"></a>Обзор
В этом учебнике показано, как toocreate ASP.NET Core веб-приложения с использованием [кода Visual Studio (VS Code)](http://code.visualstudio.com//Docs/whyvscode) и развернуть ее слишком[службе приложений Azure](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Хотя данная статья относится tooweb приложений, также применяется tooAPI приложений и мобильных приложений. 
> 
> 

ASP.NET Core является существенно переработанной версией ASP.NET. Это новая кроссплатформенная среда с открытым кодом, предназначенная для создания современных облачных веб-приложений с использованием .NET. Дополнительные сведения см. в разделе [tooASP.NET введение Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Дополнительную информацию о веб-приложениях службы приложений Azure см. в статье [Обзор веб-приложений](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Предварительные требования
* Установка [VSCode](http://code.visualstudio.com/Docs/setup).
* Установите Git. Можно установить систему с любого из этих сайтов: [Chocolatey](https://chocolatey.org/packages/git) или [git-scm.com](http://git-scm.com/downloads). Если новый tooGit, выберите [git scm.com](http://git-scm.com/downloads) и выберите вариант hello слишком**используйте Git из командной строки Windows hello**. После установки Git, вам потребуются имя пользователя Git tooset hello и адрес электронной почты как обязательный далее в учебнике hello (при выполнении фиксации из VS Code).  

## <a name="install-aspnet-core"></a>Установка ASP.NET Core
ASP.NET 5 Core представляют собой простой стек .NET для сборки современных облачных и веб-приложений, работающих в OS X, Linux и Windows. Он был создан из hello основание, tooprovide платформу разработки, оптимизированный для приложений, либо облачные развернутой toohello или выполнения в локальной. Он состоит из модульных компонентов с минимальными служебными данными, что позволяет сохранить гибкость при построении решений.

Этот учебник предназначен спроектированный tooget запущен построение приложений с помощью hello последние разработки версии ASP.NET Core. Привет, следуя инструкциям, определенных tooWindows. Инструкции по установке для OS X, Linux и Windows см. в статье [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started) (Начало работы с ASP.NET Core). 


> [!NOTE]
> Подробные указания по установке для OS X, Linux и Windows см. в статье об [установке ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-hello-web-app"></a>Создать веб-приложение hello
В этом разделе показано, как tooscaffold нового приложения ASP.NET, веб-приложения с помощью средства .NET CLI hello. 

1. Введите следующий текст hello в командной строке toocreate hello проект папку и формирования шаблонов hello приложение hello.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![Интерфейс командной строки .NET — генератор ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore hello необходимые пакеты NuGet, запустите hello следующую команду:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Запустите веб-приложение hello локально
Теперь, после создания веб-приложения hello и получения все пакеты NuGet hello, приложение hello, hello веб-приложения можно выполнять локально.

1. Выполните приложение hello (hello `dotnet run` команда выполняет построение приложения hello, когда он является устаревшим):
    ```terminal
    dotnet run
    ```
2. Откройте браузер и перейдите toohello URL-адреса.
   
    **http://localhost:5000**
   
    страница по умолчанию Hello hello веб-приложения будет выглядеть следующим образом.
   
    ![Веб-приложение, запущенное локально в браузере](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Закройте браузер. В hello **командное окно**, нажмите клавишу **Ctrl + C** tooshut работу приложения hello и закрыть hello **командное окно**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Создание веб-приложения в hello портала Azure
Hello ниже поможет выполнить создание веб-приложения в hello портала Azure.

1. Войдите в toohello [портала Azure](https://portal.azure.com).
2. Нажмите кнопку **NEW** на hello верхнего левого угла hello портала.
3. Щелкните **Веб-приложения > Веб-приложение**.
   
    ![Новое веб-приложение Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Введите значение в поле **Имя**, например **SampleWebAppDemo**. Обратите внимание, что это имя должно уникальным toobe портала hello потребует выполнения условия, при попытке имя tooenter hello. Таким образом, при выборе введите другое значение, вам потребуется toosubstitute это значение для каждого вхождения **SampleWebAppDemo** , отображаемые в этом учебнике. 
5. Выберите существующий план службы приложений в поле **План службы приложений** или создайте новый. При создании нового плана, выберите hello Ценовая категория, расположение и другие параметры. Дополнительные сведения о планах службы приложений см. в статье hello, [исчерпывающий обзор планы службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Колонка нового веб-приложения Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Щелкните **Создать**.
   
    ![Колонка веб-приложения](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Включить публикацию Git для нового веб-приложения hello
Git — это система управления распределенных версии, можно использовать toodeploy веб-приложения службы приложений Azure. Будут храниться hello код, предназначенный для веб-приложения в локальном репозитории Git и вы развернете tooAzure вашего кода с помощью принудительной отправки tooa удаленный репозиторий.   

1. Войти в hello [портала Azure](https://portal.azure.com).
2. Щелкните **Обзор**.
3. Нажмите кнопку **веб-приложений** tooview список hello веб-приложений, связанных с подпиской Azure.
4. Выберите веб-приложения hello, созданный в этом учебнике.
5. В колонке приложения hello web щелкните **параметры** > **непрерывного развертывания**. 
   
    ![Хост веб-приложений Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Щелкните **Выбор источника > Локальный репозиторий Git**.
7. Нажмите кнопку **ОК**.
   
    ![Локальный репозиторий Git для Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Если ранее вы не настроили учетные данные развертывания для публикации веб-приложения или другого приложения службы приложений, сделайте это сейчас, как показано ниже.
   
   * Щелкните **Параметры** > **Учетные данные развертывания**. Hello **задать учетные данные развертывания** отображается колонку.
   * Укажите имя пользователя и пароль.  Этот пароль потребуется позднее при настройке Git.
   * Щелкните **Сохранить**.
9. В колонке веб-приложения щелкните **Параметры > Свойства**. URL-адрес Hello hello удаленный репозиторий Git, вы развернете toois, показанный в разделе **URL-адрес GIT**.
10. Копировать hello **URL-адрес GIT** значение для последующего использования в учебнике hello.
    
    ![URL-адрес Git для Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Публикация вашего web app tooAzure службы приложений
В этом разделе вы создадите локального репозитория Git и push из этого репозитория tooAzure toodeploy вашей tooAzure web app.

1. В VS Code выберите hello **Git** параметр hello левой панели навигации.
   
    ![Значок Git в VSCode](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Выберите **Initialize репозитории** toomake убедиться, что рабочая область — в системе управления версиями git. 
   
    ![Инициализация Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Откройте окно командной строки hello и измените каталог toohello каталоги веб-приложения. Затем введите hello следующую команду:
   
        git config core.autocrlf false
   
    Эта команда предотвращает проблемы, связанные с символами конца строк CRLF и LF.
4. В VS Code, добавьте сообщение фиксации и нажмите кнопку hello **фиксации все** значок галочки.
   
    ![«Фиксировать все» в Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. После завершения обработки Git, вы увидите, что нет файлов в окно приветствия Git под **изменения**. 
   
    ![Git без изменений](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Измените задней toohello окно команд, где командную строку hello указывает каталог toohello где находится веб-приложения.
7. Создайте удаленную ссылку для принудительной отправки обновлений tooyour веб-приложения с помощью hello URL-адрес Git (окончание в «.git»), скопированное ранее.
   
        git remote add azure [URL for remote repository]
8. Настройка Git toosave учетные данные локально, чтобы они будут автоматически добавленных tooyour принудительной команды, сформированные из кода VS.
   
        git config credential.helper store
9. Принудительно вашей tooAzure изменения, введя следующую команду hello. После этого tooAzure начальной принудительной можно будет toodo все принудительной hello команд VS Code. 
   
        git push -u azure master
   
    Запрашивается пароль hello, созданный ранее в Azure. **Примечание. Ваш пароль не будет отображаться.**
   
    Вывод Hello hello выше команда завершается с сообщением, что развертывание было выполнено успешно.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> При внесении изменений tooyour приложение можно опубликовать непосредственно в коде VS, с помощью встроенных возможностей Git hello, выбрав hello **зафиксировать все** параметр следуют hello **Push** параметр. Вы найдете hello **Push** параметр, доступный в toohello Далее раскрывающееся меню hello **зафиксировать все** и **обновление** кнопки.
> 
> 

Если вам требуется toocollaborate над проектом, следует помещает tooGitHub между tooAzure принудительной отправки.

## <a name="run-hello-app-in-azure"></a>Выполните приложение hello в Azure
Теперь, когда развертывания веб-приложения, запустим приложение hello в размещенных в Azure. 

Это можно сделать двумя способами:

* Откройте браузер и введите имя веб-приложения hello следующим образом.   
  
        http://SampleWebAppDemo.azurewebsites.net
* В hello портал Azure, найдите колонка приложения hello web для веб-приложения и нажмите кнопку **Обзор** tooview приложения 
* в браузере по умолчанию.

![Веб-приложение Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Сводка
В этом учебнике вы узнали, как toocreate веб-приложения в VS Code и развернуть ее tooAzure. Дополнительные сведения о VS Code см. в статье hello, [почему кода на Visual Studio?](https://code.visualstudio.com/Docs/) Дополнительную информацию о веб-приложениях службы приложений Azure см. в статье [Обзор веб-приложений](app-service-web-overview.md). 

