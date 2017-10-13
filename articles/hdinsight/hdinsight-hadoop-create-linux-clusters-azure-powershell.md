---
title: "Создание кластеров Hadoop с помощью PowerShell в Azure HDInsight | Документы Майкрософт"
description: "Узнайте, как создавать кластеры Hadoop, HBase, Storm или Spark на платформе Linux для HDInsight с помощью Azure PowerShell."
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
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 079a3d1c7f91477d641dbc65fe0f04e86a0dcd30
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Создание кластеров под управлением Linux в HDInsight с помощью Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell — это полнофункциональная среда сценариев, которую можно использовать для контроля и автоматизации развертывания и управления вашей рабочей нагрузкой в Microsoft Azure. В этой статье содержится информация о том, как создать кластер HDInsight под управлением Linux с помощью Azure PowerShell, а также приведен пример скрипта.

> [!NOTE]
> Оболочка Azure PowerShell доступна только для клиентов Windows. Если вы используете клиент Linux, Unix или Mac OS X, сведения об использовании интерфейса командной строки Azure для создания кластера см. в статье [Создание кластеров под управлением Linux в HDInsight с помощью Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем следовать инструкциям в этой статье, необходимо подготовить следующее.

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г. В описанных в этом документе инструкциях используются новые командлеты HDInsight, которые работают с Azure Resource Manager.
    >
    > Чтобы установить последнюю версию Azure PowerShell, выполните действия из статьи [Установка и настройка Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps). Если у вас есть сценарии, в которые нужно добавить новые командлеты, работающие с Azure Resource Manager, см. статью [Переход к средствам разработки на основе Azure Resource Manager для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="create-cluster"></a>Создание кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Для создания кластера HDInsight с помощью Azure PowerShell необходимо выполнить следующие процедуры:

* создание группы ресурсов Azure;
* Создание учетной записи хранения Azure
* Создание контейнера BLOB-объектов Azure
* Создание кластера HDInsight

Следующий сценарий демонстрирует создание нового кластера.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

Значения, указываемые для входа в кластер, используются для создания учетной записи пользователя Hadoop в кластере. Используйте эту учетную запись для подключения к службам, размещенным в кластере, например веб-интерфейсам пользователя или REST API.

Значения, указываемые для пользователя SSH, используются для создания пользователя SSH в кластере. Используйте эту учетную запись для запуска удаленного сеанса SSH в кластере и выполнения заданий. Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

> [!IMPORTANT]
> Если вы планируете использовать более 32 узлов рабочей роли (при создании кластера или в ходе масштабирования после создания кластера), для головного узла потребуется минимум 8-ядерный процессор и 14 ГБ ОЗУ.
>
> Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Операция создания кластера может занять до 20 минут.

## <a name="create-cluster-configuration-object"></a>Создание кластера: объект конфигурации

Можно также создать объект конфигурации HDInsight с помощью командлета `New-AzureRmHDInsightClusterConfig`. Затем можно изменить этот объект конфигурации, чтобы включить дополнительные параметры конфигурации для кластера. Наконец, используйте параметр `-Config` командлета `New-AzureRmHDInsightCluster`, чтобы использовать эту конфигурацию.

Приведенный ниже сценарий создает объект конфигурации для настройки R Server для типа кластера HDInsight. Конфигурация включает граничный узел, RStudio и дополнительную учетную запись хранения.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> Использование учетной записи хранения, расположение которой отличается от расположения кластера HDInsight, не поддерживается. При использовании этого примера создайте дополнительную учетную запись хранения в том же расположении, что и сервер.

## <a name="customize-clusters"></a>Настройка кластеров

* Ознакомьтесь с разделом [Настройка кластеров HDInsight с помощью службы начальной загрузки](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-the-cluster"></a>Удаление кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Устранение неполадок

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы успешно создали кластер HDInsight, обратитесь к следующим ресурсам, чтобы научиться с ним работать.

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
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)

