---
title: "Как настроить федеративный единый вход для приложения из коллекции Azure AD | Документы Майкрософт"
description: "В этой статье описано, как настроить федеративный единый вход для приложения из коллекции Azure AD и быстро выполнить эти действия с помощью соответствующих руководств"
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
ms.openlocfilehash: 1b1d00718981b2c7d11f5b88428d02e16dd0b34d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="5e8b0-103">Настройка федеративного единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e8b0-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="5e8b0-104">Для всех приложений в коллекции Azure AD, для которых включен корпоративный единый вход, доступны пошаговые руководства.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="5e8b0-105">Подробное пошаговое руководство можно найти в [Списке руководств по интеграции приложений SaaS с Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="5e8b0-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="5e8b0-106">Обзор необходимых действий</span><span class="sxs-lookup"><span data-stu-id="5e8b0-106">Overview of steps required</span></span>
<span data-ttu-id="5e8b0-107">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5e8b0-108">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e8b0-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="5e8b0-109">Указание значений метаданных приложения в Azure AD (URL-адрес для входа, идентификатор, URL-адрес ответа)</span><span class="sxs-lookup"><span data-stu-id="5e8b0-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="5e8b0-110">Выбор идентификатора пользователя и добавление атрибутов пользователей, которые будут отправлены в приложение</span><span class="sxs-lookup"><span data-stu-id="5e8b0-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="5e8b0-111">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="5e8b0-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="5e8b0-112">Указание значений метаданных Azure AD в приложении (URL-адрес для входа, издатель, URL-адрес для выхода и сертификат)</span><span class="sxs-lookup"><span data-stu-id="5e8b0-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="5e8b0-113">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="5e8b0-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="5e8b0-114">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e8b0-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="5e8b0-115">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="5e8b0-116">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-116">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5e8b0-117">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e8b0-118">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e8b0-119">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e8b0-120">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-120">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="5e8b0-121">Введите имя приложения в текстовом поле **Введите имя** в разделе **Добавить из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="5e8b0-122">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="5e8b0-123">Перед добавлением приложения можно изменить его имя в текстовом поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="5e8b0-124">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="5e8b0-125">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-125">After a short period of time, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="5e8b0-126">Настройка единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e8b0-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="5e8b0-127">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="5e8b0-128">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-128">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="5e8b0-129">Откройте **расширение Azure Active Directory**, щелкнув **Дополнительные службы** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-129">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e8b0-130">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e8b0-131">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-131">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e8b0-132">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="5e8b0-133">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e8b0-134">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="5e8b0-135">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-135">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e8b0-136">В раскрывающемся списке **Режим** выберите пункт **Вход на основе SAML**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="5e8b0-137">Введите необходимые значения в поле **Домены и URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="5e8b0-138">Их можно получить у поставщика приложения.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="5e8b0-139">Чтобы настроить единый вход, инициированный поставщиком услуг, обязательно укажите URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-139">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="5e8b0-140">Для некоторых приложений также нужно указать идентификатор.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="5e8b0-141">Чтобы настроить единый вход, инициированный поставщиком удостоверений, введите URL-адрес для ответа.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="5e8b0-142">Для некоторых приложений также нужно указать идентификатор.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="5e8b0-143">**Необязательно:** щелкните **Показать дополнительные параметры URL-адресов**, чтобы увидеть необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="5e8b0-144">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="5e8b0-145">**Необязательно:** щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

  <span data-ttu-id="5e8b0-146">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="5e8b0-147">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-147">click **Add attribute**.</span></span> <span data-ttu-id="5e8b0-148">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="5e8b0-149">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-149">Click **Save.**</span></span> <span data-ttu-id="5e8b0-150">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="5e8b0-151">Щелкните **Настроить &lt;имя приложения&gt;**, чтобы открыть документацию по настройке единого входа для приложения.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="5e8b0-152">Кроме того, для настройки единого входа для приложения также потребуются URL-адреса метаданных и сертификат.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-152">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="5e8b0-153">Чтобы сохранить конфигурацию, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="5e8b0-154">Назначьте пользователей приложению.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="5e8b0-155">Выберите идентификатор пользователя и добавьте атрибуты пользователя, которые будут отправлены в приложение.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="5e8b0-156">Чтобы выбрать идентификатор пользователя или добавить атрибуты пользователя, выполните указанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="5e8b0-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="5e8b0-157">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-157">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e8b0-158">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e8b0-159">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e8b0-160">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e8b0-161">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="5e8b0-162">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e8b0-163">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5e8b0-164">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-164">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e8b0-165">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="5e8b0-166">Выбранный параметр должен соответствовать ожидаемому значению для проверки подлинности пользователя в приложении.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="5e8b0-167">Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="5e8b0-168">Дополнительные сведения см. в разделе NameIDPolicy статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="5e8b0-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="5e8b0-169">Чтобы добавить атрибуты пользователя, щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="5e8b0-170">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="5e8b0-171">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-171">click **Add attribute**.</span></span> <span data-ttu-id="5e8b0-172">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="5e8b0-173">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-173">Click **Save**.</span></span> <span data-ttu-id="5e8b0-174">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="5e8b0-175">Скачивание метаданных Azure AD или сертификата</span><span class="sxs-lookup"><span data-stu-id="5e8b0-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="5e8b0-176">Чтобы скачать метаданные приложения или сертификат в Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5e8b0-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="5e8b0-177">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-177">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e8b0-178">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-178">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e8b0-179">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e8b0-180">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-180">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e8b0-181">Щелкните **Все приложения** для просмотра списка всех приложений.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="5e8b0-182">Если нужное приложение отсутствует в списке, обратитесь к элементу управления **Фильтр** в верхней части списка **Все приложения** и для параметра **Показать** выберите значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="5e8b0-183">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5e8b0-184">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-184">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e8b0-185">Перейдите в раздел **Сертификат подписи SAML** и выберите значение в столбце **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="5e8b0-186">В зависимости от того, что именно требуется для настройки единого входа, вы сможете скачать XML-файл метаданных или сертификат.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="5e8b0-187">Azure AD не предоставляет URL-адреса для получения метаданных.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-187">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="5e8b0-188">Метаданные можно скачать только в виде XML-файла.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-188">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="5e8b0-189">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="5e8b0-189">Assign users to the application</span></span>

<span data-ttu-id="5e8b0-190">Чтобы напрямую назначить одного или нескольких пользователей для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="5e8b0-191">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-191">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5e8b0-192">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-192">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e8b0-193">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e8b0-194">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-194">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e8b0-195">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5e8b0-196">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e8b0-197">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="5e8b0-198">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-198">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e8b0-199">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5e8b0-200">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-200">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5e8b0-201">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5e8b0-202">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="5e8b0-203">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="5e8b0-204">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="5e8b0-205">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="5e8b0-206">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-206">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="5e8b0-207">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="5e8b0-208">Через некоторое время выбранные пользователи смогут запускать эти приложения с помощью методов, приведенных в описании решения.</span><span class="sxs-lookup"><span data-stu-id="5e8b0-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="5e8b0-209">Настройка утверждений SAML, отправляемых в приложение</span><span class="sxs-lookup"><span data-stu-id="5e8b0-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="5e8b0-210">Чтобы узнать, как настроить атрибут утверждений SAML, отправляемых в приложение, ознакомьтесь с разделом [Сопоставление утверждений в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping).</span><span class="sxs-lookup"><span data-stu-id="5e8b0-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e8b0-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e8b0-211">Next steps</span></span>
[<span data-ttu-id="5e8b0-212">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="5e8b0-212">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



