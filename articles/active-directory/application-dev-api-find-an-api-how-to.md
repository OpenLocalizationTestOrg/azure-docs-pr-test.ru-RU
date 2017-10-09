---
title: "aaaHow toofind определенный интерфейс API, необходимые для приложения, разработанного | Документы Microsoft"
description: "Как требуется tooaccess конкретный API в пользовательских разрешений hello tooconfigure разработала приложение Azure AD"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="6a6cf-103">Как toofind определенный интерфейс API, необходимые для приложения, разработанного</span><span class="sxs-lookup"><span data-stu-id="6a6cf-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="6a6cf-104">TooAPIs доступа требуют настройки области доступа и ролей.</span><span class="sxs-lookup"><span data-stu-id="6a6cf-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="6a6cf-105">Если требуется tooexpose tooclient ресурсов приложения веб-API-интерфейсов приложений требуется tooconfigure области доступа и роли для hello API.</span><span class="sxs-lookup"><span data-stu-id="6a6cf-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="6a6cf-106">Если вы хотите tooaccess приложения клиента веб-API, необходимо API tooconfigure разрешения tooaccess hello в регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6a6cf-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="6a6cf-107">Настройка ресурсов приложения tooexpose веб-API</span><span class="sxs-lookup"><span data-stu-id="6a6cf-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="6a6cf-108">При предоставлении доступа к веб-API, hello API отображаемый в hello **выберите API** список при добавлении регистрации приложения tooan разрешения.</span><span class="sxs-lookup"><span data-stu-id="6a6cf-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="6a6cf-109">tooadd области доступа, следуйте hello действия, описанные в [Добавление доступа к области tooyour ресурсов приложения](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="6a6cf-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="6a6cf-110">Настройка клиентского приложения tooaccess веб-API</span><span class="sxs-lookup"><span data-stu-id="6a6cf-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="6a6cf-111">При добавлении регистрации приложения tooyour разрешения, вы можете **добавить доступ к API** tooexposed веб-API.</span><span class="sxs-lookup"><span data-stu-id="6a6cf-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="6a6cf-112">tooaccess веб-API, выполните hello действия, описанные в [добавить учетные данные или разрешения tooaccess веб-API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="6a6cf-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a6cf-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a6cf-113">Next steps</span></span>

-   [<span data-ttu-id="6a6cf-114">Интеграция приложений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a6cf-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="6a6cf-115">Основные сведения о манифесте приложения hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a6cf-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


