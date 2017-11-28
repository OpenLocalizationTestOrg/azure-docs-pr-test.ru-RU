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
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="8a8a8-103">Анализ данных Twitter с помощью Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="8a8a8-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="8a8a8-104">Социальных веб-узлы, одним из основных факторов определяющим hello внедрения больших данных.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="8a8a8-105">Общедоступные API, предоставляемые сайтами, такими как Twitter, — полезный источник данных для анализа и понимания популярных тенденций.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="8a8a8-106">В этом учебнике будет получение твитов с помощью Twitter, потоковая передача API и затем с помощью Apache Hive для Azure HDInsight tooget список пользователей Twitter, отправленных hello большинство твиты, содержащих определенные слова.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a8a8-107">Hello в данном пошаговом руководстве требуется кластер HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="8a8a8-108">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8a8a8-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8a8a8-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="8a8a8-110">Для кластера под управлением Linux tooa определенные действия в разделе [Twitter анализ данных с помощью Hive в HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8a8a8-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a8a8-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8a8a8-111">Prerequisites</span></span>
<span data-ttu-id="8a8a8-112">Прежде чем начать работу с учебником, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="8a8a8-113">**Рабочая станция** , на которой установлена и настроена среда Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="8a8a8-114">tooexecute сценариев Windows PowerShell, необходимо запустить Azure PowerShell от имени администратора и задать политику выполнения hello слишком*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="8a8a8-115">Ознакомьтесь с разделом о [выполнении сценариев Windows PowerShell][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="8a8a8-116">Перед выполнением скриптов Windows PowerShell, убедитесь, что вы являетесь tooyour подключенных подписка Azure с помощью hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="8a8a8-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="8a8a8-117">Если у вас несколько подписок Azure, используйте hello, выполнив командлет tooset hello текущей подписки.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="8a8a8-118">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="8a8a8-119">шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="8a8a8-120">Выполните шаги hello в [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="8a8a8-121">При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="8a8a8-122">**Кластер Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="8a8a8-123">Инструкции по подготовке кластеров см. в разделе [Приступая к работе с HDInsight][hdinsight-get-started] или [Подготовка кластеров HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="8a8a8-124">Имя кластера hello потребуется далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="8a8a8-125">Hello следующей таблице перечислены файлы hello, используемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="8a8a8-126">Файлы</span><span class="sxs-lookup"><span data-stu-id="8a8a8-126">Files</span></span> | <span data-ttu-id="8a8a8-127">Описание</span><span class="sxs-lookup"><span data-stu-id="8a8a8-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a8a8-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="8a8a8-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="8a8a8-129">Hello исходные данные для задания Hive hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="8a8a8-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="8a8a8-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="8a8a8-131">Hello для задания Hive hello выходную папку.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="8a8a8-132">Hello имя выходного файла задания Hive по умолчанию — **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="8a8a8-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="8a8a8-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="8a8a8-134">файл скрипта HiveQL Hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="8a8a8-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="8a8a8-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="8a8a8-136">Здравствуйте, состояние задания Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="8a8a8-137">Получение канала Twitter</span><span class="sxs-lookup"><span data-stu-id="8a8a8-137">Get Twitter feed</span></span>
<span data-ttu-id="8a8a8-138">В этом учебнике будет использоваться hello [Twitter потоковой передачи API-интерфейсы][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="8a8a8-139">Hello конкретных Twitter, потоковая передача будет использовать API — [состояния и фильтрации][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="8a8a8-140">Файл, содержащий 10 000 твитов и (рассматривается в следующем разделе hello) файл скрипта Hive hello были переданы в открытый контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="8a8a8-141">Этот раздел можно пропустить, если toouse hello отправлены файлы.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="8a8a8-142">[Твиты данных](https://dev.twitter.com/docs/platform-objects/tweets) хранятся в формате JavaScript Object Notation (JSON) hello, содержащий сложных вложенной структуры.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="8a8a8-143">Вместо того чтобы писать много строк кода с использованием обычного языка программирования, эту вложенную структуру можно преобразовать в таблицу Hive, чтобы к ней можно было отправлять запросы на SQL-подобном языке — HiveQL.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="8a8a8-144">Twitter использует OAuth tooprovide право доступа tooits API.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="8a8a8-145">OAuth является протоколом проверки подлинности, позволяющий пользователям tooapprove приложений tooact от их имени без пароля для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="8a8a8-146">Дополнительные сведения можно найти по [oauth.net](http://oauth.net/) или в hello отлично [tooOAuth руководство для начинающих](http://hueniverse.com/oauth/) из Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="8a8a8-147">Hello первый шаг toouse OAuth является toocreate новое приложение на сайте разработчика Twitter hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="8a8a8-148">**toocreate приложения Twitter**</span><span class="sxs-lookup"><span data-stu-id="8a8a8-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="8a8a8-149">Войдите в слишком[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="8a8a8-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="8a8a8-150">Нажмите кнопку hello **Зарегистрируйтесь сейчас** ссылку, если у вас нет учетной записи Twitter.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="8a8a8-151">Щелкните **Создать новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="8a8a8-152">Введите **Имя**, **Описание**, **Веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="8a8a8-153">Можно использовать URL-адрес для hello **веб-сайт** поля.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="8a8a8-154">Hello в следующей таблице показаны некоторые toouse пример значения:</span><span class="sxs-lookup"><span data-stu-id="8a8a8-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="8a8a8-155">Поле</span><span class="sxs-lookup"><span data-stu-id="8a8a8-155">Field</span></span> | <span data-ttu-id="8a8a8-156">Значение</span><span class="sxs-lookup"><span data-stu-id="8a8a8-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="8a8a8-157">Имя</span><span class="sxs-lookup"><span data-stu-id="8a8a8-157">Name</span></span> |<span data-ttu-id="8a8a8-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="8a8a8-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="8a8a8-159">Описание</span><span class="sxs-lookup"><span data-stu-id="8a8a8-159">Description</span></span> |<span data-ttu-id="8a8a8-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="8a8a8-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="8a8a8-161">Веб-сайт</span><span class="sxs-lookup"><span data-stu-id="8a8a8-161">Website</span></span> |<span data-ttu-id="8a8a8-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="8a8a8-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="8a8a8-163">Установите флажок **Я принимаю** и нажмите кнопку **Создать приложение Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="8a8a8-164">Нажмите кнопку hello **разрешений** разрешение по умолчанию hello вкладку — **только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="8a8a8-165">Этого разрешения достаточно для данного учебника.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="8a8a8-166">Нажмите кнопку hello **ключей и маркеры доступа** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="8a8a8-167">Нажмите кнопку **Создать маркер доступа**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="8a8a8-168">Нажмите кнопку **OAuth теста** в правом верхнем углу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="8a8a8-169">Запишите **ключ клиента**, **Секрет клиента**, **Маркер доступа** и **Секрет маркера доступа**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="8a8a8-170">Вам потребуются значения hello далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="8a8a8-171">В этом учебнике будет использоваться Windows PowerShell toomake hello в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="8a8a8-172">Пример .NET C# см. в разделе [Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="8a8a8-173">Hello вызовов веб-служб других популярным средством toomake — [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="8a8a8-174">Curl можно скачать [отсюда][curl-download].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="8a8a8-175">При использовании команды перелистывание hello в Windows, используйте двойные кавычки вместо одинарные кавычки для значений параметра hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="8a8a8-176">**твиты tooget**</span><span class="sxs-lookup"><span data-stu-id="8a8a8-176">**tooget tweets**</span></span>

1. <span data-ttu-id="8a8a8-177">Откройте hello Сценариев Windows PowerShell интегрированной среде ().</span><span class="sxs-lookup"><span data-stu-id="8a8a8-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="8a8a8-178">(На hello 8 рабочий стол Windows, введите **PowerShell_ISE** и нажмите кнопку **интегрированной среды Сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="8a8a8-179">Ознакомьтесь с разделом [Запуск Windows PowerShell в Windows 8 и Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="8a8a8-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="8a8a8-180">Скопируйте следующий скрипт в области сценариев hello hello:</span><span class="sxs-lookup"><span data-stu-id="8a8a8-180">Copy hello following script into hello script pane:</span></span>

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

3. <span data-ttu-id="8a8a8-181">Задайте hello первые пять tooeight переменных в сценарии hello:</span><span class="sxs-lookup"><span data-stu-id="8a8a8-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="8a8a8-182">Переменная</span><span class="sxs-lookup"><span data-stu-id="8a8a8-182">Variable</span></span>|<span data-ttu-id="8a8a8-183">Описание</span><span class="sxs-lookup"><span data-stu-id="8a8a8-183">Description</span></span>
    ---|---
    <span data-ttu-id="8a8a8-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="8a8a8-184">$clusterName</span></span>|<span data-ttu-id="8a8a8-185">Это имя hello hello кластера HDInsight, где требуется приложение hello toorun.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="8a8a8-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="8a8a8-186">$oauth_consumer_key</span></span>|<span data-ttu-id="8a8a8-187">Это приложение hello Twitter **ключ потребителя** записанное ранее при создании приложения hello Twitter.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="8a8a8-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="8a8a8-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="8a8a8-189">Это приложение hello Twitter **секрет пользователя** записанное ранее.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="8a8a8-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="8a8a8-190">$oauth_token</span></span>|<span data-ttu-id="8a8a8-191">Это приложение hello Twitter **маркер доступа** записанное ранее.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="8a8a8-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="8a8a8-192">$oauth_token_secret</span></span>|<span data-ttu-id="8a8a8-193">Это приложение hello Twitter **секрет маркера доступа** записанное ранее.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="8a8a8-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="8a8a8-194">$destBlobName</span></span>|<span data-ttu-id="8a8a8-195">Это имя большого двоичного объекта hello выходные данные.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-195">This is hello output blob name.</span></span> <span data-ttu-id="8a8a8-196">значение по умолчанию Hello — **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="8a8a8-197">Если изменить значение по умолчанию hello, сценарии Windows PowerShell hello tooupdate необходимо соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="8a8a8-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="8a8a8-198">$trackString</span></span>|<span data-ttu-id="8a8a8-199">Возвращает ключевые слова связанные toothese твиты Hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="8a8a8-200">значение по умолчанию Hello — **HDInsight Azure в облаке,**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="8a8a8-201">Если изменить значение по умолчанию hello будет соответствующим образом обновить hello сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="8a8a8-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="8a8a8-202">$lineMax</span></span>|<span data-ttu-id="8a8a8-203">Hello значение определяет, сколько твиты hello скрипт будет считывать.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="8a8a8-204">Он принимает 100 твиты tooread о трех минут.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="8a8a8-205">Можно задать большее значение, но может занять больше времени toodownload.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="8a8a8-206">Нажмите клавишу **F5** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="8a8a8-207">Если возникли проблемы, чтобы избежать этого, выделите все строки hello и нажмите клавишу **F8**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="8a8a8-208">В конце выходных данных</span><span class="sxs-lookup"><span data-stu-id="8a8a8-208">You shall see "Complete!"</span></span> <span data-ttu-id="8a8a8-209">в конце hello hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-209">at hello end of hello output.</span></span> <span data-ttu-id="8a8a8-210">Все сообщения об ошибке выделяются красным цветом.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="8a8a8-211">Как процедуру проверки, вы можете проверить файл вывода hello, **/tutorials/twitter/data/tweets.txt**, на устройстве хранения больших двоичных объектов Azure с помощью обозревателя хранилищ Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="8a8a8-212">Пример сценария Windows PowerShell для перечисления файлов см. в разделе [Использование хранилища больших двоичных объектов с HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="8a8a8-213">Создание скрипта HiveQL</span><span class="sxs-lookup"><span data-stu-id="8a8a8-213">Create HiveQL script</span></span>
<span data-ttu-id="8a8a8-214">С помощью Azure PowerShell, можно выполнения нескольких инструкций HiveQL один во время или пакет hello HiveQL инструкции в файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="8a8a8-215">В этом учебнике будет создан скрипт HiveQL.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="8a8a8-216">Hello файл сценария должен быть отправленного tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="8a8a8-217">В следующем разделе hello будет выполняться hello файл скрипта с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="8a8a8-218">файл скрипта Hive Hello и файл, содержащий 10 000 твиты были переданы в открытый контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="8a8a8-219">Этот раздел можно пропустить, если toouse hello отправлены файлы.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="8a8a8-220">сценарий HiveQL Hello выполнит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8a8a8-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="8a8a8-221">**Удалить таблицу tweets_raw hello** в случае, если таблица hello уже существует.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="8a8a8-222">**Создайте таблицу Hive hello tweets_raw**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="8a8a8-223">Эта временная таблица структурированных Hive содержит hello данные для дальнейшего извлечения, преобразования и загрузки (ETL) обработки.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="8a8a8-224">Сведения о секциях см. в [руководстве по Hive][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="8a8a8-225">**Загрузка данных** из исходной папки hello, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="8a8a8-226">набор данных больших твиты Hello в вложенных формат JSON теперь преобразован временная структура таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="8a8a8-227">**Твиты hello удаления таблицы** в случае, если таблица hello уже существует.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="8a8a8-228">**Создать таблицу твиты hello**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-228">**Create hello tweets table**.</span></span> <span data-ttu-id="8a8a8-229">Прежде чем выполнять запросы к набору данных твиты hello с помощью Hive, toorun необходим другой процесс ETL.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="8a8a8-230">Этот процесс ETL определяет дополнительные схемы таблиц для hello данные, которые были сохранены в таблице «twitter_raw» hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="8a8a8-231">**Вставляет таблицу для перезаписи**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-231">**Insert overwrite table**.</span></span> <span data-ttu-id="8a8a8-232">Этот сложный сценарий Hive запускается набор длинные задания MapReduce, hello кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="8a8a8-233">В зависимости от размера кластера вашего набора данных и hello это может занять около 10 минут.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="8a8a8-234">**Вставляет каталог для перезаписи**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="8a8a8-235">Запустите файл tooa набора данных запроса и вывод hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="8a8a8-236">Этот запрос возвращает список пользователей Twitter, отправленных большинство твиты, содержащих слово hello «Azure».</span><span class="sxs-lookup"><span data-stu-id="8a8a8-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="8a8a8-237">**Куст toocreate сценариев и отправьте его tooAzure**</span><span class="sxs-lookup"><span data-stu-id="8a8a8-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="8a8a8-238">Откройте интегрированную среду сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="8a8a8-239">Скопируйте следующий скрипт в области сценариев hello hello:</span><span class="sxs-lookup"><span data-stu-id="8a8a8-239">Copy hello following script into hello script pane:</span></span>

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

3. <span data-ttu-id="8a8a8-240">Установка hello первых двух переменных в сценарии hello:</span><span class="sxs-lookup"><span data-stu-id="8a8a8-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="8a8a8-241">Переменная</span><span class="sxs-lookup"><span data-stu-id="8a8a8-241">Variable</span></span> | <span data-ttu-id="8a8a8-242">Описание</span><span class="sxs-lookup"><span data-stu-id="8a8a8-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="8a8a8-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="8a8a8-243">$clusterName</span></span> |<span data-ttu-id="8a8a8-244">Введите имя кластера HDInsight hello, в котором требуется toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="8a8a8-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="8a8a8-245">$subscriptionID</span></span> |<span data-ttu-id="8a8a8-246">Введите идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="8a8a8-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="8a8a8-247">$sourceDataPath</span></span> |<span data-ttu-id="8a8a8-248">Здравствуйте, место хранения больших двоичных объектов Azure, где запросы Hive hello будет считывать данные hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="8a8a8-249">Не нужно toochange этой переменной.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="8a8a8-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="8a8a8-250">$outputPath</span></span> |<span data-ttu-id="8a8a8-251">Здравствуйте, место хранения больших двоичных объектов Azure, где запросы Hive hello будет выдавать результаты hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="8a8a8-252">Не нужно toochange этой переменной.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="8a8a8-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="8a8a8-253">$hqlScriptFile</span></span> |<span data-ttu-id="8a8a8-254">Hello путь и имя файла hello файла сценария HiveQL hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="8a8a8-255">Не нужно toochange этой переменной.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="8a8a8-256">Нажмите клавишу **F5** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="8a8a8-257">Если возникли проблемы, чтобы избежать этого, выделите все строки hello и нажмите клавишу **F8**.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="8a8a8-258">В конце выходных данных</span><span class="sxs-lookup"><span data-stu-id="8a8a8-258">You shall see "Complete!"</span></span> <span data-ttu-id="8a8a8-259">в конце hello hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-259">at hello end of hello output.</span></span> <span data-ttu-id="8a8a8-260">Все сообщения об ошибке выделяются красным цветом.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="8a8a8-261">Как процедуру проверки, вы можете проверить файл вывода hello, **/tutorials/twitter/twitter.hql**, на устройстве хранения больших двоичных объектов Azure с помощью обозревателя хранилищ Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="8a8a8-262">Пример сценария Windows PowerShell для перечисления файлов см. в разделе [Использование хранилища больших двоичных объектов с HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="8a8a8-263">Обработка данных Twitter с помощью Hive</span><span class="sxs-lookup"><span data-stu-id="8a8a8-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="8a8a8-264">После завершения всю работу по подготовке hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="8a8a8-265">Теперь можно вызвать сценарий Hive hello и hello результаты проверки.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="8a8a8-266">Отправка задания Hive</span><span class="sxs-lookup"><span data-stu-id="8a8a8-266">Submit a Hive job</span></span>
<span data-ttu-id="8a8a8-267">Используйте следующий сценарий Hive hello toorun сценарий Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="8a8a8-268">Вам потребуется tooset hello первой переменной.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="8a8a8-269">toouse hello твитов и hello сценарий HiveQL, загруженный в двух последних разделах hello, набор $hqlScriptFile too"/tutorials/twitter/twitter.hql».</span><span class="sxs-lookup"><span data-stu-id="8a8a8-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="8a8a8-270">hello toouse те, которые были отправлены tooa большой двоичный объект открытого автоматически, задайте $hqlScriptFile слишком»wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql».</span><span class="sxs-lookup"><span data-stu-id="8a8a8-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

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

### <a name="check-hello-results"></a><span data-ttu-id="8a8a8-271">Результаты проверки hello</span><span class="sxs-lookup"><span data-stu-id="8a8a8-271">Check hello results</span></span>
<span data-ttu-id="8a8a8-272">Используйте hello следующие выходные данные задания Hive hello в toocheck сценария Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="8a8a8-273">Вам потребуется tooset hello первых двух переменных.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-273">You will need tooset hello first two variables.</span></span>

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
> Таблица Hive Hello использует \001 как hello разделитель полей. <span data-ttu-id="8a8a8-275">разделитель Hello не отображается в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="8a8a8-276">После результаты анализа hello были размещены в хранилище больших двоичных объектов Azure, можно экспортировать hello данных tooan Azure SQL базы данных или SQL server, экспортировать hello tooExcel данных с помощью Power Query или подключения к данным toohello приложения с помощью hello Hive драйвера ODBC.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="8a8a8-277">Дополнительные сведения см. в разделе [Sqoop использования с HDInsight][hdinsight-use-sqoop], [анализировать данные задержки рейсов при помощи HDInsight][hdinsight-analyze-flight-delay-data], [ Подключиться с помощью Power Query Excel tooHDInsight][hdinsight-power-query], и [tooHDInsight Excel подключиться с hello драйвер Microsoft ODBC Hive][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="8a8a8-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a8a8-278">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a8a8-278">Next steps</span></span>
<span data-ttu-id="8a8a8-279">В этом учебнике мы увидели, как tootransform набору неструктурированных данных JSON в структурированных tooquery таблицу Hive, просматривать и анализировать данные из Twitter с помощью HDInsight в Azure.</span><span class="sxs-lookup"><span data-stu-id="8a8a8-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="8a8a8-280">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="8a8a8-280">toolearn more, see:</span></span>

* <span data-ttu-id="8a8a8-281">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="8a8a8-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="8a8a8-282">[Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="8a8a8-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="8a8a8-283">[Анализ данных о задержке рейсов с помощью Hive в HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="8a8a8-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="8a8a8-284">[Подключение Excel tooHDInsight с помощью Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="8a8a8-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="8a8a8-285">[Связь с hello Hive драйвер ODBC для Microsoft Excel tooHDInsight][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="8a8a8-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="8a8a8-286">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="8a8a8-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
