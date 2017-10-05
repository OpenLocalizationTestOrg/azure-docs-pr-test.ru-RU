---
title: "Приступая к работе с системой обнаружения угроз хранилища данных SQL"
description: "Как приступить к работе с системой обнаружения угроз"
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
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="7ca22-103">Приступая к работе с системой обнаружения угроз</span><span class="sxs-lookup"><span data-stu-id="7ca22-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ca22-104">Аудит</span><span class="sxs-lookup"><span data-stu-id="7ca22-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="7ca22-105">Обнаружение угроз</span><span class="sxs-lookup"><span data-stu-id="7ca22-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7ca22-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="7ca22-106">Overview</span></span>
<span data-ttu-id="7ca22-107">Система обнаружения угроз обнаруживает подозрительную активность в базе данных, указывающую на наличие потенциальных угроз безопасности.</span><span class="sxs-lookup"><span data-stu-id="7ca22-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="7ca22-108">Система обнаружения угроз доступна в режиме предварительной версии и поддерживается в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7ca22-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="7ca22-109">Благодаря оповещениям безопасности о подозрительной активности система обнаружения угроз формирует дополнительный уровень безопасности, позволяющий клиентам обнаруживать потенциальные угрозы по мере возникновения и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="7ca22-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="7ca22-110">Пользователи могут анализировать подозрительные события с помощью [аудита хранилища данных SQL Azure](sql-data-warehouse-auditing-overview.md) , который позволяет определить причину таких событий (попытка получить доступ к данным в хранилище данных, нарушить их безопасность или использовать).</span><span class="sxs-lookup"><span data-stu-id="7ca22-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="7ca22-111">Система обнаружения угроз упрощает устранение потенциальных угроз безопасности хранилища данных, не требуя наличия у пользователя экспертных навыков в сфере безопасности либо умения работать в сложных системах отслеживания угроз.</span><span class="sxs-lookup"><span data-stu-id="7ca22-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="7ca22-112">Например, система обнаружения угроз обнаруживает определенную подозрительную активность в базе данных, указывающую на потенциальные попытки внедрения кода SQL.</span><span class="sxs-lookup"><span data-stu-id="7ca22-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="7ca22-113">Внедрение кода SQL — один из распространенных видов угроз безопасности веб-приложений в Интернете, используемый для получения несанкционированного доступа к приложениям, управляемым данными.</span><span class="sxs-lookup"><span data-stu-id="7ca22-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="7ca22-114">Взломщики используют уязвимые места приложения, чтобы ввести вредоносные инструкции SQL в поля ввода приложения, чтобы нарушить или изменить данные в базе данных.</span><span class="sxs-lookup"><span data-stu-id="7ca22-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="7ca22-115">Настройка системы обнаружения угроз для базы данных</span><span class="sxs-lookup"><span data-stu-id="7ca22-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="7ca22-116">Запустите портал Azure по адресу [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ca22-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7ca22-117">Перейдите к колонке настройки хранилища данных SQL, которое требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="7ca22-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="7ca22-118">В колонке "Параметры" выберите **Аудит и обнаружение угроз**.</span><span class="sxs-lookup"><span data-stu-id="7ca22-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Область навигации][1]
3. <span data-ttu-id="7ca22-120">В колонке настроек **Аудит и обнаружение угроз** установить переключатель аудита в положение **Вкл.**, после чего отобразятся настройки системы обнаружения угроз.</span><span class="sxs-lookup"><span data-stu-id="7ca22-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![Область навигации][2]
4. <span data-ttu-id="7ca22-122">Переведите переключатель системы обнаружения угроз в положение **ВКЛ.** .</span><span class="sxs-lookup"><span data-stu-id="7ca22-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="7ca22-123">Настройте список электронных адресов, на которые будут приходить оповещения безопасности в случае обнаружения подозрительной активности в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="7ca22-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="7ca22-124">В колонке настроек **Аудит и обнаружение угроз** щелкните **Сохранить**, чтобы сохранить новую или обновленную версию политики аудита и обнаружения угроз.</span><span class="sxs-lookup"><span data-stu-id="7ca22-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![Область навигации][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="7ca22-126">Анализ подозрительной активности в хранилище данных при обнаружении подозрительного события</span><span class="sxs-lookup"><span data-stu-id="7ca22-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="7ca22-127">При обнаружении подозрительной активности в базе данных вы получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="7ca22-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="7ca22-128">В электронном сообщении будет содержаться информация о подозрительном событии безопасности, включая характер подозрительной активности, имя базы данных и сервера, а также время, когда произошло событие.</span><span class="sxs-lookup"><span data-stu-id="7ca22-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="7ca22-129">Кроме того, в сообщении приводится информация о возможных причинах возникновения события, а также рекомендуемые действия по поиску и устранению потенциальной угрозы безопасности базы данных.</span><span class="sxs-lookup"><span data-stu-id="7ca22-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![Область навигации][4]
2. <span data-ttu-id="7ca22-131">В этом электронном сообщении щелкните ссылку **Журнал аудита SQL Azure** , которая запустит классический портал Azure, на котором будут показаны соответствующие записи аудита, зафиксированные примерно во время возникновения подозрительного события.</span><span class="sxs-lookup"><span data-stu-id="7ca22-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![Область навигации][5]
3. <span data-ttu-id="7ca22-133">Щелкните записи аудита, чтобы просмотреть более подробную информацию о подозрительной активности в базе данных, включая инструкции SQL, причины ошибки и IP-адрес клиента.</span><span class="sxs-lookup"><span data-stu-id="7ca22-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Область навигации][6]
4. <span data-ttu-id="7ca22-135">В колонке записей аудита щелкните **Открыть в Excel**, чтобы открыть предварительно настроенный шаблон Excel и импортировать для более детального анализа записи из журнала аудита, зафиксированные примерно во время возникновения подозрительного события.</span><span class="sxs-lookup"><span data-stu-id="7ca22-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="7ca22-136">
   **Примечание.** В Excel 2010 или более поздней версии требуется Power Query и параметр **Быстрое объединение**.</span><span class="sxs-lookup"><span data-stu-id="7ca22-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![Область навигации][7]
5. <span data-ttu-id="7ca22-138">Чтобы настроить параметр **Быстрое объединение**, на вкладке ленты **POWER QUERY** выберите **Параметры**, чтобы открыть диалоговое окно "Параметры".</span><span class="sxs-lookup"><span data-stu-id="7ca22-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="7ca22-139">Щелкните раздел «Конфиденциальность» и выберите в нем второй вариант — «Игнорировать уровни конфиденциальности и по возможности повышать производительность»:</span><span class="sxs-lookup"><span data-stu-id="7ca22-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![Область навигации][8]
6. <span data-ttu-id="7ca22-141">Чтобы загрузить записи журнала аудита SQL, убедитесь, что параметры на вкладке настроек установлены правильно, а затем откройте ленту «Данные» и нажмите кнопку «Обновить все».</span><span class="sxs-lookup"><span data-stu-id="7ca22-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![Область навигации][9]
7. <span data-ttu-id="7ca22-143">Результаты появятся на листе **Записи журнала аудита SQL** , что позволит выполнить более детальный анализ обнаруженной подозрительной активности, а также снизить степень влияния событий безопасности в приложении.</span><span class="sxs-lookup"><span data-stu-id="7ca22-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

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
