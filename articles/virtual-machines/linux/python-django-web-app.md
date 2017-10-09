---
title: "aaaPython веб-приложения с Django на виртуальной Машине Linux Azure | Документы Microsoft"
description: "Узнайте, как toohost на основе Django веб-приложения в Azure с помощью виртуальной Машины Linux."
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Веб-приложение Hello World на Django на виртуальной машине Linux
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

В этом учебнике показано как toohost веб-сайт на основе Django в Linux в виртуальных машинах Azure. В учебнике hello предполагается нет предыдущего опыта работы с Azure. После завершения работы с учебником hello, может иметь приложении Django вверх и работающих в облаке hello.

Ниже перечислено, что вы можете узнать.

* Настройка виртуальной машины Azure toohost Django. Несмотря на то, что в этом учебнике описано как toodo для **Linux**, можно сделать hello одинаково для ВМ Windows Server, размещенных в Azure. 
* Создайте приложение Django в Linux.

Hello учебнике рассказывается о том, как toobuild basic Hello World веб-приложения. приложение Hello размещается на виртуальной машине Azure.

Следующий снимок экрана приветствия показано приложение hello завершена:

![Окно браузера отображается страница Hello World hello в Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Создание и настройка виртуальной машины Azure toohost Django

1. виртуальной машине Azure с hello распространения Ubuntu Server 14.04 LTS toocreate см [Создание виртуальной машины Linux в hello портал Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Кроме того, можно выбрать проверку пароля вместо открытого ключа SSH.
2. tooedit hello сетевой безопасности группы tooallow входящих HTTP трафика tooport 80, в разделе [создавать группы безопасности сети в hello портал Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Необязательно.) По умолчанию у новой виртуальной машины нет полного доменного имени (FQDN).  toocreate ВМ с полным доменным ИМЕНЕМ в разделе [Создание полного доменного ИМЕНИ в hello портал Azure для виртуальной Машины Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Этот шаг не требуется для изучения этого руководства.

## <a id="setup"></a>Настроить среду разработки hello
> [!NOTE]
> Если нужна tooinstall Python ли toouse hello клиентские библиотеки, см. раздел hello [руководство по установке Python](../../python-how-to-install.md).

Hello виртуальной Машине Ubuntu Linux имеет предустановлен Python 2.7, но она не поставляется с Apache или Django. Выполните следующие шаги tooconnect tooyour ВМ hello и установите Apache и Django:

1. Откройте новое окно терминала.
2. tooconnect toohello ВМ Azure, введите следующую команду hello. Если не удалось создать полное доменное имя, можно подключиться с помощью hello общедоступный IP-адрес, отображаемый в виртуальной машине hello сводки в hello портал Azure.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, введите следующие команды hello:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache с остаток от деления wsgi, введите следующую команду hello:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Создание приложения Django
1. tooaccess SSH toouse виртуальная машина, hello откройте окно терминала, который использовался в предшествующих раздел hello.
2. toocreate новый проект Django, введите следующие команды hello:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Hello `django-admin.py` сценарий создает базовую структуру для веб-сайтов на основе Django:
   
   * `helloworld/manage.py` поможет вам начать и остановить размещение веб-сайта на основе Django.
   * `helloworld/helloworld/settings.py` содержит настройки Django для приложения.
   * `helloworld/helloworld/urls.py`имеет кода hello сопоставления между каждого URL-адреса и его представление.
3. В каталоге /var/www/helloworld/helloworld hello создайте новый файл с именем views.py. Этот файл имеет hello представление, которое отображает hello страницы «hello world». В редакторе кода введите следующие команды hello:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Замените содержимое файла urls.py hello hello hello, следующие команды:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Настройка Apache
1. В папке /etc/apache2/sites-available/helloworld.conf hello создайте файл конфигурации виртуальный узел Apache. Задайте следующие значения toohello содержимое hello. Замените *yourVmName* hello фактическое имя машины hello используется (например, *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. узел tooactivate hello hello используйте следующую команду:
   
       $ sudo a2ensite helloworld
3. toorestart Apache hello используйте следующую команду:
   
       $ sudo service apache2 reload
4. Загрузка hello веб-страницу в браузере.
   
   ![Окно обозревателя отображает hello hello world страницу в Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Завершение работы виртуальной машины Azure
После завершения работы с учебником, рекомендуется завершить работу или удаление виртуальной Машины Azure, созданную для учебника hello hello. Это позволит освободить ресурсы для работы с другими руководствами, а также избежать расходов за использование Azure.

