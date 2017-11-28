---
title: "aaaProblems вход в приложение не коллекции tooa, настроенное для федеративного единого входа | Документы Microsoft"
description: "Руководство по hello конкретных проблем, с которыми может столкнуться при входе в приложение tooan, настроенное на основе SAML федеративного единого входа в Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="d9650-103">Проблемы со входом в приложение без коллекции tooa, настроенное для федеративного единого входа</span><span class="sxs-lookup"><span data-stu-id="d9650-103">Problems signing in tooa non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="d9650-104">tootroubleshoot проблему, необходимо tooverify конфигурации приложения hello в Azure AD выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d9650-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="d9650-105">Были выполнены все действия по настройке hello для hello коллекции приложений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9650-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="d9650-106">они ожидаемые значения в приложении hello соответствует Hello идентификатора и URL-адрес ответа, настроенного в AAD</span><span class="sxs-lookup"><span data-stu-id="d9650-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="d9650-107">Назначенные пользователи toohello приложения</span><span class="sxs-lookup"><span data-stu-id="d9650-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="d9650-108">Приложение не найдено в каталоге</span><span class="sxs-lookup"><span data-stu-id="d9650-108">Application not found in directory</span></span>

<span data-ttu-id="d9650-109">*Ошибка AADSTS70001: Приложение с идентификатором «https://contoso.com» не найден в каталоге hello*.</span><span class="sxs-lookup"><span data-stu-id="d9650-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="d9650-110">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="d9650-110">**Possible cause**</span></span>

<span data-ttu-id="d9650-111">атрибут Hello издатель отправляет из tooAzure приложения hello AD в запросе SAML hello не соответствует значение идентификатора hello, настроенной в приложения hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9650-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="d9650-112">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="d9650-112">**Resolution**</span></span>

<span data-ttu-id="d9650-113">Убедитесь, этот атрибут издателя hello в запросе SAML hello, что он сопоставление hello значение идентификатора, настроенные в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d9650-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="d9650-114">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="d9650-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d9650-115">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d9650-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d9650-116">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d9650-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d9650-117">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d9650-118">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d9650-118">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d9650-119">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="d9650-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d9650-120">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="d9650-120">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d9650-121">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d9650-122"><span id="_Hlk477190042" class="anchor"></span>Go слишком**URL-адреса и домена** раздела.</span><span class="sxs-lookup"><span data-stu-id="d9650-122"><span id="_Hlk477190042" class="anchor"></span>Go too**Domain and URLs** section.</span></span> <span data-ttu-id="d9650-123">Убедитесь, что значение hello в hello идентификатором, текстового поля соответствующим hello значение отображается по ошибке hello значение идентификатора hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="d9650-124">После обновления значение идентификатора hello в Azure AD и отправляет его сопоставления hello значение приложением hello в запросе SAML hello, можно будет toosign toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d9650-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="d9650-125">обратный адрес Hello не соответствует hello адреса ответа, настроенного для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-125">hello reply address does not match hello reply addresses configured for hello application.</span></span> 

<span data-ttu-id="d9650-126">*Ошибка AADSTS50011: hello обратный адрес «https://contoso.com» не соответствует hello адреса ответа, настроенного для приложения hello*</span><span class="sxs-lookup"><span data-stu-id="d9650-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span> 

<span data-ttu-id="d9650-127">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="d9650-127">**Possible cause**</span></span> 

<span data-ttu-id="d9650-128">Hello AssertionConsumerServiceURL значение в запросе SAML hello не соответствует значение URL-адрес ответа hello или шаблон, настроенный в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9650-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="d9650-129">Hello AssertionConsumerServiceURL значение в запросе SAML hello — hello URL-адрес, содержатся в ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span> 

<span data-ttu-id="d9650-130">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="d9650-130">**Resolution**</span></span> 

<span data-ttu-id="d9650-131">Убедитесь, что значение AssertionConsumerServiceURL hello в запросе SAML hello, его сопоставления hello значение URL-адрес ответа, настроенные в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9650-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="d9650-132">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="d9650-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="d9650-133">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d9650-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="d9650-134">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d9650-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="d9650-135">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="d9650-136">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d9650-136">click **All Applications** tooview a list of all your applications.</span></span> 

  * <span data-ttu-id="d9650-137">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="d9650-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and       set hello **Show** option too**All Applications.**</span></span>
  
