---
title: "Файл теста SIPI | Документы Microsoft"
description: "Тестовый файл, чтобы проверить ReadyForTest зависимости"
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="45bc7-103">Файл SIPI теста</span><span class="sxs-lookup"><span data-stu-id="45bc7-103">Sipi test file</span></span>

<span data-ttu-id="45bc7-104">Из этого краткого руководства вы узнаете, как зарегистрировать приложение в клиенте Microsoft Azure Active Directory (Azure AD) B2C за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="45bc7-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="45bc7-105">Ознакомившись с этим руководством, вы зарегистрируете приложение для использования в клиенте Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="45bc7-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45bc7-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="45bc7-106">Prerequisites</span></span>

<span data-ttu-id="45bc7-107">Чтобы создать приложение с поддержкой регистрации и входа пользователей, его сначала нужно зарегистрировать с использованием клиента Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="45bc7-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="45bc7-108">Получите собственный клиент, следуя указаниям в статье о [создании клиента Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="45bc7-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="45bc7-109">Управление приложениями, созданными в колонке Azure AD B2C на портале Azure, должно осуществляться в том же расположении.</span><span class="sxs-lookup"><span data-stu-id="45bc7-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="45bc7-110">Если вы измените приложения B2C с помощью PowerShell или другого портала, их поддержка прекратится и они не будут работать с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="45bc7-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="45bc7-111">Дополнительные сведения см. в разделе [Неисправные приложения](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="45bc7-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="45bc7-112">Переход к параметрам B2C</span><span class="sxs-lookup"><span data-stu-id="45bc7-112">Navigate to B2C settings</span></span>

<span data-ttu-id="45bc7-113">Войдите на [портал Azure](https://portal.azure.com/) как глобальный администратор клиента B2C.</span><span class="sxs-lookup"><span data-stu-id="45bc7-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="45bc7-114">Выберите следующие действия в зависимости от типа приложения, которое регистрируется:</span><span class="sxs-lookup"><span data-stu-id="45bc7-114">Choose next steps based on the application type you are registering:</span></span>
