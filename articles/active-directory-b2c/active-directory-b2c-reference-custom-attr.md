---
title: "Azure Active Directory B2C: настраиваемые атрибуты | Документация Майкрософт"
description: "Как toouse пользовательские атрибуты в Azure Active Directory B2C toocollect сведения о потребителей"
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
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="ba0a6-103">Azure Active Directory B2C: Используйте настраиваемые атрибуты toocollect информацию о потребителей</span><span class="sxs-lookup"><span data-stu-id="ba0a6-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="ba0a6-104">Каталог Azure Active Directory (Azure AD) B2C поставляется со встроенным набором информации (атрибутов): "Given Name", "Surname", "City", "Postal Code" и т. д.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="ba0a6-105">Однако каждый потребительском приложении имеет уникальные требования, на какие атрибуты toogather от объектов-получателей.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="ba0a6-106">С Azure AD B2C можно расширить набор атрибутов, хранящихся на каждой учетной записи потребителя hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="ba0a6-107">Можно создать настраиваемые атрибуты для hello [портал Azure](https://portal.azure.com/) и использовать его в вашей организации доступа к Интернету политики, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="ba0a6-108">Можно также чтение и запись данных атрибутов с помощью hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ba0a6-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ba0a6-109">Настраиваемые атрибуты используют [расширения схемы каталога API Graph Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba0a6-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="ba0a6-110">Создание настраиваемого атрибута</span><span class="sxs-lookup"><span data-stu-id="ba0a6-110">Create a custom attribute</span></span>
1. <span data-ttu-id="ba0a6-111">[Выполните эти действия toonavigate toohello B2C функции колонку на портал Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="ba0a6-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="ba0a6-112">Щелкните **Атрибуты пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="ba0a6-113">Нажмите кнопку **+ добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ba0a6-114">Укажите **имя** для hello настраиваемого атрибута (например, «ShoeSize») и при необходимости **описание**.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="ba0a6-115">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ba0a6-116">Только Здравствуйте, «String» **тип данных** в настоящее время доступна.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="ba0a6-117">Настраиваемый атрибут Hello теперь доступен в списке hello **атрибуты пользователя**и для использования в вашей организации доступа к Интернету политики.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="ba0a6-118">Использование настраиваемого атрибута в политике регистрации</span><span class="sxs-lookup"><span data-stu-id="ba0a6-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="ba0a6-119">[Выполните эти действия toonavigate toohello B2C функции колонку на портал Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="ba0a6-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="ba0a6-120">Щелкните **Политики регистрации**.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="ba0a6-121">Tooopen вашей регистрации политики (например, «B2C_1_SiUp») щелкните его.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="ba0a6-122">Нажмите кнопку **изменить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ba0a6-123">Нажмите кнопку **регистрации атрибуты** и выберите hello настраиваемого атрибута (например, «ShoeSize»).</span><span class="sxs-lookup"><span data-stu-id="ba0a6-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="ba0a6-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-124">Click **OK**.</span></span>
5. <span data-ttu-id="ba0a6-125">Нажмите кнопку **утверждений приложения** и выберите hello настраиваемого атрибута.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="ba0a6-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-126">Click **OK**.</span></span>
6. <span data-ttu-id="ba0a6-127">Нажмите кнопку **Сохранить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="ba0a6-128">Можно использовать функцию «Запуск» hello на hello политики tooverify hello возможности использования.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="ba0a6-129">Теперь следует в список атрибутов, собранные во время регистрации потребителя hello. в разделе «ShoeSize» и отображается в приложение hello маркера tooyour отправлен назад.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="ba0a6-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="ba0a6-130">Notes</span></span>
* <span data-ttu-id="ba0a6-131">Помимо политик регистрации, настраиваемые атрибуты также можно использовать в политиках регистрации и входа в систему и в политиках изменения профилей.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="ba0a6-132">В отношении настраиваемых атрибутов действует известное ограничение.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="ba0a6-133">Только для созданных hello первый раз, он используется в любую политику, а не при его добавлении toohello список **атрибуты пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ba0a6-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>

