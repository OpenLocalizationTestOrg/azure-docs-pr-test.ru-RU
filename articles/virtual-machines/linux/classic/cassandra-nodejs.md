---
title: "aaaRun Cassandra с Linux в Azure | Документы Microsoft"
description: "Как toorun Cassandra кластеров Linux на виртуальных машинах Azure из приложения Node.js"
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Запуск Cassandra под управлением Linux в Azure и доступ к нему из Node.js
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Ознакомьтесь с шаблонами Resource Manager для [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) и [кластера Spark и Cassandra с дистрибутивом CentOS](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Обзор
Microsoft Azure — это открытая облачная платформа, на которой выполняются как программное обеспечение корпорации Майкрософт, так и сторонние программы, к которым относятся операционные системы, серверы приложений, ПО промежуточного слоя для обмена сообщениями, а также базы данных SQL и NoSQL из коммерческих моделей и моделей с открытым исходным кодом. При создании гибких служб в общедоступных облаках (в том числе Azure) требуется тщательное планирование и разработка архитектуры обоих серверов приложений, а также уровней хранилищ. Архитектура распределенного хранилища Cassandra помогает создать системы высокой доступности, которые отказоустойчивы к сбоям кластеров. Cassandra — это облачная база данных NoSQL, поддерживаемая организацией Apache Software Foundation на сайте cassandra.apache.org; решение Cassandra написано на языке Java и поэтому выполняется на платформах Windows и Linux.

Hello посвящена эта статья является развертывание Cassandra tooshow на Ubuntu как кластер одного и нескольких центрах данных, используя виртуальные машины Microsoft Azure и виртуальные сети. Hello развертывания кластера для оптимизации рабочих нагрузок выходит за рамки этой статьи для его выполнения требуется настройка нескольких диск узла, соответствующие кольцо топологии проектирования и моделирования toosupport hello данных требуется репликации, согласованность данных, пропускная способность и требования высокой доступности.

Этот подход tooshow, порядок построения hello кластера Cassandra сравнение Docker, Chef или Puppet, что может hello много упрощает развертывание инфраструктуры принимает статьи.  

## <a name="hello-deployment-models"></a>Hello модели развертывания
Сеть Microsoft Azure предоставляет hello развертывания изолированной частной кластеров, hello доступ из которых может быть ограниченным tooattain нормально настроенную сетевой безопасности.  Поскольку в этой статье об отображении hello Cassandra развертывания на базовом уровне, не рассматривается на уровень согласованности hello и проектирования hello оптимальной хранилища для пропускной способности. Ниже приведен список hello сетевые требования для наших гипотетической кластера:

* Внешние системы не могут получить доступ к базе данных Cassandra из службы Azure или за пределами.
* Кластер Cassandra имеет toobe за подсистемой балансировки нагрузки для трафика thrift
* Узлы Cassandra должны развертываться в двух группах в каждом центре обработки данных для улучшенной доступности кластера.
* Заблокировать hello кластера таким образом, только для фермы серверов приложений имеет доступ к базе данных toohello напрямую
* Не допускаются открытые сетевые конечные точки, отличные от SSH.
* Каждый узел Cassandra должен иметь фиксированный внутренний IP-адрес.

Cassandra может быть один регион Azure развернутой tooa или регионы toomultiple по hello распределенных характер hello нагрузки. Развертывание в нескольких регионах модель можно использовать tooserve конечным пользователям ближе tooa определенного geography через hello Cassandra в одной инфраструктуре. В Cassandra встроенного узла репликации позаботится о hello синхронизации базы данных master несколькими записывает, рассчитанные на основе нескольких центрах обработки данных и представляет согласованное представление данных tooapplications hello. Развертывание в нескольких регионах также для устранения риска hello hello широкой простоев службы Azure. Настраиваемая топология согласованности и репликации Cassandra обеспечит выполнение различных требований приложений к RPO.

### <a name="single-region-deployment"></a>Развертывание в одной области
Начнем с развертывание в одном регионе и уязвимость hello выводов, сделанных при создании модели регионов. Виртуальные сети Azure будет использовать toocreate изолированных подсетей, требования безопасности сети hello, упомянутых выше могут быть выполнены.  Hello процесс, описанный в создании развертывание в одном регионе hello использует Ubuntu 14.04 LTS и Cassandra 2.08; Тем не менее, процесс hello легко может быть принятый toohello другие варианты Linux. Hello ниже приведены некоторые из hello нефункциональных характеристик hello развертывание в одном регионе.  

**Высокая доступность:** hello Cassandra узлы из hello, развернутых на рис. 1 доступности tootwo устанавливается таким образом, чтобы узлы hello распределены между несколькими доменами сбоя для обеспечения высокой доступности. Виртуальные машины с заметками с каждой группой доступности — too2 сопоставленных доменах сбоя.  Microsoft Azure использует концепцию hello toomanage домена сбоя незапланированных простоев (например сбоев оборудования или программного обеспечения) при hello понятие обновление домена (например, узла или гостевой ОС установка исправлений и обновлений, обновлений приложений) используется для управления запланированных простоев. См. в разделе [аварийное восстановление и высокий уровень доступности для приложений Azure](http://msdn.microsoft.com/library/dn251004.aspx) для роли hello доменов сбоя и обновления в достижение высокой доступности.

![Развертывание в одной области](./media/cassandra-nodejs/cassandra-linux1.png)

Рисунок 1. Развертывание в одном регионе

Обратите внимание на момент написания этой статьи hello, Azure не разрешает явное сопоставление hello группы виртуальных машин tooa определенную ошибку домена; Таким образом даже в модели развертывания hello показано на рисунке 1, это статистически вероятно, что все виртуальные машины hello может быть tootwo сопоставленных доменов сбоя вместо четырех.

**Трафик Thrift балансировки нагрузки:** Thrift клиентских библиотек внутри hello веб-сервера кластера toohello подключаться через внутренний балансировщик нагрузки. Для этого необходимо hello процесс добавления подсети toohello балансировщик внутренней нагрузки hello «данные» (см. рис. 1) в контексте hello hello облачной службы, в которой размещен кластер Cassandra hello. После определения hello внутренней подсистемы балансировки нагрузки, каждый узел требуется toobe конечной точки с балансировкой нагрузки hello добавлен с заметками hello набора балансировки нагрузки с ранее имя подсистемы балансировки нагрузки. Дополнительные сведения см. в статье [Обзор внутренней подсистемы балансировки нагрузки](../../../load-balancer/load-balancer-internal-overview.md).

**Начальные значения кластера:** важно tooselect hello большинства узлов высокой доступности для начальные значения, как новые узлы hello будут взаимодействовать с топологией hello toodiscover начальное число узлов кластера hello. Один узел из каждого набора доступности обозначается как начальное значение узлов tooavoid единственной точки отказа.

**Коэффициент репликации и уровень согласованности:** Cassandra элемента сборки в высокой доступности и устойчивостью данных характеризуется hello коэффициентом репликации (RF - количество копий каждой строки, сохраненной в кластере hello) и уровень согласованности (количество реплики toobe прочитать или записать перед возвратом вызывающего объекта toohello результат hello). Коэффициент репликации указывается во время hello создания пространство КЛЮЧЕЙ (аналогично tooa реляционной базы данных), тогда как при выдаче запроса CRUD hello задан уровень согласованности hello. Обратитесь к документации Cassandra на [настройки для обеспечения согласованности](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) сведения о согласованности и hello формула для вычисления кворума.

Cassandra поддерживает два типа моделей целостности данных — и согласованности окончательной; Hello коэффициентом репликации и уровень согласованности вместе определяют при hello данных будет соответствовать сразу после завершения операции записи, или он будет согласованным. Например указание КВОРУМА как hello уровня согласованности будет всегда гарантирует данных согласованности при любом уровне согласованности, меньше числа hello записан как необходимые tooattain toobe реплик КВОРУМА (например, один) приводит данных согласованным.

Hello 8 узлов кластера, показанном выше, с коэффициентом репликации 3 и КВОРУМА (2 узла считываются или записываются на согласованность) уровень согласованности чтения и записи, сохраняется в случае hello теоретической потери в группы большинство 1 узла репликации перед запуском приложения hello hello отметить hello сбоя. Это предполагает, что все пробелы ключа hello также балансировкой запросов на чтение и запись.  Здесь представлены Hello hello параметры, которые будут использоваться для развертывания hello кластера:

Конфигурация кластера Cassandra, развернутого в одном регионе

| Параметр кластера | Значение | Примечания |
| --- | --- | --- |
| Число узлов (N) |8 |Общее число узлов в кластере hello |
| Коэффициент репликации (RF) |3 |Число реплик данной строки |
| Уровень согласованности (запись) |QUORUM[(RF/2) +1) = 2] hello результат из hello формула округляется вниз |Записывает за hello большинство 2 реплики перед отправкой ответа hello toohello вызывающий объект; 3-й реплики записывается согласованным образом. |
| Уровень согласованности (чтение) |КВОРУМ [(RF/2) + 1 = 2] hello результат формулы hello округляется вниз |Считывает 2 реплики перед отправкой ответа toohello вызывающего. |
| Стратегия репликации |Дополнительную информацию о NetworkTopologyStrategy см. в разделе [Data Replication](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) (Репликация данных) в документации по Cassandra |Понимает топологии развертывания hello и помещает реплик на узлах, таким образом, чтобы все реплики hello не попадут в hello одинаково для монтажа в стойку |
| Информатор |Дополнительную информацию о GossipingPropertyFileSnitch см. в разделе [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) (Информаторы) в документации по Cassandra |NetworkTopologyStrategy использует концепцию snitch toounderstand hello топологии. GossipingPropertyFileSnitch обеспечивает улучшенное управление в сопоставлении каждого центра toodata узла и для установки в стойку. Эти сведения toopropagate сплетни затем использует Hello кластера. Это гораздо проще относительный tooPropertyFileSnitch параметр динамического IP |

**Рекомендации по Azure для кластера Cassandra.** Виртуальные машины Microsoft Azure способны использовать хранилище BLOB-объектов Azure для сохранения данных на диске. В службе хранилища Azure сохраняется три реплики каждого диска для обеспечения высокой надежности. Это означает, что каждая строка данных, вставляемых в таблицу Cassandra уже хранится в трех реплик и поэтому согласованность данных уже работают даже если hello коэффициент репликации (RF)-1. Основная проблема Hello с коэффициентом репликации, 1 — что приложения hello, будут простаивать даже в случае сбоя одного узла Cassandra. Тем не менее, если узел не работает для проблем hello (например, оборудования, программного обеспечения сбои системы) распознаются Azure Fabric Controller, он предоставит новый узел в своем месте с помощью hello же хранения на жестких дисках. Подготовка нового узла tooreplace hello старого один может занять несколько минут.  Аналогичным образом для планового обслуживания действий, подобных изменений гостевой ОС, обновляет Cassandra и изменения приложения Azure Fabric Controller выполняет последовательные обновления hello узлов в кластере hello.  Последовательные обновления также может остановить работу на нескольких узлах одновременно и поэтому hello кластера могут возникать небольшой простой для нескольких секций. Однако hello данных, не будут потеряны из-за toohello Встроенная избыточность хранилища Azure.  

Для развертывания систем tooAzure, которой не требуется высокий уровень доступности (например около 99,9 эквивалентные too8.76 часов/год; см. [высокий уровень доступности](http://en.wikipedia.org/wiki/High_availability) подробности) может быть может toorun с RF = 1 и уровень согласованности = один.  Для приложений с требованиями высокой доступности, RF = 3 и уровень согласованности = ждать hello простою одного из узлов hello одна из реплик hello КВОРУМА. RF = 1 в традиционной развертываниях (например локальной) не может использоваться из-за toohello возможные потери данных из подобных сбоев диска.   

## <a name="multi-region-deployment"></a>Развертывание в нескольких регионах
Данные center поддерживающей репликации и модель согласованности, описанных выше способствует развертывание в нескольких регионах hello стандартной hello без hello Cassandra элемента должны для любого внешнего средства. Это отличается от традиционных реляционных баз данных hello где hello настройки зеркального отображения базы данных для операций с несколькими хозяевами записи может быть весьма сложным. Сценарии использования hello, включая следующие hello Cassandra в нескольких регионах, настройка позволяет:

**Развертывание на основе выражения с учетом:** приложения с несколькими клиентами, с помощью Очистить сопоставления пользователей клиента-в-области, можно улучшенных с низкой задержки hello регионов кластера. Пример управления обучения системы для образовательных учреждений кластер, можно развернуть распределенного в Восток США и Запад США областей tooserve hello соответствующих необязательно для транзакций, а также аналитики. Hello данные можно локально согласованное hello время чтения и записи и может быть согласованным в обоих регионах hello. Имеются другие примеры, такие как распределение носителей и электронная торговля. Так, любые сферы, пользовательская база в которых сосредоточена в одном регионе, — хороший пример использования данной модели развертывания.

**Высокая доступность.** Избыточность — ключевой фактор обеспечения высокой доступности программного и аппаратного обеспечения. Дополнительные сведения см. в статье Building Reliable Cloud Systems on Microsoft Azure (Создание надежных облачных систем в Microsoft Azure). На базе Microsoft Azure hello единственный надежный способ достижения true избыточности — развертывание кластера регионов. Приложения могут развертываться в активный / активный "или" активный / пассивный режим и если один из регионов hello не работает, диспетчер трафика Azure может перенаправить трафик toohello активной области.  С развертывание в одном регионе hello 99,9, в случае доступности hello развертывания двух области можно достичь доступности 99,9999 вычисляется по формуле hello: (1-(1-0.999) * (1-0,999)) * 100); в разделе hello выше бумаги подробные сведения.

**Аварийное восстановление.** Если кластер Cassandra, развернутый в нескольких регионах, разработан должным образом, он может выдерживать катастрофические сбои центра обработки данных. Если один регион не работает, регионы tooother развернутое приложение hello можно запустить обслуживающий hello конечных пользователей. Как и любой business continuity реализациями приложения hello имеет toobe нечувствительного к ошибкам для потеря некоторых данных, возникающие в результате данные hello в асинхронный конвейер hello. Однако Cassandra делает восстановления hello намного swifter, чем время hello процессами восстановления традиционных баз данных. На рисунке 2 показана модель обычно развертывание в нескольких регионах hello с 8 узлов в каждом регионе. Обе области являются зеркальным отображением друг от друга для hello же из симметрии; схемы в реальном мире зависят от hello тип рабочей нагрузки (например транзакций или аналитическая), RPO, RTO, согласованность данных и требования к доступности.

![Развертывание в нескольких регионах](./media/cassandra-nodejs/cassandra-linux2.png)

Рисунок 2. Развертывание Cassandra в нескольких регионах

### <a name="network-integration"></a>Сетевая интеграция
Наборы виртуальных машин, развернутых tooprivate сетей, расположенных на две области обменивается данными друг с другом с помощью VPN-туннель. VPN-туннель Hello подключается двумя шлюзами программного обеспечения, настраивается во время процесса развертывания сети hello. Обе области имеют схожую архитектуру сети с точки зрения «web» и «данные» подсети; Сети Azure позволяет создавать столько подсети hello и применяет списки управления доступом, при необходимости по сетевой безопасности. При проектировании топологии кластера hello межсайтовую данных center связи задержки и hello экономический эффект считается необходимость toobe hello сетевого трафика.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Согласованность данных при развертывании в нескольких центрах обработки данных
Распределенные развертываний необходимость toobe учитывать hello кластера топологии влияние на производительность и высокий уровень доступности. Hello RF и уровень согласованности toobe необходимость выбран таким образом hello кворума не зависит от доступности всех центрах обработки данных hello hello.
Для системы, который требуется высокий уровень согласованности, LOCAL_QUORUM уровень согласованности (для операций чтения и записи) будет убедитесь, что hello локального считывает и записывает удовлетворяются из локального hello узлов, если данные реплицируются асинхронно toohello удаленных центров данных.  В таблице 2 приводятся подробные сведения для кластера hello несколькими регионами, описанные далее в hello записи копии конфигурации hello.

**Конфигурация кластера Cassandra, развернутого в двух регионах**

| Параметр кластера | Значение | Примечания |
| --- | --- | --- |
| Число узлов (N) |8 + 8 |Общее число узлов в кластере hello |
| Коэффициент репликации (RF) |3 |Число реплик данной строки |
| Уровень согласованности (запись) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] hello результат формулы hello округляется вниз |2 узлов будут записаны toohello первого центра данных синхронно. Hello дополнительных 2 узлов для кворума будут записаны асинхронно toohello второй центр обработки данных. |
| Уровень согласованности (чтение) |LOCAL_QUORUM ((RF/2) + 1) = 2 hello результат формулы hello округляется вниз |Запросов на чтение удовлетворяются из только одну область; 2 узлов доступны для чтения перед отправкой ответа hello задней toohello клиента. |
| Стратегия репликации |Дополнительную информацию о NetworkTopologyStrategy см. в разделе [Data Replication](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) (Репликация данных) в документации по Cassandra |Понимает топологии развертывания hello и помещает реплик на узлах, таким образом, чтобы все реплики hello не попадут в hello одинаково для монтажа в стойку |
| Информатор |Дополнительную информацию о GossipingPropertyFileSnitch см. в разделе [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) (Информаторы) в документации по Cassandra |NetworkTopologyStrategy использует концепцию snitch toounderstand hello топологии. GossipingPropertyFileSnitch обеспечивает улучшенное управление в сопоставлении каждого центра toodata узла и для установки в стойку. Эти сведения toopropagate сплетни затем использует Hello кластера. Это гораздо проще относительный tooPropertyFileSnitch параметр динамического IP |

## <a name="hello-software-configuration"></a>Hello конфигурации программного обеспечения
Hello следующих версий программного обеспечения используются во время развертывания hello:

<table>
<tr><th>Программное обеспечение</th><th>Источник</th><th>Version (версия)</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

Поскольку для загрузки среды выполнения Java требуется вручную принятие условий лицензии Oracle, toosimplify hello развертывания, загрузки всех hello позже загрузку на образ шаблона Ubuntu hello, который мы создадим как кластер toohello перед обменом рабочего стола toohello необходимое программное обеспечение развертывание.

Загрузите hello выше программное обеспечение в каталог хорошо известных загрузки (например, %TEMP%/downloads в Windows или ~/Downloads на большинстве ОС Linux или Mac) на локальном компьютере hello.

### <a name="create-ubuntu-vm"></a>СОЗДАНИЕ ВИРТУАЛЬНОЙ МАШИНЫ UBUNTU
В этом шаге процесса hello мы создадим Ubuntu изображения с hello необходимое программное обеспечение, чтобы hello изображение может быть повторно использован для инициализации несколько узлов Cassandra.  

#### <a name="step-1-generate-ssh-key-pair"></a>Шаг 1. Создание пары ключей SSH
Службе Azure требуется X509 открытый ключ PEM или DER кодировке во время подготовки hello. Создать пару открытого и закрытого ключей, с помощью инструкций hello, расположенный в том, как tooUse SSH с Linux в Azure. Если планируется toouse putty.exe как клиент SSH на Windows или Linux у вас есть tooconvert hello PEM кодировке RSA tooPPK закрытого ключа с помощью puttygen.exe; Hello инструкции можно найти в hello выше веб-странице.

#### <a name="step-2-create-ubuntu-template-vm"></a>Шаг 2. Создание виртуальной машины шаблонов Ubuntu
toocreate hello шаблона виртуальной Машины, войдите на hello Azure классического портала и использовать hello, следующая последовательность: нажмите кнопку Создать, ВЫЧИСЛЕНИЙ, ВИРТУАЛЬНОЙ МАШИНЫ, из КОЛЛЕКЦИИ, UBUNTU, Ubuntu Server 14.04 LTS и нажмите кнопку со стрелкой вправо hello. Учебник, описывающий, как toocreate ВМ Linux, см. статью создания виртуальной машины с Linux.

Введите следующую информацию на экране приветствия «конфигурация виртуальной машины» #1 hello:

<table>
<tr><th>ИМЯ ПОЛЯ              </td><td>       ЗНАЧЕНИЕ ПОЛЯ               </td><td>         ПРИМЕЧАНИЯ                </td><tr>
<tr><td>ДАТА ВЫПУСКА ВЕРСИИ    </td><td> Выберите дату из раскрывающегося hello</td><td></td><tr>
<tr><td>ИМЯ ВИРТУАЛЬНОЙ МАШИНЫ    </td><td> cass-template                   </td><td> Это имя узла hello hello виртуальной Машины </td><tr>
<tr><td>УРОВЕНЬ                     </td><td> STANDARD                           </td><td> Оставьте по умолчанию hello              </td><tr>
<tr><td>РАЗМЕР                     </td><td> A1                              </td><td>Необходимые для выбора hello виртуальных Машин на основании hello операции ввода-ВЫВОДА. для этого оставьте значение по умолчанию hello </td><tr>
<tr><td> НОВОЕ ИМЯ ПОЛЬЗОВАТЕЛЯ             </td><td> localadmin                       </td><td> "admin" — это зарезервированное имя пользователя в Ubuntu 12.xx и более поздних версий.</td><tr>
<tr><td> ПРОВЕРКА ПОДЛИННОСТИ         </td><td> Щелкните флажок                 </td><td>Установите этот флажок, если toosecure с использованием ключа SSH </td><tr>
<tr><td> СЕРТИФИКАТ             </td><td> Имя файла сертификата открытого ключа hello </td><td> Используйте hello открытого ключа, созданного ранее</td><tr>
<tr><td> Новый пароль    </td><td> надежный пароль </td><td> </td><tr>
<tr><td> Подтверждение пароля    </td><td> надежный пароль </td><td></td><tr>
</table>

Введите следующую информацию на экране приветствия «конфигурация виртуальной машины» #2 hello:

<table>
<tr><th>ИМЯ ПОЛЯ             </th><th> ЗНАЧЕНИЕ ПОЛЯ                       </th><th> ПРИМЕЧАНИЯ                                 </th></tr>
<tr><td> ОБЛАЧНАЯ СЛУЖБА    </td><td> Создать новую облачную службу.    </td><td>Облачная служба — это контейнер вычислительных ресурсов, таки как виртуальные машины.</td></tr>
<tr><td> DNS-ИМЯ ОБЛАЧНОЙ СЛУЖБЫ    </td><td>ubuntu-template.cloudapp.net    </td><td>Назначьте имя независимой подсистеме балансировки нагрузки</td></tr>
<tr><td> РЕГИОН/ТЕРРИТОРИАЛЬНАЯ ГРУППА/ВИРТУАЛЬНАЯ СЕТЬ </td><td>    Запад США    </td><td> Выберите регион, из которого веб-приложений, доступ к кластеру Cassandra hello</td></tr>
<tr><td>УЧЕТНАЯ ЗАПИСЬ ХРАНЕНИЯ </td><td>    Используйте значение по умолчанию.    </td><td>Использовать учетную запись хранения по умолчанию hello или предварительно созданная учетная запись хранения в определенном регионе</td></tr>
<tr><td>группа доступности; </td><td>    None </td><td>    Оставьте пустым.</td></tr>
<tr><td>КОНЕЧНЫЕ ТОЧКИ    </td><td>Используйте значение по умолчанию. </td><td>    Использовать конфигурацию SSH по умолчанию hello </td></tr>
</table>

Нажмите кнопку со стрелкой вправо, оставьте значения по умолчанию hello на экране приветствия #3 и щелкните hello «проверка» кнопки toocomplete hello ВМ процесса подготовки. Через несколько минут hello виртуальной Машины с hello имя «ubuntu шаблона» должно быть в состоянии «выполнение».

### <a name="install-hello-necessary-software"></a>УСТАНОВИТЕ НЕОБХОДИМОЕ программное обеспечение hello
#### <a name="step-1-upload-tarballs"></a>Шаг 1. Передача архивов в формате TAR
С помощью scp или pscp, hello копирования ранее загруженные программного обеспечения слишком ~ / directory загрузки с помощью hello следующий формат команды:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gz localadmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Повторите hello выше команду для JRE также и для hello Cassandra bits.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>Шаг 2: Подготовка hello структуру каталогов и извлекать архивы hello
Вход в hello виртуальных Машин и создать структуру каталогов для hello и извлечь программного обеспечения как суперпользователя, с помощью скрипта bash hello ниже:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


При вставке этот скрипт в окно vim убедитесь, что tooremove hello каретки возвращаемого ("\r») с помощью hello следующую команду:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>Шаг 3. Изменение etc/profile
Добавьте следующие hello в конце hello:

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>Шаг 4. Установка JNA для производственных систем
Используйте hello следующая команда последовательности: следующая hello команда установки jna-3.2.7.jar и too/usr/share.java jna платформы 3.2.7.jar каталог sudo apt-get установит libjna java

Создайте символические ссылки в каталоге $CASS_HOME/lib, чтобы сценарий запуска Cassandra смог найти эти JAR-файлы.

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Шаг 5. Настройка cassandra.yaml
Измените cassandra.yaml на каждой виртуальной Машины tooreflect настройки всеми виртуальными машинами hello [мы будет настраивать это во время реальное время подготовки hello]:

<table>
<tr><th>Имя поля   </th><th> Значение  </th><th>    Примечания </th></tr>
<tr><td>cluster_name </td><td>    "CustomerService"    </td><td> Используйте имя hello, которое отражает развертывания</td></tr>
<tr><td>listen_address    </td><td>[Оставьте пустым.]    </td><td> Удалите "localhost". </td></tr>
<tr><td>rpc_addres   </td><td>[Оставьте пустым.]    </td><td> Удалите "localhost". </td></tr>
<tr><td>начальные значения    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>Список всех hello IP-адресов, которые обозначены как начальные значения.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> Hello NetworkTopologyStrateg используется для выведения центра обработки данных hello и hello стойки hello виртуальной Машины</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>Шаг 6: Захват образа виртуальной Машины hello
Войдите на виртуальную машину hello, с помощью имени узла hello (template.cloudapp.net hk ЦС) и hello SSH закрытый ключ, созданный ранее. В разделе о том, как tooUse SSH с Linux в Azure для получения подробной информации по как toolog с помощью hello команды ssh или putty.exe.

Выполните hello следующая последовательность действий toocapture hello образа:

##### <a name="1-deprovision"></a>1. Отзыв
Команда hello «sudo waagent — отзыва + пользователь «tooremove определенные сведения об экземпляре виртуальной машины. В разделе для [как tooCapture виртуальной машины Linux](capture-image.md) tooUse как шаблон более подробные сведения на запись образа hello.

##### <a name="2-shutdown-hello-vm"></a>2: hello завершение работы виртуальной Машины
Убедитесь, что выделен этой виртуальной машине hello и щелкните ссылку SHUTDOWN hello из hello нижней панели команд.

##### <a name="3-capture-hello-image"></a>3: hello записи (рисунок)
Убедитесь, что выделен этой виртуальной машине hello и щелкните ссылку ОТСЛЕЖИВАНИЯ hello из hello нижней панели команд. В следующий экран приветствия присвойте имя ОБРАЗА (например hk-cas-2-08-ub-14-04-2014071), соответствующие описание ИЗОБРАЖЕНИЯ и щелкните процесс ОТСЛЕЖИВАНИЯ hello toofinish пометить hello «проверка».

Это займет несколько секунд и hello изображения должен быть доступен в разделе Мои ОБРАЗЫ из коллекции образов hello. Hello исходной виртуальной Машины будут автоматически удалены после hello успешно образа. 

## <a name="single-region-deployment-process"></a>Процесс развертывания в одном регионе
**Шаг 1: Создание виртуальной сети hello** войти hello портал Azure и создание виртуальной сети (классической) с атрибутами hello показано в следующей таблице hello. В разделе [Создание виртуальной сети (классические) с помощью портала Azure hello](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) более подробное пошаговое описание процесса hello.      

<table>
<tr><th>Имя атрибута виртуальной машины</th><th>Значение</th><th>Примечания</th></tr>
<tr><td>Имя</td><td>vnet-cass-west-us</td><td></td></tr>
<tr><td>Регион</td><td>Запад США</td><td></td></tr>
<tr><td>DNS-серверы</td><td>None</td><td>Пропустите этот атрибут, поскольку мы не используем DNS-сервер</td></tr>
<tr><td>Пространство адресов</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>Начальный IP-адрес</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Добавьте следующие подсетей hello:

<table>
<tr><th>Имя</th><th>Начальный IP-адрес</th><th>CIDR</th><th>Примечания</th></tr>
<tr><td>web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Подсеть для hello веб-фермы</td></tr>
<tr><td>data</td><td>10.1.2.0</td><td>/24 (251)</td><td>Подсети для узлов hello базы данных</td></tr>
</table>

Данные и Web подсети могут быть защищены через сетевые группы безопасности покрытия hello, из которых выходит за рамки данной статьи.  

**Шаг 2: Подготовка виртуальных машин** с помощью hello образ, созданный ранее, она будет создана hello следующих виртуальных машин в облаке hello server» hk-c-svc запад» и привязать toohello подсетей, как показано ниже:

<table>
<tr><th>Имя компьютера    </th><th>Подсеть    </th><th>IP-адрес    </th><th>группа доступности;</th><th>Контроллер домена/стойка</th><th>Начальное значение?</th></tr>
<tr><td>hk-c1-west-us    </td><td>data    </td><td>10.1.2.4    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1 </td><td>Да</td></tr>
<tr><td>hk-c2-west-us    </td><td>data    </td><td>10.1.2.5    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1    </td><td>Нет </td></tr>
<tr><td>hk-c3-west-us    </td><td>data    </td><td>10.1.2.6    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>Да</td></tr>
<tr><td>hk-c4-west-us    </td><td>data    </td><td>10.1.2.7    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>Нет </td></tr>
<tr><td>hk-c5-west-us    </td><td>data    </td><td>10.1.2.8    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>Да</td></tr>
<tr><td>hk-c6-west-us    </td><td>data    </td><td>10.1.2.9    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>Нет </td></tr>
<tr><td>hk-c7-west-us    </td><td>data    </td><td>10.1.2.10    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>Да</td></tr>
<tr><td>hk-c8-west-us    </td><td>data    </td><td>10.1.2.11    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>Нет </td></tr>
<tr><td>hk-w1-west-us    </td><td>web    </td><td>10.1.1.4    </td><td>hk-w-aset-1    </td><td>                       </td><td>Недоступно</td></tr>
<tr><td>hk-w2-west-us    </td><td>web    </td><td>10.1.1.5    </td><td>hk-w-aset-1    </td><td>                       </td><td>Недоступно</td></tr>
</table>

Создание hello выше список виртуальных машин требуются hello, следуйте процедуре:

1. Создайте пустую облачную службу в определенном регионе.
2. Создайте виртуальную Машину из ранее записанного образа hello и присоединить ее toohello виртуальной сети, созданные ранее; Повторите это действие для всех виртуальных машин hello
3. Добавьте облачную службу toohello балансировщик внутренней нагрузки и присоединить ее подсети toohello «данные»
4. Для каждой виртуальной Машины, созданной ранее добавьте конечную точку балансировки нагрузки для трафика thrift через балансировки нагрузки подключен набор toohello ранее созданные внутренняя Подсистема балансировки нагрузки

Hello выше процесса могут быть выполнены с помощью классического портала Azure; использовать компьютер Windows (используйте ВМ в Azure, если у вас нет доступа tooa Windows машины), автоматически использовать все виртуальные машины 8 hello, следуя tooprovision сценария PowerShell.

**Список 1. Сценарий PowerShell для подготовки виртуальных машин**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**Шаг 3. Настройка Cassandra на каждой виртуальной машине**

Вход в hello виртуальной Машины и выполнить hello следующие:

* Изменение $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello центра и стойку свойств данных:
  
       dc =EASTUS, rack =rack1
* Изменение узлов cassandra.yaml tooconfigure начальное значение, как показано ниже:
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**Шаг 4: Запуск виртуальных машин hello и проверки кластера hello**

Войти в одном из узлов hello (например hk-c1-Запад США) и выполнения hello следующая команда toosee hello состояние hello кластера:

       nodetool –h 10.1.2.4 –p 7199 status

Вы должны увидеть hello отображения аналогичные toohello один ниже 8 узлов кластера.

<table>
<tr><th>Состояние</th><th>Адрес    </th><th>загрузить    </th><th>Маркеры    </th><th>Владение </th><th>Идентификатор узла    </th><th>Стойка</th></tr>
<tr><th>UN    </td><td>10.1.2.4     </td><td>87,81 КБ    </td><td>256    </td><td>38,0 %    </td><td>GUID (удален)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.5     </td><td>41,08 КБ    </td><td>256    </td><td>68,9 %    </td><td>GUID (удален)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.6     </td><td>55,29 КБ    </td><td>256    </td><td>68,8 %    </td><td>GUID (удален)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.7     </td><td>55,29 КБ    </td><td>256    </td><td>68,8 %    </td><td>GUID (удален)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.8     </td><td>55,29 КБ    </td><td>256    </td><td>68,8 %    </td><td>GUID (удален)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.9     </td><td>55,29 КБ    </td><td>256    </td><td>68,8 %    </td><td>GUID (удален)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.10     </td><td>55,29 КБ    </td><td>256    </td><td>68,8 %    </td><td>GUID (удален)</td><td>rack4</td></tr>
<tr><th>UN    </td><td>10.1.2.11     </td><td>55,29 КБ    </td><td>256    </td><td>68,8 %    </td><td>GUID (удален)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Тест hello одного региона кластера
Используйте следующие шаги tootest hello кластера hello.

1. С помощью командлета Get-AzureInternalLoadbalancer команды Powershell hello, получите IP-адрес hello hello внутренней подсистемы балансировки нагрузки (например)  10.1.2.101). Ниже приведен синтаксис Hello команды hello: Get-AzureLoadbalancer – ServiceName «hk-c-svc-west-us» [отображаются hello hello внутренней подсистемы балансировки нагрузки вместе с его IP-адрес]
2. Войти в веб-ферме hello виртуальной Машины (например hk-w1-Запад США) с помощью Putty или ssh
3. Выполните команду $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. Используйте следующие команды tooverify CQL работе кластера hello hello.
   
     CREATE KEYSPACE customers_ks WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');
   
     SELECT * FROM Customers;

Вы увидите отображения как hello один ниже:

<table>
  <tr><th> customer_id </th><th> firstname </th><th> Lastname </th></tr>
  <tr><td> 1 </td><td> Артем </td><td> Кузнецов </td></tr>
  <tr><td> 2 </td><td> Ольга </td><td> Кузнецов </td></tr>
</table>

Учтите, что пространство, hello ключей, созданного на шаге 4 используется SimpleStrategy с replication_factor 3. SimpleStrategy рекомендуется для развертываний с одним центром обработки данных, а NetworkTopologyStrategy — для развертываний с несколькими центрами. Значение параметра replication_factor, равное 3, обеспечивает отказоустойчивость узлов.

## <a id="tworegion"> </a>Процесс развертывания в нескольких регионах
Будет использовать развертывание в одном регионе hello завершения и повторите hello же процесс для установки второй области hello. Hello ключевое различие между hello одной и нескольких области развертывания является hello установки туннеля VPN для обмена данными между области; Мы начинается с установки сети hello, подготовить виртуальные машины hello и настроить Cassandra.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>Шаг 1: Создание hello виртуальной сети в hello второй области
Войдите на классический портал Azure hello и создайте виртуальную сеть с hello Показать атрибуты в таблице hello. В разделе [настройки виртуальной сети только в классический портал Azure hello](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) более подробное пошаговое описание процесса hello.      

<table>
<tr><th>Имя атрибута    </th><th>Значение    </th><th>Примечания</th></tr>
<tr><td>Name (Имя)    </td><td>vnet-cass-east-us</td><td></td></tr>
<tr><td>Регион    </td><td>Восток США</td><td></td></tr>
<tr><td>DNS-серверы        </td><td></td><td>Пропустите этот атрибут, поскольку мы не используем DNS-сервер</td></tr>
<tr><td>Настройка VPN-подключения типа "точка-сеть"</td><td></td><td>        Пропустите этот атрибут</td></tr>
<tr><td>"Настроить VPN типа "сеть-сеть"</td><td></td><td>        Пропустите этот атрибут</td></tr>
<tr><td>Пространство адресов    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>Начальный IP-адрес    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Добавьте следующие подсетей hello:

<table>
<tr><th>Имя    </th><th>Начальный IP-адрес    </th><th>CIDR    </th><th>Примечания</th></tr>
<tr><td>web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Подсеть для hello веб-фермы</td></tr>
<tr><td>data    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Подсети для узлов hello базы данных</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>Шаг 2. Создание локальных сетей
В локальной сети в Azure виртуальные сети является адресное пространство прокси-сервера, которое сопоставляет tooa удаленного сайта, включая частное облако или другом регионе Azure. Это адресное пространство прокси-сервера — привязанного tooa удаленного шлюз для маршрутизации toohello сети прямо к сети назначения. В разделе [настройки виртуальной сети tooVNet подключения](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) hello инструкции на установление подключения VNET-VNET.

Создайте две локальные сети в hello, приведенные ниже сведения:

| Имя сети | Адрес VPN-шлюза | Пространство адресов | Примечания |
| --- | --- | --- | --- |
| hk-lnet-map-to-east-us |23.1.1.1 |10.2.0.0/16 |При создании hello локальной сети предоставьте заполнитель адрес шлюза. адрес шлюза реальные Hello заполняется в том случае, после создания шлюза hello. Убедитесь, что адресное пространство hello совпадает Здравствуйте соответствующей удаленной виртуальной сети; в этом случае hello виртуальная сеть создана в hello регионе Восток США. |
| hk-lnet-map-to-west-us |23.2.2.2 |10.1.0.0/16 |При создании hello локальной сети предоставьте заполнитель адрес шлюза. адрес шлюза реальные Hello заполняется в том случае, после создания шлюза hello. Убедитесь, что адресное пространство hello совпадает Здравствуйте соответствующей удаленной виртуальной сети; в этом случае hello виртуальная сеть создана в hello Запад США. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>Шаг 3: Сопоставление «Local» сети toohello соответствующих виртуальных сетей
Из hello классический портал Azure выберите каждой виртуальной сети, щелкните «Настроить», проверьте «Connect toohello локальной сети», а затем выберите hello локальных сетей на hello, приведенные ниже сведения:

| Виртуальная сеть | Локальная сеть |
| --- | --- |
| hk-vnet-west-us |hk-lnet-map-to-east-us |
| hk-vnet-east-us |hk-lnet-map-to-west-us |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>Шаг 4. Создание шлюзов для сетей VNET1 и VNET2
С панели мониторинга hello обоих hello виртуальных сетей нажмите кнопку Создать ШЛЮЗ, который запустит процесс подготовки шлюза VPN hello. После нескольких минут hello мониторинга всех виртуальных сетей должны отображаться адрес hello фактическое шлюза.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Шаг 5: Обновление «Local» сети с адресами соответствующих «шлюз» hello
Изменение обоих hello локальных сетей tooreplace hello заполнитель шлюза IP-адрес с hello истинные IP-адреса hello просто подготовить шлюзы. Используйте hello следующие сопоставления:

<table>
<tr><th>Локальная сеть    </th><th>Шлюз виртуальной сети</th></tr>
<tr><td>hk-lnet-map-to-east-us </td><td>Шлюз сети hk-vnet-west-us</td></tr>
<tr><td>hk-lnet-map-to-west-us </td><td>Шлюз сети hk-vnet-east-us</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>Шаг 6: Обновление общего ключа hello
Используйте hello следующий ключ IPSec hello tooupdate сценария Powershell каждого шлюза VPN [реализую hello использования ключа для обоих шлюзов hello]: Set-AzureVNetGatewayKey - VNetName hk-vnet-east-us - LocalNetworkSiteName hk-lnet-map-to-west-us - SharedKey D9E76BKK Набор AzureVNetGatewayKey - VNetName hk-vnet-west-us - LocalNetworkSiteName hk-lnet-map-to-east-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>Шаг 7: Установите подключение hello виртуальной сети для виртуальной сети
Hello классический портал Azure используя меню «Панель МОНИТОРИНГА» hello оба подключения шлюза к шлюзу hello tooestablish виртуальных сетей. Используйте элементы меню «ПОДКЛЮЧИТЬСЯ» hello в hello нижней панели инструментов. Через несколько минут мониторинга hello графически отображать сведения о подключении hello.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>Шаг 8: Создание виртуальных машин hello в регионе #2
Создайте образ Ubuntu hello, описанный в регионе #1 развертывания следующие hello же шагов или скопируйте hello образа виртуального жесткого диска файл toohello учетной записи хранилища Azure в регионе #2 и hello изображения. Использовать это изображение и создать hello после списка виртуальных машин в новой облачной службы hk-c-svc-east-us:

| Имя компьютера | Подсеть | IP-адрес | группа доступности; | Контроллер домена/стойка | Начальное значение? |
| --- | --- | --- | --- | --- | --- |
| hk-c1-east-us |data |10.2.2.4 |hk-c-aset-1 |dc =EASTUS rack =rack1 |Да |
| hk-c2-east-us |data |10.2.2.5 |hk-c-aset-1 |dc =EASTUS rack =rack1 |Нет |
| hk-c3-east-us |data |10.2.2.6 |hk-c-aset-1 |dc =EASTUS rack =rack2 |Да |
| hk-c5-east-us |data |10.2.2.8 |hk-c-aset-2 |dc =EASTUS rack =rack3 |Да |
| hk-c6-east-us |data |10.2.2.9 |hk-c-aset-2 |dc =EASTUS rack =rack3 |Нет |
| hk-c7-east-us |data |10.2.2.10 |hk-c-aset-2 |dc =EASTUS rack =rack4 |Да |
| hk-c8-east-us |data |10.2.2.11 |hk-c-aset-2 |dc =EASTUS rack =rack4 |Нет |
| hk-w1-east-us |web |10.2.1.4 |hk-w-aset-1 |Недоступно |Недоступно |
| hk-w2-east-us |web |10.2.1.5 |hk-w-aset-1 |Недоступно |Недоступно |

Таким же Здравствуйте, выполните инструкции в виде области #1, но использовать 10.2.xxx.xxx адресное пространство.

### <a name="step-9-configure-cassandra-on-each-vm"></a>Шаг 9. Настройка Cassandra на каждой виртуальной машине
Вход в hello виртуальной Машины и выполнить hello следующие:

1. Изменение $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello центра и стойку свойств данных в формате hello: dc = стойка EASTUS = rack1
2. Изменение узлов начальное значение tooconfigure cassandra.yaml: начальные значения: «10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10»

### <a name="step-10-start-cassandra"></a>Шаг 10. Запуск Cassandra
Войдите на каждой виртуальной Машине и запустите Cassandra в фоновом режиме hello, выполнив следующую команду hello: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>Тест hello кластера в нескольких регионах
К этому моменту Cassandra был too16 развернутые узлы с 8 узлов в каждом регионе Azure. Эти узлы находятся в hello же кластера силу hello общее имя кластера и настройка узла hello начальное значение. Используйте следующий процесс tootest hello кластера hello.

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>Шаг 1: Получение IP-адреса подсистемы балансировки нагрузки внутренней hello для обоих регионах hello, с помощью PowerShell
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-west-us"
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-east-us"  
  
    Обратите внимание, hello IP-адреса (например - 10.1.2.101, восток - Запад 10.2.2.101) отображается.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>Шаг 2: Выполните ниже hello в hello Запад после выполнения входа в hk-w1-Запад us
1. Выполните команду $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. Выполните следующие команды CQL hello:
   
     CREATE KEYSPACE customers_ks   WITH REPLICATION = { 'class' : 'NetworkToplogyStrategy', 'WESTUS' : 3, 'EASTUS' : 3};   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

Вы увидите отображения как hello один ниже:

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |Артем |Кузнецов |
| 2 |Ольга |Кузнецов |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>Шаг 3: Выполните следующие hello в восточном регионе hello после выполнения входа в hk-w1-east-us:
1. Выполните команду $CASS_HOME/bin/cqlsh 10.2.2.101 9160.
2. Выполните следующие команды CQL hello:
   
     USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

Вы должны увидеть hello же отображения, что для западного региона hello.

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |Артем |Кузнецов |
| 2 |Ольга |Кузнецов |

Выполнить несколько дополнительных вставок и просмотреть их получение реплицированных toowest-нам частью кластера hello.

## <a name="test-cassandra-cluster-from-nodejs"></a>Тестирование кластера Cassandra из файла Node.js
С помощью одного из виртуальных машин Linux hello создан на уровне «web» hello ранее, мы будет выполнять простые hello вставленные ранее объекта данных tooread Node.js сценария

**Шаг 1. Установка Node.js и клиента Cassandra**

1. Установка Node.js и NPM
2. Установите пакет узлов "cassandra-client" с помощью NPM
3. Выполните следующий скрипт командной оболочки hello, отображающий строки json hello hello извлечения данных hello:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Заключение
Microsoft Azure — это гибкая платформа, которая разрешает запуск hello Microsoft как, так и программное обеспечение с открытым исходным кодом, как показано в этом упражнении. Высокой доступности кластеров Cassandra могут развертываться в одном центре обработки данных через hello распространение hello узлов кластера в нескольких доменах сбоя. Кластеры Cassandra также можно развертывать в нескольких географически разделенных регионах Azure для отказоустойчивых систем. Azure и позволяет совместно Cassandra hello построения высокомасштабируемых, высокой доступности и с современного Интернета аварийного восстановимых облачные службы требуется масштабирование служб.  

## <a name="references"></a>Ссылки
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

