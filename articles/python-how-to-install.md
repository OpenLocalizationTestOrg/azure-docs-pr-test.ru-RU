---
title: "aaaInstall Python и hello SDK — Azure"
description: "Узнайте, как tooinstall Python и hello toouse SDK с Azure."
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a>Установка Python и hello SDK
Python легко tooset работает в Windows и уже предварительно установлен на Mac, Linux, и [Bash Windows](https://msdn.microsoft.com/commandline/wsl/about). В этом руководстве рассматривается установка и подготовка компьютера к использованию с Azure.

## <a name="whats-in-hello-python-azure-sdk"></a>Что находится в hello Python Azure SDK?
компоненты, позволяющие toodevelop включает Hello Azure SDK для Python, развертывания и управления приложениями Python для Azure. В частности hello Azure SDK для Python содержит hello следующее:

* **Библиотеки управления**. Эти библиотеки классов предоставляют управляемые через интерфейс ресурсы Azure, такие как учетные записи хранения и виртуальные машины.
* **Библиотеки среды выполнения**. Эти библиотеки классов предоставляют интерфейс для доступа к компонентам Azure, таким как хранилище и служебная шина.

## <a name="which-python-and-which-version-toouse"></a>Какие Python и какие версии toouse
Доступно несколько видов интерпретаторов Python, например:

* CPython - интерпретатор Python стандартных и наиболее часто используемые hello
* PyPy - tooCPython быстрый, совместимые альтернативной реализации
* IronPython — интерпретатор Python, работающий на базе .net/CLR;
* Jython - интерпретатор Python, которое выполняется на виртуальной машине Java hello

**CPython** v2.7 или v3.3 + и PyPy 5.4.0 будут протестированы и поддерживаются для hello Azure SDK для Python.

## <a name="where-tooget-python"></a>Где tooget Python?
Существует несколько способов tooget CPython.

* непосредственно с сайта [www.python.org][www.python.org];
* у известного поставщика дистрибутивов, например [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] или [www.activestate.com][www.activestate.com].
* Построение из исходного кода!

Если нет особой необходимости корпорация Майкрософт рекомендует hello первые два варианта.

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Установка пакета SDK в Windows, Linux и MacOS (только клиентские библиотеки)
Если уже установлена Python, можно использовать tooinstall PIP-адрес пакета все клиентские библиотеки hello в существующих Python 2.7 или в среде Python 3.3 +. Это загружает пакеты hello из hello [индекс пакета Python] [ Python Package Index] (PyPI).

Могут потребоваться права администратора:

* Linux и MacOS, используют hello `sudo` команды: `sudo pip install azure-mgmt-compute`.
* В Windows откройте окно командной строки или окно PowerShell от имени администратора.

Вы можете установить каждую библиотеку отдельно для каждой службы Azure:

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

Предварительный просмотр пакетов можно установить с помощью hello `--pre` флаг:

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

Можно также установить набор библиотек Azure в одной строке с помощью hello `azure` мета пакета. Здравствуйте, так как не все пакеты в этом пакете meta публикуются как стабильная еще, `azure` мета пакет находится на стадии предварительной версии.
Тем не менее hello основные пакеты с точки зрения качества и полноту кода можно считать «устойчивым» в данный момент

* Соответствующая отметка будет добавлена как можно скорее и синхронно с другими языками.
  До тех пор мы не планируем каких-либо значительных изменений.

Так как это предварительная версия, необходимы toouse hello `--pre` флаг:

```console
   $ pip install --pre azure
```

или напрямую:

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>Получение дополнительных пакетов
Hello [индекс пакета Python] [ Python Package Index] (PyPI) имеет широкий выбор библиотек Python.  Если выбрано tooinstall дистрибутив будет уже обладаете почти всеми hello интересных bits для различных сценариев из tooTechnical разработка web вычислениям.

## <a name="python-tools-for-visual-studio"></a>Средства Python для Visual Studio
[Инструменты Python для Visual Studio][Инструменты Python для Visual Studio] (PTVS) представляют собой бесплатный подключаемый модуль с открытым исходным кодом от корпорации Майкрософт, который превращает Visual Studio в полноценную интегрированную среду разработки Python.

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

Использование средств PTVS необязательно, однако рекомендуется, поскольку они обеспечивают поддержку Python и веб-проектов/решений, отладку, профилирование, интерактивное окно, редактирование шаблонов и Intellisense.

PTVS также позволяет легко toodeploy tooMicrosoft Azure, поддержка развертывания слишком[облачные службы](cloud-services/cloud-services-python-ptvs.md) и [веб-сайтов](app-service-web/web-sites-python-ptvs-django-mysql.md).

PTVS работает с установленными экземплярами Visual Studio 2013, 2015 или 2017.  Документацию, скачиваемые материалы и обсуждения см. на странице [Инструменты Python для Visual Studio].  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>Сценарии Python Azure для Linux и MacOS
Для Linux и MacOS существуют следующие основные поддерживаемые сценарии Azure:

1. Использование служб Azure с помощью hello клиентские библиотеки для Python
2. Запуск приложения на виртуальной машине Linux
3. Разработка и публикации tooAzure веб-сайтов с помощью Git

первый сценарий Hello позволяет tooauthor многофункциональных веб-приложений, которые использовать hello Azure PaaS функции, такие как [хранилище больших двоичных объектов](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [хранилище очередей](storage/queues/storage-python-how-to-use-queue-storage.md), [хранилище таблиц](cosmos-db/table-storage-how-to-use-python.md) т. д. через Pythonic оболочки для hello интерфейсы API REST Azure. Они совершенно одинаково работают в Windows, Mac и Linux.  Можно также использовать эти клиентские библиотеки из вашей локальной машины или виртуальной машины Linux в Azure.

Для сценария hello виртуальных Машин просто запустить виртуальную Машину Linux по вашему выбору (Ubuntu, CentOS, Suse) и выполнения и управлять вам нравится.  Например, можно запустить [IPython] [ IPython] REPL ПК на компьютере Windows, Mac и Linux и точки вашего браузера tooa Linux или Windows запущена виртуальная машина мультипроцессорном hello IPython Engine в Azure.

Сведения о том, как tooset ВМ Linux, см. hello [создать виртуальную машину под управлением Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) учебника.

С помощью Git развертывания, можно разрабатывать веб-приложения Python и опубликовать его tooan веб-сайта Azure из любой операционной системы.  При выполнении отправки к tooAzure репозитория, он автоматически создает виртуальную среду и pip устанавливает необходимые пакеты.

Дополнительные сведения о разработке и публикации веб-сайтов Azure см. в разделе hello учебники по [Создание веб-сайтов с Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Создание веб-сайтов с бутылка](app-service-web/web-sites-python-create-deploy-bottle-app.md), и [Создание веб-сайтов с Термосе](app-service-web/web-sites-python-create-deploy-flask-app.md). Дополнительные сведения об использовании совместимой с WSGI платформы см. в статье [Настройка Python в веб-приложениях службы приложений Azure](app-service-web/web-sites-python-configure.md).

## <a name="additional-software-and-resources"></a>Дополнительные ресурсы и программное обеспечение:
* [Пакет SDK Azure для Python — ReadTheDocs](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [Пакет SDK Azure для Python — GitHub](https://github.com/Azure/azure-sdk-for-python)
* [Официальные примеры кода Azure для Python](https://azure.microsoft.com/documentation/samples/?platform=python)
* [Распространяемая среда аналитики Python][Continuum Analytics Python Distribution]
* [Распространяемый набор Enthought Python][Enthought Python Distribution]
* [Распространяемый набор ActiveState Python][ActiveState Python Distribution]
* [SciPy — набор научных библиотек Python][SciPy - A suite of Scientific Python libraries]
* [NumPy — библиотека числовых значений для Python][NumPy - A numerics library for Python]
* [Django Project — зрелая веб-платформа или CMS][Django Project - A mature web framework/CMS]
* [IPython — расширенное использование REPL и Notebook для Python][IPython - an advanced REPL/Notebook for Python]
* [Средства Python для Visual Studio на сайте GitHub][Python Tools for Visual Studio on GitHub]
* [Центр по разработке для Python](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Инструменты Python для Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
