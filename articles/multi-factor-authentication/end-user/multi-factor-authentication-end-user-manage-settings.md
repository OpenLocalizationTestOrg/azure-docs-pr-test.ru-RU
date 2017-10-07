---
title: "aaaManage параметры двухшаговой проверки | Документы Microsoft"
description: "Управление использованием многофакторной идентификации Azure, в том числе изменение контактных данных и настройка устройств."
services: multi-factor-authentication
keywords: "многофакторная проверка подлинности клиента, проблемы с проверкой подлинности, идентификатор корреляции"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="823a3-104">Управление параметрами двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="823a3-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="823a3-105">Эта статья содержит ответы на вопросы о том, как параметры tooupdate для двухшаговой проверки или многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="823a3-105">This article answers questions about how tooupdate settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="823a3-106">Если возникают проблемы со входом в учетной записи tooyour ссылаться слишком[возникли трудности, с помощью двухэтапной проверки](multi-factor-authentication-end-user-troubleshoot.md) справки по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="823a3-106">If you are having issues signing in tooyour account, refer too[Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-toofind-hello-settings-page"></a><span data-ttu-id="823a3-107">Где toofind Здравствуйте, страница "Параметры"</span><span class="sxs-lookup"><span data-stu-id="823a3-107">Where toofind hello settings page</span></span>
<span data-ttu-id="823a3-108">В зависимости от настроек многофакторной идентификации в вашей организации есть несколько способов изменения таких параметров, как номер телефона.</span><span class="sxs-lookup"><span data-stu-id="823a3-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="823a3-109">Если ИТ-администратору отправлять определенному URL-АДРЕСУ или действия toomanage двухшаговую проверку, следуйте этим инструкциям.</span><span class="sxs-lookup"><span data-stu-id="823a3-109">If your IT admin sent out a specific URL or steps toomanage two-step verification, follow those instructions.</span></span> <span data-ttu-id="823a3-110">В противном случае hello, следуя инструкциям подойдет любой другой.</span><span class="sxs-lookup"><span data-stu-id="823a3-110">Otherwise, hello following instructions should work for everybody else.</span></span> <span data-ttu-id="823a3-111">Если вы выполните следующие действия, но не видите hello же параметры, которые означает, что организация собственного собственные портала.</span><span class="sxs-lookup"><span data-stu-id="823a3-111">If you follow these steps but don't see hello same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="823a3-112">Попросите своего администратора портала Azure Multi-factor Authentication tooyour ссылку hello.</span><span class="sxs-lookup"><span data-stu-id="823a3-112">Ask your admin for hello link tooyour Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="823a3-113">Войдите в слишком[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="823a3-113">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="823a3-114">Выберите имя учетной записи в правой верхней hello, а затем **профиль**.</span><span class="sxs-lookup"><span data-stu-id="823a3-114">Select your account name in hello top right, then select **profile**.</span></span>  
3. <span data-ttu-id="823a3-115">Выберите элемент **Дополнительная проверка безопасности**.</span><span class="sxs-lookup"><span data-stu-id="823a3-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="823a3-117">загрузке Hello дополнительную безопасность проверки страницы с параметрами.</span><span class="sxs-lookup"><span data-stu-id="823a3-117">hello Additional security verification page loads with your settings.</span></span>

    ![Подтверждение](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="823a3-119">Мне требуется toochange Мой номер телефона, или добавить дополнительный номер</span><span class="sxs-lookup"><span data-stu-id="823a3-119">I want toochange my phone number, or add a secondary number</span></span>
<span data-ttu-id="823a3-120">Это важные tooconfigure номер телефона вторичной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="823a3-120">It is important tooconfigure a secondary authentication phone number.</span></span>  <span data-ttu-id="823a3-121">Поскольку основного телефона, номер и мобильного приложения возможно, на hello же телефон, Дополнительный телефон hello является единственным способом hello, можно будет tooget обратно в вашу учетную запись, если телефон потерян или украден.</span><span class="sxs-lookup"><span data-stu-id="823a3-121">Because your primary phone number and your mobile app are probably on hello same phone, hello secondary phone number is hello only way you will be able tooget back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="823a3-122">Если у вас нет доступа tooyour основной номер телефона и вам нужна помощь в tooyour учетной записи, см. в справочных статьях [возникли трудности, с помощью двухэтапной проверки](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="823a3-122">If you don't have access tooyour primary phone number, and need help getting in tooyour account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="823a3-123">**toochange основного номера телефона:**</span><span class="sxs-lookup"><span data-stu-id="823a3-123">**toochange your primary phone number:**</span></span>  

1. <span data-ttu-id="823a3-124">На странице проверки hello дополнительную безопасность выберите текстовое поле hello с текущий номер телефона и внесите в него новый номер телефона.</span><span class="sxs-lookup"><span data-stu-id="823a3-124">On hello Additional security verification page, select hello text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="823a3-125">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="823a3-125">Select **Save**.</span></span>  
3. <span data-ttu-id="823a3-126">Если это число hello, используемой в качестве предпочтительного варианта проверки имеется новый номер tooverify hello до его сохранения.</span><span class="sxs-lookup"><span data-stu-id="823a3-126">If this is hello number that you use for your preferred verification option, you have tooverify hello new number before you can save it.</span></span>  

<span data-ttu-id="823a3-127">**tooadd номер телефона получателя:**</span><span class="sxs-lookup"><span data-stu-id="823a3-127">**tooadd a secondary phone number:**</span></span>  

1. <span data-ttu-id="823a3-128">На странице проверки hello дополнительную безопасность, установите флажок hello рядом слишком**альтернативный проверочный звонок.**</span><span class="sxs-lookup"><span data-stu-id="823a3-128">On hello Additional security verification page, check hello box next too**Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="823a3-129">Введите номер телефона получателя в поле текста hello.</span><span class="sxs-lookup"><span data-stu-id="823a3-129">Enter your secondary phone number in hello text box.</span></span>  
3. <span data-ttu-id="823a3-130">Щелкните **Сохранить**. Настройка завершена.</span><span class="sxs-lookup"><span data-stu-id="823a3-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="823a3-131">Повторное выполнение двухфакторной проверки подлинности устройства, помеченного как доверенное</span><span class="sxs-lookup"><span data-stu-id="823a3-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="823a3-132">В зависимости от параметров организации при выполнении двухфакторной проверки подлинности в браузере может отображаться флажок "Больше не спрашивать **X** дн.".</span><span class="sxs-lookup"><span data-stu-id="823a3-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="823a3-133">Установите этот флажок и затем утери или думаю, что скомпрометированы вашей учетной записи, следует восстановить из двух tooall проверки устройства.</span><span class="sxs-lookup"><span data-stu-id="823a3-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification tooall your devices.</span></span> 

1. <span data-ttu-id="823a3-134">На странице проверки hello дополнительной защиты выберите **восстановления многофакторной проверки подлинности на ранее доверенных устройствах**.</span><span class="sxs-lookup"><span data-stu-id="823a3-134">On hello Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="823a3-135">Hello при очередном входе на любом устройстве, вы будете запрашиваемые tooperform двухшаговую проверку.</span><span class="sxs-lookup"><span data-stu-id="823a3-135">hello next time you sign in on any device, you'll be prompted tooperform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a><span data-ttu-id="823a3-136">Как очистить структуру проверки подлинности Майкрософт из старого устройства и переместить tooa новую?</span><span class="sxs-lookup"><span data-stu-id="823a3-136">How do I clean up Microsoft Authenticator from my old device and move tooa new one?</span></span>
<span data-ttu-id="823a3-137">При удалении приложения hello с сброса hello устройства или устройства, не удаляет hello активацию hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="823a3-137">When you uninstall hello app from your device or reset hello device, it does not remove hello activation on hello back end.</span></span> <span data-ttu-id="823a3-138">Дополнительные сведения можно найти в статье [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="823a3-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="823a3-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="823a3-139">Next steps</span></span>
* <span data-ttu-id="823a3-140">См. советы и справочные сведения по устранению неполадок в статье [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) (Трудности с двухфакторной проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="823a3-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="823a3-141">Настройте [пароли приложений](multi-factor-authentication-end-user-app-passwords.md) для всех приложений, которые не поддерживают двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="823a3-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
