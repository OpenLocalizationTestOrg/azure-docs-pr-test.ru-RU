---
title: "Настройка Python в веб-приложениях службы приложений Azure"
description: "В этом учебнике описываются возможности создания и настройки в веб-приложениях службы приложений Azure базового приложения Python, совместимого с интерфейсом шлюза веб-сервера (WSGI)."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 9683a1af13eeff364d3c4714f0b791324fd82659
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="736fe-103">Настройка Python в веб-приложениях службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="736fe-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="736fe-104">В этом учебнике описываются возможности создания и настройки в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714)базового приложения Python, совместимого с интерфейсом шлюза веб-сервера (WSGI).</span><span class="sxs-lookup"><span data-stu-id="736fe-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="736fe-105">Здесь также описываются дополнительные функции развертывания Git, например установка виртуальной среды или пакета с использованием файла requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="736fe-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="736fe-106">Bottle, Django или Flask?</span><span class="sxs-lookup"><span data-stu-id="736fe-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="736fe-107">В Azure Marketplace содержатся шаблоны для платформ Bottle, Django и Flask.</span><span class="sxs-lookup"><span data-stu-id="736fe-107">The Azure Marketplace contains templates for the Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="736fe-108">Если вы разрабатываете свое первое веб-приложение в службе приложений Azure или не знакомы с Git, советуем следовать одному из указанных ниже учебников, которые содержат пошаговые указания по созданию рабочего приложения из коллекции с помощью развертывания Git в Windows или Mac:</span><span class="sxs-lookup"><span data-stu-id="736fe-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from the gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="736fe-109">Создание веб-приложений на основе Bottle</span><span class="sxs-lookup"><span data-stu-id="736fe-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="736fe-110">Создание веб-приложений на основе Django</span><span class="sxs-lookup"><span data-stu-id="736fe-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="736fe-111">Создание веб-приложений на основе Flask</span><span class="sxs-lookup"><span data-stu-id="736fe-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="736fe-112">Создание веб-приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="736fe-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="736fe-113">Этот учебник предполагает наличие существующей подписки Azure и доступа к порталу Azure.</span><span class="sxs-lookup"><span data-stu-id="736fe-113">This tutorial assumes an existing Azure subscription and access to the Azure Portal.</span></span>

