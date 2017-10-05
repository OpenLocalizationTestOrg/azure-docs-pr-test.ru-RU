---
title: "Создание веб-приложения Azure на платформе Linux | Документация Майкрософт"
description: "Рабочий процесс создания веб-приложения для веб-приложения Azure на платформе Linux."
keywords: "служба приложений azure, веб-приложение, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="b07c7-104">Создание веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="b07c7-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="b07c7-105">Создание веб-приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="b07c7-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="b07c7-106">Чтобы приступить к созданию собственного веб-приложения в Linux на [портале Azure](https://portal.azure.com), выполните действия, как показано на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="b07c7-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Начало создания веб-приложения на портале Azure][1]

<span data-ttu-id="b07c7-108">После этого откроется колонка **Создание**, как показано на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="b07c7-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![Колонка "Создание"][2]

1. <span data-ttu-id="b07c7-110">Присвойте веб-приложению имя.</span><span class="sxs-lookup"><span data-stu-id="b07c7-110">Give your web app a name.</span></span>
2. <span data-ttu-id="b07c7-111">Выберите имеющуюся группу ресурсов или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="b07c7-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="b07c7-112">(Доступные регионы см. в [разделе с ограничениями](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="b07c7-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="b07c7-113">Выберите имеющийся план службы приложений Azure или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="b07c7-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="b07c7-114">(Заметки о плане службы приложений см. в [разделе с ограничениями](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="b07c7-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="b07c7-115">Выберите необходимый стек приложений.</span><span class="sxs-lookup"><span data-stu-id="b07c7-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="b07c7-116">На выбор предоставляется несколько версий Node.js, PHP, .NET Core и Ruby.</span><span class="sxs-lookup"><span data-stu-id="b07c7-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="b07c7-117">После создания приложения стек можно изменить в настройках, как показано на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="b07c7-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Параметры приложения][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="b07c7-119">Развертывание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="b07c7-119">Deploy your web app</span></span>
<span data-ttu-id="b07c7-120">Выберите один из доступных **вариантов развертывания** на портале управления: развертывание с использованием локального репозитория Git или развертывание с использованием репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="b07c7-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="b07c7-121">Остальная часть инструкций аналогична указаниям для веб-приложений не на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="b07c7-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="b07c7-122">Чтобы развернуть приложение, вы можете следовать указаниям по [локальному развертыванию Git](app-service-deploy-local-git.md) или [непрерывному развертыванию](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="b07c7-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="b07c7-123">Чтобы передать свое приложение на сайт, можно использовать протокол FTP.</span><span class="sxs-lookup"><span data-stu-id="b07c7-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="b07c7-124">Конечную точку FTP для веб-приложения можно получить в разделе "Журналы диагностики", как показано на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="b07c7-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Раздел "Журналы диагностики"][4]

## <a name="next-steps"></a><span data-ttu-id="b07c7-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b07c7-126">Next steps</span></span>
* [<span data-ttu-id="b07c7-127">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="b07c7-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="b07c7-128">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="b07c7-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="b07c7-129">Использование Ruby в веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="b07c7-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="b07c7-130">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="b07c7-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
