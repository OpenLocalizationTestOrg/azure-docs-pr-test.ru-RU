---
title: "aaaApp требования для Azure RemoteApp | Документы Microsoft"
description: "Дополнительные сведения о hello требования для приложений, которые должны toouse в Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a><span data-ttu-id="76c3b-103">Требования к приложениям</span><span class="sxs-lookup"><span data-stu-id="76c3b-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="76c3b-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="76c3b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="76c3b-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="76c3b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="76c3b-106">Azure RemoteApp поддерживает потоковую передачу 32-разрядных или 64-разрядных приложений Windows из образа Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="76c3b-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="76c3b-107">Большинство существующих 32-разрядных или 64-разрядных приложений Windows выполняются "как есть" в среде Azure RemoteApp (службы удаленных рабочих столов, прежнее название — службы терминалов).</span><span class="sxs-lookup"><span data-stu-id="76c3b-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="76c3b-108">Однако есть разница между выполнением и правильной работой: некоторые приложения работают правильно, тогда как другие — нет.</span><span class="sxs-lookup"><span data-stu-id="76c3b-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="76c3b-109">Hello следующую информацию предоставляет рекомендации по разработке приложений в среде служб удаленных рабочих столов и проверке совместимости tooensure.</span><span class="sxs-lookup"><span data-stu-id="76c3b-109">hello following information provides guidance for developing applications in a Remote Desktop Services environment and testing tooensure compatibility.</span></span>

