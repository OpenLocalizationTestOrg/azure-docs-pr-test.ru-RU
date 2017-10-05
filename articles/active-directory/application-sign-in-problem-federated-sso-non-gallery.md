---
title: "Проблемы с входом в приложение не из коллекции, для которого настроен федеративный единый вход | Документы Майкрософт"
description: "Рекомендации по конкретным проблемам при входе в приложение, для которого настроен федеративный единый вход на базе SAML с помощью Azure AD"
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
ms.openlocfilehash: 3afc7bca878caef424d3fa3c64aa17df0fda7de5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="4b940-103">Проблемы с входом в приложение не из коллекции, для которого настроен федеративный единый вход</span><span class="sxs-lookup"><span data-stu-id="4b940-103">Problems signing in to a non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="4b940-104">Чтобы устранить проблему, нужно проверить конфигурации приложения в Azure AD следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4b940-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="4b940-105">Выполнены все действия по настройке для приложения из коллекции Azure.</span><span class="sxs-lookup"><span data-stu-id="4b940-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="4b940-106">Идентификатор и URL-адрес ответа, настроенные в AAD, совпадают с ожидаемыми значениями в приложении.</span><span class="sxs-lookup"><span data-stu-id="4b940-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="4b940-107">Для приложения назначены пользователи.</span><span class="sxs-lookup"><span data-stu-id="4b940-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="4b940-108">Приложение не найдено в каталоге</span><span class="sxs-lookup"><span data-stu-id="4b940-108">Application not found in directory</span></span>

<span data-ttu-id="4b940-109">*Ошибка AADSTS70001: приложение с идентификатором "https://contoso.com" не найдено в каталоге*.</span><span class="sxs-lookup"><span data-stu-id="4b940-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="4b940-110">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="4b940-110">**Possible cause**</span></span>

<span data-ttu-id="4b940-111">Атрибут Issuer, отправляемый из приложения в Azure AD в запросе SAML, не соответствует значению идентификатора, настроенному в приложении Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b940-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="4b940-112">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="4b940-112">**Resolution**</span></span>

<span data-ttu-id="4b940-113">Убедитесь, что атрибут Issuer в запросе SAML совпадает со значением идентификатора, настроенным в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4b940-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="4b940-114">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4b940-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4b940-115">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4b940-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b940-116">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b940-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b940-117">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b940-118">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4b940-118">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4b940-119">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4b940-120">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4b940-120">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4b940-121">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4b940-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4b940-122"><span id="_Hlk477190042" class="anchor"></span>Перейдите в раздел **Домены и URL-адреса приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-122"><span id="_Hlk477190042" class="anchor"></span>Go to **Domain and URLs** section.</span></span> <span data-ttu-id="4b940-123">Убедитесь, что значение в поле "Идентификатор" совпадает со значением идентификатора в сообщении об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4b940-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="4b940-124">После обновления значения идентификатора в Azure AD, чтобы его подходящее значение отправлялось приложением в запросе SAML, вход в приложение должен заработать.</span><span class="sxs-lookup"><span data-stu-id="4b940-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="4b940-125">Адрес ответа не соответствует адресам ответа, настроенным для приложения.</span><span class="sxs-lookup"><span data-stu-id="4b940-125">The reply address does not match the reply addresses configured for the application.</span></span> 

<span data-ttu-id="4b940-126">*Ошибка AADSTS50011: адрес ответа "https://contoso.com" не соответствует адресам ответа, настроенным для приложения*.</span><span class="sxs-lookup"><span data-stu-id="4b940-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span> 

<span data-ttu-id="4b940-127">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="4b940-127">**Possible cause**</span></span> 

<span data-ttu-id="4b940-128">Значение AssertionConsumerServiceURL в запросе SAML не соответствует значению URL-адреса ответа или шаблону, настроенному в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b940-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="4b940-129">Значение AssertionConsumerServiceURL в запросе SAML является URL-адресом, отображаемым в сообщении об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4b940-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span> 

<span data-ttu-id="4b940-130">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="4b940-130">**Resolution**</span></span> 

<span data-ttu-id="4b940-131">Проверьте, что значение AssertionConsumerServiceURL в запросе SAML соответствует значению URL-адреса ответа, настроенному в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b940-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="4b940-132">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4b940-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="4b940-133">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4b940-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="4b940-134">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b940-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="4b940-135">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="4b940-136">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4b940-136">click **All Applications** to view a list of all your applications.</span></span> 

  * <span data-ttu-id="4b940-137">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and       set the **Show** option to **All Applications.**</span></span>
  
