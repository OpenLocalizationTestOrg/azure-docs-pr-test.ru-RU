---
title: "приложение в Azure RemoteApp aaaPublish | Документы Microsoft"
description: "Узнайте, как toopublish приложения и ресурсы в Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="6aa0d-103">Как toopublish приложения в удаленных приложений RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6aa0d-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6aa0d-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6aa0d-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6aa0d-106">После создания коллекции RemoteApp необходимо приложения hello toopublish или ресурсы необходимо toomake доступны для пользователей.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="6aa0d-107">Hello образы шаблонов, предоставленного с подпиской достаточно нескольких приложений публикации по умолчанию - tooshare hello другие приложения, необходимо toopublish их.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="6aa0d-108">Требуется tooupdate приложения?</span><span class="sxs-lookup"><span data-stu-id="6aa0d-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="6aa0d-109">Вам потребуется слишком[обновление образа hello](remoteapp-update.md) первой.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="6aa0d-110">На hello **публикации** hello портала, нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="6aa0d-111">Можно либо добавить приложение из образа шаблона **запустить** меню или укажите приложение hello hello путь toowhere устанавливается на образ шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="6aa0d-112">Если выбрать tooadd hello **запустить** меню, выберите из списка hello toopublish приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="6aa0d-113">Если приложение toohello tooprovide hello путь, введите имя для приложения hello и toohello приложение hello путь.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="6aa0d-114">Используйте переменные пути hello - например, «% systemdrive %» вместо «c:\".</span><span class="sxs-lookup"><span data-stu-id="6aa0d-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="6aa0d-115">Если требуется tooadd приложения hello **запустить** меню, необходимо toohave *добавлены toohello этого приложения **запустить** меню образ шаблона.*</span><span class="sxs-lookup"><span data-stu-id="6aa0d-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="6aa0d-116">В противном случае RemoteApp будет доступна только в том, что *—* на hello **запустить** меню и будет спутать.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="6aa0d-117">toomake убедиться, что приложение установлено в hello **запустить** меню, поместите файл ярлыка - **.lnk** — в папке Menu\Programs %systemdrive%\ProgramData\Microsoft\Windows\Start hello.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="6aa0d-118">Если вы забыли toohello приложения hello tooadd **запустить** меню при создании шаблона hello, выберите приложение toohello tooadd hello пути.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="6aa0d-119">(или создайте образ шаблона заново, что потребует больше усилий).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

