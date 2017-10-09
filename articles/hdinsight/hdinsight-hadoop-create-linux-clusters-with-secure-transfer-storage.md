---
title: "кластер aaaCreate Hadoop с безопасной передачи учетных записей хранения в Azure HDInsight | Документы Microsoft"
description: "Дополнительные сведения, включение toocreate кластеров HDInsight с безопасной передачи учетных записей хранилища Azure."
keywords: hadoop getting started,hadoop linux,hadoop quickstart,secure transfer,azure storage account
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Создание кластера Hadoop с помощью учетных записей хранения с безопасной передачей в Azure HDInsight

Hello [Безопасная передача необходимые](../storage/common/storage-require-secure-transfer.md) функция усиливает hello безопасности вашей учетной записи хранилища Azure путем применения всех tooyour учетной записи запросов через безопасное соединение. Этот компонент hello wasbs схему и поддерживаются только версия кластера HDInsight 3.6 или более поздней версии. 

## <a name="prerequisites"></a>Предварительные требования
Для работы с этим руководством вам потребуется:

* **Подписка Azure**: toocreate свободного один месяц пробную учетную запись, Обзор слишком[azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Учетная запись хранения Azure с включенной безопасной передачей**. Hello инструкции см. в разделе [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) и [требуют безопасной передачи](../storage/common/storage-require-secure-transfer.md).
* **Контейнер больших двоичных объектов в учетной записи хранения hello**. 
## <a name="create-cluster"></a>Создание кластера

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


В этом разделе вы создадите в HDInsight кластер Hadoop, используя [шаблон Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Hello шаблон находится в [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). Знакомство с шаблонами Resource Manager не является обязательным для работы с этим руководством. Для других методов создания кластера и общие сведения о свойствах hello, используемые в этом учебнике, см. [HDInsight, создания кластеров](hdinsight-hadoop-provision-linux-clusters.md).

1. Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портал Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Выполните hello инструкции toocreate hello кластера с hello следующие характеристики: 

    - Укажите HDInsight версии 3.6.  версия по умолчанию Hello — 3.5. Требуется версия 3.6 или более новая.
    - Укажите учетную запись хранения с включенной безопасной передачей.
    - Используйте короткое имя для учетной записи хранения hello.
    - Учетная запись хранения hello и hello контейнер больших двоичных объектов необходимо создать заранее. 

    Hello инструкции см. в разделе [создать кластер](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

При использовании сценария действия tooprovide файлы конфигурации, необходимо использовать wasbs в hello следующие параметры:

- fs.defaultFS (core-site)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Добавление дополнительных учетных записей хранения

Существует несколько вариантов tooadd включены дополнительные безопасной передачи учетных записей хранения:

- Изменение шаблона диспетчера ресурсов Azure hello в последнем разделе hello.
- Создание кластера с помощью hello [портал Azure](https://portal.azure.com) и укажите связанной учетной записи хранения.
- Используйте сценарий действия tooadd дополнительных безопасной передачи включить существующий кластер HDInsight хранилища учетных записей tooan.  Дополнительные сведения см. в разделе [добавить дополнительное хранилище учетных записей tooHDInsight](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы изучили, как toocreate кластер HDInsight и включить безопасной передачи toohello учетные записи хранения.

toolearn Дополнительные сведения об анализе данных с HDInsight, см. следующие статьи hello.

* toolearn Подробнее об использовании Hive с HDInsight, включая как tooperform Hive запросы из Visual Studio, в разделе [используйте Hive с HDInsight][hdinsight-use-hive].
* использовать язык toolearn о Pig tootransform данных см. в разделе [использование Pig с HDInsight][hdinsight-use-pig].
* в разделе toolearn о MapReduce программы toowrite способом обработки данных в Hadoop, [используйте MapReduce с HDInsight][hdinsight-use-mapreduce].
* в разделе toolearn об использовании hello средства HDInsight для Visual Studio tooanalyze данных на HDInsight, [приступить к работе со средствами Visual Studio Hadoop для HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Дополнительные сведения о хранением данных HDInsight toolearn или tooget данных в HDInsight, в статье hello в следующих статьях:

* Сведения о том, как HDInsight использует службу хранилища Azure, см. в статье [Использование HDFS-совместимой службы хранилища с Hadoop в HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Сведения о том, как tooHDInsight tooupload данных, в разделе [отправить данные tooHDInsight][hdinsight-upload-data].

toolearn Дополнительные сведения о создании и управлении кластер HDInsight см. следующие статьи hello.

* toolearn об управлении кластера HDInsight под управлением Linux, в разделе [управления HDInsight кластеры, использующие Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn больше о параметрах hello, можно выбрать при создании кластера HDInsight, в разделе [Создание HDInsight в Linux с использованием пользовательских параметров](hdinsight-hadoop-provision-linux-clusters.md).
* Если вы знакомы с Linux и Hadoop, но хотите tooknow подробные сведения о Hadoop в hello HDInsight, см. раздел [работу с HDInsight в Linux](hdinsight-hadoop-linux-information.md). Эта статья содержит следующую информацию:
  
  * URL-адреса для служб, размещенных в кластере hello, например, Ambari и WebHCat
  * Hello расположение файлов Hadoop и примеры hello локальной файловой системе
  * Hello использование служб Azure хранилища (WASB) вместо HDFS в качестве хранилища данных по умолчанию hello

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


