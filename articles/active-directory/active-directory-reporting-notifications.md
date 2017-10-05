---
title: "Уведомления отчетов Azure Active Directory"
description: "Использование уведомлений отчетов Azure Active Directory для определения подозрительных событий во время входа в систему."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="36161-103">Уведомления отчетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36161-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="36161-104">Какие отчеты создают уведомления по электронной почте</span><span class="sxs-lookup"><span data-stu-id="36161-104">What reports generate email notifications</span></span>
<span data-ttu-id="36161-105">В настоящее время только отчеты «Нестандартные действия при входе» инициируют уведомления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="36161-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="36161-106">Что такое «нестандартные попытки входа»?</span><span class="sxs-lookup"><span data-stu-id="36161-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="36161-107">Нестандартные входы — это входы, которые определяет алгоритм машинного обучения, исходя из невозможности путешествия, а также аномального расположения входа и устройства, используемого для входа.</span><span class="sxs-lookup"><span data-stu-id="36161-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="36161-108">Это может означать, что с помощью этой учетной записи пытается войти злоумышленник.</span><span class="sxs-lookup"><span data-stu-id="36161-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="36161-109">Кто получает уведомления по электронной почте?</span><span class="sxs-lookup"><span data-stu-id="36161-109">Who receives the email notifications?</span></span>
<span data-ttu-id="36161-110">Сообщение отправляется всем глобальным администраторам, которым назначена лицензия Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="36161-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="36161-111">Чтобы убедиться, что сообщение доставлено, мы также отправляем его на альтернативный адрес электронной почты администраторов.</span><span class="sxs-lookup"><span data-stu-id="36161-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="36161-112">Администраторы должны включить адрес aad-alerts-noreply@mail.windowsazure.com в свой список надежных отправителей, чтобы не пропустить сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="36161-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="36161-113">Как часто отправляются эти сообщения?</span><span class="sxs-lookup"><span data-stu-id="36161-113">How often are these emails sent?</span></span>
<span data-ttu-id="36161-114">Письмо отправляется, если за последние 30 дней или с момента отправки последнего письма (в зависимости от того, что меньше) происходит 10 новых нестандартных операций входа.</span><span class="sxs-lookup"><span data-stu-id="36161-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="36161-115">Как получить доступ к отчету, указанному в сообщении электронной почты</span><span class="sxs-lookup"><span data-stu-id="36161-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="36161-116">Если щелкнуть ссылку, вы перейдете на страницу отчета на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="36161-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="36161-117">Чтобы получить доступ к отчету, необходимо одновременно быть:</span><span class="sxs-lookup"><span data-stu-id="36161-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="36161-118">администратором или соадминистратором подписки Azure;</span><span class="sxs-lookup"><span data-stu-id="36161-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="36161-119">глобальным администратором в каталоге с назначенной лицензией Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="36161-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="36161-120">Дополнительные сведения см. в разделе [Выпуски Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="36161-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="36161-121">Можно ли отключить эти сообщения?</span><span class="sxs-lookup"><span data-stu-id="36161-121">Can I turn off these emails?</span></span>
<span data-ttu-id="36161-122">Да, чтобы отключить уведомления об аномальных операциях входа на классическом портале Azure, щелкните **Настройка** и выберите **Отключено** в разделе **Уведомления**.</span><span class="sxs-lookup"><span data-stu-id="36161-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="36161-123">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="36161-123">What's next</span></span>
* <span data-ttu-id="36161-124">Интересуют доступные отчеты о безопасности, аудиту и действиях?</span><span class="sxs-lookup"><span data-stu-id="36161-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="36161-125">См. раздел [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="36161-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="36161-126">Начало работы с Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="36161-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="36161-127">Добавление фирменной символики компании на страницах  входа и панели доступа</span><span class="sxs-lookup"><span data-stu-id="36161-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

