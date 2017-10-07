---
title: "aaaConfiguring Python с веб-приложениях службы приложений Azure"
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
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="c8667-103">Настройка Python в веб-приложениях службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c8667-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="c8667-104">В этом учебнике описываются возможности создания и настройки в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714)базового приложения Python, совместимого с интерфейсом шлюза веб-сервера (WSGI).</span><span class="sxs-lookup"><span data-stu-id="c8667-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="c8667-105">Здесь также описываются дополнительные функции развертывания Git, например установка виртуальной среды или пакета с использованием файла requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c8667-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="c8667-106">Bottle, Django или Flask?</span><span class="sxs-lookup"><span data-stu-id="c8667-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="c8667-107">Hello Azure Marketplace содержит шаблоны для hello бутылка, Django и термосе платформ.</span><span class="sxs-lookup"><span data-stu-id="c8667-107">hello Azure Marketplace contains templates for hello Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="c8667-108">Если вы разрабатываете первого веб-приложения в службе приложений Azure, или вы не знакомы с Git, рекомендуется использовать один из этих учебников, которые включают пошаговые инструкции по созданию работающее приложение из коллекции hello через Git развертывания из Windows или Mac:</span><span class="sxs-lookup"><span data-stu-id="c8667-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from hello gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="c8667-109">Создание веб-приложений на основе Bottle</span><span class="sxs-lookup"><span data-stu-id="c8667-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="c8667-110">Создание веб-приложений на основе Django</span><span class="sxs-lookup"><span data-stu-id="c8667-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="c8667-111">Создание веб-приложений на основе Flask</span><span class="sxs-lookup"><span data-stu-id="c8667-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="c8667-112">Создание веб-приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="c8667-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="c8667-113">В этом учебнике предполагается существующих Azure подписки и доступа toohello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c8667-113">This tutorial assumes an existing Azure subscription and access toohello Azure Portal.</span></span>

