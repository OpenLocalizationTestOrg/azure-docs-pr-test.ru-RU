---
title: "выпуск aaaCanary с Vamp на кластере Azure DC/OS | Документы Microsoft"
description: "Как toouse Vamp toocanary выпуска служб и применить фильтрацию в кластере контейнера службы Azure DC/OS смарт-трафика"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Ранний выпуск микрослужб с помощью Vamp в кластере DC/OS Службы контейнеров Azure

В этом пошаговом руководстве мы настраиваем Vamp в Службе контейнеров Azure, используя кластер DC/OS. Мы предохранителя выпуска hello Vamp Демонстрация службы «sava», а затем устраните несовместимость hello службы с Firefox путем применения фильтрации смарт-трафика. 

> [!TIP] 
> В этом пошаговом руководстве Vamp работает на кластере DC/OS, но может также служить Vamp с Kubernetes hello orchestrator.
>

## <a name="about-canary-releases-and-vamp"></a>О ранних выпусках и Vamp


Функция [раннего выпуска](https://martinfowler.com/bliki/CanaryRelease.html) — это интеллектуальная стратегия развертывания, активно применяемая в таких инновационных компаниях, как Netflix, Facebook и Spotify. Такой подход полностью обоснован, так как он сокращает вероятность возникновения проблем, формирует сети безопасности и повышает уровень инноваций. Почему же его применяют не все компании? Расширение конвейера CI/CD tooinclude предохранителя стратегии повышает сложность и требует широко devops знания и опыт. Это достаточно tooblock небольших компаний и предприятий одинаково, прежде чем они даже приступить к работе. 

[Vamp](http://vamp.io/) — система открытым исходным кодом, предназначенная tooease этот переход и перевести предохранителя освободить планировщик контейнера tooyour основной функции. Функция раннего выпуска в Vamp предоставляет больше возможностей, чем выпуски на основе процентов. Трафик могут быть отфильтрованы и разбиение по широкий набор условий, например tootarget конкретных пользователей, диапазоны IP-адресов или устройств. Vamp отслеживает и анализирует метрики производительности, позволяя обеспечить автоматизацию на основе реальных данных. Можно настроить автоматический откат в случае возникновения ошибок или масштабировать индивидуальные варианты службы на основе нагрузки или задержки.

## <a name="set-up-azure-container-service-with-dcos"></a>Настройка Службы контейнеров Azure с помощью DC/OS



1. [Разверните кластер DC/OS](container-service-deployment.md) с одним главным узлом и двумя агентами, имеющими размер по умолчанию. 

2. [Создать туннель SSH](../container-service-connect.md) tooconnect toohello DC/OS кластера. В этой статье предполагается, что вы туннелирования toohello кластера на локальный порт 80.


## <a name="set-up-vamp"></a>Настройка Vamp

Теперь, когда запущенному кластеру DC/OS Vamp можно установить из hello пользовательского интерфейса DC/OS (http://localhost: 80). 

![Пользовательский интерфейс DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

Установка выполняется в два этапа:

1. **Разверните Elasticsearch**.

2. Затем **развертывание Vamp** путем установки пакета вселенной Vamp DC/OS hello.

### <a name="deploy-elasticsearch"></a>Развертывание Elasticsearch

Vamp требуется Elasticsearch для сбора метрик и агрегации. Можно использовать hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy совместимый стека Vamp Elasticsearch.

1. В hello DC/OS пользовательского интерфейса, перейдите слишком**службы** и нажмите кнопку **служба развертывания**.

2. Выберите **режим JSON** из hello **развернуть новую службу** всплывающих.

  ![Выбор режима JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. Вставьте следующий JSON hello. Эта конфигурация запускает hello контейнера с 1 ГБ ОЗУ и базовой проверки исправности через порт Elasticsearch hello.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. Щелкните **Развернуть**.

  Контроллер домена/OS развертывает hello Elasticsearch контейнера. Можно отслеживать ход выполнения hello **служб** страницы.  

  ![Развертывание Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Развертывание Vamp

После Elasticsearch отчеты в виде **под управлением**, можно добавить пакет Vamp вселенной DC/OS hello. 

1. Go слишком**Universe** и выполните поиск **vamp**. 
  ![Vamp на DC/OS Universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. Нажмите кнопку **установить** Далее toohello vamp пакета и выбрать **расширенный установки**.

3. Прокрутите список вниз и введите hello elasticsearch-URL-адреса: `http://elasticsearch.marathon.mesos:9200`. 

  ![Введение URL-адреса Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. Нажмите кнопку **просмотрите и установите**, нажмите кнопку **установить** toostart hello развертывания.  

  DC/OS развертывает все необходимые компоненты Vamp. Можно отслеживать ход выполнения hello **служб** страницы.
  
  ![Развертывание Vamp как пакета Universe](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. После завершения развертывания можно получить доступ к hello Vamp пользовательского интерфейса.

  ![Служба Vamp в DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Пользовательский интерфейс Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>Развертывание первой службы

Теперь, когда Vamp запущена и работает, разверните службу из схемы. 

В простейшей форме [Vamp чертежом](http://vamp.io/documentation/using-vamp/blueprints/) описывает конечные точки hello (шлюзов), кластеры и toodeploy служб. Vamp использует кластеров toogroup различные варианты hello же service в логические группы для предохранителя освобождение или A / B-тестирования.  

В этом сценарии используется пример монолитного приложения с именем [**sava**](https://github.com/magneticio/sava), которое имеет версию 1.0. Hello монолита упаковывается в контейнере Docker, которая находится в концентраторе Docker под magneticio/sava:1.0.0. приложение Hello, как правило, выполняется через порт 8080, но требуется его в порт 9050 в данном случае tooexpose. Разверните приложение hello через Vamp с помощью простой проект.

1. Go слишком**развертывания**.

2. Щелкните **Добавить**.

3. Вставить в hello следующий проект YAML. Эта схема содержит один кластер только с одним вариантом службы, который мы изменим в дальнейшем:

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. Щелкните **Сохранить**. Vamp инициирует развертывание hello.

Развертывание Hello значится на hello **развертываний** страницы. Нажмите кнопку развертывания toomonitor hello его состояние.

![Пользовательский интерфейс Vamp: развертывание sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Служба sava в пользовательском интерфейсе Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

Создаются два шлюза, перечислены на hello **шлюзы** страницы:

* hello tooaccess стабильный конечной точки службы (порт 9050) 
* внутренний шлюз, управляемый Vamp (позже мы рассмотрим этот шлюз подробнее). 

![Пользовательский интерфейс Vamp: шлюзы sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

Теперь развернута служба sava Hello, но не его извне тем hello подсистемы балансировки нагрузки Azure еще не знает tooit tooforward трафика. Служба tooaccess hello, обновление hello Azure конфигурации сети.


## <a name="update-hello-azure-network-configuration"></a>Обновление конфигурации сети Azure hello

Служба sava hello vamp развернуть на узлах агента hello DC/OS, предоставляют стабильный конечную точку на порте 9050. Служба hello tooaccess из вне кластера DC/OS hello, сделать hello следующая конфигурация сети Azure toohello изменения в развертывание кластера: 

1. **Настройка балансировки нагрузки Azure hello** hello агентов (hello ресурс с именем **dcos агента-балансировки нагрузки xxxx**) с зонда работоспособности и правило tooforward трафика через порт 9050 toohello sava экземплярами. 

2. **Группы безопасности сети hello обновление** hello общих агентов (hello ресурс с именем **XXXX-агента public-nsg-XXXX**) tooallow трафик через порт 9050.

Для toocomplete подробное описание действий для этих задач с помощью hello Azure портала, см. в разделе [включить приложение Azure контейнера службы общего доступа tooan](container-service-enable-public-access.md). Укажите порт 9050 для всех параметров портов.


Когда все будет создана, перейдите toohello **Обзор** колонке подсистемы балансировки нагрузки агента hello DC/OS (hello ресурс с именем **dcos агента-балансировки нагрузки xxxx**). Найти hello **общедоступный IP-адрес**и использовать sava tooaccess hello адресов на порту 9050.

![Портал Azure: получение общедоступного IP-адреса](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>Запуск раннего выпуска

Предположим, что у вас есть новая версия этого приложения, которые должны toocanary выпуска в рабочей среде. Вы его контейнерных как magneticio/sava:1.1.0 и toogo готовности. Vamp позволяет легко добавлять новые toohello служб под управлением развертывания. Эти службы «слияние» развернута вместе с существующими службами hello в кластере hello и вес 0%. Трафик не является службой перенаправленное tooa вновь слияние, пока настроить распределение трафика hello. ползунок вес Hello в hello Vamp пользовательского интерфейса дает полный контроль над распределением hello, позволяя пошаговой корректировки (предохранителя выпуск) или мгновенное отката.

### <a name="merge-a-new-service-variant"></a>Объединение нового варианта службы

toomerge hello новой sava 1.1 службы с hello выполнение развертывания:

1. В hello Vamp пользовательского интерфейса, выберите **чертежей**.

2. Нажмите кнопку **добавить** и вставить в следующие hello чертежом YAML: этот проект описывает новые toodeploy variant (sava: 1.1.0) службы в существующий кластер hello (sava_cluster).

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. Щелкните **Сохранить**. сохраняется и отображается на hello чертежом Hello **чертежей** страницы.

4. Привет открыть меню "действие" hello sava: 1.1 проект и выберите команду **слияние с**.

  ![Пользовательский интерфейс Vamp: схемы](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. Выберите hello **sava** развертывания и нажмите кнопку **слияния**.

  ![Vamp пользовательского интерфейса — слияния toodeployment план](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp развертывает hello новый sava: 1.1.0 службы вариант описывается в план действий hello вместе с sava: 1.0.0 в hello **sava_cluster** из hello развернут. 

![Пользовательский интерфейс Vamp: обновленное развертывание sava](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

Hello **sava/sava_cluster/webport** шлюза (конечная точка кластера hello) также обновляется, добавление toohello маршрута вновь установить sava: 1.1.0. На этом этапе не трафик направляется здесь (hello **ВЕС** имеет значение too0%).

![Пользовательский интерфейс Vamp: шлюз кластера](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Ранний выпуск

С обеими версиями sava развернутых в hello же кластера, hello распределение трафика между ними, перемещая hello **ВЕС** ползунок.

1. Нажмите кнопку ![Vamp пользовательского интерфейса — изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Далее слишком**ВЕС**.

2. Установите распространения too50%/50% hello вес и нажмите кнопку **Сохранить**.

  ![Пользовательский интерфейс Vamp: ползунок веса шлюза](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Вернитесь tooyour браузера и обновите страницу приветствия sava еще несколько раз. Теперь приложение Hello sava переключений между страницы sava: 1.0 и sava: 1.1.

  ![чередование служб sava1.0 и sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > Это чередования страницы приветствия лучше всего работает с hello «Браузера» или «Anonymous» режим браузера из-за hello кэширование статических активов.
  >

### <a name="filter-traffic"></a>Фильтрация трафика

Предположим, что после развертывания в sava:1.1.0 обнаружилась несовместимость, которая вызывает проблемы с отображением в браузерах Firefox. Можно задать Vamp toofilter входящего трафика и направить все пользователи Firefox обратно toohello известные стабильный sava: 1.0.0. Этот фильтр мгновенной разрешает hello перебоев в работе пользователей Firefox при любом другом клиенте tooenjoy преимущества hello hello повышение sava: 1.1.0.

Использует vamp **условия** toofilter трафик между маршруты в шлюз. Трафик сначала фильтруется и направляются соответствующим toohello условия, применяемые tooeach маршрута. Все остальные трафик распределяется в соответствии с параметром вес toohello шлюза.

Можно создать все пользователи Firefox toofilter условие и направлять их toohello старый sava: 1.0.0:

1. На hello sava/sava_cluster/webport **шлюзы** щелкните ![Vamp пользовательского интерфейса — изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd **УСЛОВИЕ** sava/sava_cluster/sava:1.0.0/webport toohello маршрута. 

2. Введите условие hello **агент пользователя == Firefox** и нажмите кнопку ![Vamp UI - Сохранить](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).

  Vamp добавляет условие hello с стойкость по умолчанию 0%. toostart фильтрации трафика, вы должны tooadjust hello условие силы.

3. Нажмите кнопку ![Vamp пользовательского интерфейса — изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **СТОЙКОСТЬ** применения toohello условие.
 
4. Набор hello **СТОЙКОСТЬ** too100% и нажмите кнопку ![Vamp UI - Сохранить](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.

  Теперь vamp отправляет весь трафик сопоставления toosava:1.0.0 hello условие (все пользователи Firefox).

  ![Vamp пользовательского интерфейса — применить условие toogateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. Наконец следует настройте все остальные трафика (все пользователи не Firefox) toohello новый sava: 1.1.0 toosend вес hello шлюза. Нажмите кнопку ![Vamp пользовательского интерфейса — изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Далее слишком**ВЕС** и установите распространения вес hello, направленной toohello sava/sava_cluster/sava:1.1.0/webport маршрута — 100%.

  Весь трафик, не фильтруется по условию hello сейчас новый расширенный toohello sava: 1.1.0.

6. Фильтр toosee hello в действии, откройте два различных браузеров (один Firefox и другой браузер) и службы sava hello обоих. Все запросы Firefox отправляются toosava:1.0.0, пока все другие браузеры, направленной toosava:1.1.0.

  ![Пользовательский интерфейс Vamp: фильтрация трафика](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>Подведем итоги

Эта статья переведена tooVamp Краткое введение в кластере DC/OS. Во-первых есть Vamp и запуск на контейнера службы Azure DC/ОС кластера, развернуть службу с чертежом Vamp и к нему доступ в конечной точке предоставляется hello (шлюз).

Мы рассмотрели некоторые мощные функции Vamp: слияние новых службы variant toohello развернут и введение в постепенно, а затем фильтрации трафика tooresolve известные несовместимости.


## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения об управлении Vamp действия через hello [Vamp API-интерфейса REST](http://vamp.io/documentation/api/api-reference/).

* Создайте сценарии автоматизации Vamp, используя Node.js, и выполните их как [рабочие процессы Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).

* Также ознакомьтесь с дополнительными [руководствами по VAMP](http://vamp.io/documentation/tutorials/overview/).

