---
title: "aaaNever конфиденциальных данных в хранилище на пользовательских образов для Azure RemoteApp | Документы Microsoft"
description: "Дополнительные сведения о hello рекомендации по хранению данных в пользовательских образов в Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="edb5f-103">Не храните конфиденциальные данные в пользовательских образах</span><span class="sxs-lookup"><span data-stu-id="edb5f-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="edb5f-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="edb5f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="edb5f-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="edb5f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="edb5f-106">При размещении приложения в Azure RemoteApp hello первым шагом является toocreate пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="edb5f-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="edb5f-107">Мы используем этот пользовательский образ toocreate экземпляров виртуальных Машин, обслуживающих приложений tooyour пользователей.</span><span class="sxs-lookup"><span data-stu-id="edb5f-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="edb5f-108">Hello пользовательский образ должен содержать только приложения и никогда не конфиденциальных данных, которые могут быть потеряны, например баз данных SQL, файлы персонала или файлах данных, таких как QuickBooks компании.</span><span class="sxs-lookup"><span data-stu-id="edb5f-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="edb5f-109">Все конфиденциальные данные находятся внешние tooAzure RemoteApp на файловый сервер с другой ВМ, или в SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="edb5f-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="edb5f-110">изображение Hello следует просто hello приложения, которое подключается toohello источника данных и представляет данные hello.</span><span class="sxs-lookup"><span data-stu-id="edb5f-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="edb5f-111">Дополнительные сведения см. в статье [Требования к образам Azure RemoteApp](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="edb5f-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="edb5f-112">Почему не следует хранить конфиденциальные данные toounderstand требуется toounderstand, как работает Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="edb5f-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="edb5f-113">При создании или обновлении коллекции, фоновом hello клоны нескольких копий hello изображения создаются.</span><span class="sxs-lookup"><span data-stu-id="edb5f-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="edb5f-114">Все эти экземпляры виртуальной Машины будут точные реплики hello пользовательского образа; Когда пользователи запускают приложения они являются подключенных tooone эти экземпляры виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="edb5f-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="edb5f-115">Но hello того же экземпляра не гарантируется и не имеет значения, поскольку они являются непостоянными.</span><span class="sxs-lookup"><span data-stu-id="edb5f-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="edb5f-116">Здравствуйте экземпляров виртуальных Машин, размещающих приложения hello, непостоянные и могут быть уничтожается или удалить зависимости, например, во время обновления коллекции.</span><span class="sxs-lookup"><span data-stu-id="edb5f-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="edb5f-117">После коллекция hello предоставляется пользователи начинают подключающегося toohello виртуальные машины, данные пользователя является постоянным и защищена, так как оно сохраняется в отдельном хранилище в VHD, который мы называем [диск профиля пользователя (UPD)](remoteapp-upd.md), являющееся hello профиля пользователя в c:\users\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="edb5f-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="edb5f-118">При запуске приложения hello UPD подключается и обрабатываются так же, как локальный профиль операционной системой hello.</span><span class="sxs-lookup"><span data-stu-id="edb5f-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="edb5f-119">Дополнительные сведения о сохранении данных и параметров пользователей в Azure RemoteApp см. [здесь](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="edb5f-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="edb5f-120">Пример данных, не должен находиться в hello образа:</span><span class="sxs-lookup"><span data-stu-id="edb5f-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="edb5f-121">Общие данные, tooaccess пользователей</span><span class="sxs-lookup"><span data-stu-id="edb5f-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="edb5f-122">база данных SQL или QuickBooks;</span><span class="sxs-lookup"><span data-stu-id="edb5f-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="edb5f-123">любые данные на диске D:\\</span><span class="sxs-lookup"><span data-stu-id="edb5f-123">Any data in D:\\</span></span>

<span data-ttu-id="edb5f-124">Пример данных, который может находиться в toobe профиль по умолчанию hello копируется в каждый пользователей UPD:</span><span class="sxs-lookup"><span data-stu-id="edb5f-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="edb5f-125">файлы конфигурации отдельных пользователей;</span><span class="sxs-lookup"><span data-stu-id="edb5f-125">Configuration files per user</span></span>
* <span data-ttu-id="edb5f-126">сценарии, которые должны храниться на дисках профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="edb5f-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="edb5f-127">Ниже приведены основные моменты, которые следует помнить.</span><span class="sxs-lookup"><span data-stu-id="edb5f-127">Key points:</span></span>

* <span data-ttu-id="edb5f-128">Никогда не храните конфиденциальные данные, которые может быть потеряна в hello образ при создании настраиваемого образа.</span><span class="sxs-lookup"><span data-stu-id="edb5f-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="edb5f-129">Конфиденциальные данные всегда должен находиться на отдельном файловом сервере, разделения ВМ, hello облака и экземпляры виртуальной Машины всегда внешних toohello размещение приложений в Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="edb5f-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="edb5f-130">Данные пользователя сохраняется и сохраняется в диск профиля пользователя hello (UPD)</span><span class="sxs-lookup"><span data-stu-id="edb5f-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

