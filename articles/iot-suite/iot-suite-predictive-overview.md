---
title: "обслуживание aaaPredictive предварительно настроенное решение | Документы Microsoft"
description: "Описание hello Azure IoT Suite превентивного обслуживания предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>Обзор предварительно настроенного решения прогнозируемого обслуживания

Hello *превентивного обслуживания* [предварительно настроенное решение] [ lnk_preconfigured_solutions] является одним из hello [Microsoft Azure IoT Suite] [ lnk_iot_suite] предварительно настроенных решений. Это решение интегрирует сбор данных телеметрии устройства в режиме реального времени и прогнозируемую модель, созданную с помощью [машинного обучения Azure][lnk-machine-learning].

С Azure IoT Suite можно быстро и легко подключиться tooand монитор ресурсов и анализ телеметрии в режиме реального времени в панелях мониторинга и визуализации. В решении превентивного обслуживания hello hello информационные панели и визуализации предоставляют новой аналитики, которые можно диска эффективность и улучшить дохода.

## <a name="hello-scenario"></a>Hello сценария

Компания Fabrikam является региональной авиалинией, которая концентрируется на хорошем впечатлении клиентов по приемлемым ценам. Одной из причин задержки рейсов являются проблемы обслуживания, в частности, особенно сложной задачей является обслуживание двигателей самолетов. Fabrikam необходимо избежать сбоя Ядро во время рейса любой ценой, поэтому регулярно проверяет ядра и планирует в соответствии с tooa плана обслуживания. Тем не менее самолет, модули не всегда носить hello таким же. В некоторых случаях выполняется ненужное обслуживание двигателей. Что более важно, возникают проблемы, которые могут задержать самолет на земле до проведения обслуживания. Если самолете находится в расположении где hello правой специалистов или запасные части недоступны, эти проблемы может быть особенно много ресурсов.

Hello механизмах самолет Fabrikam инструментирования с датчиками, отслеживающих ядре СУБД во время рейса. Fabrikam использует датчик hello превентивного обслуживания решение toocollect hello данные, собранные во время полета hello. После накопления лет подсистемы оперативной и данные ошибки специалисты по анализу данных компании Fabrikam моделировать hello toopredict способом оставшийся срок службы (RUL) для механизма самолет. Hello модель использует корреляцию между данными из четырех датчиков engine hello и одежды ядра, который ведет tooeventual сбоя. Прерывая Fabrikam tooperform регулярных проверок tooensure безопасности его теперь можно использовать hello моделей toocompute hello RUL для каждого ядра после каждого рейса. Hello модель использует hello телеметрии, собранных на основе механизмов hello в течение рейса hello. Fabrikam теперь может прогнозировать будущие точки сбоя и планировать обслуживание и ремонт заранее.

> [!NOTE]
> модель решения Hello использует данные износ фактические ядра.

Прогнозирование hello точки, при необходимости обслуживания, Fabrikam оптимизировать его стоимости tooreduce операций.

Координаторы технического обслуживания работают с планировщиками:

- План обслуживания toocoincide с самолете остановки в определенном месте.
- Убедитесь, что достаточно времени для hello самолет toobe обслуживания без вызвал перерыв в работе расписания.
- tooensure специалистов tooschedule эффективно обслуживать самолет без времени ожидания.

Менеджеры снабжения получают планы обслуживания, чтобы оптимизировать процесс размещения заказов и хранение запасных частей.

Эти действия включить Fabrikam toominimize самолет фактическое время и сократить эксплуатационные расходы, одновременно обеспечивая безопасность hello пассажиров и сотрудники.

toounderstand как [Azure IoT Suite] [ lnk_iot_suite] предоставляет hello возможности клиенты должны toorealize hello потенциал превентивного обслуживания просмотрите это [инфографикой] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>Построение решения превентивного обслуживания hello

Hello решение использует существующую модель машинного обучения Azure как tooshow шаблона эти возможности работать из устройства телеметрии, полученные через IoT Suite служб. Корпорация Майкрософт создала [модель регрессии] [ lnk_regression_model] подсистемы самолет, на основе данных общедоступные<sup>\[1\]</sup>и пошаговые руководство по как toouse hello модели.

Hello превентивного обслуживания решения Azure IoT используется модель регрессии hello, созданные по этому шаблону. развертывается в вашей подписке Azure и через API-Интерфейс автоматически созданный Hello модели. Hello решение включает в себя набор проверочных данных, представляющий 4 (всего 100) hello ядер и потоков данных датчика hello 4 (от 21 общее). Эти данные имеют достаточные tooprovide точный результат из обученной модели hello.

