---
title: "aaaUse Pig для Hadoop с помощью PowerShell в HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как кластера tooa задания Pig toosubmit Hadoop в HDInsight с помощью Azure PowerShell."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>Используйте задания Pig toorun Azure PowerShell с HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Этот документ содержит пример использования tooa задания Hadoop для Azure PowerShell toosubmit Pig в кластере HDInsight. Pig позволяет задания MapReduce toowrite языке (Pig латиница) моделирует преобразования данных, вместо сопоставления и уменьшения функции.

> [!NOTE]
> Этот документ не предоставляет подробное описание действий hello латиница Pig инструкций, используемых в примерах hello. Сведения о hello латиница Pig, используемых в этом примере содержатся [использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).

## <a id="prereq"></a>Предварительные требования

* **Кластер Azure HDInsight**.

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* <seg>
  **Рабочая станция с Azure PowerShell**.</seg>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>Выполнение заданий Pig с помощью PowerShell

Azure PowerShell предоставляет *командлеты* , которые позволяют tooremotely запуска задания Pig в HDInsight. На внутреннем уровне PowerShell использует вызовы REST слишком[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) работающих в кластере HDInsight hello.

Hello используются следующие командлеты для выполнения заданий Pig на удаленный кластер HDInsight:

* **AzureRmAccount входа**: tooyour Azure PowerShell выполняет проверку подлинности подписки Azure
* **Новый AzureRmHDInsightPigJobDefinition**: создает *определение задания* с помощью hello указан инструкций Латинская Pig
* **Начало AzureRmHDInsightJob**: отправляет tooHDInsight определение задания hello, запускает задание hello и возвращает *задания* объект, который может быть используется toocheck hello состояние задания hello
* **Ожидание AzureRmHDInsightJob**: использует hello объекта toocheck hello состояния заданий hello задания. Он ожидает завершения задания hello или превышения времени ожидания hello.
* **Get-AzureRmHDInsightJobOutput**: использовать tooretrieve hello выходные данные задания hello

Hello следующие шаги показывают, как toouse toorun эти командлеты заданий в кластере HDInsight.

1. С помощью редактора, сохранить следующий код в виде hello **pigjob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. Откройте командную строку Windows PowerShell. Изменить расположение каталогов toohello hello **pigjob.ps1** файла, а затем используйте следующий сценарий hello toorun hello:

        .\pigjob.ps1

    Все запрашиваемые toolog в tooyour подписки Azure. После этого появится для hello HTTPs/Admin учетную запись и пароль для кластера HDInsight hello.

2. После завершения задания hello, он должен возвращать сведения аналогичные toohello следующий текст:

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>Устранение неполадок

Если данные не возвращаются при завершении задания hello, произошла ошибка во время обработки. tooview сведения об ошибке для данного задания, добавить hello, следующая команда toohello конец hello **pigjob.ps1** файл, сохраните его и затем снова запустите ее.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

Возвращает сведения hello, куда было записано tooSTDERR на сервере hello при выполнении задания hello и может помочь определить, почему происходит сбой задания hello.

## <a id="summary"></a>Сводка
Как видите, Azure PowerShell предоставляет toorun простой способ задания Pig в кластер HDInsight, состояние задания монитора hello и получить hello выход.

## <a id="nextsteps"></a>Дальнейшие действия
Общая информация о Pig в HDInsight:

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)
