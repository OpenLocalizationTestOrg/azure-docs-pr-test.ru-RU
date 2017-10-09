---
title: "aaaGet к работе с примером HBase на HDInsight - Azure | Документы Microsoft"
description: "Выполните этот пример toostart Apache HBase, с помощью hadoop в HDInsight. Создание таблиц из оболочки HBase hello, а также запросить с помощью Hive."
keywords: "hbasecommand, пример hbase"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>Начало работы с примером Apache HBase в HDInsight

Узнайте, как создать таблицы в HBase toocreate кластер HBase в HDInsight и запросы к таблицам с помощью Hive. Для получения общих сведений по HBase обратитесь к разделу [Что такое HBase в HDInsight][hdinsight-hbase-overview].

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать, в этом примере HBase попытки, необходимо иметь hello следующих элементов:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Secure Shell(SSH).](hdinsight-hadoop-linux-use-ssh-unix.md) 
* [curl](http://curl.haxx.se/download.html).

## <a name="create-hbase-cluster"></a>Создание кластера HBase
Hello следующая процедура использует toocreate шаблона диспетчера ресурсов Azure версии 3.4 HBase под управлением Linux кластера и hello зависимых по умолчанию учетная запись хранилища Azure. toounderstand hello параметров, используемых в процедуре hello и другие методы создания кластера, в разделе [кластеров под управлением Linux, создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Щелкните hello следующий шаблон hello tooopen изображения в hello портал Azure. Hello шаблон находится в большой двоичный объект открытого контейнера. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Из hello **развертывания пользовательского** колонке введите hello следующие значения:
   
   * **Подписки**: выберите подписку Azure, используемых toocreate hello кластера.
   * **Группа ресурсов**: создайте группу ресурсов Azure или выберите существующую.
   * **Расположение**: укажите расположение hello hello группы ресурсов. 
   * **Имя_кластера**: Введите имя кластера HBase hello.
   * **Имя входа и пароль кластера**: имя для входа по умолчанию hello **администратора**.
   * **SSH имя пользователя и пароль**: имя пользователя по умолчанию hello **sshuser**.  Это имя можно изменить.
     
     Все остальные параметры являются необязательными.  
     
     У каждого кластера есть зависимость учетной записи хранения для службы хранилища Azure. После удаления кластера hello данные сохраняются в учетной записи хранения hello. Имя учетной записи хранения по умолчанию Hello кластера — имя кластера hello без «store» добавлено. Это жестко задано в разделе переменных шаблона hello.
3. Выберите **я принимаю условия, указанных выше, toohello**, а затем нажмите кнопку **покупки**. Занимает около 20 минут toocreate кластера.

> [!NOTE]
> После удаления кластер HBase, можно создать другой кластер HBase с помощью hello же контейнер больших двоичных объектов по умолчанию. новый кластер Hello забирает hello HBase таблицы, которые вы создали в исходном кластере hello. tooavoid несогласованности, рекомендуется отключить hello HBase таблиц перед удалением hello кластера.
> 
> 

## <a name="create-tables-and-insert-data"></a>Создание таблиц и вставка данных
Можно использовать SSH tooconnect tooHBase кластеров и затем с помощью оболочки HBase toocreate HBase таблицы, вставка данных и запроса данных. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

Для большинства пользователей данные отображаются в табличном формате hello:

![Табличные данные HDInsight HBase][img-hbase-sample-data-tabular]

В HBase (реализацию BigTable) hello же данных имеет следующий вид:

![Данные BigTable HDInsight HBase][img-hbase-sample-data-bigtable]


**hello toouse оболочки HBase**

1. В SSH выполните следующую команду HBase hello.
   
    ```bash
    hbase shell
    ```

2. Создайте HBase с двумя столбцами:

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. Вставьте какие-либо данные:
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Оболочка HDInsight Hadoop HBase][img-hbase-shell]
4. Получите одну строку
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    Вы увидите hello же результаты, как с помощью команды проверки hello, поскольку имеется только одна строка.
   
    Дополнительные сведения о схеме таблицы в HBase hello см. в разделе [tooHBase введение структуре схемы][hbase-schema]. Дополнительные команды HBase см. в [справочнике по Apache HBase][hbase-quick-start].
5. Выйти из оболочки hello
   
    ```hbaseshell
    exit
    ```

**toobulk загрузки данных в таблицу HBase hello контактов**

HBase включает несколько методов загрузки данных в таблицы.  Для получения дополнительных сведений обратитесь к разделу [Массовая загрузка](http://hbase.apache.org/book.html#arch.bulk.load).

Пример файла данных находится в общедоступном контейнере больших двоичных объектов *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.  Hello содержимое файла данных hello является:

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

При необходимости можно создать текстовый файл и отправить файл hello tooyour собственную учетную. Hello инструкции см. в разделе [передать данные для заданий Hadoop в HDInsight][hdinsight-upload-data].

> [!NOTE]
> Эта процедура использует таблицу HBase контакты hello, созданный в последней процедуры hello.
> 

1. Запустите из SSH, следующая команда tootransform hello в файле tooStoreFiles данных и хранить в относительный путь, указанный Dimporttsv.bulk.output hello.  Если вы находитесь в оболочку HBase, используйте tooexit команду выхода hello.

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. Выполните следующие команды tooupload hello данные из таблицы HBase toohello /example/data/storeDataFileOutput hello.
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. Откройте оболочку HBase hello и использовать hello hello сканирования команда toolist содержимое таблицы.

## <a name="use-hive-tooquery-hbase"></a>Используйте куст tooquery HBase

Можно запросить данные в таблицах HBase с помощью Hive. В этом разделе, можно создать таблицу Hive, сопоставляется таблице HBase toohello и использует tooquery hello данных в таблице HBase.

1. Откройте **PuTTY**и подключите toohello кластер.  См. инструкции hello в предыдущей процедуре hello.
2. Из сеанса SSH hello используйте следующие команды toostart Beeline hello:

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Дополнительные сведения о Beeline см. в статье [Использование Hive с Hadoop в HDInsight с применением Beeline](hdinsight-hadoop-use-hive-beeline.md).
       
3. Запустите следующие toocreate сценарий HiveQL hello таблицу Hive, который сопоставляется таблице HBase toohello. Убедитесь, что вы создали образец таблицы hello ссылается ранее в этом учебнике с помощью оболочки HBase hello, перед выполнением этой инструкции.

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. Выполните следующие данные hello tooquery сценарий HiveQL в таблице HBase hello hello.

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>Использование API REST для HBase

Hello API-интерфейса REST является защищен с помощью [обычной проверки подлинности](http://en.wikipedia.org/wiki/Basic_access_authentication). Всегда должны выполнять запросы с помощью безопасного HTTP (HTTPS) toohelp убедитесь, что учетные данные безопасно отправляются toohello сервера.

2. Используйте следующие команды toolist hello существующей таблицы, HBase hello.

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. Используйте hello, следующая команда toocreate новая таблица с двумя столбцами семейства HBase:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    Схема Hello предоставляется в формате JSon hello.
4. Используйте следующие команды tooinsert hello некоторые данные:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    Необходимо base64 кодирования hello значениями, указанными в параметр -d hello. В примере hello:
   
   * MTAwMA==: 1000;
   * UGVyc29uYWw6TmFtZQ==: Personal:Name
   * Sm9obiBEb2xl: John Dole.
     
     [false ключ строки](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) позволяет tooinsert несколько значений (в пакетном режиме).
5. Используйте следующие команды tooget строку hello.
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

Дополнительные сведения см. в [справочнике по Apache HBase](https://hbase.apache.org/book.html#_rest).

> [!NOTE]
> Thrift не поддерживается HBase в HDInsight.
>
> При использовании перелистывания или любые другие связи REST с WebHCat, должен пройти проверку подлинности запросы hello, предоставляя hello имя пользователя и пароль администратора кластера HDInsight hello. Как использовать запросы toohello toosend hello server часть hello универсальный код ресурса (URI), необходимо также использовать hello имя кластера:
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    Должно появиться примерно toohello ответа, следующий ответ:
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>Проверка состояния кластера
HBase на HDInsight поставляется с веб-интерфейсом для наблюдения за кластерами. С помощью hello веб-интерфейса пользователя, можно запросить статистические данные или сведения об областях.

**hello tooaccess HBase образец пользовательского интерфейса**

1. Вход в hello hello Ambari веб-интерфейса адресу https://&lt;Имя_кластера >. azurehdinsight.net.
2. Нажмите кнопку **HBase** из меню слева hello.
3. Нажмите кнопку **быстрые ссылки** на hello вверху страницы приветствия, toohello точки активной Zookeeper узел ссылки, а затем нажмите кнопку **пользовательского интерфейса главного HBase**.  на другой вкладке браузера открывается Hello пользовательского интерфейса:

  ![Основной интерфейс HDInsight HBase](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  Hello пользовательского интерфейса главного HBase содержит hello в следующих разделах:

  - региональные серверы;
  - главные узлы резервного копирования;
  - таблицы;
  - задачи;
  - атрибуты ПО.

## <a name="delete-hello-cluster"></a>Удалить кластер hello
tooavoid несогласованности, рекомендуется отключить hello HBase таблиц перед удалением hello кластера.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Устранение неполадок

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, как toocreate кластер HBase и как данные этих таблиц из hello toocreate таблиц и представлений hello оболочки HBase. Вы также узнали, как запрос на данные в таблицах HBase и как toouse hello toocreate HBase C# API-интерфейс REST таблицу HBase и получения данных из таблицы hello toouse куста.

toolearn более, см.:

* [Что такое HBase в HDInsight][hdinsight-hbase-overview]. HBase — это база данных NoSQL с открытым исходным кодом Apache, разработанная в рамках проекта Hadoop, которая обеспечивает произвольный доступ и строгую согласованность больших объемов неструктурированных и частично структурированных данных.

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
