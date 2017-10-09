---
title: "Настройка федеративного единого входа для приложения не коллекции aaaProblem | Документы Microsoft"
description: "Адрес hello распространенных проблем, которые могут возникнуть при настройке федеративного единого входа tooyour SAML прикладной, отсутствующих в hello коллекции приложений Azure AD."
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="1ba16-103">Проблема при настройке федеративного единого входа для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="1ba16-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="1ba16-104">Если при настройке приложения возникла проблема, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1ba16-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="1ba16-105">Проверка выполнения всех шагов hello в статье hello [Настройка одной tooapplications входа, которых нет в коллекции приложений Azure Active Directory hello.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="1ba16-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="1ba16-106">Не удается добавить другой экземпляр приложения hello</span><span class="sxs-lookup"><span data-stu-id="1ba16-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="1ba16-107">tooadd второй экземпляр приложения необходимые toobe возможность.</span><span class="sxs-lookup"><span data-stu-id="1ba16-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="1ba16-108">Настройте уникальный идентификатор для второго экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="1ba16-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="1ba16-109">Не будет возможности tooconfigure приветствия же идентификатор, используемый для первого экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="1ba16-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="1ba16-110">Настройте другой сертификат hello, другая — для первого экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="1ba16-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="1ba16-111">Если hello приложение не предоставляет поддержку hello выше.</span><span class="sxs-lookup"><span data-stu-id="1ba16-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="1ba16-112">Затем не будет возможности tooconfigure второй экземпляр.</span><span class="sxs-lookup"><span data-stu-id="1ba16-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="1ba16-113">Устанавливаемый формат hello EntityID (идентификатор пользователя)</span><span class="sxs-lookup"><span data-stu-id="1ba16-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="1ba16-114">Его нельзя будет tooselect hello EntityID (идентификатор пользователя) формат, Azure AD отправляет toohello приложения hello ответа после проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="1ba16-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="1ba16-115">Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="1ba16-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="1ba16-116">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) в разделе "hello" необязательного,</span><span class="sxs-lookup"><span data-stu-id="1ba16-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="1ba16-117">Где получить метаданные приложения hello, или сертификат из Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ba16-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="1ba16-118">метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="1ba16-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ba16-119">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="1ba16-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1ba16-120">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="1ba16-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ba16-121">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="1ba16-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ba16-122">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="1ba16-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1ba16-123">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="1ba16-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1ba16-124">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="1ba16-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1ba16-125">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="1ba16-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="1ba16-126">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="1ba16-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1ba16-127">Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца.</span><span class="sxs-lookup"><span data-stu-id="1ba16-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="1ba16-128">В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="1ba16-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="1ba16-129">Azure AD не предоставляет метаданных hello tooget URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1ba16-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="1ba16-130">Hello метаданные могут быть получены только как XML-файл.</span><span class="sxs-lookup"><span data-stu-id="1ba16-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="1ba16-131">Не знаете, как утверждения SAML toocustomize отправлено tooan приложения</span><span class="sxs-lookup"><span data-stu-id="1ba16-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="1ba16-132">toolearn toocustomize hello SAML атрибут отправлять утверждений приложения tooyour разделе [утверждения сопоставления в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="1ba16-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ba16-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ba16-133">Next steps</span></span>
[<span data-ttu-id="1ba16-134">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ba16-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
