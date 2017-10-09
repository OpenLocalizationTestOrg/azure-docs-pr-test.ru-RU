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
# <a name="sql-database-threat-detection"></a>Обнаружение угроз для базы данных SQL

SQL обнаружение угроз обнаруживает аномальные действия, указывающее, необычные и потенциально вредоносных попыток tooaccess или воспользоваться баз данных.

## <a name="overview"></a>Обзор

Обнаружение угроз SQL предоставляет новый уровень безопасности, которая позволяет клиентам toodetect и отвечать toopotential угроз, как только они происходят, предоставляя предупреждения системы безопасности о подозрительной активности.  Пользователи получают оповещения о подозрительных действиях с базами данных, потенциальных уязвимостях, атаках путем внедрения кода SQL и аномальных закономерностях в доступе к базам данных. Предупреждения для обнаружения угроз SQL предоставляют подробные сведения о подозрительной активности и рекомендуем действия, о том, как tooinvestigate и устранить угрозу hello. Пользователи могут анализировать hello подозрительных событий с помощью [аудита базы данных SQL](sql-database-auditing.md) toodetermine, если они являются результатом tooaccess попытки нарушения или воспользоваться hello базы данных. Обнаружение угроз база данных он простой tooaddress потенциальных угроз toohello без необходимости hello toobe специалист по безопасности или управлять повышенной безопасности, контроль различных систем.

Например путем внедрения кода SQL — один из hello общих Web вопросами безопасности приложений на hello Интернета, используемых tooattack управляемых данными приложений. Злоумышленникам воспользоваться преимуществами tooinject уязвимостей приложения злонамеренные инструкции SQL в поля записи приложения, нарушения или изменение данных в базе данных hello.

Обнаружение угроз SQL интегрирует предупреждения с [центра безопасности Azure](https://azure.microsoft.com/en-us/services/security-center/), и каждого защищенного сервера базы данных SQL будет взиматься плата по hello же price как стандартная центра безопасности Azure уровень, на 15 долларов США/узла/месяц, где каждый защищенный SQL Сервер базы данных считается за один узел. Мы приглашаем вас tootry его 60 дней для освобождения. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>Настройка обнаружения угроз для базы данных в hello портал Azure
1. Запустите hello Azure портала в [https://portal.azure.com](https://portal.azure.com).
2. Перейдите в колонку toohello конфигурации из базы данных SQL требуется toomonitor hello. В колонке параметров hello выберите **аудита и обнаружения угроз**. 
    ![Область навигации][1]
3. В hello **аудита и обнаружения угроз** Включение колонке конфигурации **ON** аудита, который выводит параметры обнаружения угроз hello.
  
    ![Область навигации][2]
4. Переведите переключатель системы обнаружения угроз в положение **ВКЛ.** .
5. Настройте hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальные действия базы данных.
6. Нажмите кнопку **Сохранить** в hello **аудита и угрозы обнаружения** toosave колонке hello новых или обновленных аудита и угрозы параметрами обнаружения.
       
    ![Область навигации][3]

## <a name="set-up-threat-detection-using-powershell"></a>Настройка обнаружения угроз с помощью PowerShell

Пример сценария см. в статье [Настройка аудита и обнаружения угроз для базы данных SQL с помощью PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>Анализ подозрительной активности в базе данных при обнаружении подозрительного события
1. При обнаружении подозрительной активности в базе данных вы получите уведомление по электронной почте. <br/>
   Hello электронной почты будут предоставлены сведения события hello подозрительные безопасности, включая характер hello hello аномальных действий, имя базы данных, имя сервера, имя приложения и время события hello. Кроме того hello и электронной почтой предоставляются сведения о возможных причинах и рекомендуемые действия tooinvestigate снизить базы данных toohello hello потенциальных угроз.<br/>
     
    ![Область навигации][4]
2. оповещение по электронной почте Hello включает журнал аудита SQL toohello прямую ссылку. Щелкнув этот ссылка запускает hello Azure portal и открывает hello SQL записи аудита вокруг hello время hello подозрительные события. Щелкните tooview записей аудита Дополнительные сведения о действиях hello подозрительные базы данных, сделав его проще toofind hello инструкций SQL, которые были выполнены (кто обращался к, что они сделали и когда) и определить, было ли событие hello законными или злонамеренного (например приложение Внедрение tooSQL уязвимость была злоумышленниками, кто-то нарушения конфиденциальных данных и т. д.).<br/>
   ![Область навигации][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>Просмотр оповещения об обнаружении угроз для базы данных в hello портал Azure

Оповещения об обнаружении угроз базы данных SQL интегрируются с [центром безопасности Azure](https://azure.microsoft.com/en-us/services/security-center/). Живой плитки безопасности SQL в колонке базы данных hello в hello Azure портала отслеживает состояние hello активными угрозами. 

   ![Область навигации][6]
   
1. При щелчке плитки безопасности SQL hello запускает колонке оповещения центра безопасности Azure hello и общие сведения о активными угрозами SQL обнаружил в базе данных hello. 

  ![Область навигации][7]

2. Если щелкнуть определенное оповещение, отобразятся дополнительные сведения и действия для изучения этой угрозы и устранения будущих угроз.

  ![Область навигации][8]


## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о обнаружение угроз, посетите hello [блог Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* Узнайте больше об [аудите базы данных SQL Azure](sql-database-auditing.md).
* Узнайте больше о [центре безопасности Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro).
* Дополнительные сведения о ценах см. в разделе hello [страница с ценами на базы данных SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* Пример сценария PowerShell см. в статье [Настройка аудита и обнаружения угроз для базы данных SQL с помощью PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


