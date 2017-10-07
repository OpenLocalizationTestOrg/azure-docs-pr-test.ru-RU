---
title: "aaaCustomize Azure IoT Suite подключен фабрики | Документы Microsoft"
description: "Описание как поведение hello toocustomize hello подключаться фабрики предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Настроить способ hello подключения фабрики решений отображает данные с серверов OPC UA

## <a name="introduction"></a>Введение

Hello решения подключенных фабрики собираются и отображаются данные из hello решения toohello подключенных серверов OPC UA. Можно просматривать и отправлять команды toohello OPC UA серверов в вашем решении. Дополнительные сведения о OPC UA см. в разделе hello [подключен фабрики часто задаваемые вопросы о](iot-suite-faq-cf.md).

Статистические данные в решении hello примеры hello общую эффективность работы оборудования (OEE) и ключевые показатели эффективности (KPI), которые можно просмотреть на панели мониторинга hello уровне фабрики hello, строки и станции. Hello следующем снимке экрана показаны hello OEE и ключевого показателя Эффективности значения для hello **сборки** станции на **рабочей строки 1**, в hello **Мюнхен** фабрики:

![Пример значения OEE и ключевых показателей Эффективности в решении hello][img-oee-kpi]

Hello позволяет вам tooview подробные сведения из элементов данных из hello OPC UA серверы, называемые *станции*. Hello следующем снимке экрана показано точечное hello количество произведенных элементов с определенной рабочей станции:

![Графики количества произведенных элементов][img-manufactured-items]

Если щелкнуть hello диаграмм позволяет исследовать данные hello дальше с помощью аналитики ряда времени (TSI):

![Просмотр данных с помощью Time Series Insights][img-tsi]

Содержание статьи

- Как hello данных становится доступной toohello различные представления в решении hello.
- Настройка решения hello способом hello отображает hello данные.

## <a name="data-sources"></a>Источники данных

Hello подключенных фабрики решений отображает данные из hello решения toohello подключенных серверов OPC UA. Установка по умолчанию Hello включает несколько серверов OPC UA работе модели фабрики. Можно добавить собственные серверы OPC UA, [подключения через шлюз] [ lnk-connect-cf] tooyour решения.

Можно просмотреть элементы данных hello отправку подключенного сервера OPC UA tooyour решение на панели мониторинга hello:

1. Перейдите toohello **выбрать сервер OPC UA** представления:

    ![Перейдите toohello выберите представление OPC UA][img-select-server]

1. Выберите сервер и нажмите кнопку **Подключить**. Нажмите кнопку **Продолжение** при отображении hello предупреждение системы безопасности.

    > [!NOTE]
    > Это предупреждение только отображается один раз для каждого сервера и устанавливает отношение доверия между hello решений мониторинга и сервером hello.

1. Теперь можно обзора hello элементов данных hello server можно отправить toohello решения. Элементы, которые отправляются toohello решения имеют Зеленый флажок:

    ![Опубликованные элементы][img-published]

1. При наличии *администратора* hello решения, вы можете toopublish toomake элемента данных доступно в hello подключен фабрики решения. Как администратор можно изменить значение hello элементов данных и вызывать методы в hello server OPC UA.

## <a name="map-hello-data"></a>Данные карты hello

Hello подключен maps решения фабрики и статистические функции hello элементов опубликованных данных из hello toohello server OPC UA различных представлений в решении hello. Hello подключенных фабрики решение развертывается tooyour учетная запись Azure при подготовке hello решения. JSON-файла в hello решения фабрики подключить Visual Studio сохраняет сведения о сопоставлении. Можно просматривать и изменять этот файл конфигурации JSON в фабрике подключенных hello решения Visual Studio. Можно повторно развернуть решение hello, после внесения изменений.

Можно использовать файл конфигурации hello:

- Измените существующий имитацию фабрик hello, производственных линиях и станции.
- Сопоставление данных из существующих серверов OPC UA подключении toohello решения.

tooclone копию hello подключения решения Visual Studio фабрики, hello используйте следующую команду git.

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

файл Hello **ContosoTopologyDescription.json** определяет сопоставление из hello OPC UA сервера данных представления toohello элементы на панели мониторинга решения подключенных фабрики hello hello. Этот файл конфигурации можно найти в hello **Contoso\Topology** папки в hello **веб-приложение** проект в решение Visual Studio hello.

содержимое JSON-файла hello Hello, организованные в виде иерархии фабрики, строка производства и узлы станции. Эта иерархия определяет иерархии навигации hello в панель мониторинга подключенных фабрики hello. Значения в каждом узле иерархии hello определяют hello сведений, отображаемых на панели мониторинга hello. Например hello JSON-файл содержит следующие значения для hello фабрики Мюнхен hello:

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

