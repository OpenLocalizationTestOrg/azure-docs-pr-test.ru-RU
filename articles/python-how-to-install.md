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
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="6be17-103">Установка Python и hello SDK</span><span class="sxs-lookup"><span data-stu-id="6be17-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="6be17-104">Python легко tooset работает в Windows и уже предварительно установлен на Mac, Linux, и [Bash Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="6be17-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="6be17-105">В этом руководстве рассматривается установка и подготовка компьютера к использованию с Azure.</span><span class="sxs-lookup"><span data-stu-id="6be17-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="6be17-106">Что находится в hello Python Azure SDK?</span><span class="sxs-lookup"><span data-stu-id="6be17-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="6be17-107">компоненты, позволяющие toodevelop включает Hello Azure SDK для Python, развертывания и управления приложениями Python для Azure.</span><span class="sxs-lookup"><span data-stu-id="6be17-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="6be17-108">В частности hello Azure SDK для Python содержит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="6be17-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="6be17-109">**Библиотеки управления**.</span><span class="sxs-lookup"><span data-stu-id="6be17-109">**Management libraries**.</span></span> <span data-ttu-id="6be17-110">Эти библиотеки классов предоставляют управляемые через интерфейс ресурсы Azure, такие как учетные записи хранения и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="6be17-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="6be17-111">**Библиотеки среды выполнения**.</span><span class="sxs-lookup"><span data-stu-id="6be17-111">**Runtime libraries**.</span></span> <span data-ttu-id="6be17-112">Эти библиотеки классов предоставляют интерфейс для доступа к компонентам Azure, таким как хранилище и служебная шина.</span><span class="sxs-lookup"><span data-stu-id="6be17-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="6be17-113">Какие Python и какие версии toouse</span><span class="sxs-lookup"><span data-stu-id="6be17-113">Which Python and which version toouse</span></span>
<span data-ttu-id="6be17-114">Доступно несколько видов интерпретаторов Python, например:</span><span class="sxs-lookup"><span data-stu-id="6be17-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="6be17-115">CPython - интерпретатор Python стандартных и наиболее часто используемые hello</span><span class="sxs-lookup"><span data-stu-id="6be17-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="6be17-116">PyPy - tooCPython быстрый, совместимые альтернативной реализации</span><span class="sxs-lookup"><span data-stu-id="6be17-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="6be17-117">IronPython — интерпретатор Python, работающий на базе .net/CLR;</span><span class="sxs-lookup"><span data-stu-id="6be17-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="6be17-118">Jython - интерпретатор Python, которое выполняется на виртуальной машине Java hello</span><span class="sxs-lookup"><span data-stu-id="6be17-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="6be17-119">**CPython** v2.7 или v3.3 + и PyPy 5.4.0 будут протестированы и поддерживаются для hello Azure SDK для Python.</span><span class="sxs-lookup"><span data-stu-id="6be17-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="6be17-120">Где tooget Python?</span><span class="sxs-lookup"><span data-stu-id="6be17-120">Where tooget Python?</span></span>
<span data-ttu-id="6be17-121">Существует несколько способов tooget CPython.</span><span class="sxs-lookup"><span data-stu-id="6be17-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="6be17-122">непосредственно с сайта [www.python.org][www.python.org];</span><span class="sxs-lookup"><span data-stu-id="6be17-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="6be17-123">у известного поставщика дистрибутивов, например [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] или [www.activestate.com][www.activestate.com].</span><span class="sxs-lookup"><span data-stu-id="6be17-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="6be17-124">Построение из исходного кода!</span><span class="sxs-lookup"><span data-stu-id="6be17-124">Build from source!</span></span>

