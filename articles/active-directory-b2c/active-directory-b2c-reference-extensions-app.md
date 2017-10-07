---
title: "Приложения расширений Azure Active Directory B2C | Документация Майкрософт"
description: "Восстановление b2c-расширений приложение hello"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="1b041-103">Azure AD B2C: приложение расширений</span><span class="sxs-lookup"><span data-stu-id="1b041-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="1b041-104">Вызывается при создании каталога Azure AD B2C приложения `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` автоматически создается внутри нового каталога hello.</span><span class="sxs-lookup"><span data-stu-id="1b041-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="1b041-105">Этого приложения, который ссылается tooas hello **b2c расширения приложения**, отображается в *регистрации приложения*.</span><span class="sxs-lookup"><span data-stu-id="1b041-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="1b041-106">Он используется hello Azure AD B2C службы toostore сведения о пользователях и настраиваемых атрибутов.</span><span class="sxs-lookup"><span data-stu-id="1b041-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="1b041-107">При удалении приложения hello Azure AD B2C не будет работать правильно, и повлияет на рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="1b041-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b041-108">Не удаляется b2c-расширений приложение hello, если вы планируете удалить tooimmediately вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="1b041-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="1b041-109">Если приложение hello остается удаленные более 30 дней, сведения о пользователе будет безвозвратно потеряно.</span><span class="sxs-lookup"><span data-stu-id="1b041-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="1b041-110">Проверка того, приложение hello расширения присутствует</span><span class="sxs-lookup"><span data-stu-id="1b041-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="1b041-111">присутствует tooverify, hello b2c расширения приложения:</span><span class="sxs-lookup"><span data-stu-id="1b041-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="1b041-112">В клиенте Azure AD B2C щелкните **больше услуг** в меню навигации слева hello.</span><span class="sxs-lookup"><span data-stu-id="1b041-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="1b041-113">Найдите и откройте элемент **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="1b041-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="1b041-114">Найдите приложение, имя которого начинается с **b2c-extensions-app**</span><span class="sxs-lookup"><span data-stu-id="1b041-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="1b041-115">Восстановить приложение hello расширения</span><span class="sxs-lookup"><span data-stu-id="1b041-115">Recover hello extensions app</span></span>

<span data-ttu-id="1b041-116">Если вы случайно удалены b2c-расширений приложение hello, у вас есть 30 дней toorecover его.</span><span class="sxs-lookup"><span data-stu-id="1b041-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="1b041-117">Вы сможете восстановить приложения hello, с помощью Graph API hello.</span><span class="sxs-lookup"><span data-stu-id="1b041-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="1b041-118">Обзор слишком[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="1b041-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="1b041-119">Войдите в toohello сайта как глобальный администратор для каталога Azure AD B2C hello нужного приложения hello удален toorestore для.</span><span class="sxs-lookup"><span data-stu-id="1b041-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="1b041-120">Выдача HTTP GET к URL-адрес hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` с api-version = 1.6.</span><span class="sxs-lookup"><span data-stu-id="1b041-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="1b041-121">Убедитесь, что tooreplace `{tenantName}` на имя вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="1b041-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="1b041-122">Эта операция отображает список всех приложений hello, которые были удалены в течение hello за последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="1b041-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="1b041-123">Найдите приложение hello в списке hello, где hello имя начинается с «b2c расширение приложения» и скопируйте его `objectid` значение свойства.</span><span class="sxs-lookup"><span data-stu-id="1b041-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="1b041-124">Выдача HTTP POST от hello URL-адрес `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="1b041-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="1b041-125">Замените hello `{OBJECTID}` часть URL-адреса hello с hello `objectid` из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="1b041-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="1b041-126">Теперь можно будет слишком[разделе приложение hello восстановить](#verifying-that-the-extensions-app-is-present) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1b041-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="1b041-127">Приложение можно восстановить только в том случае, если он был удален в рамках hello последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="1b041-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="1b041-128">Если прошло более 30 дней, данные будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="1b041-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="1b041-129">Для получения дополнительной помощи отправьте запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="1b041-129">For more assistance, file a support ticket.</span></span>
