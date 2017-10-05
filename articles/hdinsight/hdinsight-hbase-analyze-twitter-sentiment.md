---
title: "Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в Azure | Документы Майкрософт"
description: "Узнайте, как проводить анализ мнений в режиме реального времени на основе данных большого размера Twitter с помощью HBase в кластере HDInsight (Hadoop)."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5c798ad3-a20d-4385-a463-f4f7705f9566
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jgao
ms.openlocfilehash: 4d5bb90c0e7573afb75282810c9ba58e7163e127
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-real-time-twitter-sentiment-with-hbase-in-hdinsight"></a><span data-ttu-id="17ee0-103">Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="17ee0-103">Analyze real-time Twitter sentiment with HBase in HDInsight</span></span>
<span data-ttu-id="17ee0-104">Узнайте, как выполнять [анализ тональности](http://en.wikipedia.org/wiki/Sentiment_analysis) в режиме реального времени на основе больших данных Twitter, используя кластер HBase в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17ee0-104">Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data from Twitter by using a HBase cluster in HDInsight.</span></span>

<span data-ttu-id="17ee0-105">Социальные веб-сайты являются одной из основных движущих сил для внедрения данных большого размера.</span><span class="sxs-lookup"><span data-stu-id="17ee0-105">Social websites are one of the major driving forces for big data adoption.</span></span> <span data-ttu-id="17ee0-106">Общедоступные API, предоставляемые сайтами, такими как Twitter, — полезный источник данных для анализа и понимания популярных тенденций.</span><span class="sxs-lookup"><span data-stu-id="17ee0-106">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span> <span data-ttu-id="17ee0-107">В этом руководстве вы создадите консольное приложение-службу, работающее в потоковом режиме, и веб-приложение ASP.NET для выполнения следующих задач:</span><span class="sxs-lookup"><span data-stu-id="17ee0-107">In this tutorial, you develop a console streaming service application and an ASP.NET web application to perform the following:</span></span>

![Анализ мнений пользователей Twitter с использованием HBase в HDInsight][img-app-arch]

* <span data-ttu-id="17ee0-109">Приложение потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="17ee0-109">The streaming application</span></span>

  * <span data-ttu-id="17ee0-110">получение твитов с геотегами в режиме реального времени с помощью API потоковой передачи Twitter;</span><span class="sxs-lookup"><span data-stu-id="17ee0-110">get geo-tagged tweets in real time by using the Twitter streaming API</span></span>
  * <span data-ttu-id="17ee0-111">оценка мнений на основе этих твитов;</span><span class="sxs-lookup"><span data-stu-id="17ee0-111">evaluate the sentiment of these tweets</span></span>
  * <span data-ttu-id="17ee0-112">сохранение информации о мнениях в HBase с помощью пакета SDK для Microsoft HBase.</span><span class="sxs-lookup"><span data-stu-id="17ee0-112">store the sentiment information in HBase by using the Microsoft HBase SDK</span></span>
* <span data-ttu-id="17ee0-113">Приложение веб-сайтов Azure:</span><span class="sxs-lookup"><span data-stu-id="17ee0-113">The Azure Websites application</span></span>

  * <span data-ttu-id="17ee0-114">отображение статистических результатов в режиме реального времени на картах Bing с помощью веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="17ee0-114">plot the real-time statistical results on Bing maps by using an ASP.NET web application.</span></span> <span data-ttu-id="17ee0-115">Твиты визуализируются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="17ee0-115">A visualization of the tweets is similar to the following screenshot:</span></span>

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]

    <span data-ttu-id="17ee0-117">Вы можете выполнять запросы твитов, используя определенные ключевые слова, чтобы узнать, является ли выражаемое в твитах мнение в целом положительным, отрицательным или нейтральным.</span><span class="sxs-lookup"><span data-stu-id="17ee0-117">You are able to query tweets with certain keywords to get a sense of if the expressed opinion in the tweets is positive, negative, or neutral.</span></span>

