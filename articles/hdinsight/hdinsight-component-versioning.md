---
title: "aaaHadoop компоненты и их версии - Azure HDInsight | Документы Microsoft"
description: "Узнайте hello Hadoop компоненты и их версии в HDInsight и hello уровни обслуживания, доступных в этом распространяемом облачной платформы Hortonworks данных."
keywords: "версии hadoop, компоненты экосистемы hadoop, компонентов hadoop, как toocheck версии hadoop"
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Что такое компоненты Hadoop hello и доступны с HDInsight версии?

Дополнительные сведения о hello Apache Hadoop экосистема компоненты и их версии в Microsoft Azure HDInsight, а также hello уровней обслуживания Standard и Premium. Кроме того, узнайте, как версий компонента toocheck Hadoop в HDInsight. 

Каждая версия HDInsight является облачной реализацией версии платформы данных Hortonworks Data Platform (HDP).

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>Компоненты Hadoop, доступные в разных версиях HDInsight
Azure HDInsight поддерживает несколько версий кластера Hadoop, которые могут быть развернуты в любое время. Выбор версии создает конкретной версии распространения HDP hello и набор компонентов, содержащихся в этой. Начиная с 17 февраля 2017 г. используемые Azure HDInsight версия кластера по умолчанию hello 3.5 и основанное на HDP 2.5.

в hello в следующей таблице перечислены версии компонента Hello, связанные с версиями кластеров HDInsight. 

> [!NOTE]
> версия по умолчанию Hello для hello службы HDInsight могут изменяться без предварительного уведомления. Если у вас есть зависимость версии, укажите версию HDInsight hello, при создании кластеров с помощью пакета SDK для .NET с помощью Azure PowerShell и Azure CLI hello.

| Компонент | HDInsight 3.6 (по умолчанию) | HDInsight 3.5 | HDInsight 3.4 | HDInsight 3.3 | HDInsight 3.2 | HDInsight 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2,0 |
| Apache Hadoop и YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive и HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache Ranger | 0.7.0 |0.6.0 |-|-|-|-|-|
| Apache HBase |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0 (только для Linux) |1.6.2 + 2.0 (только для Linux) |1.6.0 (только для Linux) |1.5.2 (только для экспериментальной сборки Linux) |1.3.1 (только для Windows) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>Проверка сведений о текущей версии компонентов Hadoop

с tooHDInsight обновления можно изменить компонент Hello Hadoop экосистема версии, связанные с версиями кластеров HDInsight. компоненты Hadoop toocheck hello и tooverify, какие версии, используемые для кластера, используют hello Ambari REST API. Hello **GetComponentInformation** команда извлекает сведения о компонентах службы. Дополнительные сведения см. в разделе hello [документации Ambari][ambari-docs].

Для кластеров Windows версия компонента toocheck hello другим способом является toolog tooa кластера с помощью удаленного рабочего стола и изучите содержимое hello hello C:\apps\dist\ каталога.

