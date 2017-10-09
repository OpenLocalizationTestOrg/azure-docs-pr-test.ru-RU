---
title: "aaaPython веб-приложений с бутылка в Azure"
description: "Учебник, в котором представлены toorunning Python веб-приложения в веб-приложениях службы приложений Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="adaeb-103">Создание веб-приложений с помощью Bottle в Azure</span><span class="sxs-lookup"><span data-stu-id="adaeb-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="adaeb-104">В данном учебнике как tooget была запущена Python в веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="adaeb-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="adaeb-105">Служба веб-приложений предоставляет ограниченное бесплатное размещение приложений, а также возможности их быстрого развертывания и использования языка Python.</span><span class="sxs-lookup"><span data-stu-id="adaeb-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="adaeb-106">Здравствуйте, по мере роста приложения, можно переключить toopaid размещение и также можно интегрировать со всеми другими службами Azure.</span><span class="sxs-lookup"><span data-stu-id="adaeb-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="adaeb-107">Вы создадите веб-приложения с помощью веб-платформа бутылка hello (см. другие версии этого учебника, чтобы [Django](web-sites-python-create-deploy-django-app.md) и [термосе](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="adaeb-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="adaeb-108">Будет создать веб-приложение hello из hello Azure Marketplace, Настройка развертывания Git и клонировать репозиторий hello локально.</span><span class="sxs-lookup"><span data-stu-id="adaeb-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="adaeb-109">Затем будет выполняться веб-приложение hello, внести изменения, зафиксируйте и отправьте их слишком[веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="adaeb-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="adaeb-110">Здравствуйте учебника показано, как toodo это в Windows или Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="adaeb-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="adaeb-111">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="adaeb-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="adaeb-112">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="adaeb-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="adaeb-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="adaeb-113">Prerequisites</span></span>
* <span data-ttu-id="adaeb-114">Windows, Mac или Linux</span><span class="sxs-lookup"><span data-stu-id="adaeb-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="adaeb-115">Python 2.7 или 3.4</span><span class="sxs-lookup"><span data-stu-id="adaeb-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="adaeb-116">setuptools, pip, virtualenv (только для Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="adaeb-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="adaeb-117">Git</span><span class="sxs-lookup"><span data-stu-id="adaeb-117">Git</span></span>
* <span data-ttu-id="adaeb-118">[инструменты Python 2.2 для Visual Studio][инструменты Python 2.2 для Visual Studio] (PTVS) (Примечание. Необязательный компонент.)</span><span class="sxs-lookup"><span data-stu-id="adaeb-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="adaeb-119">**Примечание.** Публикация TFS в настоящее время для проектов Python не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="adaeb-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="adaeb-120">Windows</span><span class="sxs-lookup"><span data-stu-id="adaeb-120">Windows</span></span>
<span data-ttu-id="adaeb-121">Если у вас еще не установлен Python 2.7 или 3.4 (32-разрядная версия), рекомендуется сначала установить [пакет SDK для Azure для Python 2.7] или [пакет SDK для Azure для Python 3.4] с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="adaeb-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="adaeb-122">При этом устанавливаются hello 32-разрядной версии Python дублирует, pip, virtualenv, (32-разрядных Python —, установленных на компьютерах hello Azure узлов) и т. д.</span><span class="sxs-lookup"><span data-stu-id="adaeb-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="adaeb-123">Python также можно скачать с веб-сайта [python.org].</span><span class="sxs-lookup"><span data-stu-id="adaeb-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="adaeb-124">Для Git рекомендуется использовать [Git для Windows] или [GitHub для Windows].</span><span class="sxs-lookup"><span data-stu-id="adaeb-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="adaeb-125">При использовании Visual Studio, можно использовать поддержку hello интеграции Git.</span><span class="sxs-lookup"><span data-stu-id="adaeb-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="adaeb-126">Мы также рекомендуем установить [инструменты Python 2.2 для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="adaeb-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="adaeb-127">Это не обязательно, но если у вас [Visual Studio], включая hello освободить Visual Studio Community 2013 или Visual Studio Express 2013 для Web, а затем это даст значительные среду IDE Python.</span><span class="sxs-lookup"><span data-stu-id="adaeb-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="adaeb-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="adaeb-128">Mac/Linux</span></span>
<span data-ttu-id="adaeb-129">У вас должны быть установлены Python и Git. Убедитесь, что у вас установлена версия Python 2.7 или 3.4.</span><span class="sxs-lookup"><span data-stu-id="adaeb-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="adaeb-130">Создание приложения Web на портале Azure hello</span><span class="sxs-lookup"><span data-stu-id="adaeb-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="adaeb-131">Hello первым шагом при создании приложения является toocreate hello веб-приложения через hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="adaeb-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="adaeb-132">Войдите на портал Azure hello и щелкните hello **NEW** кнопки в левом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="adaeb-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="adaeb-133">В поле поиска hello введите «python».</span><span class="sxs-lookup"><span data-stu-id="adaeb-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="adaeb-134">В результатах поиска hello, выберите **Bottle**, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="adaeb-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="adaeb-135">Настройте приложение новый бутылка hello, таких как создание нового плана служб приложений и новую группу ресурсов для него.</span><span class="sxs-lookup"><span data-stu-id="adaeb-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="adaeb-136">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="adaeb-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="adaeb-137">Настроить публикацию Git для только что созданный веб-приложения в соответствии с инструкциями hello в [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="adaeb-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="adaeb-138">Обзор приложений</span><span class="sxs-lookup"><span data-stu-id="adaeb-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="adaeb-139">Содержимое репозитория Git</span><span class="sxs-lookup"><span data-stu-id="adaeb-139">Git repository contents</span></span>
<span data-ttu-id="adaeb-140">Ниже приведен обзор hello файлов, которые можно найти в hello исходный репозиторий Git, который мы будем клонировать в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="adaeb-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="adaeb-141">Основными источниками для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="adaeb-141">Main sources for hello application.</span></span> <span data-ttu-id="adaeb-142">Состоит из 3 страниц (index, about, contact) с макетом главной страницы.</span><span class="sxs-lookup"><span data-stu-id="adaeb-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="adaeb-143">Использует такое статическое содержимое и сценарии, как bootstrap, jquery, modernizr и respond.</span><span class="sxs-lookup"><span data-stu-id="adaeb-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="adaeb-144">Поддержка локального сервера разработки.</span><span class="sxs-lookup"><span data-stu-id="adaeb-144">Local development server support.</span></span> <span data-ttu-id="adaeb-145">Используйте это приложение hello toorun локально.</span><span class="sxs-lookup"><span data-stu-id="adaeb-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="adaeb-146">Файлы проекта для использования со [средствами Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="adaeb-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="adaeb-147">Прокси-сервер IIS для виртуальных сред и поддержки удаленной отладки PTVS.</span><span class="sxs-lookup"><span data-stu-id="adaeb-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="adaeb-148">Внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="adaeb-148">External packages needed by this application.</span></span> <span data-ttu-id="adaeb-149">скрипт развертывания Hello будет pip hello пакетов установки, перечисленные в этом файле.</span><span class="sxs-lookup"><span data-stu-id="adaeb-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="adaeb-150">Файлы конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="adaeb-150">IIS configuration files.</span></span> <span data-ttu-id="adaeb-151">скрипт развертывания Hello будет использовать соответствующий web.x.y.config hello и скопируйте его в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="adaeb-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="adaeb-152">Дополнительные файлы — настройка развертывания</span><span class="sxs-lookup"><span data-stu-id="adaeb-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="adaeb-153">Дополнительные файлы — среда выполнения Python</span><span class="sxs-lookup"><span data-stu-id="adaeb-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="adaeb-154">Дополнительные файлы на сервере</span><span class="sxs-lookup"><span data-stu-id="adaeb-154">Additional files on server</span></span>
<span data-ttu-id="adaeb-155">Некоторые файлы на сервере hello существует, но не добавляются toohello репозитории.</span><span class="sxs-lookup"><span data-stu-id="adaeb-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="adaeb-156">Эти отчеты создаются с hello сценария развертывания.</span><span class="sxs-lookup"><span data-stu-id="adaeb-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="adaeb-157">Файл конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="adaeb-157">IIS configuration file.</span></span> <span data-ttu-id="adaeb-158">Создается из файла web.x.y.config при каждом развертывании.</span><span class="sxs-lookup"><span data-stu-id="adaeb-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="adaeb-159">Виртуальная среда Python.</span><span class="sxs-lookup"><span data-stu-id="adaeb-159">Python virtual environment.</span></span> <span data-ttu-id="adaeb-160">Создан во время развертывания, если совместимый виртуальной среды не существует на веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="adaeb-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="adaeb-161">Пакеты, перечисленные в requirements.txt являются pip установлен, но pip пропустит установки, если hello пакеты уже установлены.</span><span class="sxs-lookup"><span data-stu-id="adaeb-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="adaeb-162">Hello следующие 3 рассматриваются как tooproceed с hello веб-разработки приложений в разделе 3 различных сред:</span><span class="sxs-lookup"><span data-stu-id="adaeb-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="adaeb-163">Windows, со средствами Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="adaeb-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="adaeb-164">Windows с командной строкой;</span><span class="sxs-lookup"><span data-stu-id="adaeb-164">Windows, with command line</span></span>
* <span data-ttu-id="adaeb-165">Mac и Linux с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="adaeb-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="adaeb-166">Развертывание веб-приложений — Windows — инструменты Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="adaeb-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="adaeb-167">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="adaeb-167">Clone hello repository</span></span>
<span data-ttu-id="adaeb-168">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="adaeb-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="adaeb-169">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="adaeb-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="adaeb-170">Привет открыть файл решения (SLN-файл), включенный в корне репозитория hello hello.</span><span class="sxs-lookup"><span data-stu-id="adaeb-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="adaeb-171">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="adaeb-171">Create virtual environment</span></span>
<span data-ttu-id="adaeb-172">Теперь мы создадим виртуальную среду для локальной разработки веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="adaeb-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="adaeb-173">Щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add Virtual Environment...** (Добавить виртуальную среду...).</span><span class="sxs-lookup"><span data-stu-id="adaeb-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="adaeb-174">Убедитесь, что имя hello среды hello `env`.</span><span class="sxs-lookup"><span data-stu-id="adaeb-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="adaeb-175">Выберите базовый интерпретатор hello.</span><span class="sxs-lookup"><span data-stu-id="adaeb-175">Select hello base interpreter.</span></span> <span data-ttu-id="adaeb-176">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="adaeb-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="adaeb-177">Убедитесь, что параметр hello toodownload и установки пакетов.</span><span class="sxs-lookup"><span data-stu-id="adaeb-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="adaeb-178">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="adaeb-178">Click **Create**.</span></span> <span data-ttu-id="adaeb-179">Это создание виртуальной среды hello и установка зависимостей, перечисленных в requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="adaeb-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="adaeb-180">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="adaeb-180">Run using development server</span></span>
<span data-ttu-id="adaeb-181">Нажмите клавишу F5 toostart отладки и веб-браузере откроется автоматически toohello страница выполняется локально.</span><span class="sxs-lookup"><span data-stu-id="adaeb-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="adaeb-182">Можно установить точки останова в hello источников, окна контрольных значений используйте hello и т. д. . В разделе hello [средства Python для Visual Studio документации] Дополнительные сведения о hello различных функций.</span><span class="sxs-lookup"><span data-stu-id="adaeb-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="adaeb-183">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="adaeb-183">Make changes</span></span>
<span data-ttu-id="adaeb-184">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="adaeb-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="adaeb-185">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="adaeb-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="adaeb-186">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="adaeb-186">Install more packages</span></span>
<span data-ttu-id="adaeb-187">Зависимости приложений могут не ограничиваться Python и Bottle.</span><span class="sxs-lookup"><span data-stu-id="adaeb-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="adaeb-188">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="adaeb-188">You can install additional packages using pip.</span></span> <span data-ttu-id="adaeb-189">tooinstall пакета, щелкните правой кнопкой мыши виртуальную среду hello и выберите пункт **установить пакет Python**.</span><span class="sxs-lookup"><span data-stu-id="adaeb-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="adaeb-190">Например, пакет Azure SDK для Python, который предоставляет вам доступ tooAzure хранилище, service bus и другим службам Azure ввести hello tooinstall `azure`:</span><span class="sxs-lookup"><span data-stu-id="adaeb-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="adaeb-191">Щелкните правой кнопкой мыши в виртуальной среде hello и выберите **создания requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="adaeb-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="adaeb-192">Зафиксируйте hello изменения toorequirements.txt toohello репозитории.</span><span class="sxs-lookup"><span data-stu-id="adaeb-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="adaeb-193">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="adaeb-193">Deploy tooAzure</span></span>
<span data-ttu-id="adaeb-194">Щелкните tootrigger развертывания **синхронизации** или **Push**.</span><span class="sxs-lookup"><span data-stu-id="adaeb-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="adaeb-195">При синхронизации выполняется как принудительная отправка, так и применение по запросу.</span><span class="sxs-lookup"><span data-stu-id="adaeb-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="adaeb-196">Hello первого развертывания может потребоваться некоторое время, как он создаст в виртуальной среде, пакетов установки, и т. д.</span><span class="sxs-lookup"><span data-stu-id="adaeb-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="adaeb-197">Visual Studio не показывает ход выполнения развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="adaeb-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="adaeb-198">При желании вывода hello tooreview разделе hello на [Устранение неполадок - развертывания](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="adaeb-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="adaeb-199">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="adaeb-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="adaeb-200">Разработка веб-приложения — Windows — командная строка</span><span class="sxs-lookup"><span data-stu-id="adaeb-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="adaeb-201">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="adaeb-201">Clone hello repository</span></span>
<span data-ttu-id="adaeb-202">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный.</span><span class="sxs-lookup"><span data-stu-id="adaeb-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="adaeb-203">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="adaeb-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="adaeb-204">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="adaeb-204">Create virtual environment</span></span>
<span data-ttu-id="adaeb-205">Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория).</span><span class="sxs-lookup"><span data-stu-id="adaeb-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="adaeb-206">Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.</span><span class="sxs-lookup"><span data-stu-id="adaeb-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="adaeb-207">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello колонку параметров приложения для веб-приложения hello портал Azure)</span><span class="sxs-lookup"><span data-stu-id="adaeb-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="adaeb-208">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="adaeb-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="adaeb-209">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="adaeb-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="adaeb-210">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="adaeb-210">Install any external packages required by your application.</span></span> <span data-ttu-id="adaeb-211">Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:</span><span class="sxs-lookup"><span data-stu-id="adaeb-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="adaeb-212">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="adaeb-212">Run using development server</span></span>
<span data-ttu-id="adaeb-213">Приложение hello под сервером разработки можно запустить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="adaeb-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="adaeb-214">Hello консоли появится URL-адрес hello и прослушивает порт hello server:</span><span class="sxs-lookup"><span data-stu-id="adaeb-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="adaeb-215">Откройте браузер toothat URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="adaeb-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="adaeb-216">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="adaeb-216">Make changes</span></span>
<span data-ttu-id="adaeb-217">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="adaeb-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="adaeb-218">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="adaeb-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="adaeb-219">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="adaeb-219">Install more packages</span></span>
<span data-ttu-id="adaeb-220">Зависимости приложений могут не ограничиваться Python и Bottle.</span><span class="sxs-lookup"><span data-stu-id="adaeb-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="adaeb-221">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="adaeb-221">You can install additional packages using pip.</span></span> <span data-ttu-id="adaeb-222">Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:</span><span class="sxs-lookup"><span data-stu-id="adaeb-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="adaeb-223">Убедитесь, что requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="adaeb-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="adaeb-224">Применить изменения hello:</span><span class="sxs-lookup"><span data-stu-id="adaeb-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="adaeb-225">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="adaeb-225">Deploy tooAzure</span></span>
<span data-ttu-id="adaeb-226">tootrigger развертывание принудительной hello изменяет tooAzure:</span><span class="sxs-lookup"><span data-stu-id="adaeb-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="adaeb-227">Вы увидите выходные данные hello hello скрипт развертывания, включая создание виртуальной среды, установки пакетов, создания файла конфигурации Web.config.</span><span class="sxs-lookup"><span data-stu-id="adaeb-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="adaeb-228">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="adaeb-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="adaeb-229">Разработка веб-приложения — Mac/Linux — командная строка</span><span class="sxs-lookup"><span data-stu-id="adaeb-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="adaeb-230">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="adaeb-230">Clone hello repository</span></span>
<span data-ttu-id="adaeb-231">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный.</span><span class="sxs-lookup"><span data-stu-id="adaeb-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="adaeb-232">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="adaeb-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="adaeb-233">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="adaeb-233">Create virtual environment</span></span>
<span data-ttu-id="adaeb-234">Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория).</span><span class="sxs-lookup"><span data-stu-id="adaeb-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="adaeb-235">Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.</span><span class="sxs-lookup"><span data-stu-id="adaeb-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="adaeb-236">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello колонку параметров приложения из веб-приложения hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="adaeb-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="adaeb-237">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="adaeb-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="adaeb-238">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="adaeb-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="adaeb-239">или pyvenv env</span><span class="sxs-lookup"><span data-stu-id="adaeb-239">or pyvenv env</span></span>

<span data-ttu-id="adaeb-240">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="adaeb-240">Install any external packages required by your application.</span></span> <span data-ttu-id="adaeb-241">Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:</span><span class="sxs-lookup"><span data-stu-id="adaeb-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="adaeb-242">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="adaeb-242">Run using development server</span></span>
<span data-ttu-id="adaeb-243">Приложение hello под сервером разработки можно запустить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="adaeb-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="adaeb-244">Hello консоли появится URL-адрес hello и прослушивает порт hello server:</span><span class="sxs-lookup"><span data-stu-id="adaeb-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="adaeb-245">Откройте браузер toothat URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="adaeb-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="adaeb-246">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="adaeb-246">Make changes</span></span>
<span data-ttu-id="adaeb-247">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="adaeb-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="adaeb-248">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="adaeb-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="adaeb-249">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="adaeb-249">Install more packages</span></span>
<span data-ttu-id="adaeb-250">Зависимости приложений могут не ограничиваться Python и Bottle.</span><span class="sxs-lookup"><span data-stu-id="adaeb-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="adaeb-251">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="adaeb-251">You can install additional packages using pip.</span></span> <span data-ttu-id="adaeb-252">Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:</span><span class="sxs-lookup"><span data-stu-id="adaeb-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="adaeb-253">Убедитесь, что requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="adaeb-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="adaeb-254">Применить изменения hello:</span><span class="sxs-lookup"><span data-stu-id="adaeb-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="adaeb-255">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="adaeb-255">Deploy tooAzure</span></span>
<span data-ttu-id="adaeb-256">tootrigger развертывание принудительной hello изменяет tooAzure:</span><span class="sxs-lookup"><span data-stu-id="adaeb-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="adaeb-257">Вы увидите выходные данные hello hello скрипт развертывания, включая создание виртуальной среды, установки пакетов, создания файла конфигурации Web.config.</span><span class="sxs-lookup"><span data-stu-id="adaeb-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="adaeb-258">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="adaeb-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="adaeb-259">Устранение неполадок — установка пакета</span><span class="sxs-lookup"><span data-stu-id="adaeb-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="adaeb-260">Устранение неполадок — виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="adaeb-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="adaeb-261">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="adaeb-261">Next Steps</span></span>
<span data-ttu-id="adaeb-262">Выполните эти ссылки toolearn Дополнительные сведения о Bottle и инструменты Python для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="adaeb-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="adaeb-263">[Документация по работе с Bottle]</span><span class="sxs-lookup"><span data-stu-id="adaeb-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="adaeb-264">[средства Python для Visual Studio документации]</span><span class="sxs-lookup"><span data-stu-id="adaeb-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="adaeb-265">Дополнительную информацию об использовании табличного хранилища Azure и MongoDB см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="adaeb-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="adaeb-266">[Использование Bottle и MongoDB в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="adaeb-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="adaeb-267">[Использование Bottle и табличного хранилища Azure в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="adaeb-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="adaeb-268">Изменения</span><span class="sxs-lookup"><span data-stu-id="adaeb-268">What's changed</span></span>
* <span data-ttu-id="adaeb-269">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="adaeb-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Использование Bottle и MongoDB в Azure с помощью инструментов Python для Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Использование Bottle и табличного хранилища Azure в Azure с помощью инструментов Python для Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

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
[Документация по работе с Bottle]: http://bottlepy.org/docs/dev/index.html