<span data-ttu-id="17ee0-118">Пример готового решения Visual Studio можно найти на портале GitHub: [приложение анализа общественных мнений в реальном времени](https://github.com/maxluk/tweet-sentiment).</span><span class="sxs-lookup"><span data-stu-id="17ee0-118">A complete Visual Studio solution sample can be found on GitHub: [Realtime social sentiment analysis app](https://github.com/maxluk/tweet-sentiment).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="17ee0-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="17ee0-119">Prerequisites</span></span>
<span data-ttu-id="17ee0-120">Перед началом работы с этим учебником необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="17ee0-120">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="17ee0-121">**Кластер HBase в HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="17ee0-121">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="17ee0-122">Инструкции по созданию кластера см. в статье [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Linux в HDInsight][hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="17ee0-122">For instructions about creating clusters, see  [Get started using HBase with Hadoop in HDInsight][hbase-get-started].</span></span> 

* <span data-ttu-id="17ee0-123">**Рабочая станция**, на которой установлено программное обеспечение Visual Studio 2013/2015/2017.</span><span class="sxs-lookup"><span data-stu-id="17ee0-123">**A workstation** with Visual Studio 2013/2015/2017 installed.</span></span> <span data-ttu-id="17ee0-124">Инструкции см. в статье [Установка Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).</span><span class="sxs-lookup"><span data-stu-id="17ee0-124">For instructions, see [Installing Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).</span></span>

## <a name="create-a-twitter-application-id-and-secrets"></a><span data-ttu-id="17ee0-125">Создание идентификатора и секретов приложения Twitter</span><span class="sxs-lookup"><span data-stu-id="17ee0-125">Create a Twitter application ID and secrets</span></span>
<span data-ttu-id="17ee0-126">В интерфейсах API потоковой передачи Twitter для авторизации запросов используется протокол [OAuth](http://oauth.net/) .</span><span class="sxs-lookup"><span data-stu-id="17ee0-126">The Twitter streaming APIs use [OAuth](http://oauth.net/) to authorize requests.</span></span> <span data-ttu-id="17ee0-127">Первый шаг для начала использования OAuth состоит в создании нового приложения на сайте разработчиков Twitter.</span><span class="sxs-lookup"><span data-stu-id="17ee0-127">The first step to use OAuth is to create a new application on the Twitter developer site.</span></span>

<span data-ttu-id="17ee0-128">**Создание идентификатора и секретов приложения Twitter**</span><span class="sxs-lookup"><span data-stu-id="17ee0-128">**To create Twitter application ID and secrets**</span></span>

1. <span data-ttu-id="17ee0-129">Войдите на сайт [приложений Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="17ee0-129">Sign in to [Twitter Apps](https://apps.twitter.com/).</span></span> <span data-ttu-id="17ee0-130">Перейдите по ссылке **Войти сейчас** , если у вас нет учетной записи Twitter.</span><span class="sxs-lookup"><span data-stu-id="17ee0-130">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="17ee0-131">Щелкните **Создать новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-131">Click **Create New App**.</span></span>
3. <span data-ttu-id="17ee0-132">Введите **имя**, **описание** и **веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-132">Enter a **Name**, **Description**, and **Website**.</span></span> <span data-ttu-id="17ee0-133">Имя приложения Twitter должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="17ee0-133">The Twitter application name must be a unique name.</span></span> <span data-ttu-id="17ee0-134">Поле "Веб-сайт" на самом деле не используется.</span><span class="sxs-lookup"><span data-stu-id="17ee0-134">The Website field is not really used.</span></span> <span data-ttu-id="17ee0-135">В нем не обязательно указывать действительный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="17ee0-135">It doesn't have to be a valid URL.</span></span>
4. <span data-ttu-id="17ee0-136">Установите флажок **Я принимаю** и нажмите кнопку **Создать приложение Twitter**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-136">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="17ee0-137">Щелкните вкладку **Разрешения** и выберите **Только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-137">Click the **Permissions** tab, and then click **Read only**.</span></span> <span data-ttu-id="17ee0-138">Для работы с этим руководством достаточно разрешения только для чтения.</span><span class="sxs-lookup"><span data-stu-id="17ee0-138">The read-only permission is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="17ee0-139">Перейдите на вкладку **Ключи и токены доступа** .</span><span class="sxs-lookup"><span data-stu-id="17ee0-139">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="17ee0-140">Щелкните **Создать маркер доступа** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="17ee0-140">Click **Create my access token** on the bottom of the page.</span></span>
9. <span data-ttu-id="17ee0-141">Скопируйте значения **Consumer Key (API Key)** (Ключ клиента (ключ API)), **Consumer secret (API Secret)** (Секрет клиента (секрет API)), **Маркер доступа** и **Access token secret** (Секрет маркера доступа).</span><span class="sxs-lookup"><span data-stu-id="17ee0-141">Copy the **Consumer Key (API Key)**, **Consumer Secret (API Secret)**, **Access token**, and **Access token secret** values.</span></span> <span data-ttu-id="17ee0-142">Эти значения вам понадобятся позже при работе с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="17ee0-142">You need these values later in the tutorial.</span></span>

    > <span data-ttu-id="17ee0-143">![ПРИМЕЧАНИЕ] Кнопка теста OAuth больше не работает.</span><span class="sxs-lookup"><span data-stu-id="17ee0-143">![NOTE] The Test OAuth button does not work anymore.</span></span>

## <a name="create-twitter-streaming-service"></a><span data-ttu-id="17ee0-144">Создание службы потоковой передачи данных Twitter</span><span class="sxs-lookup"><span data-stu-id="17ee0-144">Create Twitter streaming service</span></span>
<span data-ttu-id="17ee0-145">Вам необходимо создать приложение для получения твитов, расчета оценки мнений на их основе и отправки обработанных слов из твитов в HBase.</span><span class="sxs-lookup"><span data-stu-id="17ee0-145">You need to create an application to get tweets, calculate tweet sentiment score, and send the processed tweet words to HBase.</span></span>

<span data-ttu-id="17ee0-146">**Создание приложения потоковой передачи**</span><span class="sxs-lookup"><span data-stu-id="17ee0-146">**To create the streaming application**</span></span>

1. <span data-ttu-id="17ee0-147">Откройте **Visual Studio** и создайте консольное приложение Visual C# под названием **TweetSentimentStreaming**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-147">Open **Visual Studio**, and create a Visual C# console application called **TweetSentimentStreaming**.</span></span>
2. <span data-ttu-id="17ee0-148">В **консоли диспетчера пакетов**выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="17ee0-148">From **Package Manager Console**, run the following commands:</span></span>

        Install-Package Microsoft.HBase.Client -version 0.4.2.0
        Install-Package TweetinviAPI -version 1.0.0.0

    <span data-ttu-id="17ee0-149">Эти команды установят [пакет SDK для HBase .NET](https://www.nuget.org/packages/Microsoft.HBase.Client/), представляющий собой клиентскую библиотеку для доступа к кластеру HBase, и пакет [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/), который используется для доступа к API Twitter.</span><span class="sxs-lookup"><span data-stu-id="17ee0-149">These commands install the [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is the client library to access the HBase cluster, and the [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/) package, which is used to access the Twitter API.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17ee0-150">Пример, использованный в этой статье, был проверен с помощью указанной выше версии.</span><span class="sxs-lookup"><span data-stu-id="17ee0-150">The sample used in this article has been tested using the version specified above.</span></span>  <span data-ttu-id="17ee0-151">Вы можете удалить параметр -version и установить последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="17ee0-151">You can remove the -version switch to install the latest version.</span></span>
   >
   >
3. <span data-ttu-id="17ee0-152">В **обозревателе решений** добавьте **System.Configuration** в ссылку.</span><span class="sxs-lookup"><span data-stu-id="17ee0-152">From **Solution Explorer**, add **System.Configuration** to the reference.</span></span>
4. <span data-ttu-id="17ee0-153">Добавьте в проект **HBaseWriter.cs**новый файл класса, а затем замените код следующим.</span><span class="sxs-lookup"><span data-stu-id="17ee0-153">Add a new class file to the project called **HBaseWriter.cs**, and then replace the code with the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Text;
        using System.Threading;
        using Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling;
        using org.apache.hadoop.hbase.rest.protobuf.generated;
        using Microsoft.HBase.Client;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class HBaseWriter
            {
                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "https://<Enter Your Cluster Name>.azurehdinsight.net/";
                const string HADOOPUSERNAME = "admin"; //the default name is "admin"
                const string HADOOPUSERPASSWORD = "<Enter the Hadoop User Password>";

                const string HBASETABLENAME = "tweets_by_words";
                const string COUNT_ROW_KEY = "~ROWCOUNT";
                const string COUNT_COLUMN_NAME = "d:COUNT";

                long rowCount = 0;

                // Sentiment dictionary file and the punctuation characters
                const string DICTIONARYFILENAME = @"..\..\dictionary.tsv";
                private static char[] _punctuationChars = new[] {
            ' ', '!', '\"', '#', '$', '%', '&', '\'', '(', ')', '*', '+', ',', '-', '.', '/',   //ascii 23--47
            ':', ';', '<', '=', '>', '?', '@', '[', ']', '^', '_', '`', '{', '|', '}', '~' };   //ascii 58--64 + misc.

                // For writting to HBase
                HBaseClient client;

                // a sentiment dictionary for estimate sentiment. It is loaded from a physical file.
                Dictionary<string, DictionaryItem> dictionary;

                // use multithread write
                Thread writerThread;
                Queue<ITweet> queue = new Queue<ITweet>();
                bool threadRunning = true;

                // This function connects to HBase, loads the sentiment dictionary, and starts the thread for writting.
                public HBaseWriter()
                {
                    ClusterCredentials credentials = new ClusterCredentials(new Uri(CLUSTERNAME), HADOOPUSERNAME, HADOOPUSERPASSWORD);
                    client = new HBaseClient(credentials);

                    // create the HBase table if it doesn't exist
                    if (!client.ListTablesAsync().Result.name.Contains(HBASETABLENAME))
                    {
                        TableSchema tableSchema = new TableSchema();
                        tableSchema.name = HBASETABLENAME;
                        tableSchema.columns.Add(new ColumnSchema { name = "d" });
                        client.CreateTableAsync(tableSchema).Wait();
                        Console.WriteLine("Table \"{0}\" is created.", HBASETABLENAME);
                    }

                    // Read current row count cell
                    rowCount = GetRowCount();

                    // Load sentiment dictionary from a file
                    LoadDictionary();

                    // Start a thread for writting to HBase
                    writerThread = new Thread(new ThreadStart(WriterThreadFunction));
                    writerThread.Start();
                }

                ~HBaseWriter()
                {
                    threadRunning = false;
                }

                private long GetRowCount()
                {
                    try
                    {
                        RequestOptions options = RequestOptions.GetDefaultOptions();
                        options.RetryPolicy = RetryPolicy.NoRetry;
                        var cellSet = client.GetCellsAsync(HBASETABLENAME, COUNT_ROW_KEY, null, null, options).Result;
                        if (cellSet.rows.Count != 0)
                        {
                            var countCol = cellSet.rows[0].values.Find(cell => Encoding.UTF8.GetString(cell.column) == COUNT_COLUMN_NAME);
                            if (countCol != null)
                            {
                                return Convert.ToInt64(Encoding.UTF8.GetString(countCol.data));
                            }
                        }
                    }
                    catch(Exception ex)
                    {
                        if (ex.InnerException.Message.Equals("The remote server returned an error: (404) Not Found.", StringComparison.OrdinalIgnoreCase))
                        {
                            return 0;
                        }
                        else
                        {
                            throw ex;
                        }

                    }

                    return 0;
                }

                // Enqueue the Tweets received
                public void WriteTweet(ITweet tweet)
                {
                    lock (queue)
                    {
                        queue.Enqueue(tweet);
                    }
                }

                // Load sentiment dictionary from a file
                private void LoadDictionary()
                {
                    List<string> lines = File.ReadAllLines(DICTIONARYFILENAME).ToList();
                    var items = lines.Select(line =>
                    {
                        var fields = line.Split('\t');
                        var pos = 0;
                        return new DictionaryItem
                        {
                            Type = fields[pos++],
                            Length = Convert.ToInt32(fields[pos++]),
                            Word = fields[pos++],
                            Pos = fields[pos++],
                            Stemmed = fields[pos++],
                            Polarity = fields[pos++]
                        };
                    });

                    dictionary = new Dictionary<string, DictionaryItem>();
                    foreach (var item in items)
                    {
                        if (!dictionary.Keys.Contains(item.Word))
                        {
                            dictionary.Add(item.Word, item);
                        }
                    }
                }

                // Calculate sentiment score
                private int CalcSentimentScore(string[] words)
                {
                    Int32 total = 0;
                    foreach (string word in words)
                    {
                        if (dictionary.Keys.Contains(word))
                        {
                            switch (dictionary[word].Polarity)
                            {
                                case "negative": total -= 1; break;
                                case "positive": total += 1; break;
                            }
                        }
                    }
                    if (total > 0)
                    {
                        return 1;
                    }
                    else if (total < 0)
                    {
                        return -1;
                    }
                    else
                    {
                        return 0;
                    }
                }

                // Popular a CellSet object to be written into HBase
                private void CreateTweetByWordsCells(CellSet set, ITweet tweet)
                {
                    // Split the Tweet into words
                    string[] words = tweet.Text.ToLower().Split(_punctuationChars);

                    // Calculate sentiment score base on the words
                    int sentimentScore = CalcSentimentScore(words);
                    var word_pairs = words.Take(words.Length - 1)
                                        .Select((word, idx) => string.Format("{0} {1}", word, words[idx + 1]));
                    var all_words = words.Concat(word_pairs).ToList();

                    // For each word in the Tweet add a row to the HBase table
                    foreach (string word in all_words)
                    {
                        string time_index = (ulong.MaxValue - (ulong)tweet.CreatedAt.ToBinary()).ToString().PadLeft(20) + tweet.IdStr;
                        string key = word + "_" + time_index;

                        // Create a row
                        var row = new CellSet.Row { key = Encoding.UTF8.GetBytes(key) };

                        // Add columns to the row, including Tweet identifier, language, coordinator(if available), and sentiment
                        var value = new Cell { column = Encoding.UTF8.GetBytes("d:id_str"), data = Encoding.UTF8.GetBytes(tweet.IdStr) };
                        row.values.Add(value);

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:lang"), data = Encoding.UTF8.GetBytes(tweet.Language.ToString()) };
                        row.values.Add(value);

                        if (tweet.Coordinates != null)
                        {
                            var str = tweet.Coordinates.Longitude.ToString() + "," + tweet.Coordinates.Latitude.ToString();
                            value = new Cell { column = Encoding.UTF8.GetBytes("d:coor"), data = Encoding.UTF8.GetBytes(str) };
                            row.values.Add(value);
                        }

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:sentiment"), data = Encoding.UTF8.GetBytes(sentimentScore.ToString()) };
                        row.values.Add(value);

                        set.rows.Add(row);
                    }
                }

                // Write a Tweet (CellSet) to HBase
                public void WriterThreadFunction()
                {
                    try
                    {
                        while (threadRunning)
                        {
                            if (queue.Count > 0)
                            {
                                CellSet set = new CellSet();
                                lock (queue)
                                {
                                    do
                                    {
                                        ITweet tweet = queue.Dequeue();
                                        CreateTweetByWordsCells(set, tweet);
                                    } while (queue.Count > 0);
                                }

                                // Write the Tweet by words cell set to the HBase table
                                client.StoreCellsAsync(HBASETABLENAME, set).Wait();
                                Console.WriteLine("\tRows written: {0}", set.rows.Count);
                            }
                            Thread.Sleep(100);
                        }
                    }
                    catch (Exception ex)
                    {
                        Console.WriteLine("Exception: " + ex.Message);
                    }
                }
            }
            public class DictionaryItem
            {
                public string Type { get; set; }
                public int Length { get; set; }
                public string Word { get; set; }
                public string Pos { get; set; }
                public string Stemmed { get; set; }
                public string Polarity { get; set; }
            }
        }
5. <span data-ttu-id="17ee0-154">Задайте константы в коде выше, в том числе **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD** и DICTIONARYFILENAME.</span><span class="sxs-lookup"><span data-stu-id="17ee0-154">Set the constants in the previous code, including **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD**, and DICTIONARYFILENAME.</span></span> <span data-ttu-id="17ee0-155">DICTIONARYFILENAME содержит имя и расположение файла direction.tsv.</span><span class="sxs-lookup"><span data-stu-id="17ee0-155">The DICTIONARYFILENAME is the filename and the location of the direction.tsv.</span></span>  <span data-ttu-id="17ee0-156">Этот файл можно скачать по ссылке **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-156">The file can be downloaded from **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**.</span></span> <span data-ttu-id="17ee0-157">Если вы хотите изменить имя таблицы HBase, вам необходимо соответствующим образом изменить имя таблицы в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="17ee0-157">If you want to change the HBase table name, you must change the table name in the web application accordingly.</span></span>
6. <span data-ttu-id="17ee0-158">Откройте файл **Program.cs**и замените код следующим.</span><span class="sxs-lookup"><span data-stu-id="17ee0-158">Open **Program.cs**, and replace the code with the following:</span></span>

        using System;
        using System.Diagnostics;
        using Tweetinvi;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class Program
            {
                const string TWITTERAPPACCESSTOKEN = "<Enter Twitter App Access Token>";
                const string TWITTERAPPACCESSTOKENSECRET = "<Enter Twitter Access Token Secret>";
                const string TWITTERAPPAPIKEY = "<Enter Twitter App API Key>";
                const string TWITTERAPPAPISECRET = "<Enter Twitter App API Secret>";

                static void Main(string[] args)
                {
                    Auth.SetUserCredentials(TWITTERAPPAPIKEY, TWITTERAPPAPISECRET, TWITTERAPPACCESSTOKEN, TWITTERAPPACCESSTOKENSECRET);

                    Stream_FilteredStreamExample();
                }

                private static void Stream_FilteredStreamExample()
                {
                    for (;;)
                    {
                        try
                        {
                            HBaseWriter hbase = new HBaseWriter();
                            var stream = Stream.CreateFilteredStream();
                            stream.AddLocation(new Coordinates(90, -180), new Coordinates(-90,180));

                            var tweetCount = 0;
                            var timer = Stopwatch.StartNew();

                            stream.MatchingTweetReceived += (sender, args) =>
                            {
                                tweetCount++;
                                var tweet = args.Tweet;

                                // Write Tweets to HBase
                                hbase.WriteTweet(tweet);

                                if (timer.ElapsedMilliseconds > 1000)
                                {
                                    if (tweet.Coordinates != null)
                                    {
                                        Console.ForegroundColor = ConsoleColor.Green;
                                        Console.WriteLine("\n{0}: {1} {2}", tweet.Id, tweet.Language.ToString(), tweet.Text);
                                        Console.ForegroundColor = ConsoleColor.White;
                                        Console.WriteLine("\tLocation: {0}, {1}", tweet.Coordinates.Longitude, tweet.Coordinates.Latitude);
                                    }

                                    timer.Restart();
                                    Console.WriteLine("\tTweets/sec: {0}", tweetCount);
                                    tweetCount = 0;
                                }
                            };

                            stream.StartStreamMatchingAllConditions();
                        }
                        catch (Exception ex)
                        {
                            Console.WriteLine("Exception: {0}", ex.Message);
                        }
                    }
                }

            }
        }
7. <span data-ttu-id="17ee0-159">Задайте константы, в том числе **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** и **TWITTERAPPAPISECRET**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-159">Set the constants including **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** and **TWITTERAPPAPISECRET**.</span></span>

<span data-ttu-id="17ee0-160">Чтобы запустить службу потоковой передачи, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-160">To run the streaming service, press **F5**.</span></span> <span data-ttu-id="17ee0-161">Далее представлен снимок экрана консольного приложения:</span><span class="sxs-lookup"><span data-stu-id="17ee0-161">The following is a screenshot of the console application:</span></span>

![hdinsight.hbase.twitter.sentiment.streaming.service][img-streaming-service]

<span data-ttu-id="17ee0-163">Оставьте консольное приложение потоковой передачи запущенным, пока вы занимаетесь разработкой веб-приложения. Это даст возможность собрать больше данных.</span><span class="sxs-lookup"><span data-stu-id="17ee0-163">Keep the streaming console application running while you develop the web application, so you have more data to use.</span></span> <span data-ttu-id="17ee0-164">Чтобы просмотреть данные, добавленные в таблицу, можно использовать оболочку HBase.</span><span class="sxs-lookup"><span data-stu-id="17ee0-164">To examine the data inserted into the table, you can use HBase Shell.</span></span> <span data-ttu-id="17ee0-165">См. статью [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data).</span><span class="sxs-lookup"><span data-stu-id="17ee0-165">See [Get started with HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data).</span></span>

## <a name="visualize-real-time-sentiment"></a><span data-ttu-id="17ee0-166">Визуализация мнений в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="17ee0-166">Visualize real-time sentiment</span></span>
<span data-ttu-id="17ee0-167">Этот подраздел посвящен созданию веб-приложения ASP.NET MVC для чтения мнений из HBase в режиме реального времени и отображения данных на картах Bing.</span><span class="sxs-lookup"><span data-stu-id="17ee0-167">In this section, you create an ASP.NET MVC web application to read the real-time sentiment data from HBase and plot the data on Bing maps.</span></span>

<span data-ttu-id="17ee0-168">**Создание веб-приложения ASP.NET MVC**</span><span class="sxs-lookup"><span data-stu-id="17ee0-168">**To create an ASP.NET MVC Web application**</span></span>

1. <span data-ttu-id="17ee0-169">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17ee0-169">Open Visual Studio.</span></span>
2. <span data-ttu-id="17ee0-170">В меню **Файл** выберите пункт **Создать**, а затем щелкните **Проект**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-170">Click **File**, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="17ee0-171">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="17ee0-171">Enter the following information:</span></span>

   * <span data-ttu-id="17ee0-172">Категория шаблона: **Visual C# или веб-сайт**</span><span class="sxs-lookup"><span data-stu-id="17ee0-172">Template category: **Visual C#/Web**</span></span>
   * <span data-ttu-id="17ee0-173">Шаблон: **веб-приложение ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="17ee0-173">Template: **ASP.NET Web Application**</span></span>
   * <span data-ttu-id="17ee0-174">Имя: **TweetSentimentWeb**</span><span class="sxs-lookup"><span data-stu-id="17ee0-174">Name: **TweetSentimentWeb**</span></span>
   * <span data-ttu-id="17ee0-175">Расположение: **C:\Tutorials**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-175">Location: **C:\Tutorials**</span></span>
4. <span data-ttu-id="17ee0-176">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-176">Click **OK**.</span></span>
5. <span data-ttu-id="17ee0-177">В разделе **Выбор шаблона** щелкните **MVC**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-177">In **Select a template**, click **MVC**.</span></span>
6. <span data-ttu-id="17ee0-178">В **Microsoft Azure** щелкните **Управление подписками**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-178">In **Microsoft Azure**, click **Manage Subscriptions**.</span></span>
7. <span data-ttu-id="17ee0-179">В окне **Управление подписками Microsoft Azure** щелкните **Вход**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-179">From **Manage Microsoft Azure Subscriptions**, click **Sign in**.</span></span>
8. <span data-ttu-id="17ee0-180">Введите учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="17ee0-180">Enter your Azure credentials.</span></span> <span data-ttu-id="17ee0-181">Сведения о вашей подписке Azure отображаются на вкладке **Учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-181">Your Azure subscription information is shown on the **Accounts** tab.</span></span>
9. <span data-ttu-id="17ee0-182">Щелкните **Закрыть**, чтобы закрыть окно **Управление подписками Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-182">Click **Close** to close the **Manage Microsoft Azure Subscriptions** window.</span></span>
10. <span data-ttu-id="17ee0-183">В окне **New ASP.NET Project - TweetSentimentWeb** (Новый проект ASP.NET — TweetSentimentWeb) нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-183">From **New ASP.NET Project - TweetSentimentWeb**, click **OK**.</span></span>
11. <span data-ttu-id="17ee0-184">В окне **Configure Microsoft Azure Site Settings** (Настройка параметров сайта Microsoft Azure) выберите ближайший к вам **регион**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-184">From **Configure Microsoft Azure Site Settings**, select the **Region** that is closest to you.</span></span> <span data-ttu-id="17ee0-185">Указывать сервер базы данных не нужно.</span><span class="sxs-lookup"><span data-stu-id="17ee0-185">You don't need to specify a database server.</span></span>
12. <span data-ttu-id="17ee0-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-186">Click **OK**.</span></span>

<span data-ttu-id="17ee0-187">**Установка пакетов Nuget**</span><span class="sxs-lookup"><span data-stu-id="17ee0-187">**To install NuGet packages**</span></span>

1. <span data-ttu-id="17ee0-188">В меню **Средства** щелкните **Диспетчер пакетов Nuget**, а затем щелкните **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-188">From the **Tools** menu, click **Nuget Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="17ee0-189">В нижней части страницы откроется консольная панель.</span><span class="sxs-lookup"><span data-stu-id="17ee0-189">The console panel is opened at the bottom of the page.</span></span>
2. <span data-ttu-id="17ee0-190">Используйте следующую команду, чтобы установить [пакет SDK для .NET HBase](https://www.nuget.org/packages/Microsoft.HBase.Client/) , который представляет клиентскую библиотеку для доступа к кластеру HBase:</span><span class="sxs-lookup"><span data-stu-id="17ee0-190">Use the following command to install the [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is the client library to access HBase cluster:</span></span>

        Install-Package Microsoft.HBase.Client

<span data-ttu-id="17ee0-191">**Добавление класса HBaseReader**</span><span class="sxs-lookup"><span data-stu-id="17ee0-191">**To add HBaseReader class**</span></span>

1. <span data-ttu-id="17ee0-192">В **обозревателе решений** разверните элемент **TweetSentiment**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-192">From **Solution Explorer**, expand **TweetSentiment**.</span></span>
2. <span data-ttu-id="17ee0-193">Щелкните правой кнопкой мыши элемент **Модели**, выберите пункт **Добавить** и щелкните **Класс**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-193">Right-click **Models**, click **Add**, and then click **Class**.</span></span>
3. <span data-ttu-id="17ee0-194">В поле **Имя** введите **HBaseReader.cs** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-194">In the **Name** field, type **HBaseReader.cs**, and then click **Add**.</span></span>
4. <span data-ttu-id="17ee0-195">Замените код на приведенный ниже:</span><span class="sxs-lookup"><span data-stu-id="17ee0-195">Replace the code with the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Web;

        using System.Configuration;
        using System.Threading.Tasks;
        using System.Text;
        using Microsoft.HBase.Client;
        using org.apache.hadoop.hbase.rest.protobuf.generated;

        namespace TweetSentimentWeb.Models
        {
            public class HBaseReader
            {
                // For reading Tweet sentiment data from HDInsight HBase
                HBaseClient client;

                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "<HBaseClusterName>";
                const string HADOOPUSERNAME = "<HBaseClusterHadoopUserName>"
                const string HADOOPUSERPASSWORD = "<HBaseCluserUserPassword>";
                const string HBASETABLENAME = "tweets_by_words";

                // The constructor
                public HBaseReader()
                {
                    ClusterCredentials creds = new ClusterCredentials(
                                    new Uri(CLUSTERNAME),
                                    HADOOPUSERNAME,
                                    HADOOPUSERPASSWORD);
                    client = new HBaseClient(creds);
                }

                // Query Tweets sentiment data from the HBase table asynchronously
                public async Task<IEnumerable<Tweet>> QueryTweetsByKeywordAsync(string keyword)
                {
                    List<Tweet> list = new List<Tweet>();

                    // Demonstrate Filtering the data from the past 6 hours the row key
                    string timeIndex = (ulong.MaxValue -
                        (ulong)DateTime.UtcNow.Subtract(new TimeSpan(6, 0, 0)).ToBinary()).ToString().PadLeft(20);
                    string startRow = keyword + "_" + timeIndex;
                    string endRow = keyword + "|";
                    Scanner scanSettings = new Scanner
                    {
                        batch = 100000,
                        startRow = Encoding.UTF8.GetBytes(startRow),
                        endRow = Encoding.UTF8.GetBytes(endRow)
                    };

                    // Make async scan call
                    ScannerInformation scannerInfo =
                        await client.CreateScannerAsync(HBASETABLENAME, scanSettings);

                    CellSet next;

                    while ((next = await client.ScannerGetNextAsync(scannerInfo)) != null)
                    {
                        foreach (CellSet.Row row in next.rows)
                        {
                            // find the cell with string pattern "d:coor"
                            var coordinates =
                                row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:coor");

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');

                                var sentimentField =
                                    row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:sentiment");
                                Int32 sentiment = 0;
                                if (sentimentField != null)
                                {
                                    sentiment = Convert.ToInt32(Encoding.UTF8.GetString(sentimentField.data));
                                }

                                list.Add(new Tweet
                                {
                                    Longtitude = Convert.ToDouble(lonlat[0]),
                                    Latitude = Convert.ToDouble(lonlat[1]),
                                    Sentiment = sentiment
                                });
                            }

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');
                            }
                        }
                    }

                    return list;
                }
            }

            public class Tweet
            {
                public string IdStr { get; set; }
                public string Text { get; set; }
                public string Lang { get; set; }
                public double Longtitude { get; set; }
                public double Latitude { get; set; }
                public int Sentiment { get; set; }
            }
        }
5. <span data-ttu-id="17ee0-196">В классе **HBaseReader** измените значения констант следующим образом:</span><span class="sxs-lookup"><span data-stu-id="17ee0-196">Inside the **HBaseReader** class, change the constant values as follows:</span></span>

   * <span data-ttu-id="17ee0-197">**CLUSTERNAME**: имя кластера HBase, например *https://<HBaseClusterName>.azurehdinsight.net/*.</span><span class="sxs-lookup"><span data-stu-id="17ee0-197">**CLUSTERNAME**: The HBase cluster name, for example, *https://<HBaseClusterName>.azurehdinsight.net/*.</span></span>
   * <span data-ttu-id="17ee0-198">**HADOOPUSERNAME**: имя пользователя Hadoop в кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="17ee0-198">**HADOOPUSERNAME**: The HBase cluster Hadoop user user name.</span></span> <span data-ttu-id="17ee0-199">Имя по умолчанию — *admin*.</span><span class="sxs-lookup"><span data-stu-id="17ee0-199">The default name is *admin*.</span></span>
   * <span data-ttu-id="17ee0-200">**HADOOPUSERPASSWORD**: пароль пользователя Hadoop в кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="17ee0-200">**HADOOPUSERPASSWORD**: The HBase cluster Hadoop user password.</span></span>
   * <span data-ttu-id="17ee0-201">**HBASETABLENAME**: tweets_by_words.</span><span class="sxs-lookup"><span data-stu-id="17ee0-201">**HBASETABLENAME** = "tweets_by_words";</span></span>

     <span data-ttu-id="17ee0-202">Имя таблицы HBase — **tweets_by_words**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-202">The HBase table name is **"tweets_by_words";**.</span></span> <span data-ttu-id="17ee0-203">Значения должны совпадать со значениями, отправленными в службу потоковой передачи, чтобы веб-приложение считывало данные из той же таблицы HBase.</span><span class="sxs-lookup"><span data-stu-id="17ee0-203">The values must match the values you sent in the streaming service, so that the web application reads the data from the same HBase table.</span></span>

<span data-ttu-id="17ee0-204">**Добавление контроллера TweetsController**</span><span class="sxs-lookup"><span data-stu-id="17ee0-204">**To add TweetsController controller**</span></span>

1. <span data-ttu-id="17ee0-205">В **обозревателе решений** разверните элемент **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-205">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="17ee0-206">Щелкните правой кнопкой мыши элемент **Контроллеры**, выберите пункт **Добавить**, а затем щелкните **Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-206">Right-click **Controllers**, click **Add**, and then click **Controller**.</span></span>
3. <span data-ttu-id="17ee0-207">Щелкните элемент **Контроллер Web API 2 — пустой** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-207">Click **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
4. <span data-ttu-id="17ee0-208">В поле **Имя контроллера** введите **TweetsController** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-208">In the **Controller name** field, type **TweetsController**, and then click **Add**.</span></span>
5. <span data-ttu-id="17ee0-209">В **обозревателе решений**дважды щелкните файл TweetsController.cs, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="17ee0-209">From **Solution Explorer**, double-click TweetsController.cs to open the file.</span></span>
6. <span data-ttu-id="17ee0-210">Измените файл так, чтобы он выглядел следующим образом:</span><span class="sxs-lookup"><span data-stu-id="17ee0-210">Modify the file, so it looks like the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;

        using System.Threading.Tasks;
        using TweetSentimentWeb.Models;

        namespace TweetSentimentWeb.Controllers
        {
            public class TweetsController : ApiController
            {
                HBaseReader hbase = new HBaseReader();

                public async Task<IEnumerable<Tweet>> GetTweetsByQuery(string query)
                {
                    return await hbase.QueryTweetsByKeywordAsync(query);
                }
            }
        }

<span data-ttu-id="17ee0-211">**Добавление файла heatmap.js**</span><span class="sxs-lookup"><span data-stu-id="17ee0-211">**To add heatmap.js**</span></span>

1. <span data-ttu-id="17ee0-212">В **обозревателе решений** разверните элемент **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-212">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="17ee0-213">Щелкните правой кнопкой мыши элемент **Скрипты**, выберите пункт **Добавить** и щелкните **Файл JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-213">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span></span>
3. <span data-ttu-id="17ee0-214">В поле **Имя элемента** введите **heatmap.js**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-214">In the **Item name** field, type **heatmap.js**.</span></span>
4. <span data-ttu-id="17ee0-215">Скопируйте приведенный ниже код и вставьте его в файл.</span><span class="sxs-lookup"><span data-stu-id="17ee0-215">Paste the following code into the file.</span></span> <span data-ttu-id="17ee0-216">Код был создан Аластером Эйтчисоном (Alastair Aitchison).</span><span class="sxs-lookup"><span data-stu-id="17ee0-216">The code was written by Alastair Aitchison.</span></span> <span data-ttu-id="17ee0-217">Дополнительные сведения см. в статье [Bing Maps AJAX v7 HeatMap Library](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/) (Библиотека тепловых карт AJAX вер. 7 для Карт Bing).</span><span class="sxs-lookup"><span data-stu-id="17ee0-217">For more information, see [Bing Maps AJAX v7 HeatMap Library](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/).</span></span>

        /*******************************************************************************
        * Author: Alastair Aitchison
        * Website: http://alastaira.wordpress.com
        * Date: 15th April 2011
        *
        * Description:
        * This JavaScript file provides an algorithm that can be used to add a heatmap
        * overlay on a Bing Maps v7 control. The intensity and temperature palette
        * of the heatmap are designed to be easily customisable.
        *
        * Requirements:
        * The heatmap layer itself is created dynamically on the client-side using
        * the HTML5 &lt;canvas> element, and therefore requires a browser that supports
        * this element. It has been tested on IE9, Firefox 3.6/4 and
        * Chrome 10 browsers. If you can confirm whether it works on other browsers or
        * not, I'd love to hear from you!
        *
        * Usage:
        * The HeatMapLayer constructor requires:
        * - A reference to a map object
        * - An array or Microsoft.Maps.Location items
        * - Optional parameters to customise the appearance of the layer
        *  (Radius,, Unit, Intensity, and ColourGradient), and a callback function
        */

        var HeatMapLayer = function (map, locations, options) {

            /* Private Properties */
            var _map = map,
                _canvas,
                _temperaturemap,
                _locations = [],
                _viewchangestarthandler,
                _viewchangeendhandler;

            // Set default options
            var _options = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 1000,

                // Whether the radius is an absolute pixel value or meters
                unit: 'meters',

                // Colour temperature gradient of the map
                colourgradient: {
                    "0.00": 'rgba(255,0,255,20)',  // Magenta
                    "0.25": 'rgba(0,0,255,40)',    // Blue
                    "0.50": 'rgba(0,255,0,80)',    // Green
                    "0.75": 'rgba(255,255,0,120)', // Yellow
                    "1.00": 'rgba(255,0,0,150)'    // Red
                },

                // Callback function to be fired after heatmap layer has been redrawn
                callback: null
            };

            /* Private Methods */
            function _init() {
                var _mapDiv = _map.getRootElement();

                if (_mapDiv.childNodes.length >= 3 && _mapDiv.childNodes[2].childNodes.length >= 2) {
                    // Create the canvas element
                    _canvas = document.createElement('canvas');
                    _canvas.style.position = 'relative';

                    var container = document.createElement('div');
                    container.style.position = 'absolute';
                    container.style.left = '0px';
                    container.style.top = '0px';
                    container.appendChild(_canvas);

                    _mapDiv.childNodes[2].childNodes[1].appendChild(container);

                    // Override defaults with any options passed in the constructor
                    _setOptions(options);

                    // Load array of location data
                    _setPoints(locations);

                    // Create a colour gradient from the suppied colourstops
                    _temperaturemap = _createColourGradient(_options.colourgradient);

                    // Wire up the event handler to redraw heatmap canvas
                    _viewchangestarthandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangestart', _clearHeatMap);
                    _viewchangeendhandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangeend', _createHeatMap);

                    _createHeatMap();

                    delete _init;
                } else {
                    setTimeout(_init, 100);
                }
            }

            // Resets the heat map
            function _clearHeatMap() {
                var ctx = _canvas.getContext("2d");
                ctx.clearRect(0, 0, _canvas.width, _canvas.height);
            }

            // Creates a colour gradient from supplied colour stops on initialisation
            function _createColourGradient(colourstops) {
                var ctx = document.createElement('canvas').getContext('2d');
                var grd = ctx.createLinearGradient(0, 0, 256, 0);
                for (var c in colourstops) {
                    grd.addColorStop(c, colourstops[c]);
                }
                ctx.fillStyle = grd;
                ctx.fillRect(0, 0, 256, 1);
                return ctx.getImageData(0, 0, 256, 1).data;
            }

            // Applies a colour gradient to the intensity map
            function _colouriseHeatMap() {
                var ctx = _canvas.getContext("2d");
                var dat = ctx.getImageData(0, 0, _canvas.width, _canvas.height);
                var pix = dat.data; // pix is a CanvasPixelArray containing height x width x 4 bytes of data (RGBA)
                for (var p = 0, len = pix.length; p < len;) {
                    var a = pix[p + 3] * 4; // get the alpha of this pixel
                    if (a != 0) { // If there is any data to plot
                        pix[p] = _temperaturemap[a]; // set the red value of the gradient that corresponds to this alpha
                        pix[p + 1] = _temperaturemap[a + 1]; //set the green value based on alpha
                        pix[p + 2] = _temperaturemap[a + 2]; //set the blue value based on alpha
                    }
                    p += 4; // Move on to the next pixel
                }
                ctx.putImageData(dat, 0, 0);
            }

            // Sets any options passed in
            function _setOptions(options) {
                for (attrname in options) {
                    _options[attrname] = options[attrname];
                }
            }

            // Sets the heatmap points from an array of Microsoft.Maps.Locations  
            function _setPoints(locations) {
                _locations = locations;
            }

            // Main method to draw the heatmap
            function _createHeatMap() {
                // Ensure the canvas matches the current dimensions of the map
                // This also has the effect of resetting the canvas
                _canvas.height = _map.getHeight();
                _canvas.width = _map.getWidth();

                _canvas.style.top = -_canvas.height / 2 + 'px';
                _canvas.style.left = -_canvas.width / 2 + 'px';

                // Calculate the pixel radius of each heatpoint at the current map zoom
                if (_options.unit == "pixels") {
                    radiusInPixel = _options.radius;
                } else {
                    radiusInPixel = _options.radius / _map.getMetersPerPixel();
                }

                var ctx = _canvas.getContext("2d");

                // Convert lat/long to pixel location
                var pixlocs = _map.tryLocationToPixel(_locations, Microsoft.Maps.PixelReference.control);
                var shadow = 'rgba(0, 0, 0, ' + _options.intensity + ')';
                var mapWidth = 256 * Math.pow(2, _map.getZoom());

                // Create the Intensity Map by looping through each location
                for (var i = 0, len = pixlocs.length; i < len; i++) {
                    var x = pixlocs[i].x;
                    var y = pixlocs[i].y;

                    if (x < 0) {
                        x += mapWidth * Math.ceil(Math.abs(x / mapWidth));
                    }

                    // Create radial gradient centred on this point
                    var grd = ctx.createRadialGradient(x, y, 0, x, y, radiusInPixel);
                    grd.addColorStop(0.0, shadow);
                    grd.addColorStop(1.0, 'transparent');

                    // Draw the heatpoint onto the canvas
                    ctx.fillStyle = grd;
                    ctx.fillRect(x - radiusInPixel, y - radiusInPixel, 2 * radiusInPixel, 2 * radiusInPixel);
                }

                // Apply the specified colour gradient to the intensity map
                _colouriseHeatMap();

                // Call the callback function, if specified
                if (_options.callback) {
                    _options.callback();
                }
            }

            /* Public Methods */

            this.Show = function () {
                if (_canvas) {
                    _canvas.style.display = '';
                }
            };

            this.Hide = function () {
                if (_canvas) {
                    _canvas.style.display = 'none';
                }
            };

            // Sets options for intensity, radius, colourgradient etc.
            this.SetOptions = function (options) {
                _setOptions(options);
            }

            // Sets an array of Microsoft.Maps.Locations from which the heatmap is created
            this.SetPoints = function (locations) {
                // Reset the existing heatmap layer
                _clearHeatMap();
                // Pass in the new set of locations
                _setPoints(locations);
                // Recreate the layer
                _createHeatMap();
            }

            // Removes the heatmap layer from the DOM
            this.Remove = function () {
                _canvas.parentNode.parentNode.removeChild(_canvas.parentNode);

                if (_viewchangestarthandler) { Microsoft.Maps.Events.removeHandler(_viewchangestarthandler); }
                if (_viewchangeendhandler) { Microsoft.Maps.Events.removeHandler(_viewchangeendhandler); }

                _locations = null;
                _temperaturemap = null;
                _canvas = null;
                _options = null;
                _viewchangestarthandler = null;
                _viewchangeendhandler = null;
            }

            // Call the initialisation routine
            _init();
        };

        // Call the Module Loaded method
        Microsoft.Maps.moduleLoaded('HeatMapModule');

<span data-ttu-id="17ee0-218">**Добавление файла twitterStream.js**</span><span class="sxs-lookup"><span data-stu-id="17ee0-218">**To add twitterStream.js**</span></span>

1. <span data-ttu-id="17ee0-219">В **обозревателе решений** разверните элемент **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-219">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="17ee0-220">Щелкните правой кнопкой мыши элемент **Скрипты**, выберите пункт **Добавить** и щелкните **Файл JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-220">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span></span>
3. <span data-ttu-id="17ee0-221">В поле **Имя элемента** введите **twitterStream.js**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-221">In the **Item name** field, type**twitterStream.js**.</span></span>
4. <span data-ttu-id="17ee0-222">Скопируйте следующий код и вставьте его в файл:</span><span class="sxs-lookup"><span data-stu-id="17ee0-222">Copy and paste the following code into the file:</span></span>

        var liveTweetsPos = [];
        var liveTweets = [];
        var liveTweetsNeg = [];
        var map;
        var heatmap;
        var heatmapNeg;
        var heatmapPos;

        function initialize() {
            // Initialize the map
            var options = {
                credentials: "AvFJTZPZv8l3gF8VC3Y7BPBd0r7LKo8dqKG02EAlqg9WAi0M7la6zSIT-HwkMQbx",
                center: new Microsoft.Maps.Location(23.0, 8.0),
                mapTypeId: Microsoft.Maps.MapTypeId.ordnanceSurvey,
                labelOverlay: Microsoft.Maps.LabelOverlay.hidden,
                zoom: 2.5
            };
            var map = new Microsoft.Maps.Map(document.getElementById('map_canvas'), options);

            // Heatmap options for positive, neutral and negative layers

            var heatmapOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels'
            };

            var heatmapPosOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 255, 191, 1)',
                    0.3: 'rgba(0, 255, 127, 1)',
                    0.4: 'rgba(0, 255, 63, 1)',
                    0.5: 'rgba(0, 127, 0, 1)',
                    0.7: 'rgba(0, 159, 0, 1)',
                    0.8: 'rgba(0, 191, 0, 1)',
                    0.9: 'rgba(0, 223, 0, 1)',
                    1.0: 'rgba(0, 255, 0, 1)'
                }
            };

            var heatmapNegOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 191, 255, 1)',
                    0.3: 'rgba(0, 127, 255, 1)',
                    0.4: 'rgba(0, 63, 255, 1)',
                    0.5: 'rgba(0, 0, 127, 1)',
                    0.7: 'rgba(0, 0, 159, 1)',
                    0.8: 'rgba(0, 0, 191, 1)',
                    0.9: 'rgba(0, 0, 223, 1)',
                    1.0: 'rgba(0, 0, 255, 1)'
                }
            };

            // Register and load the Client Side HeatMap Module
            Microsoft.Maps.registerModule("HeatMapModule", "scripts/heatmap.js");
            Microsoft.Maps.loadModule("HeatMapModule", {
                callback: function () {
                    // Create heatmap layers for positive, neutral and negative tweets
                    heatmapPos = new HeatMapLayer(map, liveTweetsPos, heatmapPosOptions);
                    heatmap = new HeatMapLayer(map, liveTweets, heatmapOptions);
                    heatmapNeg = new HeatMapLayer(map, liveTweetsNeg, heatmapNegOptions);
                }
            });

            $("#searchbox").val("xbox");
            $("#searchBtn").click(onsearch);
            $("#positiveBtn").click(onPositiveBtn);
            $("#negativeBtn").click(onNegativeBtn);
            $("#neutralBtn").click(onNeutralBtn);
            $("#neutralBtn").button("toggle");
        }

        function onsearch() {
            var uri = 'api/tweets?query=';
            var query = $('#searchbox').val();
            $.getJSON(uri + query)
                .done(function (data) {
                    liveTweetsPos = [];
                    liveTweets = [];
                    liveTweetsNeg = [];

                    // On success, 'data' contains a list of tweets.
                    $.each(data, function (key, item) {
                        addTweet(item);
                    });

                    if (!$("#neutralBtn").hasClass('active')) {
                        $("#neutralBtn").button("toggle");
                    }
                    onNeutralBtn();
                })
                .fail(function (jqXHR, textStatus, err) {
                    $('#statustext').text('Error: ' + err);
                });
        }

        function addTweet(item) {
            //Add tweet to the heat map arrays.
            var tweetLocation = new Microsoft.Maps.Location(item.Latitude, item.Longtitude);
            if (item.Sentiment > 0) {
                liveTweetsPos.push(tweetLocation);
            } else if (item.Sentiment < 0) {
                liveTweetsNeg.push(tweetLocation);
            } else {
                liveTweets.push(tweetLocation);
            }
        }

        function onPositiveBtn() {
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmapPos.SetPoints(liveTweetsPos);
            heatmapPos.Show();
            heatmapNeg.Hide();
            heatmap.Hide();

            $('#statustext').text('Tweets: ' + liveTweetsPos.length + "   " + getPosNegRatio());
        }

        function onNeutralBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmap.SetPoints(liveTweets);
            heatmap.Show();
            heatmapNeg.Hide();
            heatmapPos.Hide();

            $('#statustext').text('Tweets: ' + liveTweets.length + "   " + getPosNegRatio());
        }

        function onNegativeBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }

            heatmapNeg.SetPoints(liveTweetsNeg);
            heatmapNeg.Show();
            heatmap.Hide();;
            heatmapPos.Hide();;

            $('#statustext').text('Tweets: ' + liveTweetsNeg.length + "\t" + getPosNegRatio());
        }

        function getPosNegRatio() {
            if (liveTweetsNeg.length == 0) {
                return "";
            }
            else {
                var ratio = liveTweetsPos.length / liveTweetsNeg.length;
                var str = parseFloat(Math.round(ratio * 10) / 10).toFixed(1);
                return "Positive/Negative Ratio: " + str;
            }
        }