6.  <span data-ttu-id="d9650-138">Выберите hello приложение tooconfigure единого входа</span><span class="sxs-lookup"><span data-stu-id="d9650-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="d9650-139">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d9650-140">Go слишком**URL-адреса и домена** раздела.</span><span class="sxs-lookup"><span data-stu-id="d9650-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="d9650-141">Проверьте или измените значение hello в hello URL-адрес ответа textbox toomatch hello AssertionConsumerServiceURL значение в запросе SAML hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>

  * <span data-ttu-id="d9650-142">Если вы не видите текстовое поле URL-адрес ответа hello, выберите hello **Показывать дополнительные параметры URL-адреса** флажок.</span><span class="sxs-lookup"><span data-stu-id="d9650-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="d9650-143">После обновления значение URL-адрес ответа hello в Azure AD, и он имеет соответствующих значению hello отправляет приложением hello в hello запрос SAML, должен быть доступ toosign toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d9650-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="d9650-144">Не назначена роль пользователя</span><span class="sxs-lookup"><span data-stu-id="d9650-144">User not assigned a role</span></span>

<span data-ttu-id="d9650-145">*Ошибка AADSTS50105: hello вход пользователя "brian@contoso.com" не назначена роль tooa для приложения hello*</span><span class="sxs-lookup"><span data-stu-id="d9650-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*</span></span>

<span data-ttu-id="d9650-146">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="d9650-146">**Possible cause**</span></span>

<span data-ttu-id="d9650-147">Hello пользователь не имеет доступа toohello приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9650-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="d9650-148">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="d9650-148">**Resolution**</span></span>

<span data-ttu-id="d9650-149">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d9650-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="d9650-150">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="d9650-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d9650-151">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d9650-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d9650-152">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d9650-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d9650-153">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d9650-154">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d9650-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d9650-155">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="d9650-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d9650-156">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="d9650-157">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d9650-158">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="d9650-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d9650-159">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="d9650-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d9650-160">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="d9650-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d9650-161">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="d9650-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="d9650-162">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="d9650-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="d9650-163">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="d9650-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="d9650-164">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="d9650-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="d9650-165">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="d9650-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="d9650-166">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="d9650-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="d9650-167">После краткого периода времени hello пользователей, которые вы выбрали быть может toolaunch эти приложения используют hello методов, описанных в разделе описания решений hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="d9650-168">Недопустимый запрос SAML</span><span class="sxs-lookup"><span data-stu-id="d9650-168">Not a valid SAML Request</span></span>

<span data-ttu-id="d9650-169">*Ошибка AADSTS75005: hello запрос не допустимое сообщение протокола Saml2.*</span><span class="sxs-lookup"><span data-stu-id="d9650-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="d9650-170">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="d9650-170">**Possible cause**</span></span>

<span data-ttu-id="d9650-171">Azure AD не поддерживает hello SAML запросов, отправляемых приложением, hello единым входом.</span><span class="sxs-lookup"><span data-stu-id="d9650-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="d9650-172">К наиболее распространенным проблемам относятся:</span><span class="sxs-lookup"><span data-stu-id="d9650-172">Some common issues are:</span></span>

-   <span data-ttu-id="d9650-173">Отсутствуют обязательные поля в запросе SAML hello</span><span class="sxs-lookup"><span data-stu-id="d9650-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="d9650-174">Метод кодировки запроса SAML</span><span class="sxs-lookup"><span data-stu-id="d9650-174">SAML request encoded method</span></span>

<span data-ttu-id="d9650-175">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="d9650-175">**Resolution**</span></span>

