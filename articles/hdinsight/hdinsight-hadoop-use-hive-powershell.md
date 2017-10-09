---
title: "aaaUse Hadoop Hive с помощью PowerShell в HDInsight — Azure | Документы Microsoft"
description: "Использование запросов Hive toorun PowerShell в Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a>Выполнение запросов Hive с помощью PowerShell
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Этот документ содержит пример использования Azure PowerShell hello группы ресурсов Azure toorun Hive в запросы в режиме в кластере HDInsight Hadoop.

> [!NOTE]
> Этот документ не предоставляет подробное описание действий hello HiveQL инструкции, которые используются в примерах hello. Сведения о hello HiveQL, используемый в этом примере в разделе [используйте Hive в с Hadoop в HDInsight](hdinsight-use-hive.md).

**Предварительные требования**

* **Кластер Azure HDInsight**: он не имеет значения, является ли hello кластера Windows или Linux.

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Рабочая станция с Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Выполнение запросов Hive с помощью Azure PowerShell

Azure PowerShell предоставляет *командлеты* , которые позволяют запустить tooremotely запросов Hive в HDInsight. На внутреннем уровне командлеты hello вызовов REST слишком[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) в кластере HDInsight hello.

Hello следующие командлеты используются при выполнении запросов Hive в удаленном кластере HDInsight.

* **Добавить AzureRmAccount**: tooyour Azure PowerShell выполняет проверку подлинности подписки Azure
* **Новый AzureRmHDInsightHiveJobDefinition**: создает *определение задания* с помощью hello указан операторы HiveQL
* **Начало AzureRmHDInsightJob**: отправляет tooHDInsight определение задания hello, запускает задание hello и возвращает *задания* объект, который может быть используется toocheck hello состояние задания hello
* **Ожидание AzureRmHDInsightJob**: использует hello объекта toocheck hello состояния заданий hello задания. Он ожидает завершения задания hello или превышено время ожидания hello.
* **Get-AzureRmHDInsightJobOutput**: использовать tooretrieve hello выходные данные задания hello
* **Вызвать AzureRmHDInsightHiveJob**: использовать операторы HiveQL toorun. Этот командлет блоки hello запрос завершается, а затем возвращает результаты hello
* **Используйте AzureRmHDInsightCluster**: наборы hello текущего кластера toouse для hello **Invoke AzureRmHDInsightHiveJob** команды

Hello следующие шаги показывают, как toouse toorun эти командлеты заданий в кластере HDInsight:

1. С помощью редактора, сохранить следующий код в виде hello **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Откройте новую командную строку **Azure PowerShell** . Изменить расположение каталогов toohello hello **hivejob.ps1** файла, а затем используйте следующий сценарий hello toorun hello:

        .\hivejob.ps1

    При запуске сценария hello их запрашиваемые tooenter hello кластера имя и hello HTTPS или учетных данных администратора для кластера hello. Также может быть запросом toolog в tooyour подписки Azure.

3. По завершении заданий hello возвращается toohello аналогичные сведения, следуя thext:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Как упоминалось ранее, **Invoke-Hive** можно использовать toorun запроса и ожидать ответа hello. Используйте следующий сценарий toosee, как работает Invoke-Hive hello.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    Hello вывод выглядит следующим образом после текста hello.

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Hello Azure PowerShell можно использовать для более длинных запросов HiveQL **Here-строках** командлета или HiveQL файлы сценариев. Привет, в следующем фрагменте кода показан способ toouse hello **Invoke-Hive** командлет toorun HiveQL файла скрипта. Hello HiveQL, файл сценария должен быть отправлен toowasb: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Дополнительные сведения о командлете **Here-Strings** см. <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">здесь</a>.

## <a name="troubleshooting"></a>Устранение неполадок

Если данные не возвращаются при завершении задания hello, произошла ошибка во время обработки. tooview сведения об ошибке для данного задания, добавить hello следующему toohello конца hello **hivejob.ps1** файл, сохраните его и затем снова запустите ее.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Этот командлет возвращает hello информации, которая записывается tooSTDERR на сервере hello при выполнении задания hello.

## <a name="summary"></a>Сводка

Как видите, Azure PowerShell предоставляет простой способ toorun запросов Hive в кластер HDInsight, монитор hello состояние задания и получение выходных данных hello.

## <a name="next-steps"></a>Дальнейшие действия

Общая информация о Hive в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)
