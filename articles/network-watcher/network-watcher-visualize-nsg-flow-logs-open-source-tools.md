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
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Визуализация журнала потоков для групп безопасности сети Наблюдателя за сетями Azure с помощью инструментов с открытым кодом

Журналы потоков для групп безопасности сети содержат информацию о входящем и исходящем IP-трафике групп безопасности сети. Эти журналы потока Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5 кортежей сведения о hello потока (источник и назначение IP-адресов, исходного или целевого порта протокола), и если hello трафик разрешен или запрещен.

Эти журналы потока можно трудно toomanually синтаксического анализа и получения полезных сведений из. Однако существует несколько инструментов с открытым кодом, которые могут помочь визуализировать эти данные. В этой статье приводятся toovisualize решения эти журналы hello эластичной стека с помощью которых будет позволяют tooquickly индекса и визуализировать потока журналов на Kibana панели мониторинга.

## <a name="scenario"></a>Сценарий

В этой статье мы определим решение, которое позволит вам toovisualize сетевой группы безопасности потока журналы, с помощью hello эластичной стека.  Подключаемый модуль ввода Logstash будет получать журналы потока hello непосредственно из hello BLOB-объекта хранилища настроена для hello журналы потока, содержащего. Затем, используя hello эластичной стека, hello потока журналы будут индексироваться и использовать toocreate Kibana сведений о hello мониторинга toovisualize.

![сценарий][scenario]

## <a name="steps"></a>Действия

### <a name="enable-network-security-group-flow-logging"></a>Включение ведения журнала потоков для групп безопасности сети
В рамках данного сценария вам необходимо включить ведение журнала потоков по меньшей мере для одной группы безопасности сети в своей учетной записи. Инструкции по включению журналы потока сетевой безопасности см. в следующей статьей toohello [ведения журнала tooflow введение для групп безопасности сети](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-hello-elastic-stack"></a>Настройка hello эластичной стека
Подключив NSG потока журналов с помощью hello эластичной стека, мы можно создать панель мониторинга Kibana, что мы сможем toosearch, граф, анализировать и производные от наших журналов аналитики.

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
1. Далее нам нужна tooconfigure Logstash tooaccess и проанализировать журналы hello потока. Создайте файл logstash.conf следующим образом.

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Добавьте следующие файл содержимого toohello hello:

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

См. инструкции по установке Logstash toohello [официальной документации](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Установите hello Logstash ввода подключаемый модуль для хранилища BLOB-объектов Azure

Этот подключаемый модуль Logstash позволит вам toodirectly hello потока журналы событий из своей учетной записи указанного хранилища. tooinstall этого подключаемого модуля в каталог установки Logstash hello по умолчанию (в этом вариантов /usr/share/logstash/bin) команду hello:

```
logstash-plugin install logstash-input-azureblob
```

toostart Logstash, выполните команду hello:

```
sudo /etc/init.d/logstash start
```

Дополнительные сведения о данном подключаемом модуле см. в разделе toodocumentation [здесь](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

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
1. В этом сценарии шаблон hello индекса, используемый для потока журналов hello — «nsg потока журналы». Можно изменить шаблон индекс hello в разделе «выход» hello logstash.conf файла.

1. Панели мониторинга Kibana hello tooview удаленно, создать правило входящего трафика NSG, предоставляя доступ слишком**порт 5601**.

### <a name="create-a-kibana-dashboard"></a>Создание панели мониторинга Kibana

В этой статье мы предоставили используется пример информационной панели для вас tooview тенденции и сведения в своих предупреждений.

![Рисунок 1][1]

1. Загрузите файл мониторинга hello [здесь](https://aka.ms/networkwatchernsgflowlogdashboard), файл визуализации hello [здесь](https://aka.ms/networkwatchernsgflowlogvisualizations)и файл сохранен hello поиска [здесь](https://aka.ms/networkwatchernsgflowlogsearch).

1. В группе hello **управления** вкладку из Kibana, перейдите слишком**сохраненные объекты** и импортировать все три файла. Затем из hello **мониторинга** вкладку, можно открыть и загрузка hello в примере информационной панели.

Вы можете также создать собственные визуализации и панели мониторинга, адаптированные к интересующим вас метрикам. Дополнительные сведения о визуализациях Kibana можно получить в [официальной документации по Kibana](https://www.elastic.co/guide/en/kibana/current/visualize.html).

### <a name="visualize-nsg-flow-logs"></a>Визуализация журналов потоков NSG

Образец Hello панели мониторинга предоставляет несколько визуализаций hello потока журналов:

1. Потоки, принятия решений и направления за период времени — времени рядов диаграмм, отображая hello число потоков с течением hello период времени. Единица времени hello и диапазон оба эти представления можно изменить. Потоки путем принятия решений показано hello долю разрешение или запрет решения, принимаемые при потоки с пропорций hello показывает направление входящего и исходящего трафика. С помощью этих визуальных элементов можно проверять тенденции трафика с течением времени и искать какие-либо пики или нестандартные шаблоны.

  ![Рисунок 2][2]

1. Потоки с целевой и исходный порт — портами hello распределение потоков tootheir соответствующих круговые диаграммы. В этом представлении можно увидеть наиболее часто используемые порты. При нажатии на конкретный порт в круговой диаграмме hello rest hello мониторинга hello отфильтрует вниз tooflows порта.

  ![Рисунок 3][3]

1. Число потоков и самое раннее время журнала — метрики, показывая hello количество потоков, записанных, полученной hello дату ранней журнала hello.

  ![Рисунок 4][4]

1. Потоки, NSG и правило — Гистограмма показывает распределение потоков в пределах каждого NSG hello, а также распространения hello правил в каждом NSG. Отсюда можно видеть какие NSG и правил, сформированных hello большая часть трафика.

  ![Рисунок 5][5]

1. Первые 10 источника или целевой IP-адресов — панель диаграмм, показывающие hello первые 10 исходный и конечный IP-адреса. Вы можете настроить эти диаграммы tooshow больше или меньше верхней IP-адресов. Здесь вы может hello, наиболее часто встречающихся IP-адресов в разделе, а также hello трафика принятия решений ("Разрешить" или "Запретить"), выполненный для каждого IP.

  ![Рисунок 6][6]

1. Кортежи потока — в этой таблице показано hello сведения, содержащиеся в пределах каждого кортежа потока, а также его соответствующие параметры и правила.

  ![Рисунок 7][7]

Использование панели запросов hello hello верхней части панели мониторинга hello, можно отфильтровать вниз hello панели мониторинга на основе любого параметра hello потокам, такие как идентификатор подписки, группы ресурсов, правило или любую другую переменную, представляющие интерес. Дополнительные сведения о запросах и фильтрах Kibana ссылаться toohello [официальной документации](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Заключение

Объединяя hello сетевой группы безопасности потока журналы hello эластичной стека, мы придумать мощное и настраиваемые toovisualize нашей сетевого трафика. Эти панели мониторинга позволяют tooquickly прибыль и обмениваться информацией о сетевой трафик, а также фильтровать вниз и исследовать на любой потенциальных нарушений. Kibana можно адаптировать эти панели мониторинга и создания определенных визуализации toomeet любого аудита безопасности и соответствия требованиям.

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
