---
title: "Отчетность Azure Active Directory: начало работы | Документация Майкрософт"
description: "Здравствуйте, списки различных доступных отчетов reporting Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="4974e-103">Приступая к работе со средством создания отчетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4974e-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="4974e-104">Что это</span><span class="sxs-lookup"><span data-stu-id="4974e-104">What it is</span></span>
<span data-ttu-id="4974e-105">Azure Active Directory (Azure AD) формирует отчеты о безопасности, активности и аудите каталога.</span><span class="sxs-lookup"><span data-stu-id="4974e-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="4974e-106">Ниже приведен список включенных отчетов hello:</span><span class="sxs-lookup"><span data-stu-id="4974e-106">Here's a list of hello reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="4974e-107">Отчеты о безопасности</span><span class="sxs-lookup"><span data-stu-id="4974e-107">Security reports</span></span>
* <span data-ttu-id="4974e-108">Попытки входа из неизвестных источников</span><span class="sxs-lookup"><span data-stu-id="4974e-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="4974e-109">"Операции входа после нескольких неудачных попыток";</span><span class="sxs-lookup"><span data-stu-id="4974e-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="4974e-110">"Операции входа из нескольких географических регионов".</span><span class="sxs-lookup"><span data-stu-id="4974e-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="4974e-111">Попытки входа с IP-адресов с подозрительными действиями</span><span class="sxs-lookup"><span data-stu-id="4974e-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="4974e-112">Нестандартные действия при входе</span><span class="sxs-lookup"><span data-stu-id="4974e-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="4974e-113">Попытки входа с возможно инфицированных устройств</span><span class="sxs-lookup"><span data-stu-id="4974e-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="4974e-114">Пользователи с аномальными событиями при входе</span><span class="sxs-lookup"><span data-stu-id="4974e-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="4974e-115">Отчеты об активности</span><span class="sxs-lookup"><span data-stu-id="4974e-115">Activity reports</span></span>
* <span data-ttu-id="4974e-116">Использование приложения: сводка</span><span class="sxs-lookup"><span data-stu-id="4974e-116">Application usage: summary</span></span>
* <span data-ttu-id="4974e-117">Использование приложения: подробности</span><span class="sxs-lookup"><span data-stu-id="4974e-117">Application usage: detailed</span></span>
* <span data-ttu-id="4974e-118">Панель мониторинга приложений</span><span class="sxs-lookup"><span data-stu-id="4974e-118">Application dashboard</span></span>
* <span data-ttu-id="4974e-119">Ошибки подготовки учетной записи</span><span class="sxs-lookup"><span data-stu-id="4974e-119">Account provisioning errors</span></span>
* <span data-ttu-id="4974e-120">Устройства отдельного пользователя</span><span class="sxs-lookup"><span data-stu-id="4974e-120">Individual user devices</span></span>
* <span data-ttu-id="4974e-121">Активность отдельного пользователя</span><span class="sxs-lookup"><span data-stu-id="4974e-121">Individual user Activity</span></span>
* <span data-ttu-id="4974e-122">Отчет о действиях групп</span><span class="sxs-lookup"><span data-stu-id="4974e-122">Groups activity report</span></span>
* <span data-ttu-id="4974e-123">Отчет о событиях регистрации для сброса пароля</span><span class="sxs-lookup"><span data-stu-id="4974e-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="4974e-124">Действие сброса пароля</span><span class="sxs-lookup"><span data-stu-id="4974e-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="4974e-125">Отчеты об аудите</span><span class="sxs-lookup"><span data-stu-id="4974e-125">Audit reports</span></span>
* <span data-ttu-id="4974e-126">Отчет об аудите каталога</span><span class="sxs-lookup"><span data-stu-id="4974e-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="4974e-127">Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="4974e-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="4974e-128">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="4974e-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="4974e-129">Конвейер отчетов</span><span class="sxs-lookup"><span data-stu-id="4974e-129">Reporting pipeline</span></span>
<span data-ttu-id="4974e-130">Hello отчетов конвейер состоит из трех основных этапов.</span><span class="sxs-lookup"><span data-stu-id="4974e-130">hello reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="4974e-131">Каждый раз при входе или проверка подлинности, происходит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="4974e-131">Every time a user signs in, or an authentication is made, hello following happens:</span></span>

