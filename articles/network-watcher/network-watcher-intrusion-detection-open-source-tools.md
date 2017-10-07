---
title: "aaaPerform обнаружения проникновений в сеть с Наблюдатель сети Azure и средств с открытым исходным кодом | Документы Microsoft"
description: "В этой статье описывается, как toouse Наблюдатель сети Azure и tooperform средства открытой сети обнаружения вторжений"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="dfe4a-103">Обнаружение сетевого вторжения с помощью Наблюдателя за сетями Azure и средств с открытым исходным кодом</span><span class="sxs-lookup"><span data-stu-id="dfe4a-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="dfe4a-104">Запись пакетов — это ключевой компонент для реализации систем обнаружения сетевых вторжений и для мониторинга безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="dfe4a-105">Доступны разные средства с открытым исходным кодом для обнаружения сетевых вторжений, которые обрабатывают запись пакетов для поиска известных сигнатур потенциальных сетевых вторжений и вредоносных действий.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="dfe4a-106">Захват пакетов hello, предоставляемые Наблюдатель сети вы можете анализировать сети для любой проникновения вредоносного или уязвимости.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-106">Using hello packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="dfe4a-107">Одним из таких средств открытым исходным кодом — Suricata подсистема Идентификаторы, использует наборы правил toomonitor сетевого трафика и запускает оповещения при возникновении любого подозрительные события.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-107">One such open source tool is Suricata, an IDS engine that uses rulesets toomonitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="dfe4a-108">Механизм Suricata является многопоточным, что позволяет еще быстрее и эффективнее выполнять анализ сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="dfe4a-109">Дополнительные сведения о системе Suricata и ее возможностях см. на веб-сайте https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="dfe4a-110">Сценарий</span><span class="sxs-lookup"><span data-stu-id="dfe4a-110">Scenario</span></span>

<span data-ttu-id="dfe4a-111">В этой статье объясняется, как tooset копирование tooperform вашей среды с помощью Наблюдатель сети, Suricata, обнаружение вторжений сети и hello эластичной стека.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-111">This article explains how tooset up your environment tooperform network intrusion detection using Network Watcher, Suricata, and hello Elastic Stack.</span></span> <span data-ttu-id="dfe4a-112">Наблюдатель сети предоставляет вам пакет приветствия захватывает используется tooperform обнаружения проникновений в сеть.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-112">Network Watcher provides you with hello packet captures used tooperform network intrusion detection.</span></span> <span data-ttu-id="dfe4a-113">Снимки Suricata процессы hello пакетов и триггер оповещения на основании пакетов, которые соответствуют его заданного набора правил угроз.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-113">Suricata processes hello packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="dfe4a-114">Эти предупреждения сохраняются в файле журнала на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="dfe4a-115">С помощью hello эластичной стека, hello журналы, формируемые службой Suricata могут быть проиндексированы и используется toocreate Kibana панели мониторинга, предоставив визуальное представление журналов hello и означает tooquickly прибыль аналитики toopotential сети уязвимости.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-115">Using hello Elastic Stack, hello logs generated by Suricata can be indexed and used toocreate a Kibana dashboard, providing you with a visual representation of hello logs and a means tooquickly gain insights toopotential network vulnerabilities.</span></span>  

![Простой сценарий для веб-приложения][1]

<span data-ttu-id="dfe4a-117">Оба средства с открытым исходным кодом можно настроить на виртуальной Машине Azure, позволяя tooperform этого анализа в среде сети Azure.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-117">Both open source tools can be set up on an Azure VM, allowing you tooperform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="dfe4a-118">Действия</span><span class="sxs-lookup"><span data-stu-id="dfe4a-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="dfe4a-119">Установка Suricata</span><span class="sxs-lookup"><span data-stu-id="dfe4a-119">Install Suricata</span></span>

<span data-ttu-id="dfe4a-120">Другие методы установки описаны на странице http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="dfe4a-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="dfe4a-121">В командной строки терминалов hello вашей виртуальной машины выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-121">In hello command-line terminal of your VM run hello following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="dfe4a-122">tooverify параметры установки, выполните команду hello `suricata -h` toosee hello полный список команд.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-122">tooverify your installation, run hello command `suricata -h` toosee hello full list of commands.</span></span>

### <a name="download-hello-emerging-threats-ruleset"></a><span data-ttu-id="dfe4a-123">Загрузить набор правил новых угроз hello</span><span class="sxs-lookup"><span data-stu-id="dfe4a-123">Download hello Emerging Threats ruleset</span></span>

