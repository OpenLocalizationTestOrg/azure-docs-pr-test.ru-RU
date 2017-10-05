---
title: "Наблюдатель за сетями Azure: обнаружение сетевого вторжения с помощью средств с открытым исходным кодом | Документация Майкрософт"
description: "В этой статье описывается, как использовать службу наблюдения за сетями Azure и средства с открытым исходным кодом для обнаружения сетевого вторжения"
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
ms.openlocfilehash: 82d5e525859ebe03b152c63e4debbae469049c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="e20bb-103">Обнаружение сетевого вторжения с помощью Наблюдателя за сетями Azure и средств с открытым исходным кодом</span><span class="sxs-lookup"><span data-stu-id="e20bb-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="e20bb-104">Запись пакетов — это ключевой компонент для реализации систем обнаружения сетевых вторжений и для мониторинга безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="e20bb-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="e20bb-105">Доступны разные средства с открытым исходным кодом для обнаружения сетевых вторжений, которые обрабатывают запись пакетов для поиска известных сигнатур потенциальных сетевых вторжений и вредоносных действий.</span><span class="sxs-lookup"><span data-stu-id="e20bb-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="e20bb-106">Используя функцию записи пакетов службы наблюдения за сетями (Наблюдатель за сетями), вы можете анализировать сеть для поиска вредоносных вторжений и уязвимостей.</span><span class="sxs-lookup"><span data-stu-id="e20bb-106">Using the packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="e20bb-107">В числе средств с открытым исходным кодом можно назвать систему обнаружения сетевых вторжений Suricata, которая использует наборы правил для отслеживания сетевого трафика и создает оповещения при обнаружении подозрительных событий.</span><span class="sxs-lookup"><span data-stu-id="e20bb-107">One such open source tool is Suricata, an IDS engine that uses rulesets to monitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="e20bb-108">Механизм Suricata является многопоточным, что позволяет еще быстрее и эффективнее выполнять анализ сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="e20bb-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="e20bb-109">Дополнительные сведения о системе Suricata и ее возможностях см. на веб-сайте https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="e20bb-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="e20bb-110">Сценарий</span><span class="sxs-lookup"><span data-stu-id="e20bb-110">Scenario</span></span>

<span data-ttu-id="e20bb-111">В этой статье описывается настройка среды для обнаружения сетевых вторжений с помощью Наблюдателя за сетями, Suricata и Elastic Stack.</span><span class="sxs-lookup"><span data-stu-id="e20bb-111">This article explains how to set up your environment to perform network intrusion detection using Network Watcher, Suricata, and the Elastic Stack.</span></span> <span data-ttu-id="e20bb-112">Наблюдатель за сетями предоставляет возможность записи пакетов, которая используется для обнаружения сетевых вторжений.</span><span class="sxs-lookup"><span data-stu-id="e20bb-112">Network Watcher provides you with the packet captures used to perform network intrusion detection.</span></span> <span data-ttu-id="e20bb-113">Suricata обрабатывает запись пакетов и формирует оповещения, если обнаруживает пакеты, соответствующие набору правил для известных угроз.</span><span class="sxs-lookup"><span data-stu-id="e20bb-113">Suricata processes the packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="e20bb-114">Эти предупреждения сохраняются в файле журнала на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e20bb-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="e20bb-115">Elastic Stack позволяет индексировать журналы, созданные Suricata, и использовать их для создания панели мониторинга Kibana, которая визуализирует информацию из журналов для быстрого анализа потенциальных уязвимостей сети.</span><span class="sxs-lookup"><span data-stu-id="e20bb-115">Using the Elastic Stack, the logs generated by Suricata can be indexed and used to create a Kibana dashboard, providing you with a visual representation of the logs and a means to quickly gain insights to potential network vulnerabilities.</span></span>  

![Простой сценарий для веб-приложения][1]

<span data-ttu-id="e20bb-117">Оба средства с открытым исходным кодом можно настроить на виртуальной машине Azure, что позволяет выполнять анализ непосредственно в привычной сетевой среде Azure.</span><span class="sxs-lookup"><span data-stu-id="e20bb-117">Both open source tools can be set up on an Azure VM, allowing you to perform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="e20bb-118">Действия</span><span class="sxs-lookup"><span data-stu-id="e20bb-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="e20bb-119">Установка Suricata</span><span class="sxs-lookup"><span data-stu-id="e20bb-119">Install Suricata</span></span>

