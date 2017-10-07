---
title: "aaaContainer решения мониторинга в службе анализа журналов Azure | Документы Microsoft"
description: "решение для наблюдения за контейнера в службе анализа журналов Hello служит для просмотра и управления Docker и Windows узлы контейнера в одном месте."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Решение для мониторинга контейнеров в Log Analytics

![Символ решения "Контейнеры"](./media/log-analytics-containers/containers-symbol.png)

В этой статье описывается, как решение для наблюдения за контейнера в службы анализа журналов, который служит для просмотра и управления Docker и Windows hello tooset вверх и использовать узлы контейнера в одном месте. Docker — программной системы виртуализации используются контейнеры toocreate для автоматизации развертывания программного обеспечения tootheir ИТ инфраструктуры.

Здравствуйте, решение показывает, контейнеры, работающие под управлением, какой образ контейнера, они выполняются, и запущенным контейнеров. Также можно просматривать подробные сведения аудита, в том числе команды, используемые в контейнерах. И устранения контейнеры с помощью просмотра и поиска централизованные журналы без необходимости представление tooremotely Docker или узлов Windows. Решение позволяет находить контейнеры, содержащие ошибки и использующие слишком много ресурсов на узле. Также у вас есть возможность централизованно просматривать сведения об использовании и производительности ЦП, памяти, хранилища и сети по контейнерам. На компьютерах под управлением Windows можно централизовать и сравнивать журналы из Windows Server, Hyper-V и контейнеров Docker. решение Hello поддерживает следующие orchestrators контейнера hello:

- Docker Swarm
- DC/OS
- kubernetes
- Service Fabric
- Red Hat OpenShift.


Hello следующая диаграмма показывает hello связи между различными узлы контейнера и агентов в OMS.

