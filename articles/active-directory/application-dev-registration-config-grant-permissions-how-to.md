---
title: "Предоставление разрешений для специально разработанного приложения | Документы Майкрософт"
description: "Предоставление разрешений для специально разработанного приложения с помощью портала Azure AD или параметра URL-адреса"
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
ms.openlocfilehash: 336b945929f80e1a566f7cf71b40fd799a98c12d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a><span data-ttu-id="f461e-103">Как предоставить разрешения для специально разработанного приложения</span><span class="sxs-lookup"><span data-stu-id="f461e-103">How to grant permissions to a custom-developed application</span></span>

<span data-ttu-id="f461e-104">Если требуется дать согласие в приложении заранее или если возникло сообщение об ошибке в связи с тем, что не предоставлено согласие для приложения, попробуйте выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f461e-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span></span>

## <a name="how-to-perform-admin-consent-for-your-application"></a><span data-ttu-id="f461e-105">Предоставление согласия администратора для вашего приложения</span><span class="sxs-lookup"><span data-stu-id="f461e-105">How to perform Admin Consent for your application</span></span>

<span data-ttu-id="f461e-106">Это приводит к тому, что согласие предоставляется для всех пользователей в организации.</span><span class="sxs-lookup"><span data-stu-id="f461e-106">This has the effect of granting consent to the application for all users in your organization.</span></span>

1. <span data-ttu-id="f461e-107">Перейдите к колонке **Регистрация приложений** в качестве **глобального администратора**, а затем выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="f461e-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span></span>

2. <span data-ttu-id="f461e-108">Выберите **Необходимые разрешения** и, наконец, нажмите кнопку **Предоставить разрешения** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="f461e-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span></span>

<span data-ttu-id="f461e-109">Кроме того, можно создать запрос на адрес *login.microsoftonline.com*, указав конфигурацию приложения и добавив *&prompt=admin\_consent*.</span><span class="sxs-lookup"><span data-stu-id="f461e-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="f461e-110">После входа с учетными данными администратора приложению были предоставлены разрешения для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="f461e-110">After signing in with admin credentials, the app has been granted consent for all users.</span></span>

## <a name="how-to-force-user-consent-for-your-application"></a><span data-ttu-id="f461e-111">Принудительное предоставление согласия пользователя для приложения</span><span class="sxs-lookup"><span data-stu-id="f461e-111">How to force User Consent for your application</span></span>

* <span data-ttu-id="f461e-112">Добавьте *&prompt=consent* к запросу на аутентификацию, при этом пользователю необходимо будет давать согласие всякий раз, как он проходит аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="f461e-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f461e-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f461e-113">Next steps</span></span>

[<span data-ttu-id="f461e-114">Согласие и интеграция приложений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f461e-114">Consent and Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="f461e-115">Согласие и разрешения для конвергированных приложений в Azure AD версии 2.0</span><span class="sxs-lookup"><span data-stu-id="f461e-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="f461e-116">StackOverflow в AzureAD</span><span class="sxs-lookup"><span data-stu-id="f461e-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
