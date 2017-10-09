---
title: "Сводка колонке aaaStorSimple Virtual Array устройства | Документы Microsoft"
description: "Описание сводки колонке hello устройства для устройства StorSimple и как toouse его работоспособность hello toomonitor виртуального массива StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a>Используйте hello устройства сводки колонку для устройства StorSimple подключен tooStorSimple Virtual Array

## <a name="overview"></a>Обзор

Hello устройства StorSimple устройство колонке предоставляет Сводная информация о StorSimple Virtual Array, зарегистрированного с помощью заданного StorSimple диспетчера устройств, выделение неполадки с этих устройств, требующих вмешательства системного администратора. Этого учебника представлено сводки колонке hello устройства, описание содержимого hello и функции и описаны hello задачи, которые можно выполнять из эту колонку.

Сводка колонке Hello устройства отображает hello следующую информацию:

![Панель мониторинга устройства](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a>управления

В колонке устройства StorSimple hello вы видите hello параметры для управления устройства StorSimple. Команды управления hello разделе hello верхней части колонки hello и левой стороны hello. Используйте эти параметры tooadd папок или томов, или обновить или переключения виртуального массива.

Hello области essentials записывает некоторые hello важных свойств, таких как, состояние hello, модели, версии программного обеспечения а также toohello ссылку **веб-интерфейса** hello массива. Если находятся во внутренней сети, можно запустить напрямую hello [локальный веб-Интерфейс](storsimple-ova-web-ui-admin.md) tooadminister виртуального массива.

![Основные компоненты устройства](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a>Сводка по устройству StorSimple

* Hello **оповещения** Плитка предоставляет моментальный снимок всех активных оповещений hello виртуального массива, сгруппированных по уровню серьезности оповещения. Щелкните hello tooopen плитки приветствия **оповещения** колонку и нажмите кнопку отдельного предупреждения tooview Дополнительные сведения об этом оповещении, включая все рекомендуемые действия. Также можно очищать hello предупреждение, если hello неполадка устранена.

* Hello **емкость** плитки отображает hello основного хранилища, предоставляемому и оставшийся через hello виртуального устройства относительный toohello общего объема хранилища для hello таким же. **Подготовить** ссылается toohello объем хранилища, подготовлена и выделенный для использования, **остаток** ссылается toohello оставшихся емкости, которая может предоставляться через это устройство. Hello **оставшиеся многоуровневого** емкость — hello доступной емкости, которая может быть подготовлена, включая облачные при hello **оставшиеся локального** — объем hello, оставшихся на дисках hello присоединенного toothis виртуальный массив.

* В hello **использование** диаграммы, можно просмотреть hello основного хранилища в масштабах виртуального массива, а также hello облачного хранилища, используемых в течение hello за последние 7 дней, по умолчанию hello период времени. Используйте hello **изменить** параметр в правом верхнем углу hello toochoose диаграммы hello шкалу другое время.

* Hello **долей** или **тома** плитки Сводная информация о hello количество папок или томов в устройстве, сгруппированных по состоянию. Щелкните hello tooopen плитки приветствия **общих папок** или **тома** список колонке и щелкните отдельные папки или тома tooview или измените его свойства. Дополнительные сведения см. в разделе как слишком[Управление общими папками](storsimple-virtual-array-manage-shares.md) или [управление томами](storsimple-virtual-array-manage-volumes.md).

## <a name="next-steps"></a>Дальнейшие действия
Ниже перечислено, что вы можете узнать.
- [Управление общими файловыми ресурсами в виртуальном массиве StorSimple](storsimple-virtual-array-manage-shares.md)
    
- [Управление томами в виртуальном массиве StorSimple](storsimple-virtual-array-manage-volumes.md)

