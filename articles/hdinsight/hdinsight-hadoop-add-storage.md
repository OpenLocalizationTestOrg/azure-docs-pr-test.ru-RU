---
title: "дополнительное хранилище Azure aaaAdd учетные записи tooHDInsight | Документы Microsoft"
description: "Узнайте, как дополнительное хранилище Azure tooadd учетные записи tooan существующего кластера HDInsight."
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
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a>Добавить дополнительное хранилище учетных записей tooHDInsight

Узнайте, как tooHDInsight учетные записи toouse сценария действия tooadd дополнительных хранилища Azure. Hello в данном пошаговом руководстве Добавление существующего кластера HDInsight под управлением Linux хранилища учетной записи tooan.

> [!IMPORTANT]
> в этом документе сведения Hello содержит сведения о добавлении кластера tooa дополнительное хранилище, после его создания. Сведения о добавлении учетных записей хранения во время создания кластера см. в статье о [настройке кластеров HDInsight с Hadoop, Spark, Kafka и другими платформами](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="how-it-works"></a>Принцип работы

Этот сценарий принимает следующие параметры hello:

* __Имя учетной записи хранилища Azure__: hello имя кластера HDInsight tooadd toohello hello хранилища учетной записи. После выполнения сценария hello, HDInsight может считывать и записывать данные, хранящиеся в этой учетной записи хранения.

* __Ключ учетной записи хранилища Azure__: ключ, который предоставляет учетной записи хранилища toohello доступа.

* __-p__ (необязательно): Если указано, hello ключ не зашифрован и хранится в файле core-site.xml hello как обычный текст.

Во время обработки hello сценарий выполняет hello, следующие действия:

* Если hello учетной записи хранения уже существует в конфигурации кластера hello core-site.xml hello, hello скрипт завершается, и дальнейшие действия не выполняются.

* Проверяет, существует hello учетной записи хранилища и может осуществляться с помощью ключа hello.

* Шифрует ключ hello, с помощью учетных данных кластера hello.

* Добавление файла core-site.xml toohello учетной записи хранения hello.

* Останавливает и перезапускает службы hello Oozie, YARN, MapReduce2 и HDFS. Остановка и запуск этих служб позволяет им toouse hello новой учетной записи хранения.

> [!WARNING]
> Использование учетной записи хранилища в другом месте, чем hello кластера HDInsight не поддерживается.

## <a name="hello-script"></a>сценарий Hello

__Расположение скрипта__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__Требования__

* сценарий Hello должен применяться hello __Head узлы__.

## <a name="toouse-hello-script"></a>сценарий toouse hello

Этот скрипт можно использовать из hello портал Azure, Azure PowerShell или hello Azure CLI 1.0. Дополнительные сведения см. в разделе hello [HDInsight под управлением Linux, настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) документа.

> [!IMPORTANT]
> При использовании hello шаги, описанные в документе настройки hello, используйте следующие сведения tooapply hello этот скрипт:
>
> * Замените любой URI действия сценария пример hello URI для этого скрипта (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).
> * Замените любые параметры пример hello имя учетной записи хранилища Azure и ключ кластера добавлены toohello toobe учетной записи хранилища hello. Если с помощью hello портал Azure, эти параметры должны быть разделены пробелом.
> * Нет необходимости toomark этот скрипт как __Persisted__, как его непосредственно обновляет конфигурацию Ambari hello hello кластера.

## <a name="known-issues"></a>Известные проблемы

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Учетные записи хранения не отображаются на портале Azure или в Azure Tools

После просмотра hello HDInsight кластер в hello портал Azure, при выборе hello __учетные записи хранения__ запись в __свойства__ не отображает учетные записи хранения, добавляемые с помощью этого действия сценария. Azure PowerShell и Azure CLI не отображают hello дополнительная учетная запись хранения либо.

данные хранилища Hello не отображается, поскольку скрипт hello только изменяет hello core-site.xml конфигурации для кластера hello. Эта информация не используется при получении сведений о hello кластера с помощью API управления Azure.

сведения об учетной записи хранилища tooview добавлен toohello кластера, с помощью этого сценария, используйте hello Ambari REST API. Используйте следующие команды tooretrieve hello эту информацию для кластера:

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> Задать `$clusterName` toohello имя кластера HDInsight hello. Задать `$storageAccountName` toohello имя учетной записи хранения hello. При появлении запроса введите имя кластера hello (администратор) и пароль.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> Задать `$PASSWORD` пароль учетной записи входа (администратор) toohello кластера. Задать `$CLUSTERNAME` toohello имя кластера HDInsight hello. Задать `$STORAGEACCOUNTNAME` toohello имя учетной записи хранения hello.
>
> В этом примере используется [curl (http://curl.haxx.se/)](http://curl.haxx.se/) и [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve и синтаксический анализ данных JSON.

При использовании этой команды, замените __CLUSTERNAME__ с именем hello hello кластера HDInsight. Замените __пароль__ с hello HTTP пароль имени входа для hello кластера. Замените __STORAGEACCOUNT__ с именем hello учетной записи хранения hello, добавленные с помощью действия сценария. Эта команда возвращает сведения о появится примерно toohello следующий текст:

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

Этот текст является примером зашифрованный ключ, который используется tooaccess hello учетной записи хранилища.

### <a name="unable-tooaccess-storage-after-changing-key"></a>Не удается tooaccess хранилища после смены ключа

Если изменить hello ключ для учетной записи хранилища, HDInsight теряет доступ к учетной записи хранилища hello. HDInsight использует кэшированную копию ключа в hello core-site.xml для hello кластера. Это кэшированной копии должно быть обновленные toomatch hello новый ключ.

Выполнение действия сценария hello снова __не__ обновить ключ hello как hello скрипт проверяет toosee, если уже есть запись для учетной записи хранения hello. Если запись уже существует, он не вносит какие-либо изменения.

toowork решения этой проблемы необходимо удалить hello существующую запись для учетной записи хранения hello. Используйте следующие шаги tooremove hello существующую запись hello.

1. В веб-браузере откройте hello Ambari веб-интерфейса для кластера HDInsight. Hello URI является https://CLUSTERNAME.azurehdinsight.net. Замените __CLUSTERNAME__ с hello имя кластера.

    При появлении запроса введите hello HTTP имени входа пользователя и пароль для кластера.

2. Выберите из списка служб hello левой стороны страницы приветствия hello __HDFS__. Выберите hello __Configs__ вкладку в центре hello страницы приветствия.

3. В hello __фильтра...__  введите значение __fs.azure.account__. Это возвращает записи для дополнительных учетных записей, добавленных в toohello кластера. Есть два типа записей: __keyprovider__ и __key__. Оба содержат hello имя учетной записи хранения hello как часть имени ключа hello.

    Hello ниже приведены примеры записей для учетной записи хранилища с именем __mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. После идентификации hello ключи для hello учетной записи хранения необходимо tooremove использовать hello красный "-" toohello значок справа от toodelete входа hello его. Затем с помощью hello __Сохранить__ кнопку toosave изменения.

5. После изменения были сохранены, используйте учетную запись хранения hello tooadd в действие сценария hello и новый кластер toohello значение ключа.

### <a name="poor-performance"></a>Низкая производительность

Если учетная запись хранения hello в разных регионах hello кластера HDInsight, может наблюдаться низкая производительность. Доступ к данным в другом регионе отправляет сетевого трафика за пределами hello региональные ЦОД Azure и через hello общедоступный Интернет, что может привести к задержке.

> [!WARNING]
> Использование учетной записи хранения в разных регионах hello кластера HDInsight не поддерживается.

### <a name="additional-charges"></a>Дополнительные расходы

Если учетной записи хранилища hello в другом регионе, чем hello кластера HDInsight, вы можете заметить дополнительных исходящий трафик на ваш Azure выставления счетов. Когда данные покидают центр обработки данных, исходящий трафик тарифицируется. Эти издержки применяется, даже если hello трафика, предназначенного для другой центр обработки данных Azure в другом регионе.

> [!WARNING]
> Использование учетной записи хранения в разных регионах hello кластера HDInsight не поддерживается.

## <a name="next-steps"></a>Дальнейшие действия

Вы узнали, как tooadd дополнительное хранилище учетных записей tooan существующего кластера HDInsight. Дополнительные сведения о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).
