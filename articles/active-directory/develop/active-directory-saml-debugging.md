---
title: "aaaHow toodebug на основе SAML единого входа tooapplications в Azure Active Directory | Документы Microsoft"
description: "Узнайте, как toodebug на основе SAML единого входа tooapplications в Azure Active Directory "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="f3094-103">Как toodebug на основе SAML единого входа tooapplications в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3094-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="f3094-104">При отладке интеграции приложения на основе SAML, это часто полезно toouse средства, подобного [Fiddler](http://www.telerik.com/fiddler) toosee hello запрос SAML, ответ SAML hello и hello фактический маркер SAML выдаются toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="f3094-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="f3094-105">Изучив hello маркер SAML, убедитесь, что все hello обязательные атрибуты, Здравствуйте, имя пользователя в субъекта SAML hello и hello издателя URI поступающих через должным образом.</span><span class="sxs-lookup"><span data-stu-id="f3094-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="f3094-106">Hello ответа от Azure AD, который содержит маркер SAML hello обычно является hello, происходит после перенаправления HTTP 302 с https://login.windows.net и настроен отправленных toohello **URL-адрес ответа** приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f3094-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="f3094-107">Маркер SAML hello можно просмотреть, выбрав эту строку, а затем выбрав hello **инспекторы > WebForms** вкладку на правой панели hello.</span><span class="sxs-lookup"><span data-stu-id="f3094-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="f3094-108">После этого щелкните правой кнопкой мыши hello **SAMLResponse** значение и выберите **отправки tooTextWizard**.</span><span class="sxs-lookup"><span data-stu-id="f3094-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="f3094-109">Выберите **Base64 из** из hello **преобразования** toodecode меню hello маркер и просмотреть его содержимое.</span><span class="sxs-lookup"><span data-stu-id="f3094-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="f3094-110">**Примечание**: toosee hello содержимое этого HTTP-запроса, Fiddler может запросить расшифровки tooconfigure трафик HTTPS, необходимо будет toodo.</span><span class="sxs-lookup"><span data-stu-id="f3094-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="f3094-111">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="f3094-111">Related Articles</span></span>
* [<span data-ttu-id="f3094-112">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3094-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="f3094-113">Настройка одного tooapplications входа, которых нет в коллекции приложений Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="f3094-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="f3094-114">Как tooCustomize утверждений, выданных в hello токена SAML для Pre-Integrated приложений</span><span class="sxs-lookup"><span data-stu-id="f3094-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png