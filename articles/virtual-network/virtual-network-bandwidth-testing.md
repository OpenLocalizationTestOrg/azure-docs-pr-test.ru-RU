---
title: "Тестирование пропускной способности сети для виртуальной машины Azure | Документация Майкрософт"
description: "Узнайте, как проверить пропускную способность сети для виртуальной машины Azure."
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
ms.openlocfilehash: ccebc722386a19014674d7a59757a3685bd50793
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Проверка пропускной способности (NTTTCP)

При тестировании пропускной способности сети в Azure рекомендуется использовать инструмент, предназначенный для тестирования сети и сводящий к минимуму использование других ресурсов, которые могут повлиять на скорость. Рекомендуется использовать NTTTCP.

Скопируйте этот инструмент на две виртуальные машины Azure одного размера. Одна виртуальная машина выполняет роль отправителя, а другая — получателя.

#### <a name="deploying-vms-for-testing"></a>Развертывание виртуальных машин для тестирования
В целях данного теста две виртуальные машины должны находиться в одной облачной службе или одной группе доступности, чтобы мы могли использовать их внутренние IP-адреса и исключить из теста подсистемы балансировки нагрузки. Существует возможность тестирования с помощью виртуального IP-адреса, но это выходит за рамки данного документа.
 
Запишите IP-адрес получателя. Назовем этот IP-адрес a.b.c.r.

Запишите число ядер на виртуальной машине. Назовем это значение \#num\_cores.
 
Запустите тест NTTTCP продолжительностью 300 секунд (5 минут) на виртуальной машине-отправителе и виртуальной машине-получателе.

Совет. При настройке этого теста для первого запуска можно попробовать более короткий период тестирования, чтобы быстрее получить результат. Если инструмент будет работать ожидаемым образом, продлите период тестирования до 300 секунд, чтобы получить наиболее точные результаты.

> [!NOTE]
> Для отправителя **и** получателя нужно указать **одинаковый** параметр длительности теста (-t).

Тестирование отдельного TCP-потока в течение 10 секунд:

Параметры получателя: ntttcp -r -t 10 -P 1

Параметры отправителя: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1

> [!NOTE]
> Предыдущий пример следует использовать только для подтверждения конфигурации. Допустимые примеры тестирования рассматриваются далее в этом документе.

## <a name="testing-vms-running-windows"></a>Тестирование виртуальных машин под управлением Windows

#### <a name="get-ntttcp-onto-the-vms"></a>Скопируйте NTTTCP на виртуальные машины.

Скачайте последнюю версию NTTTCP: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Или найдите ее, если ссылка уже не работает: <https://www.bing.com/search?q=ntttcp+download>\<. Первый результат поиска должен указывать на последнюю версию.

Рекомендуется поместить NTTTCP в отдельную папку, например c:\\tools.

#### <a name="allow-ntttcp-through-the-windows-firewall"></a>Разрешение трафика NTTTCP в брандмауэре Windows
На в брандмауэре Windows виртуальной машине-получателе создайте правило, разрешающее прием трафика NTTTCP. Проще разрешить саму программу NTTTCP по имени, чем входящий трафик через определенные TCP-порты.

Разрешите трафик NTTTCP в брандмауэре Windows следующей командой.

netsh advfirewall firewall add rule program=\<путь\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

Например, если вы скопировали ntttcp.exe в папку c:\\tools, то это будет следующая команда. 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>Выполнение тестов NTTTCP

Запустите NTTTCP на виртуальной машине-получателе (**в командной строке**, а не в PowerShell).

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

Если у виртуальной машины четыре ядра и IP-адрес 10.0.0.4, то команда будет выглядеть следующим образом.

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Запустите NTTTCP на виртуальной машине-отправителе (**в командной строке**, а не в PowerShell).

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Дождитесь результатов.


## <a name="testing-vms-running-linux"></a>Тестирование виртуальных машин под управлением Linux

Используйте nttcp-for-linux. Этот инструмент доступен по адресу <https://github.com/Microsoft/ntttcp-for-linux>.

Выполните приведенные ниже команды на виртуальных машинах Linux (отправителе и получателе), чтобы подготовить на них ntttcp-for-linux.

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

Как и в примере для Windows, предполагается, что IP-адрес виртуальной машины-получателя Linux — 10.0.0.4.

Запустите ntttcp-for-linux на виртуальной машине-получателе.

``` bash
ntttcp -r -t 300
```

На виртуальной машине-отправителе выполните следующую команду.

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Если для теста не указан параметр времени, по умолчанию он длится 60 секунд.

## <a name="testing-between-vms-running-windows-and-linux"></a>Тестирование подключения между виртуальными машинами под управлением Windows и Linux

В этом сценарии нам потребуется включить режим без синхронизации, чтобы можно было запустить тест. Это делается с помощью **флага -N** для Linux и **флага -ns** для Windows.

#### <a name="from-linux-to-windows"></a>Из Linux в Windows:

Получатель <Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Отправитель <Linux>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-to-linux"></a>Из Windows в Linux:

Получатель <Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Отправитель <Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Дальнейшие действия
* В зависимости от полученных результатов в вашем сценарии вполне может быть возможность [оптимизировать пропускную способность сети виртуальных машин](virtual-network-optimize-network-bandwidth.md).
* Узнайте больше из раздела [Виртуальная сеть Azure: часто задаваемые вопросы](virtual-networks-faq.md).