<span data-ttu-id="17ee0-223">**Изменение файла layout.cshtml**</span><span class="sxs-lookup"><span data-stu-id="17ee0-223">**To modify the layout.cshtml**</span></span>

1. <span data-ttu-id="17ee0-224">В **обозревателе решений** последовательно разверните узлы **TweetSentimentWeb**, **Представления**, **Общий ресурс**, а затем дважды щелкните элемент _**Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-224">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Shared**, and then double-click _**Layout.cshtml**.</span></span>
2. <span data-ttu-id="17ee0-225">Замените содержимое на приведенное ниже:</span><span class="sxs-lookup"><span data-stu-id="17ee0-225">Replace the content with the following:</span></span>

        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>@ViewBag.Title</title>
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
            <!-- Bing Maps -->
            <script type="text/javascript" src="http://ecn.dev.virtualearth.net/mapcontrol/mapcontrol.ashx?v=7.0&mkt=en-gb"></script>
            <!-- Spatial Dashboard JavaScript -->
            <script src="~/Scripts/twitterStream.js" type="text/javascript"></script>
        </head>
        <body onload="initialize()">
            <div class="navbar navbar-inverse navbar-fixed-top">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                    </div>
                    <div class="navbar-collapse collapse">
                        <div class="row">
                            <ul class="nav navbar-nav col-lg-5">
                                <li class="col-lg-12">
                                    <div class="navbar-form">
                                        <input id="searchbox" type="search" class="form-control">
                                        <button type="button" id="searchBtn" class="btn btn-primary">Go</button>
                                    </div>
                                </li>
                            </ul>
                            <ul class="nav navbar-nav col-lg-7">
                                <li>
                                    <div class="navbar-form">
                                        <div class="btn-group" data-toggle="buttons-radio">
                                            <button type="button" id="positiveBtn" class="btn btn-primary">Positive</button>
                                            <button type="button" id="neutralBtn" class="btn btn-primary">Neutral</button>
                                            <button type="button" id="negativeBtn" class="btn btn-primary">Negative</button>
                                        </div>
                                    </div>
                                </li>
                                <li><span id="statustext" class="navbar-text"></span></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            <div class="map_container">
                @RenderBody()
            </div>
            @Scripts.Render("~/bundles/jquery")
            @Scripts.Render("~/bundles/bootstrap")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="17ee0-226">**Изменение файла Index.cshtml**</span><span class="sxs-lookup"><span data-stu-id="17ee0-226">**To modify the Index.cshtml**</span></span>

