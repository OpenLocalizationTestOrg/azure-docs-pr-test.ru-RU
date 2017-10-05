---
title: "Развертывание приложения в службе приложений Azure с помощью FTP/S | Документация Майкрософт"
description: "Узнайте, как развернуть приложение в службе приложений Azure с помощью FTP или FTPS."
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
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="1a1b9-103">Развертывание приложения в службе приложений Azure с помощью FTP или FTPS</span><span class="sxs-lookup"><span data-stu-id="1a1b9-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="1a1b9-104">В этой статье показано, как с помощью FTP или FTPS развернуть веб-приложение, серверную частью мобильного приложения или приложение API в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1a1b9-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="1a1b9-105">Конечная точка FTP или FTPS для приложения уже активна.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="1a1b9-106">Чтобы обеспечить развертывание через FTP или FTPS, не требуется никаких настроек.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a1b9-107">Мы постоянно работаем над улучшением безопасности платформы Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="1a1b9-108">В ходе этой работы планируется обновление веб-приложений в регионе "Центральная Германия" и "Северо-восточная Германия".</span><span class="sxs-lookup"><span data-stu-id="1a1b9-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="1a1b9-109">В это время веб-приложения не смогут использовать протокол FTP обычного текста для развертываний.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="1a1b9-110">Рекомендуем своим клиентам использовать для развертывания FTPS.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="1a1b9-111">Во время обновления, которое запланировано на 5 сентября, никаких нарушений в работе вашей службы не предвидится.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="1a1b9-112">Благодарим за вашу помощь!</span><span class="sxs-lookup"><span data-stu-id="1a1b9-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="1a1b9-113">Шаг 1. Настройка учетных данных развертывания</span><span class="sxs-lookup"><span data-stu-id="1a1b9-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="1a1b9-114">Для доступа вашего приложения к FTP-серверу необходимо сначала настроить учетные данные развертывания.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="1a1b9-115">Чтобы задать или сбросить учетные данные развертывания, изучите раздел [Учетные данные развертывания службы приложений Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="1a1b9-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="1a1b9-116">В этом руководстве демонстрируется использование учетных данных уровня пользователя.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="1a1b9-117">Шаг 2. Получение информации о подключении по FTP</span><span class="sxs-lookup"><span data-stu-id="1a1b9-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="1a1b9-118">Откройте [колонку ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources) приложения на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1a1b9-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="1a1b9-119">Выберите **Обзор** в левом меню и запишите значения **Пользователь FTP или развертывания**, **Имя узла FTP** и **Имя узла FTPS**.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Информация о подключении по FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="1a1b9-121">Значение параметра **Пользователь FTP или развертывания** отображается на портале Azure, включая имя приложения, чтобы обеспечить правильный контекст для FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="1a1b9-122">Эти же сведения можно отобразить, выбрав **Свойства** в левом меню.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="1a1b9-123">Кроме того, пароль развертывания никогда не отображается.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="1a1b9-124">Если вы забыли пароль развертывания, вернитесь к [шагу 1](#step1) и сбросьте его.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="1a1b9-125">Шаг 3. Развертывание файлов в Azure</span><span class="sxs-lookup"><span data-stu-id="1a1b9-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="1a1b9-126">Подключитесь к приложению из клиента FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client) и т. п.), используя полученные сведения.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="1a1b9-127">Скопируйте файлы и соответствующую им структуру каталогов в Azure в каталог [**/site/wwwroot**](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) (или в каталог веб-заданий **/site/wwwroot/App_Data/Jobs/**).</span><span class="sxs-lookup"><span data-stu-id="1a1b9-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="1a1b9-128">Перейдите по URL-адресу приложения, чтобы убедиться, что приложение работает правильно.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="1a1b9-129">В отличие от [развертываний на основе Git](app-service-deploy-local-git.md), развертывание по FTP не поддерживает следующие инструменты автоматизации развертывания:</span><span class="sxs-lookup"><span data-stu-id="1a1b9-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="1a1b9-130">восстановление зависимостей (например, в инструментах автоматизации NuGet, NPM, PIP и Composer);</span><span class="sxs-lookup"><span data-stu-id="1a1b9-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="1a1b9-131">компиляция двоичных файлов .NET;</span><span class="sxs-lookup"><span data-stu-id="1a1b9-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="1a1b9-132">создание файла Web.config (вот [пример для Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps)).</span><span class="sxs-lookup"><span data-stu-id="1a1b9-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="1a1b9-133">Необходимо вручную выполнить восстановление, сборку и создание этих необходимых файлов на локальном компьютере, а затем развернуть их вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="1a1b9-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a1b9-134">Next steps</span></span>

<span data-ttu-id="1a1b9-135">Чтобы изучить более сложные сценарии развертывания, ознакомьтесь с [развертыванием в Azure с помощью Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="1a1b9-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="1a1b9-136">Развертывание в Azure на основе Git обеспечивает систему управления версиями, восстановление пакета, MSBuild и многое другое.</span><span class="sxs-lookup"><span data-stu-id="1a1b9-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="1a1b9-137">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1a1b9-137">More Resources</span></span>

* <span data-ttu-id="1a1b9-138">[Создание веб-приложения PHP-MySQL и его развертывание с помощью FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="1a1b9-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="1a1b9-139">Учетные данные развертывания службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1a1b9-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
