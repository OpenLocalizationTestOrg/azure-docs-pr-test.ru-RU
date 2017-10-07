---
title: "aaaDeploy tooLinux приложений Node.js виртуальных машин в Azure"
description: "Узнайте, как toodeploy Node.js приложения tooLinux виртуальных машин в Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Развертывание tooLinux приложений Node.js виртуальных машин в Azure
В этом учебнике показано как tootake приложений Node.js и разверните его tooLinux виртуальные машины в Azure. Hello инструкциям этого учебника можно выполнять в любой операционной системе, поддерживающий работу Node.js.

Вы узнаете, как:

* разветвлять и клонировать репозиторий GitHub с простым приложением TODO;
* Создать и настроить две виртуальные машины Linux в Azure toorun hello приложения;
* Завершить цикл hello приложения с помощью принудительной отправки обновлений toohello web переднего плана для виртуальной машины.

> [!NOTE]
> toocomplete этого учебника требуется учетная запись GitHub и учетной записи Microsoft Azure и hello возможности toouse Git с компьютера разработки.
> 
> Если у вас нет учетной записи GitHub, вы можете зарегистрироваться [здесь](https://github.com/join).
> 
> Если у вас нет учетной записи [Microsoft Azure](https://azure.microsoft.com/), вы можете зарегистрироваться [здесь](https://azure.microsoft.com/pricing/free-trial/) и получить бесплатную ознакомительную версию. Это также поможет процедуры для регистрации hello [учетную запись Майкрософт](http://account.microsoft.com) Если вы не сделали этого. Кроме того, если вы являетесь подписчиком Visual Studio, вы можете [активировать свои преимущества MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Если на компьютере разработки не установлен Git и если вы используете компьютер Macintosh или Windows, установите Git с [этого ресурса](http://www.git-scm.com). При использовании Linux Установка git с помощью механизма hello, наиболее подходящий для вас, например `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>Разветвление и клонирование hello приложения TODO
Hello приложение TODO, используется в этом учебнике реализует простой веб-клиента через экземпляр MongoDB, который отслеживает TODO list. После входа в tooGitHub go [здесь](https://github.com/stepro/node-todo) toofind hello приложения и его с помощью ссылки hello в правом верхнем углу hello ветвления. Так вы создадите в своей учетной записи репозиторий с именем *имя_учетной_записи*/node-todo.

Теперь клонируйте этот репозиторий на компьютере разработки.

    git clone https://github.com/accountname/node-todo.git

Мы будем использовать этот локальный клон репозитория hello немного позже при внесении изменений в исходный код toohello.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>Создание и настройка виртуальных машин Linux hello
Azure имеет хорошую поддержку вычислений с использованием виртуальных машин Linux. Эта часть hello учебника показано, как можно легко запустить две виртуальные машины Linux и развертывать toothem приложения hello TODO, выполнение веб-клиентом hello на одном и hello MongoDB экземпляра на другой hello.

### <a name="creating-virtual-machines"></a>Создание виртуальных машин
Hello простым способом toocreate новую виртуальную машину в Azure — toouse hello портала Azure. Нажмите кнопку [здесь](https://portal.azure.com) toosign в и запустите hello портала Azure в веб-браузере. Сразу после загрузки hello портал Azure, выполните следующие шаги hello.

* Нажмите кнопку hello «+ создать» связи;
* Выберите категории «Вычисления» hello и выберите «Ubuntu Server 14.04 LTS»;
* Выберите модель развертывания «диспетчер ресурсов» hello и нажмите кнопку «Создать»;
* Заполните основы hello следующие рекомендации:
  * Укажите имя, которое позже сможете легко узнать.
  * В целях этого руководства выберите проверку подлинности с использованием пароля.
  * Создайте новую группу ресурсов с узнаваемым именем.
* Для hello размер виртуальной машины «Standard A1» является неплохим выбором для этого учебника.
* Для дополнительных параметров убедитесь, что тип диска hello «Standard» и принять Здравствуйте, все остальные значения по умолчанию.
* Начнем с создания приветствия на странице сводки hello.

Выполнить hello выше обработки дважды toocreate двух виртуальных машин Linux: для веб-клиентом hello и для экземпляра MongoDB hello. Создание виртуальных машин hello займет около 5 – 10 минут.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Назначение DNS-записи для виртуальных машин
Виртуальные машины, созданные в Azure, по умолчанию доступны только по общедоступному IP-адресу, например 1.2.3.4. Сделаем hello машины более понятными, назначив их DNS-записей.

После портала hello указывает, что hello виртуальных машин были созданы, щелкните ссылку «Виртуальные машины» hello в панель переходов слева hello и найдите компьютеры. Для каждой виртуальной машины:

* Найдите вкладку hello Essentials и щелкните hello общедоступный IP-адрес;
* В hello открытый IP-адрес назначьте метка DNS-имени и сохраните.

Hello портала будет убедитесь, что заданные hello имя доступно. После сохранения конфигурации hello, виртуальные машины будут иметь имена узлов аналогичные слишком`machinename.region.cloudapp.azure.com`.

### <a name="connecting-toohello-virtual-machines"></a>Подключение toohello виртуальные машины
Если виртуальные машины были подготовлены, они были предварительно настроенных tooallow удаленные подключения через SSH. Это механизм hello, мы будем использовать tooconfigure hello виртуальных машин. Если вы используете Windows для разработки, если вы не сделали этого потребуется tooget клиент SSH. Типичным вариантом является PuTTY, который можно загрузить с [этого ресурса](http://www.chiark.greenend.org.uk/~sgtatham/putty/). В операционных системах Linux и Macintosh уже есть встроенный клиент SSH.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Настройка hello виртуальная машина Web переднего плана
SSH toohello web внешнего интерфейса компьютера, созданного с помощью PuTTY, ssh командной строки или другие избранный инструмент SSH. Отобразится приветствие и командная строка.

Сначала убедитесь, что Git и узел установлены.

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Так как веб-приложения hello клиентом использует некоторые собственные модули Node.js, мы также должны tooinstall hello необходимый набор средств построения.

    sudo apt-get install -y build-essential

Наконец, давайте установить приложение Node.js вызывается *навсегда*, которые помогают toorun Node.js серверные приложения:

    sudo npm install -g forever

Это все зависимости hello, необходимые на виртуальной машине toobe может toorun hello для этого приложения веб-клиентом, так что давайте работы. toodo это, мы сначала создается исходного состояния системы клона репозитория GitHub hello ранее разделенными, можно легко опубликовать обновления toohello виртуальной машины (мы рассмотрим этот сценарий обновления более поздней версии) и затем клонировать tooprovide исходного состояния системы клон hello версии hello репозиторий, который фактически может выполняться.

Начиная с hello домашнем каталоге (~), запустите hello, следующие команды (заменяя *accountname* с вашим именем учетной записи пользователя GitHub):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Теперь введите каталог узла todo hello и выполните следующие команды:

    npm install
    forever start server.js

Hello приложения веб-клиентом теперь работает, однако есть одно действие hello приложения для доступа к веб-браузере. Hello виртуальную машину, созданную защищен ресурс Azure, которая называется *сетевой группы безопасности*, который был создан для вас при подготовке hello виртуальной машины. В настоящее время этот ресурс позволяет только внешние запросы tooport 22 toobe направлено toohello виртуальной машины, которое поддерживает связь SSH с машины hello, но ничего более. Поэтому в порядке tooview hello приложения TODO, которое служит toorun настроенный порт 8080, этот порт также должен toobe открыт.

Получите toohello портала Azure и выполните следующие шаги hello.

* Щелкните «Группы ресурсов» в левой hello панель переходов;
* Выберите группу ресурсов hello, содержащий виртуальный компьютер;
* В hello полученный список ресурсов выберите группы безопасности сети hello (hello один щита на);
* В свойствах hello выберите «правила безопасности для входящего трафика»;
* В панели инструментов hello нажмите кнопку «Добавить»;
* Укажите имя, например default-allow-todo.
* Задать протокол hello слишком «TCP»;
* Задайте диапазон портов назначения hello слишком «8080»;
* Нажмите кнопку ОК и дождитесь hello безопасности правило toobe создан.

После создания этого правила безопасности, hello приложения TODO общедоступен на hello Интернета и просмотром tooit, например с помощью URL-адреса, например:

    http://machinename.region.cloudapp.azure.com:8080

Можно заметить, несмотря на то, что мы еще не настроен hello MongoDB виртуальной машины, hello приложения TODO отображается toobe довольно работы. Это, поскольку исходный репозиторий hello жестко toouse предварительно развернутого экземпляра MongoDB. После настройки hello MongoDB виртуальной машины будет вернуться назад и изменить hello исходного кода tooutilize закрытого экземпляра MongoDB.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Настройка hello MongoDB виртуальной машины
SSH toohello второй компьютер, созданного с помощью PuTTY, ssh командной строки или другие избранный инструмент SSH. После просмотра приветственное сообщение hello и из командной строки, установите MongoDB (эти инструкции были взяты из [здесь](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

Стандартные настройки MongoDB предусматривают только локальный доступ. В этом учебнике мы настраиваем MongoDB, доступных из приложения hello виртуальной машины. В контексте sudo, откройте файл /etc/mongod.conf hello и найдите hello `# network interfaces` раздела. Изменение hello `net.bindIp` конфигурации значение слишком`0.0.0.0`.

> [!NOTE]
> Эта конфигурация предназначена для целей hello только для этого учебника. Из соображений безопасности мы **НЕ** рекомендуем использовать этот прием в производственной среде.
> 
> 

Теперь убедитесь hello MongoDB служба была запущена.

    sudo service mongod restart

По умолчанию MongoDB работает через порт 27017. Поэтому в hello таким же образом, что нам нужен tooopen порт 8080 на виртуальной машине hello web переднего плана необходимо порт tooopen 27017 на виртуальной машине hello MongoDB.

Получите toohello портала Azure и выполните следующие шаги hello.

* Щелкните «Группы ресурсов» в левой hello панель переходов;
* Выберите группу ресурсов hello, содержащий hello MongoDB виртуальной машины;
* В hello полученный список ресурсов выберите группы безопасности сети hello (hello один щита на) с hello точно такое же имя, присвоенное toohello MongoDB виртуальной машины;
* В свойствах hello выберите «правила безопасности для входящего трафика»;
* В панели инструментов hello нажмите кнопку «Добавить»;
* Укажите имя, например default-allow-mongo.
* Задать протокол hello слишком «TCP»;
* Задайте диапазон портов назначения hello слишком «27017»;
* Нажмите кнопку ОК и дождитесь hello безопасности правило toobe создан.

## <a name="iterating-on-hello-todo-application"></a>Итерации по hello приложения TODO
Итак, мы подготовили две виртуальные машины Linux:, выполняется приложение hello веб-клиентом и один, на котором запущен экземпляр MongoDB. Ошибка, но — веб-клиентом hello не использует фактически hello подготовить экземпляр MongoDB еще. Исправим это путем обновления интерфейсных кода hello web toouse переменной среды, вместо жестко экземпляра.

### <a name="changing-hello-todo-application"></a>Изменение приложения TODO hello
На компьютере разработки, где сначала клонировать репозиторий hello todo узел, откройте hello `node-todo/config/database.js` файл в любом редакторе и измените значение hello URL-адреса с hello жестко запрограммированных значений, таких как `mongodb://...` слишком`process.env.MONGODB`.

Фиксация изменений и отправить образец toohello GitHub:

    git commit -am "Get MongoDB instance from env"
    git push origin master

К сожалению это не опубликует hello изменение toohello web переднего плана для виртуальной машины. Сделаем несколько дополнительных tooenable изменения виртуальной машины toothat простой, но эффективный механизм для публикации обновлений, позволяющий быстро просматривать hello влияния изменений hello в реальной среде hello.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Настройка hello виртуальная машина Web переднего плана
Помните, что мы созданного ранее исходного состояния системы клона репозитория hello todo узла на виртуальная машина hello web переднего плана. Оказывается, что это действие создан новый Git удаленного toowhich изменения могут передаваться. Тем не менее просто помещает toothis удаленного совсем не дает модель быстрой итерации hello, ищете разработчики при работе в своем коде.

Что мы хотели бы могли toodo toobe убедитесь, что в случае принудительной toohello удаленный репозиторий на виртуальной машине hello hello запущенное приложение TODO автоматически обновлена. К счастью это легко tooachieve с git.

Git предоставляет ряд обработчиками, которые вызываются в tooactions tooreact определенные промежутки времени, затраченное на репозиторий hello. Они указываются с помощью сценариев оболочки в репозитории hello `hooks` папки. Hello обработчик, который лучше всего подходит для hello сценария автоматическое обновление — hello `post-update` событий.

В SSH сеанса toohello web переднего плана виртуальной машины, измените toohello `~/node-todo.git/hooks` каталога и добавьте следующие содержимого tooa файл с именем hello `post-update` (заменив `machinename` и `region` с указанием данных MongoDB виртуальной машины):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Убедитесь, что этот файл является исполняемым, выполнив следующую команду hello.

    chmod 755 post-update

Этот сценарий обеспечивает остановки текущего сервера приложения hello, кода hello в клонированного репозитория hello обновленные toohello последняя версия, все обновленные зависимостям, и перезапуска сервера hello. Это также гарантирует, что в этой среде hello был настроен в процессе подготовки для получения первого наш экземпляр MongoDB tooget обновления приложения hello из переменной среды.

### <a name="configuring-your-development-machine"></a>Настройка компьютера разработки
Теперь давайте компьютере подключается виртуальная машина toohello web переднего плана. Это простым добавлением на виртуальной машине hello, что и удаленный репозиторий исходного состояния системы hello. Выполните следующие команды toodo hello это (заменив *пользователя* с вашим именем входа виртуальной машины интерфейсных веб и *machinename* и *область* соответствующим образом):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

Это все, что необходимые tooenable принудительной отправки, фактически публикации, или изменяет виртуальная машина toohello web переднего плана.

### <a name="publishing-updates"></a>Публикация обновлений
Давайте публикация hello одно из изменений, сделанных к текущему моменту, чтобы приложение hello используется собственный экземпляр MongoDB.

    git push azure master

Вы увидите примерно toothis выходные данные:

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

После выполнения этой команды, попробуйте обновить приложение hello в веб-браузере. Должно быть toosee возможности, представленные здесь список TODO hello пуст и больше не равноценных toohello общего развертывания MongoDB экземпляра.

Учебник hello toocomplete, давайте сделать другой, более видимым. На компьютере разработки откройте файл node-todo/public/index.html hello, используя текстовый редактор. Найдите заголовок jumbotron hello и измените заголовок hello из «Я Todo-aholic» слишком «я Todo-aholic в Azure!».

Зафиксируем это изменение.

    git commit -am "Azurify hello title"

Это время, давайте публикации tooAzure изменение hello до отправки его в репозитории GitHub toohello tooback:

    git push azure master

После выполнения этой команды обновления hello веб-страницу, чтобы просмотреть изменения hello. Так как они выглядят правильно, push удаленный источник назад toohello hello изменений: 

    git push origin master

## <a name="next-steps"></a>Дальнейшие действия
В этой статье показано, как tootake приложений Node.js и разверните его tooLinux виртуальные машины в Azure. toolearn Дополнительные сведения о виртуальных машин Linux в Azure, в разделе [tooLinux введение в Azure](/documentation/articles/virtual-machines-linux-introduction/).

Дополнительные сведения о том, как toodevelop приложений Node.js в Azure, в разделе hello [Центр разработчика Node.js](/develop/nodejs/).

