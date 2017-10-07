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
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Настройка Python в веб-приложениях службы приложений Azure
В этом учебнике описываются возможности создания и настройки в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714)базового приложения Python, совместимого с интерфейсом шлюза веб-сервера (WSGI).

Здесь также описываются дополнительные функции развертывания Git, например установка виртуальной среды или пакета с использованием файла requirements.txt.

## <a name="bottle-django-or-flask"></a>Bottle, Django или Flask?
Hello Azure Marketplace содержит шаблоны для hello бутылка, Django и термосе платформ. Если вы разрабатываете первого веб-приложения в службе приложений Azure, или вы не знакомы с Git, рекомендуется использовать один из этих учебников, которые включают пошаговые инструкции по созданию работающее приложение из коллекции hello через Git развертывания из Windows или Mac:

* [Создание веб-приложений на основе Bottle](web-sites-python-create-deploy-bottle-app.md)
* [Создание веб-приложений на основе Django](web-sites-python-create-deploy-django-app.md)
* [Создание веб-приложений на основе Flask](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Создание веб-приложения на портале Azure
В этом учебнике предполагается существующих Azure подписки и доступа toohello портала Azure.

Если нет существующего веб-приложения, можно создать один из hello [портала Azure](https://portal.azure.com).  Щелкните новую кнопку hello в верхнем левом углу hello, а затем нажмите кнопку **Интернет + мобильные устройства** > **веб-приложения**.

## <a name="git-publishing"></a>Публикация с использованием Git
Настроить публикацию Git для только что созданный веб-приложения в соответствии с инструкциями hello в [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md). В этом учебнике используется Git toocreate, управление и публикация нашей tooAzure web app Python службы приложений.

После настройки публикации с помощью Git будет создан репозиторий Git, который затем будет связан с вашим веб-приложением. URL-адрес репозитория Hello будет отображаться и исходя из можно используется toopush данные из облака toohello среде местного разработки hello. toopublish приложений через Git, убедитесь, что клиент Git также устанавливается и используется hello инструкции toopush содержимого tooAzure каталога приложения к web службы приложений.

## <a name="application-overview"></a>Обзор приложений
В следующих разделах hello создаются следующие файлы hello. Они должны находиться в корне hello hello репозитории.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>Обработчик WSGI
WSGI — это стандарт Python, описываемого [PEP 3333](http://www.python.org/dev/peps/pep-3333/) определение интерфейса между hello веб-сервера и Python. Он предоставляет стандартный интерфейс для написания различных веб-приложений и платформ с использованием Python. Сегодня популярные веб-платформы Python используют WSGI. Azure предоставляет веб-приложений приложения служб поддержки для таких платформ; Кроме того Опытные пользователи могут даже создать собственные до тех пор, пока пользовательский обработчик hello следует hello WSGI спецификации рекомендации.

Ниже приведен пример кода `app.py`, который определяет настраиваемый обработчик:

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

Можно запустить это приложение локально с `python app.py`, найдите слишком`http://localhost:5555` в веб-браузере.

## <a name="virtual-environment"></a>Виртуальная среда
Несмотря на то, что выше пример приложения hello не требует каких-либо внешних пакетов, вполне вероятно, что некоторые необходимые приложению.

toohelp управлять внешние зависимости, развертывание Azure Git поддерживает создание виртуальных сред hello.

Когда Azure обнаруживает requirements.txt в корневом каталоге hello hello репозитория, автоматически создает виртуальной среды с именем `env`. Это происходит только при первом развертывании hello, или во время развертывания после hello заменена выбранной среды выполнения Python.

Будет необходимо toocreate виртуальную среду для разработки локально, но без включения его в репозиторий Git.

## <a name="package-management"></a>Управление пакетами
Пакеты, перечисленные в requirements.txt устанавливаются автоматически в виртуальной среде hello, с помощью PIP-адрес. Это происходит при каждом развертывании, но если пакет уже установлен, pip пропустит установку.

Пример `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>Версия Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

Пример `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
Вам потребуется toocreate toospecify файл web.config способа обработки запросов сервером hello.

Обратите внимание, что если имеется файл web.x.y.config в репозиторий, где x.y соответствует hello выбранной среды выполнения Python, то Azure будет автоматически копировать hello соответствующий файл web.config.

Hello следующие примеры web.config полагаться на скрипт прокси-сервера виртуальной среды, как описано в следующем разделе hello.  Они работают с обработчиком WSGI hello, используемый в примере hello `app.py` выше.

Пример файла `web.config` для Python 2.7:

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


Пример файла `web.config` для Python 3.4:

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


Статические файлы будут проводиться hello веб-сервер напрямую, минуя кода Python, для повышения производительности.

В hello выше примеры местоположение hello hello статических файлов на диске должно соответствовать расположение hello в URL-АДРЕСЕ hello. Это означает, что запрос `http://pythonapp.azurewebsites.net/static/site.css` будет обслуживать hello файла на диске в `\static\site.css`.

`WSGI_ALT_VIRTUALENV_HANDLER`Определяет, где задается обработчик WSGI hello. В hello выше примерах выбрано `app.wsgi_app` так, как обработчик hello является функция с именем `wsgi_app` в `app.py` в корневой папке hello.

`PYTHONPATH`можно настроить, но при установке всех зависимостей в виртуальной среде hello, указав их в requirements.txt не должны toochange его.

## <a name="virtual-environment-proxy"></a>Прокси-сервер с поддержкой виртуальной среды
следующий скрипт Hello используется tooretrieve hello WSGI обработчика, активировать hello виртуальной среды и журнал ошибок. Это спроектированный toobe универсальными и применяются без изменений.

Содержимое `ptvs_virtualenv_proxy.py`:

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


## <a name="customize-git-deployment"></a>Настройка развертывания Git
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>Устранение неполадок — установка пакета
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Устранение неполадок — виртуальная среда
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

