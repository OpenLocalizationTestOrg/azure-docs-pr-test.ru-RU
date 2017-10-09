---
title: "вход aaaAzure многофакторной проверки Подлинности с помощью двухэтапной проверки | Документы Microsoft"
description: "Эта страница предоставит рекомендации на где toogo toosee hello вход методов, доступных с помощью Azure MFA."
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
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="87681-104">Hello входа в систему с многофакторной проверкой подлинности Azure</span><span class="sxs-lookup"><span data-stu-id="87681-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="87681-105">Hello в этой статье предназначен toowalk через стандартные входа в систему.</span><span class="sxs-lookup"><span data-stu-id="87681-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="87681-106">Справку по вход в систему или tootroubleshoot проблем см. в разделе [возникли трудности с многофакторной проверкой подлинности Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="87681-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="87681-107">Каким будет ваш вариант входа</span><span class="sxs-lookup"><span data-stu-id="87681-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="87681-108">Процедура входа отличается в зависимости от того, какое значение выбрано toouse как ваш второго фактора: телефонный звонок, тексты или приложения проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="87681-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="87681-109">Выберите параметр hello, наиболее точно описывающий действиях:</span><span class="sxs-lookup"><span data-stu-id="87681-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="87681-110">Как вы входите в учетную запись?</span><span class="sxs-lookup"><span data-stu-id="87681-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="87681-111">С помощью телефонного звонка toomy мобильный или рабочий телефон</span><span class="sxs-lookup"><span data-stu-id="87681-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="87681-112">С помощью SMS на мобильный телефон toomy</span><span class="sxs-lookup"><span data-stu-id="87681-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="87681-113">С помощью уведомления в приложение для проверки подлинности Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="87681-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="87681-114">С помощью кодов подтверждения из приложения hello проверки подлинности Майкрософт</span><span class="sxs-lookup"><span data-stu-id="87681-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="87681-115">С помощью другого метода, так как я не могу использовать прямо сейчас основной вариант</span><span class="sxs-lookup"><span data-stu-id="87681-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="87681-116">Вход с помощью телефонного звонка</span><span class="sxs-lookup"><span data-stu-id="87681-116">Signing in with a phone call</span></span>
<span data-ttu-id="87681-117">Hello следующую информацию описывает hello двухэтапный проверки и опыт работы с мобильными tooyour вызова или рабочий телефон.</span><span class="sxs-lookup"><span data-stu-id="87681-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="87681-118">Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="87681-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="87681-119">Вам поступит звонок от корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="87681-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="87681-120">Ответить на телефонный hello и нажмите клавишу # hello.</span><span class="sxs-lookup"><span data-stu-id="87681-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="87681-121">Вход с помощью текстового сообщения</span><span class="sxs-lookup"><span data-stu-id="87681-121">Signing in with a text message</span></span>
<span data-ttu-id="87681-122">Hello следующую информацию описывается hello двухэтапный проверки взаимодействие с мобильным телефоном tooyour текст сообщения:</span><span class="sxs-lookup"><span data-stu-id="87681-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="87681-123">Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="87681-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="87681-124">Корпорация Майкрософт отправляет текстовое сообщение, содержащее числовой код.</span><span class="sxs-lookup"><span data-stu-id="87681-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="87681-125">Введите в поле на странице входа hello hello hello код.</span><span class="sxs-lookup"><span data-stu-id="87681-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="87681-126">Вход в приложение для проверки подлинности Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="87681-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="87681-127">Hello следующие данные описывают hello работы с приложением для проверки подлинности Microsoft hello для двухшаговой проверки.</span><span class="sxs-lookup"><span data-stu-id="87681-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="87681-128">Существует приложение hello toouse двумя различными способами.</span><span class="sxs-lookup"><span data-stu-id="87681-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="87681-129">Вы можете получать push-уведомлений на устройства или tooget приложения hello код проверки можно открыть.</span><span class="sxs-lookup"><span data-stu-id="87681-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="87681-130">toosign вход с помощью уведомления от приложения hello проверки подлинности Майкрософт</span><span class="sxs-lookup"><span data-stu-id="87681-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="87681-131">Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="87681-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="87681-132">Майкрософт отправляет приложением проверки подлинности Microsoft toohello уведомления на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="87681-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Майкрософт отправляет уведомление](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="87681-134">Откройте hello уведомления на телефон и выберите hello **проверьте** ключа.</span><span class="sxs-lookup"><span data-stu-id="87681-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="87681-135">Если компания требует ввода ПИН-кода, укажите его.</span><span class="sxs-lookup"><span data-stu-id="87681-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="87681-136">После этого вы войдете в систему.</span><span class="sxs-lookup"><span data-stu-id="87681-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="87681-137">toosign использовать код проверки с приложением для проверки подлинности Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="87681-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="87681-138">При использовании кодов проверки tooget приложение проверки подлинности Microsoft hello, затем при открытии приложение hello появляются в списке имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="87681-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="87681-139">Этот номер изменяется каждые 30 секунд, чтобы не использовать одно и тоже число дважды hello.</span><span class="sxs-lookup"><span data-stu-id="87681-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="87681-140">В ответ на запрос проверки кода, откройте приложение "hello" и использовать независимо от значения в текущий момент отображается.</span><span class="sxs-lookup"><span data-stu-id="87681-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="87681-141">Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="87681-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="87681-142">Вам будет предложено ввести код проверки.</span><span class="sxs-lookup"><span data-stu-id="87681-142">Microsoft prompts you for a verification code.</span></span>

  ![Введите код проверки](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="87681-144">Откройте приложение проверки подлинности Microsoft hello на телефоне и введите код hello в поле hello, где вы входите.</span><span class="sxs-lookup"><span data-stu-id="87681-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="87681-145">Вход с помощью альтернативного метода</span><span class="sxs-lookup"><span data-stu-id="87681-145">Signing in with an alternate method</span></span>
<span data-ttu-id="87681-146">Иногда у вас нет hello phone или устройства, настроенные как проверки предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="87681-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="87681-147">Именно поэтому мы рекомендуем настроить резервный метод проверки подлинности для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="87681-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="87681-148">Hello следующем разделе показано, как toosign с альтернативным способом при основного способа могут быть недоступны.</span><span class="sxs-lookup"><span data-stu-id="87681-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="87681-149">Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="87681-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="87681-150">Выберите **Использовать другой вариант проверки**.</span><span class="sxs-lookup"><span data-stu-id="87681-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="87681-151">Вы увидите другие варианты проверки, число которых зависит от ваших настроек.</span><span class="sxs-lookup"><span data-stu-id="87681-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="87681-152">Выберите альтернативный метод и войдите.</span><span class="sxs-lookup"><span data-stu-id="87681-152">Choose an alternate method and sign in.</span></span>

  ![Использовать другой метод](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="87681-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87681-154">Next steps</span></span>

<span data-ttu-id="87681-155">Если у вас возникли проблемы при входе в систему с помощью двухфакторной проверки подлинности, см. статью [Проблемы с двухфакторной проверкой подлинности](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="87681-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="87681-156">Узнайте, каким образом слишком[управление параметры двухшаговой проверки](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="87681-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="87681-157">Узнайте, как слишком[Приступая к работе с приложением для проверки подлинности Microsoft hello](microsoft-authenticator-app-how-to.md) , чтобы можно было использовать toosign уведомления, вместо текстов и телефонные звонки.</span><span class="sxs-lookup"><span data-stu-id="87681-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
