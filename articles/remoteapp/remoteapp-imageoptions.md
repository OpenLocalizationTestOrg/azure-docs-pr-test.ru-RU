---
title: "изображение Azure RemoteApp aaaCreate | Документы Microsoft"
description: "Дополнительные сведения о параметрах hello, доступные для создания образов для Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="39f9d-103">Создание образа Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="39f9d-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="39f9d-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="39f9d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="39f9d-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="39f9d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="39f9d-106">Azure RemoteApp использует приложения hello toohold изображения, используемые совместно с пользователями.</span><span class="sxs-lookup"><span data-stu-id="39f9d-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="39f9d-107">(Мы получить изображение и использовать его виртуальных машин toocreate -, вот что hello доступ при входе в Azure RemoteApp.) toocreate коллекцию Azure RemoteApp с выбор приложений облачной или гибридной, сначала нужно создать изображение с этими приложениями, которые установлены.</span><span class="sxs-lookup"><span data-stu-id="39f9d-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="39f9d-108">Создайте коллекцию, которая использует этот образ, назначить пользователей toohello коллекции и публикации приложений toothose пользователей.</span><span class="sxs-lookup"><span data-stu-id="39f9d-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="39f9d-109">Создавать и использовать образы можно различными способами.</span><span class="sxs-lookup"><span data-stu-id="39f9d-109">You have several options for creating or using images.</span></span> <span data-ttu-id="39f9d-110">Hello basic [требование](remoteapp-imagereqs.md) для изображения является ОС Windows Server 2012 R2 и установлена роль узла сеансов удаленных рабочих столов (RDSH) hello.</span><span class="sxs-lookup"><span data-stu-id="39f9d-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="39f9d-111">Выполнение этого требования стоит рассмотреть подробнее.</span><span class="sxs-lookup"><span data-stu-id="39f9d-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="39f9d-112">Имеются следующие параметры, когда речь заходит tooimages hello.</span><span class="sxs-lookup"><span data-stu-id="39f9d-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="39f9d-113">Можно импортировать и использовать [образ на базе виртуальной машины Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="39f9d-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="39f9d-114">Это хороший вариант для бизнес-приложений, для которых нужно настраивать собственные параметры.</span><span class="sxs-lookup"><span data-stu-id="39f9d-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="39f9d-115">Вы можете настроить hello toowork изображения для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="39f9d-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="39f9d-116">Можно [создать и отправить собственный образ](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="39f9d-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="39f9d-117">Этот вариант подходит для ситуации, когда у вас уже есть образ, который вы используете в локальном развертывании служб удаленных рабочих столов.</span><span class="sxs-lookup"><span data-stu-id="39f9d-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="39f9d-118">Можно использовать один из hello [образы шаблонов](remoteapp-images.md) подписаны RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="39f9d-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="39f9d-119">Эти изображения создаются и обслуживается сотрудникам RemoteApp hello и содержать некоторые стандартные приложения (например, пакет Office hello), которые можно сделать доступными tooyour пользователей.</span><span class="sxs-lookup"><span data-stu-id="39f9d-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="39f9d-120">Обратите внимание, что только hello Office 365 Профессиональная, а также образ можно использовать в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="39f9d-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="39f9d-121">Независимо от того, где получить изображение или как создать, будет необходимо убедиться, что вы понимаете hello toomake [требований приложений](remoteapp-appreqs.md) tooensure приложения хорошо работает в удаленных приложений RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="39f9d-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="39f9d-122">Затем hello следующим шагом является toocreate [облака](remoteapp-create-cloud-deployment.md) или [гибридных](remoteapp-create-hybrid-deployment.md) коллекции.</span><span class="sxs-lookup"><span data-stu-id="39f9d-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

