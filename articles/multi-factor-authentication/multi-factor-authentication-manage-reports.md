---
title: "отчеты о aaaAccess и использовании для многофакторной проверки Подлинности Azure | Документы Microsoft"
description: "Описывает, каким образом toouse hello функции многофакторной проверки подлинности Azure - отчеты."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="af566-103">Отчеты в службе Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="af566-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="af566-104">Azure Multi-Factor Authentication предоставляет несколько типов отчетов, которые могут быть полезны для вас и вашей организации.</span><span class="sxs-lookup"><span data-stu-id="af566-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="af566-105">Эти отчеты доступны через портал управления многофакторной проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="af566-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="af566-106">Hello ниже приведен список доступных отчетов hello:</span><span class="sxs-lookup"><span data-stu-id="af566-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="af566-107">Отчет</span><span class="sxs-lookup"><span data-stu-id="af566-107">Report</span></span> | <span data-ttu-id="af566-108">Описание</span><span class="sxs-lookup"><span data-stu-id="af566-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="af566-109">Использование</span><span class="sxs-lookup"><span data-stu-id="af566-109">Usage</span></span> |<span data-ttu-id="af566-110">сведения об отображении отчеты об использовании Hello на общем использовании, Сводка пользователей и сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="af566-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="af566-111">Состояние серверов</span><span class="sxs-lookup"><span data-stu-id="af566-111">Server Status</span></span> |<span data-ttu-id="af566-112">Этот отчет отображает состояние hello многофакторной проверки подлинности серверов, связанных с вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="af566-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="af566-113">Журнал заблокированных пользователей</span><span class="sxs-lookup"><span data-stu-id="af566-113">Blocked User History</span></span> |<span data-ttu-id="af566-114">Эти отчеты Показать журнал запросов tooblock hello или разблокирование пользователей.</span><span class="sxs-lookup"><span data-stu-id="af566-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="af566-115">Журнал обойденных пользователей</span><span class="sxs-lookup"><span data-stu-id="af566-115">Bypassed User History</span></span> |<span data-ttu-id="af566-116">Показывает историю hello toobypass запросы многофакторной проверки подлинности для номера телефона пользователя.</span><span class="sxs-lookup"><span data-stu-id="af566-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="af566-117">Предупреждение о мошенничестве</span><span class="sxs-lookup"><span data-stu-id="af566-117">Fraud Alert</span></span> |<span data-ttu-id="af566-118">Показывает историю оповещений о мошенничестве, отправленных в течение указанного диапазона дат hello.</span><span class="sxs-lookup"><span data-stu-id="af566-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="af566-119">Поставлено в очередь</span><span class="sxs-lookup"><span data-stu-id="af566-119">Queued</span></span> |<span data-ttu-id="af566-120">Отображается список отчетов, поставленных в очередь для обработки, и их состояние.</span><span class="sxs-lookup"><span data-stu-id="af566-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="af566-121">Ссылка toodownload или представления отчета hello предоставляется после завершения отчета hello.</span><span class="sxs-lookup"><span data-stu-id="af566-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="af566-122">Просмотр отчетов</span><span class="sxs-lookup"><span data-stu-id="af566-122">View reports</span></span>
1. <span data-ttu-id="af566-123">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="af566-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="af566-124">В левой части экрана приветствия выберите Active Directory.</span><span class="sxs-lookup"><span data-stu-id="af566-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="af566-125">Выберите один из описанных ниже вариантов в зависимости от того, используются ли поставщики аутентификации.</span><span class="sxs-lookup"><span data-stu-id="af566-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="af566-126">**Вариант 1**: вкладку hello поставщики многофакторной проверки подлинности. Выберите поставщика многофакторной проверки Подлинности и нажмите кнопку hello **управление** кнопку в нижней части hello.</span><span class="sxs-lookup"><span data-stu-id="af566-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="af566-127">**Вариант 2**: выберите ваш каталог и вернитесь toohello **Настройка** вкладки. В разделе "hello" многофакторной проверки подлинности, выберите **Управление параметрами службы**.</span><span class="sxs-lookup"><span data-stu-id="af566-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="af566-128">Hello нижней части страницы приветствия параметры многофакторной проверки Подлинности службы нажмите кнопку hello ссылка toohello перейти на портал.</span><span class="sxs-lookup"><span data-stu-id="af566-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="af566-129">В hello портала управления Azure Multi-factor Authentication, выберите тип hello отчета из hello **просмотра отчета** раздела hello навигации слева.</span><span class="sxs-lookup"><span data-stu-id="af566-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="af566-130"><center>![Облако](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="af566-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="af566-131">**Дополнительные ресурсы**</span><span class="sxs-lookup"><span data-stu-id="af566-131">**Additional Resources**</span></span>

* [<span data-ttu-id="af566-132">Для пользователей</span><span class="sxs-lookup"><span data-stu-id="af566-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="af566-133">Azure Multi-Factor Authentication в MSDN</span><span class="sxs-lookup"><span data-stu-id="af566-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