1. <span data-ttu-id="17ee0-227">В **обозревателе решений** последовательно разверните узлы **TweetSentimentWeb**, **Представления**, **Главная**, а затем дважды щелкните элемент **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-227">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Home**, and then double-click **Index.cshtml**.</span></span>
2. <span data-ttu-id="17ee0-228">Замените содержимое на приведенное ниже:</span><span class="sxs-lookup"><span data-stu-id="17ee0-228">Replace the content with the following:</span></span>

        @{
            ViewBag.Title = "Tweet Sentiment";
        }

        <div class="map_container">
            <div id="map_canvas"/>
        </div>

<span data-ttu-id="17ee0-229">**Изменение файла site.css**</span><span class="sxs-lookup"><span data-stu-id="17ee0-229">**To modify the site.css file**</span></span>

1. <span data-ttu-id="17ee0-230">В **обозревателе решений** последовательно разверните узлы **TweetSentimentWeb** и **Содержимое**, а затем дважды щелкните элемент **Site.css**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-230">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Content**, and then double-click **Site.css**.</span></span>
2. <span data-ttu-id="17ee0-231">Добавьте в файл следующий код:</span><span class="sxs-lookup"><span data-stu-id="17ee0-231">Append the following code to the file:</span></span>

        /* make container, and thus map, 100% width */
        .map_container {
            width: 100%;
            height: 100%;
        }

        #map_canvas{
          height:100%;
        }

        #tweets{
          position: absolute;
          top: 60px;
          left: 75px;
          z-index:1000;
          font-size: 30px;
        }