> [!IMPORTANT]
> Linux — hello только операционная система используется на HDInsight 3,4 или более поздней версии. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](#hdinsight-windows-retirement).

### <a name="release-notes"></a>Заметки о выпуске

В разделе [заметки о выпуске HDInsight](hdinsight-release-notes.md) дополнительные заметки о выпуске на последние версии HDInsight hello.

## <a name="supported-hdinsight-versions"></a>Поддерживаемые версии HDInsight
Hello следующей таблице перечислены версии hello hdinsight, доступных в настоящее время на hello портал Azure. версии HDP Hello, соответствующие версии HDInsight tooeach перечисляются вместе с даты выпуска продукта hello. даты окончания срока действия и прекращении работы поддержки Hello также предоставляются, когда они все известные.

> [!NOTE]
> После реализации поддержки истек срок действия версии, его могут оказаться недоступными через классический портал Microsoft Azure hello. Однако версии кластера по-прежнему доступно при использовании hello toobe `Version` параметр в Windows PowerShell hello [New AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) команды и hello .NET SDK до версии hello даты прекращения использования.
> 
> Высокодоступные кластеры с двумя головными узлами развертываются по умолчанию для HDInsight версии 2.1 и более поздних. Они недоступны для кластеров HDInsight версии 1.6.

| Версия HDInsight | Версия HDP | ОС виртуальной машины | высокую доступность; | Дата выпуска | Доступность на hello портал Azure | Дата прекращения поддержки | Дата вывода |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3.6 |HDP 2.6 |Ubuntu 16 |Да |4 апреля 2017 г. |Да | | |
| HDInsight 3.5 |HDP 2.5 |Ubuntu 16 |Да |30 сентября 2016 г. |Да |5 сентября 2017 г. |31 мая 2018 г. |
| HDInsight 3.4 |HDP 2.4 |Ubuntu 14.0.4 LTS |Да |29 марта 2016 г. |Да |29 декабря 2016 г. |9 января 2018 г. |
| HDInsight 3.3 |HDP 2.3 |Windows Server 2012 R2 |Да |2 декабря 2015 г. |Да |27 июня 2016 г. |31 июля 2018 г. |
| HDInsight 3.3 |HDP 2.3 |Ubuntu 14.0.4 LTS |Да |2 декабря 2015 г. |Да |27 июня 2016 г. |31 июля 2017 г. |
| HDInsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS или Windows Server 2012 R2 |Да |18 февраля 2015 г. |Нет |1 марта 2016 г. |1 апреля 2017 г. |
| HDInsight 3.1 |HDP 2,1 |Windows Server 2012 R2 |Да |24 июня 2014 г. |Нет |18 мая 2015 г. |30 июня 2016 г. |
| HDInsight 3.0 |HDP 2,0 |Windows Server 2012 R2 |Да |11 февраля 2014 г. |Нет |17 сентября 2014 г. |30 июня 2015 г. |
| HDInsight 2.1 |HDP 1,3 |Windows Server 2012 R2 |Да |28 октября 2013 г. |Нет |12 мая 2014 г. |31 мая 2015 г. |
| HDInsight 1.6 |HDP 1.1 | |Нет |28 октября 2013 г. |Нет |26 апреля 2014 г. |31 мая 2015 г. |

## <a name="hdinsight-windows-retirement"></a>Дата вывода HDInsight под управлением Windows
Microsoft Azure HDInsight версии 3.3 была последней версии HDInsight, в Windows hello. Hello Дата вывода из эксплуатации для HDInsight в Windows — 31 июля 2018. Если у вас есть все кластеры HDInsight на Windows 3.3 или более ранней версии, необходимо перенести tooHDInsight в Linux (HDInsight версии 3.5 или более поздней версии) до 31 июля 2018. Миграция toohello ОС Linux обеспечивает возможность toocreate tooretain hello или изменить размер кластеров HDInsight. Срок действия поддержки для HDInsight версии 3.3 в Windows истек 27 июня 2016 г.

Начиная с версии 3.4 HDInsight, корпорация Майкрософт выпустила HDInsight только на hello ОС Linux. В результате некоторые компоненты hello в HDInsight, доступны для Linux только. Сюда входят Apache круг, Kafka, интерактивный Hive, Spark в HDInsight приложений и хранилище Озера данных Azure как hello первичной файловой системы. Будущие выпуски HDInsight доступны только в ОС Linux hello. Будущих выпусков HDInsight под управлением Windows не будет. 

## <a name="faqs"></a>Часто задаваемые вопросы

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>Что такое временная шкала hello для прекращения использования HDInsight в Windows
31 июля 2018, — hello наступления даты для HDInsight в Windows. Если планируется hello даты прекращения использования отличается для своего региона, вы получите уведомление отдельно. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>Что такое воздействие hello снятия с учета HDInsight в Windows для существующих клиентов?
После вывода HDInsight под управлением Windows вы больше не сможете создать кластер HDInsight под управлением Windows или изменить размер имеющегося. Срок действия поддержки HDInsight версии 3.3 истек 27 июня 2016 г. Таким образом поддержки или исправления ошибок для HDInsight 3.3 или более ранних версий не будет. Будущие выпуски HDInsight доступны только в ОС Linux hello. Будущих выпусков HDInsight под управлением Windows не будет.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>Какие версии HDInsight под управлением Windows будут затронуты?
Azure HDInsight версии 3.3 — последняя версия HDInsight для Windows hello. Перед Выбывает HDInsight в Windows, все окна HDInsight 3.3 или более ранней версии кластеров должны быть перенесены tooHDInsight в Linux версии 3.5 или более поздней версии. Миграция вашей tooHDInsight кластеров в Linux обеспечивает tooretain hello возможность toocreate новые кластеры или изменять размер существующих кластеров. 

### <a name="what-do-i-need-toodo"></a>Что делать мне toodo?
Перенос кластера HDInsight Linux tooa поддерживается кластеров HDInsight Windows до 31 июля 2018. Дополнительные сведения см. в разделе hello [документа миграции HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Дополнительные сведения о версиях Azure HDInsight см. в разделе список hello [поддерживаемые версии](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions). 

### <a name="where-do-i-find-hello-cluster-os-type"></a>Где найти тип ОС hello кластера?
В hello портал Azure, перейдите toohello страница обзора кластер HDInsight и найдите **кластера типа** под **Essentials**. на этой странице перечислены типы ОС кластера Hello. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>Не удается перенести tooan кластера HDInsight Linux по 31 июля 2018. Каково влияние hello toomy кластера HDInsight Windows?
Hello кластера HDInsight Windows выполняется как-, но нельзя создать новый кластер HDInsight Windows или изменения размера существующего кластера HDInsight Windows. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>Кластер имеет зависимость .NET. Как разрешить эту зависимость в Linux?
Можно разрешить зависимости кластеров Linux с помощью hello [моно проекта](http://www.mono-project.com/). Эта реализация с открытым исходным кодом .NET доступна для кластеров HDInsight под управлением Linux. Дополнительные сведения см. в разделе hello [документа миграции HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>Я новый клиент HDInsight под управлением Windows. Как создать кластер HDInsight под управлением Windows?
Начиная с 3 июля 2017 г. только имеющиеся клиенты HDInsight под управлением Windows могут создавать кластеры HDInsight. Новых клиентов не удается создать кластер HDInsight Windows в hello портал Azure с помощью PowerShell или hello SDK. Рекомендуется, чтобы новые клиенты создавали кластер HDInsight под управлением Linux. Существующие клиенты могут создавать новые окна HDInsight кластеры до hello HDInsight в Windows даты прекращения использования. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>Такое ценообразования влияния, связанной с перемещением из HDInsight на tooHDInsight Windows в Linux?
Нет, hello цены hello же для HDInsight в любой операционной системе. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>Каковы преимущества hello клиента, связанные с hello переместить tooonly с помощью HDInsight в Linux?
* Более быстрое время на рынок для открытой технологий больших данных через hello службы HDInsight
* Большое сообщество и экосистема, где можно получить поддержку.
* Возможность tooexercise активной разработке по hello откройте источник сообщества для Hadoop и другими технологиями большие наборы данных

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>Предоставляет ли HDInsight на Linux дополнительные функции, недоступные в HDInsight под управлением Windows?
Начиная с версии 3.4 HDInsight, корпорация Майкрософт выпустила HDInsight только на hello ОС Linux. В результате некоторые компоненты hello в HDInsight, доступны для Linux только. Сюда входят Apache круг, Kafka, интерактивный Hive, Spark в HDInsight приложений и хранилище Озера данных Azure как hello первичной файловой системы. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>Соглашение об уровне обслуживания (SLA) для версий кластера HDInsight
Hello соглашения об уровне обслуживания (SLA) определяется на основе _окно поддержки_. Поддержка окна Hello — hello период времени, версия кластера HDInsight поддерживается в службу технической поддержки и поддержки. Если версия hello имеет _поддерживают дату истечения срока действия_ , достиг, кластер HDInsight hello находится за пределами окна поддержки hello. Дополнительные сведения о поддерживаемых версиях см. в разделе список hello [поддерживаемые версии кластера HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Дата окончания срока действия поддержки Hello указанного HDInsight версии X (после доступна более новая версия X + 1) вычисляется как hello более поздних версий:  

* Формула 1: Добавьте дату toohello 180 дней после выпуска версия кластера HDInsight hello X.
* Формула 2: Добавьте дату toohello 90 дней, когда версия кластера HDInsight hello X + 1 доступны на портале Azure.

Hello _даты прекращения использования_ hello Дата, после чего hello версия кластера не удается создать на HDInsight. Начиная с 31 июля 2017 г. нельзя изменить размер кластера HDInsight после даты вывода. 

> [!NOTE]
> Кластеры HDInsight Windows (включая версии 2.1, 3.0, 3.1, 3.2 и 3.3) запустите семейство гостевых ОС Azure версии 4, который использует hello 64-разрядной версии Windows Server 2012 R2. Azure семейства гостевых ОС версии 4 поддерживает hello .NET Framework версии 4.0, 4.5, 4.5.1 и 4.5.2.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>Заметки о выпуске Hortonworks, связанные с версиями HDInsight

раздел Hello ссылки toorelease заметки для распределения платформы Hortonworks Data Platform hello и Apache компонентов, которые используются с HDInsight.
* Кластер HDInsight версии 3.6 использует дистрибутив Hadoop, основанный на платформе [Нortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html).
* Кластер HDInsight версии 3.5 использует дистрибутив Hadoop, основанный на платформе [Нortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html). Версия кластера HDInsight 3.5 — hello _по умолчанию_ кластера Hadoop, созданную в hello портал Azure.
* Кластер HDInsight версии 3.4 использует пакет Hadoop, построенный на платформе [Нortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html).
* Кластер HDInsight версии 3.3 использует пакет Hadoop, построенный на платформе [Нortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html).

  * [Заметки о выпуске Apache Storm](https://storm.apache.org/2015/11/05/storm0100-released.html) доступны на веб-сайте Apache hello.
  * [Заметки о выпуске Apache Hive](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) доступны на веб-сайте Apache hello.
* Кластер HDInsight версии 3.2 использует дистрибутив Hadoop, основанный на платформе [Нortonworks Data Platform 2.2][hdp-2-2].

  * Заметки о выпуске для отдельных компонентов Apache: [Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [Common](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112) и [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* Кластер HDInsight версии 3.1 использует дистрибутив Hadoop, основанный на платформе [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Кластеры HDInsight версии 3.1, созданные до 7 ноября 2014 г., основаны на платформе [Hortonworks Data Platform 2.1.1][hdp-2-1-1].
* Кластер HDInsight версии 3.0 использует дистрибутив Hadoop, основанный на платформе [Нortonworks Data Platform 2.0][hdp-2-0-8].
* Кластер HDInsight версии 2.1 использует дистрибутив Hadoop, основанный на платформе [Нortonworks Data Platform 1.3][hdp-1-3-0].
* Кластер HDInsight версии 1.6 использует дистрибутив Hadoop, основанный на платформе [Нortonworks Data Platform 1.1][hdp-1-1-0].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight "Стандартный" и HDInsight "Премиум"

Azure HDInsight представляет предложения облака hello большие наборы данных в двух категориях: _Стандартная_ и _Premium_. Hello следующей таблице перечислены возможности, доступные _только_ в HDInsight Premium. Компоненты, которые явно не описаны в таблице hello, доступны в HDInsight Standard и Premium.

> [!NOTE]
> Здравствуйте, HDInsight Premium предложения в настоящее время находится в предварительной версии и доступна только для кластеров Linux.

| Компонент HDInsight "Премиум" | Описание |
| --- | --- |
| Присоединенные к домену кластеры HDInsight |Присоединение доменов Active Directory (Azure AD) tooAzure кластеров HDInsight для безопасности на уровне предприятия. В расширенной версии HDInsight можно настроить список сотрудников из вашей организации, можно пройти проверку подлинности Azure AD toolog в кластере HDInsight tooan. Здравствуйте, администратор предприятия можно настроить управление доступом на основе ролей для куста безопасности с помощью [круг Apache](http://hortonworks.com/apache/ranger/) и ограничить доступ toouse данных только так. И, наконец Здравствуйте, администратор может аудита данным, доступным для сотрудников и tooaccess изменения управления политиками, таким образом, достигая высокую степень управления их корпоративных ресурсов. Дополнительные сведения см. в статье [Configure domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Настройка присоединенных к домену кластеров HDInsight). |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>Типы кластеров, поддерживаемые HDInsight уровня "Премиум"
Hello следующей таблице перечислены типы hello кластера, которые поддерживаются в HDInsight Premium.

| Тип кластера | Стандартная | Premium (предварительная версия) |
| --- | --- | --- |
| Hadoop |Да |Да (только HDInsight 3.6) |
| Spark |Да |Нет |
| HBase |Да |Нет |
| Storm |Да |Нет |
| R Server |Да |Нет |
| Interactive Hive (предварительная версия) |Да |Нет |
| Kafka (предварительная версия) |Да |Нет | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>Поддержка Azure Data Lake Store в HDInsight уровня "Премиум"

Кластеры HDInsight уровня "Премиум" не поддерживают использование Azure Data Lake Store в качестве основного хранилища. Однако Azure Data Lake Store по-прежнему можно использовать в качестве дополнительного хранилища в кластерах HDInsight уровня "Премиум".

### <a name="pricing-and-sla"></a>Цены и соглашение об уровне обслуживания
Сведения о ценах и соглашение об уровне обслуживания для категории HDInsight "Премиум" см. на странице [с ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>Конфигурация узлов и размеры виртуальных машин по умолчанию для кластеров
Здравствуйте, следующие размеры виртуальной машины (VM) по умолчанию hello список таблиц для кластеров HDInsight.

> [!IMPORTANT]
> Если в кластере требуется более 32 рабочих узлов, для головного узла следует выбрать размер с по крайней мере 8 ядрами и 14 ГБ ОЗУ.
> 
> 

* Все поддерживаемые регионы, кроме южной Бразилии и западной Японии:

  | Тип кластера | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | Головной узел: размер виртуальной машины по умолчанию |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | Головной узел: рекомендуемые размеры виртуальных машин |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |A3, A4, A5 |D12 v2, D13 v2, D14 v2 |D12 v2, D13 v2, D14 v2 |
  | Рабочая роль: размер виртуальной машины по умолчанию |D3 v2 |D3 v2 |D3 v2 |Windows: D12 v2; Linux: D4 v2 |Windows: D12 v2; Linux: D4 v2 |
  | Рабочая роль: рекомендуемые размеры виртуальных машин |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
  | ZooKeeper: размер виртуальной машины по умолчанию | |A3 |A2 | | |
  | ZooKeeper: рекомендуемые размеры виртуальных машин | |A3, A4, A5 |A2, A3, A4 | | |
  | Граничный узел: размер виртуальной машины по умолчанию | | | | |Windows: D12 v2; Linux: D4 v2 |
  | Граничный узел: рекомендуемый размер виртуальной машины | | | | |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
* Только южная Бразилия и западная Япония (нет размеров v2):

  | Тип кластера | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | Головной узел: размер виртуальной машины по умолчанию |D3 |D3 |A3 |D12 |D12 |
  | Головной узел: рекомендуемые размеры виртуальных машин |D3, D4, D12 |D3, D4, D12 |A3, A4, A5 |D12, D13, D14 |D12, D13, D14 |
  | Рабочая роль: размер виртуальной машины по умолчанию |D3 |D3 |D3 |Windows: D12; Linux: D4 |Windows: D12; Linux: D4 |
  | Рабочая роль: рекомендуемые размеры виртуальных машин |D3, D4, D12 |D3, D4, D12 |D3, D4, D12 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |
  | ZooKeeper: размер виртуальной машины по умолчанию | |A2 |A2 | | |
  | ZooKeeper: рекомендуемые размеры виртуальных машин | |A2, A3, A4 |A2, A3, A4 | | |
  | Граничный узел: размеры виртуальных машин по умолчанию | | | | |Windows: D12; Linux: D4 |
  | Граничный узел: рекомендуемые размеры виртуальных машин | | | | |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |

> [!NOTE]
> - HEAD называется *Nimbus* hello Storm кластера типа.
> - Работник называется *администратора* hello Storm кластера типа.
> - Работник называется *область* hello HBase кластера типа.

## <a name="next-steps"></a>Дальнейшие действия
- [Установка кластеров в HDInsight с использованием Hadoop, Spark, Kafka и других технологий](hdinsight-hadoop-provision-linux-clusters.md)
- [Работа в экосистеме Hadoop в HDInsight на компьютере с Windows](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
