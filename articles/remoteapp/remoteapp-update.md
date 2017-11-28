---
title: "aaaUpdate вашей коллекции Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooupdate вашей коллекции Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="f0808-103">Обновление коллекции в Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f0808-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f0808-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="f0808-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f0808-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="f0808-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f0808-106">Придет время, неизбежно, при необходимости приложения hello tooupdate или image в вашей коллекции Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f0808-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="f0808-107">При использовании одного из образов hello, включенными в вашу подписку Azure RemoteApp, в облачной или гибридной коллекции, все обновления обрабатываются Azure RemoteApp, поэтому просто поместите.</span><span class="sxs-lookup"><span data-stu-id="f0808-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="f0808-108">Однако при использовании пользовательского изображения (построенная нуля или создания путем изменения одного из наших образов), вы отвечаете за обслуживание образа hello и приложений.</span><span class="sxs-lookup"><span data-stu-id="f0808-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="f0808-109">Если требуется tooupdate, изображения или любого приложения hello внутри него, необходимо toocreate новой, обновленной версии hello образа, а затем заменить hello существующий образ в коллекции с помощью этого нового образа обновленный.</span><span class="sxs-lookup"><span data-stu-id="f0808-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="f0808-110">Как же обновляется коллекция?</span><span class="sxs-lookup"><span data-stu-id="f0808-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="f0808-111">Очень просто.</span><span class="sxs-lookup"><span data-stu-id="f0808-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="f0808-112">Обновите образ hello, используемых в коллекции.</span><span class="sxs-lookup"><span data-stu-id="f0808-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="f0808-113">Примените к нему все необходимые исправления и обновления и сохраните под новым именем.</span><span class="sxs-lookup"><span data-stu-id="f0808-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="f0808-114">[Отправка](remoteapp-uploadimage.md) или [импорта](remoteapp-image-on-azurevm.md) tooRemoteApp этого образа.</span><span class="sxs-lookup"><span data-stu-id="f0808-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="f0808-115">Теперь на странице приветствия коллекции, нажмите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="f0808-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="f0808-116">Выберите новый образ hello hello **образ шаблона** списка.</span><span class="sxs-lookup"><span data-stu-id="f0808-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="f0808-117">Вот hello сложностью — нужно toodecide как toodeal пользователям, которые используют в настоящее время приложение в коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="f0808-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="f0808-118">Возможны следующие варианты hello.</span><span class="sxs-lookup"><span data-stu-id="f0808-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="f0808-119">**Предоставьте пользователям 60 минут после обновления hello**.</span><span class="sxs-lookup"><span data-stu-id="f0808-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="f0808-120">Сразу же после завершения обновления hello Azure RemoteApp отобразит сообщение tooany активных пользователей с просьбой toosave журнала и работе off и войдите снова.</span><span class="sxs-lookup"><span data-stu-id="f0808-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="f0808-121">Через 60 минут сеансы всех активных пользователей, которые не вышли из системы, будут завершены автоматически.</span><span class="sxs-lookup"><span data-stu-id="f0808-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="f0808-122">После этого пользователи смогут сразу войти в систему снова.</span><span class="sxs-lookup"><span data-stu-id="f0808-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="f0808-123">**Завершить сеансы пользователей незамедлительно**.</span><span class="sxs-lookup"><span data-stu-id="f0808-123">**Sign users out immediately**.</span></span> <span data-ttu-id="f0808-124">Сразу после завершения обновления hello, отключите всех пользователей автоматически без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="f0808-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="f0808-125">При выборе этого параметра пользователи могут потерять данные.</span><span class="sxs-lookup"><span data-stu-id="f0808-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="f0808-126">Тем не менее они могут повторно подключиться toohello приложение немедленно.</span><span class="sxs-lookup"><span data-stu-id="f0808-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="f0808-127">Нажмите кнопку Обновить hello toostart флажок hello.</span><span class="sxs-lookup"><span data-stu-id="f0808-127">Click hello check mark toostart hello update.</span></span>

