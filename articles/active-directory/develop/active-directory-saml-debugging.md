---
title: "Отладка единого входа на основе SAML в приложения в Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как выполнять отладку единого входа на основе SAML в приложения в Azure Active Directory. "
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="65bd5-103">Отладка единого входа на основе SAML в приложения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65bd5-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="65bd5-104">При отладке интеграции приложений на основе SAML часто бывает полезно использовать такой инструмент, как [Fiddler](http://www.telerik.com/fiddler) , чтобы просмотреть запрос SAML, ответ SAML и фактический токен SAML, выданный приложению.</span><span class="sxs-lookup"><span data-stu-id="65bd5-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="65bd5-105">Проверив токен SAML, можно убедиться, что все необходимые атрибуты, имя пользователя в теме SAML и универсальный код ресурса (URI) издателя поступают должным образом.</span><span class="sxs-lookup"><span data-stu-id="65bd5-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="65bd5-106">Ответ от Azure AD, который содержит токен SAML, обычно создается после перенаправления HTTP 302 с https://login.windows.net и отправляется на настроенный **URL-адрес ответа** приложения.</span><span class="sxs-lookup"><span data-stu-id="65bd5-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="65bd5-107">Токен SAML можно просмотреть, выбрав эту строку и затем выбрав вкладку **Inspectors > WebForms** (Инспекторы > Веб-формы) на правой панели.</span><span class="sxs-lookup"><span data-stu-id="65bd5-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="65bd5-108">После этого щелкните правой кнопкой мыши значение **SAMLResponse** и выберите **Send to TextWizard** (Отправить в TextWizard).</span><span class="sxs-lookup"><span data-stu-id="65bd5-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="65bd5-109">В меню **Transform** (Преобразование) выберите **From Base64** (Из Base64), чтобы расшифровать токен и просмотреть его содержимое.</span><span class="sxs-lookup"><span data-stu-id="65bd5-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="65bd5-110">**Примечание**. Чтобы просмотреть содержимое этого HTTP-запроса, Fiddler может предложить настроить шифрование трафика HTTPS. Это будет необходимо сделать.</span><span class="sxs-lookup"><span data-stu-id="65bd5-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="65bd5-111">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="65bd5-111">Related Articles</span></span>
* [<span data-ttu-id="65bd5-112">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65bd5-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="65bd5-113">Настройка единого входа для приложений, которых нет в коллекции приложений Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65bd5-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="65bd5-114">Настройка утверждений, выпущенных в маркере SAML для предварительно интегрированных приложений</span><span class="sxs-lookup"><span data-stu-id="65bd5-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png