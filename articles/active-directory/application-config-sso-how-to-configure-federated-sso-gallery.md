---
title: "aaaHow tooconfigure федеративного единого входа для приложения Azure AD коллекции | Документы Microsoft"
description: "Как tooconfigure федеративного единого входа для существующей коллекции Azure AD приложения и использование учебники tooget как быстро"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="cfe69-103">Как tooconfigure федеративного единого входа для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="cfe69-103">How tooconfigure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="cfe69-104">Все приложения в галерее hello Azure AD включена возможность корпоративного единого входа имеет доступные Пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="cfe69-104">All applications in hello Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="cfe69-105">Можно получить доступ к hello [список учебников по toointegrate приложений SaaS в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) Подробное пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="cfe69-105">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="cfe69-106">Обзор необходимых действий</span><span class="sxs-lookup"><span data-stu-id="cfe69-106">Overview of steps required</span></span>
<span data-ttu-id="cfe69-107">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="cfe69-107">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="cfe69-108">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfe69-108">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="cfe69-109">Настройка значения метаданных приложения hello в Azure AD (вход, URL-адрес ответа URL-адрес, идентификатор)</span><span class="sxs-lookup"><span data-stu-id="cfe69-109">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="cfe69-110">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="cfe69-110">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="cfe69-111">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="cfe69-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="cfe69-112">Настройка значения метаданных Azure AD в приложение hello (вход, URL-адрес, издателя, URL-адрес выхода и сертификата)</span><span class="sxs-lookup"><span data-stu-id="cfe69-112">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="cfe69-113">Назначить пользователей toohello приложения</span><span class="sxs-lookup"><span data-stu-id="cfe69-113">Assign users toohello application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="cfe69-114">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfe69-114">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="cfe69-115">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-115">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="cfe69-116">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="cfe69-116">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="cfe69-117">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="cfe69-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfe69-118">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="cfe69-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfe69-119">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfe69-120">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="cfe69-120">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="cfe69-121">В hello **введите имя** текстового поля из hello **добавить из галереи hello** раздел, имя типа hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-121">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="cfe69-122">Выберите приложение hello, требуется tooconfigure для единого входа.</span><span class="sxs-lookup"><span data-stu-id="cfe69-122">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="cfe69-123">Перед добавлением приложения hello, можно изменить его имя из hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="cfe69-123">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="cfe69-124">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cfe69-124">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="cfe69-125">После краткого периода времени быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-125">After a short period of time, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="cfe69-126">Настройка единого входа для приложения из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfe69-126">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="cfe69-127">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-127">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="cfe69-128">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **соадминистратору**.</span><span class="sxs-lookup"><span data-stu-id="cfe69-128">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="cfe69-129">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="cfe69-129">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfe69-130">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="cfe69-130">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfe69-131">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-131">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfe69-132">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="cfe69-132">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="cfe69-133">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="cfe69-133">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cfe69-134">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="cfe69-134">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="cfe69-135">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-135">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cfe69-136">Выберите **входа на базе SAML** из hello **режим** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="cfe69-136">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="cfe69-137">Введите значения требуется hello в **URL-адреса и домена.**</span><span class="sxs-lookup"><span data-stu-id="cfe69-137">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="cfe69-138">Вы должны получить эти значения с поставщиком приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-138">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="cfe69-139">приложение hello tooconfigure как единый вход, инициированные SP, hello входа на URL-адрес является обязательным.</span><span class="sxs-lookup"><span data-stu-id="cfe69-139">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="cfe69-140">Для некоторых приложений hello идентификатор также является обязательным.</span><span class="sxs-lookup"><span data-stu-id="cfe69-140">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="cfe69-141">приложение hello tooconfigure как инициированный IdP SSO, hello URL-адрес ответа является обязательным.</span><span class="sxs-lookup"><span data-stu-id="cfe69-141">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="cfe69-142">Для некоторых приложений hello идентификатор также является обязательным.</span><span class="sxs-lookup"><span data-stu-id="cfe69-142">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="cfe69-143">**Необязательно:** щелкните **Показывать дополнительные параметры URL-адреса** Если требуется toosee hello необязательные значения.</span><span class="sxs-lookup"><span data-stu-id="cfe69-143">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="cfe69-144">В hello **атрибуты пользователя**, выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="cfe69-144">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="cfe69-145">**Необязательно:** щелкните **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfe69-145">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

  <span data-ttu-id="cfe69-146">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="cfe69-146">tooadd an attribute:</span></span>
   
   1. <span data-ttu-id="cfe69-147">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="cfe69-147">click **Add attribute**.</span></span> <span data-ttu-id="cfe69-148">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-148">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   1. <span data-ttu-id="cfe69-149">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cfe69-149">Click **Save.**</span></span> <span data-ttu-id="cfe69-150">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-150">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="cfe69-151">Нажмите кнопку **Настройка &lt;имя_приложения&gt;**  tooaccess документацию по tooconfigure единого входа в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-151">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="cfe69-152">Кроме того имеет URL-адреса метаданных hello и toosetup требуется сертификат для единого входа с помощью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-152">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="cfe69-153">Нажмите кнопку **Сохранить** toosave hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-153">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="cfe69-154">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="cfe69-154">Assign users toohello application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="cfe69-155">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="cfe69-155">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="cfe69-156">tooselect hello идентификатор пользователя или добавление атрибутов пользователя, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="cfe69-156">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="cfe69-157">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="cfe69-157">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cfe69-158">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="cfe69-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfe69-159">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="cfe69-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfe69-160">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfe69-161">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="cfe69-161">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="cfe69-162">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="cfe69-162">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cfe69-163">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="cfe69-163">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="cfe69-164">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-164">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cfe69-165">В разделе hello **атрибуты пользователя** выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="cfe69-165">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="cfe69-166">Hello выбранного параметра должен toomatch hello ожидаемое значение в tooauthenticate hello hello приложения пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfe69-166">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="cfe69-167">Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="cfe69-167">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="cfe69-168">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) под hello статьи политики идентификатора имени.</span><span class="sxs-lookup"><span data-stu-id="cfe69-168">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="cfe69-169">атрибуты пользователя tooadd, нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfe69-169">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="cfe69-170">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="cfe69-170">tooadd an attribute:</span></span>
  
   1. <span data-ttu-id="cfe69-171">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="cfe69-171">click **Add attribute**.</span></span> <span data-ttu-id="cfe69-172">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-172">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="cfe69-173">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cfe69-173">Click **Save**.</span></span> <span data-ttu-id="cfe69-174">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-174">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="cfe69-175">Загрузка метаданных Azure AD hello или сертификат</span><span class="sxs-lookup"><span data-stu-id="cfe69-175">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="cfe69-176">метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="cfe69-176">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="cfe69-177">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="cfe69-177">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cfe69-178">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="cfe69-178">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfe69-179">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="cfe69-179">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfe69-180">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-180">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfe69-181">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="cfe69-181">click **All Applications** tooview a list of all your applications.</span></span>

  *  <span data-ttu-id="cfe69-182">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cfe69-182">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications**.</span></span>

