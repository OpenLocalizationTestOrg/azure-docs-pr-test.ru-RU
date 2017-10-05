---
title: "Публикация приложения в Azure RemoteApp | Документация Майкрософт"
description: "Узнайте, как публиковать приложения и ресурсы в Azure RemoteApp."
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
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="b5658-103">Публикация приложения в RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b5658-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b5658-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="b5658-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b5658-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="b5658-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b5658-106">После создания коллекции RemoteApp необходимо опубликовать приложения или ресурсы, которые должны быть доступны пользователям.</span><span class="sxs-lookup"><span data-stu-id="b5658-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="b5658-107">Образы шаблонов, входящие в подписку, по умолчанию содержат только некоторые приложения. Чтобы открыть доступ к другим приложениям, их необходимо опубликовать.</span><span class="sxs-lookup"><span data-stu-id="b5658-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="b5658-108">Если вы хотите обновить приложение,</span><span class="sxs-lookup"><span data-stu-id="b5658-108">Do you need to update an app?</span></span> <span data-ttu-id="b5658-109">сначала [обновите образ](remoteapp-update.md).</span><span class="sxs-lookup"><span data-stu-id="b5658-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="b5658-110">На вкладке **Публикация** портала щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b5658-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="b5658-111">Вы можете добавить приложение из меню **Пуск** образа шаблона или указать путь, по которому оно установлено в образе.</span><span class="sxs-lookup"><span data-stu-id="b5658-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="b5658-112">При использовании меню **Пуск** выберите нужное приложение в списке.</span><span class="sxs-lookup"><span data-stu-id="b5658-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="b5658-113">Если указывается путь к приложению, введите его имя и путь.</span><span class="sxs-lookup"><span data-stu-id="b5658-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="b5658-114">Используйте в пути переменные, например "%systemdrive%" вместо "c:\\".</span><span class="sxs-lookup"><span data-stu-id="b5658-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="b5658-115">Если вы хотите добавить приложение из меню **Пуск**, необходимо заранее *добавить это приложение в меню **Пуск** в образе шаблона*.</span><span class="sxs-lookup"><span data-stu-id="b5658-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="b5658-116">В противном случае RemoteApp распознает только те приложения, которые *добавлены* в меню **Пуск**.</span><span class="sxs-lookup"><span data-stu-id="b5658-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="b5658-117">Чтобы ваше приложение было размещено в меню **Пуск**, поместите файл ярлыка (**.lnk**) в папку %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.</span><span class="sxs-lookup"><span data-stu-id="b5658-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="b5658-118">Если вы забыли добавить приложение в меню **Пуск** при создании шаблона, добавьте путь к приложению.</span><span class="sxs-lookup"><span data-stu-id="b5658-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="b5658-119">(или создайте образ шаблона заново, что потребует больше усилий).</span><span class="sxs-lookup"><span data-stu-id="b5658-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