<span data-ttu-id="c8667-114">Если нет существующего веб-приложения, можно создать один из hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c8667-114">If you do not have an existing web app, you can create one from hello [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="c8667-115">Щелкните новую кнопку hello в верхнем левом углу hello, а затем нажмите кнопку **Интернет + мобильные устройства** > **веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="c8667-115">Click hello NEW button in hello top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="c8667-116">Публикация с использованием Git</span><span class="sxs-lookup"><span data-stu-id="c8667-116">Git Publishing</span></span>
<span data-ttu-id="c8667-117">Настроить публикацию Git для только что созданный веб-приложения в соответствии с инструкциями hello в [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c8667-117">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="c8667-118">В этом учебнике используется Git toocreate, управление и публикация нашей tooAzure web app Python службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c8667-118">This tutorial uses Git toocreate, manage, and publish our Python web app tooAzure App Service.</span></span>

<span data-ttu-id="c8667-119">После настройки публикации с помощью Git будет создан репозиторий Git, который затем будет связан с вашим веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="c8667-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="c8667-120">URL-адрес репозитория Hello будет отображаться и исходя из можно используется toopush данные из облака toohello среде местного разработки hello.</span><span class="sxs-lookup"><span data-stu-id="c8667-120">hello repository's URL will be displayed and can henceforth be used toopush data from hello local development environment toohello cloud.</span></span> <span data-ttu-id="c8667-121">toopublish приложений через Git, убедитесь, что клиент Git также устанавливается и используется hello инструкции toopush содержимого tooAzure каталога приложения к web службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c8667-121">toopublish applications via Git, make sure a Git client is also installed and use hello instructions provided toopush your web app content tooAzure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="c8667-122">Обзор приложений</span><span class="sxs-lookup"><span data-stu-id="c8667-122">Application Overview</span></span>
<span data-ttu-id="c8667-123">В следующих разделах hello создаются следующие файлы hello.</span><span class="sxs-lookup"><span data-stu-id="c8667-123">In hello next sections, hello following files are created.</span></span> <span data-ttu-id="c8667-124">Они должны находиться в корне hello hello репозитории.</span><span class="sxs-lookup"><span data-stu-id="c8667-124">They should be placed in hello root of hello Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="c8667-125">Обработчик WSGI</span><span class="sxs-lookup"><span data-stu-id="c8667-125">WSGI Handler</span></span>
<span data-ttu-id="c8667-126">WSGI — это стандарт Python, описываемого [PEP 3333](http://www.python.org/dev/peps/pep-3333/) определение интерфейса между hello веб-сервера и Python.</span><span class="sxs-lookup"><span data-stu-id="c8667-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between hello web server and Python.</span></span> <span data-ttu-id="c8667-127">Он предоставляет стандартный интерфейс для написания различных веб-приложений и платформ с использованием Python.</span><span class="sxs-lookup"><span data-stu-id="c8667-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="c8667-128">Сегодня популярные веб-платформы Python используют WSGI.</span><span class="sxs-lookup"><span data-stu-id="c8667-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="c8667-129">Azure предоставляет веб-приложений приложения служб поддержки для таких платформ; Кроме того Опытные пользователи могут даже создать собственные до тех пор, пока пользовательский обработчик hello следует hello WSGI спецификации рекомендации.</span><span class="sxs-lookup"><span data-stu-id="c8667-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as hello custom handler follows hello WSGI specification guidelines.</span></span>

<span data-ttu-id="c8667-130">Ниже приведен пример кода `app.py`, который определяет настраиваемый обработчик:</span><span class="sxs-lookup"><span data-stu-id="c8667-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

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

<span data-ttu-id="c8667-131">Можно запустить это приложение локально с `python app.py`, найдите слишком`http://localhost:5555` в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="c8667-131">You can run this application locally with `python app.py`, then browse too`http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="c8667-132">Виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="c8667-132">Virtual Environment</span></span>
<span data-ttu-id="c8667-133">Несмотря на то, что выше пример приложения hello не требует каких-либо внешних пакетов, вполне вероятно, что некоторые необходимые приложению.</span><span class="sxs-lookup"><span data-stu-id="c8667-133">Although hello example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="c8667-134">toohelp управлять внешние зависимости, развертывание Azure Git поддерживает создание виртуальных сред hello.</span><span class="sxs-lookup"><span data-stu-id="c8667-134">toohelp manage external package dependencies, Azure Git deployment supports hello creation of virtual environments.</span></span>

<span data-ttu-id="c8667-135">Когда Azure обнаруживает requirements.txt в корневом каталоге hello hello репозитория, автоматически создает виртуальной среды с именем `env`.</span><span class="sxs-lookup"><span data-stu-id="c8667-135">When Azure detects a requirements.txt in hello root of hello repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="c8667-136">Это происходит только при первом развертывании hello, или во время развертывания после hello заменена выбранной среды выполнения Python.</span><span class="sxs-lookup"><span data-stu-id="c8667-136">This only occurs on hello first deployment, or during any deployment after hello selected Python runtime has changed.</span></span>

<span data-ttu-id="c8667-137">Будет необходимо toocreate виртуальную среду для разработки локально, но без включения его в репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="c8667-137">You will probably want toocreate a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="c8667-138">Управление пакетами</span><span class="sxs-lookup"><span data-stu-id="c8667-138">Package Management</span></span>
<span data-ttu-id="c8667-139">Пакеты, перечисленные в requirements.txt устанавливаются автоматически в виртуальной среде hello, с помощью PIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c8667-139">Packages listed in requirements.txt will be installed automatically in hello virtual environment using pip.</span></span> <span data-ttu-id="c8667-140">Это происходит при каждом развертывании, но если пакет уже установлен, pip пропустит установку.</span><span class="sxs-lookup"><span data-stu-id="c8667-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="c8667-141">Пример `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="c8667-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="c8667-142">Версия Python</span><span class="sxs-lookup"><span data-stu-id="c8667-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="c8667-143">Пример `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="c8667-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="c8667-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="c8667-144">Web.config</span></span>
<span data-ttu-id="c8667-145">Вам потребуется toocreate toospecify файл web.config способа обработки запросов сервером hello.</span><span class="sxs-lookup"><span data-stu-id="c8667-145">You'll need toocreate a web.config file toospecify how hello server should handle requests.</span></span>

<span data-ttu-id="c8667-146">Обратите внимание, что если имеется файл web.x.y.config в репозиторий, где x.y соответствует hello выбранной среды выполнения Python, то Azure будет автоматически копировать hello соответствующий файл web.config.</span><span class="sxs-lookup"><span data-stu-id="c8667-146">Note that if you have a web.x.y.config file in your repository, where x.y matches hello selected Python runtime, then Azure will automatically copy hello appropriate file as web.config.</span></span>

<span data-ttu-id="c8667-147">Hello следующие примеры web.config полагаться на скрипт прокси-сервера виртуальной среды, как описано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="c8667-147">hello following web.config examples rely on a virtual environment proxy script, which is described in hello next section.</span></span>  <span data-ttu-id="c8667-148">Они работают с обработчиком WSGI hello, используемый в примере hello `app.py` выше.</span><span class="sxs-lookup"><span data-stu-id="c8667-148">They work with hello WSGI handler used in hello example `app.py` above.</span></span>

<span data-ttu-id="c8667-149">Пример файла `web.config` для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="c8667-149">Example `web.config` for Python 2.7:</span></span>

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


<span data-ttu-id="c8667-150">Пример файла `web.config` для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="c8667-150">Example `web.config` for Python 3.4:</span></span>

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


<span data-ttu-id="c8667-151">Статические файлы будут проводиться hello веб-сервер напрямую, минуя кода Python, для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="c8667-151">Static files will be handled by hello web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="c8667-152">В hello выше примеры местоположение hello hello статических файлов на диске должно соответствовать расположение hello в URL-АДРЕСЕ hello.</span><span class="sxs-lookup"><span data-stu-id="c8667-152">In hello above examples, hello location of hello static files on disk should match hello location in hello URL.</span></span> <span data-ttu-id="c8667-153">Это означает, что запрос `http://pythonapp.azurewebsites.net/static/site.css` будет обслуживать hello файла на диске в `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="c8667-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve hello file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="c8667-154">`WSGI_ALT_VIRTUALENV_HANDLER`Определяет, где задается обработчик WSGI hello.</span><span class="sxs-lookup"><span data-stu-id="c8667-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify hello WSGI handler.</span></span> <span data-ttu-id="c8667-155">В hello выше примерах выбрано `app.wsgi_app` так, как обработчик hello является функция с именем `wsgi_app` в `app.py` в корневой папке hello.</span><span class="sxs-lookup"><span data-stu-id="c8667-155">In hello above examples, it's `app.wsgi_app` because hello handler is a function named `wsgi_app` in `app.py` in hello root folder.</span></span>

<span data-ttu-id="c8667-156">`PYTHONPATH`можно настроить, но при установке всех зависимостей в виртуальной среде hello, указав их в requirements.txt не должны toochange его.</span><span class="sxs-lookup"><span data-stu-id="c8667-156">`PYTHONPATH` can be customized, but if you install all your dependencies in hello virtual environment by specifying them in requirements.txt, you shouldn't need toochange it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="c8667-157">Прокси-сервер с поддержкой виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="c8667-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="c8667-158">следующий скрипт Hello используется tooretrieve hello WSGI обработчика, активировать hello виртуальной среды и журнал ошибок.</span><span class="sxs-lookup"><span data-stu-id="c8667-158">hello following script is used tooretrieve hello WSGI handler, activate hello virtual environment and log errors.</span></span> <span data-ttu-id="c8667-159">Это спроектированный toobe универсальными и применяются без изменений.</span><span class="sxs-lookup"><span data-stu-id="c8667-159">It is designed toobe generic and used without modifications.</span></span>

<span data-ttu-id="c8667-160">Содержимое `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="c8667-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
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
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
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


## <a name="customize-git-deployment"></a><span data-ttu-id="c8667-161">Настройка развертывания Git</span><span class="sxs-lookup"><span data-stu-id="c8667-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="c8667-162">Устранение неполадок — установка пакета</span><span class="sxs-lookup"><span data-stu-id="c8667-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="c8667-163">Устранение неполадок — виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="c8667-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="c8667-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8667-164">Next steps</span></span>
<span data-ttu-id="c8667-165">Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="c8667-165">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="c8667-166">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="c8667-166">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c8667-167">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="c8667-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="c8667-168">Изменения</span><span class="sxs-lookup"><span data-stu-id="c8667-168">What's changed</span></span>
* <span data-ttu-id="c8667-169">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c8667-169">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