6.  <span data-ttu-id="cfe69-183">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="cfe69-183">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="cfe69-184">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-184">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cfe69-185">Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца.</span><span class="sxs-lookup"><span data-stu-id="cfe69-185">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="cfe69-186">В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="cfe69-186">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="cfe69-187">Azure AD не предоставляет метаданных hello tooget URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="cfe69-187">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="cfe69-188">Hello метаданные могут быть получены только как XML-файл.</span><span class="sxs-lookup"><span data-stu-id="cfe69-188">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="cfe69-189">Назначить пользователей toohello приложения</span><span class="sxs-lookup"><span data-stu-id="cfe69-189">Assign users toohello application</span></span>

<span data-ttu-id="cfe69-190">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="cfe69-190">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="cfe69-191">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="cfe69-191">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="cfe69-192">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="cfe69-192">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfe69-193">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="cfe69-193">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfe69-194">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-194">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfe69-195">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="cfe69-195">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="cfe69-196">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="cfe69-196">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cfe69-197">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-197">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="cfe69-198">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-198">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cfe69-199">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="cfe69-199">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="cfe69-200">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="cfe69-200">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="cfe69-201">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="cfe69-201">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="cfe69-202">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="cfe69-202">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="cfe69-203">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="cfe69-203">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="cfe69-204">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="cfe69-204">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="cfe69-205">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="cfe69-205">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="cfe69-206">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="cfe69-206">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="cfe69-207">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="cfe69-207">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="cfe69-208">После краткого периода времени hello пользователей, которые вы выбрали быть может toolaunch эти приложения используют hello методов, описанных в разделе описания решений hello.</span><span class="sxs-lookup"><span data-stu-id="cfe69-208">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="cfe69-209">Настройка утверждений SAML, hello отправлено tooan приложения</span><span class="sxs-lookup"><span data-stu-id="cfe69-209">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="cfe69-210">toolearn toocustomize hello SAML атрибут отправлять утверждений приложения tooyour разделе [утверждения сопоставления в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="cfe69-210">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfe69-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfe69-211">Next steps</span></span>
[<span data-ttu-id="cfe69-212">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="cfe69-212">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



