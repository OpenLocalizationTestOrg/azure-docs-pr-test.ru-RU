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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="00392-103">Веб-приложение Hello World на Django на виртуальной машине Windows Server</span><span class="sxs-lookup"><span data-stu-id="00392-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="00392-104">Azure имеет две модели развертывания для создания и работы с ресурсами: [диспетчера ресурсов Azure и hello классической модели развертывания](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="00392-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="00392-105">В этой статье описываются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="00392-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="00392-106">Корпорация Майкрософт рекомендует наиболее новые развертывания для использования модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="00392-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="00392-107">В этом учебнике показано как toohost веб-сайт на основе Django в Windows Server в виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="00392-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="00392-108">В учебнике hello предполагается нет предыдущего опыта работы с Azure.</span><span class="sxs-lookup"><span data-stu-id="00392-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="00392-109">После завершения работы с учебником hello, может иметь приложении Django вверх и работающих в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="00392-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="00392-110">Ниже перечислено, что вы можете узнать.</span><span class="sxs-lookup"><span data-stu-id="00392-110">Learn how to:</span></span>

* <span data-ttu-id="00392-111">Настройка виртуальной машины Azure toohost Django.</span><span class="sxs-lookup"><span data-stu-id="00392-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="00392-112">Несмотря на то, что в этом учебнике описано как toodo для **Windows Server**, можно сделать hello же ВМ Linux, размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="00392-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="00392-113">Создайте новое приложение Django в Windows.</span><span class="sxs-lookup"><span data-stu-id="00392-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="00392-114">Hello учебнике рассказывается о том, как toobuild basic Hello World веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="00392-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="00392-115">приложение Hello размещается на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="00392-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="00392-116">Следующий снимок экрана приветствия показано приложение hello завершена:</span><span class="sxs-lookup"><span data-stu-id="00392-116">hello following screenshot shows hello completed application:</span></span>

