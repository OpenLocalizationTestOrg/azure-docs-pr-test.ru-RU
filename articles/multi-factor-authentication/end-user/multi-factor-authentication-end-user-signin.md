---
title: "Вход с помощью Azure MFA и двухфакторной проверки подлинности | Документация Майкрософт"
description: "На этой странице предоставлены рекомендации по использованию разных методов входа с помощью Azure MFA."
keywords: "проверка подлинности пользователя, вход в систему, вход с помощью мобильного телефона, вход с помощью рабочего телефона"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: d12115be61ca00dfb86dd822ccae9f9096fa796a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="bf997-104">Варианты входа с помощью многофакторной идентификации Azure</span><span class="sxs-lookup"><span data-stu-id="bf997-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="bf997-105">В этой статье рассматривается стандартная процедура входа.</span><span class="sxs-lookup"><span data-stu-id="bf997-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="bf997-106">Если у вас возникают проблемы со входом в систему см. статью [Проблемы с двухфакторной проверкой подлинности](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="bf997-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="bf997-107">Каким будет ваш вариант входа</span><span class="sxs-lookup"><span data-stu-id="bf997-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="bf997-108">Вариант входа отличается в зависимости от того, что выбрано в качестве второго фактора: телефонный звонок, приложение аутентификации или текстовое сообщение.</span><span class="sxs-lookup"><span data-stu-id="bf997-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="bf997-109">Ниже выберите вариант, который соответствует вашим действиям.</span><span class="sxs-lookup"><span data-stu-id="bf997-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="bf997-110">Как вы входите в учетную запись?</span><span class="sxs-lookup"><span data-stu-id="bf997-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="bf997-111">С помощью звонка на мобильный или рабочий телефон</span><span class="sxs-lookup"><span data-stu-id="bf997-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="bf997-112">С помощью текстового сообщения на мобильный телефон</span><span class="sxs-lookup"><span data-stu-id="bf997-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="bf997-113">Вход с помощью уведомлений Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="bf997-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="bf997-114">Вход с помощью кодов проверки Microsoft Authenticator </span><span class="sxs-lookup"><span data-stu-id="bf997-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="bf997-115">С помощью другого метода, так как я не могу использовать прямо сейчас основной вариант</span><span class="sxs-lookup"><span data-stu-id="bf997-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="bf997-116">Вход с помощью телефонного звонка</span><span class="sxs-lookup"><span data-stu-id="bf997-116">Signing in with a phone call</span></span>
<span data-ttu-id="bf997-117">Ниже описана процедура двухфакторной проверки подлинности с помощью звонка на мобильный или рабочий телефон.</span><span class="sxs-lookup"><span data-stu-id="bf997-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="bf997-118">Войдите в приложение или службу, например Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="bf997-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="bf997-119">Вам поступит звонок от корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bf997-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="bf997-120">Ответьте на вызов и нажмите клавишу #.</span><span class="sxs-lookup"><span data-stu-id="bf997-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="bf997-121">Вход с помощью текстового сообщения</span><span class="sxs-lookup"><span data-stu-id="bf997-121">Signing in with a text message</span></span>
<span data-ttu-id="bf997-122">Ниже описана процедура двухфакторной проверки подлинности с помощью текстового сообщения на мобильный телефон.</span><span class="sxs-lookup"><span data-stu-id="bf997-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="bf997-123">Войдите в приложение или службу, например Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="bf997-123">Sign in to an application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="bf997-124">Корпорация Майкрософт отправляет текстовое сообщение, содержащее числовой код.</span><span class="sxs-lookup"><span data-stu-id="bf997-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="bf997-125">Введите код в соответствующее поле на странице входа.</span><span class="sxs-lookup"><span data-stu-id="bf997-125">Enter the code in the box provided on the sign-in page.</span></span> 

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="bf997-126">Вход с помощью приложения Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="bf997-126">Signing in with the Microsoft Authenticator app</span></span> 
<span data-ttu-id="bf997-127">Ниже описано, как использовать приложение Microsoft Authenticator для двухфакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bf997-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="bf997-128">Приложение можно использовать двумя способами.</span><span class="sxs-lookup"><span data-stu-id="bf997-128">There are two different ways to use the app.</span></span> <span data-ttu-id="bf997-129">Вы можете получить push-уведомления на устройстве или открыть приложение, чтобы получить код проверки.</span><span class="sxs-lookup"><span data-stu-id="bf997-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="bf997-130">Вход с использованием уведомления от приложения Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="bf997-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="bf997-131">Войдите в приложение или службу, например Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="bf997-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="bf997-132">Корпорация Майкрософт отправляет push-уведомление в приложение Microsoft Authenticator на ваше устройство.</span><span class="sxs-lookup"><span data-stu-id="bf997-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![Майкрософт отправляет уведомление](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="bf997-134">Откройте уведомление на телефоне и нажмите клавишу **Подтвердить**.</span><span class="sxs-lookup"><span data-stu-id="bf997-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="bf997-135">Если компания требует ввода ПИН-кода, укажите его.</span><span class="sxs-lookup"><span data-stu-id="bf997-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="bf997-136">После этого вы войдете в систему.</span><span class="sxs-lookup"><span data-stu-id="bf997-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="bf997-137">Вход через приложение Microsoft Authenticator с использованием кода проверки</span><span class="sxs-lookup"><span data-stu-id="bf997-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="bf997-138">Если вы используете приложение Microsoft Authenticator для получения кодов проверки, то при открытии приложения вы увидите число под именем своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="bf997-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="bf997-139">Это число изменяется каждые 30 секунд, чтобы вы не использовали его дважды.</span><span class="sxs-lookup"><span data-stu-id="bf997-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="bf997-140">Когда появится запрос на код проверки, откройте приложение и используйте отображаемое число.</span><span class="sxs-lookup"><span data-stu-id="bf997-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="bf997-141">Войдите в приложение или службу, например Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="bf997-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="bf997-142">Вам будет предложено ввести код проверки.</span><span class="sxs-lookup"><span data-stu-id="bf997-142">Microsoft prompts you for a verification code.</span></span>

  ![Введите код проверки](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="bf997-144">Откройте приложение Microsoft Authenticator на телефоне и введите код в поле для входа.</span><span class="sxs-lookup"><span data-stu-id="bf997-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="bf997-145">Вход с помощью альтернативного метода</span><span class="sxs-lookup"><span data-stu-id="bf997-145">Signing in with an alternate method</span></span>
<span data-ttu-id="bf997-146">Иногда у вас может не быть телефона или устройства, которые настроены для основного метода проверки.</span><span class="sxs-lookup"><span data-stu-id="bf997-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="bf997-147">Именно поэтому мы рекомендуем настроить резервный метод проверки подлинности для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="bf997-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="bf997-148">Ниже приводится процедура входа с помощью альтернативного метода, когда основной метод недоступен.</span><span class="sxs-lookup"><span data-stu-id="bf997-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="bf997-149">Войдите в приложение или службу, например Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="bf997-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="bf997-150">Выберите **Использовать другой вариант проверки**.</span><span class="sxs-lookup"><span data-stu-id="bf997-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="bf997-151">Вы увидите другие варианты проверки, число которых зависит от ваших настроек.</span><span class="sxs-lookup"><span data-stu-id="bf997-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="bf997-152">Выберите альтернативный метод и войдите.</span><span class="sxs-lookup"><span data-stu-id="bf997-152">Choose an alternate method and sign in.</span></span>

  ![Использовать другой метод](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="bf997-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf997-154">Next steps</span></span>

<span data-ttu-id="bf997-155">Если у вас возникли проблемы при входе в систему с помощью двухфакторной проверки подлинности, см. статью [Проблемы с двухфакторной проверкой подлинности](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="bf997-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="bf997-156">Узнайте, как [управлять параметрами двухфакторной проверки подлинности](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="bf997-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="bf997-157">Узнайте, как [начать работу с приложением Microsoft Authenticator](microsoft-authenticator-app-how-to.md), чтобы вместо использоваться для входа уведомления вместо текстовых сообщений и звонков.</span><span class="sxs-lookup"><span data-stu-id="bf997-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span> 