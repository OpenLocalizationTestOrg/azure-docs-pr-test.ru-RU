---
title: "Выбор разрешений для заданного API | Документы Майкрософт"
description: "Здесь описано, как найти конечные точки проверки подлинности для пользовательского приложения, которое вы разрабатываете или регистрируете в Azure AD."
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
ms.openlocfilehash: 6966cf145375bf3d830d476564c428502ae40fd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-select-permissions-for-a-given-api"></a><span data-ttu-id="f6b51-103">Выбор разрешений для заданного API</span><span class="sxs-lookup"><span data-stu-id="f6b51-103">How to select permissions for a given API</span></span>

<span data-ttu-id="f6b51-104">Конечные точки проверки подлинности для приложения можно найти на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6b51-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="f6b51-105">Перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6b51-105">Navigate to the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="f6b51-106">В области навигации слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6b51-106">From the left navigation pane, click **Azure Active Directory**.</span></span>

-   <span data-ttu-id="f6b51-107">Щелкните **Регистрация приложений** и выберите **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="f6b51-107">Click **App Registrations** and choose **Endpoints**.</span></span>

-   <span data-ttu-id="f6b51-108">Откроется страница **Конечные точки** со списком всех конечных точек проверки подлинности для клиента.</span><span class="sxs-lookup"><span data-stu-id="f6b51-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span></span>

-   <span data-ttu-id="f6b51-109">Используйте соответствующую конечную точку для протокола аутентификации в сочетании с идентификатором приложения, чтобы создать запрос на аутентификацию для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="f6b51-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6b51-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6b51-110">Next steps</span></span>
[<span data-ttu-id="f6b51-111">Руководство разработчика по Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6b51-111">Azure Active Directory developer's guide</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
