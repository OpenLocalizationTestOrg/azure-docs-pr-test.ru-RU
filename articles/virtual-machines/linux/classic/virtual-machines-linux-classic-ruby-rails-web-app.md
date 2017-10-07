---
title: "aaaHost Ruby направляющие веб-сайта на виртуальной Машине Linux | Документы Microsoft"
description: "Настройка и размещение веб-сайта на основе Ruby on Rails в Azure с помощью виртуальной машины Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Веб-приложение Ruby on Rails на виртуальной машине Azure
В этом учебнике показано как toohost Ruby на веб-сайте направляющие на виртуальных машинах Linux.  

Данный учебник был проверен с использованием Ubuntu Server 14.04 LTS. Если вы используете другой дистрибутив Linux, может потребоваться toomodify hello шаги tooinstall направляющих.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.
>
>

## <a name="create-an-azure-vm"></a>Создание виртуальной машины Azure
Начните с создания виртуальной машины Azure с помощью образа Linux.

toocreate Здравствуйте виртуальной Машины, можно использовать портал Azure hello или hello Azure интерфейс командной строки (CLI).

### <a name="azure-portal"></a>Портал Azure
1. Вход в hello [портал Azure](https://portal.azure.com)
2. Нажмите кнопку **New**, введите «Ubuntu Server 14.04» в поле поиска hello. Щелкните запись hello, возвращенных hello поиска. Модель развертывания hello, выберите **классический**, затем нажмите кнопку «Создать».
3. В колонке основы hello, предоставить значения для hello необходимые поля: имя (для hello виртуальной Машины), имя пользователя, типа проверки подлинности и соответствующие учетные данные hello, подписки Azure, группу ресурсов и расположение.

   ![Создание нового образа Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. После подготовки виртуальной Машины hello, щелкните имя виртуальной Машины hello и нажмите кнопку **конечные точки** в hello **параметры** категории. Найти конечную точку SSH hello, перечисленных в разделе **автономный**.

   ![Конечная точка по умолчанию](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>Инфраструктура CLI Azure
Следуйте указаниям hello [создать виртуальную машину под управлением Linux][vm-instructions].

После подготовки виртуальной Машины hello конечную точку SSH hello можно получить, выполнив следующую команду hello:

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>Установка Ruby on Rails
1. С помощью SSH tooconnect toohello виртуальной Машины.
2. Из сеанса SSH hello используйте hello после команды tooinstall Ruby на hello виртуальной Машины:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    Hello установка может занять несколько минут. После завершения использования hello следующая команда tooverify установку Ruby:

        ruby -v

3. Используйте hello следующая команда Направляющие tooinstall:

        sudo gem install rails --no-rdoc --no-ri -V

    Используйте hello--нет rdoc и--флаги нет ri tooskip Установка документации hello, скорость которого выше.
    Эта команда будет скорее всего долго tooexecute, поэтому добавление hello -V будут отображаться сведения о ходе установки hello.

## <a name="create-and-run-an-app"></a>Создание и запуск приложения
Хотя по-прежнему вход через SSH, выполните следующие команды hello:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Hello [новый](http://guides.rubyonrails.org/command_line.html#rails-new) команда создает новое приложение направляющих. Hello [сервера](http://guides.rubyonrails.org/command_line.html#rails-server) команда запускает hello WEBrick веб-сервер, входящий в состав направляющих. (Для использования в рабочей среде может потребоваться toouse другого сервера, например единорога или пассажира.)

Вы увидите примерно toohello следующие выходные данные.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Добавление конечной точки
1. Go toohello [портал Azure] [https://portal.azure.com] и выберите виртуальную Машину.

2. Выберите **конечные ТОЧКИ** в hello **параметры** вдоль страницы приветствия hello левого края.

3. Нажмите кнопку **добавить** вверху hello страницы приветствия.

4. В hello **добавить конечную точку** диалогового окна введите hello следующую информацию:

   * **Имя**: HTTP.
   * **Протокол**: TCP
   * **Общий порт**: 80.
   * **Частный порт**: 3000.
   * **Плавающий IP-адрес**: отключен.
   * **Список управления доступом - порядок**: 1001 или другое значение, которое задает hello приоритет этого правила доступа.
   * **Список управления доступом — имя**: allowHTTP.
   * **Список управления доступом — действие**: разрешить.
   * **Список управления доступом — удаленная подсеть**: 1.0.0.0/16.

     Эта конечная точка имеет общий порт 80, которая будет направлять трафик toohello частный порт 3000, где сервер направляющие hello прослушивается. правила списка управления доступом Hello позволяет общего трафика через порт 80.

     ![Новая конечная точка](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Нажмите кнопку ОК toosave hello endpoint.

6. Должно появиться сообщение о **сохранении конечной точки виртуальной машины**. После этого сообщение исчезнет, конечная точка hello активен. Теперь может протестировать приложение, перейдя по toohello DNS-имя виртуальной машины. Hello веб-сайт должен выглядеть примерно toohello следующее:

    ![страница Rails по умолчанию][default-rails-cloud]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы сделали большинство hello действия вручную. В рабочей среде может создавать приложения на компьютере для разработки и развернуть ее toohello виртуальной Машине Azure. Кроме того большинство рабочих средах размещения приложения направляющие hello в сочетании с другим процессом сервера, например Apache или NginX, который обрабатывает запрос маршрутизации toomultiple экземпляров приложения hello направляющие и обслуживает статические ресурсы. Дополнительные сведения см. на странице http://rubyonrails.org/deploy/.

toolearn Дополнительные сведения о Ruby на направляющие, посетите hello [Ruby направляющие руководствах по][rails-guides].

toouse Ruby приложения службы Azure см. в разделе:

* [Хранение неструктурированных данных с использованием BLOB-объектов][blobs]
* [Хранение пар "ключ-значение" с помощью таблиц][tables]
* [Обработка содержимого высокой пропускной способностью с hello сеть доставки содержимого][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
