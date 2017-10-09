---
title: "Файл теста SIPI | Документы Microsoft"
description: "Файл toocheck ReadyForTest зависимости тестов"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="0f4c2-103">Файл SIPI теста</span><span class="sxs-lookup"><span data-stu-id="0f4c2-103">Sipi test file</span></span>

<span data-ttu-id="0f4c2-104">Из этого краткого руководства вы узнаете, как зарегистрировать приложение в клиенте Microsoft Azure Active Directory (Azure AD) B2C за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0f4c2-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="0f4c2-105">После завершения приложение регистрируется для использования в клиенте hello Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="0f4c2-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f4c2-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0f4c2-106">Prerequisites</span></span>

<span data-ttu-id="0f4c2-107">toobuild приложения, которое принимает потребителя регистрации и входе в систему, необходимо сначала приложения hello tooregister с клиентом Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="0f4c2-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="0f4c2-108">Получение вашего собственного клиента с помощью hello действия, описанные в [создание клиента Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0f4c2-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="0f4c2-109">Приложения, созданные из колонки hello Azure AD B2C в hello портал Azure, должна управляться из hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="0f4c2-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="0f4c2-110">При редактировании hello B2C приложений с помощью PowerShell или другого портала становятся не поддерживается и не работают с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0f4c2-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="0f4c2-111">Просмотреть сведения в hello [произошел сбой приложения](#faulted-apps) раздела.</span><span class="sxs-lookup"><span data-stu-id="0f4c2-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="0f4c2-112">Параметры tooB2C перехода</span><span class="sxs-lookup"><span data-stu-id="0f4c2-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="0f4c2-113">Войдите в toohello [портал Azure](https://portal.azure.com/) как глобальный администратор клиента hello B2C hello.</span><span class="sxs-lookup"><span data-stu-id="0f4c2-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="0f4c2-114">Выбор следующего действия в зависимости от типа приложения hello, регистрируемая:</span><span class="sxs-lookup"><span data-stu-id="0f4c2-114">Choose next steps based on hello application type you are registering:</span></span>
