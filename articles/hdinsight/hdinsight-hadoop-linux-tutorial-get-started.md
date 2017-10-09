---
title: "aaaGet к Hadoop и Hive в Azure HDInsight | Документы Microsoft"
description: "Узнайте, как кластеры toocreate HDInsight и запроса данных с Hive."
keywords: "начало работы с hadoop, hadoop под управлением linux, краткое руководство по hadoop, начало работы с hive, краткое руководство по hive"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight

Узнайте, как toocreate [Hadoop](http://hadoop.apache.org/) кластеров HDInsight и способ задания toorun Hive в HDInsight. [Apache Hive](https://hive.apache.org/) — наиболее популярных компонент hello в экосистеме Hadoop hello. В настоящее время в HDInsight доступно [семь типов кластеров](hdinsight-hadoop-introduction.md#overview). Каждый тип кластера поддерживает свой набор компонентов. Все типы кластеров поддерживают инфраструктуру Hive. Список поддерживаемых компонентов в HDInsight см. в разделе [новые возможности версии кластера Hadoop hello, предоставляемые HDInsight?](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Предварительные требования
Для работы с этим руководством вам потребуется:

* **Подписка Azure**: toocreate свободного один месяц пробную учетную запись, Обзор слишком[azure.microsoft.com/free](https://azure.microsoft.com/free).

## <a name="create-cluster"></a>Создание кластера

Большинство заданий Hadoop — пакетные. Создание кластера, выполнение некоторых заданий и затем удалить кластер hello. В этом разделе вы создадите в HDInsight кластер Hadoop, используя [шаблон Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Знакомство с шаблонами Resource Manager не является обязательным для работы с этим руководством. Для других методов создания кластера и общие сведения о свойствах hello, используемые в этом учебнике, см. [HDInsight, создания кластеров](hdinsight-hadoop-provision-linux-clusters.md). Используйте hello выбора над hello toochoose страницы приветствия варианты создания кластера.

Hello шаблона диспетчера ресурсов, используемые в этом учебнике находится в [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). 

1. Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портал Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Введите или выберите hello следующие значения:
   
    ![Начало HDInsight Linux работы шаблона диспетчера ресурсов на портале](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "hello кластера Hadoop развертывание в HDInsigut с помощью портала Azure и шаблона диспетчера ресурсов группы").
   
    * **Подписка**. Выберите подписку Azure.
    * **Группа ресурсов.** Создайте группу ресурсов Azure или выберите имеющуюся.  Группа ресурсов — это контейнер компонентов Azure.  В этом случае группа ресурсов hello содержит кластер HDInsight hello и hello зависимых учетную запись хранилища Azure. 
    * **Расположение**: выберите расположение Azure место toocreate кластера.  Выберите расположение ближе tooyou для повышения производительности. 
    * **Тип кластера**. Для работы с этим руководством выберите **Hadoop**.
    * **Имя кластера**: Введите имя для кластера Hadoop hello.
    * **Имя входа и пароль кластера**: имя для входа по умолчанию hello **администратора**.
    * **SSH имя пользователя и пароль**: имя пользователя по умолчанию hello **sshuser**.  Это имя можно изменить. 
     
    Некоторые свойства были жестко задано в шаблоне hello.  Вы можете настроить эти значения на основе шаблона hello.

    * **Расположение**: hello расположение кластера hello и hello ресурс учетной записи службы хранилища зависимых hello местоположения hello группы ресурсов.
    * **Версия кластера**: 3.5.
    * **Тип ОС**: Linux.
    * **Количество рабочих узлов**: 2.

     У каждого кластера есть зависимость [учетной записи хранения Azure](hdinsight-hadoop-use-blob-storage.md) или [учетной записи Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md). Она называется учетной записи хранения по умолчанию hello. Кластер HDInsight и ее учетную запись хранения по умолчанию должна быть размещена в hello же регионе Azure. Удаление кластеров не приводит к удалению учетной записи хранилища hello. 
     
     Дополнительные сведения об этих свойствах см. в инструкциях по [созданию кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Выберите **я принимаю условия, указанных выше, toohello** и **toodashboard ПИН-код**, а затем нажмите кнопку **покупки**. Вы увидите новую плитку под названием **развертывание шаблона-развертывания** на панели мониторинга портала hello. Это занимает около toocreate около 20 минут кластера. После создания кластера hello заголовок hello hello плитки используется измененные toohello ресурсов группы с указанным именем. И группа ресурсов hello автоматически откроется портал hello в Новая колонка. Вы увидите кластера hello и хранения по умолчанию hello в списке.
   
    ![Группа ресурсов при начале работы с HDInsight под управлением Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Группа ресурсов кластера Azure HDInsight")

4. Щелкните hello имя tooopen hello кластера в новый колонку.

   ![Параметры кластера при начале работы с HDInsight под управлением Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "Свойства кластера HDInsight")


## <a name="run-hive-queries"></a>Выполнение запросов Hive
[Apache Hive](hdinsight-use-hive.md) — hello наиболее популярных компонент, используемый в HDInsight. Существует множество способов toorun задания Hive в HDInsight. В этом учебнике используется hello представление Ambari Hive с портала hello. Другие способы отправки заданий Hive описаны в статье [Использование Hive в HDInsight](hdinsight-use-hive.md).

1. Из предыдущего снимка экрана приветствия щелкните **мониторинга кластера**, а затем нажмите кнопку **мониторинга кластера HDInsight**.  Можно также просмотреть слишком **https://&lt;Имя_кластера >. azurehdinsight.net**, где &lt;Имя_кластера > — hello кластер, созданный в предыдущей tooopen раздел Ambari hello.
2. Введите hello Hadoop пользователя и пароль, указанный в предыдущем разделе hello. имя пользователя по умолчанию Hello **администратора**.
3. Откройте **Hive представление** как показано на следующий снимок экрана приветствия:
   
    ![Выбор представления Ambari](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "Меню представления Hive в HDInsight")
4. В hello **редактора запросов** раздел страницы приветствия, hello вставьте следующие инструкции HiveQL лист hello:
   
        SHOW TABLES;
   
   > [!NOTE]
   > Для Hive требуется точка с запятой.       
   > 
   > 
5. Нажмите **Execute (Выполнить)**. Объект **результаты процесса запроса** раздел должен отображаются под hello редактора запросов и отобразить сведения о задании hello. 
   
    После завершения запроса hello, hello **результаты процесса запроса** раздел отображает hello результаты операции hello. Вы увидите одну таблицу с именем **hivesampletable**. Этот образец таблицы Hive поставляется с всех кластеров HDInsight hello.
   
    ![Представление Hive в HDInsight](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "Редактор запросов представления Hive в HDInsight")
6. Повторите шаги 4 и следующем запросе hello toorun шаг 5:
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > Примечание hello **сохранить результаты** раскрывающийся список в hello верхнего левого угла hello **результаты процесса запроса** статьи; использовать этот результаты hello tooeither загрузки или сохранить tooHDInsight хранилища в CSV-файл.
   > 
   > 
7. Нажмите кнопку **журнал** tooget список заданий hello.

После завершения задания Hive можно [экспортировать базу данных SQL tooAzure результатов hello или базы данных SQL Server](hdinsight-use-sqoop-mac-linux.md), вы также можете [визуализировать результаты hello, с помощью Excel](hdinsight-connect-excel-power-query.md). Дополнительные сведения об использовании Hive в HDInsight см. в разделе [используйте Hive и HiveQL на Hadoop в HDInsight tooanalyze Apache log4j образец файла](hdinsight-use-hive.md).

## <a name="clean-up-hello-tutorial"></a>Очистка hello учебника
После завершения учебника hello, вы можете toodelete hello кластера. В случае с HDInsight ваши данные хранятся в службе хранилища Azure, что позволяет безопасно удалить неиспользуемый кластер. Плата за кластеры HDInsight взимается, даже когда они не используются. Поскольку плата hello для кластера hello много раз больше, чем hello плата за хранилище, экономически выгодно toodelete кластеры, когда они не используются. 

> [!NOTE]
> С помощью [фабрики данных Azure](hdinsight-hadoop-create-linux-clusters-adf.md), можно создать кластеры HDInsight по требованию, а также настроить TimeToLive параметр слишком кластеров hello автоматического удаления. 
> 
> 

**toodelete hello кластера и/или hello по умолчанию учетная запись хранения**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Из панели мониторинга портала hello щелкните плитку hello с именем группы ресурсов hello, которая использовалась при создании кластера hello.
3. Нажмите кнопку **удаление** hello колонке toodelete hello группу ресурсов, содержащий hello кластера и учетной записи хранения по умолчанию hello, или щелкните имя кластера hello на hello **ресурсов** плитку, а затем нажмите кнопку **Удалить** колонке hello кластера. Удаление группы ресурсов hello Примечание Удаляет учетную запись хранения hello. Учетная запись хранения tookeep hello, выберите toodelete только hello кластера.

## <a name="troubleshoot"></a>Устранение неполадок

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы изучили toocreate HDInsight под управлением Linux кластера с помощью шаблона диспетчера ресурсов, а также и tooperform простых запросов Hive.

toolearn Дополнительные сведения об анализе данных с HDInsight, см. следующие статьи hello.

* toolearn Подробнее об использовании Hive с HDInsight, включая как tooperform Hive запросы из Visual Studio, в разделе [используйте Hive с HDInsight][hdinsight-use-hive].
* использовать язык toolearn о Pig tootransform данных см. в разделе [использование Pig с HDInsight][hdinsight-use-pig].
* в разделе toolearn о MapReduce программы toowrite способом обработки данных в Hadoop, [используйте MapReduce с HDInsight][hdinsight-use-mapreduce].
* в разделе toolearn об использовании hello средства HDInsight для Visual Studio tooanalyze данных на HDInsight, [приступить к работе со средствами Visual Studio Hadoop для HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Если вы будете готовы toostart при работе с собственными данными и требуются дополнительные сведения о tooknow как HDInsight хранит данные, а также какие данные tooget в HDInsight, см. ниже hello:

* Сведения о том, как HDInsight использует службу хранилища Azure, см. в статье [Использование HDFS-совместимой службы хранилища с Hadoop в HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Сведения о том, как tooHDInsight tooupload данных, в разделе [отправить данные tooHDInsight][hdinsight-upload-data].

При желании toolearn Дополнительные сведения о создании и управлении кластер HDInsight см. ниже hello:

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


