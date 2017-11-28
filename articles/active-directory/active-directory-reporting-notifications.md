---
title: "aaaAzure уведомления Reporting Active Directory"
description: "Как toouse hello уведомления отчетов Azure Active Directory для подозрительных входа в систему."
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
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="2b1fc-103">Уведомления отчетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b1fc-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="2b1fc-104">Какие отчеты создают уведомления по электронной почте</span><span class="sxs-lookup"><span data-stu-id="2b1fc-104">What reports generate email notifications</span></span>
<span data-ttu-id="2b1fc-105">В настоящее время только hello нестандартные действия при входе в триггерах отчетов действия уведомления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="2b1fc-106">Что такое «нестандартные попытки входа»?</span><span class="sxs-lookup"><span data-stu-id="2b1fc-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="2b1fc-107">Нестандартных попытках входа, которые идентифицируются нашей алгоритмов машинного обучения, на основе hello условие «невозможно переместиться», в сочетании с нестандартного расположения и устройства.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="2b1fc-108">Это может означать, что злоумышленник попытки toosign имени этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="2b1fc-109">Кто получает уведомления по электронной почте hello?</span><span class="sxs-lookup"><span data-stu-id="2b1fc-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="2b1fc-110">Hello электронное письмо отправляется tooall глобальных администраторов, которым была назначена лицензия Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="2b1fc-111">tooensure, оно будет доставлено, мы отправляем его также администраторы toohello запасной адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="2b1fc-112">Администраторы должны включить aad-alerts-noreply@mail.windowsazure.com в свой список надежных отправителей, чтобы не пропустить hello электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="2b1fc-113">Как часто отправляются эти сообщения?</span><span class="sxs-lookup"><span data-stu-id="2b1fc-113">How often are these emails sent?</span></span>
<span data-ttu-id="2b1fc-114">Hello электронное письмо отправляется в том случае, если 10 новых нестандартных вход действия выполняются в hello последние 30 дней или с момента последнего hello сообщения электронной почты было отправлено, какое значение меньше.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="2b1fc-115">Как получить доступ к отчетов hello, упомянутые в hello электронной почты?</span><span class="sxs-lookup"><span data-stu-id="2b1fc-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="2b1fc-116">При нажатии на ссылку hello, будет перенаправленный toohello страницы отчета в пределах hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="2b1fc-117">В порядке tooaccess Здравствуйте отчет, необходимо, чтобы оба toobe:</span><span class="sxs-lookup"><span data-stu-id="2b1fc-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="2b1fc-118">администратором или соадминистратором подписки Azure;</span><span class="sxs-lookup"><span data-stu-id="2b1fc-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="2b1fc-119">Глобальный администратор в каталоге hello и назначить лицензию Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="2b1fc-120">Дополнительные сведения см. в разделе [Выпуски Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="2b1fc-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="2b1fc-121">Можно ли отключить эти сообщения?</span><span class="sxs-lookup"><span data-stu-id="2b1fc-121">Can I turn off these emails?</span></span>
<span data-ttu-id="2b1fc-122">Да, tooturn вывод всех уведомлений, связанных с tooanomalous входа в систему в течение hello классический портал Azure, нажмите кнопку **Настройка**, а затем выберите **отключено** под hello **уведомления**раздел.</span><span class="sxs-lookup"><span data-stu-id="2b1fc-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="2b1fc-123">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="2b1fc-123">What's next</span></span>
* <span data-ttu-id="2b1fc-124">Интересуют доступные отчеты о безопасности, аудиту и действиях?</span><span class="sxs-lookup"><span data-stu-id="2b1fc-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="2b1fc-125">См. раздел [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="2b1fc-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="2b1fc-126">Начало работы с Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="2b1fc-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="2b1fc-127">Добавить корпоративную фирменную символику tooyour страницы входа и панели доступа</span><span class="sxs-lookup"><span data-stu-id="2b1fc-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

