---
title: "Элементы сообщения с приглашением службы совместной работы Azure Active Directory B2B | Документация Майкрософт"
description: "Шаблон сообщения с приглашением в службу совместной работы Azure Active Directory B2B"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="dc13f-103">Элементы сообщения с приглашением в службу совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="dc13f-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="dc13f-104">Сообщение с приглашением является важнейшим компонентом, необходимым для подключения партнеров в качестве пользователей службы совместной работы B2B в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc13f-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="dc13f-105">Их можно использовать, чтобы повысить уровень доверия получателя.</span><span class="sxs-lookup"><span data-stu-id="dc13f-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="dc13f-106">Вы можете придать сообщению законность и социальную значимость, чтобы получатель был спокоен, нажимая кнопку **Начало работы** и принимая приглашение.</span><span class="sxs-lookup"><span data-stu-id="dc13f-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="dc13f-107">Это доверие является ключевым компонентом в процессе налаживания совместной работы.</span><span class="sxs-lookup"><span data-stu-id="dc13f-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="dc13f-108">И, конечно же, вам бы хотелось, чтобы это сообщение отлично выглядело!</span><span class="sxs-lookup"><span data-stu-id="dc13f-108">And you also want to make the email look great!</span></span>

![Сообщение с приглашением в службу Azure AD B2B](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="dc13f-110">Из чего состоит сообщение</span><span class="sxs-lookup"><span data-stu-id="dc13f-110">Explaining the email</span></span>
<span data-ttu-id="dc13f-111">Давайте рассмотрим основные элементы сообщения, чтобы понять, как лучше использовать их возможности.</span><span class="sxs-lookup"><span data-stu-id="dc13f-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="dc13f-112">Субъект</span><span class="sxs-lookup"><span data-stu-id="dc13f-112">Subject</span></span>
<span data-ttu-id="dc13f-113">Тема сообщения имеет следующий формат: "Вас приглашает организация &lt;имя_клиента&gt;".</span><span class="sxs-lookup"><span data-stu-id="dc13f-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="dc13f-114">Адрес отправителя</span><span class="sxs-lookup"><span data-stu-id="dc13f-114">From address</span></span>
<span data-ttu-id="dc13f-115">Для адреса отправителя используется формат, аналогичный сети LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="dc13f-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="dc13f-116">Вам необходимо четко указать, кто приглашает и из какой компании, а также пояснить, что сообщение поступило с адреса электронной почты Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="dc13f-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="dc13f-117">Получается следующий формат: "&lt;Отображаемое имя приглашающего&gt; из &lt;имя_клиента&gt; (с помощью Майкрософт) <invites@microsoft.com&gt;".</span><span class="sxs-lookup"><span data-stu-id="dc13f-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="dc13f-118">Ответить</span><span class="sxs-lookup"><span data-stu-id="dc13f-118">Reply To</span></span>
<span data-ttu-id="dc13f-119">В поле обратного адреса указывается адрес электронной почты приглашающего (если доступен). Таким образом, ответ на полученное сообщение будет отправлен приглашающему клиенту.</span><span class="sxs-lookup"><span data-stu-id="dc13f-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="dc13f-120">Фирменная символика</span><span class="sxs-lookup"><span data-stu-id="dc13f-120">Branding</span></span>
<span data-ttu-id="dc13f-121">В сообщениях с приглашением от клиента может использоваться фирменная символика компании, если ее настроить для клиента.</span><span class="sxs-lookup"><span data-stu-id="dc13f-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="dc13f-122">Если вы хотите воспользоваться этой возможностью, то [здесь](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) описано, как настроить использование фирменной символики.</span><span class="sxs-lookup"><span data-stu-id="dc13f-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="dc13f-123">В сообщении будет отображаться баннер с логотипом.</span><span class="sxs-lookup"><span data-stu-id="dc13f-123">The banner logo appears in the email.</span></span> <span data-ttu-id="dc13f-124">Для получения оптимальных результатов следуйте приведенным [здесь](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) инструкциям по настройке размера и качества изображения.</span><span class="sxs-lookup"><span data-stu-id="dc13f-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="dc13f-125">Кроме того, в призыве к действию также указывается имя компании.</span><span class="sxs-lookup"><span data-stu-id="dc13f-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="dc13f-126">Призыв к действию</span><span class="sxs-lookup"><span data-stu-id="dc13f-126">Call to action</span></span>
<span data-ttu-id="dc13f-127">Призыв к действию состоит из двух частей: первая поясняет, почему получатель получил это сообщение, а во второй получателю предлагается что-то сделать.</span><span class="sxs-lookup"><span data-stu-id="dc13f-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="dc13f-128">В первой части ("почему") можно обратиться к получателю, используя такой формат: "Организация &lt;имя_клиента&gt; приглашает Вас воспользоваться доступом к приложениям".</span><span class="sxs-lookup"><span data-stu-id="dc13f-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="dc13f-129">А во второй части ("что предлагается сделать") расположена кнопка **Начало работы**.</span><span class="sxs-lookup"><span data-stu-id="dc13f-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="dc13f-130">Если получатель уже добавлен и нет необходимости в отправке приглашения, то эта кнопка не отображается.</span><span class="sxs-lookup"><span data-stu-id="dc13f-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="dc13f-131">Сведения о приглашающем</span><span class="sxs-lookup"><span data-stu-id="dc13f-131">Inviter's information</span></span>
<span data-ttu-id="dc13f-132">Отображаемое имя приглашающего включено в сообщение.</span><span class="sxs-lookup"><span data-stu-id="dc13f-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="dc13f-133">Если вы настроили для своей учетной записи Azure AD изображение профиля, то в сообщение с приглашением также будет включено это изображение.</span><span class="sxs-lookup"><span data-stu-id="dc13f-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="dc13f-134">Эти элементы предназначены, чтобы повысить уровень доверия получателя к сообщению.</span><span class="sxs-lookup"><span data-stu-id="dc13f-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="dc13f-135">Если вы еще не настроили изображение профиля, вместо него отобразится значок с инициалами приглашающего.</span><span class="sxs-lookup"><span data-stu-id="dc13f-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![отображение инициалов приглашающего](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="dc13f-137">Текст</span><span class="sxs-lookup"><span data-stu-id="dc13f-137">Body</span></span>
<span data-ttu-id="dc13f-138">Текст сообщения, составленный приглашающим или переданный с помощью API приглашения.</span><span class="sxs-lookup"><span data-stu-id="dc13f-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="dc13f-139">Это текстовое поле, поэтому в целях безопасности в нем не обрабатываются HTML-теги.</span><span class="sxs-lookup"><span data-stu-id="dc13f-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="dc13f-140">Нижний колонтитул</span><span class="sxs-lookup"><span data-stu-id="dc13f-140">Footer section</span></span>
<span data-ttu-id="dc13f-141">В нижнем колонтитуле содержится фирменная символика корпорации Майкрософт, поэтому получатель узнает, если для отправки сообщения использовался неотслеживаемый псевдоним.</span><span class="sxs-lookup"><span data-stu-id="dc13f-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="dc13f-142">Особые случаи:</span><span class="sxs-lookup"><span data-stu-id="dc13f-142">Special cases:</span></span>

- <span data-ttu-id="dc13f-143">В приглашающем клиенте не указан адрес электронной почты приглашающего</span><span class="sxs-lookup"><span data-stu-id="dc13f-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![снимок экрана: в приглашающем клиенте не указан адрес электронной почты приглашающего](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="dc13f-145">Получателю не нужно активировать приглашение</span><span class="sxs-lookup"><span data-stu-id="dc13f-145">The recipient doesn't need to redeem the invitation</span></span>

  ![когда получателю не нужно активировать приглашение](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="dc13f-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc13f-147">Next steps</span></span>

<span data-ttu-id="dc13f-148">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="dc13f-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="dc13f-149">Что такое предварительная версия службы совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="dc13f-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="dc13f-150">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="dc13f-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="dc13f-151">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc13f-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="dc13f-152">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="dc13f-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="dc13f-153">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="dc13f-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="dc13f-154">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="dc13f-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="dc13f-155">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="dc13f-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="dc13f-156">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="dc13f-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="dc13f-157">Многофакторная идентификация для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="dc13f-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="dc13f-158">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="dc13f-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="dc13f-159">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc13f-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