<span data-ttu-id="76c3b-110">Подсказка. Мы работаем над созданием рабочих примеров приложений.</span><span class="sxs-lookup"><span data-stu-id="76c3b-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="76c3b-111">Появятся новые разделы, посвященные использованию Microsoft Access, QuickBooks и App-V в RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="76c3b-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="76c3b-112">Требования</span><span class="sxs-lookup"><span data-stu-id="76c3b-112">Requirements</span></span>
<span data-ttu-id="76c3b-113">При выполнении этих трех требований приложение будет правильно работать в RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="76c3b-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="76c3b-114">Приложения, которые отвечают всем [требованиям сертификации для классических приложений Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) и соответствуют слишком[рекомендации по программированию служб удаленных рабочих столов](https://msdn.microsoft.com/library/aa383490.aspx) будет иметь полной совместимости с RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="76c3b-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere too[Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="76c3b-115">Приложения никогда не следует хранить данные локально на изображение hello или экземпляры RemoteApp, которые могут быть потеряны.</span><span class="sxs-lookup"><span data-stu-id="76c3b-115">Applications should never store data locally on hello image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="76c3b-116">После создания коллекции RemoteApp, экземпляры hello клонируются и не имеют состояния и должно содержать только приложения.</span><span class="sxs-lookup"><span data-stu-id="76c3b-116">After you create a RemoteApp collection, hello instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="76c3b-117">Хранить данные из внешнего источника, или в профиле пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="76c3b-117">Store data in an external source or within hello user's profile.</span></span>
3. <span data-ttu-id="76c3b-118">Пользовательские образы не должны содержать данные, которые могут быть потеряны.</span><span class="sxs-lookup"><span data-stu-id="76c3b-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="76c3b-119">Тестирование приложений</span><span class="sxs-lookup"><span data-stu-id="76c3b-119">Testing your apps</span></span>
<span data-ttu-id="76c3b-120">Используйте эти приложения tootesting действия:</span><span class="sxs-lookup"><span data-stu-id="76c3b-120">Use these steps tootesting applications:</span></span>

1. <span data-ttu-id="76c3b-121">Установите Windows Server 2012 R2 и свое приложение.</span><span class="sxs-lookup"><span data-stu-id="76c3b-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="76c3b-122">Включите удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="76c3b-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="76c3b-123">Создайте две учетные записи пользователя а и пользователь б, добавление и группа безопасности учетных записей toohello пользователя удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="76c3b-123">Create two user accounts, UserA and UserB, adding both user accounts toohello Remote Desktop security group.</span></span>
4. <span data-ttu-id="76c3b-124">Проверка совместимости нескольких сеансов путем создания двух одновременных toohello сеансы служб удаленных рабочих СТОЛОВ ПК при запуске приложения hello.</span><span class="sxs-lookup"><span data-stu-id="76c3b-124">Check multi-session compatibility by establishing two simultaneous RDS sessions toohello PC while launching hello application.</span></span>
5. <span data-ttu-id="76c3b-125">Проверьте поведение приложения.</span><span class="sxs-lookup"><span data-stu-id="76c3b-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="76c3b-126">Рекомендации по разработке приложения</span><span class="sxs-lookup"><span data-stu-id="76c3b-126">Application development guidelines</span></span>
<span data-ttu-id="76c3b-127">Используйте hello следовать рекомендациям по разработке приложений для удаленных приложений RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="76c3b-127">Use hello following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="76c3b-128">Несколько пользователей</span><span class="sxs-lookup"><span data-stu-id="76c3b-128">Multiple users</span></span>
* <span data-ttu-id="76c3b-129">При установке [приложения для одного пользователя ](https://msdn.microsoft.com/library/aa380661.aspx)могут возникнуть проблемы в многопользовательской среде.</span><span class="sxs-lookup"><span data-stu-id="76c3b-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="76c3b-130">Приложения должны [хранить сведения о пользователе](https://msdn.microsoft.com/library/aa383452.aspx) в местах конкретного пользователя, независимо от общих сведений, применяет tooall пользователей.</span><span class="sxs-lookup"><span data-stu-id="76c3b-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies tooall users.</span></span>
* <span data-ttu-id="76c3b-131">RemoteApp использует [несколько пространств имен для объектов ядра](https://msdn.microsoft.com/library/aa382954.aspx); глобальное пространство имен используется в основном службами в клиентских или серверных приложениях.</span><span class="sxs-lookup"><span data-stu-id="76c3b-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="76c3b-132">Не является безопасным tooassume, hello имя компьютера или hello [IP-адрес](https://msdn.microsoft.com/library/aa382942.aspx) назначенного toohello компьютера связаны с одним пользователем, так как несколько пользователей могут войти в систему одновременно tooa узла сеансов удаленных рабочих столов (сеансов удаленных рабочих Столов На сервере узла).</span><span class="sxs-lookup"><span data-stu-id="76c3b-132">It is not safe tooassume that hello computer name or hello [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned toohello computer are associated with a single user because multiple users can be logged on simultaneously tooa Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="76c3b-133">Производительность</span><span class="sxs-lookup"><span data-stu-id="76c3b-133">Performance</span></span>
* <span data-ttu-id="76c3b-134">Отключить [графические эффекты](https://msdn.microsoft.com/library/aa380822.aspx) перед добавлением tooRemoteApp вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="76c3b-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app tooRemoteApp.</span></span>
* <span data-ttu-id="76c3b-135">доступность toomaximize ЦП для всех пользователей, либо отключить [фоновых задач ](https://msdn.microsoft.com/library/aa380665.aspx) или создать эффективный фоновые задачи, которые не требуется много ресурсов.</span><span class="sxs-lookup"><span data-stu-id="76c3b-135">toomaximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="76c3b-136">Следует настроить [использование потока](https://msdn.microsoft.com/library/aa383520.aspx) приложения для многопользовательской и многопроцессорной среды.</span><span class="sxs-lookup"><span data-stu-id="76c3b-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="76c3b-137">toooptimize производительность, рекомендуется для приложений слишком[обнаружить](https://msdn.microsoft.com/library/aa380798.aspx) , запущены ли они в сеансе клиента.</span><span class="sxs-lookup"><span data-stu-id="76c3b-137">toooptimize performance, it is good practice for applications too[detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

