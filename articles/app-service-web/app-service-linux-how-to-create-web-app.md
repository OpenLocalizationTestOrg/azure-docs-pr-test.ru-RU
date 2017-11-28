---
title: "aaaCreate Azure веб-приложение, работающее на платформе Linux | Документы Microsoft"
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
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="07f68-104">Создание веб-приложения Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="07f68-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="07f68-105">Использовать hello Azure портала toocreate веб-приложения</span><span class="sxs-lookup"><span data-stu-id="07f68-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="07f68-106">Вы можете начать создание веб-приложения на платформе Linux из hello [портал Azure](https://portal.azure.com) как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="07f68-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![Приступить к созданию веб-приложения на hello портал Azure][1]

<span data-ttu-id="07f68-108">Здравствуйте, затем **создать колонки** открывается, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="07f68-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![Создать колонки Hello][2]

1. <span data-ttu-id="07f68-110">Присвойте веб-приложению имя.</span><span class="sxs-lookup"><span data-stu-id="07f68-110">Give your web app a name.</span></span>
2. <span data-ttu-id="07f68-111">Выберите имеющуюся группу ресурсов или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="07f68-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="07f68-112">(См. доступных регионов в hello [разделе "ограничения"](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="07f68-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="07f68-113">Выберите имеющийся план службы приложений Azure или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="07f68-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="07f68-114">(См. примечания плана служб приложений в hello [разделе "ограничения"](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="07f68-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="07f68-115">Выберите приложение hello, следует присвоить toouse стека.</span><span class="sxs-lookup"><span data-stu-id="07f68-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="07f68-116">На выбор предоставляется несколько версий Node.js, PHP, .NET Core и Ruby.</span><span class="sxs-lookup"><span data-stu-id="07f68-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="07f68-117">После создания приложения hello, можно изменить стека приложения hello из параметров приложения hello, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="07f68-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![Параметры приложения][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="07f68-119">Развертывание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="07f68-119">Deploy your web app</span></span>
<span data-ttu-id="07f68-120">Выбор **варианты развертывания** из портала дает hello управления вы hello параметр toouse локальный Git и GitHub репозитория toodeploy приложения.</span><span class="sxs-lookup"><span data-stu-id="07f68-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="07f68-121">rest Hello hello инструкций, аналогичные toothose для веб-приложения не Linux.</span><span class="sxs-lookup"><span data-stu-id="07f68-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="07f68-122">Инструкции hello в [локальное развертывание Git](app-service-deploy-local-git.md) или [непрерывного развертывания](app-service-continuous-deployment.md) toodeploy приложения.</span><span class="sxs-lookup"><span data-stu-id="07f68-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="07f68-123">Также можно использовать FTP tooupload tooyour узла приложения.</span><span class="sxs-lookup"><span data-stu-id="07f68-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="07f68-124">Можно получить конечную точку FTP hello веб-приложения из системы диагностики hello разделе журналы как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="07f68-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![Раздел "Журналы диагностики"][4]

## <a name="next-steps"></a><span data-ttu-id="07f68-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07f68-126">Next steps</span></span>
* [<span data-ttu-id="07f68-127">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="07f68-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="07f68-128">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="07f68-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="07f68-129">Использование Ruby в веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="07f68-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="07f68-130">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="07f68-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