<span data-ttu-id="17ee0-232">**Изменение файла global.asax**</span><span class="sxs-lookup"><span data-stu-id="17ee0-232">**To modify the global.asax file**</span></span>

1. <span data-ttu-id="17ee0-233">В **обозревателе решений** разверните узел **TweetSentimentWeb** и дважды щелкните элемент **Global.asax**.</span><span class="sxs-lookup"><span data-stu-id="17ee0-233">From **Solution Explorer**, expand **TweetSentimentWeb**, and then double-click **Global.asax**.</span></span>
2. <span data-ttu-id="17ee0-234">Добавьте следующий оператор **using** :</span><span class="sxs-lookup"><span data-stu-id="17ee0-234">Add the following **using** statement:</span></span>

        using System.Web.Http;
3. <span data-ttu-id="17ee0-235">Добавьте в функцию **Application_Start()** следующие строки:</span><span class="sxs-lookup"><span data-stu-id="17ee0-235">Add the following lines inside the **Application_Start()** function:</span></span>

        // Register API routes
        GlobalConfiguration.Configure(WebApiConfig.Register);

    <span data-ttu-id="17ee0-236">Измените регистрацию маршрутов API так, чтобы веб-контроллер API работал внутри приложения MVC.</span><span class="sxs-lookup"><span data-stu-id="17ee0-236">Modify the registration of the API routes to make the Web API controller work inside the MVC application.</span></span>

