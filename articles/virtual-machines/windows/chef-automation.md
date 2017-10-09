---
title: "развертывание виртуальной машины aaaAzure с Chef | Документы Microsoft"
description: "Узнайте, как toouse Chef toodo автоматизировать развертывание виртуальной машины и конфигурации в Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Автоматизация развертывания виртуальной машины Azure с помощью Chef
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef — это отличное средство для автоматизации и для настройки требуемого состояния.

Наш последний выпуск api облака Chef обеспечивает прозрачную интеграцию с Azure, предоставляя возможность tooprovision hello и развертывание состояния конфигурации одной командой.

В этой статье я покажу как tooset копирование вашей tooprovision среды Chef Azure виртуальных машин и пошаговыми руководствами по созданию политики или «Рецепты», а затем развернуть этот сборник рецептов tooan виртуальной машины Azure.

Итак, начнем!

## <a name="chef-basics"></a>Основы использования Chef
Прежде чем начать, я рекомендую просмотрите основные понятия hello Chef. <a href="http://www.chef.io/chef" target="_blank">Вот</a> великолепный материал. Я рекомендую быстро ознакомиться с ним, прежде чем начать работу с данным пошаговым руководством. Однако я будет повторим основы hello, прежде чем приступить к работе.

Следующая схема Hello показана высокоуровневая архитектура Chef hello.

![][2]

Chef имеет три основных компонента архитектуры: сервер Chef, клиент (узел) Chef и рабочая станция Chef.

Hello сервера Chef является нашей точкой управления и есть два варианта для hello сервера Chef: ведущее решение или локальным решением. Мы будем использовать размещенное решение.

Клиент Hello Chef (узел) — hello агент, который располагается на серверах hello, которыми вы управляете.

Hello рабочая станция Chef является нашей администраторские рабочие станции, где создать нашей политики и выполнять нашей команды управления. Запустим hello **knife** команду hello рабочей станции Chef toomanage инфраструктуры.

Имеется также hello понятие «Кулинарные книги» и «Рецепты». Это эффективно политики hello мы определить и применить tooour серверов.

## <a name="preparing-hello-workstation"></a>Подготовка рабочей станции hello
Во-первых позволяет рабочей станции с подготовки hello. В данном случае используется стандартная рабочая станция Windows. Мы должны toocreate directory toostore наших файлов конфигурации и справочники.

Сначала создайте каталог с именем C:\chef.

Затем создайте каталог C:\chef\cookbooks.

Теперь нужно toodownload наш файл настроек Azure чтобы Chef можно взаимодействовать с нашей подписке Azure.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
Загрузите вашей hello PowerShell Azure с помощью параметров публикации [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) команды. 

Сохраните hello файл параметров публикации в C:\chef.