<span data-ttu-id="e20bb-120">Другие методы установки описаны на странице http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="e20bb-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="e20bb-121">В окне командной строки на виртуальной машине выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e20bb-121">In the command-line terminal of your VM run the following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="e20bb-122">Чтобы проверить установку, выполните команду `suricata -h`, которая должна отобразить полный список команд.</span><span class="sxs-lookup"><span data-stu-id="e20bb-122">To verify your installation, run the command `suricata -h` to see the full list of commands.</span></span>

### <a name="download-the-emerging-threats-ruleset"></a><span data-ttu-id="e20bb-123">Скачивание набора правил Emerging Threats</span><span class="sxs-lookup"><span data-stu-id="e20bb-123">Download the Emerging Threats ruleset</span></span>

<span data-ttu-id="e20bb-124">Пока у нас нет никаких правил, с которыми можно запустить Suricata.</span><span class="sxs-lookup"><span data-stu-id="e20bb-124">At this stage, we do not have any rules for Suricata to run.</span></span> <span data-ttu-id="e20bb-125">Вы можете создать собственные правила, если планируете обнаруживать в сети конкретные угрозы, либо применить наборы правил, разработанные несколькими поставщиками, например Emerging Threats, или правила Snort VRT.</span><span class="sxs-lookup"><span data-stu-id="e20bb-125">You can create your own rules if there are specific threats to your network you would like to detect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="e20bb-126">Для примера мы применим бесплатный набор правил Emerging Threats:</span><span class="sxs-lookup"><span data-stu-id="e20bb-126">We use the freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="e20bb-127">Скачайте набор правил и поместите их в этот каталог:</span><span class="sxs-lookup"><span data-stu-id="e20bb-127">Download the rule set and copy them into the directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="e20bb-128">Обработка записи пакетов с помощью Suricata</span><span class="sxs-lookup"><span data-stu-id="e20bb-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="e20bb-129">Чтобы поручить Suricata обработку записи пакетов, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e20bb-129">To process packet captures using Suricata, run the following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="e20bb-130">Чтобы проверить созданные оповещения, изучите файл fast.log:</span><span class="sxs-lookup"><span data-stu-id="e20bb-130">To check the resulting alerts, read the fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="e20bb-131">Настройка Elastic Stack</span><span class="sxs-lookup"><span data-stu-id="e20bb-131">Set up the Elastic Stack</span></span>

<span data-ttu-id="e20bb-132">Хотя журналы, созданные Suricata, содержат полезную информацию о ситуации в сети, эти файлы журналов не очень легко изучать.</span><span class="sxs-lookup"><span data-stu-id="e20bb-132">While the logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t the easiest to read and understand.</span></span> <span data-ttu-id="e20bb-133">Подключив Suricata к Elastic Stack, мы сможем создать панель мониторинга Kibana, которая позволяет выполнять поиск, строить диаграммы и анализировать созданные журналы.</span><span class="sxs-lookup"><span data-stu-id="e20bb-133">By connecting Suricata with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="e20bb-134">Установка Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="e20bb-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="e20bb-135">Для Elastic Stack версии 5.0 и более поздних версий требуется Java 8.</span><span class="sxs-lookup"><span data-stu-id="e20bb-135">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="e20bb-136">Выполните команду `java -version`, чтобы проверить установленную версию.</span><span class="sxs-lookup"><span data-stu-id="e20bb-136">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="e20bb-137">Если компонент Java не установлен, обратитесь к документации на [веб-сайте компании Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html).</span><span class="sxs-lookup"><span data-stu-id="e20bb-137">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="e20bb-138">Скачайте правильный двоичный пакет для своей системы.</span><span class="sxs-lookup"><span data-stu-id="e20bb-138">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="e20bb-139">Другие методы установки можно найти в [документации по установке Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html).</span><span class="sxs-lookup"><span data-stu-id="e20bb-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="e20bb-140">Убедитесь, что Elasticsearch выполняется, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e20bb-140">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="e20bb-141">Вы должны увидеть ответ следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e20bb-141">You should see a response similar to this:</span></span>

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

<span data-ttu-id="e20bb-142">Дополнительные инструкции по установке Elasticsearch можно найти на [странице установки](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html).</span><span class="sxs-lookup"><span data-stu-id="e20bb-142">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="e20bb-143">Установка Logstash</span><span class="sxs-lookup"><span data-stu-id="e20bb-143">Install Logstash</span></span>

