---
title: "Обнаружение угроз для базы данных SQL Azure | Документация Майкрософт"
description: "Система обнаружения угроз обнаруживает подозрительную активность в базе данных, указывающую на наличие потенциальных угроз безопасности."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: bd3de9ed0131edc683763b0fe7f4a2ae74533944
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="93d6c-103">Обнаружение угроз для базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="93d6c-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="93d6c-104">Система обнаружения угроз SQL выявляет аномальные операции, указывающие на нестандартные и потенциально вредоносные попытки получить доступ к базам данных или воспользоваться их уязвимостями.</span><span class="sxs-lookup"><span data-stu-id="93d6c-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="93d6c-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="93d6c-105">Overview</span></span>

<span data-ttu-id="93d6c-106">Благодаря оповещениям безопасности о подозрительной активности система обнаружения угроз формирует дополнительный уровень безопасности, позволяющий клиентам обнаруживать потенциальные угрозы по мере возникновения и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="93d6c-106">SQL Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="93d6c-107">Пользователи получают оповещения о подозрительных действиях с базами данных, потенциальных уязвимостях, атаках путем внедрения кода SQL и аномальных закономерностях в доступе к базам данных.</span><span class="sxs-lookup"><span data-stu-id="93d6c-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="93d6c-108">Оповещения об обнаружении угроз SQL содержат сведения о подозрительных операциях и рекомендации о том, как исследовать причину угрозы и устранить ее.</span><span class="sxs-lookup"><span data-stu-id="93d6c-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how to investigate and mitigate the threat.</span></span> <span data-ttu-id="93d6c-109">Пользователи могут анализировать подозрительные события с помощью [аудита базы данных SQL](sql-database-auditing.md), который позволяет определить причину таких событий (попытка получить доступ к данным в базе данных, нарушить безопасность или использовать их уязвимость).</span><span class="sxs-lookup"><span data-stu-id="93d6c-109">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach, or exploit data in the database.</span></span> <span data-ttu-id="93d6c-110">Система обнаружения угроз упрощает устранение потенциальных угроз безопасности базы данных, не требуя наличия у пользователя экспертных навыков в сфере безопасности либо умения работать в сложных системах отслеживания угроз.</span><span class="sxs-lookup"><span data-stu-id="93d6c-110">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="93d6c-111">Например, внедрение кода SQL — один из распространенных видов угроз безопасности веб-приложений в Интернете, используемый для получения несанкционированного доступа к приложениям, управляемым данными.</span><span class="sxs-lookup"><span data-stu-id="93d6c-111">For example, SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="93d6c-112">Хакеры используют уязвимости приложения, чтобы ввести вредоносные инструкции SQL в поля ввода приложения, чтобы испортить или изменить данные в базе данных.</span><span class="sxs-lookup"><span data-stu-id="93d6c-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, breaching or modifying data in the database.</span></span>

