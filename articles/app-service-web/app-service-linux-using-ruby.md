---
title: "aaaUsing Ruby в Azure приложение службы веб-приложения на платформе Linux | Документы Microsoft"
description: "Использование Ruby в веб-приложении службы приложений Azure на платформе Linux."
keywords: "Служба приложений Azure, веб-приложение, вопросы и ответы, Linux, OSS, Ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="f228c-104">Использование Ruby в веб-приложении на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="f228c-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="f228c-105">С hello последние обновления tooour серверной части мы появилась поддержка Ruby v.2.3.</span><span class="sxs-lookup"><span data-stu-id="f228c-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="f228c-106">Параметр конфигурации hello веб-приложения Linux можно изменить стека приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f228c-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="f228c-107">С помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="f228c-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="f228c-108">Новое меню hello в hello [портал Azure](https://portal.azure.com), вы можете toocreate веб-приложения на платформе Linux с hello Web + мобильный телефон как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="f228c-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Приступить к созданию веб-приложения на hello портал Azure][1]

<span data-ttu-id="f228c-110">Здравствуйте, затем **создать колонки** открывается, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="f228c-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![Создать колонки Hello][2]

1. <span data-ttu-id="f228c-112">Присвойте веб-приложению имя.</span><span class="sxs-lookup"><span data-stu-id="f228c-112">Give your web app a name.</span></span>
2. <span data-ttu-id="f228c-113">Выберите имеющуюся группу ресурсов или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="f228c-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="f228c-114">(См. доступных регионов в hello [разделе "ограничения"](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="f228c-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="f228c-115">Выберите имеющийся план службы приложений Azure или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="f228c-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="f228c-116">(См. примечания плана служб приложений в hello [разделе "ограничения"](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="f228c-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="f228c-117">Выберите hello Ruby стеки hello встроенных среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="f228c-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="f228c-118">После создания Ruby веб-приложение получает можно развернуть tooit с использованием Git или FTP.</span><span class="sxs-lookup"><span data-stu-id="f228c-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="f228c-119">toolearn Дополнительные сведения о создании приложений Ruby, проверьте hello [get руководство для начинающих](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="f228c-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f228c-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f228c-120">Next steps</span></span>
* [<span data-ttu-id="f228c-121">Что такое веб-приложение на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="f228c-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="f228c-122">Локальные развертывания Git tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="f228c-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="f228c-123">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="f228c-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="f228c-124">Создание приложения Ruby с помощью веб-приложения на платформе Linux (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="f228c-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png