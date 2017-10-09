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
# <a name="get-started-with-threat-detection"></a>Приступая к работе с системой обнаружения угроз
> [!div class="op_single_selector"]
> * [Аудит](sql-data-warehouse-auditing-overview.md)
> * [Обнаружение угроз](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>Обзор
Обнаружение угроз обнаруживает аномальные действия базы данных, указывающее базу данных toohello потенциальные угрозы безопасности. Система обнаружения угроз доступна в режиме предварительной версии и поддерживается в хранилище данных SQL.

Обнаружение угроз обеспечивает новый уровень безопасности, которая позволяет клиентам toodetect и отвечать toopotential угроз, как только они происходят, предоставляя предупреждения системы безопасности о подозрительной активности. Пользователи могут анализировать hello подозрительных событий с помощью [аудита хранилища данных Azure SQL](sql-data-warehouse-auditing-overview.md) toodetermine, если они являются результатом tooaccess попытки нарушения или воспользоваться hello хранилища данных.
Обнаружение угроз делает простой tooaddress потенциальных угроз toohello данных в хранилище без необходимости toobe hello специалист по безопасности или управлять повышенной безопасности, контроль различных систем.

Например, система обнаружения угроз обнаруживает определенную подозрительную активность в базе данных, указывающую на потенциальные попытки внедрения кода SQL. Внедрение кода SQL — одно из hello общих Web вопросами безопасности приложений на hello Интернета, используемых tooattack управляемых данными приложений. Злоумышленникам воспользоваться преимуществами tooinject уязвимостей приложения злонамеренные инструкции SQL в поля записи приложения, для нарушению или изменение данных в базе данных hello.

## <a name="set-up-threat-detection-for-your-database"></a>Настройка системы обнаружения угроз для базы данных
1. Здравствуйте, запустить портал Azure на [https://portal.azure.com](https://portal.azure.com).
2. Перейдите в колонке конфигурации toohello hello требуется toomonitor хранилище данных SQL. В колонке параметров hello выберите **аудита и обнаружения угроз**.
   
    ![Область навигации][1]
3. В hello **аудита и обнаружения угроз** Включение колонке конфигурации **ON** аудита, который будет отображать параметры обнаружения угроз hello.
   
    ![Область навигации][2]
4. Переведите переключатель системы обнаружения угроз в положение **ВКЛ.** .
5. Настройте hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальных данных складских процессов.
6. Нажмите кнопку **Сохранить** в hello **аудита и угрозы обнаружения** toosave колонке конфигурации hello новых или обновленных политику аудита и угрозы обнаружения.
   
    ![Область навигации][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>Анализ подозрительной активности в хранилище данных при обнаружении подозрительного события
1. При обнаружении подозрительной активности в базе данных вы получите уведомление по электронной почте. <br/>
   Hello электронной почты будут представлены сведения события hello подозрительные безопасности, включая характер hello hello аномальных действий, имя базы данных, время события сервера имя и hello. Кроме того он предоставит сведения о возможных причинах и рекомендуется tooinvestigate действия и устранить базы данных toohello hello потенциальных угроз.<br/>
   
    ![Область навигации][4]
2. В сообщении электронной почты hello, нажмите кнопку hello **журнал аудита SQL Azure** ссылку, которая будет запустите hello классический портал Azure и Показать hello соответствующие записи аудита вокруг hello время hello подозрительные события.
   
    ![Область навигации][5]
3. Дополнительные сведения о действия hello подозрительных баз данных, такие как инструкции SQL, щелкните tooview записей аудита hello сбоя IP причину и клиента.
   
    ![Область навигации][6]
4. В колонке hello записей аудита, щелкните **открыть в Excel** excel tooopen предварительно настроенный шаблон tooimport и выполнения углубленного анализа журнала аудита hello вокруг hello время hello подозрительные события.<br/>
   **Примечание:** в Excel 2010 или более поздней версии, Power Query и hello **Быстрое объединение** параметр является обязательным
   
    ![Область навигации][7]
5. tooconfigure hello **Быстрое объединение** параметр - в hello **POWER QUERY** выберите вкладку ленты **параметры** toodisplay диалогового окна параметров hello. Выберите раздел конфиденциальности hello и выберите второй параметр hello - «Игнорировать уровни конфиденциальности hello и повысить производительность»:
   
    ![Область навигации][8]
6. журналы аудита tooload SQL, убедитесь, что hello параметры на вкладке Параметры hello установлены правильно, а затем выберите ленту «Данные» hello и нажмите кнопку «Обновить все» hello.
   
    ![Область навигации][9]
7. Hello результаты отображаются в hello **журналы аудита SQL** лист, позволяющий более глубокого анализа toorun hello аномальных действий, которые были обнаружены и сократить влияние hello hello событий безопасности в приложении.

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
