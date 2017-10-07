---
title: "aaaDjango веб-приложения на виртуальной Машине Windows Azure Server | Документы Microsoft"
description: "Узнайте, как toohost Django под управлением веб-сайта в Azure с помощью ВМ Windows Server 2012 R2 Datacenter с hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Веб-приложение Hello World на Django на виртуальной машине Windows Server

> [!IMPORTANT] 
> Azure имеет две модели развертывания для создания и работы с ресурсами: [диспетчера ресурсов Azure и hello классической модели развертывания](../../../resource-manager-deployment-model.md). В этой статье описываются hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания для использования модели hello диспетчера ресурсов.

В этом учебнике показано как toohost веб-сайт на основе Django в Windows Server в виртуальных машинах Azure. В учебнике hello предполагается нет предыдущего опыта работы с Azure. После завершения работы с учебником hello, может иметь приложении Django вверх и работающих в облаке hello.

Ниже перечислено, что вы можете узнать.

* Настройка виртуальной машины Azure toohost Django. Несмотря на то, что в этом учебнике описано как toodo для **Windows Server**, можно сделать hello же ВМ Linux, размещенных в Azure.
* Создайте новое приложение Django в Windows.

Hello учебнике рассказывается о том, как toobuild basic Hello World веб-приложения. приложение Hello размещается на виртуальной машине Azure.

Следующий снимок экрана приветствия показано приложение hello завершена:

![Окно обозревателя отображает hello hello world страницу в Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Создание и настройка виртуальной машины Azure toohost Django

1. . в разделе toocreate виртуальной машине Azure с hello распространения Windows Server 2012 R2 Datacenter [создать виртуальную машину под управлением Windows в hello портал Azure](tutorial.md).
2. Задать порт 80 Azure toodirect трафик из hello web tooport 80 на виртуальной машине hello:
   
   1. В hello портал Azure перейдите toohello панели мониторинга и выберите только что созданный виртуальный компьютер.
   2. Щелкните **Конечные точки**, а затем нажмите кнопку **Добавить**.

     ![Добавление конечной точки](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. На hello **добавить конечную точку** страницы, для **имя**, введите **HTTP**. Задать hello открытого и закрытого TCP-порты слишком**80**.

     ![Введите имя и задайте общедоступные и частные порты.](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. Нажмите кнопку **ОК**.
     
3. В панели мониторинга hello выберите виртуальную Машину. tooremotely входа удаленного рабочего стола (RDP) toouse toohello вновь созданные виртуальной машины Azure, щелкните **Connect**.  

> [!IMPORTANT] 
> Hello в соответствии с инструкциями предполагается, что вы вошли в toohello виртуальной машины правильно. Они также предполагается, что вы выдаете команды hello виртуальной машине, а не на локальном компьютере.

## <a id="setup"> </a>Установка Python, Django и WFastCGI
> [!NOTE]
> toodownload с помощью Internet Explorer, возможно, Internet Explorer tooconfigure **конфигурация усиленной безопасности** параметры. toodo, нажмите кнопку **запустить** > **Администрирование** > **диспетчера сервера** > **слокальногосервера**. Щелкните **Конфигурация усиленной безопасности Internet Explorer**, а затем выберите **Выкл.**

1. Установить последние версии Python 2.7 или 3.4 Python из hello [python.org][python.org].
2. Установите hello wfastcgi и django пакетов, использующих PIP-адрес.
   
    Python 2.7 при помощи hello следующую команду:
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Python 3.4 при помощи hello следующую команду:
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>Установка IIS с поддержкой FastCGI
* Установите службы IIS с поддержкой FastCGI. Это может занять несколько минут tooexecute.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Создание нового приложения Django
1. В C:\inetpub\wwwroot toocreate новый проект Django, введите следующую команду hello:
   
   Python 2.7 при помощи hello следующую команду:
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Python 3.4 при помощи hello следующую команду:
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Hello результат команды New-AzureService hello](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Hello `django-admin` команда создает базовую структуру для веб-сайтов на основе Django:
   
   * `helloworld\manage.py` поможет вам начать и остановить размещение веб-сайта на основе Django.
   * `helloworld\helloworld\settings.py` содержит настройки Django для приложения.
   * `helloworld\helloworld\urls.py`имеет кода hello сопоставления между каждого URL-адреса и его представление.
3. В каталоге C:\inetpub\wwwroot\helloworld\helloworld hello создайте новый файл с именем views.py. Этот файл имеет hello представление, которое отображает hello страницы «hello world». В редакторе кода введите следующие команды hello:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Замените содержимое файла urls.py hello hello hello, следующие команды:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>Настройка IIS
1. В hello глобального файла applicationhost.config Разблокируйте раздел обработчиков hello.  Это позволяет обработчик Python hello toouse файла web.config. Добавьте команду ниже:
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. Активируйте WFastCGI. Это добавляет приложения toohello глобального файла applicationhost.config, который ссылается tooyour интерпретатор исполняемый файл и hello wfastcgi.py сценарий Python.
   
    Для Python 2.7:
   
        C:\python27\scripts\wfastcgi-enable
   
    Для Python 3.4:
   
        C:\python34\scripts\wfastcgi-enable
3. Создайте файл web.config в каталоге C:\inetpub\wwwroot\helloworld. Здравствуйте, значение hello `scriptProcessor` атрибут должен соответствовать hello выходные данные предшествующей шаг hello. Дополнительные сведения о параметре wfastcgi hello см. в разделе [pypi wfastcgi][wfastcgi].
   
   Для Python 2.7:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   Для Python 3.4:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. Обновите расположение hello приветствия IIS по умолчанию веб-сайт toopoint toohello Django папки проекта:
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Загрузите hello веб-страницу в браузере.

![Окно обозревателя отображает hello hello world страницы в Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Завершение работы виртуальной машины Azure
После завершения работы с учебником, рекомендуется завершить работу или удаление виртуальной Машины Azure, созданную для учебника hello hello. Это позволит освободить ресурсы для работы с другими руководствами, а также избежать расходов за использование Azure.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