<span data-ttu-id="6be17-125">Если нет особой необходимости корпорация Майкрософт рекомендует hello первые два варианта.</span><span class="sxs-lookup"><span data-stu-id="6be17-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="6be17-126">Установка пакета SDK в Windows, Linux и MacOS (только клиентские библиотеки)</span><span class="sxs-lookup"><span data-stu-id="6be17-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="6be17-127">Если уже установлена Python, можно использовать tooinstall PIP-адрес пакета все клиентские библиотеки hello в существующих Python 2.7 или в среде Python 3.3 +.</span><span class="sxs-lookup"><span data-stu-id="6be17-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="6be17-128">Это загружает пакеты hello из hello [индекс пакета Python] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="6be17-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="6be17-129">Могут потребоваться права администратора:</span><span class="sxs-lookup"><span data-stu-id="6be17-129">You may need administrator rights:</span></span>

* <span data-ttu-id="6be17-130">Linux и MacOS, используют hello `sudo` команды: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="6be17-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="6be17-131">В Windows откройте окно командной строки или окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="6be17-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="6be17-132">Вы можете установить каждую библиотеку отдельно для каждой службы Azure:</span><span class="sxs-lookup"><span data-stu-id="6be17-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="6be17-133">Предварительный просмотр пакетов можно установить с помощью hello `--pre` флаг:</span><span class="sxs-lookup"><span data-stu-id="6be17-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="6be17-134">Можно также установить набор библиотек Azure в одной строке с помощью hello `azure` мета пакета.</span><span class="sxs-lookup"><span data-stu-id="6be17-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="6be17-135">Здравствуйте, так как не все пакеты в этом пакете meta публикуются как стабильная еще, `azure` мета пакет находится на стадии предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="6be17-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="6be17-136">Тем не менее hello основные пакеты с точки зрения качества и полноту кода можно считать «устойчивым» в данный момент</span><span class="sxs-lookup"><span data-stu-id="6be17-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="6be17-137">Соответствующая отметка будет добавлена как можно скорее и синхронно с другими языками.</span><span class="sxs-lookup"><span data-stu-id="6be17-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="6be17-138">До тех пор мы не планируем каких-либо значительных изменений.</span><span class="sxs-lookup"><span data-stu-id="6be17-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="6be17-139">Так как это предварительная версия, необходимы toouse hello `--pre` флаг:</span><span class="sxs-lookup"><span data-stu-id="6be17-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="6be17-140">или напрямую:</span><span class="sxs-lookup"><span data-stu-id="6be17-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="6be17-141">Получение дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="6be17-141">Getting More Packages</span></span>
<span data-ttu-id="6be17-142">Hello [индекс пакета Python] [ Python Package Index] (PyPI) имеет широкий выбор библиотек Python.</span><span class="sxs-lookup"><span data-stu-id="6be17-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="6be17-143">Если выбрано tooinstall дистрибутив будет уже обладаете почти всеми hello интересных bits для различных сценариев из tooTechnical разработка web вычислениям.</span><span class="sxs-lookup"><span data-stu-id="6be17-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="6be17-144">Средства Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6be17-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="6be17-145">[Инструменты Python для Visual Studio][Инструменты Python для Visual Studio] (PTVS) представляют собой бесплатный подключаемый модуль с открытым исходным кодом от корпорации Майкрософт, который превращает Visual Studio в полноценную интегрированную среду разработки Python.</span><span class="sxs-lookup"><span data-stu-id="6be17-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="6be17-147">Использование средств PTVS необязательно, однако рекомендуется, поскольку они обеспечивают поддержку Python и веб-проектов/решений, отладку, профилирование, интерактивное окно, редактирование шаблонов и Intellisense.</span><span class="sxs-lookup"><span data-stu-id="6be17-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="6be17-148">PTVS также позволяет легко toodeploy tooMicrosoft Azure, поддержка развертывания слишком[облачные службы](cloud-services/cloud-services-python-ptvs.md) и [веб-сайтов](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="6be17-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="6be17-149">PTVS работает с установленными экземплярами Visual Studio 2013, 2015 или 2017.</span><span class="sxs-lookup"><span data-stu-id="6be17-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="6be17-150">Документацию, скачиваемые материалы и обсуждения см. на странице [Инструменты Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="6be17-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="6be17-151">Сценарии Python Azure для Linux и MacOS</span><span class="sxs-lookup"><span data-stu-id="6be17-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="6be17-152">Для Linux и MacOS существуют следующие основные поддерживаемые сценарии Azure:</span><span class="sxs-lookup"><span data-stu-id="6be17-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="6be17-153">Использование служб Azure с помощью hello клиентские библиотеки для Python</span><span class="sxs-lookup"><span data-stu-id="6be17-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="6be17-154">Запуск приложения на виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="6be17-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="6be17-155">Разработка и публикации tooAzure веб-сайтов с помощью Git</span><span class="sxs-lookup"><span data-stu-id="6be17-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="6be17-156">первый сценарий Hello позволяет tooauthor многофункциональных веб-приложений, которые использовать hello Azure PaaS функции, такие как [хранилище больших двоичных объектов](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [хранилище очередей](storage/queues/storage-python-how-to-use-queue-storage.md), [хранилище таблиц](cosmos-db/table-storage-how-to-use-python.md) т. д. через Pythonic оболочки для hello интерфейсы API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="6be17-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="6be17-157">Они совершенно одинаково работают в Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="6be17-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="6be17-158">Можно также использовать эти клиентские библиотеки из вашей локальной машины или виртуальной машины Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="6be17-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="6be17-159">Для сценария hello виртуальных Машин просто запустить виртуальную Машину Linux по вашему выбору (Ubuntu, CentOS, Suse) и выполнения и управлять вам нравится.</span><span class="sxs-lookup"><span data-stu-id="6be17-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="6be17-160">Например, можно запустить [IPython] [ IPython] REPL ПК на компьютере Windows, Mac и Linux и точки вашего браузера tooa Linux или Windows запущена виртуальная машина мультипроцессорном hello IPython Engine в Azure.</span><span class="sxs-lookup"><span data-stu-id="6be17-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="6be17-161">Сведения о том, как tooset ВМ Linux, см. hello [создать виртуальную машину под управлением Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) учебника.</span><span class="sxs-lookup"><span data-stu-id="6be17-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="6be17-162">С помощью Git развертывания, можно разрабатывать веб-приложения Python и опубликовать его tooan веб-сайта Azure из любой операционной системы.</span><span class="sxs-lookup"><span data-stu-id="6be17-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="6be17-163">При выполнении отправки к tooAzure репозитория, он автоматически создает виртуальную среду и pip устанавливает необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="6be17-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="6be17-164">Дополнительные сведения о разработке и публикации веб-сайтов Azure см. в разделе hello учебники по [Создание веб-сайтов с Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Создание веб-сайтов с бутылка](app-service-web/web-sites-python-create-deploy-bottle-app.md), и [Создание веб-сайтов с Термосе](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="6be17-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="6be17-165">Дополнительные сведения об использовании совместимой с WSGI платформы см. в статье [Настройка Python в веб-приложениях службы приложений Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6be17-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="6be17-166">Дополнительные ресурсы и программное обеспечение:</span><span class="sxs-lookup"><span data-stu-id="6be17-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="6be17-167">Пакет SDK Azure для Python — ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="6be17-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="6be17-168">Пакет SDK Azure для Python — GitHub</span><span class="sxs-lookup"><span data-stu-id="6be17-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="6be17-169">Официальные примеры кода Azure для Python</span><span class="sxs-lookup"><span data-stu-id="6be17-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="6be17-170">[Распространяемая среда аналитики Python][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6be17-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="6be17-171">[Распространяемый набор Enthought Python][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6be17-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="6be17-172">[Распространяемый набор ActiveState Python][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6be17-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="6be17-173">[SciPy — набор научных библиотек Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="6be17-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="6be17-174">[NumPy — библиотека числовых значений для Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="6be17-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="6be17-175">[Django Project — зрелая веб-платформа или CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="6be17-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="6be17-176">[IPython — расширенное использование REPL и Notebook для Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="6be17-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="6be17-177">[Средства Python для Visual Studio на сайте GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="6be17-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="6be17-178">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="6be17-178">Python Developer Center</span></span>](/develop/python/)

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
