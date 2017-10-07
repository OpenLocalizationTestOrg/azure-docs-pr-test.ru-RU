---
title: "aaaGet запуска многофакторной проверки Подлинности Azure в облаке hello | Документы Microsoft"
description: "Это hello страница Microsoft Azure, многофакторной проверки подлинности, описывающий, как tooget работу с Azure MFA в облаке hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="64606-103">Приступая к работе с многофакторной проверкой подлинности в Azure в облаке hello</span><span class="sxs-lookup"><span data-stu-id="64606-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="64606-104">В этой статье рассматриваются как tooget запущена с помощью многофакторной проверки подлинности Azure в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="64606-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="64606-105">Hello следующих разделах содержатся сведения о как hello tooenable пользователей с помощью **классический портал Azure**.</span><span class="sxs-lookup"><span data-stu-id="64606-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="64606-106">Если вам нужны дополнительные сведения о том, как tooset копирование Azure Multi-factor Authentication для пользователей Office 365 в разделе [настроить многофакторную проверку подлинности для Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="64606-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![Многофакторной проверки Подлинности в облаке hello](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="64606-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="64606-108">Prerequisite</span></span>
<span data-ttu-id="64606-109">[Зарегистрируйтесь для получения подписки Azure](https://azure.microsoft.com/pricing/free-trial/) — Если у вас еще нет подписки Azure, необходимо toosign вверх по одной.</span><span class="sxs-lookup"><span data-stu-id="64606-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="64606-110">Если вы только начинаете работать со службой "Многофакторная идентификация Microsoft Azure" (MFA), используйте пробную подписку.</span><span class="sxs-lookup"><span data-stu-id="64606-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="64606-111">Включение многофакторной проверки подлинности в Azure</span><span class="sxs-lookup"><span data-stu-id="64606-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="64606-112">При условии, что у пользователей есть лицензии, которые включают многофакторной проверки подлинности Azure, нет элементов, которые требуются tooturn toodo на многофакторной проверки Подлинности Azure.</span><span class="sxs-lookup"><span data-stu-id="64606-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="64606-113">Для отдельных пользователей можно включить двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="64606-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="64606-114">Ниже перечислены Hello лицензий, включение многофакторной проверки Подлинности Azure</span><span class="sxs-lookup"><span data-stu-id="64606-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="64606-115">Многофакторная идентификация Microsoft Azure;</span><span class="sxs-lookup"><span data-stu-id="64606-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="64606-116">Azure Active Directory Premium;</span><span class="sxs-lookup"><span data-stu-id="64606-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="64606-117">Enterprise Mobility + Security.</span><span class="sxs-lookup"><span data-stu-id="64606-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="64606-118">Если у вас нет этих трех лицензий, или у вас нет toocover достаточное количество лицензий всех пользователей, которые ОК.</span><span class="sxs-lookup"><span data-stu-id="64606-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="64606-119">Достаточно toodo выполнить дополнительное действие и [создания поставщика многофакторной проверки подлинности](multi-factor-authentication-get-started-auth-provider.md) в вашем каталоге.</span><span class="sxs-lookup"><span data-stu-id="64606-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="64606-120">Включение двухфакторной проверки подлинности для пользователей</span><span class="sxs-lookup"><span data-stu-id="64606-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="64606-121">Используйте одну из процедур hello, перечисленных в [как toorequire двухшаговую проверку для пользователя или группы](multi-factor-authentication-get-started-user-states.md) toostart с помощью многофакторной проверки Подлинности Azure.</span><span class="sxs-lookup"><span data-stu-id="64606-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="64606-122">Вы можете tooenforce двухшаговую проверку для всех входов или проверки двухэтапный toorequire политики условного доступа можно создать только в том случае, если он имеет значение tooyou.</span><span class="sxs-lookup"><span data-stu-id="64606-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64606-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64606-123">Next Steps</span></span>
<span data-ttu-id="64606-124">Теперь, когда вы настроили многофакторной проверки подлинности Azure в облаке hello, можно настроить и настройку развертывания.</span><span class="sxs-lookup"><span data-stu-id="64606-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="64606-125">Дополнительные сведения см. в статье [Настройка службы "Многофакторная идентификация Microsoft Azure"](multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="64606-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

