---
title: "aaaAnalyze данных Twitter с Apache Hive - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse использовать Hive и Hadoop в HDInsight tootransform необработанные данные TWitter в таблицу Hive с возможностью поиска."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>Анализ данных Twitter с помощью Hive и Hadoop в HDInsight

Узнайте, как toouse Apache Hive tooprocess данных Twitter. Hello результатом является список пользователей Twitter, отправленных hello большинство твиты, содержащих определенные слова.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве были протестированы на HDInsight 3.6.
>
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="get-hello-data"></a>Получение данных hello

Twitter позволяет tooretrieve hello [данные для каждого твит](https://dev.twitter.com/docs/platform-objects/tweets) как документ нотации объектов JavaScript (JSON) с помощью REST API. [OAuth](http://oauth.net) необходим для проверки подлинности toohello API.

### <a name="create-a-twitter-application"></a>Создание приложения Twitter

1. Веб-браузере вход слишком[https://apps.twitter.com/](https://apps.twitter.com/). Нажмите кнопку hello **регистрации теперь** ссылку, если у вас нет учетной записи Twitter.

2. Щелкните **Создать новое приложение**.

3. Введите **Имя**, **Описание**, **Веб-сайт**. Можно использовать URL-адрес для hello **веб-сайт** поля. Hello в следующей таблице показаны некоторые toouse пример значения:

   | Поле | Значение |
   |:--- |:--- |
   | Имя |MyHDInsightApp |
   | Описание |MyHDInsightApp |
   | Веб-сайт |http://www.myhdinsightapp.com |

4. Установите флажок **Я принимаю** и нажмите кнопку **Создать приложение Twitter**.

5. Нажмите кнопку hello **разрешений** разрешение по умолчанию hello вкладку — **только для чтения**.

6. Нажмите кнопку hello **ключей и маркеры доступа** вкладки.

7. Нажмите кнопку **Создать маркер доступа**.

8. Нажмите кнопку **OAuth теста** в правом верхнем углу hello страницы приветствия.

9. Запишите **ключ клиента**, **Секрет клиента**, **Маркер доступа** и **Секрет маркера доступа**.

### <a name="download-tweets"></a>Скачивание твитов

Следующий код Python Hello загружает 10 000 твиты из Twitter и сохраните их tooa файл с именем **tweets.txt**.

> [!NOTE]
> Hello следующие шаги выполняются на кластер HDInsight hello, так как уже установлена Python.

1. Подключите кластер HDInsight toohello с помощью SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Используйте hello следующими командами tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)и другие необходимые пакеты:

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. Используйте hello следующая команда toocreate файл с именем **gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. Используйте hello после текста как содержимое hello hello **gettweets.py** файла:

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > Замените текст заполнителя hello для следующих элементов с hello сведения из twitter приложения hello:
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. Используйте **Ctrl + X**, затем **Y** toosave hello файла.

7. Используйте следующие команды toorun hello файл hello и загрузить твиты:

    ```bash
    python gettweets.py
    ```

    Отобразится индикатор хода выполнения. Он считается hello загруженном твиты too100%.

   > [!NOTE]
   > Если это занимает много времени для tooadvance строка hello хода выполнения, следует изменить разделы тенденций tootrack фильтра hello. Если есть много твитов о разделе hello в фильтре, вы можете быстро получить hello 10000 твитов при необходимости.

### <a name="upload-hello-data"></a>Передача данных hello

tooupload hello tooHDInsight хранилища данных, hello используйте следующие команды:

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

Эти команды хранения данных hello в расположении, доступен всем узлам в кластере hello.

## <a name="run-hello-hiveql-job"></a>Запустить задание HiveQL hello

1. Используйте следующие команды toocreate файла, содержащего операторы HiveQL hello.

   ```bash
   nano twitter.hql
   ```

    Используйте hello после текста как hello содержимое файла hello.

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
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
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
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
   ```

2. Нажмите клавишу **Ctrl + X**, затем нажмите клавишу **Y** toosave hello файла.
3. Используйте hello, следующая команда hello toorun HiveQL, содержащимися в файле hello.

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    Эта команда запускает hello hello **twitter.hql** файла. После завершения выполнения запроса hello вы видите `jdbc:hive2//localhost:10001/>` строки.

4. В строке beeline hello используйте hello tooverify запроса, что данные были импортированы следующие:

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    Этот запрос возвращает не более 10 твиты, содержащих слово hello **Azure** в тексте сообщения hello.

## <a name="next-steps"></a>Дальнейшие действия

Вы узнали, каким образом tootransform набору неструктурированных данных JSON в структурированных таблицу Hive. toolearn Дополнительные сведения о Hive в HDInsight, в разделе hello следующие документы:

* [Приступая к работе с HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Анализ данных о задержке рейсов с помощью HDInsight](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
