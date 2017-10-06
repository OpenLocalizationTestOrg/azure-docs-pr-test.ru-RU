---
title: "aaaUse MapReduce и PowerShell со Hadoop - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse PowerShell tooremotely запуск заданий MapReduce с Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>Выполнение заданий MapReduce с помощью PowerShell с использованием Hadoop в HDInsight

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Этот документ содержит пример использования Azure PowerShell toorun задания MapReduce в Hadoop кластера HDInsight.

## <a id="prereq"></a>Предварительные требования

* **Кластер Azure HDInsight (Hadoop в HDInsight)**.

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* <seg>
  **Рабочая станция с Azure PowerShell**.</seg>

## <a id="powershell"></a>Выполнение задания MapReduce с помощью Azure PowerShell

Azure PowerShell предоставляет *командлеты* , которые позволяют выполнить tooremotely задания MapReduce в HDInsight. На внутреннем уровне это достигается с помощью вызовов REST слишком[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (ранее называвшиеся Templeton) под управлением hello кластера HDInsight.

Hello используются следующие командлеты для выполнения заданий MapReduce в удаленном кластере HDInsight.

* **AzureRmAccount входа**: tooyour Azure PowerShell выполняет проверку подлинности подписки Azure.

* **Новый AzureRmHDInsightMapReduceJobDefinition**: создает новый *определение задания* с помощью hello определенные сведения о MapReduce.

* **Начало AzureRmHDInsightJob**: отправляет tooHDInsight определение задания hello, запускает задание hello и возвращает *задания* объект, который может быть используется toocheck hello состояние задания hello.

* **Ожидание AzureRmHDInsightJob**: использует hello объекта toocheck hello состояния заданий hello задания. Он ожидает завершения задания hello или превышено время ожидания hello.

* **Get-AzureRmHDInsightJobOutput**: использовать tooretrieve hello выходные данные задания hello.

Hello следующие шаги показывают, как toouse toorun эти командлеты заданий в кластер HDInsight.

1. С помощью редактора, сохранить следующий код в виде hello **mapreducejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. Откройте новую командную строку **Azure PowerShell** . Изменить расположение каталогов toohello hello **mapreducejob.ps1** файла, а затем используйте следующий сценарий hello toorun hello:

        .\mapreducejob.ps1

    При запуске скрипта hello, появится для hello имя кластера HDInsight hello hello HTTPS/Admin учетной записи имя и пароль для hello кластера. Также может быть запросом tooauthenticate tooyour подписки Azure.

3. По завершении заданий hello появляется примерно toohello выходных данных после текста:

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    Это выходные данные показывают, заданием hello успешно завершена.

    > [!NOTE]
    > Если hello **ExitCode** представляет собой значение отличное от 0, в разделе [Устранение неполадок](#troubleshooting).

    В этом примере также хранит tooan файлы загружаются hello **output.txt** файл в каталоге hello при запуске сценария, hello.

### <a name="view-output"></a>Просмотр выходных данных

Откройте hello **output.txt** файла в текстовый редактор toosee hello слов и число созданных заданием hello.

> [!NOTE]
> Hello выходных файлов задания MapReduce являются неизменяемыми. Поэтому при повторном запуске этого образца, требуется имя hello toochange hello выходного файла.

## <a id="troubleshooting"></a>Устранение неполадок

Если данные не возвращаются при завершении задания hello, произошла ошибка во время обработки. tooview сведения об ошибке для данного задания, добавить hello, следующая команда toohello конец hello **mapreducejob.ps1** файл, сохраните его и затем снова запустите ее.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Этот командлет возвращает сведения hello, куда было записано tooSTDERR на сервере hello при выполнении задания hello и может помочь определить, почему происходит сбой задания hello.

## <a id="summary"></a>Сводка

Как видите, Azure PowerShell предоставляет простой способ toorun задания MapReduce на кластер HDInsight, состояние задания монитора hello и получить hello выход.

## <a id="nextsteps"></a>Дальнейшие действия

Общая информация о заданиях MapReduce в HDInsight:

* [Использование MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