1. <span data-ttu-id="e20bb-144">Введите следующие команды, чтобы установить Logstash.</span><span class="sxs-lookup"><span data-stu-id="e20bb-144">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="e20bb-145">Теперь нужно настроить Logstash для чтения выходного файла eve.json.</span><span class="sxs-lookup"><span data-stu-id="e20bb-145">Next we need to configure Logstash to read from the output of eve.json file.</span></span> <span data-ttu-id="e20bb-146">Создайте файл logstash.conf следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e20bb-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="e20bb-147">Добавьте в этот файл следующее содержимое (укажите правильный путь к файлу eve.json):</span><span class="sxs-lookup"><span data-stu-id="e20bb-147">Add the following content to the file (make sure that the path to the eve.json file is correct):</span></span>

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

1. <span data-ttu-id="e20bb-148">Не забудьте предоставить правильные разрешения для файла eve.json, чтобы программа Logstash смогла выполнить обработку.</span><span class="sxs-lookup"><span data-stu-id="e20bb-148">Make sure to give the correct permissions to the eve.json file so that Logstash can ingest the file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="e20bb-149">Чтобы запустить Logstash, выполните команду:</span><span class="sxs-lookup"><span data-stu-id="e20bb-149">To start Logstash run the command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="e20bb-150">Дополнительные инструкции по установке Logstash см. в [официальной документации](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html).</span><span class="sxs-lookup"><span data-stu-id="e20bb-150">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="e20bb-151">Установка Kibana</span><span class="sxs-lookup"><span data-stu-id="e20bb-151">Install Kibana</span></span>

1. <span data-ttu-id="e20bb-152">Введите следующие команды для установки Kibana.</span><span class="sxs-lookup"><span data-stu-id="e20bb-152">Run the following commands to install Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="e20bb-153">Запустите Kibana, выполнив следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e20bb-153">To run Kibana use the commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="e20bb-154">Чтобы открыть веб-интерфейс Kibana, перейдите к разделу `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="e20bb-154">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="e20bb-155">В нашем примере для журналов Suricata используется шаблон индексирования logstash-*.</span><span class="sxs-lookup"><span data-stu-id="e20bb-155">For this scenario, the index pattern used for the Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="e20bb-156">Чтобы просматривать панель мониторинга Kibana удаленно, создайте правило NSG для доступа к **порту 5601**.</span><span class="sxs-lookup"><span data-stu-id="e20bb-156">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="e20bb-157">Создание панели мониторинга Kibana</span><span class="sxs-lookup"><span data-stu-id="e20bb-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="e20bb-158">Для этой статьи мы подготовили пример панели мониторинга для просмотра тенденций и подробных сведений об оповещениях.</span><span class="sxs-lookup"><span data-stu-id="e20bb-158">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