*\[1\] А. Саксена (A. Saxena) и К. Гебель (K. Goebel) (2008 г.). "Набор данных для симуляции деградации турбореактивного двигателя" (Turbofan Engine Degradation Simulation Data Set), Хранилище данных Центра прогнозирования Эймса (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/, Исследовательский центр Эймса, Моффетт-филд, Калифорния*

## <a name="get-started-with-predictive-maintenance"></a>Приступая к работе с прогнозируемым обслуживанием

Этом учебнике показано, как tooprovision hello решения превентивного обслуживания. Он также поможет выполнить основные функции hello hello превентивного обслуживания решения. Многие из этих средств можно обращаться решения hello панель мониторинга, которая развертывает вместе с hello предварительно настроенных решений.

toocomplete этого учебника требуется Активная подписка Azure.

> [!NOTE]
> Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].

1. Войдите на слишком[azureiotsuite.com] [ lnk-azureiotsuite] Azure с помощью учетных данных учетной записи и нажмите кнопку  **+**  toocreate решения.
1. Нажмите кнопку **выберите** hello **превентивного обслуживания** плитки.
1. Укажите **имя** для предварительно настроенного решения прогнозируемого обслуживания.
1. Выберите hello **область** и **подписки** toouse tooprovision hello решение.
1. Нажмите кнопку **создать решение** toobegin hello процесса подготовки. Этот процесс обычно занимает несколько минут toorun.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>Дождитесь подготовки процесса toocomplete hello

1. Щелкните плитку hello в решении с **Provisioning** состояния.
1. Обратите внимание hello **подготовки состояний** мере развертывания служб Azure в подписке Azure.
1. После завершения подготовки hello изменения состояния слишком**готовности**.
1. Нажмите кнопку сведения hello toosee плитки hello решения в правой области окна hello. В этой области можно запустить hello решения панели мониторинга и доступа hello рабочей области машинного обучения.

> [!NOTE]
> Если возникли проблемы при развертывании hello предварительно настроенных решений, просмотрите [разрешения на сайт azureiotsuite.com hello] [ lnk-permissions] и hello [часто задаваемые вопросы о] [ lnk-faq]. Если сохранить проблемы hello, создать билет службы для hello [портала][lnk-portal].

Существуют следовало ожидать toosee сведения, которые отсутствуют в списке для вашего решения? Сообщите нам о своих предложениях на сайте [User Voice](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="view-hello-solution"></a>Представление решения hello

Этот раздел поможет выполнить решение hello пользовательского интерфейса.

### <a name="predictive-maintenance-dashboard"></a>Панель мониторинга диагностического обслуживания

Эта страница в веб-приложение hello использует элементы управления PowerBI JavaScript (hello в разделе [репозитория визуальных элементов PowerBI][lnk-powerbi]) toovisualize:

* Hello выходных данных из задания Stream Analytics hello в хранилище больших двоичных объектов.
* Hello RUL и цикл количество на самолет ядра.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>Контролирует поведение hello hello облачные решения

В hello портал Azure, перейдите toohello группы ресурсов с именем решения hello выбрано tooview подготовленные ресурсы.

![][img-resource-group]

При подготовке hello предварительно настроенных решений появится сообщение электронной почты с рабочей области машинного обучения toohello ссылку. Вы также можете переходить рабочей области машинного обучения toohello из hello [azureiotsuite.com] [ lnk-azureiotsuite] страницы для предоставленного решения. Плитки доступно на этой странице, когда решение hello в hello **готовности** состояния.

![][img-machine-learning]

Hello решение портала можно видно, что этот образец hello, предоставляется два самолет toorepresent четырех устройств, имитация двух ядер на самолет, каждый из которых четыре датчиков. При переходе сначала toohello решение портала моделирование hello остановлена.

![][img-simulation-stopped]

Нажмите кнопку **запустить моделирование** toobegin hello моделирования. Здравствуйте журнал датчика, RUL, циклы и RUL hello мониторинга заполнения журнала.

![][img-simulation-running]

Когда RUL меньше, чем 160 (произвольный пороговое значение для демонстрационных целей), hello решения портал отобразит предупреждение символ Далее toohello, RUL отображения. портал Hello решения также выделяется engine самолет hello желтым цветом. Обратите внимание на то, как значения RUL hello имеют общие вниз общая тенденция, но, как правило, toobounce вверх и вниз. Это поведение возникает в результате hello переменной цикла длины и точности модели hello.

![][img-simulation-warning]

Полное моделирование Hello занимает около 35 минут toocomplete 148 циклов. Оба ядер попадания hello пороговое значение на около 8 минут и Hello 160 RUL порога для hello первый раз около 5 минут.

Моделирование Hello завершит hello всего набора данных для 148 циклов и сопоставляет окончательного значения RUL и цикла.

Вы можете остановить hello моделирование на любом этапе точка, но щелкнув **запустить моделирование** воспроизведения hello моделирование с начала hello hello набора данных.

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о как Azure IoT позволяет использовать сценарии превентивного обслуживания, чтение [записать значение из Интернета вещей hello][lnk_capture_value].

Принимать [Пошаговое руководство] [ lnk-predictive-walkthrough] решения hello превентивного обслуживания.

Можно также изучить некоторые hello и другие возможности hello IoT Suite предварительно настроенных решений:

* [Часто задаваемые вопросы об IoT Suite][lnk-faq]
* [Основание безопасности IoT из hello,][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/