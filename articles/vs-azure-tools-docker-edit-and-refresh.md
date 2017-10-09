---
title: "aaaDebugging приложений в локальном контейнере Docker | Документы Microsoft"
description: "Узнайте, как toomodify приложения, запущенного в локальном контейнере Docker, обновите hello контейнере с помощью изменения и обновления и установите отладочные точки останова"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Отладка приложений в локальном контейнере Docker
## <a name="overview"></a>Обзор
Hello Visual Studio Tools для Docker предоставляет согласованный способ toodevelop в и проверка приложения на локальном компьютере в контейнер Linux Docker.
У вас нет контейнера hello toorestart каждый раз при внесении изменений в код.
В этой статье показано, как toouse hello «Изменить и обновить» функция toostart основных компонентов веб-приложение ASP.NET в локальном контейнере Docker, внесите необходимые изменения, а затем обновить браузер toosee hello эти изменения.
В этой статье также показано, как tooset точки останова для отладки.

> [!NOTE]
> Поддержка контейнера Windows будет реализована в следующем выпуске.
>
>

## <a name="prerequisites"></a>Предварительные требования
должны быть установлены следующие средства Hello.

* [Последняя версия Visual Studio](https://www.visualstudio.com/downloads/)
* Установить [пакет SDK для Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122).

toorun контейнеры Docker локально, вам потребуется клиент локальной docker.
Можно использовать hello [элементов Docker](https://www.docker.com/products/docker-toolbox), которого требуется отключить toobe Hyper-V, или можно использовать [Docker для Windows](https://www.docker.com/get-docker), когда используется Hyper-V и требуется Windows 10.

Если с помощью элементов Docker, вам потребуется слишком[настройки клиента Docker hello](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Создание веб-приложения
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Добавление поддержки Docker
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Изменение и обновление кода
tooquickly перечисления изменений, можно запустить приложение в контейнере и продолжить toomake изменения, их просмотра, как и с IIS Express.

1. Задать конфигурацию решения hello слишком`Debug` и нажмите клавишу  **&lt;сочетание клавиш CTRL + F5 >** toobuild вашей docker образа и его локального запуска.

    Когда образ контейнера hello построен и запущен в контейнер Docker, Visual Studio запустит hello веб-приложение в браузере по умолчанию.
    Если вы используете браузер Microsoft Edge hello или нет ошибок, см. раздел [Устранение неполадок](vs-azure-tools-docker-troubleshooting-docker-errors.md) раздела.
2. Go toohello о страница, которая является здесь мы увидим toomake изменения.
3. Возвращает tooVisual Studio и откройте `Views\Home\About.cshtml`.
4. Добавить hello следующему HTML содержимого toohello конца файла hello и сохранить изменения hello.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Просмотр hello окно вывода, после завершения сборки .NET hello и просмотреть эти строки, перейдите назад tooyour браузера и обновите hello о странице.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. Изменения применены!

## <a name="4-debug-with-breakpoints"></a>4. Отладка с использованием точек останова
Часто изменения потребуется дальнейшей проверки, используя hello отладки Visual Studio.

1. Возвращает tooVisual Studio и откройте`Controllers\HomeController.cs`
2. Замените содержимое метода About() hello hello hello следующие:

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Набор toohello останова слева от hello `string message`... строки.
4. Попаданий  **&lt;F5 >** toostart отладки.
5. Перейдите в toohello о toohit страницы точка останова.
6. Переключение точки останова для hello tooview Studio tooVisual и проверьте значение сообщение hello.

   ![][2]

## <a name="summary"></a>Сводка
С [инструменты Visual Studio 2015 для Docker](https://aka.ms/DockerToolsForVS), вы можете получить hello производительность работы локально, с hello реалистичности рабочей среде разработки в контейнере Docker.

## <a name="troubleshooting"></a>Устранение неполадок
[Устранение неполадок при разработке в Visual Studio Docker](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Дополнительные сведения об использовании Docker с Visual Studio, Windows и Azure
* [Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) (Инструменты Docker для Visual Studio) — разработка кода .NET Core в контейнере.
* [Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) (Инструменты Docker для Visual Studio Team Services) — сборка и развертывание контейнеров Docker.
* [Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) (Инструменты Docker для Visual Studio Code) — языковые службы для редактирования файлов Docker с дополнительными сценариями E2E (ожидаются в ближайшее время).
* [Windows Container Information](http://aka.ms/containers)(Сведения о контейнерах Windows) — сведения о Windows Server и Nano Server.
* [Служба контейнеров Azure](https://azure.microsoft.com/services/container-service/)  -  [общие сведения о службе контейнеров Azure](http://aka.ms/AzureContainerService).
* Дополнительные примеры работы с Docker см. в разделе [работы с Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) из hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [Демонстрация](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). Дополнительные примеры использования из образца hello HealthClinic.biz, в разделе [примеры использования средств разработчика Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Различные инструменты Docker
[Some great docker tools (Steve Lasker's blog) (Несколько отличных инструментов Docker — блог Стива Ласкера (Steve Lasker))](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>Рекомендуемые статьи
[Введение tooMicroservices из NGINX](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Презентации
* [Steve Lasker: VS Live Las Vegas 2016 - Docker e2e (Стив Ласкер: презентация по Visual Studio и Docker E2E — Лас-Вегас, 2016 г.)](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Введение tooASP.NET Core @ 2016 — когда вы в демонстрационной построения](https://channel9.msdn.com/Events/Build/2016/B810)
* [Developing .NET apps in containers, Channel 9 (Разработка приложений .NET в контейнерах, Channel 9)](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
