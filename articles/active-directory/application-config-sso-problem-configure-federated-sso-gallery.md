---
title: "Настройка федеративного единого входа для приложения Azure AD коллекции aaaProblem | Документы Microsoft"
description: "Адрес hello распространенных проблем, которые могут возникнуть при настройке федеративного единого входа с помощью SAML для приложений, которые перечислены в коллекции приложений Azure AD hello"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="8c7aa-103">Проблема при настройке федеративного единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c7aa-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="8c7aa-104">Если при настройке приложения возникла проблема, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="8c7aa-105">Убедитесь, что выполнены все действия hello в учебнике hello для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="8c7aa-106">В конфигурации приложения hello имеют встроенные документацию по как tooconfigure hello приложения.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="8c7aa-107">Кроме того, можно получить доступ к hello [список учебников по toointegrate приложений SaaS в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) Подробное пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="8c7aa-108">Не удается добавить другой экземпляр приложения hello</span><span class="sxs-lookup"><span data-stu-id="8c7aa-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="8c7aa-109">tooadd второй экземпляр приложения необходимые toobe возможность.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="8c7aa-110">Настройте уникальный идентификатор для второго экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="8c7aa-111">Не будет возможности tooconfigure приветствия же идентификатор, используемый для первого экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="8c7aa-112">Настройте другой сертификат hello, другая — для первого экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="8c7aa-113">Если hello приложение не предоставляет поддержку hello выше.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="8c7aa-114">Затем не будет возможности tooconfigure второй экземпляр.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="8c7aa-115">Не удается добавить идентификатор hello или hello URL-адрес ответа</span><span class="sxs-lookup"><span data-stu-id="8c7aa-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="8c7aa-116">Если вы не являетесь hello может tooconfigure идентификатор или hello URL-адрес ответа, подтвердите hello идентификатора и URL-адрес ответа совпадают шаблоны hello, заранее настроенная для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="8c7aa-117">шаблоны tooknow hello, заранее настроенная для приложения hello:</span><span class="sxs-lookup"><span data-stu-id="8c7aa-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="8c7aa-118">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.** Go toostep 7.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="8c7aa-119">Если вы уже находитесь в колонке конфигурации приложения hello на Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="8c7aa-120">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8c7aa-121">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8c7aa-122">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8c7aa-123">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="8c7aa-124">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="8c7aa-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="8c7aa-125">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="8c7aa-126">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8c7aa-127">Выберите **входа на базе SAML** из hello **режим** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="8c7aa-128">Go toohello **идентификатор** или **URL-адрес ответа** текстовое поле под hello **раздел URL-адреса и домена.**</span><span class="sxs-lookup"><span data-stu-id="8c7aa-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="8c7aa-129">Существует три способа tooknow hello поддерживается шаблонов для приложения hello:</span><span class="sxs-lookup"><span data-stu-id="8c7aa-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="8c7aa-130">В текстовом поле «hello» вы увидите шаблонам hello поддерживается как заполнитель *пример:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="8c7aa-131">Если hello шаблон не поддерживается, при попытке tooenter hello значение в текстовом поле hello появиться красный восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="8c7aa-132">Если навести указатель мыши hello красный восклицательный знак, можно увидеть шаблоны hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="8c7aa-133">В учебнике hello для приложения hello можно также получить сведения о шаблонах hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="8c7aa-134">В разделе hello **Настройка Azure AD единого входа** раздела.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="8c7aa-135">Последовательно выберите toohello шаг для hello настроенные значения в полях hello **URL-адреса и домена** раздела.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="8c7aa-136">Если hello значения не совпадают с шаблонами hello, заранее настроенная в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="8c7aa-137">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="8c7aa-137">You can:</span></span>

-   <span data-ttu-id="8c7aa-138">Работать со значениями tooget поставщика приложения hello, соответствующие шаблону hello, заранее настроенная в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c7aa-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="8c7aa-139">Или можно обратиться рабочая группа Azure AD по < aadapprequest@microsoft.com > или оставьте комментарий в обновлении hello учебника toorequest hello hello поддерживается шаблонов для приложения hello</span><span class="sxs-lookup"><span data-stu-id="8c7aa-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="8c7aa-140">Устанавливаемый формат hello EntityID (идентификатор пользователя)</span><span class="sxs-lookup"><span data-stu-id="8c7aa-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="8c7aa-141">Его нельзя будет tooselect hello EntityID (идентификатор пользователя) формат, Azure AD отправляет toohello приложения hello ответа после проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="8c7aa-142">Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="8c7aa-143">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) в разделе "hello" необязательного,</span><span class="sxs-lookup"><span data-stu-id="8c7aa-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="8c7aa-144">Не удается найти конфигурацию hello Azure AD метаданных toocomplete hello с приложением hello</span><span class="sxs-lookup"><span data-stu-id="8c7aa-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="8c7aa-145">метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="8c7aa-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="8c7aa-146">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="8c7aa-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="8c7aa-147">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8c7aa-148">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8c7aa-149">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8c7aa-150">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="8c7aa-151">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="8c7aa-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="8c7aa-152">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="8c7aa-153">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8c7aa-154">Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="8c7aa-155">В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="8c7aa-156">Azure AD не предоставляет метаданных hello tooget URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="8c7aa-157">Hello метаданные могут быть получены только как XML-файл.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="8c7aa-158">Не знаете, как утверждения SAML toocustomize отправлено tooan приложения</span><span class="sxs-lookup"><span data-stu-id="8c7aa-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="8c7aa-159">toolearn toocustomize hello SAML атрибут отправлять утверждений приложения tooyour разделе [утверждения сопоставления в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="8c7aa-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c7aa-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c7aa-160">Next steps</span></span>
[<span data-ttu-id="8c7aa-161">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c7aa-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
