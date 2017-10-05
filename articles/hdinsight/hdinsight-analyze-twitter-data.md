---
title: "Анализ данных Twitter с помощью Hadoop в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как использовать Hive для анализа данных Twitter с помощью Hadoop в HDInsight, чтобы определить частоту употребления конкретного слова."
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
ms.openlocfilehash: 711d364c36c3aba699326f4a76d42891ba3219fb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="5d145-103">Анализ данных Twitter с помощью Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5d145-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="5d145-104">Социальные веб-сайты являются одной из основных движущих сил для внедрения данных большого размера.</span><span class="sxs-lookup"><span data-stu-id="5d145-104">Social websites are one of the major driving forces for big-data adoption.</span></span> <span data-ttu-id="5d145-105">Общедоступные API, предоставляемые сайтами, такими как Twitter, — полезный источник данных для анализа и понимания популярных тенденций.</span><span class="sxs-lookup"><span data-stu-id="5d145-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="5d145-106">В этом учебнике вы будете получать твиты с помощью API потоковой передачи Twitter, а затем с помощью Apache Hive в Azure HDInsight будете получать список пользователей Twitter, отправивших большинство твитов, которые содержат определенное слово.</span><span class="sxs-lookup"><span data-stu-id="5d145-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight to get a list of Twitter users who sent the most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d145-107">Действия, описанные в этом документе, требуют наличия кластера HDInsight на основе Windows.</span><span class="sxs-lookup"><span data-stu-id="5d145-107">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="5d145-108">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5d145-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5d145-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5d145-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="5d145-110">Инструкции по работе с кластером под управлением Linux см. в статье [Анализ данных Twitter с помощью Hive в HDInsight](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5d145-110">For steps specific to a Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d145-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5d145-111">Prerequisites</span></span>
<span data-ttu-id="5d145-112">Перед началом работы с этим учебником необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="5d145-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="5d145-113">**Рабочая станция** , на которой установлена и настроена среда Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="5d145-114">Для выполнения скриптов Windows PowerShell необходимо запустить Azure PowerShell с правами администратора и задать политику выполнения *RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="5d145-114">To execute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set the execution policy to *RemoteSigned*.</span></span> <span data-ttu-id="5d145-115">Ознакомьтесь с разделом о [выполнении сценариев Windows PowerShell][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="5d145-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="5d145-116">Перед выполнением сценариев Windows PowerShell убедитесь, что вы подключены к подписке Azure, с помощью следующего командлета.</span><span class="sxs-lookup"><span data-stu-id="5d145-116">Before running Windows PowerShell scripts, make sure you are connected to your Azure subscription by using the following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="5d145-117">При наличии нескольких подписок Azure используется следующий командлет для установки текущей подписки:</span><span class="sxs-lookup"><span data-stu-id="5d145-117">If you have multiple Azure subscriptions, use the following cmdlet to set the current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="5d145-118">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="5d145-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="5d145-119">В описанных в этом документе инструкциях используются новые командлеты HDInsight, которые работают с Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5d145-119">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="5d145-120">Чтобы установить последнюю версию Azure PowerShell, выполните действия из статьи [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="5d145-120">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="5d145-121">Если у вас есть сценарии, в которые нужно добавить новые командлеты, работающие с Azure Resource Manager, см. статью [Переход к средствам разработки на основе Azure Resource Manager для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5d145-121">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="5d145-122">**Кластер Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5d145-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="5d145-123">Инструкции по подготовке кластеров см. в разделе [Приступая к работе с HDInsight][hdinsight-get-started] или [Подготовка кластеров HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="5d145-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="5d145-124">Имя кластера потребуется позже в данном учебнике.</span><span class="sxs-lookup"><span data-stu-id="5d145-124">You will need the cluster name later in the tutorial.</span></span>

<span data-ttu-id="5d145-125">В следующей таблице перечислены файлы, используемые в этом учебнике:</span><span class="sxs-lookup"><span data-stu-id="5d145-125">The following table lists the files used in this tutorial:</span></span>

| <span data-ttu-id="5d145-126">Файлы</span><span class="sxs-lookup"><span data-stu-id="5d145-126">Files</span></span> | <span data-ttu-id="5d145-127">Описание</span><span class="sxs-lookup"><span data-stu-id="5d145-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d145-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="5d145-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="5d145-129">Исходные данные для задания Hive.</span><span class="sxs-lookup"><span data-stu-id="5d145-129">The source data for the Hive job.</span></span> |
| <span data-ttu-id="5d145-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="5d145-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="5d145-131">Выходная папка для задания Hive.</span><span class="sxs-lookup"><span data-stu-id="5d145-131">The output folder for the Hive job.</span></span> <span data-ttu-id="5d145-132">Имя выходного файла задания Hive по умолчанию — **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="5d145-132">The default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="5d145-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="5d145-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="5d145-134">Файл скрипта HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5d145-134">The HiveQL script file.</span></span> |
| <span data-ttu-id="5d145-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="5d145-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="5d145-136">Состояние задания Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5d145-136">The Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="5d145-137">Получение канала Twitter</span><span class="sxs-lookup"><span data-stu-id="5d145-137">Get Twitter feed</span></span>
<span data-ttu-id="5d145-138">В этом руководстве будут использоваться [интерфейсы API потоковой передачи Twitter][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="5d145-138">In this tutorial, you will use the [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="5d145-139">В частности, вы будете использовать API [statuses/filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="5d145-139">The specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="5d145-140">Файл, содержащий 10 000 твитов, и файл сценария (рассматривается в следующем разделе) были переданы в общедоступный контейнер BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5d145-140">A file containing 10,000 tweets and the Hive script file (covered in the next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="5d145-141">Вы можете пропустить этот раздел, если хотите использовать переданные файлы.</span><span class="sxs-lookup"><span data-stu-id="5d145-141">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="5d145-142">[Данные твитов](https://dev.twitter.com/docs/platform-objects/tweets) хранятся в формате JSON в виде сложных вложенных структур.</span><span class="sxs-lookup"><span data-stu-id="5d145-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in the JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="5d145-143">Вместо того чтобы писать много строк кода с использованием обычного языка программирования, эту вложенную структуру можно преобразовать в таблицу Hive, чтобы к ней можно было отправлять запросы на SQL-подобном языке — HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5d145-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="5d145-144">Twitter использует протокол OAuth для обеспечения авторизованного доступа к API.</span><span class="sxs-lookup"><span data-stu-id="5d145-144">Twitter uses OAuth to provide authorized access to its API.</span></span> <span data-ttu-id="5d145-145">OAuth — это протокол проверки подлинности, с помощью которого пользователи разрешают приложению действовать от их имени без предоставления их паролей.</span><span class="sxs-lookup"><span data-stu-id="5d145-145">OAuth is an authentication protocol that allows users to approve applications to act on their behalf without sharing their password.</span></span> <span data-ttu-id="5d145-146">Дополнительные сведения можно найти на веб-сайте [oauth.net](http://oauth.net/) или в превосходном [руководстве по OAuth для начинающих](http://hueniverse.com/oauth/) от Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="5d145-146">More information can be found at [oauth.net](http://oauth.net/) or in the excellent [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="5d145-147">Первый шаг для начала использования OAuth состоит в создании нового приложения на сайте разработчиков Twitter.</span><span class="sxs-lookup"><span data-stu-id="5d145-147">The first step to use OAuth is to create a new application on the Twitter Developer site.</span></span>

<span data-ttu-id="5d145-148">**Создание приложения Twitter**</span><span class="sxs-lookup"><span data-stu-id="5d145-148">**To create a Twitter application**</span></span>

1. <span data-ttu-id="5d145-149">Войдите на веб-сайт [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="5d145-149">Sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="5d145-150">Щелкните ссылку **Войти сейчас** , если у вас нет учетной записи Twitter.</span><span class="sxs-lookup"><span data-stu-id="5d145-150">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="5d145-151">Щелкните **Создать новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="5d145-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="5d145-152">Введите **Имя**, **Описание**, **Веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="5d145-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="5d145-153">В поле **Веб-сайт** можно использовать URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="5d145-153">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="5d145-154">В следующей таблице приведены некоторые примеры значений:</span><span class="sxs-lookup"><span data-stu-id="5d145-154">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="5d145-155">Поле</span><span class="sxs-lookup"><span data-stu-id="5d145-155">Field</span></span> | <span data-ttu-id="5d145-156">Значение</span><span class="sxs-lookup"><span data-stu-id="5d145-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="5d145-157">Имя</span><span class="sxs-lookup"><span data-stu-id="5d145-157">Name</span></span> |<span data-ttu-id="5d145-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="5d145-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="5d145-159">Описание</span><span class="sxs-lookup"><span data-stu-id="5d145-159">Description</span></span> |<span data-ttu-id="5d145-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="5d145-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="5d145-161">Веб-сайт</span><span class="sxs-lookup"><span data-stu-id="5d145-161">Website</span></span> |<span data-ttu-id="5d145-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="5d145-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="5d145-163">Установите флажок **Я принимаю** и нажмите кнопку **Создать приложение Twitter**.</span><span class="sxs-lookup"><span data-stu-id="5d145-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="5d145-164">Выберите вкладку **Разрешения** .</span><span class="sxs-lookup"><span data-stu-id="5d145-164">Click the **Permissions** tab.</span></span> <span data-ttu-id="5d145-165">Разрешение по умолчанию: **Только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="5d145-165">The default permission is **Read only**.</span></span> <span data-ttu-id="5d145-166">Этого разрешения достаточно для данного учебника.</span><span class="sxs-lookup"><span data-stu-id="5d145-166">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="5d145-167">Перейдите на вкладку **Ключи и токены доступа** .</span><span class="sxs-lookup"><span data-stu-id="5d145-167">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="5d145-168">Нажмите кнопку **Создать маркер доступа**.</span><span class="sxs-lookup"><span data-stu-id="5d145-168">Click **Create my access token**.</span></span>
8. <span data-ttu-id="5d145-169">Нажмите кнопку **Проверить OAuth** в правом верхнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="5d145-169">Click **Test OAuth** in the upper-right corner of the page.</span></span>
9. <span data-ttu-id="5d145-170">Запишите **ключ клиента**, **Секрет клиента**, **Маркер доступа** и **Секрет маркера доступа**.</span><span class="sxs-lookup"><span data-stu-id="5d145-170">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="5d145-171">Они потребуются позже в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="5d145-171">You will need the values later in the tutorial.</span></span>

<span data-ttu-id="5d145-172">В этом учебнике для вызова веб-службы будет использоваться Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-172">In this tutorial, you will use Windows PowerShell to make the web service call.</span></span> <span data-ttu-id="5d145-173">Пример .NET C# см. в разделе [Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="5d145-173">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="5d145-174">Также можно использовать другое популярное средство, [*Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="5d145-174">The other popular tool to make web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="5d145-175">Curl можно скачать [отсюда][curl-download].</span><span class="sxs-lookup"><span data-stu-id="5d145-175">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="5d145-176">При использовании команды Curl в Windows указывайте значения параметров в двойных кавычках вместо одинарных.</span><span class="sxs-lookup"><span data-stu-id="5d145-176">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span></span>

<span data-ttu-id="5d145-177">**Получение твитов**</span><span class="sxs-lookup"><span data-stu-id="5d145-177">**To get tweets**</span></span>

1. <span data-ttu-id="5d145-178">Откройте интегрированную среду сценариев (ISE) Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-178">Open the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="5d145-179">(На начальном экране Windows 8 введите **PowerShell_ISE**, а затем щелкните **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="5d145-179">(On the Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="5d145-180">Ознакомьтесь с разделом [Запуск Windows PowerShell в Windows 8 и Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="5d145-180">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="5d145-181">Скопируйте следующий скрипт в область скриптов:</span><span class="sxs-lookup"><span data-stu-id="5d145-181">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter the HDInsight cluster name

    # Enter the OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves the tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets the tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # The script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get the default storage account name and Blob container name using the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define the Azure storage connection string ..." -ForegroundColor Green
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

    #region - Write tweets to Blob storage
    Write-Host "Write to the destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="5d145-182">Задайте первые 5-8 переменных сценария:</span><span class="sxs-lookup"><span data-stu-id="5d145-182">Set the first five to eight variables in the script:</span></span>

    <span data-ttu-id="5d145-183">Переменная</span><span class="sxs-lookup"><span data-stu-id="5d145-183">Variable</span></span>|<span data-ttu-id="5d145-184">Описание</span><span class="sxs-lookup"><span data-stu-id="5d145-184">Description</span></span>
    ---|---
    <span data-ttu-id="5d145-185">$clusterName</span><span class="sxs-lookup"><span data-stu-id="5d145-185">$clusterName</span></span>|<span data-ttu-id="5d145-186">Это имя кластера HDInsight, в котором вы хотите запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="5d145-186">This is the name of the HDInsight cluster where you want to run the application.</span></span>
    <span data-ttu-id="5d145-187">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="5d145-187">$oauth_consumer_key</span></span>|<span data-ttu-id="5d145-188">Это **ключ клиента** приложения Twitter, который вы записали ранее при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="5d145-188">This is the Twitter application **consumer key** you wrote down earlier when you created the Twitter application.</span></span>
    <span data-ttu-id="5d145-189">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="5d145-189">$oauth_consumer_secret</span></span>|<span data-ttu-id="5d145-190">Это **секрет клиента** приложения Twitter, который вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="5d145-190">This is the Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="5d145-191">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="5d145-191">$oauth_token</span></span>|<span data-ttu-id="5d145-192">Это **маркер доступа** приложения Twitter, который вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="5d145-192">This is the Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="5d145-193">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="5d145-193">$oauth_token_secret</span></span>|<span data-ttu-id="5d145-194">Это **секрет маркер доступа** приложения Twitter, который вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="5d145-194">This is the Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="5d145-195">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="5d145-195">$destBlobName</span></span>|<span data-ttu-id="5d145-196">Это имя выходной папки.</span><span class="sxs-lookup"><span data-stu-id="5d145-196">This is the output blob name.</span></span> <span data-ttu-id="5d145-197">Значение по умолчанию: **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="5d145-197">The default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="5d145-198">Если вы изменяете значение по умолчанию, то нужно будет соответствующим образом обновить скрипты Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-198">If you change the default value, you will need to update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="5d145-199">$trackString</span><span class="sxs-lookup"><span data-stu-id="5d145-199">$trackString</span></span>|<span data-ttu-id="5d145-200">Веб-служба будет возвращать твиты, связанные с этими ключевыми словами.</span><span class="sxs-lookup"><span data-stu-id="5d145-200">The web service will return tweets related to these keywords.</span></span> <span data-ttu-id="5d145-201">Значение по умолчанию: **Azure, Cloud, HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5d145-201">The default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="5d145-202">Если вы изменяете значение по умолчанию, то должны соответствующим образом обновить скрипты Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-202">If you change the default value, you will update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="5d145-203">$lineMax</span><span class="sxs-lookup"><span data-stu-id="5d145-203">$lineMax</span></span>|<span data-ttu-id="5d145-204">Это значение определяет, сколько твитов будет считывать скрипт.</span><span class="sxs-lookup"><span data-stu-id="5d145-204">The value determines how many tweets the script will read.</span></span> <span data-ttu-id="5d145-205">Чтение 100 твитов занимает около трех минут.</span><span class="sxs-lookup"><span data-stu-id="5d145-205">It takes about three minutes to read 100 tweets.</span></span> <span data-ttu-id="5d145-206">Можно задать большее число, но для загрузки потребуется больше времени.</span><span class="sxs-lookup"><span data-stu-id="5d145-206">You can set a larger number, but it will take more time to download.</span></span>

1. <span data-ttu-id="5d145-207">Нажмите клавишу **F5** для запуска скрипта.</span><span class="sxs-lookup"><span data-stu-id="5d145-207">Press **F5** to run the script.</span></span> <span data-ttu-id="5d145-208">Если у вас возникли проблемы, попробуйте выбрать все строки, а затем нажмите клавишу **F8**.</span><span class="sxs-lookup"><span data-stu-id="5d145-208">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
2. <span data-ttu-id="5d145-209">В конце выходных данных</span><span class="sxs-lookup"><span data-stu-id="5d145-209">You shall see "Complete!"</span></span> <span data-ttu-id="5d145-210">будет показана строка "Complete!".</span><span class="sxs-lookup"><span data-stu-id="5d145-210">at the end of the output.</span></span> <span data-ttu-id="5d145-211">Все сообщения об ошибках выделяются красным цветом.</span><span class="sxs-lookup"><span data-stu-id="5d145-211">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="5d145-212">В качестве проверки изучите выходной файл **/tutorials/twitter/data/tweets.txt** в хранилище BLOB-объектов Azure с помощью обозревателя хранилища Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-212">As a validation procedure, you can check the output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="5d145-213">Пример сценария Windows PowerShell для перечисления файлов см. в разделе [Использование хранилища больших двоичных объектов с HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="5d145-213">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="5d145-214">Создание скрипта HiveQL</span><span class="sxs-lookup"><span data-stu-id="5d145-214">Create HiveQL script</span></span>
<span data-ttu-id="5d145-215">С помощью Azure PowerShell можно одновременно запустить несколько инструкций HiveQL по одной за раз или упаковать инструкцию HiveQL в файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="5d145-215">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="5d145-216">В этом учебнике будет создан скрипт HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5d145-216">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="5d145-217">Этот файл скрипта необходимо отправить в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5d145-217">The script file must be uploaded to Azure Blob storage.</span></span> <span data-ttu-id="5d145-218">В следующем разделе вы будете выполнять файл скрипта с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-218">In the next section, you will run the script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="5d145-219">Файл сценария и файл, содержащий 10 000 твитов, были переданы в общедоступный контейнер BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5d145-219">The Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="5d145-220">Вы можете пропустить этот раздел, если хотите использовать переданные файлы.</span><span class="sxs-lookup"><span data-stu-id="5d145-220">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="5d145-221">Скрипт HiveQL выполнит следующее:</span><span class="sxs-lookup"><span data-stu-id="5d145-221">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="5d145-222">**Удалит таблицу tweets_raw**, если она уже существует.</span><span class="sxs-lookup"><span data-stu-id="5d145-222">**Drop the tweets_raw table** in case the table already exists.</span></span>
2. <span data-ttu-id="5d145-223">**Создаст таблицу Hive tweets_raw**.</span><span class="sxs-lookup"><span data-stu-id="5d145-223">**Create the tweets_raw Hive table**.</span></span> <span data-ttu-id="5d145-224">Эта временная структурированная таблица Hive содержит данные для дальнейшей обработки операций ETL (извлечения, преобразования и загрузки).</span><span class="sxs-lookup"><span data-stu-id="5d145-224">This temporary Hive structured table holds the data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="5d145-225">Сведения о секциях см. в [руководстве по Hive][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="5d145-225">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="5d145-226">**Загрузит данные** из исходной папки /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="5d145-226">**Load data** from the source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="5d145-227">Большой набор данных tweets во вложенном формате JSON теперь преобразован во временную табличную структуру Hive.</span><span class="sxs-lookup"><span data-stu-id="5d145-227">The large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="5d145-228">**Удаляет таблицу tweets** , если она уже существует.</span><span class="sxs-lookup"><span data-stu-id="5d145-228">**Drop the tweets table** in case the table already exists.</span></span>
5. <span data-ttu-id="5d145-229">**Создает таблицу tweets**.</span><span class="sxs-lookup"><span data-stu-id="5d145-229">**Create the tweets table**.</span></span> <span data-ttu-id="5d145-230">Прежде чем выполнять запросы в набор данных tweets с помощью Hive, необходимо запустить другой процесс ETL.</span><span class="sxs-lookup"><span data-stu-id="5d145-230">Before you can query against the tweets dataset by using Hive, you need to run another ETL process.</span></span> <span data-ttu-id="5d145-231">Он определяет более подробную схему таблицы для данных, которые хранятся в таблице twitter_raw.</span><span class="sxs-lookup"><span data-stu-id="5d145-231">This ETL process defines a more detailed table schema for the data that you have stored in the "twitter_raw" table.</span></span>
6. <span data-ttu-id="5d145-232">**Вставляет таблицу для перезаписи**.</span><span class="sxs-lookup"><span data-stu-id="5d145-232">**Insert overwrite table**.</span></span> <span data-ttu-id="5d145-233">Этот сложный скрипт Hive запускает ряд длительных заданий MapReduce в кластере Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5d145-233">This complex Hive script will kick off a set of long MapReduce jobs by the Hadoop cluster.</span></span> <span data-ttu-id="5d145-234">В зависимости от набора данных и размера кластера процесс может занять около 10 минут.</span><span class="sxs-lookup"><span data-stu-id="5d145-234">Depending on your dataset and the size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="5d145-235">**Вставляет каталог для перезаписи**.</span><span class="sxs-lookup"><span data-stu-id="5d145-235">**Insert overwrite directory**.</span></span> <span data-ttu-id="5d145-236">Выполняет запрос и выводит набор данных в файл.</span><span class="sxs-lookup"><span data-stu-id="5d145-236">Run a query and output the dataset to a file.</span></span> <span data-ttu-id="5d145-237">Этот запрос возвращает список пользователей Twitter, которые отправили больше всего твитов со словом Azure.</span><span class="sxs-lookup"><span data-stu-id="5d145-237">This query will return a list of Twitter users who sent most tweets that contained the word "Azure".</span></span>

<span data-ttu-id="5d145-238">**Создание скрипта Hive и его отправка в Azure**</span><span class="sxs-lookup"><span data-stu-id="5d145-238">**To create a Hive script and upload it to Azure**</span></span>

1. <span data-ttu-id="5d145-239">Откройте интегрированную среду сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-239">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="5d145-240">Скопируйте следующий скрипт в область скриптов:</span><span class="sxs-lookup"><span data-stu-id="5d145-240">Copy the following script into the script pane:</span></span>

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing the Hive script file
    Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define the connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing the hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write the Hive script file to Blob storage
    Write-Host "Write to the destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="5d145-241">Задайте первые две переменные скрипта:</span><span class="sxs-lookup"><span data-stu-id="5d145-241">Set the first two variables in the script:</span></span>

   | <span data-ttu-id="5d145-242">Переменная</span><span class="sxs-lookup"><span data-stu-id="5d145-242">Variable</span></span> | <span data-ttu-id="5d145-243">Описание</span><span class="sxs-lookup"><span data-stu-id="5d145-243">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="5d145-244">$clusterName</span><span class="sxs-lookup"><span data-stu-id="5d145-244">$clusterName</span></span> |<span data-ttu-id="5d145-245">Введите имя кластера HDInsight, в котором вы хотите запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="5d145-245">Enter the HDInsight cluster name where you want to run the application.</span></span> |
   |  <span data-ttu-id="5d145-246">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="5d145-246">$subscriptionID</span></span> |<span data-ttu-id="5d145-247">Введите идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5d145-247">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="5d145-248">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="5d145-248">$sourceDataPath</span></span> |<span data-ttu-id="5d145-249">Расположение хранилища больших двоичных объектов Azure, из которого запросы Hive будут считывать данные.</span><span class="sxs-lookup"><span data-stu-id="5d145-249">The Azure Blob storage location where the Hive queries will read the data from.</span></span> <span data-ttu-id="5d145-250">Нет необходимости изменять эту переменную.</span><span class="sxs-lookup"><span data-stu-id="5d145-250">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="5d145-251">$outputPath</span><span class="sxs-lookup"><span data-stu-id="5d145-251">$outputPath</span></span> |<span data-ttu-id="5d145-252">Расположение хранилища больших двоичных объектов Azure, куда запросы Hive будут выводить результаты.</span><span class="sxs-lookup"><span data-stu-id="5d145-252">The Azure Blob storage location where the Hive queries will output the results.</span></span> <span data-ttu-id="5d145-253">Нет необходимости изменять эту переменную.</span><span class="sxs-lookup"><span data-stu-id="5d145-253">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="5d145-254">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="5d145-254">$hqlScriptFile</span></span> |<span data-ttu-id="5d145-255">Расположение и имя файла скрипта HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5d145-255">The location and the file name of the HiveQL script file.</span></span> <span data-ttu-id="5d145-256">Нет необходимости изменять эту переменную.</span><span class="sxs-lookup"><span data-stu-id="5d145-256">You don't need to change this variable.</span></span> |
4. <span data-ttu-id="5d145-257">Нажмите клавишу **F5** для запуска скрипта.</span><span class="sxs-lookup"><span data-stu-id="5d145-257">Press **F5** to run the script.</span></span> <span data-ttu-id="5d145-258">Если у вас возникли проблемы, попробуйте выбрать все строки, а затем нажмите клавишу **F8**.</span><span class="sxs-lookup"><span data-stu-id="5d145-258">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
5. <span data-ttu-id="5d145-259">В конце выходных данных</span><span class="sxs-lookup"><span data-stu-id="5d145-259">You shall see "Complete!"</span></span> <span data-ttu-id="5d145-260">будет показана строка "Complete!".</span><span class="sxs-lookup"><span data-stu-id="5d145-260">at the end of the output.</span></span> <span data-ttu-id="5d145-261">Все сообщения об ошибке выделяются красным цветом.</span><span class="sxs-lookup"><span data-stu-id="5d145-261">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="5d145-262">В качестве проверки можно изучить выходной файл **/tutorials/twitter/twitter.hql** в хранилище BLOB-объектов Azure с помощью обозревателя хранилища Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d145-262">As a validation procedure, you can check the output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="5d145-263">Пример сценария Windows PowerShell для перечисления файлов см. в разделе [Использование хранилища больших двоичных объектов с HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="5d145-263">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="5d145-264">Обработка данных Twitter с помощью Hive</span><span class="sxs-lookup"><span data-stu-id="5d145-264">Process Twitter data by using Hive</span></span>
<span data-ttu-id="5d145-265">Подготовительная работа завершена.</span><span class="sxs-lookup"><span data-stu-id="5d145-265">You have finished all the preparation work.</span></span> <span data-ttu-id="5d145-266">Теперь можно вызвать скрипт Hive и проверить результаты.</span><span class="sxs-lookup"><span data-stu-id="5d145-266">Now, you can invoke the Hive script and check the results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="5d145-267">Отправка задания Hive</span><span class="sxs-lookup"><span data-stu-id="5d145-267">Submit a Hive job</span></span>
<span data-ttu-id="5d145-268">Используйте приведенный ниже скрипт Windows PowerShell для запуска скрипта Hive.</span><span class="sxs-lookup"><span data-stu-id="5d145-268">Use the following Windows PowerShell script to run the Hive script.</span></span> <span data-ttu-id="5d145-269">Вам потребуется задать первую переменную.</span><span class="sxs-lookup"><span data-stu-id="5d145-269">You will need to set the first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="5d145-270">Чтобы использовать tweets и скрипт HiveQL, загруженный в последних двух разделах, установите для переменной $hqlScriptFile значение /tutorials/twitter/twitter.hql.</span><span class="sxs-lookup"><span data-stu-id="5d145-270">To use the tweets and the HiveQL script you uploaded in the last two sections, set $hqlScriptFile to "/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="5d145-271">Чтобы использовать те, которые были переданы в общедоступный большой двоичный объект, установите для переменной $hqlScriptFile значение wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql.</span><span class="sxs-lookup"><span data-stu-id="5d145-271">To use the ones that have been uploaded to a public blob for you, set $hqlScriptFile to "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of the following
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

# Create the HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display the standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-the-results"></a><span data-ttu-id="5d145-272">Проверка результатов</span><span class="sxs-lookup"><span data-stu-id="5d145-272">Check the results</span></span>
<span data-ttu-id="5d145-273">Используйте приведенный ниже скрипт Windows PowerShell для проверки результатов выполнения задания Hive.</span><span class="sxs-lookup"><span data-stu-id="5d145-273">Use the following Windows PowerShell script to check the Hive job output.</span></span> <span data-ttu-id="5d145-274">Вам потребуется задать две первые переменные.</span><span class="sxs-lookup"><span data-stu-id="5d145-274">You will need to set the first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # The name of the blob to be downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
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
Write-Host "Download the blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display the output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> Таблица Hive использует в качестве разделителя полей \001. <span data-ttu-id="5d145-276">Разделитель не отображается в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5d145-276">The delimiter is not visible in the output.</span></span>

<span data-ttu-id="5d145-277">После размещения результатов анализа в хранилище больших двоичных объектов Azure можно экспортировать данные в базу данных SQL Azure или на сервер SQL Server, экспортировать данные в Excel с помощью Power Query или подключить приложение к данным с помощью драйвера Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="5d145-277">After the analysis results have been placed in Azure Blob storage, you can export the data to an Azure SQL database/SQL server, export the data to Excel by using Power Query, or connect your application to the data by using the Hive ODBC Driver.</span></span> <span data-ttu-id="5d145-278">Дополнительные сведения см. в статьях [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop], [Анализ данных о задержке рейсов с помощью Hive в HDInsight][hdinsight-analyze-flight-delay-data], [Подключение Excel к HDInsight с помощью Power Query][hdinsight-power-query] и [Подключение Excel к HDInsight с помощью драйвера Microsoft Hive ODBC][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="5d145-278">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel to HDInsight with Power Query][hdinsight-power-query], and [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d145-279">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d145-279">Next steps</span></span>
<span data-ttu-id="5d145-280">В этом учебнике мы рассмотрели, как преобразовать неструктурированный набор данных JSON в структурированную таблицу Hive для запроса, исследования и анализа данных из Twitter с помощью HDInsight в Azure.</span><span class="sxs-lookup"><span data-stu-id="5d145-280">In this tutorial we have seen how to transform an unstructured JSON dataset into a structured Hive table to query, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="5d145-281">Дополнительные сведения см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="5d145-281">To learn more, see:</span></span>

* <span data-ttu-id="5d145-282">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="5d145-282">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="5d145-283">[Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="5d145-283">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="5d145-284">[Анализ данных о задержке рейсов с помощью Hive в HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="5d145-284">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="5d145-285">[Подключение Excel к HDInsight с помощью Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="5d145-285">[Connect Excel to HDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="5d145-286">[Подключение Excel к HDInsight с помощью драйвера Microsoft Hive ODBC][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="5d145-286">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="5d145-287">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="5d145-287">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
