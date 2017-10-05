---
title: "Не храните конфиденциальные данные в пользовательских образах для Azure RemoteApp | Документация Майкрософт"
description: "Изучите рекомендации по хранению данных в пользовательских образах в Azure RemoteApp."
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
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="d3c9c-103">Не храните конфиденциальные данные в пользовательских образах</span><span class="sxs-lookup"><span data-stu-id="d3c9c-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d3c9c-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d3c9c-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="d3c9c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d3c9c-106">При размещении собственного приложения в Azure RemoteApp сначала нужно создать пользовательский образ.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="d3c9c-107">Мы используем его для создания экземпляров виртуальных машин, которые служат для предоставления приложений пользователям.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="d3c9c-108">Пользовательский образ должен содержать ТОЛЬКО приложения, но не конфиденциальные данные, которые могут быть утеряны, например базы данных SQL, файлы персонала или специальные файлы данных, такие как файлы QuickBooks компании.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="d3c9c-109">Все конфиденциальные данные должны храниться вне Azure RemoteApp на файловом сервере, в другой виртуальной машине Azure или в SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="d3c9c-110">В образе должно содержаться только приложение, которое подключается к источнику данных и представляет данные.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="d3c9c-111">Дополнительные сведения см. в статье [Требования к образам Azure RemoteApp](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="d3c9c-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="d3c9c-112">Чтобы понять, почему не следует хранить конфиденциальные данные в образах, следует разобраться в том, как работает Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="d3c9c-113">При создании или обновлении коллекции в фоновом режиме создается несколько клонов или копий образа.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="d3c9c-114">Все эти экземпляры виртуальной машины являются точными копиями пользовательского образа. Когда пользователи запускают приложения, они подключаются к одному из этих экземпляров.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="d3c9c-115">Однако пользователю не гарантируется подключение к одному и тому же экземпляру, но это и не важно, так как экземпляры являются непостоянными.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="d3c9c-116">Экземпляры виртуальной машины, в которой размещаются приложения, являются временными и могут уничтожаться или удаляться, например, при обновлении коллекции.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="d3c9c-117">После того как коллекция подготовлена и пользователи начинают подключаться к виртуальным машинам, данные пользователя защищены и становятся постоянными, так как они находятся в отдельном хранилище на виртуальном жестком диске, который мы называем [диском профиля пользователя](remoteapp-upd.md). Этот диск находится по пути c:\users\<профиль_пользователя>.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="d3c9c-118">При запуске приложения диск профиля пользователя подключается, и в операционной системе он представляется как профиль локального пользователя.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="d3c9c-119">Дополнительные сведения о сохранении данных и параметров пользователей в Azure RemoteApp см. [здесь](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="d3c9c-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="d3c9c-120">Примеры данных, которые не должны содержаться в образе:</span><span class="sxs-lookup"><span data-stu-id="d3c9c-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="d3c9c-121">общие данные, к которым получают доступ пользователи;</span><span class="sxs-lookup"><span data-stu-id="d3c9c-121">Shared data for users to access</span></span>
* <span data-ttu-id="d3c9c-122">база данных SQL или QuickBooks;</span><span class="sxs-lookup"><span data-stu-id="d3c9c-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="d3c9c-123">любые данные на диске D:\\</span><span class="sxs-lookup"><span data-stu-id="d3c9c-123">Any data in D:\\</span></span>

<span data-ttu-id="d3c9c-124">Примеры данных, которые могут содержаться в профиле по умолчанию, копируемом на каждый диск профиля пользователя:</span><span class="sxs-lookup"><span data-stu-id="d3c9c-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="d3c9c-125">файлы конфигурации отдельных пользователей;</span><span class="sxs-lookup"><span data-stu-id="d3c9c-125">Configuration files per user</span></span>
* <span data-ttu-id="d3c9c-126">сценарии, которые должны храниться на дисках профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="d3c9c-127">Ниже приведены основные моменты, которые следует помнить.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-127">Key points:</span></span>

* <span data-ttu-id="d3c9c-128">Никогда не сохраняйте конфиденциальные данные, которые могут быть утеряны, на создаваемом пользовательском образе.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="d3c9c-129">Конфиденциальные данные всегда должны находиться на отдельном файловом сервере, в отдельной виртуальной машине Azure в облаке вне экземпляров виртуальных машин, в которых размещаются приложения в Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d3c9c-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="d3c9c-130">Пользовательские данные хранятся на диске профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="d3c9c-130">User data is saved and persists in the user profile disk (UPD)</span></span>