<span data-ttu-id="17ee0-237">**Запуск веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="17ee0-237">**To run the web application**</span></span>

1. <span data-ttu-id="17ee0-238">Убедитесь, что консольное приложение службы потоковой передачи выполняется, чтобы вы могли просматривать изменения в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="17ee0-238">Verify that the streaming service console application is still running so you can see the real-time changes.</span></span>
2. <span data-ttu-id="17ee0-239">Нажмите клавишу **F5** , чтобы запустить веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="17ee0-239">Press **F5** to run the web application:</span></span>

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]
3. <span data-ttu-id="17ee0-241">Введите в текстовом поле ключевое слово и нажмите кнопку **Go**(Найти).</span><span class="sxs-lookup"><span data-stu-id="17ee0-241">In the text box, enter a keyword, and then click **Go**.</span></span>  <span data-ttu-id="17ee0-242">В зависимости от того, какие данные собраны в таблице HBase, некоторые ключевые слова, возможно, не будут найдены.</span><span class="sxs-lookup"><span data-stu-id="17ee0-242">Depending on the data collected in the HBase table, some keywords might not be found.</span></span> <span data-ttu-id="17ee0-243">Попробуйте использовать распространенные ключевые слова, такие как «нравится», «xbox» и «playstation».</span><span class="sxs-lookup"><span data-stu-id="17ee0-243">Try some common keywords, such as "love," "xbox," and "playstation."</span></span>
4. <span data-ttu-id="17ee0-244">Переключитесь между категориями **Positive** (Положительное), **Neutral** (Нейтральное) и **Negative** (Отрицательное), чтобы сравнить мнения.</span><span class="sxs-lookup"><span data-stu-id="17ee0-244">Toggle among **Positive**, **Neutral**, and **Negative** to compare sentiment on the subject.</span></span>
5. <span data-ttu-id="17ee0-245">Дайте службе потоковой передачи поработать еще час, а затем выполните поиск по тому же ключевому слову и сравните результаты.</span><span class="sxs-lookup"><span data-stu-id="17ee0-245">Let the streaming service run for another hour, and then search the same keywords, and compare the results.</span></span>

