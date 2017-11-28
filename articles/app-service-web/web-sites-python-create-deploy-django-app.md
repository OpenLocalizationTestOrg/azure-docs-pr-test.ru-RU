---
title: "Создание веб-приложений с помощью Django в Azure"
description: "Учебник, в котором вы ознакомитесь с запуском веб-приложения Python в веб-приложениях службы приложений Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="a3709-103">Создание веб-приложений с помощью Django в Azure</span><span class="sxs-lookup"><span data-stu-id="a3709-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="a3709-104">В этом учебнике описывается, как работать с языком Python в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a3709-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="a3709-105">Служба веб-приложений предоставляет ограниченное бесплатное размещение приложений, а также возможности их быстрого развертывания и использования языка Python.</span><span class="sxs-lookup"><span data-stu-id="a3709-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="a3709-106">По мере роста приложения его можно перевести на платное размещение и интегрировать во все другие службы Azure.</span><span class="sxs-lookup"><span data-stu-id="a3709-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="a3709-107">Вы создадите приложение с помощью веб-платформы Django (см. другие версии этого руководства для веб-платформ [Flask](web-sites-python-create-deploy-flask-app.md) и [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="a3709-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="a3709-108">Вы можете создать веб-приложение из Azure Marketplace, настроить развертывание Git и локально клонировать репозиторий.</span><span class="sxs-lookup"><span data-stu-id="a3709-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="a3709-109">Затем вы сможете запускать приложение локально, вносить изменения, фиксировать и отправлять их в Azure.</span><span class="sxs-lookup"><span data-stu-id="a3709-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="a3709-110">В этом учебнике показано, как выполнить вышеуказанные действия в Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="a3709-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="a3709-111">Если вы хотите приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="a3709-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a3709-112">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="a3709-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a3709-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a3709-113">Prerequisites</span></span>
* <span data-ttu-id="a3709-114">Windows, Mac или Linux</span><span class="sxs-lookup"><span data-stu-id="a3709-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="a3709-115">Python 2.7 или 3.4</span><span class="sxs-lookup"><span data-stu-id="a3709-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="a3709-116">setuptools, pip, virtualenv (только для Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="a3709-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="a3709-117">Git</span><span class="sxs-lookup"><span data-stu-id="a3709-117">Git</span></span>
* <span data-ttu-id="a3709-118">[средствами Python для Visual Studio][средствами Python для Visual Studio] (PTVS) (необязательно).</span><span class="sxs-lookup"><span data-stu-id="a3709-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="a3709-119">**Примечание.** Публикация TFS в настоящее время для проектов Python не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="a3709-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="a3709-120">Windows</span><span class="sxs-lookup"><span data-stu-id="a3709-120">Windows</span></span>
<span data-ttu-id="a3709-121">Если у вас еще не установлен Python 2.7 или 3.4 (32-разрядная версия), рекомендуется сначала установить [пакет SDK для Azure для Python 2.7] или [пакет SDK для Azure для Python 3.4] с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="a3709-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="a3709-122">При этом выполняется установка 32-разрядной версии Python (для установки на хост-компьютерах Azure), setuptools, pip, virtualenv, и т. д.</span><span class="sxs-lookup"><span data-stu-id="a3709-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="a3709-123">Python также можно скачать с веб-сайта [python.org].</span><span class="sxs-lookup"><span data-stu-id="a3709-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="a3709-124">Для Git рекомендуется использовать [Git для Windows] или [GitHub для Windows].</span><span class="sxs-lookup"><span data-stu-id="a3709-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="a3709-125">При использовании Visual Studio можно использовать интегрированную поддержку Git.</span><span class="sxs-lookup"><span data-stu-id="a3709-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="a3709-126">Мы также рекомендуем установить [инструменты Python 2.2 для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="a3709-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="a3709-127">Это необязательно, но, если у вас есть [Visual Studio], например бесплатная версия Visual Studio Community 2013 или Visual Studio Express 2013 для Web, вы получите отличную интегрированную среду разработки Python.</span><span class="sxs-lookup"><span data-stu-id="a3709-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="a3709-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="a3709-128">Mac/Linux</span></span>
<span data-ttu-id="a3709-129">У вас должны быть установлены Python и Git. Убедитесь, что у вас установлена версия Python 2.7 или 3.4.</span><span class="sxs-lookup"><span data-stu-id="a3709-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="a3709-130">Создание веб-приложения на портале</span><span class="sxs-lookup"><span data-stu-id="a3709-130">Web App Creation on Portal</span></span>
<span data-ttu-id="a3709-131">Первым делом нужно создать веб-приложение на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3709-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="a3709-132">Войдите на портал Azure и нажмите кнопку **СОЗДАТЬ** в нижнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="a3709-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="a3709-133">В поле поиска введите "python".</span><span class="sxs-lookup"><span data-stu-id="a3709-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="a3709-134">В результатах поиска выберите **Django** (издатель — PTVS), а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a3709-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="a3709-135">Настройте новое приложение Django, например создайте новый план службы приложений и новую группу ресурсов для него.</span><span class="sxs-lookup"><span data-stu-id="a3709-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="a3709-136">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a3709-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="a3709-137">Настройте публикацию Git для вновь созданного веб-приложения, следуя инструкциям из статьи [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a3709-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="a3709-138">Обзор приложений</span><span class="sxs-lookup"><span data-stu-id="a3709-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="a3709-139">Содержимое репозитория Git</span><span class="sxs-lookup"><span data-stu-id="a3709-139">Git repository contents</span></span>
<span data-ttu-id="a3709-140">Ниже приведен обзор файлов, которые можно найти в исходном репозитории Git. Мы клонируем его в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="a3709-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="a3709-141">Основные источники для приложения.</span><span class="sxs-lookup"><span data-stu-id="a3709-141">Main sources for the application.</span></span> <span data-ttu-id="a3709-142">Состоит из 3 страниц (index, about, contact) с макетом главной страницы.</span><span class="sxs-lookup"><span data-stu-id="a3709-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="a3709-143">Использует такое статическое содержимое и сценарии, как bootstrap, jquery, modernizr и respond.</span><span class="sxs-lookup"><span data-stu-id="a3709-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="a3709-144">Поддержка локального сервера управления и разработки.</span><span class="sxs-lookup"><span data-stu-id="a3709-144">Local management and development server support.</span></span> <span data-ttu-id="a3709-145">Используется для локального запуска приложения, синхронизации базы данных и т. д.</span><span class="sxs-lookup"><span data-stu-id="a3709-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="a3709-146">База данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a3709-146">Default database.</span></span> <span data-ttu-id="a3709-147">Содержит таблицы, необходимые для выполнения приложения, но не содержит пользователей (синхронизируйте базу данных, чтобы создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="a3709-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="a3709-148">Файлы проекта для использования со [средствами Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="a3709-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="a3709-149">Прокси-сервер IIS для виртуальных сред и поддержки удаленной отладки PTVS.</span><span class="sxs-lookup"><span data-stu-id="a3709-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="a3709-150">Внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="a3709-150">External packages needed by this application.</span></span> <span data-ttu-id="a3709-151">Сценарий развертывания установит пакеты, указанные в этом файле, с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="a3709-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="a3709-152">Файлы конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="a3709-152">IIS configuration files.</span></span> <span data-ttu-id="a3709-153">Сценарий развертывания использует соответствующий web.x.y.config и скопирует его с именем web.config.</span><span class="sxs-lookup"><span data-stu-id="a3709-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="a3709-154">Дополнительные файлы — настройка развертывания</span><span class="sxs-lookup"><span data-stu-id="a3709-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="a3709-155">Дополнительные файлы — среда выполнения Python</span><span class="sxs-lookup"><span data-stu-id="a3709-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="a3709-156">Дополнительные файлы на сервере</span><span class="sxs-lookup"><span data-stu-id="a3709-156">Additional files on server</span></span>
<span data-ttu-id="a3709-157">Некоторые файлы размещены на сервере, но не добавляются в репозиторий git.</span><span class="sxs-lookup"><span data-stu-id="a3709-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="a3709-158">Такие файлы создаются с помощью сценария развертывания.</span><span class="sxs-lookup"><span data-stu-id="a3709-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="a3709-159">Файл конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="a3709-159">IIS configuration file.</span></span> <span data-ttu-id="a3709-160">Создается из файла web.x.y.config при каждом развертывании.</span><span class="sxs-lookup"><span data-stu-id="a3709-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="a3709-161">Виртуальная среда Python.</span><span class="sxs-lookup"><span data-stu-id="a3709-161">Python virtual environment.</span></span> <span data-ttu-id="a3709-162">Создается при развертывании, если совместимая виртуальная среда еще не создана для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3709-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="a3709-163">Пакеты, указанные в файле requirements.txt, устанавливаются с помощью pip. Однако если они уже установлены, pip не будет выполнять установку.</span><span class="sxs-lookup"><span data-stu-id="a3709-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="a3709-164">В следующих 3 разделах описывается разработка веб-приложения в 3 разных средах:</span><span class="sxs-lookup"><span data-stu-id="a3709-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="a3709-165">Windows, со средствами Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3709-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="a3709-166">Windows с командной строкой;</span><span class="sxs-lookup"><span data-stu-id="a3709-166">Windows, with command line</span></span>
* <span data-ttu-id="a3709-167">Mac и Linux с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="a3709-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="a3709-168">Развертывание веб-приложений — Windows — средства Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3709-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="a3709-169">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="a3709-169">Clone the repository</span></span>
<span data-ttu-id="a3709-170">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a3709-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="a3709-171">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a3709-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="a3709-172">Откройте файл решения (SLN-файл), который содержится в корневой папке репозитория.</span><span class="sxs-lookup"><span data-stu-id="a3709-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="a3709-173">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="a3709-173">Create virtual environment</span></span>
<span data-ttu-id="a3709-174">Теперь мы создадим виртуальную среду для локальной разработки веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="a3709-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="a3709-175">Щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add Virtual Environment...** (Добавить виртуальную среду...).</span><span class="sxs-lookup"><span data-stu-id="a3709-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="a3709-176">Убедитесь, что имя среды — `env`.</span><span class="sxs-lookup"><span data-stu-id="a3709-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="a3709-177">Выберите базовый интерпретатор.</span><span class="sxs-lookup"><span data-stu-id="a3709-177">Select the base interpreter.</span></span> <span data-ttu-id="a3709-178">Убедитесь, что используется та же версия Python, которая выбрана для веб-приложения (в файле runtime.txt или в колонке **Параметры приложения** веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="a3709-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="a3709-179">Убедитесь, что установлен флажок для скачивания и установки пакетов.</span><span class="sxs-lookup"><span data-stu-id="a3709-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="a3709-180">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a3709-180">Click **Create**.</span></span> <span data-ttu-id="a3709-181">Таким образом будет создана виртуальная среда и установлены зависимости из файла requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="a3709-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="a3709-182">Создание суперпользователя</span><span class="sxs-lookup"><span data-stu-id="a3709-182">Create a superuser</span></span>
<span data-ttu-id="a3709-183">В базе данных, которая содержится в приложении, не определен суперпользователь.</span><span class="sxs-lookup"><span data-stu-id="a3709-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="a3709-184">Чтобы использовать функции входа в приложение или интерфейс администрирования Django (если вы решили включить его), необходимо будет создать суперпользователя.</span><span class="sxs-lookup"><span data-stu-id="a3709-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="a3709-185">Выполните эту команду в командной строке в папке проекта:</span><span class="sxs-lookup"><span data-stu-id="a3709-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="a3709-186">Следуйте указаниям, чтобы задать имя пользователя, пароль и т. д.</span><span class="sxs-lookup"><span data-stu-id="a3709-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="a3709-187">Запуск страницы с помощью сервера разработки</span><span class="sxs-lookup"><span data-stu-id="a3709-187">Run using development server</span></span>
<span data-ttu-id="a3709-188">Нажмите клавишу F5, чтобы начать отладку, и браузер автоматически откроет страницу, запущенную локально.</span><span class="sxs-lookup"><span data-stu-id="a3709-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="a3709-189">Можно установить точки останова в источниках, использовать окна контрольных значений и т. д. Дополнительные сведения о различных функциях см. в [документации по средствам Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="a3709-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="a3709-190">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="a3709-190">Make changes</span></span>
<span data-ttu-id="a3709-191">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="a3709-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="a3709-192">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="a3709-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="a3709-193">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="a3709-193">Install more packages</span></span>
<span data-ttu-id="a3709-194">Зависимости приложений могут не ограничиваться Python и Django.</span><span class="sxs-lookup"><span data-stu-id="a3709-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="a3709-195">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="a3709-195">You can install additional packages using pip.</span></span> <span data-ttu-id="a3709-196">Чтобы установить пакет, щелкните правой кнопкой мыши в виртуальной среде и выберите **Установить пакет Python**.</span><span class="sxs-lookup"><span data-stu-id="a3709-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="a3709-197">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине и другим службам Azure, введите `azure`:</span><span class="sxs-lookup"><span data-stu-id="a3709-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="a3709-198">Щелкните правой кнопкой мыши в виртуальной среде и выберите **Создать файл requirements.txt** , чтобы обновить файл requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="a3709-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="a3709-199">Затем сохраните внесенные в этот файл изменения в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="a3709-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="a3709-200">Развернуть в Azure</span><span class="sxs-lookup"><span data-stu-id="a3709-200">Deploy to Azure</span></span>
<span data-ttu-id="a3709-201">Чтобы запустить развертывание, щелкните **Синхронизировать** или **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="a3709-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="a3709-202">При синхронизации выполняется как принудительная отправка, так и применение по запросу.</span><span class="sxs-lookup"><span data-stu-id="a3709-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="a3709-203">Первое развертывание может занять некоторое время, необходимое для создания виртуальной среды, установку пакетов и т. д.</span><span class="sxs-lookup"><span data-stu-id="a3709-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="a3709-204">В Visual Studio не отображается ход выполнения развертывания.</span><span class="sxs-lookup"><span data-stu-id="a3709-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="a3709-205">Сведения о том, как можно просмотреть результат, см. в разделе [Устранение неполадок — развертывание](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="a3709-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="a3709-206">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="a3709-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="a3709-207">Разработка веб-приложения — Windows — командная строка</span><span class="sxs-lookup"><span data-stu-id="a3709-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="a3709-208">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="a3709-208">Clone the repository</span></span>
<span data-ttu-id="a3709-209">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure, а затем добавьте репозиторий Azure в качестве удаленного.</span><span class="sxs-lookup"><span data-stu-id="a3709-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="a3709-210">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a3709-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="a3709-211">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="a3709-211">Create virtual environment</span></span>
<span data-ttu-id="a3709-212">Давайте создадим новую виртуальную среду для разработки (не добавляйте ее в репозиторий).</span><span class="sxs-lookup"><span data-stu-id="a3709-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="a3709-213">Виртуальные среды на языке Python нельзя перемещать, поэтому каждому разработчику, работающему над приложением, будет необходимо создать такую среду локально.</span><span class="sxs-lookup"><span data-stu-id="a3709-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="a3709-214">Убедитесь, что используется та же версия Python, которая выбрана для веб-приложения (в файле runtime.txt или в колонке "Параметры приложения" веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="a3709-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="a3709-215">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="a3709-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="a3709-216">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="a3709-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="a3709-217">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="a3709-217">Install any external packages required by your application.</span></span> <span data-ttu-id="a3709-218">Чтобы установить пакеты в своей виртуальной среде, вы можете использовать файл requirements.txt в корне репозитория:</span><span class="sxs-lookup"><span data-stu-id="a3709-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="a3709-219">Создание суперпользователя</span><span class="sxs-lookup"><span data-stu-id="a3709-219">Create a superuser</span></span>
<span data-ttu-id="a3709-220">В базе данных, которая содержится в приложении, не определен суперпользователь.</span><span class="sxs-lookup"><span data-stu-id="a3709-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="a3709-221">Чтобы использовать функции входа в приложение или интерфейс администрирования Django (если вы решили включить его), необходимо будет создать суперпользователя.</span><span class="sxs-lookup"><span data-stu-id="a3709-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="a3709-222">Выполните эту команду в командной строке в папке проекта:</span><span class="sxs-lookup"><span data-stu-id="a3709-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="a3709-223">Следуйте указаниям, чтобы задать имя пользователя, пароль и т. д.</span><span class="sxs-lookup"><span data-stu-id="a3709-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="a3709-224">Запуск страницы с помощью сервера разработки</span><span class="sxs-lookup"><span data-stu-id="a3709-224">Run using development server</span></span>
<span data-ttu-id="a3709-225">Вы можете запустить приложение на сервере разработки с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="a3709-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="a3709-226">В консоли отобразится URL-адрес и порт, который прослушивает сервер:</span><span class="sxs-lookup"><span data-stu-id="a3709-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="a3709-227">Далее откройте браузер и введите этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a3709-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="a3709-228">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="a3709-228">Make changes</span></span>
<span data-ttu-id="a3709-229">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="a3709-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="a3709-230">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="a3709-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="a3709-231">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="a3709-231">Install more packages</span></span>
<span data-ttu-id="a3709-232">Зависимости приложений могут не ограничиваться Python и Django.</span><span class="sxs-lookup"><span data-stu-id="a3709-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="a3709-233">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="a3709-233">You can install additional packages using pip.</span></span> <span data-ttu-id="a3709-234">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине, а также другим службам Azure, введите:</span><span class="sxs-lookup"><span data-stu-id="a3709-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="a3709-235">Обязательно обновите файл requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="a3709-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="a3709-236">Примените изменения:</span><span class="sxs-lookup"><span data-stu-id="a3709-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="a3709-237">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="a3709-237">Deploy to Azure</span></span>
<span data-ttu-id="a3709-238">Чтобы запустить развертывание, принудительно отправьте эти изменения в Azure:</span><span class="sxs-lookup"><span data-stu-id="a3709-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="a3709-239">Отобразятся выходные данные сценария развертывания, а также создание виртуальной среды, установку пакетов, и создание файла web.config.</span><span class="sxs-lookup"><span data-stu-id="a3709-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="a3709-240">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="a3709-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="a3709-241">Разработка веб-приложения — Mac/Linux — командная строка</span><span class="sxs-lookup"><span data-stu-id="a3709-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="a3709-242">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="a3709-242">Clone the repository</span></span>
<span data-ttu-id="a3709-243">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure, а затем добавьте репозиторий Azure в качестве удаленного.</span><span class="sxs-lookup"><span data-stu-id="a3709-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="a3709-244">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a3709-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="a3709-245">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="a3709-245">Create virtual environment</span></span>
<span data-ttu-id="a3709-246">Давайте создадим новую виртуальную среду для разработки (не добавляйте ее в репозиторий).</span><span class="sxs-lookup"><span data-stu-id="a3709-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="a3709-247">Виртуальные среды на языке Python нельзя перемещать, поэтому каждому разработчику, работающему над приложением, будет необходимо создать такую среду локально.</span><span class="sxs-lookup"><span data-stu-id="a3709-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="a3709-248">Убедитесь, что используется та же версия Python, которая выбрана для веб-приложения (в файле runtime.txt или в колонке "Параметры приложения" веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="a3709-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="a3709-249">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="a3709-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="a3709-250">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="a3709-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="a3709-251">или</span><span class="sxs-lookup"><span data-stu-id="a3709-251">or</span></span>

    pyvenv env

<span data-ttu-id="a3709-252">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="a3709-252">Install any external packages required by your application.</span></span> <span data-ttu-id="a3709-253">Чтобы установить пакеты в своей виртуальной среде, вы можете использовать файл requirements.txt в корне репозитория:</span><span class="sxs-lookup"><span data-stu-id="a3709-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="a3709-254">Создание суперпользователя</span><span class="sxs-lookup"><span data-stu-id="a3709-254">Create a superuser</span></span>
<span data-ttu-id="a3709-255">В базе данных, которая содержится в приложении, не определен суперпользователь.</span><span class="sxs-lookup"><span data-stu-id="a3709-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="a3709-256">Чтобы использовать функции входа в приложение или интерфейс администрирования Django (если вы решили включить его), необходимо будет создать суперпользователя.</span><span class="sxs-lookup"><span data-stu-id="a3709-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="a3709-257">Выполните эту команду в командной строке в папке проекта:</span><span class="sxs-lookup"><span data-stu-id="a3709-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="a3709-258">Следуйте указаниям, чтобы задать имя пользователя, пароль и т. д.</span><span class="sxs-lookup"><span data-stu-id="a3709-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="a3709-259">Запуск страницы с помощью сервера разработки</span><span class="sxs-lookup"><span data-stu-id="a3709-259">Run using development server</span></span>
<span data-ttu-id="a3709-260">Вы можете запустить приложение на сервере разработки с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="a3709-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="a3709-261">В консоли отобразится URL-адрес и порт, который прослушивает сервер:</span><span class="sxs-lookup"><span data-stu-id="a3709-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="a3709-262">Далее откройте браузер и введите этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a3709-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="a3709-263">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="a3709-263">Make changes</span></span>
<span data-ttu-id="a3709-264">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="a3709-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="a3709-265">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="a3709-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="a3709-266">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="a3709-266">Install more packages</span></span>
<span data-ttu-id="a3709-267">Зависимости приложений могут не ограничиваться Python и Django.</span><span class="sxs-lookup"><span data-stu-id="a3709-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="a3709-268">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="a3709-268">You can install additional packages using pip.</span></span> <span data-ttu-id="a3709-269">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине, а также другим службам Azure, введите:</span><span class="sxs-lookup"><span data-stu-id="a3709-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="a3709-270">Обязательно обновите файл requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="a3709-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="a3709-271">Примените изменения:</span><span class="sxs-lookup"><span data-stu-id="a3709-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="a3709-272">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="a3709-272">Deploy to Azure</span></span>
<span data-ttu-id="a3709-273">Чтобы запустить развертывание, принудительно отправьте эти изменения в Azure:</span><span class="sxs-lookup"><span data-stu-id="a3709-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="a3709-274">Отобразятся выходные данные сценария развертывания, а также создание виртуальной среды, установку пакетов, и создание файла web.config.</span><span class="sxs-lookup"><span data-stu-id="a3709-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="a3709-275">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="a3709-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="a3709-276">Устранение неполадок — установка пакета</span><span class="sxs-lookup"><span data-stu-id="a3709-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="a3709-277">Устранение неполадок — виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="a3709-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="a3709-278">Устранение неполадок — статические файлы</span><span class="sxs-lookup"><span data-stu-id="a3709-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="a3709-279">Django использует концепцию сбора статических файлов.</span><span class="sxs-lookup"><span data-stu-id="a3709-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="a3709-280">Согласно этой концепции все статические файлы извлекаются из исходных расположений и копируются в одну папку.</span><span class="sxs-lookup"><span data-stu-id="a3709-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="a3709-281">Для этого приложения они копируются в папку `/static`.</span><span class="sxs-lookup"><span data-stu-id="a3709-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="a3709-282">Это делается потому, что статические файлы могут поступать из различных приложений Django.</span><span class="sxs-lookup"><span data-stu-id="a3709-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="a3709-283">Например, статические файлы интерфейсов администратора Django находятся во вложенной папке библиотеки Django в виртуальной среде.</span><span class="sxs-lookup"><span data-stu-id="a3709-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="a3709-284">Статические файлы, определенные в этом приложении, находятся в папке `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="a3709-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="a3709-285">При использовании нескольких приложений Django статические файлы будут расположены в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="a3709-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="a3709-286">При запуске приложения в режиме отладки статические файлы обслуживаются из исходного расположения.</span><span class="sxs-lookup"><span data-stu-id="a3709-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="a3709-287">При запуске приложения в режиме выпуска статические файлы **не** обслуживаются.</span><span class="sxs-lookup"><span data-stu-id="a3709-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="a3709-288">За это отвечает веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="a3709-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="a3709-289">Для этого приложения IIS будет обслуживать статические файлы из папки `/static`.</span><span class="sxs-lookup"><span data-stu-id="a3709-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="a3709-290">Сбор статических файлов выполняется автоматически в ходе выполнения сценария развертывания, а файлы, собранные ранее, удаляются.</span><span class="sxs-lookup"><span data-stu-id="a3709-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="a3709-291">Это означает, что сбор выполняется при каждом развертывании. Это немного замедляет развертывание, но обеспечивает недоступность устаревших файлов во избежание потенциальных проблем безопасности.</span><span class="sxs-lookup"><span data-stu-id="a3709-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="a3709-292">Вот как можно пропустить сбор статических файлов для приложения Django:</span><span class="sxs-lookup"><span data-stu-id="a3709-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="a3709-293">Затем вам понадобится собрать файлы вручную на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="a3709-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="a3709-294">Удалите папку `\static` из `.gitignore` и добавьте ее в репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="a3709-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="a3709-295">Устранение неполадок — настройки</span><span class="sxs-lookup"><span data-stu-id="a3709-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="a3709-296">В `DjangoWebProject/settings.py`можно изменить различные параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="a3709-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="a3709-297">Для удобства разработчиков включен режим отладки.</span><span class="sxs-lookup"><span data-stu-id="a3709-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="a3709-298">Одним из положительных внешних эффектов является возможность просматривать образы и другое статическое содержимое во время локального выполнения без сбора статических файлов.</span><span class="sxs-lookup"><span data-stu-id="a3709-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="a3709-299">Чтобы отключить режим отладки, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a3709-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="a3709-300">Если режим отладки отключен, в значении параметра `ALLOWED_HOSTS` необходимо указать имя узла Azure.</span><span class="sxs-lookup"><span data-stu-id="a3709-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="a3709-301">Например:</span><span class="sxs-lookup"><span data-stu-id="a3709-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="a3709-302">Чтобы включить любой узел, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="a3709-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="a3709-303">На практике для переключения между режимами отладки и выпуска, а также получения имени узла можно выполнять более сложные задачи.</span><span class="sxs-lookup"><span data-stu-id="a3709-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="a3709-304">Вы можете задать переменные среды на странице **Настройка** портала Azure в разделе **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3709-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="a3709-305">Таким способом можно задать значения, которые не будут отображаться в исходном коде (строки подключения, пароли и т. д.), а также задать разные значения для Azure и локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="a3709-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="a3709-306">В файле `settings.py` можно запросить переменные среды с помощью `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="a3709-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="a3709-307">Использование базы данных</span><span class="sxs-lookup"><span data-stu-id="a3709-307">Using a Database</span></span>
<span data-ttu-id="a3709-308">В приложении содержится база данных sqlite.</span><span class="sxs-lookup"><span data-stu-id="a3709-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="a3709-309">Эту базу данных по умолчанию удобно использовать для разработки, так как она практически не требует настройки.</span><span class="sxs-lookup"><span data-stu-id="a3709-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="a3709-310">Эта база данных хранится в файле db.sqlite3 в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="a3709-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="a3709-311">Azure предоставляет службы баз данных, которые легко использовать в приложении Django.</span><span class="sxs-lookup"><span data-stu-id="a3709-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="a3709-312">В руководствах по использованию [базы данных SQL] и [MySQL] в приложении на платформе Django описываются шаги по созданию службы базы данных и изменению параметров базы данных в файле `DjangoWebProject/settings.py`. В этих руководствах также приводится список библиотек, которые необходимо установить.</span><span class="sxs-lookup"><span data-stu-id="a3709-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="a3709-313">Конечно, если вы предпочитаете управлять собственными серверами баз данных, это можно сделать с помощью виртуальных машин Windows или Linux, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="a3709-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="a3709-314">Интерфейс администрирования Django</span><span class="sxs-lookup"><span data-stu-id="a3709-314">Django Admin Interface</span></span>
<span data-ttu-id="a3709-315">Как только вы начнете создавать модели, вам необходимо будет заполнять базу данных данными.</span><span class="sxs-lookup"><span data-stu-id="a3709-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="a3709-316">Интерфейс администрирования Django позволяет с легкостью добавлять и изменять содержимое в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="a3709-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="a3709-317">Код интерфейса администрирования закомментирован в исходном коде приложения, но он четко помечен, поэтому его можно легко включить (ищите слово "admin").</span><span class="sxs-lookup"><span data-stu-id="a3709-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="a3709-318">Включив код, синхронизируйте базу данных, запустите приложение и перейдите к `/admin`.</span><span class="sxs-lookup"><span data-stu-id="a3709-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3709-319">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3709-319">Next Steps</span></span>
<span data-ttu-id="a3709-320">Используйте следующие ссылки, чтобы узнать больше о средствах Django и Python для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3709-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="a3709-321">[Документация по Django]</span><span class="sxs-lookup"><span data-stu-id="a3709-321">[Django Documentation]</span></span>
* <span data-ttu-id="a3709-322">[документации по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a3709-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="a3709-323">Дополнительную информацию об использовании базы данных SQL и MySQL см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="a3709-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="a3709-324">[Использование Django и MySQL в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a3709-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="a3709-325">[Использование Django и базы данных SQL в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a3709-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="a3709-326">Дополнительную информацию можно найти в [Центре разработчика Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="a3709-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a3709-327">Изменения</span><span class="sxs-lookup"><span data-stu-id="a3709-327">What's changed</span></span>
* <span data-ttu-id="a3709-328">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a3709-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Использование Django и MySQL в Azure с помощью инструментов Python для Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Использование Django и базы данных SQL в Azure с помощью инструментов Python для Visual Studio]: web-sites-python-ptvs-django-sql.md
[базы данных SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[пакет SDK для Azure для Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[пакет SDK для Azure для Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git для Windows]: http://msysgit.github.io/
[GitHub для Windows]: https://windows.github.com/
[средствами Python для Visual Studio]: http://aka.ms/ptvs
[инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[документации по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs
[Документация по Django]: https://www.djangoproject.com/