<span data-ttu-id="dfe4a-124">На этом этапе у нас есть не все правила для Suricata toorun.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-124">At this stage, we do not have any rules for Suricata toorun.</span></span> <span data-ttu-id="dfe4a-125">Если существуют определенные угрозы tooyour сети хотелось бы toodetect или вы также можете использовать разработанные наборы правил из нескольких поставщиков, например новые угрозы или VRT правила из Snort можно создавать собственные правила.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-125">You can create your own rules if there are specific threats tooyour network you would like toodetect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="dfe4a-126">Здесь мы используем hello свободно доступен ruleset новых угроз:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-126">We use hello freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="dfe4a-127">Загрузить набор правил hello и скопируйте их в каталог hello:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-127">Download hello rule set and copy them into hello directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="dfe4a-128">Обработка записи пакетов с помощью Suricata</span><span class="sxs-lookup"><span data-stu-id="dfe4a-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="dfe4a-129">пакет tooprocess собирает, с помощью Suricata, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-129">tooprocess packet captures using Suricata, run hello following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="dfe4a-130">toocheck hello оповещения, чтение файла fast.log hello:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-130">toocheck hello resulting alerts, read hello fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="dfe4a-131">Настройка hello эластичной стека</span><span class="sxs-lookup"><span data-stu-id="dfe4a-131">Set up hello Elastic Stack</span></span>

<span data-ttu-id="dfe4a-132">Хотя hello журналы, созданные Suricata содержит ценную информацию о происходящем нашей сети, файлы журнала не являются простым tooread hello и понять.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-132">While hello logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t hello easiest tooread and understand.</span></span> <span data-ttu-id="dfe4a-133">Подключив Suricata hello эластичной стека, мы можно создать панель мониторинга Kibana, что мы сможем toosearch, граф, анализ и производные от наших журналов аналитики.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-133">By connecting Suricata with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="dfe4a-134">Установка Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="dfe4a-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="dfe4a-135">Hello эластичной стека из версии 5.0 и более поздних версий требуется Java 8.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-135">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="dfe4a-136">Выполните команду hello `java -version` toocheck вашей версии.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-136">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="dfe4a-137">Если у вас java установки, ознакомьтесь с toodocumentation по [Oracle в веб-сайта](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="dfe4a-137">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="dfe4a-138">Загрузите hello правильный двоичный пакет для вашей системы:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-138">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="dfe4a-139">Другие методы установки можно найти в [документации по установке Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html).</span><span class="sxs-lookup"><span data-stu-id="dfe4a-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="dfe4a-140">Убедитесь, что Elasticsearch выполняется с помощью команды hello:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-140">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="dfe4a-141">Вы увидите примерно toothis ответа:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-141">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="dfe4a-142">Дополнительные инструкции по установке эластичной поиска, см. страницу toohello [установки](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="dfe4a-142">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="dfe4a-143">Установка Logstash</span><span class="sxs-lookup"><span data-stu-id="dfe4a-143">Install Logstash</span></span>

