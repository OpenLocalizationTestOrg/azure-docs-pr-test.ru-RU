---
title: "Клонирование веб-приложения с помощью портала Azure"
description: "Узнайте, как клонировать веб-приложения, создавая новые веб-приложения, с помощью портала Azure."
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
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="5def3-103">Клонирование приложений службы приложений Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5def3-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="5def3-104">Функция клонирования в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) позволяет легко клонировать существующие веб-приложения, чтобы создать новое приложение в другом или том же регионе.</span><span class="sxs-lookup"><span data-stu-id="5def3-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="5def3-105">Так пользователи смогут легко и быстро развернуть целый ряд приложений в различных регионах.</span><span class="sxs-lookup"><span data-stu-id="5def3-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="5def3-106">В настоящее время клонирование приложений поддерживается только в планах службы приложений уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="5def3-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="5def3-107">В новой функции действуют те же ограничения, что и в функции архивации веб-приложений (см. статью [Резервное копирование веб-приложений в службе приложений Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="5def3-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="5def3-108">Клонирование существующего приложения</span><span class="sxs-lookup"><span data-stu-id="5def3-108">Cloning an existing App</span></span>
<span data-ttu-id="5def3-109">Веб-приложение должно быть запущено в режиме **Премиум** , чтобы можно было создать его клон.</span><span class="sxs-lookup"><span data-stu-id="5def3-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="5def3-110">Откройте колонку вашего веб-приложения на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5def3-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="5def3-111">Щелкните **Средства**.</span><span class="sxs-lookup"><span data-stu-id="5def3-111">Click **Tools**.</span></span> <span data-ttu-id="5def3-112">Затем в колонке **Средства** щелкните **Клонировать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5def3-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="5def3-113">Если веб-приложение еще не запущено в режиме **Премиум** , появится сообщение со списком поддерживаемых режимов, позволяющих использовать клонирование.</span><span class="sxs-lookup"><span data-stu-id="5def3-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="5def3-114">На этом этапе можно выбрать параметр **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="5def3-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="5def3-115">В колонке **Clone App** (Клонирование приложения) введите имя нового веб-приложения, группу ресурсов и план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5def3-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="5def3-116">Также пользователь сможет выбрать, следует ли клонировать ряд параметров исходного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5def3-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="5def3-117">После нажатия кнопки **Создать** платформа начнет создание копии исходного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5def3-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="5def3-118">Клонирование существующего приложения в среду службы приложений</span><span class="sxs-lookup"><span data-stu-id="5def3-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="5def3-119">В колонке **Clone App** (Клонирование приложения) клиент сможет выбрать пул приложений в существующей среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5def3-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="5def3-120">Существующие ограничения</span><span class="sxs-lookup"><span data-stu-id="5def3-120">Current Restrictions</span></span>
<span data-ttu-id="5def3-121">В настоящее время эта функция доступна в режиме предварительной версии, и со временем ее возможности будут расширены. В текущей версии функции клонирования приложений на портале Azure существуют следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="5def3-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="5def3-122">Параметры диспетчера трафика Azure не клонируются.</span><span class="sxs-lookup"><span data-stu-id="5def3-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="5def3-123">Параметры автоматического масштабирования не клонируются</span><span class="sxs-lookup"><span data-stu-id="5def3-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="5def3-124">Параметры расписания резервного копирования не клонируются</span><span class="sxs-lookup"><span data-stu-id="5def3-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="5def3-125">Параметры виртуальных сетей не клонируются</span><span class="sxs-lookup"><span data-stu-id="5def3-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="5def3-126">App Insights не настраивается в целевом веб-приложении автоматически</span><span class="sxs-lookup"><span data-stu-id="5def3-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="5def3-127">Параметры простой авторизации не клонируются</span><span class="sxs-lookup"><span data-stu-id="5def3-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="5def3-128">Расширение Kudu не клонируется</span><span class="sxs-lookup"><span data-stu-id="5def3-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="5def3-129">Правила TiP не клонируются</span><span class="sxs-lookup"><span data-stu-id="5def3-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="5def3-130">Содержимое базы данных не клонируется.</span><span class="sxs-lookup"><span data-stu-id="5def3-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="5def3-131">Ссылки</span><span class="sxs-lookup"><span data-stu-id="5def3-131">References</span></span>
* [<span data-ttu-id="5def3-132">Клонирование веб-приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5def3-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="5def3-133">Резервное копирование веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="5def3-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="5def3-134">Создание среды службы приложения</span><span class="sxs-lookup"><span data-stu-id="5def3-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="5def3-135">Создание веб-приложения в среде служб приложений</span><span class="sxs-lookup"><span data-stu-id="5def3-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="5def3-136">Введение в среду службы приложения</span><span class="sxs-lookup"><span data-stu-id="5def3-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
