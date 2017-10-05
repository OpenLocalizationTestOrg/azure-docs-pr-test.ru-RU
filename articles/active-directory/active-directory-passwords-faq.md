---
title: "Часто задаваемые вопросы. Azure AD SSPR | Документация Майкрософт"
description: "Часто задаваемые вопросы о самостоятельном сбросе пароля Azure AD"
services: active-directory
keywords: "Управление паролями Active Directory, управление паролями, самостоятельный сброс пароля Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="02821-104">Вопросы и ответы об управлении паролями</span><span class="sxs-lookup"><span data-stu-id="02821-104">Password management frequently asked questions</span></span>

<span data-ttu-id="02821-105">Ниже приведены некоторые вопросы и ответы о сбросе пароля.</span><span class="sxs-lookup"><span data-stu-id="02821-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="02821-106">Если у вас есть общие вопросы об Azure AD и самостоятельном сбросе пароля, которые еще не рассматривались, их можно задать участникам сообщества на [форумах Azure AD](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="02821-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="02821-107">В сообщество входят инженеры, менеджеры по продуктам, MVP и ИТ-специалисты.</span><span class="sxs-lookup"><span data-stu-id="02821-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="02821-108">Данная статья состоит из следующих разделов:</span><span class="sxs-lookup"><span data-stu-id="02821-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="02821-109">**Вопросы о регистрации данных для сброса паролей**</span><span class="sxs-lookup"><span data-stu-id="02821-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="02821-110">**Вопросы о сбросе паролей**</span><span class="sxs-lookup"><span data-stu-id="02821-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="02821-111">**Вопросы об изменении паролей**</span><span class="sxs-lookup"><span data-stu-id="02821-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="02821-112">**Вопросы об отчетах по управлению паролями**</span><span class="sxs-lookup"><span data-stu-id="02821-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="02821-113">**Вопросы об обратной записи паролей**</span><span class="sxs-lookup"><span data-stu-id="02821-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="02821-114">Регистрация данных для сброса паролей</span><span class="sxs-lookup"><span data-stu-id="02821-114">Password reset registration</span></span>
* <span data-ttu-id="02821-115">**Вопрос. Могут ли пользователи регистрировать свои собственные данные для сброса паролей?**</span><span class="sxs-lookup"><span data-stu-id="02821-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="02821-116">**Ответ.** Да. Если функция сброса пароля активирована и у пользователя есть лицензия, он может перейти на портал регистрации данных для сброса паролей по ссылке http://aka.ms/ssprsetup и зарегистрировать свои собственные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="02821-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="02821-117">Зарегистрировать данные можно также на панели доступа на странице http://myapps.microsoft.com. Здесь нужно открыть вкладку профиля и щелкнуть параметр "Зарегистрироваться для сброса пароля".</span><span class="sxs-lookup"><span data-stu-id="02821-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="02821-118">**Вопрос. Могу ли я определять данные для сброса паролей от имени пользователей?**</span><span class="sxs-lookup"><span data-stu-id="02821-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="02821-119">**Ответ.** Да, это можно сделать с помощью Azure AD Connect, PowerShell, а также на [портале Azure](https://portal.azure.com) или на портале администрирования Office.</span><span class="sxs-lookup"><span data-stu-id="02821-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="02821-120">Дополнительные сведения см. в статье [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md) (Данные, используемые при самостоятельном сбросе пароля Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02821-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="02821-121">**Вопрос. Могу ли я синхронизировать данные для контрольных вопросов из локальной среды?**</span><span class="sxs-lookup"><span data-stu-id="02821-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="02821-122">**Ответ.** На сегодняшний день это невозможно.</span><span class="sxs-lookup"><span data-stu-id="02821-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="02821-123">**Вопрос. Могут ли пользователи зарегистрировать данные так, чтобы другие пользователи эти данные не видели?**</span><span class="sxs-lookup"><span data-stu-id="02821-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="02821-124">**Ответ.** Да. Когда пользователь регистрирует данные на портале регистрации для сброса паролей, эти данные сохраняются в специальных частных полях, которые могут просматривать только глобальные администраторы и сам пользователь.</span><span class="sxs-lookup"><span data-stu-id="02821-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="02821-125">Если при регистрации **учетной записи администратора Azure** пользователь указал номер телефона для проверки подлинности, этот номер автоматически добавляется в поле "Мобильный телефон", и его видят другие пользователи.</span><span class="sxs-lookup"><span data-stu-id="02821-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="02821-126">**Вопрос. Нужно ли пользователям регистрировать данные, чтобы сбрасывать пароли?**</span><span class="sxs-lookup"><span data-stu-id="02821-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="02821-127">**Ответ.** Нет. Если вы от их имени укажете достаточно сведений для проверки подлинности, пользователям не придется регистрировать эти сведения самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="02821-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="02821-128">Для работы функции сброса паролей требуется, чтобы правильно отформатированные данные хранились в соответствующих полях каталога.</span><span class="sxs-lookup"><span data-stu-id="02821-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="02821-129">**Вопрос. Могу ли я от имени пользователей синхронизировать или указывать данные в полях "Телефон для проверки подлинности", "Адрес электронной почты для проверки подлинности" и "Дополнительный телефон для проверки подлинности"?**</span><span class="sxs-lookup"><span data-stu-id="02821-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="02821-130">**Ответ.** На сегодняшний день это невозможно.</span><span class="sxs-lookup"><span data-stu-id="02821-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="02821-131">**Вопрос. Как на портале регистрации определяется, что именно нужно показывать для того или иного пользователя?**</span><span class="sxs-lookup"><span data-stu-id="02821-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="02821-132">**Ответ.** На портале регистрации данных для сброса паролей отображаются только те данные, которые вы настроили для пользователей</span><span class="sxs-lookup"><span data-stu-id="02821-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="02821-133">в каталоге на вкладке "Настройка" в разделе "Политика сброса пароля пользователя".</span><span class="sxs-lookup"><span data-stu-id="02821-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="02821-134">То есть, если вы не настроили, например, контрольные вопросы, пользователи не смогут выбрать этот вариант при регистрации.</span><span class="sxs-lookup"><span data-stu-id="02821-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="02821-135">**Вопрос. Когда пользователь считается зарегистрированным?**</span><span class="sxs-lookup"><span data-stu-id="02821-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="02821-136">**Ответ.** Пользователь считается зарегистрированным для SSPR при регистрации по крайней мере **нескольких способов, необходимых для сброса**, заданных на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02821-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="02821-137">Сброс паролей</span><span class="sxs-lookup"><span data-stu-id="02821-137">Password reset</span></span>
* <span data-ttu-id="02821-138">**Вопрос. Как долго следует ожидать сообщение электронной почты, SMS или звонок для сброса пароля?**</span><span class="sxs-lookup"><span data-stu-id="02821-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="02821-139">**Ответ.** Время ожидания сообщения электронной почты, SMS-сообщения или телефонного звонка составляет меньше минуты. Обычно это занимает 5–20 секунд.</span><span class="sxs-lookup"><span data-stu-id="02821-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="02821-140">Если в течение этого времени ничего не произошло, выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="02821-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="02821-141">Проверьте папку нежелательной почты.</span><span class="sxs-lookup"><span data-stu-id="02821-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="02821-142">Проверьте правильность номера телефона или адреса электронной почты, на который вы ожидаете получить уведомление.</span><span class="sxs-lookup"><span data-stu-id="02821-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="02821-143">Убедитесь, что данные для проверки подлинности в каталоге имеют правильный формат.</span><span class="sxs-lookup"><span data-stu-id="02821-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="02821-144">Пример: +1 4255551234 или user@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="02821-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="02821-145">**Вопрос. Какие языки поддерживает система сброса пароля?**</span><span class="sxs-lookup"><span data-stu-id="02821-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="02821-146">**Ответ.** Пользовательский интерфейс, SMS-сообщения и голосовые вызовы для сброса пароля переведены на те же языки, что и служба Office 365:</span><span class="sxs-lookup"><span data-stu-id="02821-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="02821-147">**Вопрос. Если я настрою фирменную символику своей организации на вкладке настроек каталога, где именно появится эта символика?**</span><span class="sxs-lookup"><span data-stu-id="02821-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="02821-148">**Ответ.** Логотип вашей организации будет отображаться на портале сброса паролей. Вы также сможете настроить ссылку для связи с администратором, указав нужный вам электронный или URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="02821-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="02821-149">Все сообщения электронной почты, отправляемые порталом для сброса паролей, будут содержать логотип вашей организации, ее фирменные цвета, название в тексте сообщения и указанное вами имя в поле отправителя.</span><span class="sxs-lookup"><span data-stu-id="02821-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="02821-150">**Вопрос. Куда именно нужно направлять пользователей для сброса паролей?**</span><span class="sxs-lookup"><span data-stu-id="02821-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="02821-151">**Ответ.** Вы можете направлять их напрямую на страницу https://passwordreset.microsoftonline.com или обязать их выбирать ссылку **Can’t access your account link** (Не удается получить доступ к своей учетной записи?) на странице входа в рабочую или учебную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="02821-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="02821-152">Вы также можете опубликовать эти ссылки в удобном для пользователей месте.</span><span class="sxs-lookup"><span data-stu-id="02821-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="02821-153">**Вопрос. Могу ли я пользоваться этой страницей на мобильном устройстве?**</span><span class="sxs-lookup"><span data-stu-id="02821-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="02821-154">**Ответ.** Да. Эта страница работает на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="02821-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="02821-155">**Вопрос. Поддерживается ли разблокировка учетных записей локальной службы Active Directory, когда пользователи сбрасывают свой пароль?**</span><span class="sxs-lookup"><span data-stu-id="02821-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="02821-156">**Ответ.** Да. Если на момент сброса пароля компонент обратной записи паролей уже развернут с помощью Azure AD Connect, учетная запись пользователя будет автоматически разблокирована.</span><span class="sxs-lookup"><span data-stu-id="02821-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="02821-157">**Вопрос. Как интегрировать функцию сброса паролей напрямую в интерфейс входа на локальный компьютер?**</span><span class="sxs-lookup"><span data-stu-id="02821-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="02821-158">**Ответ.** Если вы являетесь клиентом Azure AD Premium, вы можете бесплатно установить Microsoft Identity Manager и развернуть локальное решение для сброса паролей.</span><span class="sxs-lookup"><span data-stu-id="02821-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="02821-159">**Вопрос. Могу ли я настроить разные контрольные вопросы для разных языков?**</span><span class="sxs-lookup"><span data-stu-id="02821-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="02821-160">**Ответ.** На сегодняшний день это невозможно.</span><span class="sxs-lookup"><span data-stu-id="02821-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="02821-161">**Вопрос. Сколько контрольных вопросов можно настроить для проверки подлинности?**</span><span class="sxs-lookup"><span data-stu-id="02821-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="02821-162">**Ответ.** На [портале Azure](https://portal.azure.com) можно настроить до 20 собственных контрольных вопросов.</span><span class="sxs-lookup"><span data-stu-id="02821-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="02821-163">**Вопрос. Какова допустимая длина контрольных вопросов?**</span><span class="sxs-lookup"><span data-stu-id="02821-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="02821-164">**Ответ.** Контрольный вопрос должен содержать от 3 до 200 знаков.</span><span class="sxs-lookup"><span data-stu-id="02821-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="02821-165">**Вопрос. Какова допустимая длина ответов на контрольные вопросы?**</span><span class="sxs-lookup"><span data-stu-id="02821-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="02821-166">**Ответ.** Ответы должны содержать от 3 до 40 знаков.</span><span class="sxs-lookup"><span data-stu-id="02821-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="02821-167">**Вопрос. Можно ли использовать одинаковые ответы для разных контрольных вопросов?**</span><span class="sxs-lookup"><span data-stu-id="02821-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="02821-168">**Ответ.** Нет, одинаковые ответы для разных контрольных вопросов использовать нельзя.</span><span class="sxs-lookup"><span data-stu-id="02821-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="02821-169">**Вопрос. Может ли пользователь зарегистрировать несколько одинаковых контрольных вопросов?**</span><span class="sxs-lookup"><span data-stu-id="02821-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="02821-170">**Ответ.** Нет. Если пользователь зарегистрировал определенный вопрос, он не сможет его еще раз зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="02821-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="02821-171">**Вопрос. Можно ли задать минимальное количество контрольных вопросов для регистрации и сброса?**</span><span class="sxs-lookup"><span data-stu-id="02821-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="02821-172">**Ответ.** Да, можно задать одно ограничение для регистрации, а другое — для сброса.</span><span class="sxs-lookup"><span data-stu-id="02821-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="02821-173">В обоих случаях можно настроить от 3 до 5 контрольных вопросов.</span><span class="sxs-lookup"><span data-stu-id="02821-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="02821-174">**Вопрос. Если пользователь зарегистрировал больше вопросов, чем необходимо для сброса, какие именно контрольные вопросы выбираются при сбросе?**</span><span class="sxs-lookup"><span data-stu-id="02821-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="02821-175">**Ответ.** Из общего числа контрольных вопросов, которые зарегистрировал пользователь, в случайном порядке выбираются N вопросов, где N — **количество вопросов, необходимое для выполнения сброса**.</span><span class="sxs-lookup"><span data-stu-id="02821-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="02821-176">Например, если пользователь зарегистрировал 5 контрольных вопросов, но для сброса требуются только 3, из этих 5 вопросов случайным образом будет выбрано 3, которые будут представлены во время сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="02821-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="02821-177">Если пользователь неправильно отвечает, вопросы выбираются еще раз. Это позволяет предотвратить подбор ответов.</span><span class="sxs-lookup"><span data-stu-id="02821-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="02821-178">**Вопрос. Есть ли лимиты, ограничивающие количество попыток сброса пароля за короткий промежуток времени?**</span><span class="sxs-lookup"><span data-stu-id="02821-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="02821-179">**Ответ.** Да. В системе сброса пароля есть несколько функций защиты от несанкционированного использования.</span><span class="sxs-lookup"><span data-stu-id="02821-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="02821-180">Пользователи могут сделать только 5 попыток сброса пароля в течение часа, после чего эта возможность блокируется на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="02821-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="02821-181">Пользователи могут сделать только 5 попыток подтверждения номера телефона в течение часа, после чего эта возможность блокируется на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="02821-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="02821-182">Пользователи могут воспользоваться определенным методом проверки подлинности 5 раз в течение часа, после чего эта возможность блокируется на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="02821-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="02821-183">**Вопрос. Как долго действует одноразовый секретный код, полученный по электронной почте или в SMS?**</span><span class="sxs-lookup"><span data-stu-id="02821-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="02821-184">**Ответ.** Длительность сеанса сброса пароля — 105 минут.</span><span class="sxs-lookup"><span data-stu-id="02821-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="02821-185">С начала операции сброса пароля у пользователя есть 105 минут на выполнение этой операции.</span><span class="sxs-lookup"><span data-stu-id="02821-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="02821-186">По истечении этого времени одноразовый секретный код, полученный по электронной почте или в SMS, становится недействительным.</span><span class="sxs-lookup"><span data-stu-id="02821-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="02821-187">Изменение пароля</span><span class="sxs-lookup"><span data-stu-id="02821-187">Password change</span></span>
* <span data-ttu-id="02821-188">**Вопрос. Где пользователи могут изменять свои пароли?**</span><span class="sxs-lookup"><span data-stu-id="02821-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="02821-189">**Ответ.** Пользователи могут изменять пароли в любом расположении с изображением или значком своего профиля (например, в верхнем правом углу в интерфейсах [Office 365](https://portal.office.com) или на [панели доступа](https://myapps.microsoft.com)).</span><span class="sxs-lookup"><span data-stu-id="02821-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="02821-190">Пользователи могут изменять пароли на [странице профиля "Панель доступа"](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="02821-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="02821-191">Пользователи могут также запросить автоматическое изменение пароля на экране входа Azure AD, если срок действия их паролей истек.</span><span class="sxs-lookup"><span data-stu-id="02821-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="02821-192">Наконец, пользователи могут напрямую перейти на [портал изменения паролей Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx), если им нужно изменить пароли.</span><span class="sxs-lookup"><span data-stu-id="02821-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="02821-193">**Вопрос. Могут ли мои пользователи получать уведомления на портале Office по истечении срока действия локального пароля?**</span><span class="sxs-lookup"><span data-stu-id="02821-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="02821-194">**Ответ.** Если вы используете службы AD FS, вы можете настроить отправку уведомления, следуя инструкциям по [отправке утверждений политики паролей с помощью служб AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="02821-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="02821-195">Если вы используете синхронизацию хэша паролей, сейчас вы не сможете настроить отправку уведомлений.</span><span class="sxs-lookup"><span data-stu-id="02821-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="02821-196">Это связано с тем, что мы не синхронизируем политики паролей из локальных сред, поэтому мы не можем публиковать уведомления об истечении срока действия в облачных интерфейсах.</span><span class="sxs-lookup"><span data-stu-id="02821-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="02821-197">В любом случае вы также можете [уведомлять пользователей, что срок действия их паролей скоро завершится, с помощью PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="02821-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="02821-198">Отчеты об управлении паролями</span><span class="sxs-lookup"><span data-stu-id="02821-198">Password management reports</span></span>
* <span data-ttu-id="02821-199">**Вопрос. Через какое время данные отображаются в отчетах об управлении паролями?**</span><span class="sxs-lookup"><span data-stu-id="02821-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="02821-200">**Ответ.** Обычно данные появляются в отчетах об управлении паролями в течение 5–10 минут.</span><span class="sxs-lookup"><span data-stu-id="02821-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="02821-201">Но иногда на это может уйти до одного часа.</span><span class="sxs-lookup"><span data-stu-id="02821-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="02821-202">**Вопрос. Как отфильтровать отчеты об управлении паролями?**</span><span class="sxs-lookup"><span data-stu-id="02821-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="02821-203">**Ответ.** Отчеты можно фильтровать, используя кнопку с изображением лупы справа от заголовков столбцов в верхней части отчета.</span><span class="sxs-lookup"><span data-stu-id="02821-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="02821-204">Для более сложной фильтрации откройте отчет в программе Excel и создайте сводную таблицу.</span><span class="sxs-lookup"><span data-stu-id="02821-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="02821-205">**Вопрос. Каково максимальное число событий, которые хранятся в отчетах об управлении паролями?**</span><span class="sxs-lookup"><span data-stu-id="02821-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="02821-206">**Ответ.** В отчетах об управлении паролями хранится до 75 000 событий сброса паролей или событий регистрации сброса паролей за последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="02821-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="02821-207">Мы работаем над тем, чтобы увеличить это количество.</span><span class="sxs-lookup"><span data-stu-id="02821-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="02821-208">**Вопрос. Какой промежуток времени охватывают отчеты об управлении паролями?**</span><span class="sxs-lookup"><span data-stu-id="02821-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="02821-209">**Ответ.** Отчеты об управлении паролями включают операции за последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="02821-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="02821-210">Сейчас, если вам нужно вести архив этих данных, их можно периодически скачивать и сохранять в отдельном месте.</span><span class="sxs-lookup"><span data-stu-id="02821-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="02821-211">**Вопрос. Есть ли максимальное количество строк, которые могут отображаться в отчетах об управлении паролями?**</span><span class="sxs-lookup"><span data-stu-id="02821-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="02821-212">**Ответ.** Да. Каждый отчет может вмещать не более 75 000 строк — как в пользовательском интерфейсе, так и в скачанном файле.</span><span class="sxs-lookup"><span data-stu-id="02821-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="02821-213">**Вопрос. Есть ли API для доступа к данным сброса паролей или регистрации данных отчетов?**</span><span class="sxs-lookup"><span data-stu-id="02821-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="02821-214">**Ответ.** Да. Сведения о получении доступа к потоку данных отчетов о сбросе паролей см.</span><span class="sxs-lookup"><span data-stu-id="02821-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="02821-215">[здесь](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="02821-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="02821-216">Обратная запись паролей</span><span class="sxs-lookup"><span data-stu-id="02821-216">Password writeback</span></span>
* <span data-ttu-id="02821-217">**Вопрос. Что происходит во время обратной записи паролей?**</span><span class="sxs-lookup"><span data-stu-id="02821-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="02821-218">**Ответ.** В разделе [Как работает обратная запись паролей](active-directory-passwords-writeback.md) описано, что происходит при включении обратной записи паролей и как данные перемещаются через систему обратно в локальную среду.</span><span class="sxs-lookup"><span data-stu-id="02821-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="02821-219">**Вопрос. Как быстро происходит обратная запись паролей?  Существует ли задержка синхронизации, как при синхронизации хэша паролей?**</span><span class="sxs-lookup"><span data-stu-id="02821-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="02821-220">**Ответ.** Обратная запись паролей происходит мгновенно.</span><span class="sxs-lookup"><span data-stu-id="02821-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="02821-221">Для этого используется синхронный конвейер, принцип работы которого принципиально отличается от синхронизации хэша паролей.</span><span class="sxs-lookup"><span data-stu-id="02821-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="02821-222">При обратной записи паролей пользователи сразу узнают о результате сброса или смены пароля.</span><span class="sxs-lookup"><span data-stu-id="02821-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="02821-223">Среднее время успешной операции обратной записи не превышает 500 мс.</span><span class="sxs-lookup"><span data-stu-id="02821-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="02821-224">**Вопрос. Если локальная учетная запись отключена, повлияет ли это на учетную запись или доступ к облаку?**</span><span class="sxs-lookup"><span data-stu-id="02821-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="02821-225">**Ответ.** При отключении локального идентификатора ИД облако или доступ к нему также будут отключены с помощью AAD Connect по умолчанию в следующем интервале синхронизации (каждые 30 минут).</span><span class="sxs-lookup"><span data-stu-id="02821-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="02821-226">**Вопрос. Если локальная учетная запись ограничена локальной политикой паролей Active Directory, будет ли эта политика распространяться на функцию SSPR при изменении пароля?**</span><span class="sxs-lookup"><span data-stu-id="02821-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="02821-227">**Ответ.** Да. Функция SSPR руководствуется локальной политикой паролей AD, включая типичную политику паролей домена AD, а также любые определенные детальные политики паролей, назначенные данному пользователю.</span><span class="sxs-lookup"><span data-stu-id="02821-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="02821-228">**Вопрос. Для каких типов учетных записей работает обратная запись паролей?**</span><span class="sxs-lookup"><span data-stu-id="02821-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="02821-229">**Ответ.** Обратная запись паролей может применяться для федеративных пользователей и пользователей с синхронизацией хэша пароля.</span><span class="sxs-lookup"><span data-stu-id="02821-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="02821-230">**Вопрос. Соблюдает ли служба обратной записи паролей политики, применяемые к паролям в моем домене?**</span><span class="sxs-lookup"><span data-stu-id="02821-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="02821-231">**Ответ.** Да, компонент обратной записи паролей соблюдает настройки срока действия пароля, журнала, сложности, фильтров и другие ограничения, установленные для паролей в локальном домене.</span><span class="sxs-lookup"><span data-stu-id="02821-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="02821-232">**Вопрос. Защищена ли служба обратной записи паролей?  Насколько можно быть уверенным, что ее не взломают?**</span><span class="sxs-lookup"><span data-stu-id="02821-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="02821-233">**Ответ.** Да, компонент обратной записи паролей защищен.</span><span class="sxs-lookup"><span data-stu-id="02821-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="02821-234">Дополнительные сведения о 4 уровнях безопасности, реализованных в службе обратной записи паролей, см. в подразделе [Модель безопасности обратной записи паролей](active-directory-passwords-writeback.md#password-writeback-security-model) раздела "Как работает обратная запись паролей".</span><span class="sxs-lookup"><span data-stu-id="02821-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="02821-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02821-235">Next steps</span></span>

<span data-ttu-id="02821-236">Дополнительные сведения о сбросе пароля с помощью Azure AD см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="02821-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="02821-237">[**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02821-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="02821-238">[**Licensing requirements for Azure AD self-service password reset**](active-directory-passwords-licensing.md) (Требования к лицензированию самостоятельного сброса пароля в Azure AD). Сведения о настройке лицензирования Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02821-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="02821-239">[**Deploy password reset without requiring end-user registration**](active-directory-passwords-data.md) (Развертывание сброса пароля без регистрации пользователя). Сведения о необходимых данных и их использовании для управления паролями.</span><span class="sxs-lookup"><span data-stu-id="02821-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="02821-240">[**Развертывание компонентов управления паролями и обучение пользователей их использованию**](active-directory-passwords-best-practices.md). Рекомендации по планированию и развертыванию SSPR для пользователей.</span><span class="sxs-lookup"><span data-stu-id="02821-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="02821-241">[**Настройка компонентов управления паролями в соответствии с требованиями организации**](active-directory-passwords-customize.md). Сведения о настройке интерфейса и параметров использования SSPR для организации.</span><span class="sxs-lookup"><span data-stu-id="02821-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="02821-242">[**Параметры отчетов для управления паролями Azure AD**](active-directory-passwords-reporting.md). Определяйте, кто и когда использовал функцию SSPR.</span><span class="sxs-lookup"><span data-stu-id="02821-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="02821-243">[**Политики и ограничения для паролей в Azure Active Directory**](active-directory-passwords-policy.md). Общие сведения и информация об установке политик паролей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02821-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="02821-244">[**Обзор компонента обратной записи паролей**](active-directory-passwords-writeback.md). Как работает функция обратной записи паролей с вашим локальным каталогом.</span><span class="sxs-lookup"><span data-stu-id="02821-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="02821-245">[**Как работает управление паролями в Azure Active Directory**](active-directory-passwords-how-it-works.md). Сведения о принципе работы управления паролями.</span><span class="sxs-lookup"><span data-stu-id="02821-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="02821-246">[**Устранение неполадок, связанных с управлением паролями**](active-directory-passwords-troubleshoot.md). Сведения об устранении распространенных проблем с SSPR.</span><span class="sxs-lookup"><span data-stu-id="02821-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
