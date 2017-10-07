---
title: "кластеры Hadoop aaaCreate с помощью PowerShell, Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Hadoop, HBase, ураган или Spark кластеров в Linux для HDInsight с помощью Azure PowerShell."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Создание кластеров под управлением Linux в HDInsight с помощью Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell — это мощная среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления ими в Microsoft Azure рабочих нагрузок. Этот документ содержит сведения о как кластер toocreate HDInsight под управлением Linux с помощью Azure PowerShell. а также приведен пример скрипта.

> [!NOTE]
> Оболочка Azure PowerShell доступна только для клиентов Windows. Если вы используете клиент Linux, Unix или Mac OS X, см. раздел [создание кластера HDInsight под управлением Linux с помощью Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) сведения об использовании hello Azure CLI toocreate кластера.

## <a name="prerequisites"></a>Предварительные требования
Необходимо иметь следующие hello перед началом этой процедуры.

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г. шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.
    >
    > Выполните шаги hello в [установите Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello последнюю версию Azure PowerShell. При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.

## <a name="create-cluster"></a>Создание кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toocreate кластер HDInsight с помощью Azure PowerShell, необходимо выполнить hello следующих процедур:

* создание группы ресурсов Azure;
* Создание учетной записи хранения Azure
* Создание контейнера BLOB-объектов Azure
* Создание кластера HDInsight

Hello следующий сценарий демонстрирует, каким образом toocreate нового кластера:

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

Hello значения, указываемые для имени входа кластера hello: hello используется toocreate учетной записи пользователя Hadoop для кластера hello. С помощью этой учетной записи tooservices tooconnect, размещенных в кластере hello, например веб-интерфейсы пользователя или API REST.

значения Hello, указать для пользователя SSH hello, используется toocreate hello SSH пользователя для кластера hello. Этот метод следует использовать учетную запись toostart удаленный сеанс SSH на кластере hello и запуска заданий. Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.

> [!IMPORTANT]
> Если планируется toouse более 32 рабочих узлов (или при создании кластера масштабирования hello кластера после создания), необходимо также указать размер головного узла с по крайней мере 8 ядер, 14 ГБ ОЗУ.
>
> Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Он может занять toocreate минут too20 кластера.

## <a name="create-cluster-configuration-object"></a>Создание кластера: объект конфигурации

Можно также создать объект конфигурации HDInsight с помощью командлета `New-AzureRmHDInsightClusterConfig`. Затем можно изменить этот конфигурации объекта tooenable Дополнительные параметры конфигурации для кластера. Наконец, используйте hello `-Config` параметр hello `New-AzureRmHDInsightCluster` конфигурации hello toouse командлета.

Hello следующий скрипт создает tooconfigure объекта конфигурации сервера R на тип кластера HDInsight. Hello настройку граничного узла, RStudio и дополнительная учетная запись хранения.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> Использование учетной записи хранилища в другом месте, чем hello кластера HDInsight не поддерживается. При использовании в этом примере, создать hello дополнительная учетная запись хранения в hello местоположения сервера hello.

## <a name="customize-clusters"></a>Настройка кластеров

* Ознакомьтесь с разделом [Настройка кластеров HDInsight с помощью службы начальной загрузки](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Удалить кластер hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Устранение неполадок

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы успешно создали кластер HDInsight, используйте следующие ресурсы toolearn как hello toowork с кластером.

### <a name="hadoop-clusters"></a>Кластеры Hadoop

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Кластеры HBase

* [Начало работы с HBase в HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Разработка приложений Java для HBase в HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Кластеры Storm

* [Разработка приложений Java для Storm в HDInsight](hdinsight-storm-develop-java-topology.md)
* [Использование компонентов Python в Storm в HDInsight](hdinsight-storm-develop-python-topology.md)
* [Развертывание и мониторинг топологий с помощью Storm в HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Кластеры Spark

* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)

