---
title: "aaaAdd tooAzure приложения Java веб-приложений служб приложений"
description: "Этом учебнике показано, как tooadd приложения или страницы tooyour экземпляр веб-приложениях Azure приложения службы, который уже настроен toouse Java."
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
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a><span data-ttu-id="a9b23-103">Добавить tooAzure приложения Java веб-приложений служб приложений</span><span class="sxs-lookup"><span data-stu-id="a9b23-103">Add a Java application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="a9b23-104">После инициализации веб-приложения Java в [службе приложений Azure] [ Azure App Service] как описано в статье [Создание веб-приложения Java в службе приложений Azure](web-sites-java-get-started.md), можно отправить приложение путем размещения Ваш WAR в hello **веб-приложений** папки.</span><span class="sxs-lookup"><span data-stu-id="a9b23-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in hello **webapps** folder.</span></span>

<span data-ttu-id="a9b23-105">Здравствуйте, toohello пути навигации **веб-приложений** папки зависит от настройки экземпляра веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="a9b23-105">hello navigation path toohello **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="a9b23-106">Если настройка веб-приложения с помощью hello Azure Marketplace, hello путь toohello **веб-приложений** папка находится в форме hello **d:\home\site\wwwroot\bin\application\_server\webapps**, где **приложения\_сервера** — hello имя сервера приложения hello в силе для конкретного экземпляра веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="a9b23-106">If you set up your web app by using hello Azure Marketplace, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is hello name of hello application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="a9b23-107">Если настройка веб-приложения с помощью hello Azure пользовательский Интерфейс конфигурации hello путь toohello **веб-приложений** папка находится в форме hello **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="a9b23-107">If you set up your web app by using hello Azure configuration UI, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="a9b23-108">Обратите внимание что tooupload управления источника можно использовать приложение или веб-страницы, включая [сценариев непрерывной интеграции](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a9b23-108">Note that you can use source control tooupload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="a9b23-109">FTP может также использоваться для загрузки приложения или веб-страниц. Дополнительные сведения о развертывании приложений через FTP см. в разделе [развертывание вашего приложения tooAzure службы приложений].</span><span class="sxs-lookup"><span data-stu-id="a9b23-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app tooAzure App Service].</span></span>

<span data-ttu-id="a9b23-110">Примечание для веб-приложений Tomcat: после отправки вашего WAR файл toohello **веб-приложений** папки, сервера приложений Tomcat hello обнаружит добавили его и автоматически загружает его.</span><span class="sxs-lookup"><span data-stu-id="a9b23-110">Note for Tomcat web apps: Once you've uploaded your WAR file toohello **webapps** folder, hello Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="a9b23-111">Обратите внимание, что при копировании файлов (кроме WAR-файлы) toohello КОРНЕВОЙ каталог сервера приложений hello будет toobe перезапуска перед использованием этих файлов.</span><span class="sxs-lookup"><span data-stu-id="a9b23-111">Note that if you copy files (other than WAR files) toohello ROOT directory, hello application server will need toobe restarted before those files are used.</span></span> <span data-ttu-id="a9b23-112">функция Hello автозагрузки (AutoLoad) для веб-приложений Tomcat Java hello, работающих в Azure основана на новый WAR-файл добавляется или новые файлы или каталоги добавляются toohello **веб-приложений** папки.</span><span class="sxs-lookup"><span data-stu-id="a9b23-112">hello autoload functionality for hello Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added toohello **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="a9b23-113">См. также</span><span class="sxs-lookup"><span data-stu-id="a9b23-113">See Also</span></span>
<span data-ttu-id="a9b23-114">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure].</span><span class="sxs-lookup"><span data-stu-id="a9b23-114">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

[<span data-ttu-id="a9b23-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="a9b23-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[развертывание вашего приложения tooAzure службы приложений]: ./web-sites-deploy.md
