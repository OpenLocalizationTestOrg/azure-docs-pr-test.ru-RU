---
title: "контроллер StorSimple EBOD aaaReplace | Документы Microsoft"
description: "Объясняет, как tooremove и заменить один или оба контроллера EBOD на устройстве StorSimple 8600."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>Замена контроллера EBOD на устройстве StorSimple
## <a name="overview"></a>Обзор
В этом учебнике описано как tooreplace неисправный модуль контроллера EBOD на устройстве Microsoft Azure StorSimple. tooreplace модуль контроллера EBOD, необходимо:

* Удалить неисправный контроллер EBOD hello
* установить новый контроллер EBOD

Рассмотрим следующую информацию, прежде чем начать hello.

* Во все неиспользуемые отсеки должны быть установлены пустые модули EBOD. Hello охлаждение корпуса не будет правильно Если слот остается открытым.
* с поддержкой горячей замены контроллера EBOD Hello и могут удаляться или заменяться. Не снимайте неисправный модуль, если у вас нет модуля на замену. При запуске процесса hello замены необходимо завершить в течение 10 минут.

> [!IMPORTANT]
> Прежде чем tooremove или заменить любой компонент StorSimple, обязательно изучите hello [условные обозначения значков безопасности](storsimple-safety.md#safety-icon-conventions) и других [меры предосторожности](storsimple-safety.md).
> 
> 

## <a name="remove-an-ebod-controller"></a>Снятие контроллера EBOD
Перед замена hello сбой модуля контроллера EBOD в вашем устройстве StorSimple, убедитесь, что hello другой модуль контроллера EBOD включен и запущен. Hello следующей процедуре и таблице объясняется, как tooremove hello модуль контроллера EBOD.

#### <a name="tooremove-an-ebod-module"></a>tooremove модуля EBOD
1. Откройте hello классический портал Azure.
2. Перейдите в слишком**устройств** > **обслуживания** > **состояние оборудования**и убедитесь, что ИНДИКАТОРЫ состояния hello объекта hello hello active EBOD модуль контроллера имеет зеленый цвет и hello Индикатор hello сбой модуля контроллера EBOD — красным.
3. Найдите модуль контроллера EBOD сбой hello в hello задняя сторона устройства hello.
4. Отсоедините кабели hello, подключения контроллера toohello модуль контроллера EBOD hello перед извлечением модуля EBOD hello из системы hello.
5. Запишите hello точный номер порта SAS модуля контроллера EBOD hello, подключенных toohello контроллера. Конфигурация toothis необходимые toorestore hello системы будет после замены модуля EBOD hello. 
   
   > [!NOTE]
   > Как правило, это будет порт A, который обозначается как **размещения в** в hello следующие схемы.
   > 
   > 
   
    ![Задняя панель контроллера EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Рис. 1.** Задняя поверхность модуля EBOD
   
   | Метка | Описание |
   |:--- |:--- |
   | 1 |Индикатор сбоя |
   | 2 |Индикатор питания |
   | 3 |Соединители SAS |
   | 4 |Индикаторы SAS |
   | 5 |Последовательные порты только для служебного использования |
   | 6 |Порт A (Входной порт узла) |
   | 7 |Порт B (Выходной порт узла) |
   | 8 |Порт C (только для служебного использования) |

## <a name="install-a-new-ebod-controller"></a>установить новый контроллер EBOD
Hello следующей процедуре и таблице поясняется, как tooinstall модуль контроллера EBOD в вашем устройстве StorSimple.

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall контроллера EBOD
1. Проверьте устройство EBOD hello наличие повреждений, особенно toohello разъем для подключения. Если какие-либо выводы погнуты, не устанавливайте hello нового контроллера EBOD.
2. Откройте позиции модуля hello слайд в корпус hello пока hello защелки hello кратковременных блокировок в hello.
   
    ![Установка контроллера EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **На рисунке 2** модуль контроллера EBOD Установка hello
3. Закрыть hello кратковременной блокировки. При фиксации защелки hello должны услышать щелчок.
   
    ![Освобождение защелки EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Рис. 3** закрытие защелки модуля EBOD hello
4. Подключите кабели hello. Используйте hello точной конфигурации, который существовал до замены hello. Просмотреть hello, следующая диаграмма и таблица, Дополнительные сведения о том, как tooconnect hello кабели.
   
    ![Подключите питание к устройству 4U](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Рис. 4**. Повторное подключение кабелей
   
   | Метка | Описание |
   |:--- |:--- |
   | 1 |Основной корпус |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Контроллер 0 |
   | 5 |Контроллер 1 |
   | 6 |Контроллер EBOD 0 |
   | 7 |Контроллер EBOD 1 |
   | 8 |Корпус EBOD |
   | 9 |Блоки распределения питания |

## <a name="next-steps"></a>Дальнейшие действия
Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).

