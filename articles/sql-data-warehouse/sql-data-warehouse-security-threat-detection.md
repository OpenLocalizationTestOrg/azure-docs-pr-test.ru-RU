---
title: "aaaGet к работе с обнаружением угроз для хранилища данных SQL"
description: "Как tooget запущена с обнаружением угроз"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="9a2a6-103">Приступая к работе с системой обнаружения угроз</span><span class="sxs-lookup"><span data-stu-id="9a2a6-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a2a6-104">Аудит</span><span class="sxs-lookup"><span data-stu-id="9a2a6-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="9a2a6-105">Обнаружение угроз</span><span class="sxs-lookup"><span data-stu-id="9a2a6-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9a2a6-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="9a2a6-106">Overview</span></span>
<span data-ttu-id="9a2a6-107">Обнаружение угроз обнаруживает аномальные действия базы данных, указывающее базу данных toohello потенциальные угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="9a2a6-108">Система обнаружения угроз доступна в режиме предварительной версии и поддерживается в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="9a2a6-109">Обнаружение угроз обеспечивает новый уровень безопасности, которая позволяет клиентам toodetect и отвечать toopotential угроз, как только они происходят, предоставляя предупреждения системы безопасности о подозрительной активности.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="9a2a6-110">Пользователи могут анализировать hello подозрительных событий с помощью [аудита хранилища данных Azure SQL](sql-data-warehouse-auditing-overview.md) toodetermine, если они являются результатом tooaccess попытки нарушения или воспользоваться hello хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="9a2a6-111">Обнаружение угроз делает простой tooaddress потенциальных угроз toohello данных в хранилище без необходимости toobe hello специалист по безопасности или управлять повышенной безопасности, контроль различных систем.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="9a2a6-112">Например, система обнаружения угроз обнаруживает определенную подозрительную активность в базе данных, указывающую на потенциальные попытки внедрения кода SQL.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="9a2a6-113">Внедрение кода SQL — одно из hello общих Web вопросами безопасности приложений на hello Интернета, используемых tooattack управляемых данными приложений.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="9a2a6-114">Злоумышленникам воспользоваться преимуществами tooinject уязвимостей приложения злонамеренные инструкции SQL в поля записи приложения, для нарушению или изменение данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="9a2a6-115">Настройка системы обнаружения угроз для базы данных</span><span class="sxs-lookup"><span data-stu-id="9a2a6-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="9a2a6-116">Здравствуйте, запустить портал Azure на [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a2a6-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9a2a6-117">Перейдите в колонке конфигурации toohello hello требуется toomonitor хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="9a2a6-118">В колонке параметров hello выберите **аудита и обнаружения угроз**.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Область навигации][1]
3. <span data-ttu-id="9a2a6-120">В hello **аудита и обнаружения угроз** Включение колонке конфигурации **ON** аудита, который будет отображать параметры обнаружения угроз hello.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![Область навигации][2]
4. <span data-ttu-id="9a2a6-122">Переведите переключатель системы обнаружения угроз в положение **ВКЛ.** .</span><span class="sxs-lookup"><span data-stu-id="9a2a6-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="9a2a6-123">Настройте hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальных данных складских процессов.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="9a2a6-124">Нажмите кнопку **Сохранить** в hello **аудита и угрозы обнаружения** toosave колонке конфигурации hello новых или обновленных политику аудита и угрозы обнаружения.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![Область навигации][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="9a2a6-126">Анализ подозрительной активности в хранилище данных при обнаружении подозрительного события</span><span class="sxs-lookup"><span data-stu-id="9a2a6-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="9a2a6-127">При обнаружении подозрительной активности в базе данных вы получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="9a2a6-128">Hello электронной почты будут представлены сведения события hello подозрительные безопасности, включая характер hello hello аномальных действий, имя базы данных, время события сервера имя и hello.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="9a2a6-129">Кроме того он предоставит сведения о возможных причинах и рекомендуется tooinvestigate действия и устранить базы данных toohello hello потенциальных угроз.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![Область навигации][4]
2. <span data-ttu-id="9a2a6-131">В сообщении электронной почты hello, нажмите кнопку hello **журнал аудита SQL Azure** ссылку, которая будет запустите hello классический портал Azure и Показать hello соответствующие записи аудита вокруг hello время hello подозрительные события.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![Область навигации][5]
3. <span data-ttu-id="9a2a6-133">Дополнительные сведения о действия hello подозрительных баз данных, такие как инструкции SQL, щелкните tooview записей аудита hello сбоя IP причину и клиента.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Область навигации][6]
4. <span data-ttu-id="9a2a6-135">В колонке hello записей аудита, щелкните **открыть в Excel** excel tooopen предварительно настроенный шаблон tooimport и выполнения углубленного анализа журнала аудита hello вокруг hello время hello подозрительные события.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="9a2a6-136">
   **Примечание:** в Excel 2010 или более поздней версии, Power Query и hello **Быстрое объединение** параметр является обязательным</span><span class="sxs-lookup"><span data-stu-id="9a2a6-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![Область навигации][7]
5. <span data-ttu-id="9a2a6-138">tooconfigure hello **Быстрое объединение** параметр - в hello **POWER QUERY** выберите вкладку ленты **параметры** toodisplay диалогового окна параметров hello.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="9a2a6-139">Выберите раздел конфиденциальности hello и выберите второй параметр hello - «Игнорировать уровни конфиденциальности hello и повысить производительность»:</span><span class="sxs-lookup"><span data-stu-id="9a2a6-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![Область навигации][8]
6. <span data-ttu-id="9a2a6-141">журналы аудита tooload SQL, убедитесь, что hello параметры на вкладке Параметры hello установлены правильно, а затем выберите ленту «Данные» hello и нажмите кнопку «Обновить все» hello.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![Область навигации][9]
7. <span data-ttu-id="9a2a6-143">Hello результаты отображаются в hello **журналы аудита SQL** лист, позволяющий более глубокого анализа toorun hello аномальных действий, которые были обнаружены и сократить влияние hello hello событий безопасности в приложении.</span><span class="sxs-lookup"><span data-stu-id="9a2a6-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
