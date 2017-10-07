---
title: "aaaUsing App-V приложения Azure RemoteApp. | Документы Microsoft"
description: "Узнайте, как приложения toouse App-V в Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="faf86-103">Работа с приложением App-V в Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="faf86-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="faf86-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="faf86-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="faf86-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="faf86-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="faf86-106">Приложения App-V можно использовать в гибридной коллекции Azure RemoteApp, которая требует присоединения к домену.</span><span class="sxs-lookup"><span data-stu-id="faf86-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="faf86-107">Перед началом работы убедитесь, что клиент App-V 5.1 hello tooinstall с последними обновлениями hello.</span><span class="sxs-lookup"><span data-stu-id="faf86-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="faf86-108">Вам потребуется toocreate [пользовательского образа](remoteapp-create-custom-image.md) , включает клиент App-V hello.</span><span class="sxs-lookup"><span data-stu-id="faf86-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="faf86-109">Это легко toouse существующую инфраструктуру App-V с Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="faf86-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="faf86-110">Поскольку гибридной коллекции развернута в виртуальной сети Azure с контроллера домена tooyour доступ и виртуальные машины hello были присоединены к домену, можно использовать существующие App-v инфраструктуры и развертывания методы tooeasyily узла App-V приложения в Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="faf86-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="faf86-111">Ниже приведены некоторые соображения, которые следует учитывать на основе hello типа развертывания App-V, который в настоящий момент.</span><span class="sxs-lookup"><span data-stu-id="faf86-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="faf86-112">Варианты настройки</span><span class="sxs-lookup"><span data-stu-id="faf86-112">Configuration options</span></span> |  | <span data-ttu-id="faf86-113">Positive</span><span class="sxs-lookup"><span data-stu-id="faf86-113">Positive</span></span> | <span data-ttu-id="faf86-114">Negative</span><span class="sxs-lookup"><span data-stu-id="faf86-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="faf86-115">Метод доставки.</span><span class="sxs-lookup"><span data-stu-id="faf86-115">Delivery method</span></span> |<span data-ttu-id="faf86-116">Потоковая передача (по требованию).</span><span class="sxs-lookup"><span data-stu-id="faf86-116">Streaming (on-demand)</span></span> |<span data-ttu-id="faf86-117">Приложения всегда является hello последнюю и новая</span><span class="sxs-lookup"><span data-stu-id="faf86-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="faf86-118">Задержка при первом запуске.</span><span class="sxs-lookup"><span data-stu-id="faf86-118">First time latency</span></span> |
| <span data-ttu-id="faf86-119">Подключение.</span><span class="sxs-lookup"><span data-stu-id="faf86-119">Mounted</span></span> |<span data-ttu-id="faf86-120">Самый быстрый; приложение уже существует на hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="faf86-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="faf86-121">Раздувание: образ занимает место (ограничение — 127 ГБ).</span><span class="sxs-lookup"><span data-stu-id="faf86-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="faf86-122">Хранилище местонахождения приложения.</span><span class="sxs-lookup"><span data-stu-id="faf86-122">App location storage</span></span> |<span data-ttu-id="faf86-123">Общая папка.</span><span class="sxs-lookup"><span data-stu-id="faf86-123">Shared content</span></span> |<span data-ttu-id="faf86-124">Приложение запускается в памяти экземпляра Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="faf86-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="faf86-125">Требуют большого объема памяти и качество подключения сервера toostreaming (файл) где находится приложение hello</span><span class="sxs-lookup"><span data-stu-id="faf86-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="faf86-126">Диск (с кэшированием).</span><span class="sxs-lookup"><span data-stu-id="faf86-126">Disk (Cached)</span></span> |<span data-ttu-id="faf86-127">Быстрое выполнение.</span><span class="sxs-lookup"><span data-stu-id="faf86-127">Fast execution.</span></span> <span data-ttu-id="faf86-128">Приложение не зависит от доступности источника содержимого.</span><span class="sxs-lookup"><span data-stu-id="faf86-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="faf86-129">Раздувание: образ занимает место (ограничение — 127 ГБ).</span><span class="sxs-lookup"><span data-stu-id="faf86-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="faf86-130">Отслеживание.</span><span class="sxs-lookup"><span data-stu-id="faf86-130">Targeting</span></span> |<span data-ttu-id="faf86-131">Пользователь</span><span class="sxs-lookup"><span data-stu-id="faf86-131">User</span></span> |<span data-ttu-id="faf86-132">Требуется совершенно автономная инфраструктура App-V.</span><span class="sxs-lookup"><span data-stu-id="faf86-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="faf86-133">Глобально (машина).</span><span class="sxs-lookup"><span data-stu-id="faf86-133">Global (machine)</span></span> |<span data-ttu-id="faf86-134">Предварительная публикация или отслеживание с помощью сервера публикации.</span><span class="sxs-lookup"><span data-stu-id="faf86-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="faf86-135">Требуется tooupdate образ Azure, если вы хотите tooupdate приложение hello (огромный).</span><span class="sxs-lookup"><span data-stu-id="faf86-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="faf86-136">Занимает место в образе.</span><span class="sxs-lookup"><span data-stu-id="faf86-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="faf86-137">После создания настраиваемого образа и гибридной коллекции, публикации приложения, назначить пользователей и предоставляются существующие приложения App-V, размещенных в Azure RemoteApp, доставленных tooany устройства в любом месте.</span><span class="sxs-lookup"><span data-stu-id="faf86-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

