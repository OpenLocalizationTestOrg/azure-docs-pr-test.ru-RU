---
title: "Замена компонентов оборудования серии aaaStorSimple 8000 | Документы Microsoft"
description: "Описывает, как заменить toosafely PCM hello, батареи, модулей контроллера, контроллеры EBOD, диски и корпуса устройства StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.custom: 
ms.openlocfilehash: 5baca8ff630a1c064cb8bf7e1024b6590f0d6b81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>Замена аппаратного компонента на устройстве StorSimple серии 8000

## <a name="overview"></a>Обзор
учебники замена компонентов оборудования Hello описывают hello аппаратные компоненты в Microsoft Azure StorSimple 8000 ряда устройства и hello действия необходимые tooremove и замените их. В этой статье описываются значки безопасности hello, предоставляет указатели toohello подробные учебники и списки hello компоненты, которые можно заменить.

> [!IMPORTANT]
> Прежде чем tooremove или заменить любой компонент StorSimple, обязательно изучите hello [условные обозначения значков безопасности](#safety-icon-conventions) и других [меры предосторожности](storsimple-safety.md).


### <a name="safety-icon-conventions"></a>Условные обозначения сведений о безопасности
Hello следующей таблице описываются значки безопасности hello, используемые в этих учебниках. Обратите особое внимание toothese значки безопасности, как пройти tooremove hello действия и замена компонентов устройства.

| Значок | текст | Дополнительная информация |
|:--- |:--- |:--- |
| ![Значок "Внимание!"](./media/storsimple-hardware-component-replacement/Warning.png) |**ОПАСНОСТЬ!** |Указывает на опасную ситуацию, которая наверняка приведет к смерти или серьезной травме. Это сигнальное слово используется ограниченный toohello наиболее опасных ситуациях. |
| ![Значок "Внимание!"](./media/storsimple-hardware-component-replacement/Warning.png) |**ВНИМАНИЕ!** |Указывает на опасную ситуацию, которая может привести к смерти или серьезной травме. |
| ![Значок предупреждения](./media/storsimple-hardware-component-replacement/Caution.png) |**ОСТОРОЖНО!** |Указывает на опасную ситуацию, которая может привести к травме легкой или средней тяжести. |
| ![Значок "Примечание"](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**ПРИМЕЧАНИЕ.** |Указывает на важные сведения, не связанные с угрозой здоровью и жизни человека. |
| ![Значок "Опасность поражения электрическим током"](./media/storsimple-hardware-component-replacement/Electric.png) |**Опасность поражения электрическим током** |Указывает на высокий уровень напряжения. |
| ![Значок "Большой вес"](./media/storsimple-hardware-component-replacement/Weight.png) |**Большой вес** | |
| ![Значок "Компоненты не подлежат обслуживанию пользователем"](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**Компоненты не подлежат обслуживанию пользователем** |Не проводите техническое обслуживание устройства без должной подготовки. |
| ![Значок "Обязательно прочтите инструкции"](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**Сначала ознакомьтесь с инструкциями** | |
| ![Значок "Опасность опрокидывания"](./media/storsimple-hardware-component-replacement/TipHazard.png) |**Опасность опрокидывания** | |

### <a name="before-you-begin"></a>Перед началом работы
Ознакомьтесь с hello безопасности сведения о значках вашего устройства и безопасности, используемые в этом учебнике. Go слишком[безопасно Установка и эксплуатация устройства StorSimple](storsimple-safety.md) полные сведения. Быть убедиться, что hello tooreview [меры предосторожности](storsimple-safety.md#handling-precautions) до обработки устройства StorSimple.

Прежде чем tooreplace компонента, рассмотрите возможность hello следующую информацию.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **ВНИМАНИЕ!**

* При обращении с модулями и компонентами устройства StorSimple заземлите себя с помощью средств электростатического разряда или антистатического коврика.
* Не касайтесь электрических цепей. Используйте дескрипторов предоставленный hello и руководства при обработке компонентов, которые могут доступ к схемам.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **ПРИМЕЧАНИЕ.**

При замене модуля **никогда не оставляйте пустой отсек hello задней стенке корпуса hello**. Получите запасной модуль или заглушку перед удалением hello неисправной части.

## <a name="hardware-component-replacement-procedures"></a>Замена компонентов оборудования
Устройства серии StorSimple 8000 состоит из нескольких подключаемых модулей в основной hello и корпусе EBOD. Hello 8100 имеет только один основной корпус, а hello 8600 состоит из двух корпусов основного корпуса и корпуса EBOD.

Hello основные аппаратные компоненты в вашем устройстве, приведены в следующей таблице hello. Щелкните ссылку hello в hello **процедуры замены** toohello toogo столбца связанные учебника.

| Компоненты | Количество | Подключаемый модуль? | Процедура замены |
|:--- |:--- |:--- |:--- |
| Корпус |1 |Нет |[Замена шасси hello на устройстве StorSimple](storsimple-8000-chassis-replacement.md) |
| Основные контроллеры |2 |Да |[Замена модуля контроллера на устройстве StorSimple](storsimple-8000-controller-replacement.md) |
| Блоки питания и охлаждения (БПО) мощностью 764 Вт |2 |Да |[Замена блока питания и охлаждения на устройстве StorSimple](storsimple-8000-power-cooling-module-replacement.md) |
| Резервный аккумулятор |2 |Да |[Замените hello резервного аккумуляторного модуля на устройстве StorSimple](storsimple-8000-battery-replacement.md) |
| Диски |12 |Да |[Замена диска на устройстве StorSimple](storsimple-8000-disk-drive-replacement.md) |

**Таблица 1** аппаратные компоненты в основном корпусе hello

Hello основного корпуса и корпуса EBOD hello отличаются в свои модули ввода-вывода. Кроме того hello PCM имеют разный уровень мощности. Hello PCM в основном корпусе hello 764 Вт, тогда как в hello корпус EBOD — 580 W. PCM hello в hello основной корпус также содержать резервного аккумуляторного модуля.

| Компоненты | Количество | Подключаемый модуль? | Процедура замены |
|:--- |:--- |:--- |:--- |
| Корпус |1 |Нет |[Замена шасси hello на устройстве StorSimple](storsimple-8000-chassis-replacement.md) |
| Контроллеры EBOD |2 |Да |[Замена контроллера EBOD на устройстве StorSimple](storsimple-8000-ebod-controller-replacement.md) |
| Блоки питания и охлаждения (БПО) мощностью 580 Вт |2 |Да |[Замена блока питания и охлаждения на устройстве StorSimple](storsimple-8000-power-cooling-module-replacement.md) |
| Диски |12 |Да |[Замена диска на устройстве StorSimple](storsimple-8000-disk-drive-replacement.md) |

**В таблице 2** аппаратные компоненты в корпусе hello

Hello подключаемых модулей на устройстве hello, выделяются в следующие схемы передней и задней hello. Можно использовать эти схемы toodetermine hello расположение hello различных подключаемых модулей, если требуется замена. Hello передней показан hello жестких дисков и обратной сторон hello hello EBOD hello основного корпуса показаны hello подключаемых модулей.

![Передняя панель устройства с дисками](./media/storsimple-hardware-component-replacement/IC741028.png)

**Рис. 1** Передняя сторона устройства hello

| Метка | Описание |
|:--- |:--- |
| 0–11 |Дисковые накопители (всего 12) |

Hello основного корпуса и корпуса EBOD hello содержат дисковые модули. Hello шасси содержит двенадцать 3,5" жестких дисков в формат 3 х 4.

![Задняя панель модулей основного корпуса устройства](./media/storsimple-hardware-component-replacement/IC740994.png)

**На рисунке 2** задняя сторона основного корпуса hello

| Метка | Описание |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Контроллер 0 |
| 4. |Контроллер 1 |

![Задняя панель модулей корпуса EBOD устройства](./media/storsimple-hardware-component-replacement/IC769599.png)

**Рис. 3** задняя сторона корпуса EBOD hello

| Метка | Описание |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Контроллер EBOD 0 |
| 4 |Контроллер EBOD 1 |

## <a name="field-replaceable-units"></a>Блоки, заменяемые в полевых условиях
для устройства StorSimple доступны Hello следующие поля замену в условиях эксплуатации (FRU).

* Корпус (включая встроенную операционную панель hello)
* Блоки питания и охлаждения (БПО) мощностью 764 Вт
* Блоки питания и охлаждения (БПО) мощностью 580 Вт
* Жесткий диск с дисковым модулем
* Модуль контроллера
* Модуль контроллера EBOD
* Модуль резервного аккумулятора
* Комплект направляющих для монтажа в стойке

Проверьте [обратитесь в службу поддержки корпорации Майкрософт](storsimple-8000-contact-microsoft-support.md) tooorder любой из этих запасных частей.

## <a name="next-steps"></a>Дальнейшие действия
Проверьте все [информация по безопасности](storsimple-safety.md) перед началом tooreplace это аппаратный компонент StorSimple.

