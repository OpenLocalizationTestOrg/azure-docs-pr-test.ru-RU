---
title: "панели мониторинга aaaPower BI в Azure Stream Analytics | Документы Microsoft"
description: "Использовать в режиме реального времени потоковой передачи Power BI панель мониторинга toogather бизнес-аналитики и анализа больших объемов данных из задания Stream Analytics."
keywords: "панель мониторинга аналитики, панель мониторинга в режиме реального времени"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Stream Analytics и Power BI. Панель мониторинга для анализа потоковой передачи данных
Azure Stream Analytics дает преимущество tootake одного hello начальные средства бизнес-аналитики, [Microsoft Power BI](https://powerbi.com/). В этой статье вы узнаете, как создавать средства бизнес-аналитики, отображая в Power BI выходные данные заданий Azure Stream Analytics. Вы также узнаете, как toocreate и использовать панели мониторинга в режиме реального времени.

В этой статье продолжается с hello Stream Analytics [в режиме реального времени мошенничества](stream-analytics-real-time-fraud-detection.md) учебника. Он основан на hello рабочий процесс, созданный в этом учебнике и добавляет Power BI, выходные данные, чтобы вы можете визуализировать мошеннические телефонных звонков, которые определяются задание Streaming Analytics. 

Посмотрите [видео](https://www.youtube.com/watch?v=SGUpT-a99MA) об этом сценарии.


## <a name="prerequisites"></a>Предварительные требования

Прежде чем начать, убедитесь, что у вас есть следующие hello:

* Учетная запись Azure.
* Учетная запись для Power BI. Вы можете использовать рабочую или учебную учетную запись.
* Полную версию hello [в режиме реального времени мошенничества](stream-analytics-real-time-fraud-detection.md) учебника. Hello учебник содержит приложение, создающее вымышленной телефону метаданных. В учебнике hello Создание концентратора событий и отправки hello потоковой передачи концентратора событий toohello данных телефонный звонок. При написании запроса, определяющую мошеннические вызовов (вызовы из hello одно и тоже число в hello одновременную в разных местах). 


## <a name="add-power-bi-output"></a>Добавление Power BI в качестве места назначения выходных данных
В учебнике обнаружения мошенничества в режиме реального времени hello hello вывод направляется tooAzure хранилища больших двоичных объектов. В этом разделе добавьте вывода, который отправляет сведения tooPower бизнес-Аналитики.

1. Hello портал Azure откройте задание Streaming Analytics hello, созданного ранее. При использовании предлагаемое имя hello hello задание называется `sa_frauddetection_job_demo`.

2. Выберите hello **выходов** в середине hello панель мониторинга задания hello и затем выберите **+ добавить**.

3. В поле **Выходной псевдоним** введите `CallStream-PowerBI`. Вы можете использовать другое имя. В противном случае запишите его, поскольку его нужно имя hello. 

4. В поле **Приемник** выберите **Power BI**.

   ![Создание выхода для Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Щелкните **Авторизовать**.

    Откроется окно, где можно ввести учетные данные Azure (рабочей или учебной учетной записи). 

    ![Введите учетные данные для доступа к tooPower бизнес-Аналитики](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Введите свои учетные данные. Имейте в виду то при вводе учетных данных, можно также предоставить разрешение toohello Streaming Analytics задания tooaccess местных Power BI.

7. Когда вы будете перенаправлены toohello **новый Выход** колонке введите hello следующую информацию:

    * **Группы рабочей**: Выбор рабочей области в клиенте Power BI, где требуется набор данных toocreate hello.
    * **Имя набора данных.** Введите `sa-dataset`. Вы можете использовать другое имя. Если вы используете другое имя, запишите его.
    * **Имя таблицы.** Введите `fraudulent-calls`. Сейчас для вывода выходных данных из заданий Stream Analytics в Power BI можно использовать только одну таблицу в наборе данных.

    ![Рабочая область Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Если Power BI содержит источники данных и таблицы, для которых hello совпадают с именами hello те, которые указываются в задании Stream Analytics hello, перезаписываются существующих hello.
    > Мы не рекомендуем явным образом создавать набор данных и таблицу в учетной записи Power BI. Они создаются автоматически, если запустить задание Stream Analytics и hello заданий начинает инициализируемого выходные данные в Power BI. Если задание запрос не возвращает никаких результатов, hello набора данных и таблицы не создаются.
    >

8. Щелкните **Создать**.

Hello набор данных создается с hello следующие параметры:

* **defaultRetentionPolicy: BasicFIFO**. Для данных используется метод FIFO, максимальное число строк — 200 тыс.;
* **defaultMode: pushStreaming**: hello поддерживает набор данных потоковой передачи плитки и традиционные визуальных элементов на основе отчетов (так) (данные для отправки).

Сейчас нельзя создавать наборы данных с другими флагами.

Дополнительные сведения о наборах данных Power BI см. в разделе hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) ссылки.


## <a name="write-hello-query"></a>Написать запрос hello

1. Закрыть hello **выходов** колонки и возврата toohello задания колонку.

2. Нажмите кнопку hello **запроса** поле. 

3. Введите приветствия при следующем запросе. Этот запрос является подобный toohello самосоединение запрос, созданный в учебнике мошенничества hello. Hello отличается отправляет новый toohello результаты вывода был создан этот запрос (`CallStream-PowerBI`). 

    >[!NOTE]
    >Если не было имя входных данных hello `CallStream` в учебнике мошенничества hello, замените на имя `CallStream` в hello **FROM** и **JOIN** предложений в запросе hello.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. Щелкните **Сохранить**.


## <a name="test-hello-query"></a>Проверка запроса hello
Этот раздел необязательный, но мы рекомендуем ознакомиться с ним. 

1. Если приложение hello TelcoStreaming еще не запущен, запустите ее, выполнив следующие действия:

    * Откройте командное окно.
    * Последовательно выберите toohello папку, где hello telcogenerator.exe и telcodatagen.exe.config измененные файлы.
    * Выполните следующую команду hello.

            telcodatagen.exe 1000 .2 2

2. В hello **запроса** колонке нажмите кнопку Далее toohello точек hello `CallStream` входных данных, а затем выберите **выборку данных из входных данных**.

3. Укажите, что необходим трехминутный образец данных, и щелкните **ОК**. Подождите, пока выполняется уведомление, что hello данные выборок значений.

4. Щелкните **Тест** и убедитесь, что вы получаете результаты.


## <a name="run-hello-job"></a>Запустить задание hello

1. Убедитесь, что выполнение этого приложения hello TelcoStreaming.

2. Закрыть hello **запроса** колонку.

3. В колонке hello задания, нажмите кнопку **запустить**.

    ![Запустить задание Stream Analytics hello](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

Ваше задание Streaming Analytics запускает поиск мошеннические вызовы в hello входящего потока. Задание Hello также создает hello набора данных и таблицы в Power BI и начинает отправлять данные об toothem мошеннические вызовы hello.


## <a name="create-hello-dashboard-in-power-bi"></a>Создание панели мониторинга hello в Power BI

1. Go слишком[Powerbi.com](https://powerbi.com) и выполните вход с рабочей или школьной учетной записью. Если результат запроса задания Stream Analytics hello, отобразятся уже создан набор данных:

    ![Набор данных потоковой передачи в Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. В рабочей области щелкните **+&nbsp;Создать**.

    ![кнопки "Создать" Hello в рабочей области Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Создайте информационную панель и назовите ее `Fraudulent Calls`.

    ![Создание информационной панели и присвоение ей имени в рабочей области Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. Hello верхней части окна hello, нажмите кнопку **добавить плитку**выберите **ПОЛЬЗОВАТЕЛЬСКИЕ данные потоковой ПЕРЕДАЧИ**, а затем нажмите кнопку **Далее**.

    ![Пользовательский набор данных потоковой передачи](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. В области **Your datsets** (Ваши наборы данных) выберите свой набор данных и щелкните **Далее**.

    ![Ваш набор данных потоковой передачи](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. В разделе **тип визуализации**выберите **карты**, а затем в hello **поля** выберите **fraudulentcalls**.

    ![Сведения о визуализации для новой плитки](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. Щелкните **Далее**.

8. Заполните сведения о плитке, такие как заголовок и подзаголовок.

    ![Заголовок и подзаголовок для новой плитки](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. Нажмите кнопку **Применить**.

    Теперь у вас есть счетчик попыток совершения мошенничества.

    ![Счетчик попыток мошенничества](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. Hello выполните шаги tooadd плитки (начиная с шага 4) еще раз. На этот раз hello следующие:

    * При получении слишком**тип визуализации**выберите **график**. 
    * Добавьте ось и выберите **windowend**. 
    * Добавьте значение и выберите **fraudulentcalls**.
    * Для **toodisplay окно времени**выберите hello последние 10 минут.

    ![Создание плитки графика](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Щелкните **Далее**, добавьте заголовок и подзаголовок, а затем щелкните **Применить**.

    панели мониторинга Power BI Hello теперь содержатся два представления данных о мошенничестве вызовы обнаруженного в hello потоковой передачи данных.

    ![Готовая информационная панель Power BI, отображающая 2 плитки со сведениями о мошеннических вызовах](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Подробнее о Power BI

В этом учебнике показано как toocreate несколько видов визуализации для набора данных. Power BI позволяет создавать другие клиентские инструменты бизнес-аналитики для вашей организации. Дополнительные идеи см. следующие ресурсы hello.

* Другой пример панели мониторинга Power BI, посмотрите hello [Приступая к работе с Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) видео.
* Дополнительные сведения о настройке Streaming Analytics задания tooPower выходных данных бизнес-Аналитики и использование групп Power BI, проверьте hello [Power BI](stream-analytics-define-outputs.md#power-bi) раздел hello [выводит Stream Analytics](stream-analytics-define-outputs.md) статьи. 
* Дополнительные сведения об использовании Power BI см. в статье [Панели мониторинга в службе Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>Информация об ограничениях и рекомендациях
Сейчас Power BI можно вызывать примерно один раз в секунду. Визуальные элементы потоковой передачи поддерживают пакеты размером в 15 КБ. Кроме этого Сбой потоковой передачи визуальные элементы (но по-прежнему toowork push). Из-за этих ограничений Power BI пригоден наиболее естественным образом toocases, когда Azure Stream Analytics осуществляет сокращение загрузки значительного объема данных. Мы рекомендуем использовать «переворачивающееся» окно или tooensure окна «прыгающие» окна, принудительная отправка данных в журнал не чаще одного push в секунду и запрос попадает в hello пропускной способности.

Можно использовать окна Следующая формула toocompute hello значение toogive hello в секундах:

![Выражение 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Например:

* У вас есть 1000 устройств, отправляющих данные с интервалами в 1 секунду.
* Вы используете hello Power BI Pro номера SKU, поддерживающий 1 000 000 строк в час.
* Вы хотите toopublish hello объем среднего значения данных на устройстве tooPower бизнес-Аналитики.

В результате hello уравнение выглядит следующим образом:

![Выражение 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

При такой конфигурации можно изменить hello исходного запроса toohello следующее:

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>Обновление авторизации
Если hello пароль изменен с момента создания задания или последний раз проверку подлинности, то необходимо tooreauthenticate учетную запись Power BI. Если Azure многофакторная проверка подлинности настроена в клиенте Azure Active Directory (Azure AD), необходимо также авторизации Power BI toorenew каждые две недели. Если не будет обновлен, можно просмотреть проблемы, например об отсутствии выходные данные задания или `Authenticate user error` в журналах операций hello.

Аналогично Если задание запускается после истечения срока действия токена hello, возникает ошибка и hello задание завершается ошибкой. tooresolve эту проблему, остановить задание hello, на котором выполняется и перейти tooyour, выходные данные Power BI. потеря данных tooavoid, выберите hello **авторизацию** связь, а затем перезапустите задание из hello **время последней остановки**.

После обновления hello авторизации с помощью Power BI появится зеленый предупреждение в области tooreflect hello авторизации hello проблема была разрешена.

## <a name="get-help"></a>Получение справки
За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
