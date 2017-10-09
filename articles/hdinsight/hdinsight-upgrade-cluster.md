---
title: "Новая версия кластера HDInsight tooa aaaUpgrade-Azure | Документы Microsoft"
description: "Узнайте, как tooUpgrade HDInsight кластера tooa более новой версии."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>Обновление кластера tooa более новой версии HDInsight
преимущества tootake Здравствуйте компонентам последней версии HDInsight, мы рекомендуем использовать обновленный toolatest версия кластеров HDInsight. Выполните hello ниже рекомендации tooupgrade версий кластера HDInsight.

> [!NOTE]
> Поддержка кластеров HDInsight версий 3.2 и 3.3 скоро завершится. См. дополнительные сведения о [версиях компонентов HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).
>
>

## <a name="upgrade-tasks"></a>Задачи обновления
рабочий процесс tooupgrade Hello кластера HDInsight выглядит следующим образом.

![Схема рабочего процесса](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. Прочитайте каждый раздел этого документа toounderstand изменения, которые могут потребоваться при обновлении кластера HDInsight.
2. Создайте кластер как среду тестирования и контроля качества. Дополнительные сведения о создании кластера см. в разделе [узнать, как toocreate HDInsight под управлением Linux кластеров](hdinsight-hadoop-provision-linux-clusters.md)
3. Копирование существующих заданий, источники данных и приемники toohello новой среды. В разделе [tooTest копирование данных среды](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) для получения дополнительных сведений.
4. Выполните Проверочное тестирование toomake убедиться, что заданиям работать должным образом на новый кластер hello.


После проверки того, что все работает правильно, необходимо запланируйте время простоя для миграции hello. Во время этого простоя hello следующие действия:

1.  Создайте резервную копию временные данные, хранящиеся локально на узлах кластера hello. Например, к ним могут относиться данные, которые хранятся непосредственно на головном узле.
2.  Удалите существующий кластер hello.
3.  Создание кластера hello же виртуальной сети подсеть с последней (или не поддерживаются) HDI версии с помощью hello одно хранилище данных по умолчанию, hello предыдущего кластера. Это позволяет hello нового кластера toocontinue работать с существующие рабочих данных.
4.  Импортируйте все временные данные из резервной копии.
5.  Запуск заданий и продолжить обработку с помощью нового кластера hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Узнайте, как toocreate HDInsight под управлением Linux кластеров](hdinsight-hadoop-provision-linux-clusters.md)
* [Подключиться с помощью SSH tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Выполняйте управление кластером под управлением Linux с помощью Ambari](hdinsight-hadoop-manage-ambari.md)