![Окно обозревателя отображает hello hello world страницу в Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="00392-118">Создание и настройка виртуальной машины Azure toohost Django</span><span class="sxs-lookup"><span data-stu-id="00392-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="00392-119">. в разделе toocreate виртуальной машине Azure с hello распространения Windows Server 2012 R2 Datacenter [создать виртуальную машину под управлением Windows в hello портал Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="00392-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="00392-120">Задать порт 80 Azure toodirect трафик из hello web tooport 80 на виртуальной машине hello:</span><span class="sxs-lookup"><span data-stu-id="00392-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="00392-121">В hello портал Azure перейдите toohello панели мониторинга и выберите только что созданный виртуальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="00392-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="00392-122">Щелкните **Конечные точки**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00392-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Добавление конечной точки](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="00392-124">На hello **добавить конечную точку** страницы, для **имя**, введите **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="00392-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="00392-125">Задать hello открытого и закрытого TCP-порты слишком**80**.</span><span class="sxs-lookup"><span data-stu-id="00392-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Введите имя и задайте общедоступные и частные порты.](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="00392-127">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="00392-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="00392-128">В панели мониторинга hello выберите виртуальную Машину.</span><span class="sxs-lookup"><span data-stu-id="00392-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="00392-129">tooremotely входа удаленного рабочего стола (RDP) toouse toohello вновь созданные виртуальной машины Azure, щелкните **Connect**.</span><span class="sxs-lookup"><span data-stu-id="00392-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="00392-130">Hello в соответствии с инструкциями предполагается, что вы вошли в toohello виртуальной машины правильно.</span><span class="sxs-lookup"><span data-stu-id="00392-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="00392-131">Они также предполагается, что вы выдаете команды hello виртуальной машине, а не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="00392-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="00392-132"><a id="setup"> </a>Установка Python, Django и WFastCGI</span><span class="sxs-lookup"><span data-stu-id="00392-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="00392-133">toodownload с помощью Internet Explorer, возможно, Internet Explorer tooconfigure **конфигурация усиленной безопасности** параметры.</span><span class="sxs-lookup"><span data-stu-id="00392-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="00392-134">toodo, нажмите кнопку **запустить** > **Администрирование** > **диспетчера сервера** > **слокальногосервера**.</span><span class="sxs-lookup"><span data-stu-id="00392-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="00392-135">Щелкните **Конфигурация усиленной безопасности Internet Explorer**, а затем выберите **Выкл.**</span><span class="sxs-lookup"><span data-stu-id="00392-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="00392-136">Установить последние версии Python 2.7 или 3.4 Python из hello [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="00392-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="00392-137">Установите hello wfastcgi и django пакетов, использующих PIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="00392-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="00392-138">Python 2.7 при помощи hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="00392-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="00392-139">Python 3.4 при помощи hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="00392-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="00392-140">Установка IIS с поддержкой FastCGI</span><span class="sxs-lookup"><span data-stu-id="00392-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="00392-141">Установите службы IIS с поддержкой FastCGI.</span><span class="sxs-lookup"><span data-stu-id="00392-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="00392-142">Это может занять несколько минут tooexecute.</span><span class="sxs-lookup"><span data-stu-id="00392-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="00392-143">Создание нового приложения Django</span><span class="sxs-lookup"><span data-stu-id="00392-143">Create a new Django application</span></span>
1. <span data-ttu-id="00392-144">В C:\inetpub\wwwroot toocreate новый проект Django, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="00392-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="00392-145">Python 2.7 при помощи hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="00392-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="00392-146">Python 3.4 при помощи hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="00392-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Hello результат команды New-AzureService hello](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="00392-148">Hello `django-admin` команда создает базовую структуру для веб-сайтов на основе Django:</span><span class="sxs-lookup"><span data-stu-id="00392-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="00392-149">`helloworld\manage.py` поможет вам начать и остановить размещение веб-сайта на основе Django.</span><span class="sxs-lookup"><span data-stu-id="00392-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="00392-150">`helloworld\helloworld\settings.py` содержит настройки Django для приложения.</span><span class="sxs-lookup"><span data-stu-id="00392-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="00392-151">`helloworld\helloworld\urls.py`имеет кода hello сопоставления между каждого URL-адреса и его представление.</span><span class="sxs-lookup"><span data-stu-id="00392-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="00392-152">В каталоге C:\inetpub\wwwroot\helloworld\helloworld hello создайте новый файл с именем views.py.</span><span class="sxs-lookup"><span data-stu-id="00392-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="00392-153">Этот файл имеет hello представление, которое отображает hello страницы «hello world».</span><span class="sxs-lookup"><span data-stu-id="00392-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="00392-154">В редакторе кода введите следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="00392-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="00392-155">Замените содержимое файла urls.py hello hello hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="00392-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="00392-156">Настройка IIS</span><span class="sxs-lookup"><span data-stu-id="00392-156">Set up IIS</span></span>
1. <span data-ttu-id="00392-157">В hello глобального файла applicationhost.config Разблокируйте раздел обработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="00392-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="00392-158">Это позволяет обработчик Python hello toouse файла web.config.</span><span class="sxs-lookup"><span data-stu-id="00392-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="00392-159">Добавьте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="00392-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="00392-160">Активируйте WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="00392-160">Activate WFastCGI.</span></span> <span data-ttu-id="00392-161">Это добавляет приложения toohello глобального файла applicationhost.config, который ссылается tooyour интерпретатор исполняемый файл и hello wfastcgi.py сценарий Python.</span><span class="sxs-lookup"><span data-stu-id="00392-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="00392-162">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="00392-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="00392-163">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="00392-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="00392-164">Создайте файл web.config в каталоге C:\inetpub\wwwroot\helloworld.</span><span class="sxs-lookup"><span data-stu-id="00392-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="00392-165">Здравствуйте, значение hello `scriptProcessor` атрибут должен соответствовать hello выходные данные предшествующей шаг hello.</span><span class="sxs-lookup"><span data-stu-id="00392-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="00392-166">Дополнительные сведения о параметре wfastcgi hello см. в разделе [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="00392-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="00392-167">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="00392-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="00392-168">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="00392-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="00392-169">Обновите расположение hello приветствия IIS по умолчанию веб-сайт toopoint toohello Django папки проекта:</span><span class="sxs-lookup"><span data-stu-id="00392-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="00392-170">Загрузите hello веб-страницу в браузере.</span><span class="sxs-lookup"><span data-stu-id="00392-170">Load hello webpage in your browser.</span></span>

![Окно обозревателя отображает hello hello world страницы в Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="00392-172">Завершение работы виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="00392-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="00392-173">После завершения работы с учебником, рекомендуется завершить работу или удаление виртуальной Машины Azure, созданную для учебника hello hello.</span><span class="sxs-lookup"><span data-stu-id="00392-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="00392-174">Это позволит освободить ресурсы для работы с другими руководствами, а также избежать расходов за использование Azure.</span><span class="sxs-lookup"><span data-stu-id="00392-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
