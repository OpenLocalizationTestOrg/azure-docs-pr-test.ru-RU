---
title: "aaaVisualize NSG Наблюдатель сети Azure потока журналов с помощью средств с открытым исходным кодом | Документы Microsoft"
description: "На этой странице описаны как toouse открыть журналах источника средства toovisualize NSG потока."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="2e1df-103">Визуализация журнала потоков для групп безопасности сети Наблюдателя за сетями Azure с помощью инструментов с открытым кодом</span><span class="sxs-lookup"><span data-stu-id="2e1df-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="2e1df-104">Журналы потоков для групп безопасности сети содержат информацию о входящем и исходящем IP-трафике групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="2e1df-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="2e1df-105">Эти журналы потока Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5 кортежей сведения о hello потока (источник и назначение IP-адресов, исходного или целевого порта протокола), и если hello трафик разрешен или запрещен.</span><span class="sxs-lookup"><span data-stu-id="2e1df-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="2e1df-106">Эти журналы потока можно трудно toomanually синтаксического анализа и получения полезных сведений из.</span><span class="sxs-lookup"><span data-stu-id="2e1df-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="2e1df-107">Однако существует несколько инструментов с открытым кодом, которые могут помочь визуализировать эти данные.</span><span class="sxs-lookup"><span data-stu-id="2e1df-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="2e1df-108">В этой статье приводятся toovisualize решения эти журналы hello эластичной стека с помощью которых будет позволяют tooquickly индекса и визуализировать потока журналов на Kibana панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="2e1df-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="2e1df-109">Сценарий</span><span class="sxs-lookup"><span data-stu-id="2e1df-109">Scenario</span></span>

<span data-ttu-id="2e1df-110">В этой статье мы определим решение, которое позволит вам toovisualize сетевой группы безопасности потока журналы, с помощью hello эластичной стека.</span><span class="sxs-lookup"><span data-stu-id="2e1df-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="2e1df-111">Подключаемый модуль ввода Logstash будет получать журналы потока hello непосредственно из hello BLOB-объекта хранилища настроена для hello журналы потока, содержащего.</span><span class="sxs-lookup"><span data-stu-id="2e1df-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="2e1df-112">Затем, используя hello эластичной стека, hello потока журналы будут индексироваться и использовать toocreate Kibana сведений о hello мониторинга toovisualize.</span><span class="sxs-lookup"><span data-stu-id="2e1df-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![сценарий][scenario]

## <a name="steps"></a><span data-ttu-id="2e1df-114">Действия</span><span class="sxs-lookup"><span data-stu-id="2e1df-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="2e1df-115">Включение ведения журнала потоков для групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="2e1df-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="2e1df-116">В рамках данного сценария вам необходимо включить ведение журнала потоков по меньшей мере для одной группы безопасности сети в своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2e1df-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="2e1df-117">Инструкции по включению журналы потока сетевой безопасности см. в следующей статьей toohello [ведения журнала tooflow введение для групп безопасности сети](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e1df-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="2e1df-118">Настройка hello эластичной стека</span><span class="sxs-lookup"><span data-stu-id="2e1df-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="2e1df-119">Подключив NSG потока журналов с помощью hello эластичной стека, мы можно создать панель мониторинга Kibana, что мы сможем toosearch, граф, анализировать и производные от наших журналов аналитики.</span><span class="sxs-lookup"><span data-stu-id="2e1df-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="2e1df-120">Установка Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="2e1df-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="2e1df-121">Hello эластичной стека из версии 5.0 и более поздних версий требуется Java 8.</span><span class="sxs-lookup"><span data-stu-id="2e1df-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="2e1df-122">Выполните команду hello `java -version` toocheck вашей версии.</span><span class="sxs-lookup"><span data-stu-id="2e1df-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="2e1df-123">Если у вас java установки, ознакомьтесь с toodocumentation по [Oracle в веб-сайта](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="2e1df-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="2e1df-124">Загрузите hello правильный двоичный пакет для вашей системы:</span><span class="sxs-lookup"><span data-stu-id="2e1df-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="2e1df-125">Другие методы установки можно найти в [документации по установке Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html).</span><span class="sxs-lookup"><span data-stu-id="2e1df-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="2e1df-126">Убедитесь, что Elasticsearch выполняется с помощью команды hello:</span><span class="sxs-lookup"><span data-stu-id="2e1df-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="2e1df-127">Вы увидите примерно toothis ответа:</span><span class="sxs-lookup"><span data-stu-id="2e1df-127">You should see a response similar toothis:</span></span>

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

