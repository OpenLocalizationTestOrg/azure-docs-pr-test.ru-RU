---
title: "Управление параметрами двухфакторной проверки подлинности | Документация Майкрософт"
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
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="5f17e-104">Управление параметрами двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="5f17e-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="5f17e-105">Эта статья содержит информацию о том, как изменить параметры двухфакторной проверки подлинности или многофакторной идентификации.</span><span class="sxs-lookup"><span data-stu-id="5f17e-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="5f17e-106">Если у вас возникают проблемы со входом в учетную запись, см. сведения об устранении неполадок в статье [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) (Трудности с двухфакторной проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="5f17e-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="5f17e-107">Где найти страницу параметров</span><span class="sxs-lookup"><span data-stu-id="5f17e-107">Where to find the settings page</span></span>
<span data-ttu-id="5f17e-108">В зависимости от настроек многофакторной идентификации в вашей организации есть несколько способов изменения таких параметров, как номер телефона.</span><span class="sxs-lookup"><span data-stu-id="5f17e-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="5f17e-109">Если ИТ-администратор предоставил вам URL-адрес или процедуру для управления параметрами двухфакторной проверки подлинности, используйте эти сведения.</span><span class="sxs-lookup"><span data-stu-id="5f17e-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="5f17e-110">Для всех остальных случаев должны подойти следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5f17e-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="5f17e-111">Если при выполнении следующих действий вы увидите параметры, отличающиеся от описанных, значит ваша организация использует персонализированную версию портала.</span><span class="sxs-lookup"><span data-stu-id="5f17e-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="5f17e-112">Попросите у администратора ссылку на портал многофакторной идентификации Azure.</span><span class="sxs-lookup"><span data-stu-id="5f17e-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="5f17e-113">Войдите на портал по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5f17e-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="5f17e-114">В правом верхнем углу выберите имя учетной записи и **профиль**.</span><span class="sxs-lookup"><span data-stu-id="5f17e-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="5f17e-115">Выберите элемент **Дополнительная проверка безопасности**.</span><span class="sxs-lookup"><span data-stu-id="5f17e-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="5f17e-117">Загрузится страница дополнительной проверки безопасности с настроенными параметрами.</span><span class="sxs-lookup"><span data-stu-id="5f17e-117">The Additional security verification page loads with your settings.</span></span>

    ![Подтверждение](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="5f17e-119">Я хочу изменить свой номер телефона или добавить дополнительный номер</span><span class="sxs-lookup"><span data-stu-id="5f17e-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="5f17e-120">Важно настроить дополнительный номер телефона для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5f17e-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="5f17e-121">Скорее всего, ваш основной номер телефона и мобильное приложение находятся на одном телефоне. Поэтому дополнительный номер телефона является единственным способом возврата в вашу учетную запись в случае потери или кражи телефона.</span><span class="sxs-lookup"><span data-stu-id="5f17e-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="5f17e-122">Если у вас нет доступа к основному телефону и вам требуется помощь для входа в учетную запись, см. справочную информацию в статье [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) (Трудности с двухфакторной проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="5f17e-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="5f17e-123">**Изменение основного номера телефона**</span><span class="sxs-lookup"><span data-stu-id="5f17e-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="5f17e-124">На странице дополнительной проверки безопасности выберите текстовое поле с текущим номером телефона и исправьте его на новый номер телефона.</span><span class="sxs-lookup"><span data-stu-id="5f17e-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="5f17e-125">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5f17e-125">Select **Save**.</span></span>  
3. <span data-ttu-id="5f17e-126">Если вы используете этот номер в качестве основного варианта проверки подлинности, для сохранения нового номера потребуется подтвердить его.</span><span class="sxs-lookup"><span data-stu-id="5f17e-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="5f17e-127">**Добавление дополнительного номера телефона**</span><span class="sxs-lookup"><span data-stu-id="5f17e-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="5f17e-128">На странице дополнительной проверки безопасности установите флажок **Дополнительный телефон для проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="5f17e-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="5f17e-129">В текстовом поле введите дополнительный номер телефона.</span><span class="sxs-lookup"><span data-stu-id="5f17e-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="5f17e-130">Щелкните **Сохранить**. Настройка завершена.</span><span class="sxs-lookup"><span data-stu-id="5f17e-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="5f17e-131">Повторное выполнение двухфакторной проверки подлинности устройства, помеченного как доверенное</span><span class="sxs-lookup"><span data-stu-id="5f17e-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="5f17e-132">В зависимости от параметров организации при выполнении двухфакторной проверки подлинности в браузере может отображаться флажок "Больше не спрашивать **X** дн.".</span><span class="sxs-lookup"><span data-stu-id="5f17e-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="5f17e-133">Если вы установили этот флажок и потеряли устройство или вам кажется, что учетная запись была скомпрометирована, двухфакторную проверку подлинности необходимо восстановить на всех своих устройствах.</span><span class="sxs-lookup"><span data-stu-id="5f17e-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="5f17e-134">На странице "Дополнительная проверка безопасности" выберите **Восстановление многофакторной проверки подлинности на ранее доверенных устройствах**.</span><span class="sxs-lookup"><span data-stu-id="5f17e-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="5f17e-135">При следующем входе в систему на любом устройстве отобразится запрос на выполнение двухфакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5f17e-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="5f17e-136">Как удалить Microsoft Authenticator со старого устройства и перенести на новое?</span><span class="sxs-lookup"><span data-stu-id="5f17e-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="5f17e-137">При удалении приложения с устройства или сбросе его параметров активация на внутреннем сервере не удаляется.</span><span class="sxs-lookup"><span data-stu-id="5f17e-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="5f17e-138">Дополнительные сведения можно найти в статье [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="5f17e-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f17e-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f17e-139">Next steps</span></span>
* <span data-ttu-id="5f17e-140">См. советы и справочные сведения по устранению неполадок в статье [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) (Трудности с двухфакторной проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="5f17e-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="5f17e-141">Настройте [пароли приложений](multi-factor-authentication-end-user-app-passwords.md) для всех приложений, которые не поддерживают двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="5f17e-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
