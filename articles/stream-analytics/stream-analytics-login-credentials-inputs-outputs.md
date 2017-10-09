---
title: "Stream Analytics: смена учетных данных для источников входных данных и мест назначения выходных данных | Документация Майкрософт"
description: "Узнайте, как tooupdate hello учетные данные для Stream Analytics входов и выходов."
keywords: "учетные данные для входа в систему"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Смена учетных данных для входа в систему
## <a name="abstract"></a>Аннотация
Azure Stream Analytics сегодня не допускает замены hello учетные данные при вводе выводе во время выполнения задания hello.

Хотя Azure Stream Analytics поддерживает возобновление задания из последнего вывода, нам необходимо было tooshare hello весь процесс минимизации hello промежуток между hello остановка и запуск задания hello и поворот hello учетные данные для входа.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Часть 1 — Подготовка hello новый набор учетных данных:
Эта часть — применимо toohello после ввода вывода:

* Хранилище BLOB-объектов
* Концентраторы событий
* База данных SQL
* Хранилище таблиц

Сведения, касающиеся других источников входных данных и мест назначения выходных данных см. в части 2.

### <a name="blob-storagetable-storage"></a>Хранилище больших двоичных объектов и табличное хранилище
1. Расширения хранилища toohello перейдите на портал управления Azure hello:  
   ![рисунок1][graphic1]
2. Найдите hello хранилища, используемого в задание, а в его:  
   ![рисунок2][graphic2]
3. Выберите команду hello управление ключами доступа:  
   ![рисунок3][graphic3]
4. Между hello первичный ключ доступа и вторичный ключ доступа, hello **выбрать hello не используется в вашей работы**.
5. Нажмите кнопку повторного создания:   
   ![рисунок4][graphic4]
6. Скопируйте hello вновь созданный ключ:  
   ![рисунок5][graphic5]
7. По-прежнему tooPart 2.

### <a name="event-hubs"></a>Концентраторы событий
1. Расширения Service Bus toohello перейдите на портал управления Azure hello:  
   ![рисунок6][graphic6]
2. Найдите hello пространство имен служебной шины, используемые вашей работы и перейдите в него:  
   ![рисунок7][graphic7]
3. Если задание на hello пространства имен шины обслуживания использует политику общего доступа, перейдите к toostep 6  
4. Перейдите вкладку toohello концентраторов событий:  
   ![рисунок8][graphic8]
5. Найдите hello концентратора событий, используемых вашей работы и перейдите в него:  
   ![рисунок9][graphic9]
6. Воспользуйтесь toohello вкладке "Настройка".  
   ![рисунок10][graphic10]
7. На hello раскрывающегося списка имя политики найдите hello общего доступа от политики задания:  
   ![рисунок11][graphic11]
8. Между hello первичный ключ и вторичный ключ hello **выбрать hello не используется в вашей работы**.  
9. Нажмите кнопку повторного создания:   
   ![рисунок12][graphic12]
10. Скопируйте hello вновь созданный ключ:  
   ![рисунок13][graphic13]
11. По-прежнему tooPart 2.  

### <a name="sql-database"></a>База данных SQL
> [!NOTE]
> Примечание: необходимо будет tooconnect toohello службы базы данных SQL. Мы будем tooshow toodo это с помощью hello возможности управления на hello портала управления Azure, но вы можете toouse некоторые клиентские средства, как SQL Server Management Studio также.
>
> 

1. Расширение базы данных SQL toohello перейдите на портале управления Azure hello:  
   ![рисунок14][graphic14]
2. Найдите hello базы данных SQL, используемой вашей работы и **щелкните на сервере hello** ссылку hello же строки:  
   ![рисунок15][graphic15]
3. Выберите команду Управление hello:  
   ![рисунок16][graphic16]
4. Введите главный ключ базы данных:   
   ![рисунок17][graphic17]
5. Введите свои имя пользователя и пароль и нажмите кнопку "Вход":   
   ![рисунок18][graphic18]
6. Щелкните "Создать запрос":   
   ![рисунок19][graphic19]
7. Тип в hello следующий запрос, заменив < login_name > — именем пользователя и замена <enterStrongPasswordHere> с новым паролем:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Щелкните "Выполнить":   
   ![рисунок20][graphic20]
9. Вернитесь обратно toostep 2, и это время щелкните hello базы данных:  
   ![рисунок21][graphic21]
10. Выберите команду Управление hello:  
   ![рисунок22][graphic22]
11. Введите свои имя пользователя и пароль и нажмите кнопку "Вход":   
   ![рисунок23][graphic23]
12. Щелкните "Создать запрос":   
   ![рисунок24][graphic24]
