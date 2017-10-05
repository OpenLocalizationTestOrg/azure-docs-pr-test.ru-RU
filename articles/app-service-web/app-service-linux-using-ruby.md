---
title: "Использование Ruby в веб-приложении службы приложений Azure на платформе Linux | Документация Майкрософт"
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
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="e450a-104">Использование Ruby в веб-приложении на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="e450a-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="e450a-105">В последнем обновлении нашей серверной части мы добавили поддержку Ruby версии 2.3.</span><span class="sxs-lookup"><span data-stu-id="e450a-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="e450a-106">Настроив конфигурацию веб-приложения Linux, вы можете изменить стек приложений.</span><span class="sxs-lookup"><span data-stu-id="e450a-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="e450a-107">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="e450a-107">Using the Azure portal</span></span> ##

<span data-ttu-id="e450a-108">Из меню "Создать" на [портале Azure](https://portal.azure.com) вы можете создать веб-приложение на платформе Linux, выбрав "Интернет+мобильные устройства", как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="e450a-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![Начало создания веб-приложения на портале Azure][1]

<span data-ttu-id="e450a-110">После этого откроется колонка **Создание**, как показано на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="e450a-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![Колонка "Создание"][2]

1. <span data-ttu-id="e450a-112">Присвойте веб-приложению имя.</span><span class="sxs-lookup"><span data-stu-id="e450a-112">Give your web app a name.</span></span>
2. <span data-ttu-id="e450a-113">Выберите имеющуюся группу ресурсов или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="e450a-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="e450a-114">(Доступные регионы см. в [разделе с ограничениями](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="e450a-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="e450a-115">Выберите имеющийся план службы приложений Azure или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="e450a-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="e450a-116">(Заметки о плане службы приложений см. в [разделе с ограничениями](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="e450a-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="e450a-117">Выберите Ruby из списка встроенных стеков времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="e450a-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="e450a-118">После создания веб-приложения Ruby его можно развернуть с помощью Git или FTP.</span><span class="sxs-lookup"><span data-stu-id="e450a-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

<span data-ttu-id="e450a-119">Дополнительные сведения о создании приложения Ruby см. в [этом руководстве по началу работы](app-service-linux-ruby-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e450a-119">To learn more about creating a Ruby app, check the [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e450a-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e450a-120">Next steps</span></span>
* [<span data-ttu-id="e450a-121">Что такое веб-приложение на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="e450a-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="e450a-122">Развертывание локального репозитория Git в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e450a-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="e450a-123">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="e450a-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="e450a-124">Создание приложения Ruby с помощью веб-приложения на платформе Linux (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="e450a-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png