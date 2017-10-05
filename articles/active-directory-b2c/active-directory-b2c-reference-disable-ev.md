---
title: "Azure Active Directory B2C: отключение проверки адреса электронной почты во время регистрации потребителя | Документация Майкрософт"
description: "В этой статье демонстрируется, как отключить проверку адреса электронной почты во время регистрации потребителя в Azure Active Directory B2C."
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
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="cb35e-103">Azure Active Directory B2C: отключение проверки адреса электронной почты во время регистрации потребителя</span><span class="sxs-lookup"><span data-stu-id="cb35e-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="cb35e-104">Когда этот параметр включен, служба Azure Active Directory (Azure AD) B2C предоставляет потребителю возможность зарегистрироваться для получения доступа к приложениям, предоставив адрес электронной почты и создав локальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="cb35e-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="cb35e-105">Чтобы убедиться, что адреса электронной почты являются действительными, Azure AD B2C требует от потребителей выполнить их проверку в процессе регистрации.</span><span class="sxs-lookup"><span data-stu-id="cb35e-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="cb35e-106">Также предотвращаются вредоносные автоматизированные процессы, создающие для приложений фальшивые учетные записи.</span><span class="sxs-lookup"><span data-stu-id="cb35e-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="cb35e-107">Некоторые разработчики приложений предпочитают пропустить проверку адреса электронной почты в процессе регистрации. При таком сценарии потребители должны будут проверить адрес позже.</span><span class="sxs-lookup"><span data-stu-id="cb35e-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="cb35e-108">Для этого в Azure AD B2C можно отключить проверку адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="cb35e-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="cb35e-109">Это позволяет упростить процедуру регистрации, а также дает разработчикам возможность разделить потребителей на прошедших проверку адреса и на тех, кто такую проверку еще не прошел.</span><span class="sxs-lookup"><span data-stu-id="cb35e-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="cb35e-110">По умолчанию в политиках регистрации определено, что проверка адреса включена.</span><span class="sxs-lookup"><span data-stu-id="cb35e-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="cb35e-111">Чтобы ее выключить, следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="cb35e-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="cb35e-112">[Выполните эти действия, чтобы перейти к колонке функций B2C на портале Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="cb35e-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="cb35e-113">В зависимости от своих настроек регистрации выберите **Sign-up policies** (Политики регистрации) или **Sign-up or sign-in policies** (Политики регистрации или входа).</span><span class="sxs-lookup"><span data-stu-id="cb35e-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="cb35e-114">Откройте политику (например B2C_1_SiUp), щелкнув ее.</span><span class="sxs-lookup"><span data-stu-id="cb35e-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="cb35e-115">Щелкните **Изменить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="cb35e-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="cb35e-116">Щелкните **Page UI Customization** (Настройка пользовательского интерфейса страницы).</span><span class="sxs-lookup"><span data-stu-id="cb35e-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="cb35e-117">Щелкните **страницу регистрации локальной учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="cb35e-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="cb35e-118">В столбце **Name** (Имя) в разделе **Sign-up attributes** (Атрибуты регистрации) щелкните **Email Address** (Адрес электронной почты).</span><span class="sxs-lookup"><span data-stu-id="cb35e-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="cb35e-119">Переключите параметр **Require verification** (Требовать проверку) в положение **No** (Нет).</span><span class="sxs-lookup"><span data-stu-id="cb35e-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="cb35e-120">Несколько раз нажмите кнопку **ОК** внизу, пока не откроется колонка **Изменение политики**.</span><span class="sxs-lookup"><span data-stu-id="cb35e-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="cb35e-121">Щелкните **Сохранить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="cb35e-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="cb35e-122">Готово!</span><span class="sxs-lookup"><span data-stu-id="cb35e-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="cb35e-123">Отключение проверки адреса электронной почты в процессе регистрации может привести к получению спама.</span><span class="sxs-lookup"><span data-stu-id="cb35e-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="cb35e-124">Если вы отключаете эту проверку по умолчанию, то рекомендуется добавить собственную систему проверки.</span><span class="sxs-lookup"><span data-stu-id="cb35e-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="cb35e-125">Мы всегда рады вашим отзывам и предложениям!</span><span class="sxs-lookup"><span data-stu-id="cb35e-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="cb35e-126">Если у вас возникли трудности с выполнением действий, описанных в этой статье или у вас есть рекомендации по улучшению этого материала, поделитесь с нами своими наблюдениями, воспользовавшись формой в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="cb35e-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="cb35e-127">Запросы функций оставляйте на форуме [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="cb35e-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>