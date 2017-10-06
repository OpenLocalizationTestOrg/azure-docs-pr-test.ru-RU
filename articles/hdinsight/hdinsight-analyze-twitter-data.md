---
title: "aaaAnalyze данных Twitter с Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse куст tooanalyze Twitter данные в Hadoop в HDInsight toofind hello частоту использования определенного слова."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Анализ данных Twitter с помощью Hive в HDInsight
Социальных веб-узлы, одним из основных факторов определяющим hello внедрения больших данных. Общедоступные API, предоставляемые сайтами, такими как Twitter, — полезный источник данных для анализа и понимания популярных тенденций.
В этом учебнике будет получение твитов с помощью Twitter, потоковая передача API и затем с помощью Apache Hive для Azure HDInsight tooget список пользователей Twitter, отправленных hello большинство твиты, содержащих определенные слова.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight под управлением Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Для кластера под управлением Linux tooa определенные действия в разделе [Twitter анализ данных с помощью Hive в HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Рабочая станция** , на которой установлена и настроена среда Azure PowerShell.

    tooexecute сценариев Windows PowerShell, необходимо запустить Azure PowerShell от имени администратора и задать политику выполнения hello слишком*RemoteSigned*. Ознакомьтесь с разделом о [выполнении сценариев Windows PowerShell][powershell-script].

    Перед выполнением скриптов Windows PowerShell, убедитесь, что вы являетесь tooyour подключенных подписка Azure с помощью hello, выполнив командлет:

    ```powershell
    Login-AzureRmAccount
    ```

    Если у вас несколько подписок Azure, используйте hello, выполнив командлет tooset hello текущей подписки.

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г. шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.
    >
    > Выполните шаги hello в [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell. При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.

* **Кластер Azure HDInsight**. Инструкции по подготовке кластеров см. в разделе [Приступая к работе с HDInsight][hdinsight-get-started] или [Подготовка кластеров HDInsight][hdinsight-provision]. Имя кластера hello потребуется далее в учебнике hello.

Hello следующей таблице перечислены файлы hello, используемые в этом учебнике.

| Файлы | Описание |
| --- | --- |
| /tutorials/twitter/data/tweets.txt |Hello исходные данные для задания Hive hello. |
| /tutorials/twitter/output |Hello для задания Hive hello выходную папку. Hello имя выходного файла задания Hive по умолчанию — **000000_0**. |
| tutorials/twitter/twitter.hql |файл скрипта HiveQL Hello. |
| /tutorials/twitter/jobstatus |Здравствуйте, состояние задания Hadoop. |

## <a name="get-twitter-feed"></a>Получение канала Twitter
В этом учебнике будет использоваться hello [Twitter потоковой передачи API-интерфейсы][twitter-streaming-api]. Hello конкретных Twitter, потоковая передача будет использовать API — [состояния и фильтрации][twitter-statuses-filter].

> [!NOTE]
> Файл, содержащий 10 000 твитов и (рассматривается в следующем разделе hello) файл скрипта Hive hello были переданы в открытый контейнер больших двоичных объектов. Этот раздел можно пропустить, если toouse hello отправлены файлы.

[Твиты данных](https://dev.twitter.com/docs/platform-objects/tweets) хранятся в формате JavaScript Object Notation (JSON) hello, содержащий сложных вложенной структуры. Вместо того чтобы писать много строк кода с использованием обычного языка программирования, эту вложенную структуру можно преобразовать в таблицу Hive, чтобы к ней можно было отправлять запросы на SQL-подобном языке — HiveQL.

Twitter использует OAuth tooprovide право доступа tooits API. OAuth является протоколом проверки подлинности, позволяющий пользователям tooapprove приложений tooact от их имени без пароля для управления доступом. Дополнительные сведения можно найти по [oauth.net](http://oauth.net/) или в hello отлично [tooOAuth руководство для начинающих](http://hueniverse.com/oauth/) из Hueniverse.

Hello первый шаг toouse OAuth является toocreate новое приложение на сайте разработчика Twitter hello.

**toocreate приложения Twitter**

1. Войдите в слишком[https://apps.twitter.com/](https://apps.twitter.com/). Нажмите кнопку hello **Зарегистрируйтесь сейчас** ссылку, если у вас нет учетной записи Twitter.
2. Щелкните **Создать новое приложение**.
3. Введите **Имя**, **Описание**, **Веб-сайт**. Можно использовать URL-адрес для hello **веб-сайт** поля. Hello в следующей таблице показаны некоторые toouse пример значения:

   | Поле | Значение |
   | --- | --- |
   |  Имя |MyHDInsightApp |
   |  Описание |MyHDInsightApp |
   |  Веб-сайт |http://www.myhdinsightapp.com |
4. Установите флажок **Я принимаю** и нажмите кнопку **Создать приложение Twitter**.
5. Нажмите кнопку hello **разрешений** разрешение по умолчанию hello вкладку — **только для чтения**. Этого разрешения достаточно для данного учебника.
6. Нажмите кнопку hello **ключей и маркеры доступа** вкладки.
7. Нажмите кнопку **Создать маркер доступа**.
8. Нажмите кнопку **OAuth теста** в правом верхнем углу hello страницы приветствия.
9. Запишите **ключ клиента**, **Секрет клиента**, **Маркер доступа** и **Секрет маркера доступа**. Вам потребуются значения hello далее в учебнике hello.

В этом учебнике будет использоваться Windows PowerShell toomake hello в веб-службу. Пример .NET C# см. в разделе [Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment]. Hello вызовов веб-служб других популярным средством toomake — [ *Curl*][curl]. Curl можно скачать [отсюда][curl-download].

> [!NOTE]
> При использовании команды перелистывание hello в Windows, используйте двойные кавычки вместо одинарные кавычки для значений параметра hello.

**твиты tooget**

1. Откройте hello Сценариев Windows PowerShell интегрированной среде (). (На hello 8 рабочий стол Windows, введите **PowerShell_ISE** и нажмите кнопку **интегрированной среды Сценариев Windows PowerShell**. Ознакомьтесь с разделом [Запуск Windows PowerShell в Windows 8 и Windows][powershell-start].)
2. Скопируйте следующий скрипт в области сценариев hello hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Задайте hello первые пять tooeight переменных в сценарии hello:

    Переменная|Описание
    ---|---
    $clusterName|Это имя hello hello кластера HDInsight, где требуется приложение hello toorun.
    $oauth_consumer_key|Это приложение hello Twitter **ключ потребителя** записанное ранее при создании приложения hello Twitter.
    $oauth_consumer_secret|Это приложение hello Twitter **секрет пользователя** записанное ранее.
    $oauth_token|Это приложение hello Twitter **маркер доступа** записанное ранее.
    $oauth_token_secret|Это приложение hello Twitter **секрет маркера доступа** записанное ранее.
    $destBlobName|Это имя большого двоичного объекта hello выходные данные. значение по умолчанию Hello — **tutorials/twitter/data/tweets.txt**. Если изменить значение по умолчанию hello, сценарии Windows PowerShell hello tooupdate необходимо соответствующим образом.
    $trackString|Возвращает ключевые слова связанные toothese твиты Hello веб-службы. значение по умолчанию Hello — **HDInsight Azure в облаке,**. Если изменить значение по умолчанию hello будет соответствующим образом обновить hello сценариев Windows PowerShell.
    $lineMax|Hello значение определяет, сколько твиты hello скрипт будет считывать. Он принимает 100 твиты tooread о трех минут. Можно задать большее значение, но может занять больше времени toodownload.

1. Нажмите клавишу **F5** toorun hello скрипта. Если возникли проблемы, чтобы избежать этого, выделите все строки hello и нажмите клавишу **F8**.
2. В конце выходных данных в конце hello hello выходных данных. Все сообщения об ошибке выделяются красным цветом.

Как процедуру проверки, вы можете проверить файл вывода hello, **/tutorials/twitter/data/tweets.txt**, на устройстве хранения больших двоичных объектов Azure с помощью обозревателя хранилищ Azure или Azure PowerShell. Пример сценария Windows PowerShell для перечисления файлов см. в разделе [Использование хранилища больших двоичных объектов с HDInsight][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>Создание скрипта HiveQL
С помощью Azure PowerShell, можно выполнения нескольких инструкций HiveQL один во время или пакет hello HiveQL инструкции в файл скрипта. В этом учебнике будет создан скрипт HiveQL. Hello файл сценария должен быть отправленного tooAzure хранилища больших двоичных объектов. В следующем разделе hello будет выполняться hello файл скрипта с помощью Azure PowerShell.

> [!NOTE]
> файл скрипта Hive Hello и файл, содержащий 10 000 твиты были переданы в открытый контейнер больших двоичных объектов. Этот раздел можно пропустить, если toouse hello отправлены файлы.

сценарий HiveQL Hello выполнит hello следующее:

1. **Удалить таблицу tweets_raw hello** в случае, если таблица hello уже существует.
2. **Создайте таблицу Hive hello tweets_raw**. Эта временная таблица структурированных Hive содержит hello данные для дальнейшего извлечения, преобразования и загрузки (ETL) обработки. Сведения о секциях см. в [руководстве по Hive][apache-hive-tutorial].
3. **Загрузка данных** из исходной папки hello, /tutorials/twitter/data. набор данных больших твиты Hello в вложенных формат JSON теперь преобразован временная структура таблицы Hive.
4. **Твиты hello удаления таблицы** в случае, если таблица hello уже существует.
5. **Создать таблицу твиты hello**. Прежде чем выполнять запросы к набору данных твиты hello с помощью Hive, toorun необходим другой процесс ETL. Этот процесс ETL определяет дополнительные схемы таблиц для hello данные, которые были сохранены в таблице «twitter_raw» hello.
6. **Вставляет таблицу для перезаписи**. Этот сложный сценарий Hive запускается набор длинные задания MapReduce, hello кластера Hadoop. В зависимости от размера кластера вашего набора данных и hello это может занять около 10 минут.
7. **Вставляет каталог для перезаписи**. Запустите файл tooa набора данных запроса и вывод hello. Этот запрос возвращает список пользователей Twitter, отправленных большинство твиты, содержащих слово hello «Azure».

**Куст toocreate сценариев и отправьте его tooAzure**

1. Откройте интегрированную среду сценариев Windows PowerShell.
2. Скопируйте следующий скрипт в области сценариев hello hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Установка hello первых двух переменных в сценарии hello:

   | Переменная | Описание |
   | --- | --- |
   |  $clusterName |Введите имя кластера HDInsight hello, в котором требуется toorun приложения hello. |
   |  $subscriptionID |Введите идентификатор подписки Azure. |
   |  $sourceDataPath |Здравствуйте, место хранения больших двоичных объектов Azure, где запросы Hive hello будет считывать данные hello. Не нужно toochange этой переменной. |
   |  $outputPath |Здравствуйте, место хранения больших двоичных объектов Azure, где запросы Hive hello будет выдавать результаты hello. Не нужно toochange этой переменной. |
   |  $hqlScriptFile |Hello путь и имя файла hello файла сценария HiveQL hello. Не нужно toochange этой переменной. |
4. Нажмите клавишу **F5** toorun hello скрипта. Если возникли проблемы, чтобы избежать этого, выделите все строки hello и нажмите клавишу **F8**.
5. В конце выходных данных в конце hello hello выходных данных. Все сообщения об ошибке выделяются красным цветом.

Как процедуру проверки, вы можете проверить файл вывода hello, **/tutorials/twitter/twitter.hql**, на устройстве хранения больших двоичных объектов Azure с помощью обозревателя хранилищ Azure или Azure PowerShell. Пример сценария Windows PowerShell для перечисления файлов см. в разделе [Использование хранилища больших двоичных объектов с HDInsight][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Обработка данных Twitter с помощью Hive
После завершения всю работу по подготовке hello. Теперь можно вызвать сценарий Hive hello и hello результаты проверки.

### <a name="submit-a-hive-job"></a>Отправка задания Hive
Используйте следующий сценарий Hive hello toorun сценарий Windows PowerShell hello. Вам потребуется tooset hello первой переменной.

> [!NOTE]
> toouse hello твитов и hello сценарий HiveQL, загруженный в двух последних разделах hello, набор $hqlScriptFile too"/tutorials/twitter/twitter.hql». hello toouse те, которые были отправлены tooa большой двоичный объект открытого автоматически, задайте $hqlScriptFile слишком»wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql».

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Результаты проверки hello
Используйте hello следующие выходные данные задания Hive hello в toocheck сценария Windows PowerShell. Вам потребуется tooset hello первых двух переменных.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> Таблица Hive Hello использует \001 как hello разделитель полей. разделитель Hello не отображается в выходных данных hello.

После результаты анализа hello были размещены в хранилище больших двоичных объектов Azure, можно экспортировать hello данных tooan Azure SQL базы данных или SQL server, экспортировать hello tooExcel данных с помощью Power Query или подключения к данным toohello приложения с помощью hello Hive драйвера ODBC. Дополнительные сведения см. в разделе [Sqoop использования с HDInsight][hdinsight-use-sqoop], [анализировать данные задержки рейсов при помощи HDInsight][hdinsight-analyze-flight-delay-data], [ Подключиться с помощью Power Query Excel tooHDInsight][hdinsight-power-query], и [tooHDInsight Excel подключиться с hello драйвер Microsoft ODBC Hive][hdinsight-hive-odbc].

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике мы увидели, как tootransform набору неструктурированных данных JSON в структурированных tooquery таблицу Hive, просматривать и анализировать данные из Twitter с помощью HDInsight в Azure. toolearn более, см.:

* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]
* [Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment]
* [Анализ данных о задержке рейсов с помощью Hive в HDInsight][hdinsight-analyze-flight-delay-data]
* [Подключение Excel tooHDInsight с помощью Power Query][hdinsight-power-query]
* [Связь с hello Hive драйвер ODBC для Microsoft Excel tooHDInsight][hdinsight-hive-odbc]
* [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