## <a name="creating-a-managed-chef-account"></a>Создание управляемой учетной записи Chef
Зарегистрируйте размещенную учетную запись Chef [здесь](https://manage.chef.io/signup).

Во время процесса регистрации hello, появится запрос toocreate новой организации.

![][3]

После создания вашей организации, загрузите начальный набор hello.

![][4]

> [!NOTE]
> Если появится предупреждение, что ключи будут сброшены, это будет ОК tooproceed, поскольку у нас есть без существующей инфраструктуры, как еще не настроены.
> 
> 

Этот ZIP-файл начального набора содержит ключи и файлы конфигурации вашей организации.

## <a name="configuring-hello-chef-workstation"></a>Настройка рабочей станции Chef hello
Извлеките содержимое hello tooC:\chef chef starter.zip hello.

Скопируйте все файлы в starter\chef-chef-repo\.chef tooyour c:\chef каталога.

Каталог должен выглядеть примерно следующий пример hello.

![][5]

Должны появиться четыре файлы, включая hello Azure файла публикации в корне c:\chef hello.

PEM-файлы Hello содержаться вашей организации и закрытый ключи администратора для обмена данными, а файл knife.rb hello содержит конфигурацию инструментом. Нам понадобится файл knife.rb tooedit hello.

Откройте файл hello в редакторе по выбору и изменить cookbook_path «hello», удалив hello /... из пути hello выводится так, как показано далее.

    cookbook_path  ["#{current_dir}/cookbooks"]

Также добавьте hello следующей строке, отражающей имя hello Azure файл параметров публикации.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

Файл knife.rb должен выглядеть примерно toohello следующий пример.

![][6]

Эти строки будут убедитесь, что Knife ссылается на каталог справочники hello в c:\chef\cookbooks и также использует наш файл настроек публикации Azure во время операций Azure.

## <a name="installing-hello-chef-development-kit"></a>Установка пакета средств разработки Chef hello
Далее [загрузить и установить](http://downloads.getchef.com/chef-dk/windows) hello tooset ChefDK (Chef Development Kit) вверх рабочей станции Chef.

![][7]

Установите в расположение по умолчанию hello c:\opscode. Эта установка займет около 10 минут.

Убедитесь, что переменная PATH содержит записи для путей C:\opscode\chefdk\bin, C:\opscode\chefdk\embedded\bin и C:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin.

Если они отсутствуют, обязательно добавьте эти пути!

*Примечание hello ЗАКАЗА из hello путь — важно!* Если ваш opscode пути не в правильном порядке hello связаны проблемы.

Прежде чем продолжить, перезагрузите рабочую станцию.

После этого будет установлен модуль Knife для Azure hello. Это предоставляет Knife hello «Подключаемый модуль Azure».

Выполните следующую команду hello.

    chef gem install knife-azure ––pre

> [!NOTE]
> Аргумент – pre Hello гарантирует, что вы получили hello последнюю версию-КАНДИДАТ hello подключаемый модуль Azure инструментом, который предоставляет доступ toohello последний набор API-интерфейсов.
> 
> 

Вполне вероятно, что число зависимостей, также будут установлены в hello то же время.

![][8]

tooensure — все компоненты настроены неправильно, выполнения hello следующую команду.

    knife azure image list

Если все настроено правильно, появится прокручиваемый список доступных образов Azure.

Поздравляем! Настройка рабочей станции Hello!

## <a name="creating-a-cookbook"></a>Создание подробной инструкции
Рецепты используется Chef toodefine набор команд, которые нужно tooexecute на управляемый клиент. Создание кулинарной книги довольно просто, и мы используем hello **chef создания рецепты** команды toogenerate нашей рецепты шаблона. Мы назовем свою подробную инструкцию именем webserver, так как нам нужна политика, которая автоматически развертывает службы IIS.

В каталоге C:\Chef выполните следующую команду hello.

    chef generate cookbook webserver

Будет создан набор файлов в каталоге C:\Chef\cookbooks\webserver hello. Теперь мы должны toodefine hello набор команд, что мы предлагаем наши tooexecute клиент Chef на нашем управляемую виртуальную машину.

Hello команды сохраняются в файле default.rb hello. В этом файле я будет определяться набор команд, установка служб IIS, запускающий IIS и копирует папку wwwroot toohello файла шаблона.

Измените файл C:\chef\cookbooks\webserver\recipes\default.rb hello и добавьте следующие строки hello.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

Сохраните файл hello, после завершения работы.

## <a name="creating-a-template"></a>Создание шаблона
Как упоминалось ранее, мы должны toogenerate файл шаблона, который будет использоваться в качестве нашу страницу default.html.

Запустите следующий шаблон hello toogenerate команды hello.

    chef generate template webserver Default.htm

Теперь перейдите toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb файл. Измените файл hello, добавление простого кода HTML «Hello World», а затем сохраните файл hello.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Отправка toohello рецепты hello сервера Chef
На этом шаге мы создавая копию hello рецепты, созданную на локальном компьютере и передачи их toohello размещенного сервера Chef. После отправки hello рецепты будут отображаться в узле hello **политики** вкладки.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Развертывание виртуальной машины с помощью Knife Azure
Мы развертывание виртуальной машины Azure и применить hello «Веб-сервер» рецепты, который будет установлен в нашей IIS web service и по умолчанию веб-страницы.

В заказ toodo это, используйте hello **knife azure server создать** команды.

Уверен, что пример hello команды появится рядом.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

Hello параметров говорят сами за себя. Подставьте свои переменные и запустите команду.

> [!NOTE]
> Через командную строку hello hello я также автоматизация правила фильтра конечной точки сети с помощью параметра hello конечные точки — tcp. Открыли порты 80 и 3389 tooprovide доступа toomy веб-страницы и сеансу удаленного рабочего СТОЛА.
> 
> 

После выполнения команды hello перехода toohello Azure портал, чтобы просмотреть начать tooprovision компьютере.

![][13]

Далее появится Hello Командная строка.

![][10]

После завершения развертывания hello, мы должен быть веб-службы может tooconnect toohello через порт 80, как мы открыт порт hello, когда мы провизионировали hello виртуальную машину с hello команд Knife для Azure. Как эта виртуальная машина hello только виртуальной машины в облачной службе, он будет подключен с URL-адрес hello облачной службы.

![][11]

Здесь вы могли наблюдать пример творческого подхода к написанию кода.

Не забывайте, что можно также подключиться через сеанс RDP с портала Azure через порт 3389 hello.

Надеюсь, что эта информация была для вас полезной! Начинайте использовать подход "инфраструктура как код" прямо сейчас с помощью Azure!

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
