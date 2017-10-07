---
title: "aaaInstall MongoDB на виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Дополнительные сведения, способ создания tooinstall MongoDB на ВМ Azure с ОС Windows Server 2012 R2 с моделью развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Установка и настройка базы данных MongoDB на виртуальной машине Windows в Azure
[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом. В этой статье приведены инструкции по установке и настройке MongoDB на виртуальной машине Windows Server 2012 R2 в Azure. [MongoDB можно также установить на виртуальной машине Linux в Azure](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем установить и настроить MongoDB, toocreate виртуальной Машины и, в идеальном случае добавьте tooit диска данных. См. следующие статьи toocreate ВМ hello и добавьте диск данных.

* Создание виртуальной Машины Windows Server с помощью [hello портал Azure](quick-create-portal.md) или [Azure PowerShell](quick-create-powershell.md).
* Присоединение данных диска tooa виртуальной Машины Windows Server с помощью [hello портал Azure](attach-managed-disk-portal.md) или [Azure PowerShell](attach-disk-ps.md).

toobegin Установка и настройка MongoDB, [войти в систему виртуальной Машины Windows Server tooyour](connect-logon.md) с помощью удаленного рабочего стола.

## <a name="install-mongodb"></a>Установка MongoDB
> [!IMPORTANT]
> Функции безопасности MongoDB, такие как проверка подлинности и привязка IP-адреса, не включены по умолчанию. Средства безопасности должна быть включена перед развертыванием MongoDB tooa рабочей среде. Чтобы узнать больше, ознакомьтесь с [системой безопасности и аутентификацией MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).


1. После подключения tooyour виртуальную Машину с помощью удаленного рабочего стола, откройте Internet Explorer из hello **запустить** меню hello виртуальной Машины.
2. При первом запуске Internet Explorer выберите **Использовать рекомендуемые параметры безопасности, конфиденциальности и совместимости** и нажмите кнопку **ОК**.
3. Конфигурация усиленной безопасности Internet Explorer включена по умолчанию. Добавьте hello MongoDB веб-сайт toohello списка разрешенных сайтов:
   
   * Выберите hello **средства** значок в правом верхнем углу hello.
   * В **обозревателя**выберите hello **безопасности** , а затем выберите hello **надежных узлов** значок.
   * Нажмите кнопку hello **сайтов** кнопки. Добавить *https://\*. mongodb.org* toohello список надежных сайтов и затем закройте окно hello-диалоговое окно.
     
     ![Настройка параметров безопасности Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. Обзор toohello [загружает MongoDB -](http://www.mongodb.org/downloads) страницы (http://www.mongodb.org/downloads).
5. При необходимости выберите hello **сервер сообщества** выпуска и hello, а затем выберите последний текущей стабильной выпуск для Windows Server 2008 R2 64-разрядных систем и более поздних версий. toodownload Здравствуйте установщика, нажмите кнопку **загрузки (msi)**.
   
    ![Скачивание установщика MongoDB](./media/install-mongodb/download-mongodb.png)
   
    Запустите установщик hello, после завершения загрузки hello.
6. Прочтите и примите лицензионное соглашение hello. Когда появится запрос, выберите **Complete** (Завершить).
7. На последнем экране приветствия, нажмите кнопку **установить**.

## <a name="configure-hello-vm-and-mongodb"></a>Настройка виртуальной Машины hello и MongoDB
1. переменные пути Hello не обновляются с помощью установщика MongoDB hello. Без hello MongoDB `bin` расположения в переменной путь требуется полный путь hello toospecify каждый раз при использовании исполняемый объект MongoDB. переменная path tooyour расположение hello tooadd:
   
   * Щелкните правой кнопкой мыши hello **запустить** и выбрать пункт **системы**.
   * Выберите **Дополнительные параметры системы**, а затем щелкните **Переменные среды**.
   * В разделе **Системные переменные** выберите **Путь** и нажмите кнопку **Изменить**.
     
     ![Настройка переменных PATH](./media/install-mongodb/configure-path-variables.png)
     
     Добавить путь hello tooyour MongoDB `bin` папки. Приложение MongoDB обычно устанавливается в папку *C:\Program Files\MongoDB*. Проверьте путь установки hello на ВМ. Hello следующий пример добавляет hello по умолчанию MongoDB установки расположение toohello `PATH` переменной:
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Быть убедиться, что tooadd hello начальные точки с запятой (`;`) tooindicate, что вы добавляете tooyour расположение `PATH` переменной.

2. Создайте каталоги данных и журналов MongoDB на диске данных. Из hello **запустить** последовательно выберите пункты **командной строки**. Следующие примеры Hello создать hello каталоги на диске «f:»
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Запуск экземпляра MongoDB с hello следующую команду, настройки hello путь tooyour данных и журналов каталоги соответствующим образом:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Он может занять несколько минут для MongoDB tooallocate hello файлов журнала и начать ожидать соединения. Все сообщения журнала, направленной toohello *F:\MongoLogs\mongolog.log* файл с именем `mongod.exe` server запущен и выделяет файлы журнала.
   
   > [!NOTE]
   > командную строку Hello остается ориентированы на эту задачу во время выполнения экземпляра MongoDB. Оставьте hello командной строки окна откройте toocontinue под управлением MongoDB. Кроме того, можно установить MongoDB как служба, как описано в следующем шаге hello.

4. Для более надежной работы MongoDB, установить hello `mongod.exe` как служба. Создание службы означает, что не требуется tooleave командной строки необходимо toouse MongoDB каждый раз. Создайте hello службы следующим образом, Настройка hello путь tooyour каталоги данных и журнала соответственно:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Hello предыдущая команда создает службу с именем MongoDB, с описанием «Mongo DB». также указываются Hello следующие параметры:
   
   * Hello `--dbpath` указывает расположение hello hello данных каталога.
   * Hello `--logpath` должен указываться используется toospecify файла журнала, поскольку работающую службу hello не имеет toodisplay вывода окна команд.
   * Hello `--logappend` параметр указывает на то, что перезапуск службы hello вызывает tooappend toohello существующего файла журнала.
   
   hello MongoDB toostart службе, выполните следующую команду hello:
   
    ```
    net start MongoDB
    ```
   
    Дополнительные сведения о создании службы MongoDB hello см. в разделе [Настройка службы Windows для MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Экземпляр MongoDB hello теста
Теперь, когда компонент MongoDB выполняется как один экземпляр или установлен в качестве службы, можно приступить к созданию и использованию баз данных. hello toostart MongoDB административной оболочки, открыть другое окно командной строки от hello **запустить** меню и введите следующую команду hello:

```
mongo  
```

Можно получить список баз данных hello с hello `db` команды. Вставьте некоторые данные следующим образом.

```
db.foo.insert( { a : 1 } )
```

Выполните поиск данных следующим образом.

```
db.foo.find()
```

Hello вывода будет примерно toohello следующий пример:

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Выход hello `mongo` консоли следующим образом:

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Настройка брандмауэра и правил группы безопасности сети
Теперь, когда MongoDB установлены и запущены, откройте порт в брандмауэре Windows, чтобы удаленно подключиться tooMongoDB. toocreate новое правило для входящего трафика tooallow TCP-порт 27017, откройте командной строке PowerShell с правами администратора и введите hello следующую команду:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

Можно также создать правило hello с помощью hello **брандмауэр Windows в режиме повышенной безопасности** графическое средство управления. Создайте новое правило для входящего трафика tooallow TCP-порт 27017.

При необходимости создайте группы безопасности сети правило tooallow доступа tooMongoDB из вне hello существующей подсети виртуальной сети Azure. Hello можно создать правила группы безопасности сети с помощью hello [портал Azure](nsg-quickstart-portal.md) или [Azure PowerShell](nsg-quickstart-powershell.md). С помощью правил брандмауэра Windows hello, разрешить TCP toohello 27017 порта виртуального сетевого интерфейса виртуальной Машины MongoDB.

> [!NOTE]
> TCP-порт 27017 — hello по умолчанию порт MongoDB. Этот порт можно изменить с помощью hello `--port` параметра при запуске `mongod.exe` вручную или из службы. Если вы измените порт hello, делает убедиться, что tooupdate hello брандмауэра Windows и группы безопасности сети правила в предыдущих шагах hello.


## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, как tooinstall и настройте MongoDB на виртуальной Машине Windows. Теперь вы можете просматривать MongoDB на виртуальной Машине Windows, по следующие дополнительные разделы в hello hello [документацию MongoDB](https://docs.mongodb.com/manual/).

