---
title: "aaaCreate ASP.NET веб-приложения в Azure | Документы Microsoft"
description: "Узнайте, как toorun веб-приложений в службе приложений Azure путем развертывания по умолчанию hello ASP.NET веб-приложения."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Создание веб-приложения ASP.NET в Azure

[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.  Краткого руководства показано, как toodeploy первый ASP.NET веб-приложения tooAzure веб-приложений. В результате будет создана группа ресурсов, состоящая из плана службы приложений и развернутого веб-приложения Azure.

Посмотрите видео toosee hello краткого руководства в действии, а затем следуйте hello шаги самостоятельно toopublish своего первого приложения .NET в Azure.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

* Установка [2017 г. Visual Studio](https://www.visualstudio.com/downloads/) с hello следующие рабочие нагрузки:
    - **ASP.NET и веб-разработка;**
    - **разработка Azure.**

    ![ASP.NET и веб-разработка, разработка Azure (в разделе Web & Cloud (Сеть и облако))](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>Создание веб-приложения ASP.NET

Создайте проект в Visual Studio, последовательно выбрав пункты **Файл > Создать > Проект**. 

В hello **новый проект** диалогового окна выберите **Visual C# > Web > веб-приложения ASP.NET (.NET Framework)**.

Имя приложения hello _myFirstAzureWebApp_, а затем выберите **ОК**.
   
![Диалоговое окно "Новый проект"](./media/app-service-web-get-started-dotnet/new-project.png)

Вы можете развернуть любого типа tooAzure приложения ASP.NET web. Для краткого руководства, выберите hello **MVC** шаблона и убедитесь, что проверка подлинности задано слишком**без проверки подлинности**.
      
Нажмите кнопку **ОК**.

![Диалоговое окно "Новый проект ASP.NET"](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

Меню "hello" выберите **Отладка > Начать без отладки** toorun hello веб-приложения локально.

![Локальный запуск приложения](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>Публикация tooAzure

В hello **обозревателе решений**, щелкните правой кнопкой мыши hello **myFirstAzureWebApp** проект и выберите **публикации**.

![Публикация в обозревателе решений](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

Выберите **Служба приложений Microsoft Azure** и нажмите кнопку **Опубликовать**.

![Публикация с помощью страницы обзора проекта](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

При этом откроется hello **Создание приложения службы** диалоговое окно, которое служит для создания всех hello необходимые ресурсы Azure toorun hello, ASP.NET веб-приложения в Azure.

## <a name="sign-in-tooazure"></a>Войдите в tooAzure

В hello **Создание приложения службы** диалогового окна выберите **добавить учетную запись**и выполните вход tooyour подписки Azure. Если вы уже выполнили вход, выберите hello учетной записи, содержащей hello правильно подписку из раскрывающегося списка hello.

> [!NOTE]
> Если вы уже выполнили вход, пока не нажимайте кнопку **Создать**.
>
>
   
![Войдите в tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Создание группы ресурсов

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Далее слишком**группы ресурсов**выберите **New**.

Имя группы ресурсов hello **myResourceGroup** и выберите **ОК**.

## <a name="create-an-app-service-plan"></a>Создание плана службы приложений

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Далее слишком**план служб приложений**выберите **New**. 

В hello **настроить план служб приложений** диалогового окна, используйте параметры hello в таблице hello следующий снимок экрана приветствия.

![Создание плана службы приложений](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Настройка | Рекомендуемое значение | Описание |
|-|-|-|
|План обслуживания приложения| myAppServicePlan | Имя плана служб приложений hello. |
| Расположение | Западная Европа | Hello центра обработки данных, где размещается веб-приложение hello. |
| Размер | Free | [Ценовая категория](https://azure.microsoft.com/pricing/details/app-service/) определяет возможности размещения. |

Нажмите кнопку **ОК**.

## <a name="create-and-publish-hello-web-app"></a>Создание и публикация веб-приложения hello

В **имя веб-приложения**, введите имя уникальным приложения (допустимые символы — `a-z`, `0-9`, и `-`), или примите hello автоматически создается уникальное имя. Hello URL-адрес веб-приложения hello `http://<app_name>.azurewebsites.net`, где `<app_name>` является имя вашего веб-приложения.

Выберите **создать** toostart Создание hello ресурсов Azure.

![Настройка имени веб-приложения](./media/app-service-web-get-started-dotnet/web-app-name.png)

После завершения работы мастера hello, он публикует hello ASP.NET web app tooAzure и затем запускает hello приложение в браузере по умолчанию hello.

![Опубликованное веб-приложение ASP.NET в Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

Имя веб-приложения Hello, указанный в hello [Создание и публикация шаг](#create-and-publish-the-web-app) используется как префикс URL-адреса в формате hello hello `http://<app_name>.azurewebsites.net`.

Поздравляем, ваше веб-приложение ASP.NET работает в службе приложений Azure в режиме реального времени.

## <a name="update-hello-app-and-redeploy"></a>Приложение hello обновления и повторного развертывания

Из hello **обозревателе решений**откройте _Views\Home\Index.cshtml_.

Найти hello `<div class="jumbotron">` HTML тег верхней hello и замените весь элемент hello hello, следующий код:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooAzure tooredeploy, щелкните правой кнопкой мыши hello **myFirstAzureWebApp** проекта в **обозревателе решений** и выберите **публикации**.

Страница "Публикация" hello, установите **публикации**.

По завершении публикации Visual Studio запускает браузер toohello URL-адрес веб-приложения hello.

![Обновленное веб-приложение ASP.NET в Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Управление hello Azure веб-приложения

Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toomanage hello веб-приложения.

Hello в левом меню, выберите **службы приложений**, а затем выберите имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-get-started-dotnet/access-portal.png)

Отобразится страница обзора вашего веб-приложения. Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление. 

![Колонка службы приложений на портале Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

меню слева Hello предоставляет различные страницы для настройки приложения. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Создание приложения ASP.NET в Azure с подключением к базе данных SQL](app-service-web-tutorial-dotnet-sqldatabase.md)
