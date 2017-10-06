---
title: "кластеры aaaInstall и используйте Giraph на Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toocustomize HDInsight кластер с Giraph и как toouse Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Установка и использование Giraph в кластерах HDInsight под управлением Windows

Узнайте, как toocustomize Windows на основе кластеров HDInsight с Giraph, с помощью действия скрипта и как toouse Giraph tooprocess крупномасштабных диаграмм. Сведения об использовании Giraph с кластером под управлением Linux см. в статье [Установка Giraph в кластерах HDInsight Hadoop и использование Giraph для обработки диаграмм больших объемов](hdinsight-hadoop-giraph-install-linux.md).

> [!IMPORTANT]
> Hello шагов в этот документ корректно работать только с кластерами HDInsight под управлением Windows. Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Сведения о том, как tooinstall Giraph в кластере HDInsight под управлением Linux. в разделе [Giraph установить в кластерах HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).


Giraph можно установить в кластере любого типа (Hadoop, Storm, HBase, Spark) в HDInsight в Azure, воспользовавшись *действием скрипта*. Образец сценария tooinstall Giraph в кластере HDInsight доступна из большого двоичного объекта хранилища Azure только для чтения, в [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). Пример сценария Hello работает только с кластера HDInsight версии 3.1. Дополнительную информацию о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight](hdinsight-component-versioning.md).

**Связанные статьи**

* [Установка Giraph на кластерах HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.
* [Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.
* [Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-giraph"></a>Что такое Giraph?
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> дает graph tooperform обработки с помощью Hadoop и может использоваться с Azure HDInsight. Графы моделирования связей между объектами, например hello соединения между маршрутизаторами в больших сетях, как Интернет, hello или связи между пользователями в социальных сетях (который иногда ссылается tooas социального графа). Обработка Graph позволяет tooreason о hello связей между объектами в граф, такие как:

* определение потенциальных друзей на основе текущих взаимоотношений;
* Определение hello кратчайший маршрут между двумя компьютерами в сети.
* Вычисление ранга hello страницы веб-страниц.

## <a name="install-giraph-using-portal"></a>Установка Giraph с помощью портала
1. Начать создание кластера с помощью hello **НАСТРАИВАЕМОЕ создание** параметра, как описано в разделе [кластеров создать Hadoop в HDInsight](hdinsight-provision-clusters.md).
2. На hello **действия скрипта** страница приветствия мастера нажмите кнопку **добавьте действия скрипта** tooprovide сведений о hello действие скрипта, как показано ниже:

    ![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize действия скрипта для использования кластера")

    <table border='1'>
        <tr><th>Свойство</th><th>Значение</th></tr>
        <tr><td>Имя</td>
            <td>Укажите имя для действия сценария hello. Например, <b>Установка Giraph</b>.</td></tr>
        <tr><td>URI-адрес сценария</td>
            <td>Укажите сценарий toohello универсальный код ресурса (URI) hello, вызванный toocustomize hello кластера. Например, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i>.</td></tr>
        <tr><td>Тип узла</td>
            <td>Укажите hello узлов, на которых выполняется скрипт настройки hello. Вы можете выбрать одно из трех значений: <b>Все узлы</b>, <b>Только головные узлы</b> или <b>Worker nodes only</b> (Только рабочие узлы).
        <tr><td>Параметры</td>
            <td>Укажите параметры hello, если это требуется для сценария hello. сценарий Hello tooinstall Giraph параметры не требуются, поэтому это поле можно оставить пустым.</td></tr>
    </table>

    Можно добавить несколько компонентов несколько tooinstall действие сценария в кластере hello. После добавления скриптов hello, щелкните флажок toostart hello, для создания кластера hello.

## <a name="use-giraph"></a>Использование Giraph
Мы используем hello SimpleShortestPathsComputation пример toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> реализацию для обнаружения hello кратчайшего пути между объектами в граф. Используйте следующие шаги tooupload hello образец данных и hello образец JAR-файл, запустите задание, используя пример SimpleShortestPathsComputation hello и просмотр результатов hello hello.

1. Отправьте tooAzure файла данных образец хранилища больших двоичных объектов. На локальной рабочей станции создайте новый файл с именем **tiny_graph.txt**. Она должна содержать hello следующие строки:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Отправьте hello tiny_graph.txt файл toohello основного хранилища для кластера HDInsight. Дополнительные сведения о данных tooupload. в разделе [передать данные для заданий Hadoop в HDInsight](hdinsight-upload-data.md).

    Эти данные описывает связь между объектами в направленный граф, используя формат hello [источника\_идентификатор, источник\_значение, [[dest\_id], [edge\_значение],...]]. Каждая строка представляет взаимоотношение между объектом **source\_id** и одним или несколькими объектами **dest\_id**. Hello **edge\_значение** (или вес) можно рассматривать как стойкость hello или расстояние hello соединения между **source_id** и **dest\_идентификатор**.

    Рисования, используя значение hello (или вес) в качестве hello расстояния между объектами, hello выше данных может выглядеть следующим образом:

    ![tiny_graph.txt начерчен в виде кругов с линиями различной длины между](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Запустите пример SimpleShortestPathsComputation hello. Используйте следующий пример hello toorun командлетов Azure PowerShell с помощью файла tiny_graph.txt hello в качестве входных данных hello.

    > [!IMPORTANT]
    > Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г. шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.
    >
    > Выполните шаги hello в [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell. При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    В приведенном выше примере hello, замените **clustername** с hello имя кластера HDInsight с Giraph установлен.
3. Просмотр результатов hello. По завершении задания hello hello результаты будет храниться в двух файлах вывода в hello **wasb: / / / пример/out/shotestpaths** папки. Привет, называются **часть m 00001 было указано** и **часть m-00002**. Выполните следующие действия toodownload и просмотреть выходной hello hello.

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Это создаст hello **пример, выходные данные или shortestpaths** структуру каталогов в текущем каталоге hello на рабочей станции и toothat файлы расположения для загрузки hello два выходных данных.

    Используйте hello **Cat** командлет toodisplay hello содержимое файлов hello:

        Cat example/output/shortestpaths/part*

    Hello вывод должен выглядеть примерно следующие toohello:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    Пример SimpleShortestPathComputation Hello является жестко заданный toostart с Идентификатором 1 объекта и поиска hello кратчайший путь tooother объектов. Поэтому hello выходные данные должны читаться как `destination_id distance`, где расстояние — hello значение (или вес) границ hello пути между объектом с Идентификатором 1 и идентификатором hello объекта.

    Визуализация это, можно проверить результаты hello, проходящих hello кратчайшего пути между Идентификатором 1 и других объектов. Обратите внимание, что hello кратчайшего пути между 1 идентификатор и идентификатор 4 — 5. Это hello общее расстояние между <span style="color:orange">идентификатор 1 и 3</span>, а затем <span style="color:red">идентификатор 3 и 4</span>.

    ![Представление объектов в виде кругов с кратчайшими путями между ними](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Установка Giraph с помощью Azure PowerShell
См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Hello образце показано, как tooinstall Spark с помощью Azure PowerShell. Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>Установка Giraph с помощью пакета SDK для .NET
См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Hello образце показано, как tooinstall Spark с помощью пакета SDK для .NET "hello". Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="see-also"></a>См. также
* [Установка Giraph на кластерах HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.
* [Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.
* [Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).
* [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. Пример действия сценария для установки Spark.
* [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]. Пример действия сценария для установки R.
* [Установка и использование Solr на кластерах HDInsight Hadoop](hdinsight-hadoop-solr-install.md) — пример действия скрипта для установки Solr.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
