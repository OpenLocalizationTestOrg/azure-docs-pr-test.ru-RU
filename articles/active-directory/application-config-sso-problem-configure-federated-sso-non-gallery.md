---
title: "Проблема при настройке федеративного единого входа для приложения не из коллекции | Документы Майкрософт"
description: "В этом разделе приводятся решения распространенных проблем, которые могут возникнуть при настройке федеративного единого входа для пользовательского приложения SAML, которое отсутствует в коллекции приложений Azure AD"
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
ms.openlocfilehash: 4eb2c04c940dd6ad15a491a331aed76c237f0387
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="8a0db-103">Проблема при настройке федеративного единого входа для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="8a0db-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="8a0db-104">Если при настройке приложения возникла проблема, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8a0db-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="8a0db-105">Выполните все действия, описанные в статье [Настройка единого входа для приложений, которых нет в коллекции приложений Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps).</span><span class="sxs-lookup"><span data-stu-id="8a0db-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="8a0db-106">Невозможно добавить другой экземпляр приложения</span><span class="sxs-lookup"><span data-stu-id="8a0db-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="8a0db-107">Чтобы добавить второй экземпляр приложения, нужно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8a0db-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="8a0db-108">Настроить уникальный идентификатор для второго экземпляра.</span><span class="sxs-lookup"><span data-stu-id="8a0db-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="8a0db-109">Вы не сможете использовать тот же идентификатор, что и у первого экземпляра.</span><span class="sxs-lookup"><span data-stu-id="8a0db-109">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="8a0db-110">Настроить другой сертификат для второго экземпляра.</span><span class="sxs-lookup"><span data-stu-id="8a0db-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="8a0db-111">Если приложение не поддерживает перечисленные выше действия,</span><span class="sxs-lookup"><span data-stu-id="8a0db-111">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="8a0db-112">вы не сможете настроить второй экземпляр.</span><span class="sxs-lookup"><span data-stu-id="8a0db-112">Then, you won’t be able to configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="8a0db-113">Можно ли изменить формат идентификатора EntityID (идентификатора пользователя)?</span><span class="sxs-lookup"><span data-stu-id="8a0db-113">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="8a0db-114">Вы не можете изменить формат EntityID (идентификатора пользователя), который Azure AD отправляет приложению после проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="8a0db-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="8a0db-115">Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="8a0db-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="8a0db-116">Дополнительные сведения см. в разделе "NameIDPolicy" статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="8a0db-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="8a0db-117">Как получить метаданные приложения или сертификат в Azure AD?</span><span class="sxs-lookup"><span data-stu-id="8a0db-117">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="8a0db-118">Чтобы скачать метаданные приложения или сертификат в Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8a0db-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="8a0db-119">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="8a0db-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="8a0db-120">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="8a0db-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8a0db-121">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a0db-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8a0db-122">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8a0db-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8a0db-123">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="8a0db-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="8a0db-124">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8a0db-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="8a0db-125">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="8a0db-125">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="8a0db-126">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="8a0db-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8a0db-127">Перейдите в раздел **Сертификат подписи SAML** и выберите значение в столбце **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="8a0db-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="8a0db-128">В зависимости от того, что именно требуется для настройки единого входа, вы сможете скачать XML-файл метаданных или сертификат.</span><span class="sxs-lookup"><span data-stu-id="8a0db-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="8a0db-129">Azure AD не предоставляет URL-адреса для получения метаданных.</span><span class="sxs-lookup"><span data-stu-id="8a0db-129">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="8a0db-130">Метаданные можно скачать только в виде XML-файла.</span><span class="sxs-lookup"><span data-stu-id="8a0db-130">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="8a0db-131">Не знаете, как настроить утверждения SAML, отправляемые в приложение</span><span class="sxs-lookup"><span data-stu-id="8a0db-131">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="8a0db-132">Чтобы узнать, как настроить атрибут утверждений SAML, отправляемых в приложение, ознакомьтесь с разделом [Сопоставление утверждений в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping).</span><span class="sxs-lookup"><span data-stu-id="8a0db-132">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a0db-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a0db-133">Next steps</span></span>
[<span data-ttu-id="8a0db-134">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a0db-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
