---
title: "Действие сценария aaaUse tooinstall Solr в кластере Hadoop - Azure | Документы Microsoft"
description: "Узнайте, как toocustomize HDInsight кластер с Solr, с помощью действия сценария."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Установка и использование Solr в кластерах HDInsight под управлением Windows

Узнайте, как кластер toocustomize HDInsight под управлением Windows с Solr, с помощью действия скрипта и как toouse Solr toosearch данных.

> [!IMPORTANT]
> Hello шагов в этот документ корректно работать только с кластерами HDInsight под управлением Windows. Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Сведения об использовании Solr с кластером под управлением Linux см. в статье [Установка и использование Solr на кластерах HDInsight Hadoop](hdinsight-hadoop-solr-install-linux.md).


Solr можно установить в кластере любого типа (Hadoop, Storm, HBase, Spark) в HDInsight в Azure, воспользовавшись *Действием сценария*. Образец сценария tooinstall Solr в кластере HDInsight доступна из большого двоичного объекта хранилища Azure только для чтения, в [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

Пример сценария Hello работает только с кластера HDInsight версии 3.1. Дополнительную информацию о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight](hdinsight-component-versioning.md).

Пример сценария Hello, используемые в данном разделе создается кластер Solr под управлением Windows с указанной конфигурацией. Если требуется кластер Solr hello tooconfigure с различными коллекциями, сегментами, схемы, реплики, т. д., следует изменить скрипт hello и Solr двоичные файлы соответствующим образом.

**Связанные статьи**

* [Установка и использование Solr в кластерах HDInsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.
* [Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.
* [Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-solr"></a>Что такое Solr?
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> — это корпоративная платформа поиска, предоставляющая многофункциональные инструменты полнотекстового поиска данных. Хотя Hadoop позволяет хранения и управления огромный объем данных, Apache Solr предоставляет возможности поиска hello tooquickly извлекать данные hello.

## <a name="install-solr-using-portal"></a>Установка Solr с помощью портала
1. Начать создание кластера с помощью hello **НАСТРАИВАЕМОЕ создание** параметра, как описано в разделе [кластеров создать Hadoop в HDInsight](hdinsight-provision-clusters.md).
2. На hello **действия скрипта** страница приветствия мастера нажмите кнопку **добавьте действия скрипта** tooprovide сведений о hello действие скрипта, как показано ниже:

    ![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize действия скрипта для использования кластера")

    <table border='1'>
        <tr><th>Свойство</th><th>Значение</th></tr>
        <tr><td>Имя</td>
            <td>Укажите имя для действия сценария hello. Например, <b>Установить Solr</b>.</td></tr>
        <tr><td>URI-адрес сценария</td>
            <td>Укажите сценарий toohello универсальный код ресурса (URI) hello, вызванный toocustomize hello кластера. Например, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>.</td></tr>
        <tr><td>Тип узла</td>
            <td>Укажите hello узлов, на которых выполняется скрипт настройки hello. Вы можете выбрать одно из трех значений: <b>Все узлы</b>, <b>Только головные узлы</b> или <b>Worker nodes only</b> (Только рабочие узлы).
        <tr><td>Параметры</td>
            <td>Укажите параметры hello, если это требуется для сценария hello. сценарий Hello tooinstall Solr параметры не требуются, поэтому это поле можно оставить пустым.</td></tr>
    </table>

    Можно добавить несколько компонентов несколько tooinstall действие сценария в кластере hello. После добавления скриптов hello, щелкните флажок toostart hello, для создания кластера hello.

## <a name="use-solr"></a>Использование Solr
Необходимо начать с индексирования системой Solr нескольких файлов данных. Затем можно использовать запросы поиска toorun Solr hello индексированных данных. Выполните следующие шаги toouse Solr в кластер HDInsight hello.

1. **Использовать протокол удаленного рабочего стола (RDP) tooremote в кластер HDInsight hello с Solr установлен**. Из hello портал Azure необходимо включите удаленный рабочий стол для кластера hello, созданного с помощью Solr hello установлены и затем удаленный в кластер. Инструкции см. в разделе [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Выполните индексирование Solr, передав файлы данных**. Если индексируются Solr, в него, может понадобиться toosearch поместить документы. tooindex Solr tooremote использования RDP в кластер hello перейдите toohello рабочего стола, откройте hello Hadoop командной строки и перейдите в слишком**C:\apps\dist\solr-4.7.2\example\exampledocs**. Выполните следующую команду hello.

        java -jar post.jar solr.xml monitor.xml

    Вы увидите hello после вывода на консоль hello:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Программа Hello post.jar индексирует Solr с два образца документов **solr.xml** и **monitor.xml**. Программа post.jar Hello и документы образец hello доступные при установке Solr.
3. **Используйте hello Solr мониторинга toosearch внутри hello индексированных документов**. В toohello сеанс RDP hello HDInsight кластера, откройте Internet Explorer и запуска мониторинга Solr hello в **http://headnodehost:8983/solr / #/**. Из левой области hello из hello **селектор Core** раскрывающийся список, выберите **collection1**и в этот пункт **запроса**. Пример, tooselect и возвращают все документы hello в Solr, предоставляют hello следующие значения:

   * В hello **q** текста введите  **\*:**\*. Это будет возвращать все документы hello, которые индексируются в Solr. Если требуется toosearch конкретную строку в документах hello, можно ввести здесь строку.
   * В hello **wt** текстовое поле, выберите hello выходной формат. По умолчанию используется **JSON**. Щелкните **Выполнить запрос**.

     ![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "запуска запроса на панели мониторинга Solr")

     выходные данные Hello возвращает hello два документа, мы использовали для индексирования Solr. выходные данные Hello аналогичные hello ниже:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **Рекомендуется: Резервное копирование hello индексированных данных из Solr tooAzure хранилища больших двоичных объектов, связанных с кластером HDInsight hello**. В хорошей практикой должны резервные копии hello индексированных данных из узлов кластера Solr hello в хранилище больших двоичных объектов Azure. Выполните hello, поэтому следующие шаги toodo.

   1. Hello сеансу удаленного рабочего СТОЛА откройте Internet Explorer и toohello точки URL-адреса:

           http://localhost:8983/solr/replication?command=backup

       Вы должны получить примерно следующий ответ:

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. В удаленном сеансе hello, перейдите слишком {SOLR_HOME}\{коллекции} \data. Для кластера hello, созданные с помощью сценария образец hello, это должен быть **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. В этом месте должна появиться папка моментальных снимков, созданные с именем аналогичные слишком**моментальных снимков.* Отметка времени***.
   3. ZIP-папка моментальных снимков hello и отправьте его tooAzure хранилища больших двоичных объектов. Из командной строки Hadoop hello перейти toohello расположение папки моментальных снимков hello, используя hello следующую команду:

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       Эта команда копии данных моментального снимка слишком/пример/hello/контейнере hello в по умолчанию hello хранилища учетной записи связанного с кластером hello.

## <a name="install-solr-using-aure-powershell"></a>Установка Solr с помощью Azure PowerShell
См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Hello образце показано, как tooinstall Spark с помощью Azure PowerShell. Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>Установка Solr с помощью пакета SDK для .NET
См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Hello образце показано, как tooinstall Spark с помощью пакета SDK для .NET "hello". Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>См. также
* [Установка и использование Solr в кластерах HDInsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.
* [Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.
* [Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).
* [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. Пример действия сценария для установки Spark.
* [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]. Пример действия сценария для установки R.
* [Установка и использование Giraph в HDInsight](hdinsight-hadoop-giraph-install.md) — пример действия скрипта для установки Giraph.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