1. <span data-ttu-id="e20bb-159">Файл панели мониторинга вы можете скачать [здесь](https://aka.ms/networkwatchersuricatadashboard), файл визуализации — [здесь](https://aka.ms/networkwatchersuricatavisualization), а сохраненный файл поиска — [здесь](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="e20bb-159">Download the dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), the visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and the saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="e20bb-160">На вкладке **Management** (Управление) в Kibana перейдите к элементу **Saved Objects** (Сохраненные объекты) и импортируйте все три файла.</span><span class="sxs-lookup"><span data-stu-id="e20bb-160">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="e20bb-161">Затем откройте вкладку **Dashboard** (Панель мониторинга) и загрузите пример панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="e20bb-161">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="e20bb-162">Вы можете также создать собственные визуализации и панели мониторинга, адаптированные к интересующим вас метрикам.</span><span class="sxs-lookup"><span data-stu-id="e20bb-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="e20bb-163">Дополнительные сведения о визуализациях Kibana можно получить в [официальной документации по Kibana](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="e20bb-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![Панель мониторинга Kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="e20bb-165">Визуализация журналов оповещений IDS</span><span class="sxs-lookup"><span data-stu-id="e20bb-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="e20bb-166">Пример панели мониторинга содержит несколько визуализаций для журналов оповещений Suricata:</span><span class="sxs-lookup"><span data-stu-id="e20bb-166">The sample dashboard provides several visualizations of the Suricata alert logs:</span></span>

1. <span data-ttu-id="e20bb-167">Оповещения по GeoIP — эта карта распределения оповещений по странам, составленная по данным о географическом расположении (определяется по IP-адресу)</span><span class="sxs-lookup"><span data-stu-id="e20bb-167">Alerts by GeoIP – a map showing the distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![Географическое распределение IP-адресов][3]

1. <span data-ttu-id="e20bb-169">10 основных оповещений — сводка из 10 наиболее часто создаваемых оповещений с описаниями.</span><span class="sxs-lookup"><span data-stu-id="e20bb-169">Top 10 Alerts – a summary of the 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="e20bb-170">Щелкнув конкретное оповещение, можно отфильтровать информацию на панели мониторинга и просмотреть сведения, имеющие отношение к этому оповещению.</span><span class="sxs-lookup"><span data-stu-id="e20bb-170">Clicking an individual alert filters down the dashboard to the information pertaining to that specific alert.</span></span>

    ![рисунок 4][4]

1. <span data-ttu-id="e20bb-172">Число оповещений — общее число оповещений, созданных по набору правил</span><span class="sxs-lookup"><span data-stu-id="e20bb-172">Number of Alerts – the total count of alerts triggered by the ruleset</span></span>

    ![Рис. 5][5]

1. <span data-ttu-id="e20bb-174">20 основных исходных/целевых IP-адресов/портов — эти круговые диаграммы представляют информацию об IP-адресах и портах, для которых создано больше всего оповещений.</span><span class="sxs-lookup"><span data-stu-id="e20bb-174">Top 20 Source/Destination IPs/Ports - pie charts showing the top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="e20bb-175">Можно отфильтровать информацию по конкретным IP-адресам или портам, чтобы увидеть количество и типы оповещений по ним.</span><span class="sxs-lookup"><span data-stu-id="e20bb-175">You can filter down on specific IPs/ports to see how many and what kind of alerts are being triggered.</span></span>

    ![Рис. 6][6]

1. <span data-ttu-id="e20bb-177">Сводка оповещения — таблица с подробными сведениями по каждому конкретному оповещению.</span><span class="sxs-lookup"><span data-stu-id="e20bb-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="e20bb-178">Можно настроить эту таблицу для отображения разных параметров по каждому оповещению.</span><span class="sxs-lookup"><span data-stu-id="e20bb-178">You can customize this table to show other parameters of interest for each alert.</span></span>

    ![Рис. 7][7]

<span data-ttu-id="e20bb-180">Дополнительную документацию по созданию пользовательских визуализаций и панелей мониторинга см. в [официальной документации по Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="e20bb-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="e20bb-181">Заключение</span><span class="sxs-lookup"><span data-stu-id="e20bb-181">Conclusion</span></span>

<span data-ttu-id="e20bb-182">Сочетая возможность записи пакетов, реализованную в Наблюдателе за сетями, и функции таких средств с открытым исходным кодом, как Suricata, вы можете определять сетевые вторжения самого разного толка.</span><span class="sxs-lookup"><span data-stu-id="e20bb-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="e20bb-183">Такие панели мониторинга позволяют быстро выявлять тенденции и аномалии в сети, а также подробно изучать данные для анализа основных причин оповещений, включая активность злоумышленников или уязвимость портов.</span><span class="sxs-lookup"><span data-stu-id="e20bb-183">These dashboards allow you to quickly spot trends and anomalies within your network, as well dig into the data to discover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="e20bb-184">На основе полученных данных вы сможете принять взвешенные решения о методах реагирования и защиты сети от вредоносных попыток вторжения, а также создать новые правила для предотвращения будущих сетевых вторжений.</span><span class="sxs-lookup"><span data-stu-id="e20bb-184">With this extracted data, you can make informed decisions on how to react to and protect your network from any harmful intrusion attempts, and create rules to prevent future intrusions to your network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e20bb-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e20bb-185">Next steps</span></span>

<span data-ttu-id="e20bb-186">Дополнительные сведения о функции записи пакетов на основе оповещений см. в статье [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md) (Использование записи пакетов для упреждающего мониторинга сети с помощью функций Azure).</span><span class="sxs-lookup"><span data-stu-id="e20bb-186">Learn how to trigger packet captures based on alerts by visiting [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="e20bb-187">Ознакомьтесь со статьей [Visualizing Network Security Group flow logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Визуализация журналов потоков для групп безопасности сети с помощью Power BI).</span><span class="sxs-lookup"><span data-stu-id="e20bb-187">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
