---
title: "Добавление приложения Java в веб-приложения службы приложений Azure"
description: "В этом учебнике показано, как добавить страницу или приложение в экземпляр веб-приложений службы приложений Azure, который уже настроен на использование Java."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="4b4fe-103">Добавление приложения Java в веб-приложения службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4b4fe-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="4b4fe-104">После инициализации веб-приложения в [службе приложений Azure][Azure App Service], как описано в статье [Создание веб-приложения Java в службе приложений Azure](web-sites-java-get-started.md), приложение можно передать, поместив WAR-файл в папку **webapps**.</span><span class="sxs-lookup"><span data-stu-id="4b4fe-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="4b4fe-105">Путь к папке **webapps** зависит от настроек экземпляра веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="4b4fe-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="4b4fe-106">Если веб-приложение настроено с использованием Azure Marketplace, то папка **webapps** находится по пути **d:\home\site\wwwroot\bin\сервер\_приложений\webapps**, где **сервер\_приложений** — имя сервера приложений в экземпляре веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="4b4fe-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="4b4fe-107">После настройки веб-приложения в пользовательском интерфейсе Azure путь к папке **webapps** будет иметь вид **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="4b4fe-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="4b4fe-108">Обратите внимание, что для отправки веб-страниц или приложения можно использовать систему управления версиями, в том числе в [сценариях непрерывной интеграции](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="4b4fe-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="4b4fe-109">FTP позволяет также передать приложение или веб-страницы. Дополнительные сведения о развертывании приложений посредством протокола FTP см. в разделе [Развертывание приложения в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="4b4fe-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="4b4fe-110">Примечание для веб-приложений Tomcat. Сразу после передачи WAR-файла в папку **webapps** сервер приложений Tomcat определит это и автоматически загрузит этот файл.</span><span class="sxs-lookup"><span data-stu-id="4b4fe-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="4b4fe-111">Обратите внимание, что при копировании файлов (кроме WAR-файлов) в КОРНЕВОЙ каталог необходимо перезапустить сервер приложений, прежде чем использовать эти файлы.</span><span class="sxs-lookup"><span data-stu-id="4b4fe-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="4b4fe-112">Работа функции автозагрузки для запущенных в Azure веб-приложений Java Tomcat основана на добавлении нового WAR-файла либо новых файлов или каталогов в папку **webapps**.</span><span class="sxs-lookup"><span data-stu-id="4b4fe-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="4b4fe-113">См. также</span><span class="sxs-lookup"><span data-stu-id="4b4fe-113">See Also</span></span>
<span data-ttu-id="4b4fe-114">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure].</span><span class="sxs-lookup"><span data-stu-id="4b4fe-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="4b4fe-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="4b4fe-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="4b4fe-116">[Центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="4b4fe-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="4b4fe-117">[Развертывание приложения в службе приложений Azure]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="4b4fe-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
