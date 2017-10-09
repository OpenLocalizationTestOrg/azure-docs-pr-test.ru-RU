---
title: "aaaAutomate развертывание приложения Azure с помощью средства командной строки | Документы Microsoft"
description: "Обнаружить сведения о развертывании приложения Azure из командной строки hello"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Автоматизация развертывания приложения Azure с помощью программ командной строки
Вы можете автоматизировать развертывание приложений Azure с помощью программ командной строки. В этой статье перечислены доступные средства и hello полезные ссылки, которые показывают, как toouse их в рабочий процесс развертывания. 

## <a name="msbuild"></a>Автоматизация развертывания с помощью MSBuild
Если вы используете hello [интегрированной среды разработки Visual Studio](#vs) для разработки, можно использовать [MSBuild](http://msbuildbook.com/) tooautomate ничего можно сделать в интерфейс IDE. Либо можно настроить MSBuild toouse [веб-развертывания](#webdeploy) или [FTP или FTPS](#ftp) toocopy файлов. Веб-развертывание может также автоматизировать множество других связанных с развертыванием задач, таких как развертывание баз данных.

Дополнительные сведения о развертывания из командной строки с помощью MSBuild см. в разделе hello следующие ресурсы:

* [Веб-развертывание ASP.NET с помощью Visual Studio: развертывание с использованием командной строки](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). Десятая в серию учебников, о tooAzure развертывания с помощью Visual Studio. Показано, как toouse hello toodeploy командной строки после настройки профилей публикации в Visual Studio.
* [Hello внутри Microsoft Build Engine: с помощью MSBuild и Team Foundation Build](http://msbuildbook.com/). Печатная копия книги, который содержит разделы о том, как toouse MSBuild для развертывания.

## <a name="powershell"></a>Автоматизация развертывания с помощью Windows PowerShell
Можно выполнять функции развертывания с использованием MSBuild или FTP из [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Если сделать это, также можно использовать набор командлетов Windows PowerShell, которые позволяют легко toocall hello Azure REST управления API.

Дополнительные сведения см. в разделе hello следующие ресурсы:

* [Развертывание репозиторий GitHub tooa связанного приложения web](app-service-web-arm-from-github-provision.md)
* [Подготовка веб-приложения к работе с базой данных SQL](app-service-web-arm-with-sql-database-provision.md)
* [Предсказуемые подготовка и развертывание микрослужб в Azure](app-service-deploy-complex-application-predictably.md)
* [Создание реальных облачных приложений в Azure — полная автоматизация](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything) Электронная книга главе, описывается, как пример приложения hello hello электронную показано использует toocreate сценариев Windows PowerShell Azure тестовой среде и развертывание tooit. В разделе hello [ресурсы](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) раздел для ссылки tooadditional документация по Azure PowerShell.
* [С помощью скриптов Windows PowerShell tooPublish tooDev и тестовых средах](../vs-azure-tools-publishing-using-powershell-scripts.md). Как toouse развертывания Windows PowerShell сценарии, Visual Studio создает.

## <a name="api"></a>Автоматизация развертывания с помощью API управления .NET
Можно написать код C# функции tooperform MSBuild или FTP для развертывания. Если сделать это, можно открыть сайт hello управления Azure REST API tooperform функций управления.

Дополнительные сведения см. в разделе hello следующих ресурсов:

* [Автоматизация все данные с помощью библиотеки управления hello Azure и .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Введение toohello .NET API и ссылки toomore документация управления.

## <a name="cli"></a>Развертывание из интерфейса командной строки Azure (Azure CLI)
Hello командной строки можно использовать в Windows, Mac или Linux toodeploy машины по протоколу FTP. Если сделать это, можно также открыть hello Azure REST управления API с помощью Azure CLI hello.

Дополнительные сведения см. в разделе hello следующих ресурсов:

* [Программы командной строки Azure](https://azure.microsoft.com/downloads/). Страница портала на сайте Azure.com с информацией о программе командной строки.

## <a name="webdeploy"></a>Развертывание из командной строки веб-развертывания
[Веб-развертывание](http://www.iis.net/downloads/microsoft/web-deploy) — это программное обеспечение Майкрософт для tooIIS развертывания, не только предоставляет интеллектуальной службе синхронизации функции, но также можно выполнять или координации многих других связанных с развертыванием задачи, которые не могут быть автоматизированы при использовании FTP. Например, веб-развертывание позволяет развернуть новую базу данных или обновления базы данных вместе с веб-приложением. Веб-развертывания можно сократить время, необходимое hello tooupdate существующий сайт, так как он интеллектуально можно скопировать только измененные файлы. Microsoft Visual Studio и Team Foundation Server была добавлена поддержка веб-развертывания встроенные, но можно также использовать веб-развертывание непосредственно из развертывания tooautomate hello командной строки. Команд веб-развертывания являются очень мощными, но hello можно легко запутаться.

## <a name="more-resources"></a>Дополнительные ресурсы
Другой автоматизации toocommand строки параметр развертывания — toouse облачные службы, таких как [развертывание множественного](http://en.wikipedia.org/wiki/Octopus_Deploy). Дополнительные сведения см. в разделе [tooAzure приложений ASP.NET, развертывание веб-сайтов](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Дополнительные сведения о средствах командной строки см. в разделе hello следующих ресурсов:

* [Простые веб-приложения: развертывание](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Блог по Дэвид Эббо о средстве написал toomake его проще toouse веб-развертывания.
* [Средство веб-развертывания](http://technet.microsoft.com/library/dd568996). Официальной документации на сайте Microsoft TechNet hello. Выпущен, но по-прежнему toostart лучше всего.
* [Использование веб-развертывания](http://www.iis.net/learn/publish/using-web-deploy). Официальной документации на сайте Microsoft IIS.NET hello. Также выпущен но toostart лучше всего.
* [Веб-развертывание ASP.NET с помощью Visual Studio: развертывание с использованием командной строки](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild — hello построить механизм, используемый в Visual Studio, а также может использоваться из приложений web tooWeb приложения hello командной строки toodeploy. Этот учебник входит в серию учебных материалов, посвященных главным образом развертыванию в Visual Studio.

