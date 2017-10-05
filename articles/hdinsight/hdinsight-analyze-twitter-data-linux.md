---
title: "Анализ данных Twitter с помощью Apache Hive в Azure HDInsight | Документация Майкрософт"
description: "Сведения о преобразовании необработанных данных Twitter в поддерживающую поиск таблицу Hive с помощью Hive и Hadoop в HDInsight."
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
ms.openlocfilehash: b8656123fa9c5158f366872ab050f370080ec18a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="8f6e1-103">Анализ данных Twitter с помощью Hive и Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f6e1-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="8f6e1-104">В этой статье показано, как обрабатывать данные Twitter с помощью Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-104">Learn how to use Apache Hive to process Twitter data.</span></span> <span data-ttu-id="8f6e1-105">Результатом является список пользователей Twitter, отправивших большинство твитов, которые содержат определенное слово.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-105">The result is a list of Twitter users who sent the most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f6e1-106">Действия, описанные в этом документе, были протестированы в HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-106">The steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="8f6e1-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8f6e1-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8f6e1-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-the-data"></a><span data-ttu-id="8f6e1-109">Получение данных</span><span class="sxs-lookup"><span data-stu-id="8f6e1-109">Get the data</span></span>

<span data-ttu-id="8f6e1-110">Twitter позволяет получать [данные для каждого твита](https://dev.twitter.com/docs/platform-objects/tweets) в виде документа JavaScript Object Notation (JSON) с помощью интерфейса REST API.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-110">Twitter allows you to retrieve the [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="8f6e1-111">[OAuth](http://oauth.net) .</span><span class="sxs-lookup"><span data-stu-id="8f6e1-111">[OAuth](http://oauth.net) is required for authentication to the API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="8f6e1-112">Создание приложения Twitter</span><span class="sxs-lookup"><span data-stu-id="8f6e1-112">Create a Twitter application</span></span>

1. <span data-ttu-id="8f6e1-113">С помощью браузера войдите на веб-сайт [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="8f6e1-113">From a web browser, sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="8f6e1-114">Щелкните ссылку **Зарегистрируйтесь прямо сейчас**, если у вас нет учетной записи Twitter.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-114">Click the **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="8f6e1-115">Щелкните **Создать новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="8f6e1-116">Введите **Имя**, **Описание**, **Веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="8f6e1-117">В поле **Веб-сайт** можно использовать URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-117">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="8f6e1-118">В следующей таблице приведены некоторые примеры значений:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-118">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="8f6e1-119">Поле</span><span class="sxs-lookup"><span data-stu-id="8f6e1-119">Field</span></span> | <span data-ttu-id="8f6e1-120">Значение</span><span class="sxs-lookup"><span data-stu-id="8f6e1-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="8f6e1-121">Имя</span><span class="sxs-lookup"><span data-stu-id="8f6e1-121">Name</span></span> |<span data-ttu-id="8f6e1-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="8f6e1-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="8f6e1-123">Описание</span><span class="sxs-lookup"><span data-stu-id="8f6e1-123">Description</span></span> |<span data-ttu-id="8f6e1-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="8f6e1-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="8f6e1-125">Веб-сайт</span><span class="sxs-lookup"><span data-stu-id="8f6e1-125">Website</span></span> |<span data-ttu-id="8f6e1-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="8f6e1-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="8f6e1-127">Установите флажок **Я принимаю** и нажмите кнопку **Создать приложение Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="8f6e1-128">Выберите вкладку **Разрешения** . Разрешение по умолчанию: **Только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-128">Click the **Permissions** tab. The default permission is **Read only**.</span></span>

6. <span data-ttu-id="8f6e1-129">Перейдите на вкладку **Ключи и токены доступа** .</span><span class="sxs-lookup"><span data-stu-id="8f6e1-129">Click the **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="8f6e1-130">Нажмите кнопку **Создать маркер доступа**.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="8f6e1-131">Нажмите кнопку **Проверить OAuth** в правом верхнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-131">Click **Test OAuth** in the upper-right corner of the page.</span></span>

9. <span data-ttu-id="8f6e1-132">Запишите **ключ клиента**, **Секрет клиента**, **Маркер доступа** и **Секрет маркера доступа**.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="8f6e1-133">Скачивание твитов</span><span class="sxs-lookup"><span data-stu-id="8f6e1-133">Download tweets</span></span>

<span data-ttu-id="8f6e1-134">Следующий код Python скачивает 10 000 твитов из Twitter и сохраняет их в файл с именем **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-134">The following Python code downloads 10,000 tweets from Twitter and save them to a file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6e1-135">Так как Python уже установлен, в кластере HDInsight выполняются следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-135">The following steps are performed on the HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="8f6e1-136">Подключитесь к кластеру HDInsight с помощью протокола SSH:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-136">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="8f6e1-137">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8f6e1-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="8f6e1-138">Чтобы установить [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2) и другие необходимые пакеты, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-138">Use the following commands to install [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

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

4. <span data-ttu-id="8f6e1-139">Создайте файл **gettweets.py** с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-139">Use the following command to create a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="8f6e1-140">В качестве содержимого файла **gettweets.py** используйте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-140">Use the following text as the contents of the **gettweets.py** file:</span></span>

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

   #The number of tweets we want to get
   max_tweets=10000

   #Create the listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set the counter to zero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append the tweet to the 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment the number of tweets
               self.num_tweets += 1
               #Check to see if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment the progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get the OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use the listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="8f6e1-141">Вместо замещающего текста в следующих элементах введите данные из своего приложения Twitter:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-141">Replace the placeholder text for the following items with the information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="8f6e1-142">Нажмите клавиши **Ctrl + X**, а затем **Y** (Да) для сохранения файла.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-142">Use **Ctrl + X**, then **Y** to save the file.</span></span>

7. <span data-ttu-id="8f6e1-143">Чтобы запустить файл и скачать твиты, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-143">Use the following command to run the file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="8f6e1-144">Отобразится индикатор хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-144">A progress indicator appears.</span></span> <span data-ttu-id="8f6e1-145">Он дойдет до 100 % по мере скачивания твитов.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-145">It counts up to 100% as the tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f6e1-146">Если индикатор хода выполнения перемещается очень медленно, то следует изменить фильтр, чтобы отслеживать популярные темы.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-146">If it is taking a long time for the progress bar to advance, you should change the filter to track trending topics.</span></span> <span data-ttu-id="8f6e1-147">При наличии множества доступных твитов по отфильтровываемой теме вы сможете быстро получить 10 000 необходимых записей.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-147">When there are many tweets about the topic in your filter, you can quickly get the 10000 tweets needed.</span></span>

### <a name="upload-the-data"></a><span data-ttu-id="8f6e1-148">Передача данных</span><span class="sxs-lookup"><span data-stu-id="8f6e1-148">Upload the data</span></span>

<span data-ttu-id="8f6e1-149">Для отправки данных в хранилище HDInsight используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-149">To upload the data to HDInsight storage, use the following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="8f6e1-150">Эти команды сохраняют данные в расположении, к которому могут обращаться все узлы в кластере.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-150">These commands store the data in a location that all nodes in the cluster can access.</span></span>

## <a name="run-the-hiveql-job"></a><span data-ttu-id="8f6e1-151">Выполнение задания HiveQL</span><span class="sxs-lookup"><span data-stu-id="8f6e1-151">Run the HiveQL job</span></span>

1. <span data-ttu-id="8f6e1-152">Используйте следующую команду, чтобы создать файл, содержащий инструкции HiveQL:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-152">Use the following command to create a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="8f6e1-153">В качестве содержимого файла добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-153">Use the following text as the contents of the file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward the tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate the destination table
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
   -- Select tweets from the imported data, parse the JSON,
   -- and insert into the tweets table
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

2. <span data-ttu-id="8f6e1-154">Нажмите клавиши **Ctrl + X**, а затем **Y** (Да) для сохранения файла.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-154">Press **Ctrl + X**, then press **Y** to save the file.</span></span>
3. <span data-ttu-id="8f6e1-155">Выполните приведенную ниже команду, чтобы запустить код HiveQL в файле:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-155">Use the following command to run the HiveQL contained in the file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="8f6e1-156">Эта команда запускает файл **twitter.hql**.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-156">This command runs the the **twitter.hql** file.</span></span> <span data-ttu-id="8f6e1-157">После выполнения запроса отобразится строка `jdbc:hive2//localhost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-157">Once the query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="8f6e1-158">Используйте следующий запрос в командной строке Beeline, чтобы убедиться, что данные импортированы:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-158">From the beeline prompt, use the following query to verify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="8f6e1-159">Этот запрос возвращает не более 10 твитов, содержащих слово **Azure** в тексте сообщения.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-159">This query returns a maximum of 10 tweets that contain the word **Azure** in the message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f6e1-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f6e1-160">Next steps</span></span>

<span data-ttu-id="8f6e1-161">Мы рассмотрели, как преобразовать неструктурированный набор данных JSON в структурированную таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="8f6e1-161">You have learned how to transform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="8f6e1-162">Дополнительные сведения о Hive в HDInsight см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="8f6e1-162">To learn more about Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="8f6e1-163">Приступая к работе с HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f6e1-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="8f6e1-164">Анализ данных о задержке рейсов с помощью HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f6e1-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
