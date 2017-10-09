---
title: "Azure Active Directory B2C: отключение проверки адреса электронной почты во время регистрации потребителя | Документация Майкрософт"
description: "Статьи, демонстрации, как toodisable электронной почты проверки во время регистрации в Azure Active Directory B2C потребителя"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="a6827-103">Azure Active Directory B2C: отключение проверки адреса электронной почты во время регистрации потребителя</span><span class="sxs-lookup"><span data-stu-id="a6827-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="a6827-104">При включении B2C Azure Active Directory (Azure AD) предоставляет получателя hello toosign возможности для приложений, предоставив адрес электронной почты и создание локальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a6827-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="a6827-105">Azure AD B2C гарантирует допустимых адресов электронной почты, требуя от потребителей tooverify их во время процесса регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="a6827-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="a6827-106">Он также препятствует вредоносных автоматизированный процесс формировать фиктивное учетные записи для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a6827-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="a6827-107">Некоторые разработчики приложений предпочитают tooskip проверки адреса электронной почты, во время процесса регистрации hello и вместо у потребителей проверить адрес электронной почты hello позднее.</span><span class="sxs-lookup"><span data-stu-id="a6827-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="a6827-108">toosupport это Azure AD B2C может быть настроенный toodisable проверки адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="a6827-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="a6827-109">Это создает гладкую процесс регистрации и предоставляет разработчикам hello гибкость toodifferentiate hello потребителями, которые проверили свой адрес электронной почты от этих потребителей, которые не были.</span><span class="sxs-lookup"><span data-stu-id="a6827-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="a6827-110">По умолчанию в политиках регистрации определено, что проверка адреса включена.</span><span class="sxs-lookup"><span data-stu-id="a6827-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="a6827-111">Используйте hello следующие шаги tooturn его из системы:</span><span class="sxs-lookup"><span data-stu-id="a6827-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="a6827-112">[Выполните эти действия toonavigate toohello B2C функции колонку на портал Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="a6827-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="a6827-113">В зависимости от своих настроек регистрации выберите **Sign-up policies** (Политики регистрации) или **Sign-up or sign-in policies** (Политики регистрации или входа).</span><span class="sxs-lookup"><span data-stu-id="a6827-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="a6827-114">Щелкните ваш tooopen политики (например, «B2C_1_SiUp») ее.</span><span class="sxs-lookup"><span data-stu-id="a6827-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="a6827-115">Нажмите кнопку **изменить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="a6827-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="a6827-116">Щелкните **Page UI Customization** (Настройка пользовательского интерфейса страницы).</span><span class="sxs-lookup"><span data-stu-id="a6827-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="a6827-117">Щелкните **страницу регистрации локальной учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="a6827-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="a6827-118">Нажмите кнопку **адрес электронной почты** в hello **имя** столбца в списке hello **регистрации атрибуты** раздела.</span><span class="sxs-lookup"><span data-stu-id="a6827-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="a6827-119">Переключить hello **требуется проверка** параметр слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="a6827-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="a6827-120">Нажмите кнопку **ОК** внизу hello, пока не достигнете hello **изменение политики** колонку.</span><span class="sxs-lookup"><span data-stu-id="a6827-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="a6827-121">Нажмите кнопку **Сохранить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="a6827-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="a6827-122">Готово!</span><span class="sxs-lookup"><span data-stu-id="a6827-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="a6827-123">Отключение проверки адреса электронной почты в процессе регистрации hello может привести к toospam.</span><span class="sxs-lookup"><span data-stu-id="a6827-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="a6827-124">Если отключена по умолчанию hello один рекомендуется добавлять свои собственные системы проверки.</span><span class="sxs-lookup"><span data-stu-id="a6827-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="a6827-125">Мы всегда являются предложения и откройте toofeedback!</span><span class="sxs-lookup"><span data-stu-id="a6827-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="a6827-126">Если возникли проблемы с этим разделом, или иметь рекомендации по улучшению это содержимое, мы ценим ваши отзывы hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="a6827-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="a6827-127">Для запросов, компонент, добавьте их слишком[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="a6827-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