<span data-ttu-id="93d6c-113">Оповещения об обнаружении угроз SQL интегрируются с оповещениями [центра безопасности Azure](https://azure.microsoft.com/en-us/services/security-center/). Каждый защищенный сервер базы данных SQL оплачивается по такому же тарифу, как и центр безопасности Azure категории "Стандартный" (15 долларов США за узел в месяц), где каждый защищенный сервер базы данных SQL считается как один узел.</span><span class="sxs-lookup"><span data-stu-id="93d6c-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at the same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="93d6c-114">Приглашаем воспользоваться бесплатным 60-дневным периодом.</span><span class="sxs-lookup"><span data-stu-id="93d6c-114">We invite you to try it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a><span data-ttu-id="93d6c-115">Настройка обнаружения угроз для базы данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="93d6c-115">Set up threat detection for your database in the Azure portal</span></span>
1. <span data-ttu-id="93d6c-116">Запустите портал Azure по адресу [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="93d6c-116">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="93d6c-117">Перейдите к колонке настройки базы данных SQL, которую требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="93d6c-117">Navigate to the configuration blade of the SQL Database you want to monitor.</span></span> <span data-ttu-id="93d6c-118">В колонке "Параметры" выберите **Аудит и обнаружение угроз**.</span><span class="sxs-lookup"><span data-stu-id="93d6c-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="93d6c-119">![Область навигации][1]</span><span class="sxs-lookup"><span data-stu-id="93d6c-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="93d6c-120">В колонке настроек **Аудит и обнаружение угроз** установите переключатель аудита в положение **Вкл.**, после чего отобразятся настройки обнаружения угроз.</span><span class="sxs-lookup"><span data-stu-id="93d6c-120">In the **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display the threat detection settings.</span></span>
  
    ![Область навигации][2]
4. <span data-ttu-id="93d6c-122">Переведите переключатель системы обнаружения угроз в положение **ВКЛ.** .</span><span class="sxs-lookup"><span data-stu-id="93d6c-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="93d6c-123">Настройте список электронных адресов, на которые будут приходить оповещения безопасности в случае обнаружения подозрительной активности в базе данных.</span><span class="sxs-lookup"><span data-stu-id="93d6c-123">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="93d6c-124">В колонке **Аудит и обнаружение угроз** щелкните **Сохранить**, чтобы сохранить новые или обновленные параметры аудита и обнаружения угроз.</span><span class="sxs-lookup"><span data-stu-id="93d6c-124">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection settings.</span></span>
       
    ![Область навигации][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="93d6c-126">Настройка обнаружения угроз с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="93d6c-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="93d6c-127">Пример сценария см. в статье [Настройка аудита и обнаружения угроз для базы данных SQL с помощью PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="93d6c-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="93d6c-128">Анализ подозрительной активности в базе данных при обнаружении подозрительного события</span><span class="sxs-lookup"><span data-stu-id="93d6c-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="93d6c-129">При обнаружении подозрительной активности в базе данных вы получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="93d6c-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="93d6c-130">В электронном сообщении будет содержаться информация о подозрительном событии безопасности, включая характер подозрительных операций, имя базы данных, имя сервера, имя приложения, а также время, когда произошло событие.</span><span class="sxs-lookup"><span data-stu-id="93d6c-130">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name, application name, and the event time.</span></span> <span data-ttu-id="93d6c-131">Кроме того, в сообщении будет приведена информация о возможных причинах возникновения события, а также рекомендуемые действия по поиску и устранению потенциальной угрозы безопасности базы данных.</span><span class="sxs-lookup"><span data-stu-id="93d6c-131">In addition, the email will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
     
    ![Область навигации][4]
2. <span data-ttu-id="93d6c-133">Оповещение по электронной почте содержит прямую ссылку на журнал аудита SQL.</span><span class="sxs-lookup"><span data-stu-id="93d6c-133">The email alert includes a direct link to the SQL Audit log.</span></span> <span data-ttu-id="93d6c-134">Если щелкнуть эту ссылку, откроется портал Azure и отобразятся записи аудита SQL, созданные во время подозрительного события.</span><span class="sxs-lookup"><span data-stu-id="93d6c-134">Clicking on this link launches the Azure portal and opens the SQL Audit records around the time of the suspicious event.</span></span> <span data-ttu-id="93d6c-135">Щелкните запись аудита, чтобы просмотреть дополнительные сведения о подозрительных действиях с базой данных. Это упростит поиск инструкций SQL, которые были выполнены (кто получил доступ, что сделал и когда), и позволит определить, было ли событие допустимым или злоумышленным (например, была использована уязвимость приложения для атаки путем внедрения кода SQL, кто-то нарушил конфиденциальность данных и т. д.).</span><span class="sxs-lookup"><span data-stu-id="93d6c-135">Click on an audit record to view more details on the suspicious database activities, making it easier to find the SQL statements that were executed (who accessed, what they did and when) and determine if the event was legitimate or malicious (e.g. application vulnerability to SQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="93d6c-136">
   ![Область навигации][5]</span><span class="sxs-lookup"><span data-stu-id="93d6c-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-the-azure-portal"></a><span data-ttu-id="93d6c-137">Изучение оповещений об обнаружении угроз базы данных на портале Azure</span><span class="sxs-lookup"><span data-stu-id="93d6c-137">Explore threat detection alerts for your database in the Azure portal</span></span>

<span data-ttu-id="93d6c-138">Оповещения об обнаружении угроз базы данных SQL интегрируются с [центром безопасности Azure](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="93d6c-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="93d6c-139">Динамический элемент системы безопасности SQL в колонке базы данных на портале Azure отображает состояние активных угроз.</span><span class="sxs-lookup"><span data-stu-id="93d6c-139">A live SQL security tile within the database blade in the Azure portal tracks the status of active threats.</span></span> 

   ![Область навигации][6]
   
1. <span data-ttu-id="93d6c-141">Если щелкнуть элемент системы безопасности SQL, откроется колонка оповещений центра безопасности Azure, содержащая обзор обнаруженных активных угроз для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="93d6c-141">Clicking on the SQL security tile launches the Azure Security Center alerts blade and provides an overview of active SQL threats detected on the database.</span></span> 

  ![Область навигации][7]

2. <span data-ttu-id="93d6c-143">Если щелкнуть определенное оповещение, отобразятся дополнительные сведения и действия для изучения этой угрозы и устранения будущих угроз.</span><span class="sxs-lookup"><span data-stu-id="93d6c-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Область навигации][8]


## <a name="next-steps"></a><span data-ttu-id="93d6c-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="93d6c-145">Next steps</span></span>

* <span data-ttu-id="93d6c-146">Узнайте больше об обнаружении угроз, посетив [блог Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/).</span><span class="sxs-lookup"><span data-stu-id="93d6c-146">Learn more about Threat Detection, visit the [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="93d6c-147">Узнайте больше об [аудите базы данных SQL Azure](sql-database-auditing.md).</span><span class="sxs-lookup"><span data-stu-id="93d6c-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="93d6c-148">Узнайте больше о [центре безопасности Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro).</span><span class="sxs-lookup"><span data-stu-id="93d6c-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="93d6c-149">Дополнительные сведения о ценах см. на [странице цен на Базу данных SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="93d6c-149">For more details on pricing, please see the [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="93d6c-150">Пример сценария PowerShell см. в статье [Настройка аудита и обнаружения угроз для базы данных SQL с помощью PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="93d6c-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


