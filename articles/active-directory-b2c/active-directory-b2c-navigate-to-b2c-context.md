---
title: "Azure Active Directory B2C. Переключение на клиент B2C | Документация Майкрософт"
description: "Как переключиться в контекст клиента Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 40d8d57d974a949fbdc0a06eeceb2d06bfbaa09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="switching-to-your-azure-ad-b2c-tenant"></a><span data-ttu-id="7f541-103">Переключение на клиент Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7f541-103">Switching to your Azure AD B2C tenant</span></span>

<span data-ttu-id="7f541-104">Чтобы настроить Azure AD B2C, вам нужно быть в контексте вашего клиента Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7f541-104">In order to configure Azure AD B2C, you need to be in the context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="7f541-105">Вход в клиент Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7f541-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="7f541-106">Чтобы перейти к вашему клиенту Azure AD B2C, необходимо войти на портал Azure как глобальный администратор клиента Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7f541-106">To navigate to your Azure AD B2C tenant, you must be logged into the Azure portal as a global administrator of the Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="7f541-107">Войдите на [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f541-107">Sign into the [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="7f541-108">Щелкните адрес электронной почты или картинку в правом верхнем углу, чтобы переключить клиентов.</span><span class="sxs-lookup"><span data-stu-id="7f541-108">Switch tenants by clicking your email address or picture in the top-right corner.</span></span>
1. <span data-ttu-id="7f541-109">В списке `Directory` выберите клиента Azure AD B2C, которым вы хотите управлять.</span><span class="sxs-lookup"><span data-stu-id="7f541-109">In the `Directory` list that appears, select the Azure AD B2C tenant that you wish to manage.</span></span>

<span data-ttu-id="7f541-110">Портал Azure обновится.</span><span class="sxs-lookup"><span data-stu-id="7f541-110">The Azure Portal will refresh.</span></span>  <span data-ttu-id="7f541-111">Теперь вы вошли на портал Azure в контексте вашего клиента Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7f541-111">Now you are signed into the Azure Portal in the context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-to-the-b2c-features-blade"></a><span data-ttu-id="7f541-112">Переход в колонку функций B2C</span><span class="sxs-lookup"><span data-stu-id="7f541-112">Navigate to the B2C features blade</span></span>

1. <span data-ttu-id="7f541-113">Нажмите кнопку **Обзор** в области навигации слева.</span><span class="sxs-lookup"><span data-stu-id="7f541-113">Click **Browse** on the left hand navigation.</span></span>
1. <span data-ttu-id="7f541-114">Щелкните **Больше служб**, а затем в области навигации слева найдите `Azure AD B2C`.</span><span class="sxs-lookup"><span data-stu-id="7f541-114">Click **> More services** and then search for `Azure AD B2C` in the left navigation pane.</span></span>  <span data-ttu-id="7f541-115">(Щелкните звезду слева от Azure AD B2C, чтобы закрепить его на левой начальной панели.)</span><span class="sxs-lookup"><span data-stu-id="7f541-115">(To pin to your left-hand Startboard, click the star to the left of Azure AD B2C)</span></span>
1. <span data-ttu-id="7f541-116">Для доступа к колонке с функциями B2C щелкните ярлык **Azure AD B2C** .</span><span class="sxs-lookup"><span data-stu-id="7f541-116">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![Снимок экрана: переход к колонке функций B2C](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="7f541-118">Вам необходимо быть глобальным администратором данного клиента B2C, чтобы получить доступ к колонке функций B2C.</span><span class="sxs-lookup"><span data-stu-id="7f541-118">You need to be a Global Administrator of the B2C tenant to be able to access the B2C features blade.</span></span> <span data-ttu-id="7f541-119">Доступ к ней невозможен для глобальных администраторов или пользователей из других клиентов.</span><span class="sxs-lookup"><span data-stu-id="7f541-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="7f541-120">Переключиться на клиент B2C можно с помощью переключателя клиента в правом верхнем углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7f541-120">You can switch to your B2C tenant by using the tenant switcher in the top right corner of the Azure portal.</span></span>
