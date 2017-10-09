---
title: "Создание - Azure кластера библиотек Hive aaaAdd во время HDInsight | Документы Microsoft"
description: "Узнайте, как tooadd библиотек Hive (jar-файлы), tooan HDInsight кластера во время создания кластера."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Добавление пользовательских библиотек Hive при создании кластера HDInsight

Если у вас есть библиотек, которые часто используются с Hive в HDInsight, этот документ содержит сведения об использовании библиотеки hello действие сценария toopre нагрузки во время создания кластера. Библиотеки, добавленные с помощью hello шаги в этом документе глобально доступны в кусте - у без необходимости toouse [Добавьте JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload их.

## <a name="how-it-works"></a>Принцип работы

При создании кластера, можно также задать действие скрипта, который запускает сценарий на узлах кластера hello при их создании. сценарий Hello в этом документе принимает один параметр, являющийся WASB расположение, которое содержит предварительно загружать toobe библиотеки (хранятся в виде файлов jar) hello.

Во время создания кластера hello скрипт Перечисляет файлы hello, копирует их toohello `/usr/lib/customhivelibs/` каталог на головном и рабочих узлов, после чего они добавляются toohello `hive.aux.jars.path` свойство в hello `core-site.xml` файла. Для кластеров под управлением Linux, он обновляет hello `hive-env.sh` файл с hello расположение файлов hello.

> [!NOTE]
> С помощью действий скрипта hello в этой статье обеспечивает библиотеки hello в hello следующие сценарии:
>
> * **HDInsight под управлением Linux** — Если с помощью hello клиентом куст **WebHCat**, и **HiveServer2**.
> * **HDInsight под управлением Windows** — при использовании клиента Hive hello и **WebHCat**.

## <a name="hello-script"></a>сценарий Hello

**Расположение скрипта**

Для **кластеров под управлением Linux** — [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh).

Для **кластеров под управлением Windows** — [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1).

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

**Требования**

* Hello сценарии должны быть hello примененных tooboth **Head узлы** и **рабочих узлов**.

* Здравствуйте, JAR-файлов необходимо tooinstall должны храниться в хранилище больших двоичных объектов Azure в **один контейнер**.

* Учетная запись хранения Hello hello библиотеку jar-файла, содержащего **должен** быть кластера HDInsight связанные toohello во время создания. Оно должно быть учетной записи хранения по умолчанию hello, или учетной записи добавляются через __необязательная конфигурация__.

* путь toohello Hello WASB контейнер должен быть указан как параметр toohello действие сценария. Например, если hello JAR-файлов хранятся в контейнере с именем **библиотеки** в учетной записи хранения с именем **mystorage**, нужно указать параметр hello  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Данный документ предполагает уже создания учетной записи хранилища, контейнер больших двоичных объектов и tooit hello загруженные файлы.
  >
  > Если вы не создали учетную запись хранения, это можно сделать через hello [портал Azure](https://portal.azure.com). Затем можно использовать программу например [обозреватель хранилищ Azure](http://storageexplorer.com/) toocreate контейнера в учетной записи hello и передача файлов tooit.

## <a name="create-a-cluster-using-hello-script"></a>Создание кластера с помощью скрипта hello

> [!NOTE]
> следующие шаги Hello создать кластер HDInsight под управлением Linux. Выберите toocreate кластера под управлением Windows, **Windows** как hello кластера ОС при создании кластера hello и используйте вместо hello bash script script приветствия Windows (PowerShell).
>
> Можно также использовать Azure PowerShell или toocreate HDInsight .NET SDK hello в кластер, использующий этот сценарий. Дополнительные сведения об использовании этих методов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

1. Запуск подготовки кластера с помощью действия hello в [HDInsight подготовки кластеров в Linux](hdinsight-hadoop-provision-linux-clusters.md), но не завершайте подготовки.

2. На hello **необязательная конфигурация** колонке выберите **действия скрипта**и укажите hello следующую информацию:

   * **ИМЯ**: Введите понятное имя для действия сценария hello.

   * **Универсальный код ресурса скрипта** — https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh;

   * **Головной** — установите флажок.

   * **Рабочая роль** — установите флажок;

   * **Zookeeper** — оставьте это поле пустым;

   * **Параметры**: Введите hello WASB адрес toohello контейнера и учетную запись хранилища, содержащий hello JAR-файлов. (например, **wasb://libs@mystorage.blob.core.windows.net/**).

3. Внизу hello hello **действия скрипта**, использовать hello **выберите** конфигурация hello toosave кнопок.

4. На hello **необязательная конфигурация** колонке выберите **связанные учетные записи хранения** и выберите hello **добавить ключ хранилища** ссылку. Выберите учетную запись хранения hello, содержащий hello JAR-файлов, а затем использовать hello **выберите** кнопки toosave параметров и возвращаемого hello **необязательная конфигурация** колонку.

5. Используйте hello **выберите** кнопку внизу hello hello **необязательная конфигурация** колонке toosave hello необязательная конфигурация сведения.

6. Продолжить подготовки кластера hello, как описано в [HDInsight подготовки кластеров в Linux](hdinsight-hadoop-provision-linux-clusters.md).

После завершения выполнения создания кластера, вы, добавляемые с помощью этого скрипта из куста без необходимости toouse hello JAR-файлов hello может toouse `ADD JAR` инструкции.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о работе с Hive см. в статье [Использование Hive и HiveQL с Hadoop в HDInsight для анализа примера файла Apache log4j](hdinsight-use-hive.md).
