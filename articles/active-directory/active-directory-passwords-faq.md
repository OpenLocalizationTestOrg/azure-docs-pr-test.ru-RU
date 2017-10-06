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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="4e93d-104">Вопросы и ответы об управлении паролями</span><span class="sxs-lookup"><span data-stu-id="4e93d-104">Password management frequently asked questions</span></span>

<span data-ttu-id="4e93d-105">следующие Hello являются некоторые часто задаваемые вопросы для прочих связанных toopassword сброса.</span><span class="sxs-lookup"><span data-stu-id="4e93d-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="4e93d-106">Если у вас есть вопрос об Azure AD и паролем самообслуживания Сброс, который не отвечает на здесь, вы можете запросить сообщества hello обратитесь за помощью на hello [форумы Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="4e93d-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="4e93d-107">Члены сообщества hello включать инженеров, менеджеры по продуктам, специалисты MVP и совета ИТ-специалистов.</span><span class="sxs-lookup"><span data-stu-id="4e93d-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="4e93d-108">Вопросы и ответы разбивается на hello в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="4e93d-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="4e93d-109">**Вопросы о регистрации данных для сброса паролей**</span><span class="sxs-lookup"><span data-stu-id="4e93d-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="4e93d-110">**Вопросы о сбросе паролей**</span><span class="sxs-lookup"><span data-stu-id="4e93d-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="4e93d-111">**Вопросы об изменении паролей**</span><span class="sxs-lookup"><span data-stu-id="4e93d-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="4e93d-112">**Вопросы об отчетах по управлению паролями**</span><span class="sxs-lookup"><span data-stu-id="4e93d-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="4e93d-113">**Вопросы об обратной записи паролей**</span><span class="sxs-lookup"><span data-stu-id="4e93d-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="4e93d-114">Регистрация данных для сброса паролей</span><span class="sxs-lookup"><span data-stu-id="4e93d-114">Password reset registration</span></span>
* <span data-ttu-id="4e93d-115">**Вопрос. Могут ли пользователи регистрировать свои собственные данные для сброса паролей?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="4e93d-116">**Ответ** Да, при условии, что включен сброс паролей и у пользователей есть лицензии, они могут перейти портал регистрации сброса пароля toohello по адресу http://aka.ms/ssprsetup tooregister данные проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4e93d-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="4e93d-117">Пользователи также могут регистрировать с переходом панели доступа toohello на http://myapps.microsoft.com, щелкнув вкладку профиль hello и hello регистрации для сброса пароля параметр.</span><span class="sxs-lookup"><span data-stu-id="4e93d-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="4e93d-118">**Вопрос. Могу ли я определять данные для сброса паролей от имени пользователей?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="4e93d-119">**Ответ** Да, это можно сделать с помощью Azure AD Connect PowerShell hello [портал Azure](https://portal.azure.com), или портал администрирования Office hello.</span><span class="sxs-lookup"><span data-stu-id="4e93d-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="4e93d-120">Дополнительные сведения см. в статье hello [данные, используемые Azure AD самостоятельного сброса пароля](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="4e93d-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="4e93d-121">**Вопрос. Могу ли я синхронизировать данные для контрольных вопросов из локальной среды?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="4e93d-122">**Ответ.** На сегодняшний день это невозможно.</span><span class="sxs-lookup"><span data-stu-id="4e93d-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="4e93d-123">**Вопрос. Могут ли пользователи зарегистрировать данные так, чтобы другие пользователи эти данные не видели?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="4e93d-124">**Ответ** Да, если пользователи регистрировать данные с помощью hello регистрации портал для сброса пароля он сохраняется в закрытых полях проверки подлинности, видны только глобальным администраторам и hello пользователем.</span><span class="sxs-lookup"><span data-stu-id="4e93d-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="4e93d-125">Если **учетной записи администратора Azure** регистрирует свой номер телефона проверки подлинности, он также включаются в поле мобильного телефона hello и является видимым.</span><span class="sxs-lookup"><span data-stu-id="4e93d-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="4e93d-126">**Вопрос у пользователей есть toobe зарегистрировать, прежде чем они смогут использовать сброс пароля?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="4e93d-127">**Ответ** нет, если вы определили достаточно сведений для проверки подлинности от их имени, пользователи могут не tooregister.</span><span class="sxs-lookup"><span data-stu-id="4e93d-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="4e93d-128">Сброс пароля работает, до тех пор, пока имеются правильно отформатированные данные, хранящиеся в соответствующие поля hello в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="4e93d-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="4e93d-129">**Вопрос. можно ли синхронизировать или задать поля hello телефон для аутентификации, проверка подлинности по электронной почте или дополнительный телефон для проверки подлинности от имени пользователей**</span><span class="sxs-lookup"><span data-stu-id="4e93d-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="4e93d-130">**Ответ.** На сегодняшний день это невозможно.</span><span class="sxs-lookup"><span data-stu-id="4e93d-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="4e93d-131">**Вопрос. как портал регистрации hello узнает, какие параметры tooshow моих пользователей?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="4e93d-132">**Ответ** сброса пароля hello портала регистрации, только показано hello параметры, которые включены для пользователей.</span><span class="sxs-lookup"><span data-stu-id="4e93d-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="4e93d-133">Эти параметры будут расположены в разделе Политика сброса пароля пользователя на вкладке Настройка» hello. Например это означает, что если не включить контрольные вопросы, затем пользователи не могли tooregister для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="4e93d-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="4e93d-134">**Вопрос. Когда пользователь считается зарегистрированным?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="4e93d-135">**Ответ** считается пользователь, зарегистрированных для SSPR при регистрации по крайней мере hello **число tooreset необходимые методы** , устанавливаемое hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e93d-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="4e93d-136">Сброс паролей</span><span class="sxs-lookup"><span data-stu-id="4e93d-136">Password reset</span></span>
* <span data-ttu-id="4e93d-137">**Вопрос. как долго следует ждать tooreceive электронной почты, SMS или звонок из службы сброса паролей?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="4e93d-138">**Ответ** электронной почты, сообщения SMS и телефонные звонки должны поступать в меньше одной минуты с hello обычно 5-20 секунд.</span><span class="sxs-lookup"><span data-stu-id="4e93d-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="4e93d-139">Если вы не получите уведомления hello в этот промежуток времени:</span><span class="sxs-lookup"><span data-stu-id="4e93d-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="4e93d-140">Проверьте папку нежелательной почты.</span><span class="sxs-lookup"><span data-stu-id="4e93d-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="4e93d-141">Проверка hello электронной почты, к которому не hello, который ожидается.</span><span class="sxs-lookup"><span data-stu-id="4e93d-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="4e93d-142">Убедитесь, что данные проверки подлинности hello в каталоге hello имеет правильный формат.</span><span class="sxs-lookup"><span data-stu-id="4e93d-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="4e93d-143">Пример: +1 4255551234 или user@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4e93d-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="4e93d-144">**Вопрос. Какие языки поддерживает система сброса пароля?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="4e93d-145">**Ответ** hello пользовательский Интерфейс сброса пароля, SMS-сообщения и голосовые вызовы локализованы на hello те же языки, которые поддерживаются в Office 365.</span><span class="sxs-lookup"><span data-stu-id="4e93d-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="4e93d-146">**Вопрос, какие части интерфейса для сброса пароля hello применяется при установке организации в каталоге Мои продвижения настроить вкладку?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="4e93d-147">**Ответ** портала сброса паролей hello отображение логотип вашей организации и tooconfigure hello контакт ваш администратор ссылку toopoint tooa пользовательский адрес электронной почты или URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="4e93d-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="4e93d-148">Сообщения электронной почты, отправляемые сброса пароля включает логотип вашей организации, цвета, имя в тексте hello hello электронной почты и настроенные на основе имени.</span><span class="sxs-lookup"><span data-stu-id="4e93d-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="4e93d-149">**Вопрос. как можно направлять пользователей о том, где toogo tooreset свои пароли?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="4e93d-150">**Ответ** toohttps://passwordreset.microsoftonline.com к пользователям можно отправлять непосредственно, или задать их tooclick hello **нет доступа к вашей учетной записи ссылка** на любой работы или учебы страницы входа.</span><span class="sxs-lookup"><span data-stu-id="4e93d-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="4e93d-151">Также можно опубликовать по этим ссылкам пользователи tooyour легкодоступном месте.</span><span class="sxs-lookup"><span data-stu-id="4e93d-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="4e93d-152">**Вопрос. Могу ли я пользоваться этой страницей на мобильном устройстве?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="4e93d-153">**Ответ.** Да. Эта страница работает на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="4e93d-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="4e93d-154">**Вопрос. Поддерживается ли разблокировка учетных записей локальной службы Active Directory, когда пользователи сбрасывают свой пароль?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="4e93d-155">**Ответ.** Да. Если на момент сброса пароля компонент обратной записи паролей уже развернут с помощью Azure AD Connect, учетная запись пользователя будет автоматически разблокирована.</span><span class="sxs-lookup"><span data-stu-id="4e93d-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="4e93d-156">**Вопрос. Как интегрировать функцию сброса паролей напрямую в интерфейс входа на локальный компьютер?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="4e93d-157">**Ответ** Если вы являетесь клиентом Azure AD Premium, можно установить Microsoft Identity Manager без дополнительной платы и развернуть hello локальный пароль сброса решения toomeet это требование.</span><span class="sxs-lookup"><span data-stu-id="4e93d-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="4e93d-158">**Вопрос. Могу ли я настроить разные контрольные вопросы для разных языков?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="4e93d-159">**Ответ.** На сегодняшний день это невозможно.</span><span class="sxs-lookup"><span data-stu-id="4e93d-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="4e93d-160">**В. сколько вопросов можно настроить для проверки подлинности параметра hello контрольные вопросы?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="4e93d-161">**Ответ** можно настроить too20 контрольных вопросов в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e93d-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="4e93d-162">**Вопрос. Какова допустимая длина контрольных вопросов?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="4e93d-163">**Ответ.** Контрольный вопрос должен содержать от 3 до 200 знаков.</span><span class="sxs-lookup"><span data-stu-id="4e93d-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="4e93d-164">**Вопрос. как long может быть ответы toosecurity вопросы**</span><span class="sxs-lookup"><span data-stu-id="4e93d-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="4e93d-165">**Ответ** ответы могут быть 3 знаков too40.</span><span class="sxs-lookup"><span data-stu-id="4e93d-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="4e93d-166">**Вопрос. есть отклонены повторяющиеся ответы toosecurity вопросы?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="4e93d-167">**Ответ** Да, мы отклоняем повторяющиеся ответы toosecurity вопросы.</span><span class="sxs-lookup"><span data-stu-id="4e93d-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="4e93d-168">**Вопрос может зарегистрировать пользователь hello же контрольный вопрос несколько раз?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="4e93d-169">**Ответ.** Нет. Если пользователь зарегистрировал определенный вопрос, он не сможет его еще раз зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="4e93d-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="4e93d-170">**Вопрос. есть его возможных tooset минимальное количество контрольных вопросов для регистрации и сброса?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="4e93d-171">**Ответ.** Да, можно задать одно ограничение для регистрации, а другое — для сброса.</span><span class="sxs-lookup"><span data-stu-id="4e93d-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="4e93d-172">В обоих случаях можно настроить от 3 до 5 контрольных вопросов.</span><span class="sxs-lookup"><span data-stu-id="4e93d-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="4e93d-173">**Вопрос. Если пользователь зарегистрировал hello максимальное количество превышает число необходимых tooreset вопросы, как контрольные вопросы выбираются во время сброса параметров?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="4e93d-174">**Ответ** безопасности N, вопросы выбираются случайным образом из hello общее количество вопросов, пользователь зарегистрировал, где N — hello **количество необходимых tooreset вопросы**.</span><span class="sxs-lookup"><span data-stu-id="4e93d-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="4e93d-175">Например если пользователь зарегистрировал 5 вопросов безопасности, но tooreset обязательным является только 3, 3 из hello 5 выбираются случайным образом и представлены при перезагрузке.</span><span class="sxs-lookup"><span data-stu-id="4e93d-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="4e93d-176">Процесс выбора hello повторится ли hello пользователь получает ответы hello вопросы toohello неправильный, tooprevent подбора ответов.</span><span class="sxs-lookup"><span data-stu-id="4e93d-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="4e93d-177">**Вопрос. Есть ли лимиты, ограничивающие количество попыток сброса пароля за короткий промежуток времени?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="4e93d-178">**Ответ** существуют средства безопасности, встроенные в tooprotect сброс пароля от несанкционированного использования.</span><span class="sxs-lookup"><span data-stu-id="4e93d-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="4e93d-179">Пользователи могут сделать только 5 попыток сброса пароля в течение часа, после чего эта возможность блокируется на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="4e93d-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="4e93d-180">Пользователь может попытаться только toovalidate номер телефона 5 раз в течение часа, после чего попытки блокируются на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="4e93d-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="4e93d-181">Пользователи могут воспользоваться определенным методом проверки подлинности 5 раз в течение часа, после чего эта возможность блокируется на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="4e93d-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="4e93d-182">**Вопрос в том, как долго допустимы hello электронной почты и SMS одноразовый пароль?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="4e93d-183">**Ответ** hello время жизни сеанса для сброса пароля — 105 минут.</span><span class="sxs-lookup"><span data-stu-id="4e93d-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="4e93d-184">От начала hello hello операции сброса пароля, hello пользователя есть 105 минут tooreset свой пароль.</span><span class="sxs-lookup"><span data-stu-id="4e93d-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="4e93d-185">Hello электронной почты и SMS одноразовый пароль являются недопустимыми после истечения этого периода времени.</span><span class="sxs-lookup"><span data-stu-id="4e93d-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="4e93d-186">Изменение пароля</span><span class="sxs-lookup"><span data-stu-id="4e93d-186">Password change</span></span>
* <span data-ttu-id="4e93d-187">**Вопрос. где мои пользователи пойдет toochange свои пароли?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="4e93d-188">**Ответ** пользователи могут изменять свои пароли в любом разделе их профиль рисунок или значок (как и в hello правый верхний угол их [Office 365](https://portal.office.com) или [панели доступа](https://myapps.microsoft.com) возникает.</span><span class="sxs-lookup"><span data-stu-id="4e93d-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="4e93d-189">Пользователи могут изменять свои пароли с hello [страницы панели доступа профиля](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="4e93d-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="4e93d-190">Пользователи также могут быть запрос toochange свои пароли автоматически на экране входа hello Azure AD, если истек срок действия паролей.</span><span class="sxs-lookup"><span data-stu-id="4e93d-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="4e93d-191">Наконец, пользователи могут перемещаться toohello [портал изменения паролей Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) непосредственно по желанию toochange свои пароли.</span><span class="sxs-lookup"><span data-stu-id="4e93d-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="4e93d-192">**Вопрос моим пользователям уведомления hello портала Office после истечения срока действия пароля в локальной среде?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="4e93d-193">**Ответ** это можно сделать сегодня при использовании служб федерации Active Directory, следуя инструкциям hello: [отправки утверждений политики пароля с помощью служб федерации Active Directory](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="4e93d-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="4e93d-194">Если вы используете синхронизацию хэша паролей, сейчас вы не сможете настроить отправку уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4e93d-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="4e93d-195">Так как не выполнять синхронизацию политиками паролей из локальной, поэтому невозможно нам toocloud уведомления об истечении срока действия toopost возникает.</span><span class="sxs-lookup"><span data-stu-id="4e93d-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="4e93d-196">В любом случае можно также слишком[уведомите пользователей, чьи пароли будут tooexpire с помощью PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e93d-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="4e93d-197">Отчеты об управлении паролями</span><span class="sxs-lookup"><span data-stu-id="4e93d-197">Password management reports</span></span>
* <span data-ttu-id="4e93d-198">**Вопрос. как времени требуется для tooshow данных вверх на hello отчеты по управлению паролями?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="4e93d-199">**Ответ** данные должны появляться в отчетах по управлению паролями hello в течение 5 – 10 минут.</span><span class="sxs-lookup"><span data-stu-id="4e93d-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="4e93d-200">Он иногда это может потребоваться до часа tooappear tooan.</span><span class="sxs-lookup"><span data-stu-id="4e93d-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="4e93d-201">**Вопрос. как можно фильтровать отчеты по управлению паролями hello**</span><span class="sxs-lookup"><span data-stu-id="4e93d-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="4e93d-202">**Ответ** можно фильтровать отчеты по управлению паролями hello, щелкнув hello небольшой значок лупы toohello справа от названия столбцов hello, вверху hello hello отчета.</span><span class="sxs-lookup"><span data-stu-id="4e93d-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="4e93d-203">Если требуется более сложной фильтрации toodo, можно загрузить отчет tooexcel hello и создать сводную таблицу.</span><span class="sxs-lookup"><span data-stu-id="4e93d-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="4e93d-204">**Вопрос. Какова hello максимальное число событий хранятся в отчетах по управлению паролями hello?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="4e93d-205">**Ответ** копирование too75, 000 пароль сброса пароля сброса регистрации событий или хранятся в hello отчеты по управлению паролями, охват резервное копирование too30 дней.</span><span class="sxs-lookup"><span data-stu-id="4e93d-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="4e93d-206">Мы активно работаем над tooexpand это число tooinclude дополнительные события.</span><span class="sxs-lookup"><span data-stu-id="4e93d-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="4e93d-207">**Вопрос. временной промежуток go hello отчеты по управлению паролями?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="4e93d-208">**Ответ** hello пароль отчеты об управлении Показать операции, произошедшие за hello последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="4e93d-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="4e93d-209">При необходимости tooarchive эти данные теперь можно периодически загрузить отчеты hello и сохранить их в другом месте.</span><span class="sxs-lookup"><span data-stu-id="4e93d-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="4e93d-210">**Вопрос. есть ли максимальное количество строк, которые могут отображаться в отчетах по управлению паролями hello?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="4e93d-211">**Ответ** Да, может появиться более 75 000 строк на одном из отчеты об управлении паролями hello ли они отображаются hello пользовательского интерфейса или загрузке.</span><span class="sxs-lookup"><span data-stu-id="4e93d-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="4e93d-212">**Вопрос. есть ли API tooaccess hello пароль сброса или регистрации данных отчетов?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="4e93d-213">**Ответ** Да см. в разделе hello следующие toolearn документации способ доступа к пароль hello сбросить отчетов потока данных.</span><span class="sxs-lookup"><span data-stu-id="4e93d-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="4e93d-214">[Узнайте, как tooaccess события сброса пароля отчетов программным образом](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="4e93d-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="4e93d-215">Обратная запись паролей</span><span class="sxs-lookup"><span data-stu-id="4e93d-215">Password writeback</span></span>
* <span data-ttu-id="4e93d-216">**Вопрос. как работает обратная запись паролей фоновом hello?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="4e93d-217">**Ответ** разделе [как работает обратная запись паролей](active-directory-passwords-writeback.md) для пояснения о том, что происходит, если включена обратная запись паролей и потоки данных через систему hello обратно в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="4e93d-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="4e93d-218">**Вопрос. как долго обратной записи паролей может быть toowork?  Существует ли задержка синхронизации, как при синхронизации хэша паролей?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="4e93d-219">**Ответ.** Обратная запись паролей происходит мгновенно.</span><span class="sxs-lookup"><span data-stu-id="4e93d-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="4e93d-220">Для этого используется синхронный конвейер, принцип работы которого принципиально отличается от синхронизации хэша паролей.</span><span class="sxs-lookup"><span data-stu-id="4e93d-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="4e93d-221">Обратной записи паролей пользователи tooget Своевременная информация об успешности hello свой пароль, сбросить или изменить операцию.</span><span class="sxs-lookup"><span data-stu-id="4e93d-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="4e93d-222">Среднее время успешной обратной записи пароля Hello составляет менее 500 мс.</span><span class="sxs-lookup"><span data-stu-id="4e93d-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="4e93d-223">**Вопрос. Если локальная учетная запись отключена, повлияет ли это на учетную запись или доступ к облаку?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="4e93d-224">**Ответ** свой идентификатор в локальной среде при отключении облако с Идентификатором, доступ будет также отключена по hello следующего интервала синхронизации через AAD Connect бай по умолчанию это каждые 30 минут.</span><span class="sxs-lookup"><span data-stu-id="4e93d-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="4e93d-225">**Вопрос. Если Моя учетная запись локальной ограничена политики паролей в локальной Active Directory, SSPR подчиняются этой политики при изменении пароля hello?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="4e93d-226">**Ответ** Да, зависит от SSPR и не зависящим от hello локальной политики паролей AD, включая стандартные политики паролей домена AD, а также любые определенные политики пароля детально настроенную целевые tooa заданного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4e93d-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="4e93d-227">**Вопрос. Для каких типов учетных записей работает обратная запись паролей?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="4e93d-228">**Ответ.** Обратная запись паролей может применяться для федеративных пользователей и пользователей с синхронизацией хэша пароля.</span><span class="sxs-lookup"><span data-stu-id="4e93d-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="4e93d-229">**Вопрос. Соблюдает ли служба обратной записи паролей политики, применяемые к паролям в моем домене?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="4e93d-230">**Ответ.** Да, компонент обратной записи паролей соблюдает настройки срока действия пароля, журнала, сложности, фильтров и другие ограничения, установленные для паролей в локальном домене.</span><span class="sxs-lookup"><span data-stu-id="4e93d-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="4e93d-231">**Вопрос. Защищена ли служба обратной записи паролей?  Насколько можно быть уверенным, что ее не взломают?**</span><span class="sxs-lookup"><span data-stu-id="4e93d-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="4e93d-232">**Ответ.** Да, компонент обратной записи паролей защищен.</span><span class="sxs-lookup"><span data-stu-id="4e93d-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="4e93d-233">tooread Дополнительные сведения о hello четыре уровня безопасности, реализованный hello служба обратной записи паролей, ознакомьтесь с hello [модель безопасности обратной записи паролей](active-directory-passwords-writeback.md#password-writeback-security-model) раздела как работает обратная запись паролей.</span><span class="sxs-lookup"><span data-stu-id="4e93d-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="4e93d-234">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e93d-234">Next steps</span></span>

<span data-ttu-id="4e93d-235">Привет, следующие ссылки предоставляют дополнительную информацию об пароль с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e93d-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="4e93d-236">[**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e93d-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="4e93d-237">[**Licensing requirements for Azure AD self-service password reset**](active-directory-passwords-licensing.md) (Требования к лицензированию самостоятельного сброса пароля в Azure AD). Сведения о настройке лицензирования Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e93d-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="4e93d-238">[**Данные** ](active-directory-passwords-data.md) — понять hello данные, которые не требуется и как она используется для управления паролями</span><span class="sxs-lookup"><span data-stu-id="4e93d-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="4e93d-239">[**Развертывание** ](active-directory-passwords-best-practices.md) -планирование и развертывание SSPR tooyour пользователей с помощью hello рекомендации по следующему адресу</span><span class="sxs-lookup"><span data-stu-id="4e93d-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="4e93d-240">[**Настройка** ](active-directory-passwords-customize.md) -настроить hello внешний вид и поведение hello SSPR взаимодействие с вашей компании.</span><span class="sxs-lookup"><span data-stu-id="4e93d-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="4e93d-241">[**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.</span><span class="sxs-lookup"><span data-stu-id="4e93d-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="4e93d-242">[**Политики и ограничения для паролей в Azure Active Directory**](active-directory-passwords-policy.md). Общие сведения и информация об установке политик паролей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e93d-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="4e93d-243">[**Обзор компонента обратной записи паролей**](active-directory-passwords-writeback.md). Как работает функция обратной записи паролей с вашим локальным каталогом.</span><span class="sxs-lookup"><span data-stu-id="4e93d-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="4e93d-244">[**Технические глубокое погружение** ](active-directory-passwords-how-it-works.md) -перейдите за занавесом toounderstand hello принцип работы</span><span class="sxs-lookup"><span data-stu-id="4e93d-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="4e93d-245">[**Устранение неполадок** ](active-directory-passwords-troubleshoot.md) -Узнайте, как tooresolve распространенные проблемы, мы увидим с SSPR</span><span class="sxs-lookup"><span data-stu-id="4e93d-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
