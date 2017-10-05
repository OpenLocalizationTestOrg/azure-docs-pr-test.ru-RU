---
title: "Как действует согласие для приложения | Документация Майкрософт"
description: "Дополнительные сведения о действии инфраструктуры согласия Azure AD, а также о том, как вы можете использовать ее при разработке приложений в Azure AD"
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
ms.openlocfilehash: 5abddf3a8698e3eb39f118f54eeac62ce68fed39
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-application-consent-works"></a><span data-ttu-id="5cfa4-103">Как действует согласие для приложения</span><span class="sxs-lookup"><span data-stu-id="5cfa4-103">How application consent works</span></span>

<span data-ttu-id="5cfa4-104">Эта статья содержит дополнительные сведения о действии инфраструктуры согласия Azure AD, используя которые вы сможете оптимизировать разработку приложений.</span><span class="sxs-lookup"><span data-stu-id="5cfa4-104">This article is to help you learn more about how the Azure AD consent framework works so you can develop applications more effectively.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="5cfa4-105">Рекомендуемые документы</span><span class="sxs-lookup"><span data-stu-id="5cfa4-105">Recommended documents</span></span>

- <span data-ttu-id="5cfa4-106">Получите общее представление о том, [как владелец ресурса может управлять доступом приложения к ресурсам благодаря согласию](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent).</span><span class="sxs-lookup"><span data-stu-id="5cfa4-106">Get a general understanding of [how consent allows a resource owner to govern an application's access to resources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent).</span></span>
- <span data-ttu-id="5cfa4-107">Ознакомьтесь с пошаговым руководством по [реализации согласия в инфраструктуре согласия Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="5cfa4-107">Get a step-by-step overview of [how the Azure AD consent framework implements consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework).</span></span>
- <span data-ttu-id="5cfa4-108">Получите более подробные сведения об [использовании инфраструктуры согласия в мультитенантном приложении](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent), чтобы реализовать согласие пользователя и администратора, с поддержкой нескольких дополнительных шаблонов многоуровневого приложения.</span><span class="sxs-lookup"><span data-stu-id="5cfa4-108">For more depth, learn [how a multi-tenant application can use the consent framework](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to implement "user" and "admin" consent, supporting more advanced multi-tier application patterns.</span></span>
- <span data-ttu-id="5cfa4-109">Узнайте подробнее о том, [как согласие поддерживается на уровне протокола OAuth 2.0 во время предоставления кода авторизации.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span><span class="sxs-lookup"><span data-stu-id="5cfa4-109">For more depth, learn [how consent is supported at the OAuth 2.0 protocol layer during the authorization code grant flow.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cfa4-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5cfa4-110">Next steps</span></span>
[<span data-ttu-id="5cfa4-111">StackOverflow в AzureAD</span><span class="sxs-lookup"><span data-stu-id="5cfa4-111">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