* <span data-ttu-id="4974e-132">Во-первых проверки подлинности пользователя hello (успешно или неуспешно) и hello результат сохраняется в базах данных службы Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="4974e-132">First, hello user is authenticated (successfully or unsuccessfully), and hello result is stored in hello Azure Active Directory service databases.</span></span>
* <span data-ttu-id="4974e-133">Все недавние попытки пользователей войти в систему регулярно обрабатываются с определенными интервалами.</span><span class="sxs-lookup"><span data-stu-id="4974e-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="4974e-134">На этом этапе наши алгоритмы безопасности и поиска аномальных событий проверяют все недавние входы в систему на предмет подозрительных действий.</span><span class="sxs-lookup"><span data-stu-id="4974e-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="4974e-135">После обработки hello отчеты записываются, кэшируются и обработаны в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4974e-135">After processing, hello reports are written, cached, and served in hello Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="4974e-136">Время создания отчета</span><span class="sxs-lookup"><span data-stu-id="4974e-136">Report generation times</span></span>
<span data-ttu-id="4974e-137">Из-за toohello большой объем проверки подлинности и входа, что модули обрабатываемых hello платформы Azure AD hello последнего входа в систему обработки, в среднем старого один час.</span><span class="sxs-lookup"><span data-stu-id="4974e-137">Due toohello large volume of authentications and sign ins processed by hello Azure AD platform, hello most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="4974e-138">В редких случаях может потребоваться копирование too8 часы tooprocess hello последнего входа в систему.</span><span class="sxs-lookup"><span data-stu-id="4974e-138">In rare cases, it may take up too8 hours tooprocess hello most recent sign-ins.</span></span>

<span data-ttu-id="4974e-139">Изучив текст справки hello hello верхней части каждого отчета, можно найти вход hello последней обработки.</span><span class="sxs-lookup"><span data-stu-id="4974e-139">You can find hello most recent processed sign-in by examining hello help text at hello top of each report.</span></span>

