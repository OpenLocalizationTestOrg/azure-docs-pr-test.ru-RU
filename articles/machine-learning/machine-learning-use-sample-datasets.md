---
title: "образцы наборов данных hello aaaUse в студии машинного обучения | Документы Microsoft"
description: "Описания hello наборов данных, используемых в моделей-примеров, включенных в студии машинного обучения. Эти наборы данных можно использовать для собственных экспериментов."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Используйте образцы наборов данных hello в студии машинного обучения Azure
[top]: #machine-learning-sample-datasets

При создании рабочей области в службе машинного обучения Azure по умолчанию в нее добавляется ряд примеров экспериментов и наборов данных. Многие из этих примеров наборов данных используются в моделях hello образец hello [коллекции аналитики Azure Cortana](http://gallery.cortanaintelligence.com/). Остальные примеры включают примеры различных типов данных, обычно используемых в машинном обучении.

Некоторые из этих наборов данных доступны в хранилище BLOB-объектов Azure. Для этих наборов данных hello в следующей таблице обеспечивает прямую ссылку. Эти наборы данных можно использовать в эксперименты с помощью hello [импорта данных] [ import-data] модуля.

остальные Hello эти образцы наборов данных в вашей рабочей области доступны **сохраненные наборы данных** модуль hello палитры слева toohello холст эксперимента hello при открытии или создании нового эксперимента в студии машинного обучения.
Любой из этих наборов данных можно использовать в собственных эксперимент, перетащив его tooyour холст эксперимента.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>Имя набора данных</th>
  <th align=left>Описание набора данных</th>
</tr>

<tr>
  <td valign=top>набор данных Adult Census Income Binary Classification;</td>
  <td valign=top>
Подмножество hello 1994 переписи населения базы данных в рабочее взрослых возрастной группы hello 16 с индексом скорректированное доход > 100.<p> </p><b>Использование:</b> классифицировать людей, использующих демографические данные toopredict ли пользователь получает более чем 50 КБ в год.<p> </p><b>Связанные исследования:</b> Kohavi, R., Becker, B. (1996 г.). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>Набор данных кодов аэропортов</td>
  <td valign=top>
Коды аэропортов США.<p> </p>Этот набор данных содержит по одной строке для каждого аэропорта США, предоставляя hello аэропорта Идентификационный номер и имя вместе с hello местоположение города и штата.
  </td>
</tr>

<tr>
  <td valign=top>данные о ценах на автомобили (необработанные);</td>
  <td valign=top>
Сведения о автомобили, изготовитель и модель, включая цены hello функции, такие как количество hello цилиндров MPG, а также оценка рисков страхования.<p> </p>Оценка риска Hello изначально связана с ценой auto и настройки для фактического риска в рамках процесса под tooactuaries как symboling. Значение + 3 указывает автоматически hello рискованно, которое имеет значение -3 скорее всего, что он.<p> </p><b>Использование:</b> оценки риска hello Predict компонентами с помощью регрессии или многомерного классификации. <p> </p><b>Связанное исследование:</b> Schlimmer, J.C. (1987). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>Набор данных по прокату велосипедов UCI</td>
  <td valign=top>
Набор данных по прокату велосипедов UCI, основанный на реальных данных компании Capital Bikeshare, которая обслуживает сеть проката велосипедов в Вашингтоне, округ Колумбия.<p> </p>Hello набор данных содержит одну строку за каждый час каждый день в 2012 г. и 2011 для 17,379 строк. диапазон Hello каждый час внаем велосипедов — от 1 too977.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Изображение RGB Билла Гейтса</td>
  <td valign=top>
Данные tooCSV общедоступным изображения преобразованного файла.<p> </p>Hello для преобразования изображения hello в указан код hello <strong>цвет дискретизация с помощью кластеризации К-средних</strong> страницу сведений о модели.
  </td>
</tr>

<tr>
  <td valign=top>Данные о донорах крови</td>
  <td valign=top>
Подмножество данных из базы данных донорства крови hello объекта hello службы тю Center Hsin крови Transfusion города, Тайвань.<p> </p>Донорства включает hello месяцев с момента последнего пожертвование) и частоту или hello общее число пожертвования, время с момента последнего пожертвование и сумма пожертвования крови.<p> </p><b>Использование:</b> hello предназначена toopredict через классификации ли донорства hello пожертвования крови в марта 2007 г., где 1 означает донорства во время периода целевой hello и 0 не донорства-. <p> </p><b>Связанное исследование:</b> Yeh, I.C. (2008 г.). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  <p> </p>Yeh, I-Cheng, Yang, King-Jang и Ting, Tao-Ming, Knowledge discovery on RFM model using Bernoulli sequence, Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  .</td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Обзоры книг на Amazon</td>
  <td valign=top>
