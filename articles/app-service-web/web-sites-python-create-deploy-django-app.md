---
title: "aaaCreating веб-приложений с Django в Azure"
description: "Учебник, в котором представлены toorunning Python веб-приложения в веб-приложениях службы приложений Azure."
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
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="198a2-103">Создание веб-приложений с помощью Django в Azure</span><span class="sxs-lookup"><span data-stu-id="198a2-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="198a2-104">В данном учебнике как tooget к выполнению Python на [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="198a2-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="198a2-105">Служба веб-приложений предоставляет ограниченное бесплатное размещение приложений, а также возможности их быстрого развертывания и использования языка Python.</span><span class="sxs-lookup"><span data-stu-id="198a2-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="198a2-106">Здравствуйте, по мере роста приложения, можно переключить toopaid размещение и также можно интегрировать со всеми другими службами Azure.</span><span class="sxs-lookup"><span data-stu-id="198a2-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="198a2-107">Вы создадите приложения с помощью веб-платформа Django hello (см. другие версии этого учебника, чтобы [термосе](web-sites-python-create-deploy-flask-app.md) и [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="198a2-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="198a2-108">Будет создать веб-приложение hello из hello Azure Marketplace, Настройка развертывания Git и клонировать репозиторий hello локально.</span><span class="sxs-lookup"><span data-stu-id="198a2-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="198a2-109">Затем можно будет запустить приложение hello локально, внести изменения, зафиксируйте и отправьте их tooAzure.</span><span class="sxs-lookup"><span data-stu-id="198a2-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="198a2-110">Здравствуйте учебника показано, как toodo это в Windows или Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="198a2-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="198a2-111">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="198a2-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="198a2-112">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="198a2-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="198a2-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="198a2-113">Prerequisites</span></span>
* <span data-ttu-id="198a2-114">Windows, Mac или Linux</span><span class="sxs-lookup"><span data-stu-id="198a2-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="198a2-115">Python 2.7 или 3.4</span><span class="sxs-lookup"><span data-stu-id="198a2-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="198a2-116">setuptools, pip, virtualenv (только для Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="198a2-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="198a2-117">Git</span><span class="sxs-lookup"><span data-stu-id="198a2-117">Git</span></span>
* <span data-ttu-id="198a2-118">[средствами Python для Visual Studio][средствами Python для Visual Studio] (PTVS) (необязательно).</span><span class="sxs-lookup"><span data-stu-id="198a2-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="198a2-119">**Примечание.** Публикация TFS в настоящее время для проектов Python не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="198a2-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="198a2-120">Windows</span><span class="sxs-lookup"><span data-stu-id="198a2-120">Windows</span></span>
<span data-ttu-id="198a2-121">Если у вас еще не установлен Python 2.7 или 3.4 (32-разрядная версия), рекомендуется сначала установить [пакет SDK для Azure для Python 2.7] или [пакет SDK для Azure для Python 3.4] с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="198a2-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="198a2-122">При этом устанавливаются hello 32-разрядной версии Python дублирует, pip, virtualenv, (32-разрядных Python —, установленных на компьютерах hello Azure узлов) и т. д.</span><span class="sxs-lookup"><span data-stu-id="198a2-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="198a2-123">Python также можно скачать с веб-сайта [python.org].</span><span class="sxs-lookup"><span data-stu-id="198a2-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="198a2-124">Для Git рекомендуется использовать [Git для Windows] или [GitHub для Windows].</span><span class="sxs-lookup"><span data-stu-id="198a2-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="198a2-125">При использовании Visual Studio, можно использовать поддержку hello интеграции Git.</span><span class="sxs-lookup"><span data-stu-id="198a2-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="198a2-126">Мы также рекомендуем установить [инструменты Python 2.2 для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="198a2-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="198a2-127">Это не обязательно, но если у вас [Visual Studio], включая hello освободить Visual Studio Community 2013 или Visual Studio Express 2013 для Web, а затем это даст значительные среду IDE Python.</span><span class="sxs-lookup"><span data-stu-id="198a2-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="198a2-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="198a2-128">Mac/Linux</span></span>
<span data-ttu-id="198a2-129">У вас должны быть установлены Python и Git. Убедитесь, что у вас установлена версия Python 2.7 или 3.4.</span><span class="sxs-lookup"><span data-stu-id="198a2-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="198a2-130">Создание веб-приложения на портале</span><span class="sxs-lookup"><span data-stu-id="198a2-130">Web App Creation on Portal</span></span>
<span data-ttu-id="198a2-131">Hello первым шагом при создании приложения является toocreate hello веб-приложения через hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="198a2-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="198a2-132">Войдите на портал Azure hello и щелкните hello **NEW** кнопки в левом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="198a2-133">В поле поиска hello введите «python».</span><span class="sxs-lookup"><span data-stu-id="198a2-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="198a2-134">В результатах поиска hello, выберите **Django** (опубликованное PTVS), затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="198a2-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="198a2-135">Настройте hello новый Django приложение, таких как создание нового плана служб приложений и новую группу ресурсов для него.</span><span class="sxs-lookup"><span data-stu-id="198a2-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="198a2-136">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="198a2-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="198a2-137">Настроить публикацию Git для только что созданный веб-приложения в соответствии с инструкциями hello в [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="198a2-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="198a2-138">Обзор приложений</span><span class="sxs-lookup"><span data-stu-id="198a2-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="198a2-139">Содержимое репозитория Git</span><span class="sxs-lookup"><span data-stu-id="198a2-139">Git repository contents</span></span>
<span data-ttu-id="198a2-140">Ниже приведен обзор hello файлов, которые можно найти в hello исходный репозиторий Git, который мы будем клонировать в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

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

<span data-ttu-id="198a2-141">Основными источниками для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-141">Main sources for hello application.</span></span> <span data-ttu-id="198a2-142">Состоит из 3 страниц (index, about, contact) с макетом главной страницы.</span><span class="sxs-lookup"><span data-stu-id="198a2-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="198a2-143">Использует такое статическое содержимое и сценарии, как bootstrap, jquery, modernizr и respond.</span><span class="sxs-lookup"><span data-stu-id="198a2-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="198a2-144">Поддержка локального сервера управления и разработки.</span><span class="sxs-lookup"><span data-stu-id="198a2-144">Local management and development server support.</span></span> <span data-ttu-id="198a2-145">Используйте это приложение hello toorun локально, синхронизацию базы данных hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="198a2-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="198a2-146">База данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="198a2-146">Default database.</span></span> <span data-ttu-id="198a2-147">Включает необходимые таблицы hello для toorun приложения hello, но не содержит всех пользователей (синхронизации toocreate hello базы данных пользователя).</span><span class="sxs-lookup"><span data-stu-id="198a2-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="198a2-148">Файлы проекта для использования со [средствами Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="198a2-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="198a2-149">Прокси-сервер IIS для виртуальных сред и поддержки удаленной отладки PTVS.</span><span class="sxs-lookup"><span data-stu-id="198a2-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="198a2-150">Внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="198a2-150">External packages needed by this application.</span></span> <span data-ttu-id="198a2-151">скрипт развертывания Hello будет pip hello пакетов установки, перечисленные в этом файле.</span><span class="sxs-lookup"><span data-stu-id="198a2-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="198a2-152">Файлы конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="198a2-152">IIS configuration files.</span></span> <span data-ttu-id="198a2-153">скрипт развертывания Hello будет использовать соответствующий web.x.y.config hello и скопируйте его в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="198a2-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="198a2-154">Дополнительные файлы — настройка развертывания</span><span class="sxs-lookup"><span data-stu-id="198a2-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="198a2-155">Дополнительные файлы — среда выполнения Python</span><span class="sxs-lookup"><span data-stu-id="198a2-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="198a2-156">Дополнительные файлы на сервере</span><span class="sxs-lookup"><span data-stu-id="198a2-156">Additional files on server</span></span>
<span data-ttu-id="198a2-157">Некоторые файлы на сервере hello существует, но не добавляются toohello репозитории.</span><span class="sxs-lookup"><span data-stu-id="198a2-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="198a2-158">Эти отчеты создаются с hello сценария развертывания.</span><span class="sxs-lookup"><span data-stu-id="198a2-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="198a2-159">Файл конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="198a2-159">IIS configuration file.</span></span> <span data-ttu-id="198a2-160">Создается из файла web.x.y.config при каждом развертывании.</span><span class="sxs-lookup"><span data-stu-id="198a2-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="198a2-161">Виртуальная среда Python.</span><span class="sxs-lookup"><span data-stu-id="198a2-161">Python virtual environment.</span></span> <span data-ttu-id="198a2-162">Создан во время развертывания, если совместимый виртуальной среды не существует на веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="198a2-163">Пакеты, перечисленные в requirements.txt являются pip установлен, но pip пропустит установки, если hello пакеты уже установлены.</span><span class="sxs-lookup"><span data-stu-id="198a2-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="198a2-164">Hello следующие 3 рассматриваются как tooproceed с hello веб-разработки приложений в разделе 3 различных сред:</span><span class="sxs-lookup"><span data-stu-id="198a2-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="198a2-165">Windows, со средствами Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="198a2-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="198a2-166">Windows с командной строкой;</span><span class="sxs-lookup"><span data-stu-id="198a2-166">Windows, with command line</span></span>
* <span data-ttu-id="198a2-167">Mac и Linux с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="198a2-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="198a2-168">Развертывание веб-приложений — Windows — средства Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="198a2-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="198a2-169">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="198a2-169">Clone hello repository</span></span>
<span data-ttu-id="198a2-170">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="198a2-171">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="198a2-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="198a2-172">Привет открыть файл решения (SLN-файл), включенный в корне репозитория hello hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="198a2-173">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="198a2-173">Create virtual environment</span></span>
<span data-ttu-id="198a2-174">Теперь мы создадим виртуальную среду для локальной разработки веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="198a2-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="198a2-175">Щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add Virtual Environment...** (Добавить виртуальную среду...).</span><span class="sxs-lookup"><span data-stu-id="198a2-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="198a2-176">Убедитесь, что имя hello среды hello `env`.</span><span class="sxs-lookup"><span data-stu-id="198a2-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="198a2-177">Выберите базовый интерпретатор hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-177">Select hello base interpreter.</span></span> <span data-ttu-id="198a2-178">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="198a2-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="198a2-179">Убедитесь, что параметр hello toodownload и установки пакетов.</span><span class="sxs-lookup"><span data-stu-id="198a2-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="198a2-180">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="198a2-180">Click **Create**.</span></span> <span data-ttu-id="198a2-181">Это создание виртуальной среды hello и установка зависимостей, перечисленных в requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="198a2-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="198a2-182">Создание суперпользователя</span><span class="sxs-lookup"><span data-stu-id="198a2-182">Create a superuser</span></span>
<span data-ttu-id="198a2-183">Hello базы данных, входящий в состав приложения hello не поддерживает любой суперпользователя определен.</span><span class="sxs-lookup"><span data-stu-id="198a2-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="198a2-184">Порядок toouse hello вход функциональных возможностей приложения hello или интерфейса администратора Django hello (Если вы решите tooenable его), вам потребуется toocreate привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="198a2-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="198a2-185">Выполните это из hello командной строки из вашей папки проекта.</span><span class="sxs-lookup"><span data-stu-id="198a2-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="198a2-186">Выполните запросы tooset hello hello-имя пользователя, пароль и т. д.</span><span class="sxs-lookup"><span data-stu-id="198a2-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="198a2-187">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="198a2-187">Run using development server</span></span>
<span data-ttu-id="198a2-188">Нажмите клавишу F5 toostart отладки и веб-браузере откроется автоматически toohello страница выполняется локально.</span><span class="sxs-lookup"><span data-stu-id="198a2-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="198a2-189">Можно установить точки останова в hello источников, окна контрольных значений используйте hello и т. д. . В разделе hello [средства Python для Visual Studio документации] Дополнительные сведения о hello различных функций.</span><span class="sxs-lookup"><span data-stu-id="198a2-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="198a2-190">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="198a2-190">Make changes</span></span>
<span data-ttu-id="198a2-191">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="198a2-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="198a2-192">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="198a2-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="198a2-193">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="198a2-193">Install more packages</span></span>
<span data-ttu-id="198a2-194">Зависимости приложений могут не ограничиваться Python и Django.</span><span class="sxs-lookup"><span data-stu-id="198a2-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="198a2-195">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="198a2-195">You can install additional packages using pip.</span></span> <span data-ttu-id="198a2-196">tooinstall пакета, щелкните правой кнопкой мыши виртуальную среду hello и выберите пункт **установить пакет Python**.</span><span class="sxs-lookup"><span data-stu-id="198a2-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="198a2-197">Например, пакет Azure SDK для Python, который предоставляет вам доступ tooAzure хранилище, service bus и другим службам Azure ввести hello tooinstall `azure`:</span><span class="sxs-lookup"><span data-stu-id="198a2-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="198a2-198">Щелкните правой кнопкой мыши в виртуальной среде hello и выберите **создания requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="198a2-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="198a2-199">Зафиксируйте hello изменения toorequirements.txt toohello репозитории.</span><span class="sxs-lookup"><span data-stu-id="198a2-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="198a2-200">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="198a2-200">Deploy tooAzure</span></span>
<span data-ttu-id="198a2-201">Щелкните tootrigger развертывания **синхронизации** или **Push**.</span><span class="sxs-lookup"><span data-stu-id="198a2-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="198a2-202">При синхронизации выполняется как принудительная отправка, так и применение по запросу.</span><span class="sxs-lookup"><span data-stu-id="198a2-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="198a2-203">Hello первого развертывания может потребоваться некоторое время, как он создаст в виртуальной среде, пакетов установки, и т. д.</span><span class="sxs-lookup"><span data-stu-id="198a2-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="198a2-204">Visual Studio не показывает ход выполнения развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="198a2-205">При желании вывода hello tooreview разделе hello на [Устранение неполадок - развертывания](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="198a2-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="198a2-206">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="198a2-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="198a2-207">Разработка веб-приложения — Windows — командная строка</span><span class="sxs-lookup"><span data-stu-id="198a2-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="198a2-208">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="198a2-208">Clone hello repository</span></span>
<span data-ttu-id="198a2-209">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный.</span><span class="sxs-lookup"><span data-stu-id="198a2-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="198a2-210">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="198a2-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="198a2-211">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="198a2-211">Create virtual environment</span></span>
<span data-ttu-id="198a2-212">Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория).</span><span class="sxs-lookup"><span data-stu-id="198a2-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="198a2-213">Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.</span><span class="sxs-lookup"><span data-stu-id="198a2-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="198a2-214">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello колонку параметров приложения из веб-приложения hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="198a2-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="198a2-215">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="198a2-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="198a2-216">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="198a2-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="198a2-217">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="198a2-217">Install any external packages required by your application.</span></span> <span data-ttu-id="198a2-218">Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:</span><span class="sxs-lookup"><span data-stu-id="198a2-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="198a2-219">Создание суперпользователя</span><span class="sxs-lookup"><span data-stu-id="198a2-219">Create a superuser</span></span>
<span data-ttu-id="198a2-220">Hello базы данных, входящий в состав приложения hello не поддерживает любой суперпользователя определен.</span><span class="sxs-lookup"><span data-stu-id="198a2-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="198a2-221">Порядок toouse hello вход функциональных возможностей приложения hello или интерфейса администратора Django hello (Если вы решите tooenable его), вам потребуется toocreate привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="198a2-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="198a2-222">Выполните это из hello командной строки из вашей папки проекта.</span><span class="sxs-lookup"><span data-stu-id="198a2-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="198a2-223">Выполните запросы tooset hello hello-имя пользователя, пароль и т. д.</span><span class="sxs-lookup"><span data-stu-id="198a2-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="198a2-224">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="198a2-224">Run using development server</span></span>
<span data-ttu-id="198a2-225">Приложение hello под сервером разработки можно запустить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="198a2-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="198a2-226">Hello консоли появится URL-адрес hello и прослушивает порт hello server:</span><span class="sxs-lookup"><span data-stu-id="198a2-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="198a2-227">Откройте браузер toothat URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="198a2-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="198a2-228">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="198a2-228">Make changes</span></span>
<span data-ttu-id="198a2-229">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="198a2-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="198a2-230">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="198a2-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="198a2-231">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="198a2-231">Install more packages</span></span>
<span data-ttu-id="198a2-232">Зависимости приложений могут не ограничиваться Python и Django.</span><span class="sxs-lookup"><span data-stu-id="198a2-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="198a2-233">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="198a2-233">You can install additional packages using pip.</span></span> <span data-ttu-id="198a2-234">Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:</span><span class="sxs-lookup"><span data-stu-id="198a2-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="198a2-235">Убедитесь, что requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="198a2-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="198a2-236">Применить изменения hello:</span><span class="sxs-lookup"><span data-stu-id="198a2-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="198a2-237">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="198a2-237">Deploy tooAzure</span></span>
<span data-ttu-id="198a2-238">tootrigger развертывание принудительной hello изменяет tooAzure:</span><span class="sxs-lookup"><span data-stu-id="198a2-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="198a2-239">Вы увидите выходные данные hello hello скрипт развертывания, включая создание виртуальной среды, установки пакетов, создания файла конфигурации Web.config.</span><span class="sxs-lookup"><span data-stu-id="198a2-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="198a2-240">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="198a2-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="198a2-241">Разработка веб-приложения — Mac/Linux — командная строка</span><span class="sxs-lookup"><span data-stu-id="198a2-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="198a2-242">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="198a2-242">Clone hello repository</span></span>
<span data-ttu-id="198a2-243">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный.</span><span class="sxs-lookup"><span data-stu-id="198a2-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="198a2-244">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="198a2-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="198a2-245">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="198a2-245">Create virtual environment</span></span>
<span data-ttu-id="198a2-246">Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория).</span><span class="sxs-lookup"><span data-stu-id="198a2-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="198a2-247">Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.</span><span class="sxs-lookup"><span data-stu-id="198a2-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="198a2-248">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello колонку параметров приложения из веб-приложения hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="198a2-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="198a2-249">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="198a2-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="198a2-250">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="198a2-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="198a2-251">или</span><span class="sxs-lookup"><span data-stu-id="198a2-251">or</span></span>

    pyvenv env

<span data-ttu-id="198a2-252">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="198a2-252">Install any external packages required by your application.</span></span> <span data-ttu-id="198a2-253">Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:</span><span class="sxs-lookup"><span data-stu-id="198a2-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="198a2-254">Создание суперпользователя</span><span class="sxs-lookup"><span data-stu-id="198a2-254">Create a superuser</span></span>
<span data-ttu-id="198a2-255">Hello базы данных, входящий в состав приложения hello не поддерживает любой суперпользователя определен.</span><span class="sxs-lookup"><span data-stu-id="198a2-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="198a2-256">Порядок toouse hello вход функциональных возможностей приложения hello или интерфейса администратора Django hello (Если вы решите tooenable его), вам потребуется toocreate привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="198a2-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="198a2-257">Выполните это из hello командной строки из вашей папки проекта.</span><span class="sxs-lookup"><span data-stu-id="198a2-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="198a2-258">Выполните запросы tooset hello hello-имя пользователя, пароль и т. д.</span><span class="sxs-lookup"><span data-stu-id="198a2-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="198a2-259">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="198a2-259">Run using development server</span></span>
<span data-ttu-id="198a2-260">Приложение hello под сервером разработки можно запустить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="198a2-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="198a2-261">Hello консоли появится URL-адрес hello и прослушивает порт hello server:</span><span class="sxs-lookup"><span data-stu-id="198a2-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="198a2-262">Откройте браузер toothat URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="198a2-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="198a2-263">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="198a2-263">Make changes</span></span>
<span data-ttu-id="198a2-264">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="198a2-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="198a2-265">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="198a2-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="198a2-266">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="198a2-266">Install more packages</span></span>
<span data-ttu-id="198a2-267">Зависимости приложений могут не ограничиваться Python и Django.</span><span class="sxs-lookup"><span data-stu-id="198a2-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="198a2-268">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="198a2-268">You can install additional packages using pip.</span></span> <span data-ttu-id="198a2-269">Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:</span><span class="sxs-lookup"><span data-stu-id="198a2-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="198a2-270">Убедитесь, что requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="198a2-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="198a2-271">Применить изменения hello:</span><span class="sxs-lookup"><span data-stu-id="198a2-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="198a2-272">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="198a2-272">Deploy tooAzure</span></span>
<span data-ttu-id="198a2-273">tootrigger развертывание принудительной hello изменяет tooAzure:</span><span class="sxs-lookup"><span data-stu-id="198a2-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="198a2-274">Вы увидите выходные данные hello hello скрипт развертывания, включая создание виртуальной среды, установки пакетов, создания файла конфигурации Web.config.</span><span class="sxs-lookup"><span data-stu-id="198a2-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="198a2-275">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="198a2-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="198a2-276">Устранение неполадок — установка пакета</span><span class="sxs-lookup"><span data-stu-id="198a2-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="198a2-277">Устранение неполадок — виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="198a2-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="198a2-278">Устранение неполадок — статические файлы</span><span class="sxs-lookup"><span data-stu-id="198a2-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="198a2-279">Django имеет концепции hello сбора статических файлов.</span><span class="sxs-lookup"><span data-stu-id="198a2-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="198a2-280">Это занимает все статические файлы hello из своих исходных расположений и копирует их в одну папку tooa.</span><span class="sxs-lookup"><span data-stu-id="198a2-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="198a2-281">Для этого приложения, они копируются слишком`/static`.</span><span class="sxs-lookup"><span data-stu-id="198a2-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="198a2-282">Это делается потому, что статические файлы могут поступать из различных приложений Django.</span><span class="sxs-lookup"><span data-stu-id="198a2-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="198a2-283">Например hello статические файлы из интерфейсов admin Django hello расположены во вложенной папке библиотеки Django в виртуальной среде hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="198a2-284">Статические файлы, определенные в этом приложении, находятся в папке `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="198a2-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="198a2-285">При использовании нескольких приложений Django статические файлы будут расположены в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="198a2-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="198a2-286">При запуске приложения hello в режиме отладки, приложение hello служит hello статические файлы из своих исходных расположений.</span><span class="sxs-lookup"><span data-stu-id="198a2-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="198a2-287">При запуске приложения hello в режиме выпуска, приложение hello выполняет **не** обрабатывать hello статические файлы.</span><span class="sxs-lookup"><span data-stu-id="198a2-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="198a2-288">Он несет hello hello tooserve файлов для hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="198a2-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="198a2-289">Для этого приложения IIS будет обслуживать hello статические файлы из `/static`.</span><span class="sxs-lookup"><span data-stu-id="198a2-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="198a2-290">Коллекция Hello статических файлов выполняется как часть скрипта развертывания hello, сняв ранее собранные файлы автоматически.</span><span class="sxs-lookup"><span data-stu-id="198a2-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="198a2-291">Это означает, что hello сборка выполняется для всех развертываний, замедляя развертывания немного, но гарантирует, что устаревшие файлы не будут доступны, как избежать является потенциальной угрозой безопасности.</span><span class="sxs-lookup"><span data-stu-id="198a2-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="198a2-292">Если нужно tooskip коллекцию статических файлов для приложения Django:</span><span class="sxs-lookup"><span data-stu-id="198a2-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="198a2-293">Затем вам потребуется коллекции hello toodo вручную на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="198a2-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="198a2-294">Затем удалите hello `\static` папку из `.gitignore` и добавьте его toohello репозитории.</span><span class="sxs-lookup"><span data-stu-id="198a2-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="198a2-295">Устранение неполадок — настройки</span><span class="sxs-lookup"><span data-stu-id="198a2-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="198a2-296">Можно изменить различные параметры для приложения hello в `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="198a2-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="198a2-297">Для удобства разработчиков включен режим отладки.</span><span class="sxs-lookup"><span data-stu-id="198a2-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="198a2-298">Хорошо побочным эффектом того, является будете иметь может toosee изображения и другие статическое содержимое, если выполняется локально, без необходимости toocollect статические файлы.</span><span class="sxs-lookup"><span data-stu-id="198a2-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="198a2-299">режим отладки toodisable:</span><span class="sxs-lookup"><span data-stu-id="198a2-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="198a2-300">При отключении отладки hello значение `ALLOWED_HOSTS` toobe потребностей обновить имя Azure узла tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="198a2-301">Например:</span><span class="sxs-lookup"><span data-stu-id="198a2-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="198a2-302">или tooenable любой:</span><span class="sxs-lookup"><span data-stu-id="198a2-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="198a2-303">На практике можно toodo что-нибудь более сложные toodeal с переключением между, отладки и выпуска режим и получение имени узла hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="198a2-304">Можно задать переменные среды через портал Azure hello **Настройка** страницы в hello **параметры приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="198a2-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="198a2-305">Это может быть полезно для задания значений, что может потребоваться не tooappear в источниках hello (строки подключения, пароли, и т. д.), или что tooset по-разному между Azure и локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="198a2-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="198a2-306">В `settings.py`, можно запросить с помощью переменных среды hello `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="198a2-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="198a2-307">Использование базы данных</span><span class="sxs-lookup"><span data-stu-id="198a2-307">Using a Database</span></span>
<span data-ttu-id="198a2-308">Hello базы данных, которая входит в состав приложения hello является базой данных sqlite.</span><span class="sxs-lookup"><span data-stu-id="198a2-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="198a2-309">Это toouse базы данных по умолчанию удобный и полезно для разработки, поскольку оно требует практически никакой дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="198a2-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="198a2-310">Hello база данных хранится в файле db.sqlite3 hello в папке проекта hello.</span><span class="sxs-lookup"><span data-stu-id="198a2-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="198a2-311">Azure предоставляет базы данных служб, которые являются просто toouse из Django приложения.</span><span class="sxs-lookup"><span data-stu-id="198a2-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="198a2-312">Учебники по использованию [базы данных SQL] и [MySQL] из приложения Django Показать шаги hello необходимые toocreate hello базы данных службы, измените параметры базы данных hello в `DjangoWebProject/settings.py`и hello tooinstall необходимые библиотеки.</span><span class="sxs-lookup"><span data-stu-id="198a2-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="198a2-313">Конечно Если вы предпочитаете toomanage серверах баз данных, можно сделать с помощью Windows или Linux виртуальных машин, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="198a2-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="198a2-314">Интерфейс администрирования Django</span><span class="sxs-lookup"><span data-stu-id="198a2-314">Django Admin Interface</span></span>
<span data-ttu-id="198a2-315">После начала построения моделей, будет необходимо toopopulate hello базы данных некоторые данными.</span><span class="sxs-lookup"><span data-stu-id="198a2-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="198a2-316">Простой способ toodo Добавление и изменение содержимого в интерактивном режиме — toouse hello Django администрирования интерфейс.</span><span class="sxs-lookup"><span data-stu-id="198a2-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="198a2-317">Код Hello для интерфейса администрирования hello закомментированы в источниках приложения hello, но он помечается, его можно легко включить (поиск «admin»).</span><span class="sxs-lookup"><span data-stu-id="198a2-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="198a2-318">После включения синхронизации базы данных hello, запустите приложение hello и перехода слишком`/admin`.</span><span class="sxs-lookup"><span data-stu-id="198a2-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="198a2-319">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="198a2-319">Next Steps</span></span>
<span data-ttu-id="198a2-320">Выполните эти ссылки toolearn Дополнительные сведения о Django и инструменты Python для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="198a2-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="198a2-321">[Документация по Django]</span><span class="sxs-lookup"><span data-stu-id="198a2-321">[Django Documentation]</span></span>
* <span data-ttu-id="198a2-322">[средства Python для Visual Studio документации]</span><span class="sxs-lookup"><span data-stu-id="198a2-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="198a2-323">Дополнительную информацию об использовании базы данных SQL и MySQL см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="198a2-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="198a2-324">[Использование Django и MySQL в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="198a2-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="198a2-325">[Использование Django и базы данных SQL в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="198a2-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="198a2-326">Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="198a2-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="198a2-327">Изменения</span><span class="sxs-lookup"><span data-stu-id="198a2-327">What's changed</span></span>
* <span data-ttu-id="198a2-328">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="198a2-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
[средства Python для Visual Studio документации]: http://aka.ms/ptvsdocs
[Документация по Django]: https://www.djangoproject.com/