1. <span data-ttu-id="dfe4a-144">tooinstall Logstash выполните hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-144">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="dfe4a-145">Далее нам нужно tooread Logstash tooconfigure из выходных данных hello eve.json файла.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-145">Next we need tooconfigure Logstash tooread from hello output of eve.json file.</span></span> <span data-ttu-id="dfe4a-146">Создайте файл logstash.conf следующим образом.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="dfe4a-147">Добавьте следующие файл содержимого toohello hello (Убедитесь, что это правильный файл eve.json toohello hello путь):</span><span class="sxs-lookup"><span data-stu-id="dfe4a-147">Add hello following content toohello file (make sure that hello path toohello eve.json file is correct):</span></span>

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. <span data-ttu-id="dfe4a-148">Сделайте что toogive hello правильные разрешения toohello eve.json файл, чтобы Logstash можно принять файл hello.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-148">Make sure toogive hello correct permissions toohello eve.json file so that Logstash can ingest hello file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="dfe4a-149">toostart Logstash, выполните команду hello:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-149">toostart Logstash run hello command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="dfe4a-150">См. инструкции по установке Logstash toohello [официальной документации](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="dfe4a-150">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="dfe4a-151">Установка Kibana</span><span class="sxs-lookup"><span data-stu-id="dfe4a-151">Install Kibana</span></span>

1. <span data-ttu-id="dfe4a-152">Выполните следующие команды tooinstall Kibana hello.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-152">Run hello following commands tooinstall Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="dfe4a-153">toorun Kibana использование hello команд:</span><span class="sxs-lookup"><span data-stu-id="dfe4a-153">toorun Kibana use hello commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="dfe4a-154">tooview Kibana веб-интерфейсом, слишком перехода`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="dfe4a-154">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="dfe4a-155">Для этого сценария является hello индекс модель использования hello журналы Suricata «logstash-*»</span><span class="sxs-lookup"><span data-stu-id="dfe4a-155">For this scenario, hello index pattern used for hello Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="dfe4a-156">Панели мониторинга Kibana hello tooview удаленно, создать правило входящего трафика NSG, предоставляя доступ слишком**порт 5601**.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-156">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="dfe4a-157">Создание панели мониторинга Kibana</span><span class="sxs-lookup"><span data-stu-id="dfe4a-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="dfe4a-158">В этой статье мы предоставили используется пример информационной панели для вас tooview тенденции и сведения в своих предупреждений.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-158">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

1. <span data-ttu-id="dfe4a-159">Загрузите файл мониторинга hello [здесь](https://aka.ms/networkwatchersuricatadashboard), файл визуализации hello [здесь](https://aka.ms/networkwatchersuricatavisualization)и файл сохранен hello поиска [здесь](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="dfe4a-159">Download hello dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), hello visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and hello saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="dfe4a-160">В группе hello **управления** вкладку из Kibana, перейдите слишком**сохраненные объекты** и импортировать все три файла.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-160">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="dfe4a-161">Затем из hello **мониторинга** вкладку, можно открыть и загрузка hello в примере информационной панели.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-161">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="dfe4a-162">Вы можете также создать собственные визуализации и панели мониторинга, адаптированные к интересующим вас метрикам.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="dfe4a-163">Дополнительные сведения о визуализациях Kibana можно получить в [официальной документации по Kibana](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="dfe4a-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![Панель мониторинга Kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="dfe4a-165">Визуализация журналов оповещений IDS</span><span class="sxs-lookup"><span data-stu-id="dfe4a-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="dfe4a-166">Образец Hello панели мониторинга предоставляет несколько визуализаций журналов предупреждений Suricata hello.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-166">hello sample dashboard provides several visualizations of hello Suricata alert logs:</span></span>

1. <span data-ttu-id="dfe4a-167">Оповещения по GeoIP — карта, показывающая распределение hello оповещения по их стране происхождения, на основе географического расположения (определяется по IP-Адресу)</span><span class="sxs-lookup"><span data-stu-id="dfe4a-167">Alerts by GeoIP – a map showing hello distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![Географическое распределение IP-адресов][3]

1. <span data-ttu-id="dfe4a-169">Первые 10 оповещения — Сводка по оповещениям hello 10 наиболее частые запуска и их описание.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-169">Top 10 Alerts – a summary of hello 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="dfe4a-170">Щелкнув отдельное предупреждение фильтрует вниз hello мониторинга toohello сведения, соответствующие toothat конкретные предупреждения.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-170">Clicking an individual alert filters down hello dashboard toohello information pertaining toothat specific alert.</span></span>

    ![рисунок 4][4]

1. <span data-ttu-id="dfe4a-172">Количество предупреждений — общее число оповещений, активируемых hello ruleset hello</span><span class="sxs-lookup"><span data-stu-id="dfe4a-172">Number of Alerts – hello total count of alerts triggered by hello ruleset</span></span>

    ![Рис. 5][5]

1. <span data-ttu-id="dfe4a-174">20 основных источника или целевой IP-адресов и портов - круговых диаграмм, показывающие hello top 20 IP-адресов и портов, которые предупреждения было запущено на.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-174">Top 20 Source/Destination IPs/Ports - pie charts showing hello top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="dfe4a-175">Можно фильтровать работу на определенных IP-адресов и портов toosee количество и тип оповещения инициируются.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-175">You can filter down on specific IPs/ports toosee how many and what kind of alerts are being triggered.</span></span>

    ![Рис. 6][6]

1. <span data-ttu-id="dfe4a-177">Сводка оповещения — таблица с подробными сведениями по каждому конкретному оповещению.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="dfe4a-178">Tooshow этой таблицы можно настроить другие параметры, представляющие интерес для каждого предупреждения.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-178">You can customize this table tooshow other parameters of interest for each alert.</span></span>

    ![Рис. 7][7]

<span data-ttu-id="dfe4a-180">Дополнительную документацию по созданию пользовательских визуализаций и панелей мониторинга см. в [официальной документации по Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="dfe4a-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="dfe4a-181">Заключение</span><span class="sxs-lookup"><span data-stu-id="dfe4a-181">Conclusion</span></span>

<span data-ttu-id="dfe4a-182">Сочетая возможность записи пакетов, реализованную в Наблюдателе за сетями, и функции таких средств с открытым исходным кодом, как Suricata, вы можете определять сетевые вторжения самого разного толка.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="dfe4a-183">Эти панели мониторинга позволяют вам tooquickly отслеживать тенденции и аномалий в сети, также детализировать данные toodiscover основные причины предупреждения, например, злонамеренный пользователь агентов или уязвимым портам приветствия.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-183">These dashboards allow you tooquickly spot trends and anomalies within your network, as well dig into hello data toodiscover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="dfe4a-184">С извлеченными данными можно принимать обоснованные решения с как tooreact tooand защиты сети от проникновения вредоносных попыток и Создание правила tooprevent будущих вторжения tooyour сети.</span><span class="sxs-lookup"><span data-stu-id="dfe4a-184">With this extracted data, you can make informed decisions on how tooreact tooand protect your network from any harmful intrusion attempts, and create rules tooprevent future intrusions tooyour network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfe4a-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dfe4a-185">Next steps</span></span>

<span data-ttu-id="dfe4a-186">Узнайте, как снимки tootrigger пакетов на основе оповещения, посетив [использовать пакет отслеживания toodo упреждающего мониторинга сети с помощью функций Azure](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="dfe4a-186">Learn how tootrigger packet captures based on alerts by visiting [Use packet capture toodo proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="dfe4a-187">Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="dfe4a-187">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
