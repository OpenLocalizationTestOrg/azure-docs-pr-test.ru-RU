---
title: "Установка Python и пакета SDK — Azure"
description: "Узнайте, как установить Python и пакет SDK для использования с Azure."
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
ms.openlocfilehash: c9df4e1f7677b2ed10684f6f3c981f2abf64f171
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="installing-python-and-the-sdk"></a><span data-ttu-id="6b3cc-103">Установка Python и пакета SDK</span><span class="sxs-lookup"><span data-stu-id="6b3cc-103">Installing Python and the SDK</span></span>
<span data-ttu-id="6b3cc-104">Python легко устанавливается в Windows и поставляется предварительно установленным в Mac, Linux и [Bash для Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="6b3cc-104">Python is easy to set up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="6b3cc-105">В этом руководстве рассматривается установка и подготовка компьютера к использованию с Azure.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-the-python-azure-sdk"></a><span data-ttu-id="6b3cc-106">Новые возможности пакета Python Azure SDK</span><span class="sxs-lookup"><span data-stu-id="6b3cc-106">What's in the Python Azure SDK?</span></span>
<span data-ttu-id="6b3cc-107">Azure SDK для Python включает компоненты для разработки, развертывания приложений Python в Azure и управления ими.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="6b3cc-108">Пакет Azure SDK для Python включает следующие средства:</span><span class="sxs-lookup"><span data-stu-id="6b3cc-108">Specifically, the Azure SDK for Python includes the following:</span></span>

* <span data-ttu-id="6b3cc-109">**Библиотеки управления**.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-109">**Management libraries**.</span></span> <span data-ttu-id="6b3cc-110">Эти библиотеки классов предоставляют управляемые через интерфейс ресурсы Azure, такие как учетные записи хранения и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="6b3cc-111">**Библиотеки среды выполнения**.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-111">**Runtime libraries**.</span></span> <span data-ttu-id="6b3cc-112">Эти библиотеки классов предоставляют интерфейс для доступа к компонентам Azure, таким как хранилище и служебная шина.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="6b3cc-113">Какой вариант и какую версию Python использовать</span><span class="sxs-lookup"><span data-stu-id="6b3cc-113">Which Python and which version to use</span></span>
<span data-ttu-id="6b3cc-114">Доступно несколько видов интерпретаторов Python, например:</span><span class="sxs-lookup"><span data-stu-id="6b3cc-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="6b3cc-115">CPython — стандартный и наиболее часто используемый интерпретатор Python;</span><span class="sxs-lookup"><span data-stu-id="6b3cc-115">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="6b3cc-116">PyPy — быстродействующий аналог интерпретатора CPython;</span><span class="sxs-lookup"><span data-stu-id="6b3cc-116">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="6b3cc-117">IronPython — интерпретатор Python, работающий на базе .net/CLR;</span><span class="sxs-lookup"><span data-stu-id="6b3cc-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="6b3cc-118">Jython — интерпретатор Python, работающий на базе виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-118">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="6b3cc-119">**CPython** (версия 2.7 или 3.3 и выше) и PyPy 5.4.0 были протестированы и совместимы с пакетом SDK Azure для Python.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="6b3cc-120">Где можно получить Python?</span><span class="sxs-lookup"><span data-stu-id="6b3cc-120">Where to get Python?</span></span>
<span data-ttu-id="6b3cc-121">Существует несколько способов получить CPython:</span><span class="sxs-lookup"><span data-stu-id="6b3cc-121">There are several ways to get CPython:</span></span>

* <span data-ttu-id="6b3cc-122">непосредственно с сайта [www.python.org][www.python.org];</span><span class="sxs-lookup"><span data-stu-id="6b3cc-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="6b3cc-123">у известного поставщика дистрибутивов, например [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] или [www.activestate.com][www.activestate.com].</span><span class="sxs-lookup"><span data-stu-id="6b3cc-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="6b3cc-124">Построение из исходного кода!</span><span class="sxs-lookup"><span data-stu-id="6b3cc-124">Build from source!</span></span>

<span data-ttu-id="6b3cc-125">При отсутствии особой необходимости мы рекомендуем использовать первые два варианта.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-125">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="6b3cc-126">Установка пакета SDK в Windows, Linux и MacOS (только клиентские библиотеки)</span><span class="sxs-lookup"><span data-stu-id="6b3cc-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="6b3cc-127">Если вы уже установили Python, вы можете использовать pip для установки пакета всех клиентских библиотек в существующей среде Python 2.7 или Python 3.3+.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="6b3cc-128">При этом будут скачаны пакеты из [индекса пакетов Python][Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="6b3cc-128">This downloads the packages from the [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="6b3cc-129">Могут потребоваться права администратора:</span><span class="sxs-lookup"><span data-stu-id="6b3cc-129">You may need administrator rights:</span></span>

* <span data-ttu-id="6b3cc-130">В Linux и MacOS используйте команду `sudo`: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="6b3cc-131">В Windows откройте окно командной строки или окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="6b3cc-132">Вы можете установить каждую библиотеку отдельно для каждой службы Azure:</span><span class="sxs-lookup"><span data-stu-id="6b3cc-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install the latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="6b3cc-133">Предварительные версии пакетов можно установить с помощью флага `--pre` :</span><span class="sxs-lookup"><span data-stu-id="6b3cc-133">Preview packages can be installed using the `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only the latest Compute Management library
```

<span data-ttu-id="6b3cc-134">Набор библиотек Azure также можно установить одной строкой с помощью пакета метаданных `azure` .</span><span class="sxs-lookup"><span data-stu-id="6b3cc-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span> <span data-ttu-id="6b3cc-135">Так как не все пакеты в этом пакете метаданных публикуются как стабильные, то и сам пакет метаданных `azure` является предварительным.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="6b3cc-136">Однако основные пакеты уже можно считать "стабильными" с точки зрения качества и полноты кода.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="6b3cc-137">Соответствующая отметка будет добавлена как можно скорее и синхронно с другими языками.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="6b3cc-138">До тех пор мы не планируем каких-либо значительных изменений.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="6b3cc-139">Так как это предварительный выпуск, необходимо использовать флаг `--pre` :</span><span class="sxs-lookup"><span data-stu-id="6b3cc-139">Since it's a preview release, you need to use the `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="6b3cc-140">или напрямую:</span><span class="sxs-lookup"><span data-stu-id="6b3cc-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="6b3cc-141">Получение дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="6b3cc-141">Getting More Packages</span></span>
<span data-ttu-id="6b3cc-142">[Индекс пакета Python][Python Package Index] (PyPI) предлагает широкий выбор библиотек Python.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="6b3cc-143">Если вы решили установить дистрибутив, то получите основную часть нужного кода для самых различных сценариев — от веб-разработки до технических вычислений.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="6b3cc-144">Средства Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b3cc-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="6b3cc-145">[Инструменты Python для Visual Studio][Инструменты Python для Visual Studio] (PTVS) представляют собой бесплатный подключаемый модуль с открытым исходным кодом от корпорации Майкрософт, который превращает Visual Studio в полноценную интегрированную среду разработки Python.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="6b3cc-147">Использование средств PTVS необязательно, однако рекомендуется, поскольку они обеспечивают поддержку Python и веб-проектов/решений, отладку, профилирование, интерактивное окно, редактирование шаблонов и Intellisense.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="6b3cc-148">PTVS также упрощает развертывание в Microsoft Azure с поддержкой для развертывания в [облачных службах](cloud-services/cloud-services-python-ptvs.md) и на [веб-сайтах](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="6b3cc-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="6b3cc-149">PTVS работает с установленными экземплярами Visual Studio 2013, 2015 или 2017.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="6b3cc-150">Документацию, скачиваемые материалы и обсуждения см. на странице [Инструменты Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="6b3cc-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="6b3cc-151">Сценарии Python Azure для Linux и MacOS</span><span class="sxs-lookup"><span data-stu-id="6b3cc-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="6b3cc-152">Для Linux и MacOS существуют следующие основные поддерживаемые сценарии Azure:</span><span class="sxs-lookup"><span data-stu-id="6b3cc-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="6b3cc-153">Использование служб Azure с помощью клиентских библиотек для Python</span><span class="sxs-lookup"><span data-stu-id="6b3cc-153">Consuming Azure Services by using the client libraries for Python</span></span>
2. <span data-ttu-id="6b3cc-154">Запуск приложения на виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="6b3cc-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="6b3cc-155">Разработка и публикация на веб-сайтах Azure с помощью Git</span><span class="sxs-lookup"><span data-stu-id="6b3cc-155">Developing and publishing to Azure Websites using Git</span></span>

<span data-ttu-id="6b3cc-156">Первый сценарий позволяет создавать полнофункциональные веб-приложения, использующие преимущества возможностей Azure PaaS, такие как [хранилище BLOB-объектов](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [хранилище очередей](storage/queues/storage-python-how-to-use-queue-storage.md), [Хранилище таблиц](cosmos-db/table-storage-how-to-use-python.md) и т. д., через оболочки Pythonic для интерфейсов REST API Azure.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for the Azure REST APIs.</span></span> <span data-ttu-id="6b3cc-157">Они совершенно одинаково работают в Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="6b3cc-158">Можно также использовать эти клиентские библиотеки из вашей локальной машины или виртуальной машины Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="6b3cc-159">При сценарии с виртуальной машиной вы просто запускаете выбранную виртуальную машину Linux (Ubuntu, CentOS, Suse), а затем выполняете нужные компоненты и управляете ими.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="6b3cc-160">В качестве примера можно запустить REPL или Notebook [IPython][IPython] на компьютере Windows, Mac либо Linux и указать в браузере многопроцессорную виртуальную машину Linux или Windows с запущенной подсистемой IPython в Azure.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span></span>

<span data-ttu-id="6b3cc-161">Дополнительные сведения о способах настройки виртуальной машины Linux см. в руководстве [Создание виртуальной машины Linux с помощью Azure CLI](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b3cc-161">For information on how to set up a Linux VM, see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="6b3cc-162">С помощью развертывания Git можно разработать веб-приложение Python и опубликовать его на веб-сайте Azure из любой операционной системы.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-162">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span></span>  <span data-ttu-id="6b3cc-163">При принудительной отправке репозитория в Azure автоматически создается виртуальная среда, а pip устанавливает требуемые пакеты.</span><span class="sxs-lookup"><span data-stu-id="6b3cc-163">When you push your repository to Azure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="6b3cc-164">Дополнительные сведения о разработке и публикации Веб-сайтов Azure см. в руководствах по [созданию Веб-сайтов с помощью Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md) и [Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="6b3cc-164">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="6b3cc-165">Дополнительные сведения об использовании совместимой с WSGI платформы см. в статье [Настройка Python в веб-приложениях службы приложений Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6b3cc-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="6b3cc-166">Дополнительные ресурсы и программное обеспечение:</span><span class="sxs-lookup"><span data-stu-id="6b3cc-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="6b3cc-167">Пакет SDK Azure для Python — ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="6b3cc-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="6b3cc-168">Пакет SDK Azure для Python — GitHub</span><span class="sxs-lookup"><span data-stu-id="6b3cc-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="6b3cc-169">Официальные примеры кода Azure для Python</span><span class="sxs-lookup"><span data-stu-id="6b3cc-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="6b3cc-170">[Распространяемая среда аналитики Python][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6b3cc-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="6b3cc-171">[Распространяемый набор Enthought Python][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6b3cc-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="6b3cc-172">[Распространяемый набор ActiveState Python][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6b3cc-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="6b3cc-173">[SciPy — набор научных библиотек Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="6b3cc-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="6b3cc-174">[NumPy — библиотека числовых значений для Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="6b3cc-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="6b3cc-175">[Django Project — зрелая веб-платформа или CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="6b3cc-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="6b3cc-176">[IPython — расширенное использование REPL и Notebook для Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="6b3cc-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="6b3cc-177">[Средства Python для Visual Studio на сайте GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="6b3cc-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="6b3cc-178">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="6b3cc-178">Python Developer Center</span></span>](/develop/python/)

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
[Setting up a Linux VM via the Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How to use the Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
