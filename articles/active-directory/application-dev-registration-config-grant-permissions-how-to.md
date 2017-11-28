---
title: "aaaHow toogrant разрешений tooa сторонних разрабатываемых приложений | Документы Microsoft"
description: "Как toogrant разрешения tooyour приложения, разработанного с помощью hello портала Azure AD или параметра URL-адреса"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="d03f5-103">Как tooa toogrant разрешения разработанного приложения</span><span class="sxs-lookup"><span data-stu-id="d03f5-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="d03f5-104">Требуется согласие toogrant приоритетным прерыванием в приложении или при запуске произошла ошибка, вы не согласие tooan приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d03f5-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="d03f5-105">Как tooperform согласие администратора для вашего приложения</span><span class="sxs-lookup"><span data-stu-id="d03f5-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="d03f5-106">Действует hello предоставления согласия toohello приложения для всех пользователей в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="d03f5-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="d03f5-107">Перейдите toohello **регистрации приложения** колонки как **глобального администратора**, а затем выберите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="d03f5-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="d03f5-108">Выберите **требуемые разрешения**и, наконец, появится hello **GRANT, предоставление разрешений** кнопку hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="d03f5-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="d03f5-109">Кроме того, можно создать запрос слишком*login.microsoftonline.com* с вашей конфигурации приложения и добавления на *& prompt = admin\_согласия*.</span><span class="sxs-lookup"><span data-stu-id="d03f5-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="d03f5-110">После входа в систему с учетными данными администратора, приложение hello было предоставлено согласие для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="d03f5-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="d03f5-111">Как tooforce согласия пользователя для приложения</span><span class="sxs-lookup"><span data-stu-id="d03f5-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="d03f5-112">Добавление на запросы проверки подлинности *& Запрос согласия =* , требующую tooconsent конечных пользователей каждый раз при проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="d03f5-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d03f5-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d03f5-113">Next steps</span></span>

[<span data-ttu-id="d03f5-114">Запрос согласия и интеграция приложений tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="d03f5-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="d03f5-115">Согласие и разрешения для конвергированных приложений в Azure AD версии 2.0</span><span class="sxs-lookup"><span data-stu-id="d03f5-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="d03f5-116">StackOverflow в AzureAD</span><span class="sxs-lookup"><span data-stu-id="d03f5-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
