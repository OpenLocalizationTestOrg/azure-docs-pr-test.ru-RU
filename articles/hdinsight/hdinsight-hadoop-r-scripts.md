---
title: "aaaUse R в кластерах HDInsight toocustomize - Azure | Документы Microsoft"
description: "Узнайте, как tooinstall R с помощью сценария действия и использования R в кластерах HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>Установка и использование R на кластерах HDInsight Hadoop

Узнайте, как toocustomize Windows на основе кластеров HDInsight с R, с помощью действия скрипта и как кластеры toouse R в HDInsight. Hello [HDInsight предложения](https://azure.microsoft.com/pricing/details/hdinsight/) включает R Server как часть кластера HDInsight. Это позволяет R-скриптов toouse MapReduce и Spark toorun распределенных вычислений. Дополнительные сведения см. в статье [Приступая к работе с R Server в HDInsight](hdinsight-hadoop-r-server-get-started.md). Сведения об использовании R с кластером под управлением Linux см. в статье [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md) (Установка и использование R в кластерах HDInsight Hadoop (Linux)).

R можно установить в кластере любого типа (Hadoop, Storm, HBase, Spark) в HDInsight в Azure, воспользовавшись *Действием сценария*. Образец сценария tooinstall R в кластере HDInsight доступна из большого двоичного объекта хранилища Azure только для чтения в [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**Связанные статьи**

* [Установка и использование R на кластерах HDInsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md) — общие сведения о создании кластеров HDInsight.
* [Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.
* [Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>Что такое R
Hello <a href="http://www.r-project.org/" target="_blank">проект R для статистических вычислений</a> языка с открытым исходным и среды для статистических вычислений. R предоставляет сотни встраиваемых статистических функций и собственный язык программирования, который сочетает аспекты функционального и объектно-ориентированного программирования. Этот проект также обеспечивает обширные графические возможности. R — hello предпочтительный программирования среда профессиональные статистике и специалистов по анализу в самых разнообразных поля.

R совместим с хранилищем больших двоичных объектов Azure (WASB). Это дает возможность обрабатывать находящиеся там данные, используя R в HDInsight.  

## <a name="install-r"></a>Установка R
Объект [пример сценария](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R в кластере HDInsight доступна только для чтения больших двоичных объектов в хранилище Azure. Этот раздел содержит инструкции о как toouse hello образец скрипта при создании кластера hello, с помощью портала Azure hello.

> [!NOTE]
> Пример сценария Hello впервые появилась в кластер HDInsight версии 3.1. Дополнительные сведения о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)
>
>

1. При создании кластера HDInsight из hello портала щелкните **необязательная конфигурация**и нажмите кнопку **действия скрипта**.
2. На hello **действия скрипта** введите hello следующие значения:

    ![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize действия скрипта для использования кластера")

    <table border='1'>
        <tr><th>Свойство</th><th>Значение</th></tr>
        <tr><td>Имя</td>
            <td>Например, укажите имя для действия сценария hello, <b>установить R</b>.</td></tr>
        <tr><td>URI-адрес сценария</td>
            <td>Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера, например, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Тип узла</td>
            <td>Укажите hello узлов, на которых выполняется скрипт настройки hello. Вы можете выбрать одно из трех значений: <b>Все узлы</b>, <b>Только головные узлы</b> или <b>Worker nodes only</b> (Только рабочие узлы).
        <tr><td>Параметры</td>
            <td>Укажите параметры hello, если это требуется для сценария hello. Тем не менее tooinstall hello скрипт R не требует параметров, поэтому это поле можно оставить пустым.</td></tr>
    </table>

    Можно добавить несколько компонентов несколько tooinstall действие сценария в кластере hello. После добавления скриптов hello щелкните toostart флажок hello установки кластера hello.

Также можно использовать tooinstall hello сценария R в HDInsight с помощью Azure PowerShell или hello HDInsight .NET SDK. Указания по выполнению этих процедур приведены ниже в этой статье.

## <a name="run-r-scripts"></a>Запуск сценариев R
В этом разделе описывает, как сценарий toorun R на hello Hadoop кластер с HDInsight.

1. **Создание кластера toohello подключения удаленного рабочего стола**: из hello портала, включить удаленный рабочий стол для кластера hello, созданные с помощью R установлен, а затем подключите toohello кластера. Инструкции см. в разделе [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Консоли откройте hello R**: hello R Установка помещает ссылку toohello R консоли на рабочем столе hello hello головного узла. Щелкните его tooopen hello R консоли.
3. **Запустить сценарий hello R**: hello R-сценарий можно запустить непосредственно из консоли hello R с вставкой, выбрав его и нажав клавишу ВВОД. Ниже приведен простой пример сценарий, который приводит к возникновению ошибки too100 чисел от 1 hello и затем умножает их на 2.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Hello первые две строки вызова hello RHadoop библиотек, которые устанавливаются вместе с R. hello последняя строка печатает hello результаты toohello консоли. Hello вывод должен выглядеть следующим образом:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Установка R с помощью Azure PowerShell
См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Hello образце показано, как tooinstall Spark с помощью Azure PowerShell. Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>Установка R с помощью пакета SDK для .NET
См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Hello образце показано, как tooinstall Spark с помощью пакета SDK для .NET "hello". Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>См. также
* [Установка и использование R на кластерах HDInsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md) — общие сведения о создании кластеров HDInsight.
* [Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.
* [Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md)
* [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. Пример действия сценария для установки Spark.
* [Установка и использование Giraph в HDInsight](hdinsight-hadoop-giraph-install.md) — пример действия скрипта для установки Giraph.
* [Установка и использование Solr на кластерах HDInsight Hadoop](hdinsight-hadoop-solr-install-linux.md) — пример действия скрипта для установки Solr.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