1.  <span data-ttu-id="d9650-176">Захватите запрос SAML.</span><span class="sxs-lookup"><span data-stu-id="d9650-176">Capture SAML request.</span></span> <span data-ttu-id="d9650-177">выполните действия из учебника hello [как toodebug на основе SAML единого входа tooapplications в Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn способ запроса toocapture hello SAML.</span><span class="sxs-lookup"><span data-stu-id="d9650-177">follow hello tutorial on [how toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="d9650-178">Обратитесь к поставщику приложения hello и общую папку:</span><span class="sxs-lookup"><span data-stu-id="d9650-178">Contact hello application vendor and share:</span></span>

    -   <span data-ttu-id="d9650-179">Запрос SAML</span><span class="sxs-lookup"><span data-stu-id="d9650-179">SAML request</span></span>

    -   [<span data-ttu-id="d9650-180">Требования к протоколу SAML единого входа в Azure</span><span class="sxs-lookup"><span data-stu-id="d9650-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="d9650-181">Они должны проверить их поддержки реализации hello Azure AD SAML для единого входа.</span><span class="sxs-lookup"><span data-stu-id="d9650-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="d9650-182">Нет ресурсов в списке requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="d9650-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="d9650-183">*Ошибка AADSTS65005: hello клиентское приложение запросило tooresource доступа "00000002-0000-0000-c000-000000000000'. Этот запрос не выполнено, поскольку hello клиент не указал этот ресурс в своем списке requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="d9650-183">*Error AADSTS65005: hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="d9650-184">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="d9650-184">**Possible cause**</span></span>

<span data-ttu-id="d9650-185">объект приложения Hello поврежден.</span><span class="sxs-lookup"><span data-stu-id="d9650-185">hello application object is corrupted.</span></span>

<span data-ttu-id="d9650-186">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="d9650-186">**Resolution**</span></span>

<span data-ttu-id="d9650-187">toosolve hello проблему, удалите приложение hello из каталога hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-187">toosolve hello problem, remove hello application from hello directory.</span></span> <span data-ttu-id="d9650-188">Добавьте и перенастройте приложение hello, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="d9650-188">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d9650-189">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="d9650-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d9650-190">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d9650-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d9650-191">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d9650-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d9650-192">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d9650-193">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d9650-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d9650-194">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="d9650-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d9650-195">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="d9650-195">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d9650-196">Нажмите кнопку **удаление** в hello верхней левой части приложения hello **Обзор** колонку.</span><span class="sxs-lookup"><span data-stu-id="d9650-196">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="d9650-197">Обновление Azure AD и добавьте приложение hello из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9650-197">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="d9650-198">Затем настройте приложение hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="d9650-198">Then, Configure hello application again.</span></span>

<span data-ttu-id="d9650-199">После перенастройки приложения hello, должен быть доступ toosign toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d9650-199">After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="d9650-200">Не настроен сертификат или ключ</span><span class="sxs-lookup"><span data-stu-id="d9650-200">Certificate or key not configured</span></span>

<span data-ttu-id="d9650-201">Ошибка AADSTS50003: не настроен ключ подписывания.</span><span class="sxs-lookup"><span data-stu-id="d9650-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="d9650-202">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="d9650-202">**Possible cause**</span></span>

<span data-ttu-id="d9650-203">поврежден объект приложения Hello и Azure AD не распознает hello сертификата, настроенного для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-203">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="d9650-204">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="d9650-204">**Resolution**</span></span>

<span data-ttu-id="d9650-205">toodelete и создать новый сертификат, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d9650-205">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="d9650-206">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="d9650-206">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d9650-207">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d9650-207">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d9650-208">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d9650-208">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d9650-209">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-209">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d9650-210">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d9650-210">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d9650-211">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="d9650-211">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d9650-212">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="d9650-212">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d9650-213">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d9650-213">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d9650-214">Нажмите кнопку **Создание нового сертификата** под hello **SAML сертификат подписи** раздела.</span><span class="sxs-lookup"><span data-stu-id="d9650-214">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="d9650-215">Выберите срок действия.</span><span class="sxs-lookup"><span data-stu-id="d9650-215">Select Expiration date.</span></span> <span data-ttu-id="d9650-216">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d9650-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="d9650-217">Проверьте **активировать новый сертификат** сертификата active toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-217">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="d9650-218">Нажмите кнопку **Сохранить** hello верхней части колонки hello и принять сертификат продолжения tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="d9650-218">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="d9650-219">В разделе hello **сертификат подписи SAML** щелкните **удалить** tooremove hello **не используется** сертификат.</span><span class="sxs-lookup"><span data-stu-id="d9650-219">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="d9650-220">Проблемы при настройке утверждения SAML hello отправлено tooan приложения</span><span class="sxs-lookup"><span data-stu-id="d9650-220">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="d9650-221">toolearn toocustomize hello SAML атрибут отправлять утверждений приложения tooyour разделе [утверждения сопоставления в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d9650-221">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9650-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9650-222">Next steps</span></span>
[<span data-ttu-id="d9650-223">Требования к протоколу SAML единого входа в Azure</span><span class="sxs-lookup"><span data-stu-id="d9650-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