<span data-ttu-id="2e1df-128">Дополнительные инструкции по установке эластичной поиска, см. страницу toohello [установки](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="2e1df-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="2e1df-129">Установка Logstash</span><span class="sxs-lookup"><span data-stu-id="2e1df-129">Install Logstash</span></span>

1. <span data-ttu-id="2e1df-130">tooinstall Logstash выполните hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2e1df-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="2e1df-131">Далее нам нужна tooconfigure Logstash tooaccess и проанализировать журналы hello потока.</span><span class="sxs-lookup"><span data-stu-id="2e1df-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="2e1df-132">Создайте файл logstash.conf следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2e1df-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="2e1df-133">Добавьте следующие файл содержимого toohello hello:</span><span class="sxs-lookup"><span data-stu-id="2e1df-133">Add hello following content toohello file:</span></span>

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

<span data-ttu-id="2e1df-134">См. инструкции по установке Logstash toohello [официальной документации](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="2e1df-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="2e1df-135">Установите hello Logstash ввода подключаемый модуль для хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="2e1df-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="2e1df-136">Этот подключаемый модуль Logstash позволит вам toodirectly hello потока журналы событий из своей учетной записи указанного хранилища.</span><span class="sxs-lookup"><span data-stu-id="2e1df-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="2e1df-137">tooinstall этого подключаемого модуля в каталог установки Logstash hello по умолчанию (в этом вариантов /usr/share/logstash/bin) команду hello:</span><span class="sxs-lookup"><span data-stu-id="2e1df-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="2e1df-138">toostart Logstash, выполните команду hello:</span><span class="sxs-lookup"><span data-stu-id="2e1df-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="2e1df-139">Дополнительные сведения о данном подключаемом модуле см. в разделе toodocumentation [здесь](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="2e1df-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="2e1df-140">Установка Kibana</span><span class="sxs-lookup"><span data-stu-id="2e1df-140">Install Kibana</span></span>

1. <span data-ttu-id="2e1df-141">Выполните следующие команды tooinstall Kibana hello.</span><span class="sxs-lookup"><span data-stu-id="2e1df-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="2e1df-142">toorun Kibana использование hello команд:</span><span class="sxs-lookup"><span data-stu-id="2e1df-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="2e1df-143">tooview Kibana веб-интерфейсом, слишком перехода`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="2e1df-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="2e1df-144">В этом сценарии шаблон hello индекса, используемый для потока журналов hello — «nsg потока журналы».</span><span class="sxs-lookup"><span data-stu-id="2e1df-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="2e1df-145">Можно изменить шаблон индекс hello в разделе «выход» hello logstash.conf файла.</span><span class="sxs-lookup"><span data-stu-id="2e1df-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="2e1df-146">Панели мониторинга Kibana hello tooview удаленно, создать правило входящего трафика NSG, предоставляя доступ слишком**порт 5601**.</span><span class="sxs-lookup"><span data-stu-id="2e1df-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="2e1df-147">Создание панели мониторинга Kibana</span><span class="sxs-lookup"><span data-stu-id="2e1df-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="2e1df-148">В этой статье мы предоставили используется пример информационной панели для вас tooview тенденции и сведения в своих предупреждений.</span><span class="sxs-lookup"><span data-stu-id="2e1df-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![Рисунок 1][1]

1. <span data-ttu-id="2e1df-150">Загрузите файл мониторинга hello [здесь](https://aka.ms/networkwatchernsgflowlogdashboard), файл визуализации hello [здесь](https://aka.ms/networkwatchernsgflowlogvisualizations)и файл сохранен hello поиска [здесь](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="2e1df-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="2e1df-151">В группе hello **управления** вкладку из Kibana, перейдите слишком**сохраненные объекты** и импортировать все три файла.</span><span class="sxs-lookup"><span data-stu-id="2e1df-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="2e1df-152">Затем из hello **мониторинга** вкладку, можно открыть и загрузка hello в примере информационной панели.</span><span class="sxs-lookup"><span data-stu-id="2e1df-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="2e1df-153">Вы можете также создать собственные визуализации и панели мониторинга, адаптированные к интересующим вас метрикам.</span><span class="sxs-lookup"><span data-stu-id="2e1df-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="2e1df-154">Дополнительные сведения о визуализациях Kibana можно получить в [официальной документации по Kibana](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="2e1df-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="2e1df-155">Визуализация журналов потоков NSG</span><span class="sxs-lookup"><span data-stu-id="2e1df-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="2e1df-156">Образец Hello панели мониторинга предоставляет несколько визуализаций hello потока журналов:</span><span class="sxs-lookup"><span data-stu-id="2e1df-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="2e1df-157">Потоки, принятия решений и направления за период времени — времени рядов диаграмм, отображая hello число потоков с течением hello период времени.</span><span class="sxs-lookup"><span data-stu-id="2e1df-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="2e1df-158">Единица времени hello и диапазон оба эти представления можно изменить.</span><span class="sxs-lookup"><span data-stu-id="2e1df-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="2e1df-159">Потоки путем принятия решений показано hello долю разрешение или запрет решения, принимаемые при потоки с пропорций hello показывает направление входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="2e1df-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="2e1df-160">С помощью этих визуальных элементов можно проверять тенденции трафика с течением времени и искать какие-либо пики или нестандартные шаблоны.</span><span class="sxs-lookup"><span data-stu-id="2e1df-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![Рисунок 2][2]

1. <span data-ttu-id="2e1df-162">Потоки с целевой и исходный порт — портами hello распределение потоков tootheir соответствующих круговые диаграммы.</span><span class="sxs-lookup"><span data-stu-id="2e1df-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="2e1df-163">В этом представлении можно увидеть наиболее часто используемые порты.</span><span class="sxs-lookup"><span data-stu-id="2e1df-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="2e1df-164">При нажатии на конкретный порт в круговой диаграмме hello rest hello мониторинга hello отфильтрует вниз tooflows порта.</span><span class="sxs-lookup"><span data-stu-id="2e1df-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![Рисунок 3][3]

1. <span data-ttu-id="2e1df-166">Число потоков и самое раннее время журнала — метрики, показывая hello количество потоков, записанных, полученной hello дату ранней журнала hello.</span><span class="sxs-lookup"><span data-stu-id="2e1df-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![Рисунок 4][4]

1. <span data-ttu-id="2e1df-168">Потоки, NSG и правило — Гистограмма показывает распределение потоков в пределах каждого NSG hello, а также распространения hello правил в каждом NSG.</span><span class="sxs-lookup"><span data-stu-id="2e1df-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="2e1df-169">Отсюда можно видеть какие NSG и правил, сформированных hello большая часть трафика.</span><span class="sxs-lookup"><span data-stu-id="2e1df-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![Рисунок 5][5]

1. <span data-ttu-id="2e1df-171">Первые 10 источника или целевой IP-адресов — панель диаграмм, показывающие hello первые 10 исходный и конечный IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="2e1df-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="2e1df-172">Вы можете настроить эти диаграммы tooshow больше или меньше верхней IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="2e1df-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="2e1df-173">Здесь вы может hello, наиболее часто встречающихся IP-адресов в разделе, а также hello трафика принятия решений ("Разрешить" или "Запретить"), выполненный для каждого IP.</span><span class="sxs-lookup"><span data-stu-id="2e1df-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![Рисунок 6][6]

1. <span data-ttu-id="2e1df-175">Кортежи потока — в этой таблице показано hello сведения, содержащиеся в пределах каждого кортежа потока, а также его соответствующие параметры и правила.</span><span class="sxs-lookup"><span data-stu-id="2e1df-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![Рисунок 7][7]

<span data-ttu-id="2e1df-177">Использование панели запросов hello hello верхней части панели мониторинга hello, можно отфильтровать вниз hello панели мониторинга на основе любого параметра hello потокам, такие как идентификатор подписки, группы ресурсов, правило или любую другую переменную, представляющие интерес.</span><span class="sxs-lookup"><span data-stu-id="2e1df-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="2e1df-178">Дополнительные сведения о запросах и фильтрах Kibana ссылаться toohello [официальной документации](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="2e1df-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="2e1df-179">Заключение</span><span class="sxs-lookup"><span data-stu-id="2e1df-179">Conclusion</span></span>

<span data-ttu-id="2e1df-180">Объединяя hello сетевой группы безопасности потока журналы hello эластичной стека, мы придумать мощное и настраиваемые toovisualize нашей сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="2e1df-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="2e1df-181">Эти панели мониторинга позволяют tooquickly прибыль и обмениваться информацией о сетевой трафик, а также фильтровать вниз и исследовать на любой потенциальных нарушений.</span><span class="sxs-lookup"><span data-stu-id="2e1df-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="2e1df-182">Kibana можно адаптировать эти панели мониторинга и создания определенных визуализации toomeet любого аудита безопасности и соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="2e1df-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e1df-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e1df-183">Next steps</span></span>

<span data-ttu-id="2e1df-184">Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="2e1df-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