13. Введите следующий запрос, заменив < имя_пользователя > с именем, по которому требуется tooidentify hello это имя входа в контексте hello этой базы данных (вы можете предоставить hello одинаковое значение, заданное для < login_name >, например) и замены < login_name > новое имя пользователя:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Щелкните "Выполнить":   
   ![рисунок25][graphic25]
15. Теперь необходимо предоставить нового пользователя с hello же роли и имели пользовательскими правами.
16. По-прежнему tooPart 2.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>Часть 2: Привет остановка задания Stream Analytics
1. Расширение Stream Analytics toohello перейдите на портал управления Azure hello:  
   ![рисунок26][graphic26]
2. Найдите задание и перейдите к нему:   
   ![рисунок27][graphic27]
3. Go toohello входов вкладку или hello выходы зависимости от того, который требуется сменить hello учетные данные на вход или выход.  
   ![рисунок28][graphic28]
4. Выберите команду Stop hello и убедитесь, что задание hello остановлена:  
   ![graphic29][graphic29] ожидания toostop задания hello.
5. Найдите hello ввода вывода требуется toorotate учетные данные на и вернитесь в него:  
   ![рисунок30][graphic30]
6. Продолжайте tooPart 3.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>Часть 3: Изменение hello учетные данные в задание Stream Analytics hello
### <a name="blob-storagetable-storage"></a>Хранилище больших двоичных объектов и табличное хранилище
1. Найти поле ключа учетной записи хранения hello и вставьте в него к вновь созданному ключу:  
   ![рисунок31][graphic31]
2. Выберите команды "Сохранить" hello и подтвердить сохранение изменений:  
   ![рисунок32][graphic32]
3. При сохранении изменений автоматически запускается проверка подключения. Убедитесь, что она прошла успешно.
4. Продолжайте tooPart 4.

### <a name="event-hubs"></a>Концентраторы событий
1. Найти поле ключ политики концентратора событий hello и вставьте в него к вновь созданному ключу:  
   ![рисунок33][graphic33]
2. Выберите команды "Сохранить" hello и подтвердить сохранение изменений:  
   ![рисунок34][graphic34]
3. При сохранении изменений автоматически запускается проверка подключения. Убедитесь, что она прошла успешно.
4. Продолжайте tooPart 4.

### <a name="power-bi"></a>Power BI
1. Щелкните hello Renew авторизации:  

   ![рисунок35][graphic35]
2. Вы получите hello, после подтверждения:  

   ![рисунок36][graphic36]
3. Выберите команды "Сохранить" hello и подтвердить сохранение изменений:  
   ![рисунок37][graphic37]
4. При сохранении изменений автоматически запускается проверка подключения. Убедитесь, что она прошла успешно.
5. Продолжайте tooPart 4.

### <a name="sql-database"></a>База данных SQL
1. Найти hello поля имя пользователя и пароль и вставляется в только что созданный набор учетных данных:  
   ![рисунок38][graphic38]
2. Выберите команды "Сохранить" hello и подтвердить сохранение изменений:  
   ![рисунок39][graphic39]
3. При сохранении изменений автоматически запускается проверка подключения. Убедитесь, что она прошла успешно.  
4. Продолжайте tooPart 4.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Часть 4. Запуск задания с момента последней остановки
1. Покинуть Здравствуй ввода-вывода:  
   ![рисунок40][graphic40]
2. Щелкните команду Start hello:  
   ![рисунок41][graphic41]
3. Выберите время последней остановки hello и нажмите кнопку ОК:  
   ![рисунок42][graphic42]
4. Продолжайте tooPart 5.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>Часть 5: Удаление hello старый набор учетных данных
Эта часть — применимо toohello после ввода вывода:

* Хранилище BLOB-объектов
* Концентраторы событий
* База данных SQL
* Хранилище таблиц

### <a name="blob-storagetable-storage"></a>Хранилище больших двоичных объектов и табличное хранилище
Повторите часть 1 для hello ключ доступа, который ранее использовался путем задания toorenew hello теперь неиспользуемый ключ доступа.

### <a name="event-hubs"></a>Концентраторы событий
Повторите часть 1 для hello ключ, который ранее использовался путем задания toorenew hello теперь неиспользуемый ключ.

### <a name="sql-database"></a>База данных SQL
1. Вернитесь к предыдущему окну toohello окна запроса из части 1 шаг 7 и введите hello в следующем запросе, заменив < previous_login_name > hello имя пользователя, который ранее использовался путем задания:  
   `DROP LOGIN <previous_login_name>`  
2. Щелкните "Выполнить":   
   ![рисунок43][graphic43]  

Вы должны получить hello, после подтверждения: 

    Command(s) completed successfully.

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

