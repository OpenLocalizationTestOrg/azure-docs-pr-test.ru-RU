---
title: "aaaInstall или обновить Mono на HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse конкретной версии моно с кластером HDInsight. Моно — используется toorun приложений .NET в кластерах HDInsight под управлением Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a>Установка или обновление Mono в HDInsight

Узнайте, как tooinstall конкретную версию из [моно](https://www.mono-project.com) на HDInsight 3.4 или более поздней версии.

Моно установлена в HDInsight 3.4 и выше и используется toorun приложений .NET. Сведения о версии hello Mono, входящий в состав каждой версии HDInsight см. в разделе [управление версиями компонента HDInsight](hdinsight-component-versioning.md). tooinstall другой версии в кластере, используйте действие скрипта hello в этом документе. 

## <a name="how-it-works"></a>Принцип работы

Этот сценарий принимает hello следующий параметр:

* __Номер версии моно__: hello версии моно tooinstall. Hello версии должны быть доступны из [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

Hello скрипт устанавливает следующие пакеты моно hello:

* __mono-complete__;

* __ca-certificates-mono__.

## <a name="hello-script"></a>сценарий Hello

__Расположение скрипта:__ [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Требования__

* сценарий Hello должен применяться hello __head узлы__ и __рабочих узлов__.

## <a name="toouse-hello-script"></a>сценарий toouse hello

Сведения о toouse этот сценарий с HDInsight, в статье hello [HDInsight под управлением Linux, настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) документа. Можно использовать сценарий hello hello портал Azure, Azure PowerShell или hello Azure CLI.

Во время следующих hello документ действие скрипта, используйте hello, следующий URI:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> При настройке HDInsight с помощью этого сценария необходимо пометить hello скрипта как __Persisted__. Этот параметр позволяет HDInsight tooapply hello скрипт tooworker узлы, добавленные с помощью операции масштабирования.


## <a name="next-steps"></a>Дальнейшие действия

Вы узнали, как tooupgrade или установить определенную версию Mono на HDInsight. См. Дополнительные сведения об использовании приложений .NET с моно на HDInsight hello следующие документы:

* [Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md);
* [Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md);
* [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md);
* [Перенос решений .NET на основе tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Дополнительные сведения об использовании действий скрипта см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).