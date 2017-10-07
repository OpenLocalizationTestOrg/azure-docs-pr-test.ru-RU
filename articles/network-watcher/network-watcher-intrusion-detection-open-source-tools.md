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
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Обнаружение сетевого вторжения с помощью Наблюдателя за сетями Azure и средств с открытым исходным кодом

Запись пакетов — это ключевой компонент для реализации систем обнаружения сетевых вторжений и для мониторинга безопасности сети. Доступны разные средства с открытым исходным кодом для обнаружения сетевых вторжений, которые обрабатывают запись пакетов для поиска известных сигнатур потенциальных сетевых вторжений и вредоносных действий. Захват пакетов hello, предоставляемые Наблюдатель сети вы можете анализировать сети для любой проникновения вредоносного или уязвимости.

Одним из таких средств открытым исходным кодом — Suricata подсистема Идентификаторы, использует наборы правил toomonitor сетевого трафика и запускает оповещения при возникновении любого подозрительные события. Механизм Suricata является многопоточным, что позволяет еще быстрее и эффективнее выполнять анализ сетевого трафика. Дополнительные сведения о системе Suricata и ее возможностях см. на веб-сайте https://suricata-ids.org/.

## <a name="scenario"></a>Сценарий

В этой статье объясняется, как tooset копирование tooperform вашей среды с помощью Наблюдатель сети, Suricata, обнаружение вторжений сети и hello эластичной стека. Наблюдатель сети предоставляет вам пакет приветствия захватывает используется tooperform обнаружения проникновений в сеть. Снимки Suricata процессы hello пакетов и триггер оповещения на основании пакетов, которые соответствуют его заданного набора правил угроз. Эти предупреждения сохраняются в файле журнала на локальном компьютере. С помощью hello эластичной стека, hello журналы, формируемые службой Suricata могут быть проиндексированы и используется toocreate Kibana панели мониторинга, предоставив визуальное представление журналов hello и означает tooquickly прибыль аналитики toopotential сети уязвимости.  

![Простой сценарий для веб-приложения][1]

Оба средства с открытым исходным кодом можно настроить на виртуальной Машине Azure, позволяя tooperform этого анализа в среде сети Azure.

## <a name="steps"></a>Действия

### <a name="install-suricata"></a>Установка Suricata

Другие методы установки описаны на странице http://suricata.readthedocs.io/en/latest/install.html

1. В командной строки терминалов hello вашей виртуальной машины выполните следующие команды hello:

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify параметры установки, выполните команду hello `suricata -h` toosee hello полный список команд.

### <a name="download-hello-emerging-threats-ruleset"></a>Загрузить набор правил новых угроз hello

На этом этапе у нас есть не все правила для Suricata toorun. Если существуют определенные угрозы tooyour сети хотелось бы toodetect или вы также можете использовать разработанные наборы правил из нескольких поставщиков, например новые угрозы или VRT правила из Snort можно создавать собственные правила. Здесь мы используем hello свободно доступен ruleset новых угроз:

Загрузить набор правил hello и скопируйте их в каталог hello:

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>Обработка записи пакетов с помощью Suricata

пакет tooprocess собирает, с помощью Suricata, запустите hello следующую команду:

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
toocheck hello оповещения, чтение файла fast.log hello:
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>Настройка hello эластичной стека

Хотя hello журналы, созданные Suricata содержит ценную информацию о происходящем нашей сети, файлы журнала не являются простым tooread hello и понять. Подключив Suricata hello эластичной стека, мы можно создать панель мониторинга Kibana, что мы сможем toosearch, граф, анализ и производные от наших журналов аналитики.

#### <a name="install-elasticsearch"></a>Установка Elasticsearch

