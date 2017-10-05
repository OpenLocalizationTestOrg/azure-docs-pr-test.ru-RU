---
title: "Azure Active Directory B2C: настраиваемые атрибуты | Документация Майкрософт"
description: "Как использовать настраиваемые атрибуты в Azure Active Directory B2C для сбора данных о потребителях."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="2b147-103">Azure Active Directory B2C: использование настраиваемых атрибутов для сбора данных о потребителях</span><span class="sxs-lookup"><span data-stu-id="2b147-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="2b147-104">Каталог Azure Active Directory (Azure AD) B2C поставляется со встроенным набором информации (атрибутов): "Given Name", "Surname", "City", "Postal Code" и т. д.</span><span class="sxs-lookup"><span data-stu-id="2b147-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="2b147-105">Однако у каждого потребительского приложения особые требования к атрибутам, которые им требуется собирать у потребителей.</span><span class="sxs-lookup"><span data-stu-id="2b147-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="2b147-106">С помощью Azure AD B2C можно расширить набор атрибутов, хранящихся в каждой учетной записи потребителя.</span><span class="sxs-lookup"><span data-stu-id="2b147-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="2b147-107">На [портале Azure](https://portal.azure.com/) можно создать настраиваемые атрибуты и использовать их в политиках регистрации, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2b147-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="2b147-108">Можно также читать и записывать эти атрибуты с помощью [API Graph Azure AD](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2b147-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2b147-109">Настраиваемые атрибуты используют [расширения схемы каталога API Graph Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b147-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="2b147-110">Создание настраиваемого атрибута</span><span class="sxs-lookup"><span data-stu-id="2b147-110">Create a custom attribute</span></span>
1. <span data-ttu-id="2b147-111">[Выполните эти действия, чтобы перейти к колонке функций B2C на портале Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="2b147-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="2b147-112">Щелкните **Атрибуты пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2b147-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="2b147-113">Нажмите **+Добавить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="2b147-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="2b147-114">Введите **имя** настраиваемого атрибута (например, ShoeSize) и, при необходимости, его **описание**.</span><span class="sxs-lookup"><span data-stu-id="2b147-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="2b147-115">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2b147-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2b147-116">Сейчас доступен только **тип данных** String.</span><span class="sxs-lookup"><span data-stu-id="2b147-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="2b147-117">Теперь настраиваемый атрибут доступен в списке **Атрибуты пользователя**и может использоваться в ваших политиках регистрации.</span><span class="sxs-lookup"><span data-stu-id="2b147-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="2b147-118">Использование настраиваемого атрибута в политике регистрации</span><span class="sxs-lookup"><span data-stu-id="2b147-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="2b147-119">[Выполните эти действия, чтобы перейти к колонке функций B2C на портале Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="2b147-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="2b147-120">Щелкните **Политики регистрации**.</span><span class="sxs-lookup"><span data-stu-id="2b147-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="2b147-121">Откройте политику регистрации (например B2C_1_SiUp), щелкнув ее.</span><span class="sxs-lookup"><span data-stu-id="2b147-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="2b147-122">Щелкните **Изменить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="2b147-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="2b147-123">Щелкните **Атрибуты регистрации** и выберите настраиваемый атрибут (например, ShoeSize).</span><span class="sxs-lookup"><span data-stu-id="2b147-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="2b147-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2b147-124">Click **OK**.</span></span>
5. <span data-ttu-id="2b147-125">Щелкните **Утверждения приложения** и выберите настраиваемый атрибут.</span><span class="sxs-lookup"><span data-stu-id="2b147-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="2b147-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2b147-126">Click **OK**.</span></span>
6. <span data-ttu-id="2b147-127">Щелкните **Сохранить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="2b147-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="2b147-128">Чтобы проверить взаимодействие с потребителем, можно использовать функцию «Выполнить» для политики.</span><span class="sxs-lookup"><span data-stu-id="2b147-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="2b147-129">Теперь вы увидите ShoeSize в списке атрибутов, собираемых во время регистрации потребителя, а также в токене, возвращаемом в приложение.</span><span class="sxs-lookup"><span data-stu-id="2b147-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="2b147-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="2b147-130">Notes</span></span>
* <span data-ttu-id="2b147-131">Помимо политик регистрации, настраиваемые атрибуты также можно использовать в политиках регистрации и входа в систему и в политиках изменения профилей.</span><span class="sxs-lookup"><span data-stu-id="2b147-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="2b147-132">В отношении настраиваемых атрибутов действует известное ограничение.</span><span class="sxs-lookup"><span data-stu-id="2b147-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="2b147-133">Они создаются только при первом использовании в любой политике, но не при добавлении в список **пользовательских атрибутов**.</span><span class="sxs-lookup"><span data-stu-id="2b147-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

