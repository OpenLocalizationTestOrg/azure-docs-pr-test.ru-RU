---
title: "фильтры соединения IP концентратора IoT aaaAzure | Документы Microsoft"
description: "Как toouse по IP-адресам tooblock соединений из определенного диапазона IP-адресов для tooyour центр Azure IoT. Вы можете блокировать подключения с отдельных IP-адресов или их диапазонов."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>Использование фильтрации IP-адресов

Безопасность является важным аспектом любого решения Интернета вещей на базе Центра Интернета вещей Azure. Иногда требуется tooexplicitly указать hello IP-адресов, из которых устройства могут подключаться как часть конфигурации безопасности. Hello _IP-фильтра_ дают возможность tooconfigure правила для отклонения или прием трафика с определенных адресов IPv4.

## <a name="when-toouse"></a>Когда toouse

Существует два конкретных вариантов использования при конечные точки центра IoT hello tooblock полезны для определенных IP-адресов:

- Центр Интернета вещей должен принимать трафик только из определенного диапазона IP-адресов и отклонять весь остальной трафик. Например, вы используете концентратор IoT с [Azure Express Route] toocreate частные подключения между центр IoT и локальной инфраструктуры.
- Необходимо tooreject трафика с IP-адресов, которые определены как подозрительные администратором концентратора IoT hello.

## <a name="how-filter-rules-are-applied"></a>Применение правил фильтрации

правила фильтрации IP Hello применяются на hello центра IoT уровня обслуживания. Таким образом правил фильтрации IP hello применяются tooall подключения с устройств и приложений серверной части, используя любой поддерживаемый протокол.

При попытке подключения с IP-адреса, который соответствует правилу отклонения IP-адресов в Центре Интернета вещей, пользователь получает сообщение об ошибке с кодом состояния 401 (Не авторизовано) и описанием. ответное сообщение Hello не упоминал hello IP правило.

## <a name="default-setting"></a>Значение по умолчанию

По умолчанию hello **IP-фильтра** сетки hello портала для центр IoT является пустым. Этот означает, что по умолчанию ваш центр принимает подключения с любых IP-адресов. Этот параметр по умолчанию — эквивалент tooa правило, которое принимает hello 0.0.0.0/0 IP-адресов.

![Параметры фильтрации IP-адресов по умолчанию для Центра Интернета вещей][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>Добавление или изменение правила фильтрации IP-адресов

При добавлении правила фильтра IP появится для hello следующие значения:

- **Имя правила фильтрации IP** , должно быть строкой уникальный, без учета регистра, буквенно-цифровое копирование too128 символов. Только hello ASCII 7-разрядных буквы, цифры и `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` принимаются.
- Выберите **Отклонить** или **принимать** как hello **действие** правила фильтрации сообщений hello IP.
- Укажите один IPv4-адрес или блок IP-адресов в нотации CIDR. Например, в CIDR нотации 192.168.100.0/22 представляет hello 1024 IPv4-адреса из 192.168.100.0 too192.168.103.255.

![Добавление центра IoT tooan правило фильтра IP][img-ip-filter-add-rule]

После сохранения правила hello, вы увидите оповещение, уведомляющее о том, что выполняется обновление hello.

![Уведомление о сохранении правила фильтрации IP-адресов][img-ip-filter-save-new-rule]

Hello **добавить** параметр отключен, при достижении hello максимум десять правил фильтра IP.

Можно изменить существующее правило, дважды щелкнув строку hello, которая содержит правило hello.

> [!NOTE]
> Отклонение IP адресов можно запретить другим службам Azure (Azure Stream Analytics, виртуальные машины Azure или hello обозреватель устройств на портале hello) взаимодействует с центром IoT hello.

> [!WARNING]
> При использовании сообщения tooread Azure Stream Analytics (ASA) из центра IoT с включена фильтрация IP-адресов, используйте hello концентратора событий-совместимое имя и ваш центр IoT конечной точки в hello ASA строки подключения.

## <a name="delete-an-ip-filter-rule"></a>Удаление правила фильтрации IP-адресов

toodelete правило фильтра IP выберите одно или несколько правил в сетке hello и щелкните **удалить**.

![Удаление правила фильтрации IP-адресов в Центре Интернета вещей][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>Оценка правила фильтрации IP-адресов

Правила фильтрации IP применяются в определенном порядке и hello первое правило, IP-адрес соответствует hello определяет hello принять или отклонить действие.

Например tooaccept адреса в диапазоне 192.168.100.0/22 hello и Отклонить все остальное, hello первого правила в сетке hello должен принимать 192.168.100.0/22 диапазона адресов hello. с помощью диапазона 0.0.0.0/0 hello следующего правила Hello Отклонить все адреса.

Можно изменить порядок hello правил фильтра IP в сетке hello, щелкнув hello вертикальное многоточие в начале строки hello и с помощью перетаскивания.

Фильтрация на новый IP-адрес toosave порядку правил, щелкните **Сохранить**.

![Изменение порядка hello правил фильтрации IP концентратора IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a>Дальнейшие действия

Изучение возможностей hello центра IoT toofurther см. в разделе:

- [Мониторинг операций][lnk-monitor]
- [Метрики Центра Интернета вещей][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md