Hello имя, описание и расположение отображаются в представлении, в панели мониторинга hello:

![Данные Мюнхен hello панели управления][img-munich]

Каждая фабрика, производственная линия и станция имеют свойство изображений. JPEG-файлы можно найти в hello **Content\img** папки в hello **веб-приложение** проекта. Эти изображения файлы отображаются в панели мониторинга подключенных фабрики hello.

Каждая станция включает несколько подробные свойства, определяющие hello сопоставления из hello OPC UA элементов данных. Эти свойства описаны в следующих разделах hello:

### <a name="opcuri"></a>OpcUri

Hello **OpcUri** значение — hello OPC UA приложения URI, однозначно определяющий hello server OPC UA. Например, hello **OpcUri** станции сборки hello в строке производственного 1 в Мюнхен выглядит hello следующее значение: **urn: scada2194:ua:munich:productionline0:assemblystation**.

Hello идентификаторы URI hello подключенных серверов OPC UA можно просмотреть в панели мониторинга hello решения:

![Представление идентификаторов URI сервера OPC UA][img-server-uris]

### <a name="simulation"></a>Моделирование

Здравствуйте, сведения в hello **моделирование** узел является конкретных toohello моделирование OPC UA, которое выполняется в hello OPC UA серверов, предоставляемых по умолчанию. Он не используется для физических серверов OPC UA.

### <a name="kpi1-and-kpi2"></a>Kpi1 и Kpi2

Эти узлы описывают, как данные из станции hello влияют toohello два значения ключевого показателя Эффективности в панель мониторинга hello. В развертывании по умолчанию эти значения KPI являются единицами в час и расходом энергии в кВт в час. решение Hello вычисляет значения ключевого показателя Эффективности на уровне hello станции и объединяет их на уровнях фабрики и строка hello производства.

Каждый показатель KPI имеет минимальное, максимальное и целевое значение. Каждое значение ключевого показателя Эффективности можно также определить предупреждения действия для решения tooperform hello подключен фабрики. Hello следующий фрагмент кода показывает hello определений KPI для hello сборки станции производственного строке 1 в Мюнхен:

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

Hello следующем снимке экрана показано hello данных ключевого показателя Эффективности в панель мониторинга hello.

![Сведения о ключевых показателей Эффективности в hello панели мониторинга][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

Hello **OpcNodes** идентификации узлов hello элементов опубликованных данных из сервера OPC UA hello и указать способ tooprocess этих данных.

Hello **NodeId** значение идентифицирует hello конкретных NodeID UA OPC из hello server OPC UA. первый узел Hello в hello станции сборки для производства 1 в Мюнхен имеет значение **ns = 2; i = 385**. Объект **NodeId** указывает hello tooread элемента данных из сервера OPC UA hello и hello **символическое** предоставляет toouse понятное имя в панели мониторинга hello для этих данных.

Другие значения, связанные с каждым узлом, приведены в следующей таблице hello:

| Значение | Описание |
| ----- | ----------- |
| релевантности  | значения ключевого показателя Эффективности и OEE Hello позволяет согласовывать данные. |
| OpCode     | Агрегирование данных hello. |
| Units      | toouse единицы Hello в панели мониторинга hello.  |
| Visible    | Ли toodisplay, это значение в панель мониторинга hello. Некоторые значения используются в вычислениях, но не отображаются.  |
| Максимальная    | Hello максимальное значение, которое создает предупреждение в панели мониторинга hello. |
| MaximumAlertActions | Tootake действие в предупреждении tooan ответа. Например отправьте команды tooa станции. |
| ConstValue | Значение константы, используемое в вычислениях. |

## <a name="deploy-hello-changes"></a>Развертывание изменений hello

После завершения внесения изменений toohello **ContosoTopologyDescription.json** файл, необходимо повторно развернуть hello подключен tooyour решения фабрики учетная запись Azure.

Hello **-iot подключен фабрики azure** репозиторий включает **build.ps1** сценарий PowerShell, можно использовать toorebuild и развернуть решение hello.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об hello подключен фабрики предварительно настроенное решение hello чтение, следующие статьи:

* [Пошаговое руководство по работе с настроенным решением для удаленного мониторинга][lnk-rm-walkthrough]
* [Развертывание шлюза для подключенной фабрики][lnk-connect-cf]
* [Разрешения на сайт azureiotsuite.com hello][lnk-permissions]
* [Подключенная фабрика: вопросы и ответы](iot-suite-faq-cf.md)
* [Часто задаваемые вопросы об IoT Suite][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md