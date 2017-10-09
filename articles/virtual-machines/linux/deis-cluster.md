---
title: "aaaDeploy Deis 3-узловой кластер | Документы Microsoft"
description: "В этой статье описывается как toocreate 3-узловой Deis кластера в Azure с помощью шаблона диспетчера ресурсов Azure"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Развертывание и настройка 3-узлового кластера Deis в Azure
В этой статье пошагово описана подготовка кластера [Deis](http://deis.io/) в Azure. Она охватывает все действия hello на создание сертификатов, необходимых toodeploying hello и масштабирование образец **Go** приложение hello нового кластера.

Hello следующей схеме показана архитектура hello hello развертывания системы. Системный администратор управляет hello кластера с помощью Deis средств, таких как **deis** и **deisctl**. Соединения устанавливаются с помощью балансировки нагрузки Azure, направляет tooone подключений hello члена hello узлы в кластере hello. доступ клиентов Hello развернутых приложений через hello также балансировки нагрузки. В этом случае балансировки нагрузки hello перенаправляет трафик tooa hello Deis сетки маршрутизатор, который дальнейшей перенаправляет вызвавший контейнеры Docker toocorresponding трафика, размещенных в кластере hello.

  ![Схема архитектуры развернутого кластера Deis](./media/deis-cluster/architecture-overview.png)

Порядок toorun через hello, выполнив действия вам потребуется:

* Активная подписка Azure. Если у вас ее нет, можно получить бесплатную ознакомительную версию на сайте [azure.com](https://azure.microsoft.com/).
* Рабочий или группы ресурсов Azure toouse идентификатор учебного заведения. Если имеется личная учетная запись и войти в систему с Microsoft id, необходимо слишком[создать из вашего личного один идентификатор рабочего](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Либо — в зависимости от операционной системы клиента--hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) или hello [Azure CLI для Mac, Linux и Windows](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL — используется toogenerate hello необходимые сертификаты.
* Клиент Git, например [Git Bash](https://git-scm.com/).
* Пример приложения hello tootest, кроме того, потребуется DNS-сервера. Можно использовать любые DNS-серверы или службы, которые поддерживают записи A с подстановочным знаком.
* Toorun компьютер Deis клиентских средств. Можно использовать локальный компьютер или виртуальную машину. Эти инструменты можно использовать на любой дистрибутив Linux, но hello следующие инструкции используют Ubuntu.

## <a name="provision-hello-cluster"></a>Подготовка кластера hello
В этом разделе мы используем [диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-overview.md) шаблона из открытого репозитория hello [azure — начало работы — шаблоны](https://github.com/Azure/azure-quickstart-templates). Во-первых будет копировать вниз hello шаблона. Затем создадите новую пару ключей SSH для аутентификации. После этого вы настроите новый идентификатор для кластера. И наконец, используйте сценарий hello или hello PowerShell скрипт tooprovision hello кластера.

1. Репозиторий hello клона: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Перейдите в папку toohello шаблона:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. Создайте новую пару ключей SSH, используя ssh-keygen:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Создайте сертификат с помощью hello выше закрытого ключа:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. Go слишком[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate новый маркер кластера, который выглядит примерно:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Для каждого кластера CoreOS должен toohave уникального токена из этой бесплатной службой. Дополнительные сведения см. в [документации по CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/).
6. Изменить hello **облака config.yaml** файла существующие hello tooreplace **обнаружения** токена с hello новый маркер:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Изменение hello **azuredeploy parameters.json** файла: hello откройте сертификат, созданный на шаге 4, в текстовом редакторе. Скопируйте весь текст между `----BEGIN CERTIFICATE-----` и `-----END CERTIFICATE-----` в hello **sshKeyData** параметра (потребуется tooremove все символы новой строки).
8. Изменение hello **newStorageAccountName** параметра. Это учетная запись хранения hello для дисков операционной системы виртуальной Машины. Это имя учетной записи имеет toobe глобально уникальным.
9. Изменение hello **publicDomainName** параметра. Это значение станет частью hello DNS-имя, связанное с общедоступным IP-подсистемы балансировки нагрузки hello. Hello окончательного полное доменное имя будет иметь формат hello *[значение этого параметра]*. *[region]* . cloudapp.azure.com. Например если указать имя hello как deishbai32 и группы ресурсов hello toohello развернутой области Запад США, а затем hello окончательного deishbai32.westus.cloudapp.azure.com будет балансировки нагрузки tooyour полное доменное имя.
10. Сохраните файл параметров hello. И затем можно подготовить hello кластера с помощью Azure PowerShell:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    Или с помощью Azure CLI:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. После подготовки hello группы ресурсов, можно просмотреть все ресурсы hello в группе hello на классический портал Azure. Как показано на следующий снимок экрана, hello hello, группа ресурсов содержит виртуальную сеть с трех виртуальных машин, которые являются объединить toohello одной группе доступности. Группа Hello также содержит подсистему балансировки нагрузки, имеющая связанный общедоступный IP-адрес.
    
    ![Группа ресурсов на классический портал Azure подготовлена Hello](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Установка клиента на приветствия
Требуется **deisctl** toocontrol вашей Deis кластера. Несмотря на то, что deisctl автоматически устанавливается на всех узлах кластера hello, это deisctl toouse рекомендаций на отдельном компьютере правами администратора. Кроме того так как все узлы должны быть настроены только частные IP-адреса, вам потребуется toouse туннелирования SSH с помощью подсистемы балансировки нагрузки hello, имеющая общедоступный IP-адрес, узел машины tooconnect toohello. Hello ниже приведены hello шаги по настройке deisctl на отдельном Ubuntu физической или виртуальной машины.

1. Установите deisctl:mkdir deis:
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Добавление агента toossh закрытого ключа:
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Настройте deisctl:
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

Hello шаблон определяет NAT правила для входящих подключений, которые сопоставляют 2223 tooinstance 1, 2224 tooinstance 2 и 2225 tooinstance 3. Это обеспечивает избыточность для использования инструмента deisctl hello. Можно просмотреть эти правила на классическом портале Azure.

![Подсистема балансировки нагрузки правила NAT на hello](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> В настоящее время шаблона hello поддерживает только 3 узлов кластеров. Это связано с ограничением в определении правил NAT шаблона диспетчера ресурсов Azure, которое не позволяет использовать синтаксис цикла.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>Установка и запуск hello Deis платформы
Теперь можно использовать deisctl tooinstall и запустить hello Deis платформа:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Начальный платформы hello занимает некоторое время (до 10 минут). Особенно запуск hello построитель службы может занять много времени. Иногда занимает несколько попыток toosucceed: Если hello операции toohang, попробуйте ввести `ctrl+c` toobreak выполнения команды hello и повторите попытку.
> 
> 

Можно использовать `deisctl list` tooverify, если все службы запущены:

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

Поздравляем! Теперь у вас есть работающий кластер Deis в Azure! Теперь давайте развернуть пример Go приложения toosee hello кластера в действии.

## <a name="deploy-and-scale-a-hello-world-application"></a>Развертывание и масштабирование приложения Hello World
Hello следующие шаги показывают, как toodeploy «Hello World» Go кластера toohello приложения. на основе действия Hello [Deis документации](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Для маршрутизации toowork сетки hello надлежащим образом, вам потребуется toohave запись A подстановочный знак для вашего домена, указывающий toohello общедоступный IP-адрес подсистемы балансировки нагрузки hello. Hello следующем снимке экрана показана запись hello A для регистрации домена образец на GoDaddy:
   
    ![Запись A Godaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Установите deis:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Создание нового ключа SSH, а затем добавьте открытого ключа tooGitHub hello (Конечно, можно также повторно использовать существующие ключи). toocreate новую пару ключей SSH, используйте:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. Добавьте id_rsa.pub или открытый ключ hello по своему усмотрению, tooGitHub. Это можно сделать с помощью hello добавить SSH ключа кнопки на экране настройки ключей SSH:
   
   ![Ключ GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. Зарегистрируйте нового пользователя:
   
        deis register http://deis.[your domain]
   <p />
6. Добавьте hello SSH-ключ:
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. Создайте приложение:
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.Отправка git Hello активируют Docker изображения toobe построения и развертывания, который может занять несколько минут. Из Мои возможности в некоторых случаях шаг 10 (Pushing tooprivate репозитория образов) может зависнуть. В этом случае вы можете остановить процесс hello приложения hello удалить с помощью "deis приложений: уничтожить <application name> ` tooremove hello application and try again. You can use `deis apps:list" toofind hello имя приложения. Если все работает, вы увидите нечто похожее на следующее hello в конце hello выходные данные команды:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Проверьте, работает ли приложение hello.
   
        curl -S http://[your application name].[your domain]
   Вы должны увидеть следующее:
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Масштабирование экземпляров too3 приложения hello:
    
        deis scale cmd=3
    <p />
11. При необходимости можно использовать deis сведения подробности tooexamine приложения. Hello следующие выходные данные приведены из моей развертывания приложения.
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>Дальнейшие действия
В этой статье подробно описан все tooprovision действия hello Deis новый кластер в Azure с помощью шаблона диспетчера ресурсов Azure. шаблон Hello поддерживает избыточность подключений, а также балансировку нагрузки для развернутых приложений для работы с проектами. шаблон Hello также позволяет избежать с помощью общедоступных IP-адресов на узлы элементов, которые обеспечивает экономию ценное открытый IP и предоставляет более безопасной среде toohost приложений. toolearn более, см. следующие статьи hello.

[Общие сведения о диспетчере ресурсов Azure][resource-group-overview]  
[Как toouse hello Azure CLI][azure-command-line-tools]  
[Использование Azure PowerShell с Azure Resource Manager][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
