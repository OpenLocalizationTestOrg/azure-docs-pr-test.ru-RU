---
title: "aaaVisualize сетевой трафик с Наблюдатель сети Azure и средств с открытым исходным кодом | Документы Microsoft"
description: "На этой странице описываются как пакет Наблюдатель сети toouse захвата с tooand Capanalysis toovisualize трафика шаблонов из виртуальных машин."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Визуализация tooand шаблоны сетевой трафик из виртуальных машин с помощью средств с открытым исходным кодом

Захват пакетов содержат данные сети, которые позволяют расследований tooperform сети и глубокую проверку пакетов. Существует много откроется средств источника, о сети можно использовать снимки toogain tooanalyze пакетов аналитики. В числе таких средств можно назвать средство с открытым кодом CapAnalysis, предназначенное для визуализации захвата пакетов. Визуализация данных отслеживания пакетов способ ценных tooquickly производные важные сведения о шаблонах и аномалий в сети. Также визуализация позволяет передавать такую информацию другим людям в простом и доступном формате.

Наблюдатель сети Azure предоставляет hello toocapture возможности, которые записывает эти ценные данные, позволяя tooperform пакетов в сети. В этой статье мы предоставляем Пошаговое руководство по как захватывает Наблюдатель сети при помощи CapAnalysis toovisualize и приращение полезных сведений из пакета.

## <a name="scenario"></a>Сценарий

У вас есть развертывания простого веб-приложения на виртуальной Машине в Azure требуется toouse открытой средства toovisualize его tooquickly трафика сети определить поток характер и любых возможных аномалий. Наблюдатель за сетями позволяет получить захват пакетов конкретной сетевой среды и сохранить эти данные в учетной записи хранения. CapAnalysis можно приема hello захват пакетов непосредственно из большого двоичного объекта хранилища hello и отобразить его содержимое.

![сценарий][1]

## <a name="steps"></a>Действия

### <a name="install-capanalysis"></a>Установка CapAnalysis

tooinstall CapAnalysis на виртуальной машине, могут ссылаться инструкции официальный toohello https://www.capanalysis.net/ca/how-to-install-capanalysis здесь.
В порядке удаленного доступа к CapAnalysis, то необходимо порт tooopen 9877 на ВМ путем добавления нового правила безопасности для входящего трафика. Дополнительные сведения о создании правил в группах безопасности сети, см. слишком[создавать правила в существующей NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). После успешного добавления hello правило должно быть возможности tooaccess CapAnalysis из`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Используйте пакет отслеживания сеанса toostart Наблюдатель сети Azure

Наблюдатель сети разрешает трафик tootrack toocapture пакетов и из него виртуальную машину. Можно ссылаться инструкции toohello на [снимки управление пакетов с Наблюдатель сети](network-watcher-packet-capture-manage-portal.md) toostart сеанс отслеживания пакетов. На этом снимке пакетов могут храниться в toobe хранилища больших двоичных объектов, доступ к CapAnalysis.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Отправка tooCapAnalysis захват пакетов
Захват пакетов, выполняемое Наблюдатель сети с помощью вкладки «Импорт из URL-адрес» hello и предоставляя toohello ссылку хранилища BLOB-объекта хранения hello захват пакетов можно передать напрямую.

При предоставлении tooCapAnalysis ссылку, сделать tooappend убедиться, что URL-адрес SAS BLOB-объекта маркера toohello хранилища.  toodo, перейдите tooShared подписи доступа из учетной записи хранения hello, назначить hello разрешения и нажмите клавишу toocreate кнопку Создать SAS hello маркер. Затем можно добавить этот токен toohello пакетов записи хранилища больших двоичных объектов URL-адрес SAS.

Hello полученный URL-адрес будет выглядеть примерно следующим образом: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Анализ захвата пакетов

CapAnalysis предлагает различные параметры toovisualize получения пакетов, каждый обеспечивает анализ из другой точки зрения. Эти наглядные сводки помогают понять тенденции распределения сетевого трафика и быстро выявлять любые необычные действия. Некоторые из этих компонентов, показаны в hello после списка.

1. Таблицы потоков

    Это дает таблицы hello список потоках данных пакета hello, hello отметка времени, связанная с потоками hello и hello различных протоколов, связанных с потоком hello, а также исходный и конечный IP.

    ![Страница потоков CapAnalysis][5]

1. Обзор протоколов

    Эта панель позволяет tooquickly просмотра hello распределение сетевого трафика за hello различные протоколы и географических регионах.

    ![Обзор протоколов CapAnalysis][6]

1. Статистика

    Эта панель позволяет вы tooview статистики по сетевому трафику — байт отправлено и получено из источника и назначения IP-адресов, потоков для каждого из hello исходный и конечный IP-адресов, использовать протокол для различных потоков, а также срок hello потоков.

    ![Статистика CapAnalysis][7]

1. Географическая карта

    Эта панель предоставляет представление карты сетевого трафика, с цветами, масштабирование toohello объем трафика из каждой страны. Вы можете выбрать выделенный стран tooview дополнительный поток статистику, например hello долю данных отправленных и полученных от IP-адресов в данной стране.

    ![Географическая карта][8]

1. Фильтры

    CapAnalysis предоставляет набор фильтров для быстрого анализа пакетов определенного типа. Например вы можете toofilter hello данных с помощью протокола toogain конкретных аналитики на данном подмножестве трафика.

    ![filters][11]

    Посетите [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn Дополнительные сведения о всех CapAnalysis возможности.

## <a name="conclusion"></a>Заключение

Функция записи пакетов Наблюдатель сети позволяет экспертизы toocapture hello данных необходимости tooperform сети и лучше понять сетевого трафика. На этом примере мы показали, как можно легко интегрировать захват пакетов Наблюдателя за сетями со средствами визуализации с открытым кодом. С помощью средств с открытым исходным кодом, таких как захватывает CapAnalysis toovisualize пакетов, можно выполнять тщательную проверку пакетов и быстро определить тенденции в пределах сетевого трафика.

## <a name="next-steps"></a>Дальнейшие действия

Посетите toolearn Дополнительные сведения о журналах потока NSG, [журналы NSG потока](network-watcher-nsg-flow-logging-overview.md)

Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