Обзоры книг в Amazon, взяты из веб-сайте amazon.com hello исследователями университет Пенсильвании (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">мнений</a>). См. в документе research hello, «биографии, Bollywood, аналог поля и Blenders: адаптации домена для классификация мнений» Джон Blitzer, Dredze метки и Фернандо Перейра; Связь вычислительных лингвистические (ACL), 2007.<p> </p>Hello исходный набор данных содержит обзоры 975K с рейтингами 1, 2, 3, 4 или 5. обзоры Hello были записаны на английском языке и сохраняются в hello период 1997-2007. Этот набор данных был уменьшается too10K проверки.
  </td>
</tr>

<tr>
  <td valign=top>Данные о раке молочной железы</td>
  <td valign=top>
Одно из трех связанных рак наборы данных, предоставляемые hello Oncology Institute, часто появляется в литературе обучения машины. Объединяет диагностическую информацию с функциями из лабораторных анализов приблизительно с 300 образцами ткани.<p> </p><b>Использование:</b> классификации типа hello рак, на основе 9 атрибутов, некоторые из которых являются линейными и некоторые являются категориальными. <p> </p><b>Связанное исследование:</b> Wohlberg, W.H., Street, W.N., & Mangasarian, O.L. (1995). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>Признаки рака молочной железы <td valign=top>
Hello набор данных содержит сведения для областей подозрительные 102K (кандидатов) пассажиров изображения, каждый описывается 117 компонентами. функции Hello являются закрытыми, и их значение не раскрываются создателями hello набора данных (Siemens здравоохранения). 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>Информация о раке молочной железы</td>
  <td valign=top>
Hello набор данных содержит дополнительные сведения для каждого региона подозрительные пассажиров изображения. Каждый пример содержит сведения (например, метки, patient ID координаты исправление относительный toohello всего изображения) о hello соответствующий номер строки в наборе данных функции рак груди hello. Каждый пациент имеет ряд примеров. Для пациентов, больных раком, часть примеров — положительные, а часть — отрицательные. Для пациентов, не больных раком, все примеры — отрицательные. Hello набор данных содержит примеры 102K. смещенной Hello набора данных, имеют положительное значение 0,6% точек hello, hello rest являются отрицательными. набор данных Hello стало доступно по Siemens здравоохранение.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>Общие метки стремления CRM</td>
  <td valign=top>
Метки для hello KDD Cup 2009 клиента связь прогнозирующего запроса (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>Общие метки оттока CRM</td>
  <td valign=top>
Метки для hello KDD Cup 2009 клиента связь прогнозирующего запроса (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>Общий набор данных CRM</td>
  <td valign=top>
Эти данные поступают из hello KDD Cup 2009 клиента связь прогнозирующего запроса (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>Hello набор данных содержит 50K клиентов из hello Telecom французский компании оранжевым цветом. У каждого клиента есть 230 обезличенных характеристик, из которых 190 — числовые, а 40 — категорийные. компоненты Hello, очень разреженным.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>Общие метки увеличения суммы покупок CRM</td>
  <td valign=top>
Метки для hello KDD Cup 2009 клиента связь прогнозирующего запроса (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>Данные о регрессии энергетического КПД</td>
  <td valign=top>
Набор смоделированных профилей энергии, основанных на 12 различных формах здания. Hello зданий отличаются друг от 8 возможностей, таких как glazing области hello glazing области распространения и ориентацию.<p> </p><b>Использование:</b> использовать регрессии или классификации toopredict hello-энергопотребление оценка на основе как один из двух real ценных ответов. Для многоклассовый классификатор является round hello ответа переменной toohello ближайшего целого. <p> </p><b>Связанное исследование:</b> Xifara, A. и Tsanas, A. (2012). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>Данные о задержках рейсов</td>
  <td valign=top>
Пассажира рейса на время данные о производительности из hello сбора данных TranStats hello США Министерство транспорта США (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">данные о соблюдении графиков</a>).<p> </p>набор данных Hello охватывает hello период октябрь апреля 2013 г. Перед отправкой tooAzure студии машинного обучения, hello набор данных был обработан следующим образом:<ul><li>набор данных Hello был отфильтрованные toocover только hello 70 максимальной загрузки аэропортов hello континентальной США</li><li>Отмененные рейсы были отмечены как задержанные более, чем на 15 минут.</li><li>Рейсы с отклонением были удалены.</li><li>Hello следующие столбцы были выбраны: год, месяц, день месяца, DayOfWeek, контроля несущей, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, отменено</li></ul>
</td>
</tr>

<tr>
  <td valign=top>Данные о соблюдении графиков рейсов (необработанные)</td>
  <td valign=top>
Записи о прибытии и отправлении авиарейсов в США, начиная с октября 2011 г.<p> </p><b>Использование:</b> прогнозирование задержки рейсов. <p> </p><b>Связанное исследование:</b> данные Министерства транспорта США <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>Данные о лесных пожарах</td>
  <td valign=top>
Содержит данные о погоде, такие как температура, влажность и скорость ветра, из северо-восточной Португалии, объединенные с записями о лесных пожарах.<p> </p><b>Использование:</b> это задача сложно регрессии, где hello aim toopredict hello записать области активируется леса. <p> </p><b>Связанное исследование:</b> Cortez, P. и Morais, A. (2008). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  <p> </p>[Cortez и Morais, 2007] P. Cortez и A. Morais. TooPredict подход интеллектуального анализа данных активируется леса с использованием Meteorological данных. In J. Neves, M. F. Сантос и J. Machado Eds., новые тенденции в искусственный интеллект, событий hello 13 EPIA 2007 - конференции португальский искусственного аналитика, за декабрь, Guimarães, Португалия стр. 512-523, 2007. APPIA, ISBN-13 978-989-95618-0-9. Доступно по адресу: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>Набор данных German Credit Card UCI</td>
  <td valign=top>
Здравствуйте, набора данных UCI Statlog (немецкой кредитной карты) (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + немецкий + + данные кредита</a>), с помощью файла german.data hello.<p> </p>набор данных Hello классифицирует людей, описываемого набор атрибутов, как высокое или низкое кредитных рисков. Каждый пример представляет собой физическое лицо. Существует 20 функций, как числовые, так и категориальных и двоичные метки (значение риска кредитной hello). Записи с высоким уровнем риска имеют метку со значением 2, записи с низким уровнем риска имеют метку со значением 1. ошибочную пример низким уровнем риска, как высокая стоимость Hello-1, тогда как ошибочную пример высокого риска как низкая стоимость hello равно 5.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>Названия фильмов на сайте IMDB</td>
  <td valign=top>
Hello набор данных содержит сведения о фильмах, которые были оценены в твиты Twitter: IMDB идентификатор фильма, названия фильма, Жанр и производственного года. Существует в наборе данных hello 17K фильмов. Hello набор данных был введен в документе hello «S. Dooms, T. De Pessemier and L. Martens. MovieTweetings: a Movie Rating Dataset Collected From Twitter. Workshop on Crowdsourcing and Human Computation for Recommender Systems, CrowdRec at RecSys 2013."
  </td>
</tr>

<tr>
  <td valign=top>Двухклассовые данные об ирисе</td>
  <td valign=top>
Это может быть hello в литературе распознавания шаблон hello самые известные toobe базы данных. Hello набора данных относительно невелико, содержащие 50 примеры лепесток измерений из трех видов iris.<p> </p><b>Использование:</b> прогнозирования типа iris hello из измерений hello.  <p> </p><b>Связанное исследование:</b> Fisher, R. A. (1988). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>Твиты о фильмах</td>
  <td valign=top>
набор данных Hello — расширенная версия набора данных Tweetings фильма hello. Hello набор данных содержит 170K оценки фильмов, извлеченных из хорошо структурированных твиты в Twitter. Каждый экземпляр представляет собой твит и является кортежем: идентификатор пользователя, идентификатор фильма IMDB, оценка, метка времени, число добавлений в избранное для твита и число ретвитов. набор данных Hello стало доступно, говорят, что A., S. Dooms, B. Loni и Tikk г. для 2014 запрос систем рекомендаций.
  </td>
</tr>

<tr>
  <td valign=top>Данные об MPG для различных автомобилей</td>
  <td valign=top>
Этот набор данных является незначительной модификацией hello набора данных, предоставляемые библиотекой StatLib hello объекта Карнеги-Меллона. Hello набор данных, используемый в hello 1983 American надстройках статистических взаимосвязей.<p> </p>Hello данных указано потребления топлива для различных автомобили в милях на галлон, вместе с информацией таких hello номер цилиндров, смещения ядра, мощность, общий вес и ускорения.<p> </p><b>Использование:</b> прогнозирование уровня экономии топлива на основе 3 многозначных дискретных атрибутов и 5 непрерывных атрибутов. <p> </p><b>Связанное исследование:</b> StatLib, Университет Карнеги — Меллон (1993 г.). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  </td>
</tr>

<tr>
  <td valign=top>Набор данных Pima Indians Diabetes Binary Classification</td>
  <td valign=top>
Подмножество данных из базы данных Национальным институтом для контроля уровня сахара и Digestive и Овально болезней hello. набор данных Hello был отфильтрованные toofocus на гнездо пациентов индийский наследия Pima. Hello данные включают медицинские данные, например глюкоза инсулин уровней, а также факторы жизненного цикла.<p> </p><b>Использование:</b> прогнозирования, имеет ли субъект hello контроля уровня сахара (двоичная классификация). <p> </p><b>Связанное исследование:</b> Sigillito, V. (1990). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  </td>
</tr>

<tr>
  <td valign=top>Данные о клиентах ресторанов</td>
  <td valign=top>
Набор метаданных о клиентах, включая демографические сведения и предпочтения.<p> </p><b>Использование:</b> используют этот набор данных, в сочетании с hello других двух ресторан наборов данных, tootrain и тестировать система рекомендаций. <p> </p><b>Связанное исследование:</b> Bache, K. и Lichman, M. (2013). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин: Калифорнийский университет, школа информационных и компьютерных наук.
  </td>
</tr>

<tr>
  <td valign=top>Данные об услугах ресторанов</td>
  <td valign=top>
Набор метаданных о ресторанах и их услугах, например о типе пищи, стиле ресторанов и местоположении.<p> </p><b>Использование:</b> используют этот набор данных, в сочетании с hello других двух ресторан наборов данных, tootrain и тестировать система рекомендаций. <p> </p><b>Связанное исследование:</b> Bache, K. и Lichman, M. (2013). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин: Калифорнийский университет, школа информационных и компьютерных наук.
  </td>
</tr>

<tr>
  <td valign=top>Оценки ресторанов</td>
  <td valign=top>
Содержит оценки, предоставленных toorestaurants пользователей по шкале от 0 too2.<p> </p><b>Использование:</b> используют этот набор данных, в сочетании с hello других двух ресторан наборов данных, tootrain и тестировать система рекомендаций. <p> </p><b>Связанное исследование:</b> Bache, K. и Lichman, M. (2013). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин: Калифорнийский университет, школа информационных и компьютерных наук.
  </td>
</tr>

<tr>
  <td valign=top>Многоклассовый набор данных об отжиге стали</td>
  <td valign=top>
Этот набор данных содержит набор записей с стали annealing пробные версии с hello физические атрибуты (ширину, толщину, тип (элемент, лист, т. д.) возникающие hello сталь типов.<p> </p><b>Использование:</b> прогнозирование любого из двух числовых атрибутов класса (твердость или сопротивление). Вы также можете анализировать корреляции между атрибутами.<p> </p>Марка стали соответствует заданному стандарту, определенному ассоциацией SAE и другими организациями. Вам нужны для конкретного «уровень» (переменная класса hello) и необходимые значения hello toounderstand. <p> </p><b>Связанное исследование:</b> Sterling, D. и Buntine, W. (нет данных). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин, Калифорния: Калифорнийский Университет, школа информационных и компьютерных наук  <p> </p>Оценки toosteel представлено руководство можно найти здесь: <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>Данные телескопов</td>
  <td valign=top>
Записи данных о пучках высокоэнергетичных гамма-частиц вместе с фоновым шумом, которые моделируются с помощью метода Монте-Карло.<p> </p>Hello моделирования hello предполагалось tooimprove hello точности на основе нуля атмосферные Cherenkov гамма полюса, с помощью статистических методов toodifferentiate между hello нужного сигнала (Cherenkov излучение душевых) и (hadronic фоновых шумов душевых инициировано космических лучей в верхнем атмосферы hello).<p> </p>Hello данные были предварительно обработанные toocreate elongated кластер с длинная ось hello ориентировано на достижение center hello камеры. Ниже приведены характеристики Hello данного эллипса (часто называемые Hillas параметров) среди параметров hello изображения, которые могут использоваться для сравнения.<p> </p><b>Использование:</b> прогнозирование того, представляет изображение ливня сигнал или фоновый шум.<p> </p><b>Примечания.</b> Уровень точности простой классификации не имеет значения для этих данных, так как классификация фонового события в качестве сигнала хуже, чем классификация события сигнала в качестве фона. Для сравнения различных классификаторов следует использовать график ROC hello. Здравствуйте, вероятность принимать события фоновой сигнала должен быть ниже одного из следующих пороговых значений hello: 0,01, 0,02, 0,05, 0,1 или 0,2.<p> </p>Кроме того, что является недооценили hello число фоновых событий (для hadronic душевых h), тогда как в реальные показатели hello h или шума класс представляет hello большинства событий. <p> </p><b>Связанное исследование:</b> Bock, R. K. (1995). Репозиторий машинного обучения UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Ирвин: Калифорнийский университет, школа информационных наук </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>Набор погодных данных</td>
  <td valign=top>
Почасовой основе Земли погоды наблюдения за NOAA (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">объединенных данных из 201304 too201310</a>).<p> </p>данные о погоде Hello охватывает наблюдений из станций погоды аэропорта, охватывающих период времени октябрь апреля 2013 hello. Перед отправкой tooAzure студии машинного обучения, hello набор данных был обработан следующим образом:<ul><li>Идентификаторы погоды станции были аэропорта сопоставленных toocorresponding идентификаторы</li><li>Были отфильтрованы погоды станции, не связанные с 70 максимальной загрузки аэропортах hello</li><li>столбец даты Hello была разделена на отдельные столбцы год, месяц и день</li><li>Hello следующие столбцы были выбраны: AirportID, год, месяц, день, время, часовой пояс, SkyCondition, видимость, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, WindSpeed, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, Altimeter</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Набор данных SP 500 из Википедии</td>
  <td valign=top>
Данные взяты из Википедии (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>) и основаны на статьях о каждой из компаний, включенной в фондовый индекс S&P 500. Они сохранены в формате XML.<p> </p>Перед отправкой tooAzure студии машинного обучения, hello набор данных был обработан следующим образом:<ul><li>Был извлечен текст по каждой конкретной компании</li><li>Удалено форматирование Википедии</li><li>Удалены символы, не являющиеся буквами или цифрами</li><li>Преобразовать все toolowercase текста</li><li>Были добавлены известные категории компаний</li></ul><p> </p>Обратите внимание, что для некоторых компаний статьи не найден, поэтому hello число записей будет меньше 500.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
Hello набор данных содержит данные клиента и указания об их ответа tooa прямой кампании прямой почтовой рассылки. В каждой строке представлен один клиент. Hello набор данных содержит 9 функции о демографические данные пользователя, а также за поведение и три столбца метки (посещать, преобразование и потратить).  Посетите является двоичного столбца, который указывает, что пользователь посетил после hello маркетинговой кампании, преобразование указывает, что клиент приобрел нечто и потратить является сумма hello, которое было затрачено.  Hello dataset стало доступно, Kevin Hillstrom для MineThatData электронной почты аналитика и данным интеллектуального анализа данных запроса.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
Функции примеры тестов в наборе данных новостей RCV1 V2 Reuters hello. Hello набор данных содержит новости 781K вместе с их идентификаторами (первый столбец набора данных hello). Для каждой статьи выполнен анализ по лексемам, стоп-словам и однокоренным словам. набор данных Hello стало доступно, Дэвид. D. Lewis).
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Компоненты обучающих примеров в наборе данных новостей RCV1 V2 Reuters hello. Hello набор данных содержит статьи вместе с их идентификаторами 23K (первый столбец набора данных hello). Для каждой статьи выполнен анализ по лексемам, стоп-словам и однокоренным словам. набор данных Hello стало доступно, Дэвид. D. Lewis).
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
Набор данных на основе hello KDD Cup 1999 обнаружения набора знаний и конкуренции при средства интеллектуального анализа данных (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>набор данных Hello загружена и хранятся в хранилище больших двоичных объектов Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) и включает в себя обучающий и проверочный набор данных. Hello обучающий набор данных — приблизительно 126 тысяч строк и столбцов 43, включая метки hello. Три столбца входят сведения о метке hello и 40 столбцов, состоящий из числового типа и строки или категориальные функции, доступные для обучения модели hello. данные теста Hello имеет приблизительно 22,5 K проверить примеры со столбцами hello же 43 как hello обучающих данных.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></td>
  <td valign=top>
Раздел назначения для статьи в наборе данных новостей RCV1 V2 Reuters hello. Tooseveral разделы могут назначаться новостной статье. Формат Hello каждой строки «&lt;имя раздела&gt; &lt;идентификатор документа&gt; 1». Hello набор данных содержит раздел назначения 2,6 МБ. набор данных Hello стало доступно, Дэвид. D. Lewis).
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
Эти данные поступают из hello запрос оценки производительности студента 2010 Cup KDD (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">оценку производительности студента</a>). Hello данные берутся hello Algebra_2008_2009 обучающий набор (Niculescu об отметке, J.,-Mizil, S. A. Ritter, Gordon, G.J. & Koedinger K.R. (2010). Алгебра 2008-2009. Опробуйте набор данных из состязания KDD Cup 2010: интеллектуальный анализ образовательных данных. Он находится в файле <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> или <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>.<p> </p>набор данных Hello загружена и хранятся в хранилище больших двоичных объектов Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) и содержит файлы журнала из студент частные уроки системы. предоставленный Hello функции включают проблемный идентификатор и краткое описание, идентификатор студента, timestamp, и сколько попыток до решения проблемы hello в hello студента hello способ. Hello исходный набор данных содержит записи 8,9 M; Этот набор данных был toohello уменьшается первые 100 тысяч строк. Hello набор данных содержит 23 табуляцией столбцы различных типов: числовые, категориальных и отметку времени.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
