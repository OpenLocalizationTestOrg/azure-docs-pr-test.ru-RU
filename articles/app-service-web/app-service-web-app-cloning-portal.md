---
title: "aaaWeb клонирования приложения с помощью портала Azure"
description: "Узнайте, как tooclone toonew вашего веб-приложения веб-приложений с помощью портала Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="29321-103">Клонирование приложений службы приложений Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="29321-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="29321-104">Hello клонирования в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) Здравствуйте, позволяет легко создать копию существующего веб-приложения только что созданный tooa приложения в другом регионе или в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="29321-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="29321-105">Это позволит клиентам toodeploy количество приложений в разных регионах быстро и легко.</span><span class="sxs-lookup"><span data-stu-id="29321-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="29321-106">В настоящее время клонирование приложений поддерживается только в планах службы приложений уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="29321-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="29321-107">новый компонент использует Hello hello же ограничения, как средство резервного копирования приложений Web, в разделе [резервное копирование веб-приложения в службе приложений Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="29321-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="29321-108">Клонирование существующего приложения</span><span class="sxs-lookup"><span data-stu-id="29321-108">Cloning an existing App</span></span>
<span data-ttu-id="29321-109">Hello веб-приложения должна быть запущена в hello **Premium** режим toocreate клон hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="29321-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="29321-110">В hello [портала Azure](https://portal.azure.com/), откройте колонку веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="29321-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="29321-111">Щелкните **Средства**.</span><span class="sxs-lookup"><span data-stu-id="29321-111">Click **Tools**.</span></span> <span data-ttu-id="29321-112">Затем в hello **средства** колонка, щелкните **клонирование приложений**.</span><span class="sxs-lookup"><span data-stu-id="29321-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="29321-113">Если веб-приложение hello уже не hello **Premium** режиме, вы получите сообщение, указывающее режимы hello поддерживается для клонирования приложения.</span><span class="sxs-lookup"><span data-stu-id="29321-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="29321-114">На этом этапе, что у вас есть hello параметр tooselect **обновление**.</span><span class="sxs-lookup"><span data-stu-id="29321-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="29321-115">В hello **клонирование приложений** колонки введите имя нового веб-приложения hello, группа ресурсов и план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="29321-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="29321-116">Также hello пользователь будет toochoose, может ли tooclone ряд параметров источника веб-приложения или нет.</span><span class="sxs-lookup"><span data-stu-id="29321-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="29321-117">После нажатия кнопки **создания** платформы hello начнет работать на Создание клона hello исходного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="29321-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="29321-118">Клонирование существующих приложений tooan среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="29321-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="29321-119">В hello **клонирование приложений** колонке hello клиента имеется параметр toochoose hello пул приложений в существующей среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="29321-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="29321-120">Существующие ограничения</span><span class="sxs-lookup"><span data-stu-id="29321-120">Current Restrictions</span></span>
<span data-ttu-id="29321-121">Эта функция в настоящее время находится в предварительной версии, новые возможности tooadd Корпорация Майкрософт работает со временем, hello после списка являются hello известные ограничения в текущей поддержки hello клонирования приложения на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="29321-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="29321-122">Параметры диспетчера трафика Azure не клонируются.</span><span class="sxs-lookup"><span data-stu-id="29321-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="29321-123">Параметры автоматического масштабирования не клонируются</span><span class="sxs-lookup"><span data-stu-id="29321-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="29321-124">Параметры расписания резервного копирования не клонируются</span><span class="sxs-lookup"><span data-stu-id="29321-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="29321-125">Параметры виртуальных сетей не клонируются</span><span class="sxs-lookup"><span data-stu-id="29321-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="29321-126">Подробные сведения о приложении не настраиваются автоматически на веб-приложения hello назначения</span><span class="sxs-lookup"><span data-stu-id="29321-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="29321-127">Параметры простой авторизации не клонируются</span><span class="sxs-lookup"><span data-stu-id="29321-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="29321-128">Расширение Kudu не клонируется</span><span class="sxs-lookup"><span data-stu-id="29321-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="29321-129">Правила TiP не клонируются</span><span class="sxs-lookup"><span data-stu-id="29321-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="29321-130">Содержимое базы данных не клонируется.</span><span class="sxs-lookup"><span data-stu-id="29321-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="29321-131">Ссылки</span><span class="sxs-lookup"><span data-stu-id="29321-131">References</span></span>
* [<span data-ttu-id="29321-132">Клонирование веб-приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="29321-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="29321-133">Резервное копирование веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="29321-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="29321-134">Как tooCreate среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="29321-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="29321-135">Создание веб-приложения в среде служб приложений</span><span class="sxs-lookup"><span data-stu-id="29321-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="29321-136">Введение tooApp среды службы</span><span class="sxs-lookup"><span data-stu-id="29321-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