<span data-ttu-id="17ee0-246">При желании вы можете также развернуть приложение на Веб-сайтах Azure.</span><span class="sxs-lookup"><span data-stu-id="17ee0-246">Optionally, you can deploy the application to Azure Websites.</span></span> <span data-ttu-id="17ee0-247">Инструкции см. в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio][website-get-started].</span><span class="sxs-lookup"><span data-stu-id="17ee0-247">For instructions, see [Get started with Azure Websites and ASP.NET][website-get-started].</span></span>

## <a name="next-steps"></a><span data-ttu-id="17ee0-248">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17ee0-248">Next Steps</span></span>
<span data-ttu-id="17ee0-249">Из этого учебника вы узнали, как получать твиты, анализировать мнения на их основе, сохранять полученные оценки мнений в HBase и представлять данные по мнениям пользователей Twitter на Картах Bing в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="17ee0-249">In this tutorial, you learned how to get tweets, analyze the sentiment of tweets, save the sentiment data to HBase, and present the real-time Twitter sentiment data to Bing maps.</span></span> <span data-ttu-id="17ee0-250">Дополнительные сведения см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="17ee0-250">To learn more, see:</span></span>

* <span data-ttu-id="17ee0-251">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="17ee0-251">[Get started with HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="17ee0-252">Настройка репликации HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="17ee0-252">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* <span data-ttu-id="17ee0-253">[Анализ данных Twitter с помощью Hadoop в HDInsight][hdinsight-analyze-twitter-data]</span><span class="sxs-lookup"><span data-stu-id="17ee0-253">[Analyze Twitter data with Hadoop in HDInsight][hdinsight-analyze-twitter-data]</span></span>
* <span data-ttu-id="17ee0-254">[Анализ данных о задержке рейсов с помощью Hive в HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="17ee0-254">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="17ee0-255">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="17ee0-255">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[website-get-started]: ../app-service-web/app-service-web-get-started-dotnet.md



[img-app-arch]: ./media/hdinsight-hbase-analyze-twitter-sentiment/AppArchitecture.png
[img-twitter-app]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterApp.png
[img-streaming-service]: ./media/hdinsight-hbase-analyze-twitter-sentiment/StreamingService.png
[img-bing-map]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterSentimentBingMap.png



[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-analyze-twitter-data]: hdinsight-analyze-twitter-data.md




[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
