---
title: "подписки aaaNo найдены ошибки при повторите toosign на портале tooAzure или в центре учетных записей Azure | Документы Microsoft"
description: "Предлагается решение hello подписки не найдены возникает ошибка проблемы при входе в портал tooAzure или центр учетных записей Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="4bc56-103">Ошибка "Подписки не найдены" на портале Azure или в Центре управления учетной записью Azure</span><span class="sxs-lookup"><span data-stu-id="4bc56-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="4bc56-104">Может появиться сообщение об ошибке «Подписки не найден» при попытке toosign в toohello [портал Azure](https://portal.azure.com/) или hello [центр учетных записей Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="4bc56-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="4bc56-105">В этой статье предлагается решение указанной проблемы.</span><span class="sxs-lookup"><span data-stu-id="4bc56-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="4bc56-106">Симптом</span><span class="sxs-lookup"><span data-stu-id="4bc56-106">Symptom</span></span>

<span data-ttu-id="4bc56-107">При попытке toosign в toohello [портал Azure](https://portal.azure.com/) или hello [центр учетных записей Azure](https://account.windowsazure.com/Subscriptions), появляется сообщение об ошибке после hello: «Подписки не найдены».</span><span class="sxs-lookup"><span data-stu-id="4bc56-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="4bc56-108">Причина:</span><span class="sxs-lookup"><span data-stu-id="4bc56-108">Cause</span></span>

<span data-ttu-id="4bc56-109">Эта проблема возникает, если учетная запись не предоставляет необходимых разрешений.</span><span class="sxs-lookup"><span data-stu-id="4bc56-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="4bc56-110">Решение</span><span class="sxs-lookup"><span data-stu-id="4bc56-110">Solution</span></span>

<span data-ttu-id="4bc56-111">Убедитесь, что войдите как администратор правильный hello.</span><span class="sxs-lookup"><span data-stu-id="4bc56-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="4bc56-112">Администратор учетной записи может получить доступ только hello центр учетных записей.</span><span class="sxs-lookup"><span data-stu-id="4bc56-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="4bc56-113">Администраторы служб (SA) и Соадминистраторами (CA) имеют только toohello разрешение доступа к порталу Azure, или hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4bc56-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="4bc56-114">Сценарий 1: Получено сообщение об ошибке в hello [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="4bc56-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="4bc56-115">toofix этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="4bc56-115">toofix this issue:</span></span>

* <span data-ttu-id="4bc56-116">Убедитесь, что правильных Azure directory выбран, щелкнув вашей учетной записи в правом верхнем углу hello hello.</span><span class="sxs-lookup"><span data-stu-id="4bc56-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Выберите hello каталогов в hello верхнему правому углу hello портал Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="4bc56-118">Если hello справа Azure directory выбран, но по-прежнему сообщение hello, [свою учетную запись, добавляемого в качестве владельца](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="4bc56-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="4bc56-119">Сценарий 2: Получено сообщение об ошибке в hello [центр учетных записей Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="4bc56-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="4bc56-120">Проверка hello учетной записью, используемой hello учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="4bc56-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="4bc56-121">tooverify кто Здравствуйте, администратор учетной записи, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4bc56-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="4bc56-122">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4bc56-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4bc56-123">Выберите меню концентратора hello **подписки**.</span><span class="sxs-lookup"><span data-stu-id="4bc56-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="4bc56-124">Выберите подписку hello требуется toocheck, а затем выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="4bc56-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="4bc56-125">Выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4bc56-125">Select **Properties**.</span></span> <span data-ttu-id="4bc56-126">Здравствуйте, администратор учетной записи подписки hello отображается в hello **администратор учетной записи** поле.</span><span class="sxs-lookup"><span data-stu-id="4bc56-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="4bc56-127">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="4bc56-127">Need help?</span></span> <span data-ttu-id="4bc56-128">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="4bc56-128">Contact support.</span></span>
<span data-ttu-id="4bc56-129">Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="4bc56-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
