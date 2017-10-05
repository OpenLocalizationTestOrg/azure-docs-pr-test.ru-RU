---
title: "Ошибка на странице приложения после входа | Документы Майкрософт"
description: "Устранение проблем со входом в Azure AD, когда само приложение выдает ошибку"
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="c9d7b-103">Ошибка на странице приложения после входа</span><span class="sxs-lookup"><span data-stu-id="c9d7b-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="c9d7b-104">В этом сценарии пользователь вошел в Azure AD, однако приложение отображает ошибку, не позволяя завершить процедуру входа.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="c9d7b-105">В этом случае приложение не принимает ответ от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="c9d7b-106">Существует несколько возможных причин, по которым приложение не приняло ответ от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="c9d7b-107">Если ошибка в приложении недостаточно информативна, чтобы понять, что именно отсутствует в ответе, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9d7b-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="c9d7b-108">Если приложение является коллекцией Azure AD, выполните все действия, описанные в статье [Отладка единого входа на основе SAML в приложения в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="c9d7b-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="c9d7b-109">Используйте такое средство, как [Fiddler](http://www.telerik.com/fiddler), для захвата запроса, ответа и токена SAML.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="c9d7b-110">Предоставьте ответ SAML поставщику приложения, чтобы узнать, чего именно не хватает.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="c9d7b-111">Недостающие атрибуты в ответе SAML</span><span class="sxs-lookup"><span data-stu-id="c9d7b-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="c9d7b-112">Чтобы добавить атрибут в конфигурацию Azure AD для отправки в ответе Azure AD, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9d7b-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="c9d7b-113">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c9d7b-114">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9d7b-115">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9d7b-116">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9d7b-117">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c9d7b-118">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c9d7b-119">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c9d7b-120">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c9d7b-121">В разделе **Атрибуты пользователя** щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="c9d7b-122">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-122">To add an attribute:</span></span>

   * <span data-ttu-id="c9d7b-123">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-123">click **Add attribute**.</span></span> <span data-ttu-id="c9d7b-124">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="c9d7b-125">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-125">Click **Save.**</span></span> <span data-ttu-id="c9d7b-126">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="c9d7b-127">Сохраните конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-127">Save the configuration.</span></span>

<span data-ttu-id="c9d7b-128">При следующем входе пользователя в приложение Azure AD отправляет новый атрибут в ответе SAML.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="c9d7b-129">Приложение ожидает идентификатор пользователя с другим значением или в другом формате</span><span class="sxs-lookup"><span data-stu-id="c9d7b-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="c9d7b-130">Вход в приложение не удается выполнить, потому что в ответе SAML отсутствуют такие атрибуты, как роли, либо приложение ожидает другой формат для атрибута EntityID.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="c9d7b-131">Добавление атрибута в конфигурацию приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9d7b-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="c9d7b-132">Чтобы изменить значение идентификатора пользователя, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9d7b-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="c9d7b-133">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c9d7b-134">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9d7b-135">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9d7b-136">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9d7b-137">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c9d7b-138">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c9d7b-139">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c9d7b-140">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c9d7b-141">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="c9d7b-142">Изменение формата идентификатора EntityID (идентификатора пользователя)</span><span class="sxs-lookup"><span data-stu-id="c9d7b-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="c9d7b-143">В этом случае приложение ожидает другой формат для атрибута EntityID.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="c9d7b-144">Вы не можете изменить формат EntityID (идентификатора пользователя), который Azure AD отправляет приложению после проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="c9d7b-145">Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="c9d7b-146">Дополнительные сведения см. в разделе NameIDPolicy статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="c9d7b-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="c9d7b-147">Приложение ожидает другой метод подписи для ответа SAML</span><span class="sxs-lookup"><span data-stu-id="c9d7b-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="c9d7b-148">Нужно изменить, на какие именно части токена SAML Azure Active Directory ставит цифровую подпись.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="c9d7b-149">Для этого сделайте вот что.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="c9d7b-150">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c9d7b-151">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9d7b-152">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9d7b-153">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9d7b-154">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="c9d7b-155">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c9d7b-156">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c9d7b-157">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c9d7b-158">Щелкните **Показать дополнительные параметры подписывания сертификатов** в разделе **Сертификат подписи SAML**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="c9d7b-159">Выберите тот **Вариант подписывания**, который ожидает приложение:</span><span class="sxs-lookup"><span data-stu-id="c9d7b-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="c9d7b-160">Ответ знака SAML</span><span class="sxs-lookup"><span data-stu-id="c9d7b-160">Sign SAML response</span></span>

  * <span data-ttu-id="c9d7b-161">Ответ знака SAML и утверждение</span><span class="sxs-lookup"><span data-stu-id="c9d7b-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="c9d7b-162">Утверждение знака SAML</span><span class="sxs-lookup"><span data-stu-id="c9d7b-162">Sign SAML assertion</span></span>

<span data-ttu-id="c9d7b-163">При следующем входе пользователя в приложение Azure AD подписывает выбранную часть ответа SAML.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="c9d7b-164">Приложение ожидает алгоритм подписи SHA-1</span><span class="sxs-lookup"><span data-stu-id="c9d7b-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="c9d7b-165">По умолчанию Azure AD подписывает токен SAML с помощью наиболее безопасного алгоритма.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="c9d7b-166">Рекомендуется изменять алгоритм подписи на SHA-1 только тогда, когда это необходимо приложению.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="c9d7b-167">Чтобы изменить алгоритм подписи, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9d7b-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="c9d7b-168">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c9d7b-169">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c9d7b-170">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c9d7b-171">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c9d7b-172">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c9d7b-173">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c9d7b-174">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c9d7b-175">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c9d7b-176">Щелкните **Показать дополнительные параметры подписывания сертификатов** в разделе **Сертификат подписи SAML**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="c9d7b-177">Выберите SHA-1 в поле **Алгоритм подписи**.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="c9d7b-178">При следующем входе пользователя в приложение Azure AD подписывает токен SAML с использованием алгоритма SHA-1.</span><span class="sxs-lookup"><span data-stu-id="c9d7b-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9d7b-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9d7b-179">Next steps</span></span>
[<span data-ttu-id="c9d7b-180">Отладка единого входа на основе SAML в приложения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9d7b-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
