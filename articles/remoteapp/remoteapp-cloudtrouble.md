---
title: "RemoteApp облака aaaTroubleshoot коллекции — Создание | Документы Microsoft"
description: "Дополнительные сведения об удаленных приложений RemoteApp tootroubleshoot облачных сбои при создании коллекции"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="5f4fa-103">Устранение неполадок при создании облачных коллекций RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5f4fa-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5f4fa-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5f4fa-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5f4fa-106">Если возникают проблемы при создании облачной коллекции, просмотрите hello следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="5f4fa-107">Недопустимый образ</span><span class="sxs-lookup"><span data-stu-id="5f4fa-107">Your image is invalid</span></span>
<span data-ttu-id="5f4fa-108">При появлении сообщения, как «GoldImageInvalid», когда ожидается для Azure tooprovision вашей коллекции, это означает, что образ шаблона не соответствует hello [определенные требования изображения](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="5f4fa-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="5f4fa-109">Начинаем, читать их [требования](remoteapp-imagereqs.md), исправьте образ и повторите попытку коллекции toocreate.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="5f4fa-110">На портале управления Azure hello распространенных ошибок</span><span class="sxs-lookup"><span data-stu-id="5f4fa-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="5f4fa-111">Часто сбои облачных коллекций происходят при создании из-за того, что вы используете настраиваемые образы.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="5f4fa-112">Если вы используете коллекцию hello toocreate пользовательского образа появиться hello выше ошибки, проверьте hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5f4fa-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="5f4fa-113">Убедитесь, что для этого настраиваемого образа hello загруженный образ требованиям.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="5f4fa-114">Чаще всего hello распространенная проблема связана, что это изображение hello не является правильно обработанной командой Sysprep.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="5f4fa-115">Проверьте hello изображение может загружаться в Hyper-V или попробуйте создать ВМ IAAS непосредственно в вашей подписке Azure с помощью образа hello.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="5f4fa-116">В случае hello ВМ tooboot и не запускается, то обычно это означает, что не подготовлен этого настраиваемого образа hello.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="5f4fa-117">Убедитесь, что hello пользовательский образ был создан после hello как toocreate шаблон пользовательского образа для удаленных приложений RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5f4fa-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="5f4fa-118">При использовании одного из образов Microsoft hello, включенными в вашу подписку, попробуйте toocreate hello коллекции еще раз.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="5f4fa-119">Если hello проблема повторится, затем обратитесь в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="5f4fa-120">Если данная ошибка возникает это обычно означает, который был обновлен tooa Платная учетная запись, но вы пытаетесь toouse предоставленный Майкрософт образ, который действителен только при режиме пробной версии hello hello службы.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="5f4fa-121">В этом случае попробуйте toocreate вашей облачной коллекции еще раз, но будет убедиться, что toospecify hello нужного образа.</span><span class="sxs-lookup"><span data-stu-id="5f4fa-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

