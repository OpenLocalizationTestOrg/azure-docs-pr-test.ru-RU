---
title: "ресурсы документации aaaAzure веб-заданий"
description: "Рекомендуется использовать ресурсы для обучения как toouse веб-заданий Azure и hello Azure SDK веб-заданий."
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Документация по веб-заданиям Azure
## <a name="overview"></a>Обзор
Этот раздел содержит ссылки ресурсов toodocumentation о toouse веб-заданий Azure и hello Azure SDK веб-заданий. Веб-задания Azure предоставляют простой способ toorun сценариев или программ в качестве фоновые процессы в контексте hello [службы приложений веб-приложения, приложения API или мобильного приложения](../app-service/app-service-value-prop-what-is.md). Можно загружать и запускать исполняемые файлы, например CMD, BAT, EXE (.NET), PS1, SH, PHP, PY, JS и JAR. Эти программы могут работать как веб-задания по расписанию (cron) или постоянно.

Здравствуйте, назначение hello [SDK веб-заданий](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) является toosimplify hello код, предназначенный для выполнения стандартных задач, которые могут выполнять веб-задания, например обработки изображений, обработки очередей, объединение RSS, обслуживание файлов и отправки сообщений электронной почты. Hello SDK веб-задания имеет встроенные функции для работы с хранилищем Azure и Service Bus, планирование задач и обработка ошибок и других стандартных сценариев. Кроме того, он имеет разработан toobe расширяемой и [репозитория открытым исходным кодом для расширений](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [Функции Azure](../azure-functions/functions-overview.md) (в настоящее время предварительная версия) основан на версии hello SDK веб-задания, который работает с C# скрипта, Node.js и другие языки. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Создание, развертывание веб-заданий и управление ими средствами Visual Studio не вызовет проблем. Веб-задания можно создавать из шаблонов, публиковать их и управлять ими (запуск, остановка, мониторинг и отладка). 

панель мониторинга веб-заданий Hello в hello портал Azure предоставляет возможности управления, которые обеспечивают полный контроль над hello выполнение веб-заданий, включая hello возможность tooinvoke отдельные функции в веб-заданий. панель мониторинга Hello также отображает функции среды выполнения и вывода. 

## <a name="getstarted"></a>Начало работы с веб-задания и hello SDK веб-заданий
* [Введение tooAzure веб-заданий](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Веб-задания Azure потрясающие, начните использовать их прямо сейчас!](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (Запись блога Троя Ханта (Troy Hunt).)
* [Компоненты веб-заданий Azure](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [Что такое hello SDK веб-заданий](websites-dotnet-webjobs-sdk.md)
* [Руководство по фоновым заданиям на основе шаблонов и рекомендаций от Майкрософт](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [Объявляет о hello 1.1.0 RTM из веб-задания пакета SDK Microsoft Azure](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Приступая к работе с hello Azure SDK веб-заданий](websites-dotnet-webjobs-sdk-get-started.md)
* [Как toouse Azure очередь хранилища с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Как toouse Azure таблицу хранилища с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Как toouse шины обслуживания Azure с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-service-bus.md)
* [Краткий справочник по пакету SDK веб-заданий (скачиваемый PDF-файл)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [Документация по настройке веб-заданий в GitHub](https://github.com/projectkudu/kudu/wiki/Web-jobs).
* Видеоролики
  * [Веб-задания и hello SDK веб-заданий](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Серия видеопрограмм по веб-заданиям Azure на канале 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Введение в средства для работы с веб-заданиями для Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Средства для работы с веб-заданиями и удаленная отладка](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Обновление веб-заданий Azure с Пранавом Растоги. Расширяемость в выпуске 1.1](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

См. также: hello в следующих разделах [развертывание веб-заданий](#deploy) и [тестирование и отладка веб-задания](#debug).

## <a name="deploy"></a>Развертывание веб-заданий
* [Как tooDeploy веб-заданий Azure с помощью Visual Studio](websites-dotnet-deploy-webjobs.md)
* [Как с помощью веб-заданий toodeploy hello портала Azure](web-sites-create-web-jobs.md)
* [Включение предоставления веб-заданий Azure из командной строки или постоянно](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Развертывание .NET Git консоли tooAzure приложения с помощью веб-заданий](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [Развертывание веб-задания F # tooAzure](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Развертывание пользовательских служб в качестве веб-заданий Azure](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Видеоролики
  * [Введение в средства для работы с веб-заданиями для Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Средства для работы с веб-заданиями и удаленная отладка](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>Планирование веб-заданий
* [Hello Добавление Azure веб-задания диалогового окна](websites-dotnet-deploy-webjobs.md#configure)
* [Создание веб-задания запланировано hello портала Azure](web-sites-create-web-jobs.md#CreateScheduled)
* [Подключение tooa задания планировщика веб-задания](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Планирование веб-заданий Azure с помощью выражений cron](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [Планирование отдельных функций веб-задания, с помощью hello TimerTrigger SDK веб-заданий](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Проверка и отладка веб-заданий
* [Новые функции для разработки и отладки для веб-заданий Azure в Visual Studio](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Hello представления панели мониторинга веб-заданий](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Как toowrite журналов с помощью hello SDK веб-задания и просматривать их в панель мониторинга hello](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [Удаленная отладка веб-заданий](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Кто записал этот большой двоичный объект?](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Размещение интерактивного кода в облаке hello](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [Добавление трассировки tooAzure веб-заданий](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [Наблюдение, диагностика и устранение неисправностей хранилища Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Видеоролики
  * [Средства для работы с веб-заданиями и удаленная отладка](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Масштабирование веб-заданий
* [Масштабирование приложения с помощью веб-сайтов Azure](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Служба приложений Azure: конструирование веб-приложений для бизнеса c широкими возможностями масштабирования](https://channel9.msdn.com/Events/Build/2014/3-626). Описание масштабирования веб-приложений с веб-заданий, включая hello SDK веб-заданий.
* Видеоролики
  * [Масштабирование веб-заданий](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Дополнительные ресурсы по веб-заданиям
* [Общедоступная запись в блоге о веб-заданиях Azure Магнуса Мортенссона (Magnus Mårtensson)](http://magnusmartensson.com/azure-webjobs-ga)
* [Запуск веб-заданий Powershell в службе приложений Azure](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Получение уведомлений после завершения веб-заданий, инициированных Azure](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Простые правила резервного копирования веб-приложений с веб-заданиями](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Замедление работы веб-приложений и облачных служб Azure по первому требованию](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Показывает, как веб-заданий toosimulate toouse hello функцию AlwaysOn, которая доступна только для ценовой категории Standard hello.
* [Нормальное завершение работы веб-заданий](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). Сведения о нормальном завершении работы пакета SDK для веб-заданий см. в разделе [Нормальное завершение работы](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
* [Automating Backups with Azure WebJobs & AzCopy](http://markjbrown.com/azure-webjobs-azcopy/) (Автоматизация резервного копирования с помощью веб-заданий Azure и AzCopy)
* Видеоролики
  * [Видеопрограммы по веб-заданиям Azure от Магнуса Мортенссона (Magnus Mårtensson)](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Серия видеопрограмм по веб-заданиям Azure на канале 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Дополнительные ресурсы по пакету SDK для веб-заданий
* [Заметки о выпуске пакета SDK веб-заданий](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [Исходный код пакета SDK веб-заданий](https://github.com/Azure/azure-webjobs-sdk)
* [Расширения пакета SDK веб-задания в исходном коде](https://github.com/Azure/azure-webjobs-sdk-extensions), с [модель расширяемости подробное руководство toohello](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [Исходный код пакета SDK для веб-заданий](https://github.com/Azure/azure-webjobs-sdk-script/) (для [функций Azure](../azure-functions/functions-overview.md))
* [Веб-задания tooupload FREB файлов tooAzure хранилища с использованием пакета SDK веб-задания "hello"](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Размещение веб-задания Azure за пределами Azure, с hello, ведение журнала преимуществ от Azure размещенного веб-задания](http://bypassion.dk/?p=510)
* [Создание средства импорта данных с помощью веб-заданий Azure](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Обзор функций Azure](../azure-functions/functions-overview.md)
* Видеоролики
  * [Серия видеопрограмм по веб-заданиям Azure на канале 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Примеры приложений веб-заданий
* [Примеры приложений, предоставленные группой hello веб-задания на GitHub](https://github.com/azure/azure-webjobs-sdk-samples)
* [Простой веб-приложения Azure с сервером веб-заданий с помощью hello SDK веб-заданий](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Демонстрирует применение веб-заданий по расписанию или при наступлении определенных событий. См. hello блога [перестроение hello SiteMonitR, с помощью пакета SDK веб-заданий Azure](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Блоги
* [Блог Azure](/blog)
* [Блог Amit Apple](http://blog.amitapple.com/). Основное внимание уделяется веб-заданий (не hello SDK).
* [Блог Магнуса Мортенссона (Magnus Mårtensson)](http://magnusmartensson.com/)

## <a name="gethelp"></a>Справочная информация о веб-заданиях
* [StackOverflow для веб-заданий](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [Переполнение стека для hello SDK веб-заданий](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [StackOverflow для функций Azure](http://stackoverflow.com/questions/tagged/azure-functions)
* [Форум по Azure и ASP.NET](http://forums.asp.net/1247.aspx)
* [Форум по веб-приложениям службы приложений Azure](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Сайт пользовательских мнений по веб-приложениям Azure](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Используйте hello хэштегом #AzureWebJobs.
* [Сообщение об ошибке или проблеме в веб-задании](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

