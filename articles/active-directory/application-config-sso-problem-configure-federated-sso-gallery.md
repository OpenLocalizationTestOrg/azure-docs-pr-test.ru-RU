---
title: "Проблема при настройке федеративного единого входа для приложения из коллекции Azure AD | Документы Майкрософт"
description: "В этой статье приводятся решения распространенных проблем, которые могут возникнуть при настройке федеративного единого входа с использованием SAML для приложений, которые присутствуют в коллекции приложений Azure AD."
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="c0a4f-103">Проблема при настройке федеративного единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0a4f-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="c0a4f-104">Если при настройке приложения возникла проблема, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="c0a4f-105">Убедитесь, что выполнены все шаги в учебнике по приложению.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="c0a4f-106">В конфигурации приложения имеется встроенная документация по настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="c0a4f-107">Кроме того, подробное пошаговое руководство можно найти в [списке учебников по интеграции приложений SaaS с Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="c0a4f-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="c0a4f-108">Невозможно добавить другой экземпляр приложения</span><span class="sxs-lookup"><span data-stu-id="c0a4f-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="c0a4f-109">Чтобы добавить второй экземпляр приложения, нужно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c0a4f-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="c0a4f-110">Настроить уникальный идентификатор для второго экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="c0a4f-111">Вы не сможете использовать тот же идентификатор, что и у первого экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="c0a4f-112">Настроить другой сертификат для второго экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="c0a4f-113">Если приложение не поддерживает перечисленные выше действия,</span><span class="sxs-lookup"><span data-stu-id="c0a4f-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="c0a4f-114">вы не сможете настроить второй экземпляр.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="c0a4f-115">Не удается добавить идентификатор или URL-адрес ответа</span><span class="sxs-lookup"><span data-stu-id="c0a4f-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="c0a4f-116">Если вы не можете настроить идентификатор или URL-адрес ответа, убедитесь, что их значения соответствуют шаблонам, предварительно настроенным для приложения.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="c0a4f-117">Чтобы узнать предварительно настроенные шаблоны, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c0a4f-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="c0a4f-118">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="c0a4f-119">Перейдите к шагу 7.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-119">Go to step 7.</span></span> <span data-ttu-id="c0a4f-120">Если вы уже находитесь в колонке настройки приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="c0a4f-121">Откройте **расширение Azure Active Directory**, щелкнув **Дополнительные службы** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c0a4f-122">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c0a4f-123">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c0a4f-124">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c0a4f-125">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c0a4f-126">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c0a4f-127">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c0a4f-128">В раскрывающемся списке **Режим** выберите пункт **Вход на основе SAML**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="c0a4f-129">Перейдите в текстовое поле **Идентификатор** или **URL-адрес ответа** в разделе **Домены и URL-адреса приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="c0a4f-130">Узнать поддерживаемые шаблоны для приложения можно тремя способами:</span><span class="sxs-lookup"><span data-stu-id="c0a4f-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="c0a4f-131">В текстовом поле поддерживаемые шаблоны отображаются в виде заполнителя, *например,* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="c0a4f-132">Если шаблон не поддерживается, при попытке ввести значение в текстовом поле появляется красный восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="c0a4f-133">Если навести на него указатель мыши, отображаются поддерживаемые шаблоны.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="c0a4f-134">В этом учебнике для приложения также можно получить сведения о поддерживаемых шаблонах.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="c0a4f-135">В разделе **Настройка единого входа Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="c0a4f-136">Перейдите к шагу для настройки значений в разделе **Домены и URL-адреса приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="c0a4f-137">Если значения не совпадают с шаблонами, предварительно настроенными в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="c0a4f-138">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="c0a4f-138">You can:</span></span>

-   <span data-ttu-id="c0a4f-139">Обратитесь к поставщику приложения, чтобы получить значения, соответствующие предварительно настроенному шаблону в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0a4f-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="c0a4f-140">Кроме того, вы можете обратиться в группу разработчиков Azure AD по адресу <aadapprequest@microsoft.com> или оставить комментарий в учебнике, чтобы запросить обновление поддерживаемых шаблонов для приложения.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="c0a4f-141">Можно ли изменить формат идентификатора EntityID (идентификатора пользователя)?</span><span class="sxs-lookup"><span data-stu-id="c0a4f-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="c0a4f-142">Вы не можете изменить формат EntityID (идентификатора пользователя), который Azure AD отправляет приложению после проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="c0a4f-143">Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="c0a4f-144">Дополнительные сведения см. в разделе "NameIDPolicy" статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="c0a4f-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="c0a4f-145">Не удается найти метаданные Azure AD для завершения настройки в приложении</span><span class="sxs-lookup"><span data-stu-id="c0a4f-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="c0a4f-146">Чтобы скачать метаданные приложения или сертификат в Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c0a4f-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="c0a4f-147">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c0a4f-148">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c0a4f-149">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c0a4f-150">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c0a4f-151">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c0a4f-152">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c0a4f-153">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="c0a4f-154">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c0a4f-155">Перейдите в раздел **Сертификат подписи SAML** и выберите значение в столбце **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="c0a4f-156">В зависимости от того, что именно требуется для настройки единого входа, вы сможете скачать XML-файл метаданных или сертификат.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="c0a4f-157">Azure AD не предоставляет URL-адреса для получения метаданных.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="c0a4f-158">Метаданные можно скачать только в виде XML-файла.</span><span class="sxs-lookup"><span data-stu-id="c0a4f-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="c0a4f-159">Не знаете, как настроить утверждения SAML, отправляемые в приложение</span><span class="sxs-lookup"><span data-stu-id="c0a4f-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="c0a4f-160">Чтобы узнать, как настроить атрибут утверждений SAML, отправляемых в приложение, ознакомьтесь с разделом [Сопоставление утверждений в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping).</span><span class="sxs-lookup"><span data-stu-id="c0a4f-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0a4f-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0a4f-161">Next steps</span></span>
[<span data-ttu-id="c0a4f-162">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0a4f-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