<span data-ttu-id="736fe-114">Если у вас нет веб-приложения, его можно создать на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="736fe-114">If you do not have an existing web app, you can create one from the [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="736fe-115">В верхнем левом углу нажмите кнопку "Создать", а затем щелкните **Интернет + мобильные устройства** > **Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="736fe-115">Click the NEW button in the top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="736fe-116">Публикация с использованием Git</span><span class="sxs-lookup"><span data-stu-id="736fe-116">Git Publishing</span></span>
<span data-ttu-id="736fe-117">Настройте публикацию Git для вновь созданного веб-приложения, следуя инструкциям из статьи [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="736fe-117">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="736fe-118">В этом учебнике для создания, контроля и публикации веб-приложения Python в службе приложений Azure используется Git.</span><span class="sxs-lookup"><span data-stu-id="736fe-118">This tutorial uses Git to create, manage, and publish our Python web app to Azure App Service.</span></span>

<span data-ttu-id="736fe-119">После настройки публикации с помощью Git будет создан репозиторий Git, который затем будет связан с вашим веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="736fe-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="736fe-120">Появится URL-адрес репозитория, который с этого момента может использоваться для передачи данных в облако из локальной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="736fe-120">The repository's URL will be displayed and can henceforth be used to push data from the local development environment to the cloud.</span></span> <span data-ttu-id="736fe-121">Для публикации приложений с помощью Git убедитесь, что клиент Git также установлен. Затем следуйте предоставленным указаниям для передачи содержимого веб-приложения в службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="736fe-121">To publish applications via Git, make sure a Git client is also installed and use the instructions provided to push your web app content to Azure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="736fe-122">Обзор приложения</span><span class="sxs-lookup"><span data-stu-id="736fe-122">Application Overview</span></span>
<span data-ttu-id="736fe-123">В дальнейших разделах будут созданы следующие файлы.</span><span class="sxs-lookup"><span data-stu-id="736fe-123">In the next sections, the following files are created.</span></span> <span data-ttu-id="736fe-124">Их нужно сохранить в корневую папку репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="736fe-124">They should be placed in the root of the Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="736fe-125">Обработчик WSGI</span><span class="sxs-lookup"><span data-stu-id="736fe-125">WSGI Handler</span></span>
<span data-ttu-id="736fe-126">WSGI — это стандарт Python, описываемый в [PEP 3333](http://www.python.org/dev/peps/pep-3333/) и определяющий интерфейс между веб-сервером и Python.</span><span class="sxs-lookup"><span data-stu-id="736fe-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between the web server and Python.</span></span> <span data-ttu-id="736fe-127">Он предоставляет стандартный интерфейс для написания различных веб-приложений и платформ с использованием Python.</span><span class="sxs-lookup"><span data-stu-id="736fe-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="736fe-128">Сегодня популярные веб-платформы Python используют WSGI.</span><span class="sxs-lookup"><span data-stu-id="736fe-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="736fe-129">Веб-приложения службы приложений Azure предоставляют поддержку любых таких платформ. Кроме того, опытные пользователи даже могут создавать собственные платформы, если пользовательский обработчик следует правилам спецификации WSGI.</span><span class="sxs-lookup"><span data-stu-id="736fe-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as the custom handler follows the WSGI specification guidelines.</span></span>

<span data-ttu-id="736fe-130">Ниже приведен пример кода `app.py`, который определяет настраиваемый обработчик:</span><span class="sxs-lookup"><span data-stu-id="736fe-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="736fe-131">Это приложение можно запустить локально с помощью `python app.py`, а затем перейти в браузере по адресу `http://localhost:5555`.</span><span class="sxs-lookup"><span data-stu-id="736fe-131">You can run this application locally with `python app.py`, then browse to `http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="736fe-132">Виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="736fe-132">Virtual Environment</span></span>
<span data-ttu-id="736fe-133">Хотя приведенное выше приложение не требует каких-либо внешних пакетов, они, вероятно, потребуются.</span><span class="sxs-lookup"><span data-stu-id="736fe-133">Although the example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="736fe-134">Для облегчения управления зависимостями внешних пакетов, развертывание Azure Git поддерживает создание виртуальных сред.</span><span class="sxs-lookup"><span data-stu-id="736fe-134">To help manage external package dependencies, Azure Git deployment supports the creation of virtual environments.</span></span>

<span data-ttu-id="736fe-135">Если платформа Azure обнаруживает в корневой папке репозитория файл requirements.txt, она автоматически создает виртуальную среду с именем `env`.</span><span class="sxs-lookup"><span data-stu-id="736fe-135">When Azure detects a requirements.txt in the root of the repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="736fe-136">Это происходит только при первом развертывании или после изменения выбранной среды выполнения Python.</span><span class="sxs-lookup"><span data-stu-id="736fe-136">This only occurs on the first deployment, or during any deployment after the selected Python runtime has changed.</span></span>

<span data-ttu-id="736fe-137">Возможно, потребуется создать виртуальную среду для локальной разработки, но не нужно включать ее в репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="736fe-137">You will probably want to create a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="736fe-138">Управление пакетами</span><span class="sxs-lookup"><span data-stu-id="736fe-138">Package Management</span></span>
<span data-ttu-id="736fe-139">Пакеты, перечисленные в файле requirements.txt, устанавливаются автоматически в виртуальной среде с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="736fe-139">Packages listed in requirements.txt will be installed automatically in the virtual environment using pip.</span></span> <span data-ttu-id="736fe-140">Это происходит при каждом развертывании, но если пакет уже установлен, pip пропустит установку.</span><span class="sxs-lookup"><span data-stu-id="736fe-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="736fe-141">Пример `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="736fe-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="736fe-142">Версия Python</span><span class="sxs-lookup"><span data-stu-id="736fe-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="736fe-143">Пример `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="736fe-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="736fe-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="736fe-144">Web.config</span></span>
<span data-ttu-id="736fe-145">Чтобы указать, как сервер должен обрабатывать запросы, нужно будет создать файл web.config.</span><span class="sxs-lookup"><span data-stu-id="736fe-145">You'll need to create a web.config file to specify how the server should handle requests.</span></span>

<span data-ttu-id="736fe-146">Обратите внимание, что если в репозитории есть файл web.x.y.config, в котором x.y совпадает с выбранной средой выполнения Python, а затем Azure автоматически скопирует соответствующий файл с именем web.config.</span><span class="sxs-lookup"><span data-stu-id="736fe-146">Note that if you have a web.x.y.config file in your repository, where x.y matches the selected Python runtime, then Azure will automatically copy the appropriate file as web.config.</span></span>

<span data-ttu-id="736fe-147">Следующие примеры файла web.config зависят от сценария прокси в виртуальной среде, который описан в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="736fe-147">The following web.config examples rely on a virtual environment proxy script, which is described in the next section.</span></span>  <span data-ttu-id="736fe-148">Они работают с обработчиком WSGI, который использовался в приведенном выше примере `app.py` .</span><span class="sxs-lookup"><span data-stu-id="736fe-148">They work with the WSGI handler used in the example `app.py` above.</span></span>

<span data-ttu-id="736fe-149">Пример файла `web.config` для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="736fe-149">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="736fe-150">Пример файла `web.config` для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="736fe-150">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="736fe-151">Для повышения производительности статические файлы будут непосредственно обрабатываться веб-сервером без использования кода Python.</span><span class="sxs-lookup"><span data-stu-id="736fe-151">Static files will be handled by the web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="736fe-152">В приведенных выше примерах расположение статических файлов на диске должно совпадать с расположением в поле URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="736fe-152">In the above examples, the location of the static files on disk should match the location in the URL.</span></span> <span data-ttu-id="736fe-153">Это означает, что запрос `http://pythonapp.azurewebsites.net/static/site.css` будет использовать файл на диске в расположении `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="736fe-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve the file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="736fe-154">`WSGI_ALT_VIRTUALENV_HANDLER` — здесь указывается обработчик WSGI.</span><span class="sxs-lookup"><span data-stu-id="736fe-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify the WSGI handler.</span></span> <span data-ttu-id="736fe-155">А в приведенных выше примерах обработчик указывается в файле `app.wsgi_app`, так как обработчик является функцией с именем `wsgi_app` в файле `app.py` в корневой папке.</span><span class="sxs-lookup"><span data-stu-id="736fe-155">In the above examples, it's `app.wsgi_app` because the handler is a function named `wsgi_app` in `app.py` in the root folder.</span></span>

<span data-ttu-id="736fe-156">`PYTHONPATH` можно настраивать, но если вы устанавливаете все зависимости в виртуальной среде, указывая их в файле requirements.txt, путь менять не нужно.</span><span class="sxs-lookup"><span data-stu-id="736fe-156">`PYTHONPATH` can be customized, but if you install all your dependencies in the virtual environment by specifying them in requirements.txt, you shouldn't need to change it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="736fe-157">Прокси-сервер с поддержкой виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="736fe-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="736fe-158">Следующий сценарий используется для извлечения обработчика WSGI, активации виртуальной среды и ведения журнала ошибок.</span><span class="sxs-lookup"><span data-stu-id="736fe-158">The following script is used to retrieve the WSGI handler, activate the virtual environment and log errors.</span></span> <span data-ttu-id="736fe-159">Он разработан как универсальный и применяется без изменений.</span><span class="sxs-lookup"><span data-stu-id="736fe-159">It is designed to be generic and used without modifications.</span></span>

<span data-ttu-id="736fe-160">Содержимое `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="736fe-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject to terms and conditions of the Apache License, Version 2.0. A 
     # copy of the license can be found in the License.html file at the root of this distribution. If 
     # you cannot locate the Apache License, Version 2.0, please send an email to 
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing to be bound 
     # by the terms of the Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors to a log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="736fe-161">Настройка развертывания Git</span><span class="sxs-lookup"><span data-stu-id="736fe-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="736fe-162">Устранение неполадок — установка пакета</span><span class="sxs-lookup"><span data-stu-id="736fe-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="736fe-163">Устранение неполадок — виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="736fe-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="736fe-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="736fe-164">Next steps</span></span>
<span data-ttu-id="736fe-165">Дополнительную информацию можно найти в [Центре разработчика Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="736fe-165">For more information, see the [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="736fe-166">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="736fe-166">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="736fe-167">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="736fe-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="736fe-168">Изменения</span><span class="sxs-lookup"><span data-stu-id="736fe-168">What's changed</span></span>
* <span data-ttu-id="736fe-169">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="736fe-169">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