![Схема контейнеров](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>Требования к системе

Прежде чем начать, просмотрите следующие сведения о tooverify требованиям hello hello.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Поддержка решений для мониторинга контейнеров: оркестратор Docker и платформа ОС
Hello следующей таблице показано hello Docker orchestration и операционной системы, наблюдение за поддержку инвентаризации контейнера, производительности и журналов с помощью аналитики журналов.   

| | ACS | Linux | Windows | Контейнер<br>Список | Образ —<br>Список | Узел<br>Список | Контейнер<br>Производительность | Контейнер<br>Событие | Событие<br>Журнал | Контейнер<br>Журнал |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| служба<br>Fabric | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat Open<br>Shift | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(изолированный) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Linux Server<br>(изолированный) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Версии Docker, поддерживаемые в Linux

- Docker 1.11 too1.13
- Docker CE и EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>Дистрибутивы Linux x64, поддерживаемые в качестве узлов контейнера

- Ubuntu 14.04 LTS и 16.04 LTS
- CoreOS (стабильный выпуск);
- Amazon Linux 2016.09.0;
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 и 7.3
- SLES 12
- RHEL 7.2 и 7.3
- Платформа контейнеров Red Hat OpenShift (OCP) 3.4 и 3.5
- Too1.8.8 DC/OS 1.7.3 ACS Mesosphere
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>Поддерживаемая операционная система Windows

- Windows Server 2016
- Юбилейный выпуск Windows 10 (профессиональный или корпоративный)

### <a name="docker-versions-supported-on-windows"></a>Версии Docker, поддерживаемые в Windows

- Docker 1.12 и 1.13
- Docker 17.03.0 и более поздних версий

## <a name="installing-and-configuring-hello-solution"></a>Установка и настройка решения hello
Используйте следующие сведения tooinstall hello и настроить решение hello.

1. Добавление hello мониторинга контейнера решение tooyour OMS рабочей области из [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).

2. Установите и используйте Docker с агентом OMS.  В зависимости от операционной системы, можно выбрать из hello следующие методы:

  * Установите на поддерживаемых операционных систем Linux, а запуска Docker и затем установите и настройте hello [агента OMS для Linux](log-analytics-agent-linux.md).  
  * На CoreOS невозможно запустить hello агента OMS для Linux. Вместо этого выполняется контейнерного версии hello агента OMS для Linux. Если вы работаете с контейнерами в облаке "Azure для государственных организаций", то см. раздел [Для всех узлов контейнера Linux, включая CoreOS](#for-all-linux-container-hosts-including-coreos) или [Для всех узлов контейнера Linux Azure для государственных организаций, включая CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos).
  * В Windows Server 2016 и Windows 10 установить hello подсистемы Docker и клиент затем подключения агента toogather сведения и отправить его tooLog Analytics.  

### <a name="container-services"></a>Служба контейнеров

- Если вы используете среду Red Hat OpenShift, то см. раздел [Настройка агента OMS для Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).
- При наличии Kubernetes кластер, использующий hello контейнера службы Azure, просмотрите [мониторинга контейнера службы Azure с Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).
- При наличии кластера DC/OS в службе контейнеров Azure дополнительные сведения см. в статье [Мониторинг кластера DC/OS в службе контейнеров Azure с помощью Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).
- При наличии среды режима Docker Swarm ознакомьтесь с разделом [Настройка агента OMS для Docker Swarm](#configure-an-oms-agent-for-docker-swarm).
- При использовании контейнеров с Service Fabric см. статью [Общие сведения о Service Fabric](../service-fabric/service-fabric-overview.md).
- Просмотрите hello [подсистема Docker в Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) статьи для получения дополнительных сведений о tooinstall и настройте ядер Docker на компьютерах под управлением Windows.

> [!IMPORTANT]
> Должен быть запущен docker **перед** установить hello [агента OMS для Linux](log-analytics-agent-linux.md) узлов контейнера. Если уже установлен агент hello перед установкой Docker, необходимо tooreinstall hello агента OMS для Linux. Дополнительные сведения о Docker см. в разделе hello [веб-узел Docker](https://www.docker.com).


## <a name="linux-container-hosts"></a>Узлы контейнера Linux

После установки Docker, используйте следующие параметры для агента hello tooconfigure узла контейнера для использования с помощью Docker hello. Во-первых, требуется свой идентификатор рабочей области OMS и ключ, который можно найти в hello портал Azure. В рабочей области, нажмите кнопку **быстрый запуск** > **компьютеры** tooview вашей **идентификатор рабочей области** и **первичный ключ**.  Скопируйте их и вставьте в любой удобный для вас редактор.

### <a name="for-all-linux-container-hosts-except-coreos"></a>Для всех узлов контейнера Linux, за исключением CoreOS

- Дополнительные сведения и инструкции по как tooinstall hello агента OMS для Linux см. в разделе [подключения на компьютерах Linux tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).

### <a name="for-all-linux-container-hosts-including-coreos"></a>Для всех узлов контейнера Linux, включая CoreOS

Запустите контейнер hello OMS, что требуется toomonitor. Изменить и использовать следующий пример hello:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>Для всех узлов контейнера Linux Azure для государственных организаций, включая CoreOS

Запустите контейнер hello OMS, что требуется toomonitor. Изменить и использовать следующий пример hello:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>Переключение из установленных tooone агент Linux, в контейнере с помощью
Если ранее используется hello напрямую установлен агент и требуется использование tooinstead агента, работающего в контейнере, необходимо сначала удалить hello агента OMS для Linux. В разделе [hello Удаление агента OMS для Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand, как удалить toosuccessfully hello агента.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Настройка агента OMS для Docker Swarm

Hello агента OMS как глобальная служба запускается с помощью Docker Swarm. Используйте следующие сведения toocreate службу агента OMS hello. Необходимо tooinsert идентификатор рабочей области OMS и первичный ключ.

- Запустите следующие hello hello главного узла.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Настройка агента OMS для Red Hat OpenShift
Нет агента OMS hello tooRed Hat OpenShift toostart сбора данных мониторинга данные контейнера для трех способов tooadd.

* [Установка hello агента OMS для Linux](log-analytics-agent-linux.md) непосредственно на каждом узле OpenShift  
* [включить расширение виртуальной машины Log Analytics](log-analytics-azure-vm-extension.md) на каждом узле OpenShift, размещенном в Azure;  
* Установка агента OMS hello как набор управляющей программы OpenShift  

В этом разделе будет рассматриваться как набор управляющая программа OpenShift hello действия требуется tooinstall hello агента OMS.  

1. Войдите на toohello OpenShift главного узла и скопируйте hello yaml файла [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) из GitHub tooyour главного узла и изменить значение hello с Идентификатором рабочей области OMS и первичный ключ.
2. Запустите следующие команды toocreate hello проекта для OMS и задайте hello учетной записи пользователя.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. hello toodeploy управляющей программы набора, выполните следующие hello:

    `oc create -f ocp-omsagent.yaml`

5. tooverify может быть сконфигурирован и работают правильно, введите ниже hello:

    `oc describe daemonset omsagent`  

    и hello выходные данные должны иметь:

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

Секреты toosecure toouse идентификатор рабочей области OMS и первичный ключ при использовании файла yaml набор управляющей программы агента OMS hello, выполните hello следующие шаги.

1. Войдите на toohello OpenShift главного узла и скопируйте hello yaml файла [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) и секрет Создание сценария [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) из GitHub.  Данный сценарий создаст файл yaml секреты hello для toosecure идентификатор рабочей области OMS и первичный ключ к secrete сведения.  
2. Запустите следующие команды toocreate hello проекта для OMS и задайте hello учетной записи пользователя. Создание скрипта секрет Hello запрашивает свой идентификатор рабочей области OMS <WSID> и первичный ключ <KEY> и после завершения, он создает файл ocp secret.yaml hello.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Развертывание файла секретный hello, выполнив следующие hello:

    `oc create -f ocp-secret.yaml`

5. Проверка развертывания, выполнив следующие hello:

    `oc describe secret omsagent-secret`  

    и hello выходные данные должны иметь:  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Развертывание файла yaml набор управляющей программы агента OMS hello, выполнив следующие hello:

    `oc create -f ocp-ds-omsagent.yaml`  

7. Проверка развертывания, выполнив следующие hello:

    `oc describe ds oms`

    и hello выходные данные должны иметь:

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Защита секретных сведений для Docker Swarm и Kubernetes

Вы можете защитить секретный идентификатор рабочей области OMS и первичные ключи для служб контейнеров Docker Swarm и Kubernetes.

#### <a name="secure-secrets-for-docker-swarm"></a>Защита секретов для Docker Swarm

Для помощью Docker Swarm, создав hello секрет для идентификатора рабочей области и первичный ключ, вы можете запустить hello создайте службу hello Docker для OMSagent. Используйте следующие сведения toocreate hello секретные данные.

1. Запустите следующие hello hello главного узла.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. Убедитесь, что секретные данные созданы надлежащим образом.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. Выполнения hello, следующая команда toomount hello секреты toohello контейнерных агента OMS.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>Защита секретов для Kubernetes с помощью файлов YAML

Для Kubernetes используйте файл сценария секреты hello toogenerate yaml для идентификатора рабочей области и первичный ключ. В hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) есть файлы, которые можно использовать с или без вашего конфиденциальные сведения.

- Hello DaemonSet по умолчанию для агента OMS имеет секретные сведения (omsagent.yaml)
- файл yaml Hello DaemonSet агента OMS использует секретные сведения (secrets.yaml omsagent доменных служб Active Directory) с файл yaml (omsagentsecret.yaml) секреты hello toogenerate секретный формирования сценариев.

Вы можете toocreate omsagent DaemonSets с или без секретные данные.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>Стандартный файл YAML DaemonSet агента OMS без секретов

- Для файла yaml DaemonSet агента OMS по умолчанию hello, замените hello `<WSID>` и `<KEY>` tooyour WSID и ключ. Скопируйте hello файл tooyour главного узла и выполнения hello следующее:

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>Стандартный файл YAML DaemonSet агента OMS с секретами

1. toouse DaemonSet агента OMS с помощью секретная информация, создайте hello секретные данные.
    1. Скопируйте сценарий hello и файл секретный шаблона и убедитесь, что они находятся на hello один каталог.
        - Сценарий создания секретов — secret-gen.sh
        - Шаблон секретов — secret-template.yaml
    2. Выполните сценарий hello, как следующий пример hello. Hello скрипт запрашивает hello идентификатор рабочей области OMS и первичный ключ и после их ввода hello скрипт создает секретный yaml файл, чтобы можно было запустить.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Создайте pod hello секретные данные, выполнив следующие hello:
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify hello следующей:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        Выходные данные должны выглядеть примерно так:

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        Выходные данные должны выглядеть примерно так:

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. Создание свой набор daemon-set omsagent, выполнив команду ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```

2. Проверьте, hello запущенного DaemonSet агента OMS аналогичные toohello следующие:

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Для Kubernetes используйте файл сценария секреты hello toogenerate yaml идентификатор рабочей области и первичный ключ. Hello используйте следующую информацию пример с hello [omsagent yaml файл](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure вашей конфиденциальные сведения.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a>Узлы контейнеров Windows

### <a name="preparation-before-installing-windows-agents"></a>Подготовка к установке агентов Windows

Прежде чем устанавливать агенты на компьютерах под управлением Windows, необходима служба Docker tooconfigure hello. Настройка Hello позволяет hello Windows агента или hello анализа журналов виртуальную машину расширения toouse hello сокета Docker TCP, чтобы агенты hello можно удаленный доступ к управляющей программе Docker hello и toocapture данных мониторинга.

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker и проверьте его конфигурацию

Существует tooset шаги, которые необходимы копирование TCP, именованный канал для Windows Server.

1. Включите канал TCP и именованный канал в Windows PowerShell.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. Настройка Docker с hello файла конфигурации для канала TCP и именованного канала. Hello файл конфигурации расположен в C:\ProgramData\docker\config\daemon.json.

    В файле daemon.json hello вам потребуется hello следующее:

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

Дополнительные сведения о настройке управляющей программы Docker hello, используемые с контейнерами Windows см. в разделе [подсистема Docker в Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).


### <a name="install-windows-agents"></a>Установка агентов Windows

tooenable Windows и контейнер Hyper-V наблюдения, установите hello агента наблюдения Майкрософт (MMA) на компьютерах Windows, которые являются узлами контейнера. Для компьютеров под управлением Windows в локальной среде, в разделе [tooLog компьютеров Windows для подключения аналитики](log-analytics-windows-agents.md). Для виртуальных машин, запущенных в Azure, подключите их tooLog аналитика с помощью hello [расширение виртуальной машины](log-analytics-azure-vm-extension.md).

Вы можете отслеживать контейнеры Windows, запущенные в Service Fabric. Однако сейчас для Service Fabric поддерживаются только [виртуальные машины, работающие в Azure](log-analytics-azure-vm-extension.md), и [компьютеры под управлением Windows в локальной среде](log-analytics-windows-agents.md).

Можно проверить, что правильно установлены, hello решения отслеживания контейнера Windows. toocheck ли пакет управления hello был загрузки надлежащим образом, поиск *ContainerManagement.xxx*. Hello файлы должны находиться в папке C:\Program Files\Microsoft мониторинг Agent\Agent\Health Service State\Management Packs hello.


## <a name="solution-components"></a>Компоненты решения

При использовании агентов Windows, затем hello следующий пакет управления устанавливается на каждом компьютере с агентом при добавлении этого решения. Настройки или обслуживания является обязательным для пакета управления hello.

- *ContainerManagement.xxx* устанавливается в папке, расположенной по адресу C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.

## <a name="container-data-collection-details"></a>Сведения о сборе данных из контейнеров
Hello решения отслеживания контейнера сбор узлы контейнера и контейнеры, агенты, которые можно включить с помощью различных данных метрики и журнала производительности.

Собирает данные каждые три минуты hello следующие типы агентов.

- [Агент OMS для Linux](log-analytics-linux-agents.md)
- [Агент Windows](log-analytics-windows-agents.md)
- [Расширение виртуальной машины Log Analytics](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>Записи контейнеров

Hello следующей таблице приведены примеры записей, собранные решением отслеживания контейнера hello и hello типы данных, которые отображаются в результатах поиска журналов.

| Тип данных | Тип данных, используемый для поиска в журналах | Поля |
| --- | --- | --- |
| Производительность узлов и контейнеров | `Type=Perf` | Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem |
| Список контейнеров | `Type=ContainerInventory` | TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID |
| Список образов контейнеров | `Type=ContainerImageInventory` | TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer |
| Журнал контейнеров | `Type=ContainerLog` | TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID |
| Журнал службы контейнеров | `Type=ContainerServiceLog`  | TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID |
| Список узлов контейнеров | `Type=ContainerNodeInventory_CL`| TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Список Kubernetes | `Type=KubePodInventory_CL` | TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| Процесс контейнера | `Type=ContainerProcess_CL` | TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| События Kubernetes | `Type=KubeEvents_CL` | TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message |

Метки добавлено слишком*PodLabel* типами данных являются собственные пользовательские метки. Hello присоединенных PodLabel метки, приведенных в таблице hello приведены примеры. Таким образом, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` будут отличаться в наборе данных вашей среды и должны выглядеть примерно так: `PodLabel_yourlabel_s`.


## <a name="monitor-containers"></a>Мониторинг контейнеров
После включения на портале OMS hello решения hello, hello **контейнеры** плитки отображаются сводные данные о узлах контейнера и контейнерами hello в узлах.

![Плитка "Контейнеры"](./media/log-analytics-containers/containers-title.png)

Плитка приветствия приведен обзор количество контейнеров в среде hello и ли они все не удалось, запущенной или остановленной.

### <a name="using-hello-containers-dashboard"></a>С помощью панели мониторинга контейнеры hello
Нажмите кнопку hello **контейнеры** плитки. Отсюда можно открыть представления, упорядоченные по:

- **Событиям контейнера.** Здесь отображается состояние контейнера и компьютеры, содержащие контейнеры со сбоями.
- **Журналы контейнера** -показана диаграмма контейнера файлов журнала, созданные со временем и список компьютеров с hello наибольшее количество файлов журнала.
- **События Kubernetes** -показана диаграмма Kubernetes события, создаваемые со временем и список hello причин, почему модулей созданных событий hello. *Этот набор данных используется только в средах Linux.*
- **Инвентаризацию пространств имен Kubernetes** — показывает количество hello пространств имен и модулей и показывает их иерархии. *Этот набор данных используется только в средах Linux.*
- **Инвентаризация узел контейнера** -показывает количество hello orchestration типы, используемые на узлы контейнера. узлы и узлы, Hello компьютера также перечислены hello число контейнеров. *Этот набор данных используется только в средах Linux.*
- **Контейнер образов инвентаризации** -показывает общее количество контейнера изображений, используемых для hello и количество типов изображений. Hello несколько образов, также перечислены hello тег изображения.
- **Состояние контейнеры** -показывает общее количество hello контейнера узлов или узел компьютеров с запущенными контейнерами. Hello число запущенных узлов также перечислены компьютеры.
- **Процессу контейнера.** Здесь отображается график процессов контейнера, выполняемых за период времени. Контейнеры также перечислены по выполняемым в них командам или процессам. *Этот набор данных используется только в средах Linux.*
- **Производительность ЦП контейнера** -показывает график hello средняя загрузка ЦП со временем для компьютера узлы. Также перечислены hello компьютера узлы и узлы, основанные на средней загрузки ЦП.
- **Производительности памяти контейнера.** Здесь отображается график использования памяти по времени, а также использование памяти компьютера по имени экземпляра.
- **Производительность компьютера** -показывает процент использования памяти со временем и объем свободного места на диске графиках hello процентов производительности ЦП с течением времени, с течением времени. Наводите указатель мыши на любую строку в tooview диаграммы Дополнительные сведения см.


Каждая область hello мониторинга — это визуальное представление поиска, которое запускается на собранных данных.

![Панель мониторинга "Контейнеры"](./media/log-analytics-containers/containers-dash01.png)

![Панель мониторинга "Контейнеры"](./media/log-analytics-containers/containers-dash02.png)

В hello **состояние контейнера** области, щелкните hello верхней области, как показано ниже.

![Состояние контейнера](./media/log-analytics-containers/containers-status.png)

Откроется поиска журналов сведения о состоянии hello вашей контейнеров.

![Колонка "Поиск по журналам" для контейнеров](./media/log-analytics-containers/containers-log-search.png)

Здесь можно изменить toomodify запрос поиска hello его конкретные сведения toofind hello вас интересует. Дополнительные сведения об использовании поиска по журналам см. в статье [Поиск по журналам в Log Analytics](log-analytics-log-searches.md).

## <a name="troubleshoot-by-finding-a-failed-container"></a>Устранение неполадок с помощью поиска контейнера со сбоем

Log Analytics добавляет к контейнеру пометку **Сбой**, если такой контейнер завершил работу с ненулевым кодом выхода. Можно просмотреть обзор hello ошибок и сбоев в среде hello в hello **сбой контейнеры** области.

### <a name="toofind-failed-containers"></a>не удалось выполнить toofind контейнеров
1. Нажмите кнопку hello **состояние контейнера** области.  
   ![состояние контейнера](./media/log-analytics-containers/containers-status.png)
2. Поиск журналов открывает и отображает состояние hello вашей контейнеров, аналогичные toohello следующие.  
   ![Состояние контейнеров](./media/log-analytics-containers/containers-log-search.png)
3. После этого щелкните значение hello суммарный неудачных контейнеры tooview дополнительных сведений. Разверните **Показать больше** ИД tooview hello образа.  
   ![Контейнеры со сбоями](./media/log-analytics-containers/containers-state-failed.png)  
4. Далее введите ниже hello в hello поискового запроса. `Type=ContainerInventory <ImageID>`toosee подробные сведения о hello изображения, например размер образа и число образов остановлена, которая завершилась неудачно.  
   ![Контейнеры со сбоями](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>Поиск данных контейнера по журналам
При устранении неполадок конкретную ошибку, он может помочь toosee, где происходит в вашей среде. следующие типы журналов Hello поможет вам создать запросы нужные сведения tooreturn hello.


- **ContainerImageInventory** — этот тип используется, если вы пытаетесь toofind данные, организованные изображения и tooview изображения такие сведения, идентификаторы изображения или размеров.
- **ContainerInventory** — этот тип используется для получения сведений о расположении контейнеров, их именах и образах, которые в них выполняются.
- **ContainerLog** — используйте этот тип, если нужно toofind конкретных сведений об ошибке журнала и записи.
- **ContainerNodeInventory_CL** этот тип используется hello сведения о узла и где находятся контейнеры. С его помощью можно получить сведения о версии Docker, типе оркестрации, хранилище и сведения о сети.
- **ContainerProcess_CL** используйте этот тип tooquickly разделе hello процесс, запущенный в контейнере hello.
- **ContainerServiceLog** — этот тип используется, если вы пытаетесь toofind аудита сведения об аудите для hello управляющей программы Docker, такие как запуск, остановка, удалить или по запросу команды.
- **KubeEvents_CL** использовать этот тип toosee hello Kubernetes события.
- **KubePodInventory_CL** этот тип используется при необходимости сведения об иерархии toounderstand hello кластера.


### <a name="toosearch-logs-for-container-data"></a>toosearch журналы для контейнера данных
* Выберите изображение, которое известно недавно произошел сбой и поиск журналов ошибок hello. Сначала найдите имя контейнера, в котором выполняется этот образ, выполнив поиск в журнале **ContainerInventory**. Например, выполните поиск по запросу `Type=ContainerInventory ubuntu Failed`  
    ![Поиск контейнеров Ubuntu](./media/log-analytics-containers/search-ubuntu.png)

  Здравствуйте имя контейнера hello рядом слишком**имя**и выполните поиск эти журналы. В нашем примере поисковый запрос будет выглядеть так: `Type=ContainerLog cranky_stonebreaker`.

**Просмотр сведений о производительности**

При начиная tooconstruct запросы, может помочь toosee возможности возможных сначала. Например toosee поиск все данные производительности, попробуйте hello общих запросов, введя следующий запрос.

```
Type=Perf
```

![Производительность контейнеров](./media/log-analytics-containers/containers-perf01.png)

Вы можете задать область hello данные о производительности, что вы видите tooa конкретному контейнеру, введя имя hello его toohello справа от запроса.

```
Type=Perf <containerName>
```

Отображается список hello метрики производительности, собранных для отдельных контейнера.

![Производительность контейнеров](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>Примеры запросов для поиска по журналам
Часто полезно toobuild запрашивает начиная с примером или два, а затем изменить их toofit вашей среде. В качестве отправной точки, можно поэкспериментировать с hello **примеры запросов** toohelp область построения более сложные запросы.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Запросы по контейнерам](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>Сохранение запросов для поиска по журналам
Сохранение запросов — это стандартная функция в Log Analytics. Она позволяет сохранять полезные запросы для использования в будущем.

После создания запроса, который вам пригодиться, сохраните его, выбрав **Избранное** hello верхней части страницы поиска журналов hello. Затем можно легко получить его позже из hello **Моя панель мониторинга** страницы.

## <a name="next-steps"></a>Дальнейшие действия
* [Выполнять поиск в журналах](log-analytics-log-searches.md) tooview подробные записи данных контейнера.