6.  <span data-ttu-id="4b940-138">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4b940-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="4b940-139">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4b940-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4b940-140">Перейдите в раздел **Домены и URL-адреса приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="4b940-141">Проверьте или измените значение в текстовом поле "URL-адрес ответа" в соответствии со значением AssertionConsumerServiceURL в запросе SAML.</span><span class="sxs-lookup"><span data-stu-id="4b940-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>

  * <span data-ttu-id="4b940-142">Если текстовое поле "URL-адрес ответа" не отображается, установите флажок **Показывать дополнительные параметры URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="4b940-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="4b940-143">После обновления значения URL-адреса ответа в Azure AD, чтобы его подходящее значение отправлялось приложением в запросе SAML, вход в приложение должен заработать.</span><span class="sxs-lookup"><span data-stu-id="4b940-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="4b940-144">Не назначена роль пользователя</span><span class="sxs-lookup"><span data-stu-id="4b940-144">User not assigned a role</span></span>

<span data-ttu-id="4b940-145">*Ошибка AADSTS50105: выполнившему вход пользователю "brian@contoso.com" не назначена роль для приложения*.</span><span class="sxs-lookup"><span data-stu-id="4b940-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*</span></span>

<span data-ttu-id="4b940-146">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="4b940-146">**Possible cause**</span></span>

<span data-ttu-id="4b940-147">Пользователю не предоставлен доступ к приложению в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b940-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="4b940-148">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="4b940-148">**Resolution**</span></span>

<span data-ttu-id="4b940-149">Чтобы напрямую назначить одного или нескольких пользователей для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4b940-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="4b940-150">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="4b940-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4b940-151">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4b940-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b940-152">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b940-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b940-153">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b940-154">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4b940-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4b940-155">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4b940-156">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="4b940-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="4b940-157">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4b940-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4b940-158">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4b940-159">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4b940-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4b940-160">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="4b940-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4b940-161">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="4b940-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="4b940-162">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4b940-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="4b940-163">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="4b940-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="4b940-164">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="4b940-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="4b940-165">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="4b940-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="4b940-166">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="4b940-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="4b940-167">Через некоторое время выбранные пользователи смогут запускать эти приложения с помощью методов, приведенных в описании решения.</span><span class="sxs-lookup"><span data-stu-id="4b940-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="4b940-168">Недопустимый запрос SAML</span><span class="sxs-lookup"><span data-stu-id="4b940-168">Not a valid SAML Request</span></span>

<span data-ttu-id="4b940-169">*Ошибка AADSTS75005: запрос не является допустимым сообщением протокола Saml2*.</span><span class="sxs-lookup"><span data-stu-id="4b940-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="4b940-170">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="4b940-170">**Possible cause**</span></span>

<span data-ttu-id="4b940-171">Azure AD не поддерживает запрос SAML, отправленный приложением для единого входа.</span><span class="sxs-lookup"><span data-stu-id="4b940-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="4b940-172">К наиболее распространенным проблемам относятся:</span><span class="sxs-lookup"><span data-stu-id="4b940-172">Some common issues are:</span></span>

-   <span data-ttu-id="4b940-173">Отсутствие обязательных полей в запросе SAML</span><span class="sxs-lookup"><span data-stu-id="4b940-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="4b940-174">Метод кодировки запроса SAML</span><span class="sxs-lookup"><span data-stu-id="4b940-174">SAML request encoded method</span></span>

<span data-ttu-id="4b940-175">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="4b940-175">**Resolution**</span></span>

