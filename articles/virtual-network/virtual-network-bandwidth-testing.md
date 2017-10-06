---
title: "пропускная способность сети виртуальной Машины Azure aaaTesting | Документы Microsoft"
description: "Узнайте, как виртуальная машина Azure tootest сетевой пропускной способности."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Проверка пропускной способности (NTTTCP)

При тестировании производительность и пропускную способность сети в Azure, это лучший toouse средство, предназначенное hello сети для тестирования и сводит к минимуму использование hello другие ресурсы, которые могут повлиять на производительность. Рекомендуется использовать NTTTCP.

Скопируйте средство hello tootwo виртуальных машин Azure, hello одинакового размера. Одна виртуальная машина работает как ОТПРАВИТЕЛЯ, так и другие как получатель hello.

#### <a name="deploying-vms-for-testing"></a>Развертывание виртуальных машин для тестирования
В целях hello этого теста hello две виртуальные машины должны находиться в hello одной облачной службе или hello же группу доступности, мы можно использовать свои внутренние IP-адреса и исключить из теста hello hello подсистемы балансировки нагрузки. Это возможно tootest с hello виртуальных IP-адресов, но этот тип тестирования выходит за рамки данного документа hello.
 
Запишите IP-адрес ПОЛУЧАТЕЛЯ hello. Назовем этот IP-адрес a.b.c.r.

Запишите hello число ядер hello виртуальной Машины. Назовем это значение \#num\_cores.
 
Проведение hello отправителя виртуальной Машины и получателя виртуальной Машины hello NTTTCP проверки на 300 секунд (или 5 минут).

Совет: При настройке этого теста для hello первый раз, можно попробовать короткий отзыв tooget периода тестирования быстрее. После hello средство работает надлежащим образом, расширьте секунд периода too300 hello теста для hello наиболее точные результаты.

> [!NOTE]
> Отправитель Hello **и** необходимо указать получателя **hello же** параметра время проверки (-t).

tootest одного потока TCP на 10 секунд:

Параметры получателя: ntttcp -r -t 10 -P 1

Параметры отправителя: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1

> [!NOTE]
> предшествующий Образец Hello следует использовать tooconfirm конфигурации. Допустимые примеры тестирования рассматриваются далее в этом документе.

## <a name="testing-vms-running-windows"></a>Тестирование виртуальных машин под управлением Windows

#### <a name="get-ntttcp-onto-hello-vms"></a>Получите NTTTCP на hello виртуальных машин.

Загрузка последней версии hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Или найдите ее, если ссылка уже не работает: <https://www.bing.com/search?q=ntttcp+download>\<. Первый результат поиска должен указывать на последнюю версию.

Рекомендуется поместить NTTTCP в отдельную папку, например c:\\tools.

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>Разрешить NTTTCP через брандмауэр Windows hello
На hello ПОЛУЧАТЕЛЯ создайте разрешающее правило на tooallow брандмауэра Windows hello tooarrive трафика NTTTCP. Это простой tooallow hello всей NTTTCP программы по имени, а не tooallow определенные порты TCP входящего трафика.

Разрешить ntttcp через hello брандмауэра Windows следующим образом:

netsh advfirewall firewall add rule program=\<путь\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

Например, если вы скопировали ntttcp.exe toohello «c:\\средства» папку, это было бы hello команды: 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>Выполнение тестов NTTTCP

Запуск NTTTCP hello ПОЛУЧАТЕЛЯ (**запуска из CMD**, а не с PowerShell):

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

Если hello виртуальной Машины имеет четыре ядра и IP-адрес 10.0.0.4, он будет выглядеть следующим образом:

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Запуск NTTTCP hello ОТПРАВИТЕЛЯ (**запуска из CMD**, а не с PowerShell):

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Ожидание результатов hello.


## <a name="testing-vms-running-linux"></a>Тестирование виртуальных машин под управлением Linux

Используйте nttcp-for-linux. Этот инструмент доступен по адресу <https://github.com/Microsoft/ntttcp-for-linux>.

На hello виртуальных машин Linux (ОТПРАВИТЕЛЯ и ПОЛУЧАТЕЛЯ) выполните следующие команды, чтобы подготовить ntttcp для linux на виртуальные машины:

CentOS: установка Git.
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu: установка Git.
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Создание и установка в обеих ОС.
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Как показано в примере Windows hello предполагается, что IP-адрес ПОЛУЧАТЕЛЯ hello Linux — 10.0.0.4

Начало hello ПОЛУЧАТЕЛЯ NTTTCP для Linux:

``` bash
ntttcp -r -t 300
```

И на hello ОТПРАВИТЕЛЯ, выполните:

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Получает значения по умолчанию too60 длины теста секунды, если параметр отсутствует время

## <a name="testing-between-vms-running-windows-and-linux"></a>Тестирование подключения между виртуальными машинами под управлением Windows и Linux

В этом сценарии мы следует включить режим без синхронизации hello hello теста для запуска. Это делается с помощью hello **-N флаг** для Linux, и **-ns флаг** для Windows.

#### <a name="from-linux-toowindows"></a>Из Linux tooWindows:

Получатель <Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Отправитель <Linux>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>Из Windows tooLinux:

Получатель <Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Отправитель <Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Дальнейшие действия
* В зависимости от результатов, возможно, место слишком[оптимизировать пропускную способность виртуальных машин в сети](virtual-network-optimize-network-bandwidth.md) для вашего сценария.
* Узнайте больше из раздела [Виртуальная сеть Azure: часто задаваемые вопросы](virtual-networks-faq.md).