![Текст справки hello верхней части каждого отчета](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="4974e-141">Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="4974e-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="4974e-142">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="4974e-142">Getting started</span></span>
### <a name="sign-into-hello-azure-classic-portal"></a><span data-ttu-id="4974e-143">Вход в hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="4974e-143">Sign into hello Azure classic portal</span></span>
<span data-ttu-id="4974e-144">Во-первых, необходимо toosign в hello [классический портал Azure](https://manage.windowsazure.com) администратор глобальной или соответствия.</span><span class="sxs-lookup"><span data-stu-id="4974e-144">First, you'll need toosign into hello [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="4974e-145">Также должен быть администратором службы подписки Azure или соадминистратора, или использовать hello» доступа tooAzure AD» подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4974e-145">You must also be an Azure subscription service administrator or co-administrator, or be using hello "Access tooAzure AD" Azure subscription.</span></span>

### <a name="navigate-tooreports"></a><span data-ttu-id="4974e-146">Перейдите tooReports</span><span class="sxs-lookup"><span data-stu-id="4974e-146">Navigate tooReports</span></span>
<span data-ttu-id="4974e-147">Отчеты tooview Перейдите вкладку отчеты toohello вверху hello вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="4974e-147">tooview Reports, navigate toohello Reports tab at hello top of your directory.</span></span>

<span data-ttu-id="4974e-148">Если вы впервые, просмотр отчетов hello, вам потребуется tooa tooagree-диалоговое окно перед просмотром отчетов hello.</span><span class="sxs-lookup"><span data-stu-id="4974e-148">If this is your first time viewing hello reports, you'll need tooagree tooa dialog box before you can view hello reports.</span></span> <span data-ttu-id="4974e-149">Это tooensure, что он допустим для администраторов в вашей организации tooview эти данные, которые может рассматриваться как конфиденциальные сведения, в некоторых странах.</span><span class="sxs-lookup"><span data-stu-id="4974e-149">This is tooensure that it's acceptable for admins in your organization tooview this data, which may be considered private information in some countries.</span></span>

![Диалоговое окно](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="4974e-151">Изучение каждого отчета</span><span class="sxs-lookup"><span data-stu-id="4974e-151">Explore each report</span></span>
<span data-ttu-id="4974e-152">Перейдите в каждой toosee hello отчета во время сбора и обработки входа в систему hello.</span><span class="sxs-lookup"><span data-stu-id="4974e-152">Navigate into each report toosee hello data being collected and hello sign-ins processed.</span></span> <span data-ttu-id="4974e-153">Можно найти [списка всех отчетов hello здесь](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="4974e-153">You can find a [list of all hello reports here](active-directory-reporting-guide.md).</span></span>

![Все отчеты](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a><span data-ttu-id="4974e-155">Загрузить hello отчеты в формате CSV</span><span class="sxs-lookup"><span data-stu-id="4974e-155">Download hello reports as CSV</span></span>
<span data-ttu-id="4974e-156">Каждый отчет можно загрузить как CSV-файл (с разделителями-запятыми).</span><span class="sxs-lookup"><span data-stu-id="4974e-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="4974e-157">Можно использовать эти файлы в Excel, PowerBI или анализа сторонних программ toofurther анализа данных.</span><span class="sxs-lookup"><span data-stu-id="4974e-157">You can use these files in Excel, PowerBI or third-party analysis programs toofurther analyze your data.</span></span>

<span data-ttu-id="4974e-158">любой отчет в виде CSV-ФАЙЛ, toodownload перейдите toohello отчета и нажмите кнопку «Загрузить» внизу hello.</span><span class="sxs-lookup"><span data-stu-id="4974e-158">toodownload any report as a CSV, navigate toohello report and click "Download" at hello bottom.</span></span>

![Кнопка загрузки](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="4974e-160">Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="4974e-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4974e-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4974e-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="4974e-162">Настройка оповещений в случае аномальных действий при входе в систему</span><span class="sxs-lookup"><span data-stu-id="4974e-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="4974e-163">Перейдите toohello вкладку «Настройка» каталога.</span><span class="sxs-lookup"><span data-stu-id="4974e-163">Navigate toohello "Configure" tab of your directory.</span></span>

<span data-ttu-id="4974e-164">Прокрутите toohello раздел «Уведомления».</span><span class="sxs-lookup"><span data-stu-id="4974e-164">Scroll toohello "Notifications" section.</span></span>

<span data-ttu-id="4974e-165">Включить или отключить раздел «Уведомления по электронной почте об аномальных попытках входа» hello.</span><span class="sxs-lookup"><span data-stu-id="4974e-165">Enable or disable hello "Email Notifications of Anomalous sign-ins" section.</span></span>

![Hello раздел уведомлений](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a><span data-ttu-id="4974e-167">Интеграция с hello API отчетов Azure AD</span><span class="sxs-lookup"><span data-stu-id="4974e-167">Integrate with hello Azure AD Reporting API</span></span>
<span data-ttu-id="4974e-168">В разделе [Приступая к работе с hello Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4974e-168">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="4974e-169">Включение службы Multi-Factor Authentication для пользователей</span><span class="sxs-lookup"><span data-stu-id="4974e-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="4974e-170">Выберите пользователя в отчете.</span><span class="sxs-lookup"><span data-stu-id="4974e-170">Select a user in a report.</span></span>

<span data-ttu-id="4974e-171">Нажмите кнопку «Включить многофакторную проверку Подлинности» hello hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="4974e-171">Click hello "Enable MFA" button at hello bottom of hello screen.</span></span>

![Кнопка многофакторной проверки подлинности Hello hello нижней части экрана приветствия](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="4974e-173">Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="4974e-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="4974e-174">Подробнее</span><span class="sxs-lookup"><span data-stu-id="4974e-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="4974e-175">Аудит событий</span><span class="sxs-lookup"><span data-stu-id="4974e-175">Audit events</span></span>
<span data-ttu-id="4974e-176">Дополнительные сведения о какие события подлежат аудиту в каталоге hello в [Azure Active Directory Reporting событий аудита](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="4974e-176">Learn about what events are audited in hello directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="4974e-177">Интеграция API</span><span class="sxs-lookup"><span data-stu-id="4974e-177">API Integration</span></span>
<span data-ttu-id="4974e-178">В разделе [Приступая к работе с hello Reporting API](active-directory-reporting-api-getting-started.md) и hello [справочная документация по API](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="4974e-178">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md) and hello [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="4974e-179">Будьте на связи</span><span class="sxs-lookup"><span data-stu-id="4974e-179">Get in touch</span></span>
<span data-ttu-id="4974e-180">Чтобы отправить отзыв, получить справку или задать вопросы, напишите электронное письмо по адресу [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="4974e-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="4974e-181">Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="4974e-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