1. Hello эластичной стека из версии 5.0 и более поздних версий требуется Java 8. Выполните команду hello `java -version` toocheck вашей версии. Если у вас java установки, ознакомьтесь с toodocumentation по [Oracle в веб-сайта](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Загрузите hello правильный двоичный пакет для вашей системы:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Другие методы установки можно найти в [документации по установке Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html).

1. Убедитесь, что Elasticsearch выполняется с помощью команды hello:

    ```
    curl http://127.0.0.1:9200
    ```

    Вы увидите примерно toothis ответа:

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

Дополнительные инструкции по установке эластичной поиска, см. страницу toohello [установки](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Установка Logstash

1. tooinstall Logstash выполните hello, следующие команды:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. Далее нам нужно tooread Logstash tooconfigure из выходных данных hello eve.json файла. Создайте файл logstash.conf следующим образом.

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Добавьте следующие файл содержимого toohello hello (Убедитесь, что это правильный файл eve.json toohello hello путь):

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

1. Сделайте что toogive hello правильные разрешения toohello eve.json файл, чтобы Logstash можно принять файл hello.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. toostart Logstash, выполните команду hello:

    ```
    sudo /etc/init.d/logstash start
    ```

См. инструкции по установке Logstash toohello [официальной документации](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-kibana"></a>Установка Kibana

1. Выполните следующие команды tooinstall Kibana hello.

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. toorun Kibana использование hello команд:

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. tooview Kibana веб-интерфейсом, слишком перехода`http://localhost:5601`
1. Для этого сценария является hello индекс модель использования hello журналы Suricata «logstash-*»

1. Панели мониторинга Kibana hello tooview удаленно, создать правило входящего трафика NSG, предоставляя доступ слишком**порт 5601**.

### <a name="create-a-kibana-dashboard"></a>Создание панели мониторинга Kibana

В этой статье мы предоставили используется пример информационной панели для вас tooview тенденции и сведения в своих предупреждений.

1. Загрузите файл мониторинга hello [здесь](https://aka.ms/networkwatchersuricatadashboard), файл визуализации hello [здесь](https://aka.ms/networkwatchersuricatavisualization)и файл сохранен hello поиска [здесь](https://aka.ms/networkwatchersuricatasavedsearch).

1. В группе hello **управления** вкладку из Kibana, перейдите слишком**сохраненные объекты** и импортировать все три файла. Затем из hello **мониторинга** вкладку, можно открыть и загрузка hello в примере информационной панели.

Вы можете также создать собственные визуализации и панели мониторинга, адаптированные к интересующим вас метрикам. Дополнительные сведения о визуализациях Kibana можно получить в [официальной документации по Kibana](https://www.elastic.co/guide/en/kibana/current/visualize.html).

![Панель мониторинга Kibana][2]

### <a name="visualize-ids-alert-logs"></a>Визуализация журналов оповещений IDS

Образец Hello панели мониторинга предоставляет несколько визуализаций журналов предупреждений Suricata hello.

1. Оповещения по GeoIP — карта, показывающая распределение hello оповещения по их стране происхождения, на основе географического расположения (определяется по IP-Адресу)

    ![Географическое распределение IP-адресов][3]

1. Первые 10 оповещения — Сводка по оповещениям hello 10 наиболее частые запуска и их описание. Щелкнув отдельное предупреждение фильтрует вниз hello мониторинга toohello сведения, соответствующие toothat конкретные предупреждения.

    ![рисунок 4][4]

1. Количество предупреждений — общее число оповещений, активируемых hello ruleset hello

    ![Рис. 5][5]

1. 20 основных источника или целевой IP-адресов и портов - круговых диаграмм, показывающие hello top 20 IP-адресов и портов, которые предупреждения было запущено на. Можно фильтровать работу на определенных IP-адресов и портов toosee количество и тип оповещения инициируются.

    ![Рис. 6][6]

1. Сводка оповещения — таблица с подробными сведениями по каждому конкретному оповещению. Tooshow этой таблицы можно настроить другие параметры, представляющие интерес для каждого предупреждения.

    ![Рис. 7][7]

Дополнительную документацию по созданию пользовательских визуализаций и панелей мониторинга см. в [официальной документации по Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).

## <a name="conclusion"></a>Заключение

Сочетая возможность записи пакетов, реализованную в Наблюдателе за сетями, и функции таких средств с открытым исходным кодом, как Suricata, вы можете определять сетевые вторжения самого разного толка. Эти панели мониторинга позволяют вам tooquickly отслеживать тенденции и аномалий в сети, также детализировать данные toodiscover основные причины предупреждения, например, злонамеренный пользователь агентов или уязвимым портам приветствия. С извлеченными данными можно принимать обоснованные решения с как tooreact tooand защиты сети от проникновения вредоносных попыток и Создание правила tooprevent будущих вторжения tooyour сети.

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как снимки tootrigger пакетов на основе оповещения, посетив [использовать пакет отслеживания toodo упреждающего мониторинга сети с помощью функций Azure](network-watcher-alert-triggered-packet-capture.md)

Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
