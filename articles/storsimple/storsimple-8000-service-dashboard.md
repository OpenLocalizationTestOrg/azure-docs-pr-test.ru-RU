---
title: "Сводка устройства серии StorSimple 8000 aaaUse | Документы Microsoft"
description: "Описывает колонке сводки службы StorSimple hello и объясняет, как toouse его toomonitor hello работоспособность решения StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: ec1d971a8656df0be6eb1e3ec2603d97737ff070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-summary-blade-for-storsimple-8000-series-device"></a>Используйте сводки колонке hello службы для устройства серии StorSimple 8000

## <a name="overview"></a>Обзор

Сводка колонке Hello устройства StorSimple службы предоставляет сводное представление всех hello устройствах, подключенных toohello службе диспетчера устройств StorSimple, с выделением тех устройств, которые требуется внимание системных администраторов. Этот учебник представлено сводки колонке hello службы, описывается содержимое панели hello и функции и описаны hello задачи, которые можно выполнять на этой странице.

![Сводка по службе](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a>Команды управления

В hello StorSimple службы сводки колонки отображается hello параметры для управления службой диспетчера устройств StorSimple и службы toothis зарегистрированных устройств серии hello StorSimple 8000. Команды управления hello разделе hello верхней части колонки hello и левой стороны hello.

![Панель команд](./media/storsimple-8000-service-dashboard/service-summary2.png)

Используйте эти параметры, tooperform различные операции такие как добавление общих папок или томов или монитор hello различных заданий, выполняемых на устройствах StorSimple hello.


## <a name="essentials"></a>Основные компоненты

область essentials Hello записывает некоторые важные свойства hello, такие как группы ресурсов hello, местоположение и подписку, в которой был создан в диспетчере устройств StorSimple.

![Основные компоненты](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a>Сводные данные о службе диспетчера устройств StorSimple

* Hello **оповещения** Плитка предоставляет моментальный снимок всех активных оповещений hello на всех устройствах, сгруппированных по уровню серьезности оповещения.

    ![Элемент "Оповещения"](./media/storsimple-8000-service-dashboard/service-summary4.png)

    Выбрав hello плитки открывает hello **оповещения** колонке там, где можно щелкнуть отдельные предупреждения tooview Дополнительные сведения об этом оповещении, включая все рекомендуемые действия. Также можно очищать hello предупреждение, если hello неполадка устранена.

    ![Выбор элемента "Оповещения"](./media/storsimple-8000-service-dashboard/service-summary8.png)

* Hello **емкость** плитке отображается показано hello объем основного хранилища, подготовлена и оставшихся на всех устройствах относительный toohello общего объема хранилища на всех устройствах. **Подготовить** ссылается toohello объем хранилища, подготовлена и выделенный для использования, **остаток** ссылается toohello оставшихся емкости, которая может предоставляться на всех устройствах.

    ![Элемент "Емкость"](./media/storsimple-8000-service-dashboard/service-summary6.png)

    Hello **оставшиеся многоуровневого** емкость — hello доступной емкости, которая может быть подготовлена, включая облачные при hello **оставшиеся локального** — объем hello, оставшихся на дисках hello присоединенного toohello Устройства серии StorSimple 8000.


* В hello **использование** диаграммы, для устройств можно увидеть соответствующие метрики hello. Вы можете просмотреть hello основного хранилища, используемый для всех устройств и hello облачного хранилища, используемые устройствами через hello за последние 7 дней, по умолчанию hello период времени. 

    ![Плитка "Использование"](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    toochoose шкалу другое время используйте hello **изменить** параметр в правом верхнем углу hello hello диаграммы.

     ![Выбор элемента "Использование"](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![Экспорт данных диаграммы](./media/storsimple-8000-service-dashboard/service-summary11.png)

* Hello **устройств** Плитка предоставляет сводку hello количеством устройств серии StorSimple 8000 в своем StorSimple устройство Manager группируются по состоянию устройства. 

    ![Элемент "Устройства"](./media/storsimple-8000-service-dashboard/service-summary5.png)

    Щелкните этот hello tooopen плитки **устройств** колонки, затем щелкните toodrill отдельное устройство в устройство сводки toohello конкретного устройства hello. Кроме того, в колонке сводных данных о конкретном устройстве можно выполнять действия с этим устройством. Дополнительные сведения о колонке Сводка устройства hello go слишком[сводки колонке устройства](storsimple-8000-device-dashboard.md).

    ![Выбор элемента "Устройства"](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-hello-activity-logs"></a>Просмотр журналов действие hello

hello tooview различные операции выполняются в рамках вашей StorSimple диспетчер устройств, нажмите кнопку hello **журналы действий** ссылку на hello слева от оператора к колонке сводки службы StorSimple. После этого вы перейдете toohello **журналы действий** колонки, где можно просмотреть сводку последних операций hello выполнена.

![Журналы действий](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о том, как слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