1.  <span data-ttu-id="4b940-176">Захватите запрос SAML.</span><span class="sxs-lookup"><span data-stu-id="4b940-176">Capture SAML request.</span></span> <span data-ttu-id="4b940-177">Сведения о захвате запроса SAML см. в учебнике [Отладка единого входа на основе SAML в приложения в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="4b940-177">follow the tutorial on [how to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="4b940-178">Свяжитесь с разработчиком приложения и передайте ему следующее:</span><span class="sxs-lookup"><span data-stu-id="4b940-178">Contact the application vendor and share:</span></span>

    -   <span data-ttu-id="4b940-179">Запрос SAML</span><span class="sxs-lookup"><span data-stu-id="4b940-179">SAML request</span></span>

    -   [<span data-ttu-id="4b940-180">Требования к протоколу SAML единого входа в Azure</span><span class="sxs-lookup"><span data-stu-id="4b940-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="4b940-181">Он должен проверить, поддерживается ли в Azure AD реализация единого входа на базе SAML.</span><span class="sxs-lookup"><span data-stu-id="4b940-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="4b940-182">Нет ресурсов в списке requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="4b940-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="4b940-183">*Ошибка AADSTS65005: клиентское приложение запросило доступ к ресурсу "00000002-0000-0000-c000-000000000000". Этот запрос не выполнен, так как клиент не указал данный ресурс в своем списке requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="4b940-183">*Error AADSTS65005: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="4b940-184">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="4b940-184">**Possible cause**</span></span>

<span data-ttu-id="4b940-185">Поврежден объект приложения.</span><span class="sxs-lookup"><span data-stu-id="4b940-185">The application object is corrupted.</span></span>

<span data-ttu-id="4b940-186">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="4b940-186">**Resolution**</span></span>

<span data-ttu-id="4b940-187">Чтобы решить проблему, удалите приложение из каталога.</span><span class="sxs-lookup"><span data-stu-id="4b940-187">To solve the problem, remove the application from the directory.</span></span> <span data-ttu-id="4b940-188">После этого добавьте и перенастройте его, следуя указанным ниже действиям:</span><span class="sxs-lookup"><span data-stu-id="4b940-188">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="4b940-189">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4b940-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4b940-190">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4b940-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b940-191">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b940-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b940-192">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b940-193">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4b940-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4b940-194">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4b940-195">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4b940-195">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4b940-196">Щелкните **Удалить** в верхней левой части колонки **Обзор** приложения.</span><span class="sxs-lookup"><span data-stu-id="4b940-196">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="4b940-197">Обновите Azure AD и добавьте приложение из коллекции Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b940-197">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="4b940-198">После этого настройте приложение снова.</span><span class="sxs-lookup"><span data-stu-id="4b940-198">Then, Configure the application again.</span></span>

<span data-ttu-id="4b940-199">После повторной настройки приложения вход в него должен заработать.</span><span class="sxs-lookup"><span data-stu-id="4b940-199">After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="4b940-200">Не настроен сертификат или ключ</span><span class="sxs-lookup"><span data-stu-id="4b940-200">Certificate or key not configured</span></span>

<span data-ttu-id="4b940-201">Ошибка AADSTS50003: не настроен ключ подписывания.</span><span class="sxs-lookup"><span data-stu-id="4b940-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="4b940-202">**Возможная причина**</span><span class="sxs-lookup"><span data-stu-id="4b940-202">**Possible cause**</span></span>

<span data-ttu-id="4b940-203">Поврежден объект приложения, и Azure AD не распознает сертификат, настроенный для приложения.</span><span class="sxs-lookup"><span data-stu-id="4b940-203">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="4b940-204">**Способы устранения:**</span><span class="sxs-lookup"><span data-stu-id="4b940-204">**Resolution**</span></span>

<span data-ttu-id="4b940-205">Чтобы удалить и создать сертификат, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4b940-205">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="4b940-206">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4b940-206">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4b940-207">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4b940-207">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b940-208">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b940-208">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b940-209">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-209">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b940-210">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4b940-210">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4b940-211">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b940-211">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4b940-212">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4b940-212">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4b940-213">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4b940-213">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4b940-214">В разделе **Сертификат подписи SAML** щелкните **Создать сертификат**.</span><span class="sxs-lookup"><span data-stu-id="4b940-214">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="4b940-215">Выберите срок действия.</span><span class="sxs-lookup"><span data-stu-id="4b940-215">Select Expiration date.</span></span> <span data-ttu-id="4b940-216">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4b940-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="4b940-217">Установите флажок **Сделать сертификат активным**, чтобы переопределить активный сертификат.</span><span class="sxs-lookup"><span data-stu-id="4b940-217">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="4b940-218">Нажмите кнопку **Сохранить** в верхней части колонки и активируйте сертификат возобновления.</span><span class="sxs-lookup"><span data-stu-id="4b940-218">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="4b940-219">В разделе **Сертификат подписи SAML** щелкните **Удалить**, чтобы удалить **неиспользуемый** сертификат.</span><span class="sxs-lookup"><span data-stu-id="4b940-219">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="4b940-220">Проблема при настройке утверждений SAML, отправляемых в приложение</span><span class="sxs-lookup"><span data-stu-id="4b940-220">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="4b940-221">Чтобы узнать, как настроить утверждения атрибута SAML, отправляемые в приложение, ознакомьтесь с разделом [Сопоставление утверждений в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping).</span><span class="sxs-lookup"><span data-stu-id="4b940-221">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b940-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4b940-222">Next steps</span></span>
[<span data-ttu-id="4b940-223">Требования к протоколу SAML единого входа в Azure</span><span class="sxs-lookup"><span data-stu-id="4b940-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
