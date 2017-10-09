---
title: "aaaPower мониторинга бизнес-Аналитики за vehicle работоспособности и управление им привычки - Azure | Документы Microsoft"
description: "Использовать возможности hello toogain Cortana аналитики в реальном времени и прогнозной аналитики на автомобиль работоспособности и пешком привычки."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>Инструкции по настройке информационной панели Power BI шаблона решения для аналитики телеметрии автомобилей
Это **меню** toohello главах этого репертуара ссылки. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

решения для анализа телеметрии Vehicle Hello демонстрирует, как дилеров автомобиля, автомобиль производители и страховых компаний могут использовать возможности hello средств аналитики Cortana toogain в режиме реального времени и прогнозирующего анализа работоспособности транспортного средства и управление им Усовершенствования toodrive привычки hello области клиента возникают, R & D и маркетинговых кампаний. Этот документ содержит инструкции по настройке hello Power BI отчеты и панели мониторинга после развертывания решения hello в вашей подписке. 

## <a name="prerequisites"></a>Предварительные требования
1. Развертывание hello [Analytics телеметрии](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) решения  
2. [Установите Microsoft Power BI Desktop.](http://www.microsoft.com/download/details.aspx?id=45331)
3. [Подписка Azure](https://azure.microsoft.com/pricing/free-trial/). Если у вас нет подписки Azure, для начала получите бесплатную подписку Azure.
4. Учетная запись Microsoft Power BI

## <a name="cortana-intelligence-suite-components"></a>Компоненты Cortana Intelligence Suite
Как часть шаблона решения транспортных средств телеметрии Analytics hello следующие службы аналитики Cortana hello развертываются в вашей подписке.

* **Концентратор событий** принимает миллионы событий телеметрии автомобилей в Azure.
* **Stream Analytics** получает данные аналитики о работоспособности автомобиля в режиме реального времени и сохраняет их в долговременное хранилище для более детальной пакетной аналитики.
* **Машинное Обучение** для обнаружения аномалий в режиме реального времени и пакетной обработки toogain прогнозной аналитики.
* **HDInsight** tootransform использовать данные в масштабе
* **Фабрика данных** обрабатывает orchestration, планирование, управление ресурсами и мониторинг hello конвейера обработки пакета.

**Power BI** предоставляет для этого решения расширенную панель мониторинга для визуализации данных в режиме реального времени и прогнозной аналитики. 

Hello решение использует два различных источников данных: **имитируемые vehicle сигналы и набор диагностических данных** и **vehicle каталога**.

В это решение входит симулятор телематики автомобиля. Он выдает диагностических сведений и сообщает состояние соответствующего toohello hello vehicle и определяющим шаблон в определенный момент времени. 

Hello Vehicle каталог представляет собой справочник по набора данных содержащего VIN toomodel сопоставление

## <a name="power-bi-dashboard-preparation"></a>Подготовка информационной панели Power BI
### <a name="setup-power-bi-real-time-dashboard"></a>Настройка панели мониторинга Power BI в реальном времени

**Запустите приложение в режиме реального времени мониторинга hello** после завершения развертывания hello, необходимо выполнить инструкции по эксплуатации hello вручную

* Скачайте файл RealtimeDashboardApp.zip с приложением панели мониторинга в режиме реального времени и распакуйте его.
*  В распакованную папку hello откройте файл конфигурации приложения «RealtimeDashboardApp.exe.config» replace appSettings для соединений службы Eventhub хранилища больших двоичных объектов и ML со значениями hello в hello инструкции операции вручную и сохраните изменения.
* Запустите приложение RealtimeDashboardApp.exe. Окно входа будет всплывающее окно, допустимым PowerBI учетные данные и нажмите кнопку hello **Accept** кнопки. Затем приложение hello начнется toorun.

   ![Вход tooPower бизнес-Аналитики](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Разрешения для информационной панели Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* Веб-сайт tooPowerBI входа в систему и создать панель мониторинга в режиме реального времени.

Теперь вы являетесь панели мониторинга Power BI готов tooconfigure hello с широкими возможностями визуализации toogain в режиме реального времени и привычки прогнозной аналитики на автомобиль работоспособности и управление им. Занимает около 45 минут tooan час toocreate hello все отчеты и настройка панели hello. 

### <a name="configure-power-bi-reports"></a>Настройка отчетов Power BI
Hello в режиме реального времени отчеты и панели мониторинга hello занимает приблизительно toocomplete 30 – 45 минут. Обзор слишком[http://powerbi.com](http://powerbi.com) и имя входа.

![Вход tooPower бизнес-Аналитики](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

В Power BI создается новый набор данных. Нажмите кнопку hello **ConnectedCarsRealtime** набора данных.

![Выберите набор данных подключенных автомобилей в реальном времени](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Сохранить с помощью пустого отчета hello **Ctrl + s**.

![Сохраните пустой отчет.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

Введите для отчета имя *Аналитика телеметрии автомобилей в реальном времени: отчеты*.

![Присвойте имя отчету.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>Отчеты в реальном времени
Это решение включает три отчета в реальном времени, описывающие:

1. исправные автомобили;
2. автомобили, которым требуется обслуживание;
3. Статистика работоспособности автомобилей

Можно выбрать tooconfigure всех отчетов в режиме реального времени hello для трех или остановить после любой стадии и вы toohello Настройка отчетов пакета hello следующего раздела. Мы рекомендуем toocreate всех трех hello сообщает toovisualize hello полный аналитики hello в режиме реального времени пути решения hello.  

### <a name="1-vehicles-in-operation"></a>1. исправные автомобили;
Дважды щелкните **страница 1** и переименуйте его слишком «Транспортных средств в операции»  
    ![Подключенные автомобили — исправные автомобили](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

В разделе **Поля** выберите поле **VIN** и укажите тип визуализации **Карточка**.  

Создается карточка визуализации, как показано на рисунке.  
    ![Подключенные автомобили — выберите номер шасси](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

Щелкните новую визуализацию hello пустую область tooadd.  

Выберите поля **Город** и **VIN**. Измените визуализацию слишком**«Карта»**. Перетащите поле **VIN** в область значений. Перетащите **Город** из полей слишком**условных обозначений** области.   
    ![Подключенные автомобили — визуализация "Карточка"](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

Выберите **формат** статьи **визуализации**, нажмите кнопку **заголовок** и измените hello **текст** слишком**автомобилей» в Операция по городу»**.  
    ![Подключенные автомобили — исправные автомобили по городам](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

Визуализация будет выглядеть, как показано на рисунке.    
    ![Подключенные автомобили — итоговая визуализация](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

Щелкните новую визуализацию hello пустую область tooadd.  

Выберите **Город** и **vin**, измените тип визуализации слишком**гистограмму с группировкой**. Убедитесь, что поле **Город** размещено в области **Ось**, а **VIN** — в области **Значение**.  

Отсортируйте гистограмму по параметру **Count of vin** (Количество VIN).  
    ![Подключенные автомобили — количество номеров шасси](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

Изменение диаграммы **заголовок** слишком**«Транспортных средств в операции по городам»**  

Нажмите кнопку hello **формат** статьи, а затем выберите **цвета данных**, щелкните hello **«На»** слишком**Показать все**  
    ![Подключенные автомобили — отображение всех цветов данных](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

Измените цвет hello отдельные города, щелкнув значок цвета.  
    ![Подключенные автомобили — изменение цветов](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

Щелкните новую визуализацию hello пустую область tooadd.  

Выберите тип визуализации **Гистограмма с группировкой**, перетащите поле **Город** в область **Ось**, поле **Модель** — в область **Условные обозначения**, а поле **VIN** — в область **Значение**.  
    ![Подключенные автомобили — кластеризованная гистограмма](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Подключенные автомобили — отрисовка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

Измените визуальное представление на странице, как показано на рисунке.  
    ![Подключенные автомобили — визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

В режиме реального времени отчета «Транспортных средств в операции» hello успешно настроена. Можно продолжить toocreate hello в режиме реального времени отчет или пропустить и настройки мониторинга hello. 

### <a name="2-vehicles-requiring-maintenance"></a>2. автомобили, которым требуется обслуживание;
Нажмите кнопку ![добавить](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd нового отчета, переименуйте его слишком**«Автомобилей требует Maintenance»**

![Подключенные автомобили — автомобили, требующие обслуживания](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

Выберите **vin** и измените тип визуализации слишком**карты**.  
    ![Подключенные автомобили — визуализация "Карточка номера шасси"](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

У нас есть поле с именем «MaintenanceLabel» в наборе данных hello. Это поле может иметь значение 0 или 1. Он задается модели машинного обучения Azure hello подготовить как часть решения и интегрированные в путь в реальном времени hello. Hello значение «1» указывает, что транспортного средства требуется его обслуживание. 

tooadd **уровне страниц** фильтр для отображения данных автомобилей, который, которым обслуживания: 

1. Перетащите hello **«MaintenanceLabel»** в **фильтры уровня страницы**.  
   ![Подключенные автомобили — фильтры уровня страницы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. В нижней части фильтра уровня страницы MaintenanceLabel щелкните меню **Простая фильтрация** .  
   ![Подключенные автомобили — базовая фильтрация](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. Присвойте ему значение фильтра слишком**«1»**    
   ![Подключенные автомобили — значение фильтра](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

Щелкните новую визуализацию hello пустую область tooadd.  

Выберите тип визуализации **Гистограмма с группировкой**.  
![Подключенные автомобили — визуализация «Карточка номера шасси»](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Подключенные автомобили — кластеризованная гистограмма](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

Перетащите поле **модель** в **оси** область, **Vin** слишком**значение** области. Отсортируйте визуализацию по параметру **Количество VIN**.  Изменение диаграммы **заголовок** слишком**«Транспортных средств требуется обслуживание модели»**  

Перетащите поля **VIN** в область **Насыщенность цвета** (раздел **Поля** ![Поля](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) на вкладке **Визуализация**).  
![Подключенные автомобили — насыщенность цвета](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

Измените тип визуализации параметра **Цвета данных** из раздела **Формат**.  
Измените минимальное значение цвета на **F2C812**.  
Измените максимальное значение цвета на **FF6300**.  
![Подключенные автомобили — изменения цвета](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Подключенные автомобили — новые цвета визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

Щелкните новую визуализацию hello пустую область tooadd.  

Выберите тип визуализации **Гистограмма с группировкой**. Затем перетащите поле **VIN** в область **Значение**, а поле **Город** — в область **Ось**. Отсортируйте гистограмму по параметру **Count of vin** (Количество VIN). Изменение диаграммы **заголовок** слишком**«Автомобилей, требующие обслуживания по городам»**   
![Подключенные автомобили — автомобили, требующие обслуживания, по городам](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

Щелкните новую визуализацию hello пустую область tooadd.  

Выберите **многострочных карточек** визуализации из визуализаций, перетащите **модель** и **vin** в hello **поля** области.  
![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Реорганизовать все визуализации hello, hello окончательный отчет выглядит следующим образом:  
![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

Отчет в режиме реального времени «Автомобилей требует обслуживания» hello успешно настроена. Можно продолжить toocreate hello в режиме реального времени отчет или пропустить и настройки мониторинга hello. 

### <a name="3-vehicles-health-statistics"></a>3. Статистика работоспособности автомобилей
Нажмите кнопку ![добавить](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd нового отчета, переименуйте его слишком**«Статистика транспортных средств работоспособности»**  

Выберите **датчика** визуализации из визуализаций, затем перетащите hello **скорость** в **значение, минимальное, максимальное значение** областей.  
![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

Изменение статистической обработки по умолчанию hello **скорость** в **значение области** слишком**среднее** 

Изменение статистической обработки по умолчанию hello **скорость** в **область минимум** слишком**минимум**

Изменение статистической обработки по умолчанию hello **скорость** в **область максимально** слишком**максимальное**

![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Переименование hello **заголовок датчика** слишком**«Средняя скорость»** 

![Подключенные автомобили — датчик](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

Щелкните новую визуализацию hello пустую область tooadd.  

Аналогичным образом добавьте следующие **датчики**: **Среднее количество моторного масла**, **Среднее количество топлива** и **Средняя температура двигателя**.  

Изменение статистической обработки по умолчанию hello полей в каждой шкалы с указанными выше действия, описанные в **«Средняя скорость»** датчика.

![Подключенные автомобили — датчики](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

Щелкните новую визуализацию hello пустую область tooadd.

Выберите **строки и гистограмму с группировкой** из визуализаций, затем перетащите **Город** в **общей оси**, перетащите **скорость**, **поля tirepressure и engineoil** в **значения столбца** область, изменить их тип статистической обработки слишком**среднее**. 

Перетащите hello **engineTemperature** в **значения строки** область, измените тип статистической обработки hello слишком**среднее**. 

![Подключенные автомобили — поля визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

Изменение диаграммы hello **заголовок** слишком**«Среднее значение скорости, нагрузка велосипеда, engine нефти и температуры подсистемы»**.  

![Подключенные автомобили — поля визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

Щелкните новую визуализацию hello пустую область tooadd.

Выберите **древовидной диаграммы** визуализации из визуализаций, перетащите hello **модель** в hello **группы** области и перетащите поле hello  **MaintenanceProbability** в hello **значения** области.

Изменение диаграммы hello **заголовок** слишком**«Vehicle моделей, требующие обслуживания»**.

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

Щелкните новую визуализацию hello пустую область tooadd.

Выберите **Нормированная линейчатая диаграмма** из визуализации, перетащите hello **Город** в hello **оси** области и перетащите hello **MaintenanceProbability**, **RecallProbability** полей с получением hello **значение** области.

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

Нажмите кнопку **формат**выберите **цвета данных**и набор hello **MaintenanceProbability** цвета значение toohello **«F2C80F»**.

Изменение hello **заголовок** из hello диаграммы слишком**«Вероятность из транспортного средства обслуживания & отозвать по городам»**.

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

Щелкните новую визуализацию hello пустую область tooadd.

Выберите **диаграмма с областями** визуализации из визуализаций, перетащите hello **модель** в hello **оси** области и перетащите hello **engineOil, tirepressure, скорость и MaintenanceProbability** полей с получением hello **значения** области. Изменить их тип статистической обработки слишком**«Среднее»**. 

![Подключенные автомобили — изменение типа агрегирования](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Измените заголовок hello hello диаграммы слишком**«Среднее нефти ядра, tire вероятность давления, скорости и обслуживание модели»**.

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Щелкните новую визуализацию hello пустую область tooadd:

1. Выберите тип визуализации **Точечная диаграмма** .
2. Перетащите hello **модель** в hello **сведения** и **условных обозначений** области.
3. Перетащите hello **топливо** в hello **оси x** область, измените агрегирования данных hello слишком**среднее**.
4. Перетащите **engineTemparature** в **оси y области**, измените агрегирования данных hello слишком**среднее**
5. Перетащите hello **vin** в hello **размер** области.

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

Изменение диаграммы hello **заголовок** слишком**«Средних топливо, температуры ядра моделью»**.

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

Hello окончательный отчет будет выглядеть, как показано ниже.

![Подключенные автомобили — итоговый отчет](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>Визуализации ПИН-код из панели мониторинга в реальном времени toohello hello отчеты
Создайте пустую панель, щелкнув значок "плюс" hello tooDashboards Далее. Панели можно присвоить имя «Панель мониторинга аналитики телеметрии автомобилей».

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

Закрепление hello визуализацию на hello выше мониторинга toohello отчеты. 

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

панель мониторинга Hello должен выглядеть следующим образом все hello три отчеты создаются и hello соответствующий визуализации, закрепленные toohello панели мониторинга. Если вы не создали все отчеты hello, панели мониторинга может выглядеть иначе. 

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

Поздравляем! Панель мониторинга в реальном времени hello успешно создана. Как вы по-прежнему tooexecute CarEventGenerator.exe и RealtimeDashboardApp.exe, вы увидите динамические обновления на панели мониторинга hello. Может потребоваться hello toocomplete too15 около 10 минут, следующие шаги.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Настройка панели мониторинга пакетной обработки Power BI
> [!NOTE]
> Он занимает примерно в два часа (из hello успешного завершения развертывания hello) для hello окончания tooend пакетной обработки toofinish выполнение конвейера и обрабатывает созданный данные за год. Поэтому дождитесь hello обработки toofinish перед продолжением hello дальнейшие действия. 
> 
> 

**Загрузите файл конструктора Power BI hello**

* Предварительно настроенный файл конструктора Power BI входит в состав развертывания hello инструкции операции вручную
* Найдите пункт 2. Установки PowerBI пакетной обработки мониторинга можно скачать шаблон PowerBI hello Пакетная обработка панели мониторинга расположена **ConnectedCarsPbiReport.pbix**.
* Сохраните файл на локальном компьютере.

**Настройка отчетов Power BI**

* Привет открыть файл конструктора "**ConnectedCarsPbiReport.pbix**" с помощью Power BI Desktop. Если вы уже не устанавливать hello Power BI Desktop из [установки Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331). 
* Нажмите кнопку hello **изменить запросы**.

![Изменение запроса Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Дважды щелкните hello **источника**.

![Настройка источника Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Обновите строки соединения сервера с сервером Azure SQL hello, полученный подготовлены в ходе развертывания hello.  Искать в hello вручную операции инструкции в разделе 

    4. База данных SQL Azure
    
    * Сервер: somethingsrv.database.windows.net
    * База данных: connectedcar
    * Имя пользователя: username
    * Пароль: паролем к серверу SQL можно управлять на портале Azure

* Для параметра **База данных** оставьте значение *connectedcar*.

![Настройка базы данных Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* Нажмите кнопку **ОК**.
* Вы увидите **учетные данные Windows** вкладка по умолчанию, измените его слишком**учетные данные базы данных** , щелкнув **базы данных** вкладки справа.
* Укажите hello **Username** и **пароль** , указанное во время его установки для развертывания базы данных SQL Azure.

![Указание учетных данных базы данных](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* Добавьте новый отчет, щелкнув **Подключить**
* Повторите hello выше действия для каждого hello три остальных запросов отсутствует на правой панели, а затем обновите сведения о подключении источника данных hello.
* Щелкните **Close and Load**(Закрыть и загрузить). Наборов данных Power BI Desktop файл — это таблицы подключенной tooSQL базы данных Azure.
* **Закройте** файл Power BI Desktop.

![Закрытие Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* Нажмите кнопку **Сохранить** кнопку toosave hello изменения. 

Теперь вы настроили все отчеты hello соответствующий toohello пути обработки пакета в решении hello. 

## <a name="upload-toopowerbicom"></a>Отправка слишком*powerbi.com*
1. Перейдите toohello Power BI веб-портала на http://powerbi.com и входа.
2. Щелкните **Получить данные**  
3. Отправьте файл Power BI Desktop hello.  
4. tooupload, нажмите кнопку **получение данных "->" файлы, получение локальный файл "->"**  
5. Перейдите toohello **»**ConnectedCarsPbiReport.pbix**»**  
6. После загрузки файла hello можно навигацию задней tooyour Power BI в рабочей области.  

Набор данных, отчет и пустая панель мониторинга будут созданы автоматически.  

Новая панель мониторинга tooa вызывается диаграммы ПИН-код **транспортного средства мониторинга аналитических данных телеметрии** в **Power BI**. Щелкните пустую панель hello, созданная выше, а затем перейдите toohello **отчеты** щелкните hello вновь отправлен отчет.  

![Телеметрия автомобилей Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**Примечание hello отчет содержит шесть страниц:**  
Страница 1. Плотность автомобиля.  
Страница 2. Работоспособность автомобилей в реальном времени.  
Страница 3. Агрессивно управляемые автомобили.   
Страница 4. Отозванные автомобили.  
Страница 5. Автомобили с экономным расходом топлива.  
Страница 6. Логотип компании Contoso.  

![Подключенные автомобили Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**На странице 3**, закрепить hello следующее:  

1. Количество VIN  
   ![Подключенные автомобили Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. Агрессивно управляемые автомобили по моделям — каскадная диаграмма.  
   ![Телеметрия автомобиля — закрепление диаграмм 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**От 5 страницы**, закрепить hello следующее: 

1. Количество VIN    
   ![Телеметрия автомобиля — закрепление диаграмм 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. Автомобили с экономным расходом топлива по моделям: гистограмма с группировкой.  
   ![Телеметрия автомобиля — закрепление диаграмм 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**Страница 4**, закрепить hello следующее:  

1. Количество VIN  
   ![Телеметрия автомобиля — закрепление диаграмм 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. Отозванные автомобили по городам, моделям: диаграмма "дерево".  
   ![Телеметрия автомобиля — закрепление диаграмм 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**От 6 страницы**, закрепить hello следующее:  

1. Логотип компании Contoso Motors.  
   ![Телеметрия автомобиля — закрепление диаграмм 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Упорядочение мониторинга hello**  

1. Перейдите на панель мониторинга toohello
2. Наведите указатель мыши на каждой диаграммы и переименуйте его основании именования hello в приведенном ниже рисунке hello панелей мониторинга. Также можно переместите hello диаграммы вокруг toolook как мониторинга "hello" ниже.  
   ![Телеметрия автомобиля — упорядочение панели мониторинга 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Телеметрия автомобилей Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. При создании все отчеты hello, описанным в этом документе hello последней завершенной мониторинга должна выглядеть как hello следующий рисунок. 

![Телеметрия автомобиля — упорядочение панели мониторинга 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

Поздравляем! Успешно создана отчеты hello и hello toogain панели мониторинга в режиме реального времени, прогнозирования и привычки пакета важные сведения о работоспособности транспортного средства и управление им.  
