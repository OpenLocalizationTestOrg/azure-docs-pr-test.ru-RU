---
title: "aaaThreat обнаружение – базы данных SQL Azure | Документы Microsoft"
description: "Обнаружение угроз обнаруживает аномальные действия базы данных, указывающее базу данных toohello потенциальные угрозы безопасности."
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
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="47c0f-103">Обнаружение угроз для базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="47c0f-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="47c0f-104">SQL обнаружение угроз обнаруживает аномальные действия, указывающее, необычные и потенциально вредоносных попыток tooaccess или воспользоваться баз данных.</span><span class="sxs-lookup"><span data-stu-id="47c0f-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="47c0f-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="47c0f-105">Overview</span></span>

<span data-ttu-id="47c0f-106">Обнаружение угроз SQL предоставляет новый уровень безопасности, которая позволяет клиентам toodetect и отвечать toopotential угроз, как только они происходят, предоставляя предупреждения системы безопасности о подозрительной активности.</span><span class="sxs-lookup"><span data-stu-id="47c0f-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="47c0f-107">Пользователи получают оповещения о подозрительных действиях с базами данных, потенциальных уязвимостях, атаках путем внедрения кода SQL и аномальных закономерностях в доступе к базам данных.</span><span class="sxs-lookup"><span data-stu-id="47c0f-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="47c0f-108">Предупреждения для обнаружения угроз SQL предоставляют подробные сведения о подозрительной активности и рекомендуем действия, о том, как tooinvestigate и устранить угрозу hello.</span><span class="sxs-lookup"><span data-stu-id="47c0f-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="47c0f-109">Пользователи могут анализировать hello подозрительных событий с помощью [аудита базы данных SQL](sql-database-auditing.md) toodetermine, если они являются результатом tooaccess попытки нарушения или воспользоваться hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="47c0f-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="47c0f-110">Обнаружение угроз база данных он простой tooaddress потенциальных угроз toohello без необходимости hello toobe специалист по безопасности или управлять повышенной безопасности, контроль различных систем.</span><span class="sxs-lookup"><span data-stu-id="47c0f-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="47c0f-111">Например путем внедрения кода SQL — один из hello общих Web вопросами безопасности приложений на hello Интернета, используемых tooattack управляемых данными приложений.</span><span class="sxs-lookup"><span data-stu-id="47c0f-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="47c0f-112">Злоумышленникам воспользоваться преимуществами tooinject уязвимостей приложения злонамеренные инструкции SQL в поля записи приложения, нарушения или изменение данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="47c0f-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="47c0f-113">Обнаружение угроз SQL интегрирует предупреждения с [центра безопасности Azure](https://azure.microsoft.com/en-us/services/security-center/), и каждого защищенного сервера базы данных SQL будет взиматься плата по hello же price как стандартная центра безопасности Azure уровень, на 15 долларов США/узла/месяц, где каждый защищенный SQL Сервер базы данных считается за один узел.</span><span class="sxs-lookup"><span data-stu-id="47c0f-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="47c0f-114">Мы приглашаем вас tootry его 60 дней для освобождения.</span><span class="sxs-lookup"><span data-stu-id="47c0f-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="47c0f-115">Настройка обнаружения угроз для базы данных в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="47c0f-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="47c0f-116">Запустите hello Azure портала в [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47c0f-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="47c0f-117">Перейдите в колонку toohello конфигурации из базы данных SQL требуется toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="47c0f-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="47c0f-118">В колонке параметров hello выберите **аудита и обнаружения угроз**.</span><span class="sxs-lookup"><span data-stu-id="47c0f-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="47c0f-119">![Область навигации][1]</span><span class="sxs-lookup"><span data-stu-id="47c0f-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="47c0f-120">В hello **аудита и обнаружения угроз** Включение колонке конфигурации **ON** аудита, который выводит параметры обнаружения угроз hello.</span><span class="sxs-lookup"><span data-stu-id="47c0f-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![Область навигации][2]
4. <span data-ttu-id="47c0f-122">Переведите переключатель системы обнаружения угроз в положение **ВКЛ.** .</span><span class="sxs-lookup"><span data-stu-id="47c0f-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="47c0f-123">Настройте hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальные действия базы данных.</span><span class="sxs-lookup"><span data-stu-id="47c0f-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="47c0f-124">Нажмите кнопку **Сохранить** в hello **аудита и угрозы обнаружения** toosave колонке hello новых или обновленных аудита и угрозы параметрами обнаружения.</span><span class="sxs-lookup"><span data-stu-id="47c0f-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![Область навигации][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="47c0f-126">Настройка обнаружения угроз с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="47c0f-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="47c0f-127">Пример сценария см. в статье [Настройка аудита и обнаружения угроз для базы данных SQL с помощью PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="47c0f-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="47c0f-128">Анализ подозрительной активности в базе данных при обнаружении подозрительного события</span><span class="sxs-lookup"><span data-stu-id="47c0f-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="47c0f-129">При обнаружении подозрительной активности в базе данных вы получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="47c0f-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="47c0f-130">Hello электронной почты будут предоставлены сведения события hello подозрительные безопасности, включая характер hello hello аномальных действий, имя базы данных, имя сервера, имя приложения и время события hello.</span><span class="sxs-lookup"><span data-stu-id="47c0f-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="47c0f-131">Кроме того hello и электронной почтой предоставляются сведения о возможных причинах и рекомендуемые действия tooinvestigate снизить базы данных toohello hello потенциальных угроз.</span><span class="sxs-lookup"><span data-stu-id="47c0f-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![Область навигации][4]
2. <span data-ttu-id="47c0f-133">оповещение по электронной почте Hello включает журнал аудита SQL toohello прямую ссылку.</span><span class="sxs-lookup"><span data-stu-id="47c0f-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="47c0f-134">Щелкнув этот ссылка запускает hello Azure portal и открывает hello SQL записи аудита вокруг hello время hello подозрительные события.</span><span class="sxs-lookup"><span data-stu-id="47c0f-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="47c0f-135">Щелкните tooview записей аудита Дополнительные сведения о действиях hello подозрительные базы данных, сделав его проще toofind hello инструкций SQL, которые были выполнены (кто обращался к, что они сделали и когда) и определить, было ли событие hello законными или злонамеренного (например приложение Внедрение tooSQL уязвимость была злоумышленниками, кто-то нарушения конфиденциальных данных и т. д.).</span><span class="sxs-lookup"><span data-stu-id="47c0f-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="47c0f-136">
   ![Область навигации][5]</span><span class="sxs-lookup"><span data-stu-id="47c0f-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="47c0f-137">Просмотр оповещения об обнаружении угроз для базы данных в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="47c0f-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="47c0f-138">Оповещения об обнаружении угроз базы данных SQL интегрируются с [центром безопасности Azure](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="47c0f-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="47c0f-139">Живой плитки безопасности SQL в колонке базы данных hello в hello Azure портала отслеживает состояние hello активными угрозами.</span><span class="sxs-lookup"><span data-stu-id="47c0f-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![Область навигации][6]
   
1. <span data-ttu-id="47c0f-141">При щелчке плитки безопасности SQL hello запускает колонке оповещения центра безопасности Azure hello и общие сведения о активными угрозами SQL обнаружил в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="47c0f-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![Область навигации][7]

2. <span data-ttu-id="47c0f-143">Если щелкнуть определенное оповещение, отобразятся дополнительные сведения и действия для изучения этой угрозы и устранения будущих угроз.</span><span class="sxs-lookup"><span data-stu-id="47c0f-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Область навигации][8]


## <a name="next-steps"></a><span data-ttu-id="47c0f-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47c0f-145">Next steps</span></span>

* <span data-ttu-id="47c0f-146">Дополнительные сведения о обнаружение угроз, посетите hello [блог Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="47c0f-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="47c0f-147">Узнайте больше об [аудите базы данных SQL Azure](sql-database-auditing.md).</span><span class="sxs-lookup"><span data-stu-id="47c0f-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="47c0f-148">Узнайте больше о [центре безопасности Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro).</span><span class="sxs-lookup"><span data-stu-id="47c0f-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="47c0f-149">Дополнительные сведения о ценах см. в разделе hello [страница с ценами на базы данных SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="47c0f-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="47c0f-150">Пример сценария PowerShell см. в статье [Настройка аудита и обнаружения угроз для базы данных SQL с помощью PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="47c0f-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


