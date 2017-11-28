---
title: "aaaDeploy tooAzure вашего приложения службы приложений с помощью FTP/S | Документы Microsoft"
description: "Узнайте, как toodeploy tooAzure вашего приложения, приложение службы с помощью FTP или FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="2b378-103">Развертывание вашего приложения tooAzure службы приложений с помощью FTP/S</span><span class="sxs-lookup"><span data-stu-id="2b378-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="2b378-104">В этой статье показано, как toouse FTP или FTPS toodeploy вашего веб-приложения, внутреннего сервера мобильного приложения или приложения API слишком[службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="2b378-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="2b378-105">конечную точку FTP/S Hello для приложения уже активен.</span><span class="sxs-lookup"><span data-stu-id="2b378-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="2b378-106">Конфигурация не является развертывание FTP/S необходимые tooenable.</span><span class="sxs-lookup"><span data-stu-id="2b378-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b378-107">Мы выполняем постоянно tooimprove действия безопасности на платформе Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b378-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="2b378-108">В ходе этой работы планируется обновление веб-приложений в регионе "Центральная Германия" и "Северо-восточная Германия".</span><span class="sxs-lookup"><span data-stu-id="2b378-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="2b378-109">Во время этого веб-приложения отключение hello использование протокола обычный текст FTP для развертывания.</span><span class="sxs-lookup"><span data-stu-id="2b378-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="2b378-110">Рекомендации клиентов tooour — tooFTPS tooswitch для развертываний.</span><span class="sxs-lookup"><span data-stu-id="2b378-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="2b378-111">Не ожидается tooyour любой перебоев в работе службы во время этого обновления, который планируется для 9/5.</span><span class="sxs-lookup"><span data-stu-id="2b378-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="2b378-112">Благодарим за вашу помощь!</span><span class="sxs-lookup"><span data-stu-id="2b378-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="2b378-113">Шаг 1. Настройка учетных данных развертывания</span><span class="sxs-lookup"><span data-stu-id="2b378-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="2b378-114">сервер tooaccess hello FTP для приложения, необходимо сначала учетные данные развертывания.</span><span class="sxs-lookup"><span data-stu-id="2b378-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="2b378-115">tooset или Сброс учетных данных развертывания, см. раздел [учетные данные развертывания службы приложения Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="2b378-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="2b378-116">В этом учебнике показано hello использовать учетные данные уровня пользователя.</span><span class="sxs-lookup"><span data-stu-id="2b378-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="2b378-117">Шаг 2. Получение информации о подключении по FTP</span><span class="sxs-lookup"><span data-stu-id="2b378-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="2b378-118">В hello [портал Azure](https://portal.azure.com), откройте ваше приложение [колонки ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="2b378-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="2b378-119">Выберите **Обзор** в левом меню hello, затем запишите значения hello для **пользователя FTP или развертывание**, **имя узла FTP**, и **FTPS имя узла**.</span><span class="sxs-lookup"><span data-stu-id="2b378-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Информация о подключении по FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="2b378-121">Hello **пользователя FTP или развертывание** значение пользователя, отображаться по hello портал Azure, включая имя приложения hello в порядке tooprovide правильный контекст для hello FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="2b378-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="2b378-122">Можно найти hello же данные при выборе **свойства** в левом меню hello.</span><span class="sxs-lookup"><span data-stu-id="2b378-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="2b378-123">Кроме того пароль развертывания hello никогда не отображается.</span><span class="sxs-lookup"><span data-stu-id="2b378-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="2b378-124">Если вы забудете пароль развертывания, вернитесь слишком[шаг 1](#step1) и сбросить пароль развертывания.</span><span class="sxs-lookup"><span data-stu-id="2b378-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="2b378-125">Шаг 3: Развертывание файлов tooAzure</span><span class="sxs-lookup"><span data-stu-id="2b378-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="2b378-126">Из клиента FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)и т. д), используйте сведения о подключении hello собранные tooconnect tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="2b378-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="2b378-127">Скопировать файлы и их соответствующих структуры toohello [ **/сайт/wwwroot** каталога](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) в Azure (или hello **/сайта и wwwroot/App_Data и задания или** каталогом Веб-заданий).</span><span class="sxs-lookup"><span data-stu-id="2b378-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="2b378-128">Приложение hello tooverify URL-адрес приложения tooyour обзора выполняется правильно.</span><span class="sxs-lookup"><span data-stu-id="2b378-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="2b378-129">В отличие от [развертывания на основе Git](app-service-deploy-local-git.md), развертывание FTP не поддерживает следующие автоматизации развертывания hello:</span><span class="sxs-lookup"><span data-stu-id="2b378-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="2b378-130">восстановление зависимостей (например, в инструментах автоматизации NuGet, NPM, PIP и Composer);</span><span class="sxs-lookup"><span data-stu-id="2b378-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="2b378-131">компиляция двоичных файлов .NET;</span><span class="sxs-lookup"><span data-stu-id="2b378-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="2b378-132">создание файла Web.config (вот [пример для Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps)).</span><span class="sxs-lookup"><span data-stu-id="2b378-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="2b378-133">Необходимо вручную выполнить восстановление, сборку и создание этих необходимых файлов на локальном компьютере, а затем развернуть их вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="2b378-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2b378-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b378-134">Next steps</span></span>

<span data-ttu-id="2b378-135">Для более сложных сценариев развертывания, попробуйте [развертывание tooAzure с Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="2b378-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="2b378-136">Развертывание на основе Git tooAzure позволяет системе управления версиями, восстановление пакета, MSBuild и многое другое.</span><span class="sxs-lookup"><span data-stu-id="2b378-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="2b378-137">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2b378-137">More Resources</span></span>

* <span data-ttu-id="2b378-138">[Создание веб-приложения PHP-MySQL и его развертывание с помощью FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="2b378-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="2b378-139">Учетные данные развертывания службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="2b378-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
