---
title: "aaaCreating веб-приложений с термосе в Azure"
description: "Учебник, в котором представлены toorunning Python веб-приложения в Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="add33-103">Создание веб-приложений с помощью Flask в Azure</span><span class="sxs-lookup"><span data-stu-id="add33-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="add33-104">В данном учебнике как tooget была запущена Python в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="add33-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="add33-105">Служба веб-приложений предоставляет ограниченное бесплатное размещение приложений, а также возможности их быстрого развертывания и использования языка Python.</span><span class="sxs-lookup"><span data-stu-id="add33-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="add33-106">Здравствуйте, по мере роста приложения, можно переключить toopaid размещение и также можно интегрировать со всеми другими службами Azure.</span><span class="sxs-lookup"><span data-stu-id="add33-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="add33-107">Вы создадите приложения с помощью веб-платформа термосе hello (см. другие версии этого учебника, чтобы [Django](web-sites-python-create-deploy-django-app.md) и [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="add33-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="add33-108">Будет создать веб-сайт hello из коллекции Azure hello, Настройка развертывания Git и клонировать репозиторий hello локально.</span><span class="sxs-lookup"><span data-stu-id="add33-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="add33-109">Затем можно будет запустить приложение hello локально, внести изменения, зафиксируйте и отправьте их tooAzure.</span><span class="sxs-lookup"><span data-stu-id="add33-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="add33-110">Здравствуйте учебника показано, как toodo это в Windows или Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="add33-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="add33-111">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="add33-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="add33-112">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="add33-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="add33-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="add33-113">Prerequisites</span></span>
* <span data-ttu-id="add33-114">Windows, Mac или Linux</span><span class="sxs-lookup"><span data-stu-id="add33-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="add33-115">Python 2.7 или 3.4</span><span class="sxs-lookup"><span data-stu-id="add33-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="add33-116">setuptools, pip, virtualenv (только для Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="add33-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="add33-117">Git</span><span class="sxs-lookup"><span data-stu-id="add33-117">Git</span></span>
* <span data-ttu-id="add33-118">[средствами Python для Visual Studio][средствами Python для Visual Studio] (PTVS) (необязательно).</span><span class="sxs-lookup"><span data-stu-id="add33-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="add33-119">**Примечание.** Публикация TFS в настоящее время для проектов Python не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="add33-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="add33-120">Windows</span><span class="sxs-lookup"><span data-stu-id="add33-120">Windows</span></span>
<span data-ttu-id="add33-121">Если у вас еще не установлен Python 2.7 или 3.4 (32-разрядная версия), рекомендуется сначала установить [пакет SDK для Azure для Python 2.7] или [пакет SDK для Azure для Python 3.4] с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="add33-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="add33-122">При этом устанавливаются hello 32-разрядной версии Python дублирует, pip, virtualenv, (32-разрядных Python —, установленных на компьютерах hello Azure узлов) и т. д.</span><span class="sxs-lookup"><span data-stu-id="add33-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="add33-123">Python также можно скачать с веб-сайта [python.org].</span><span class="sxs-lookup"><span data-stu-id="add33-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="add33-124">Для Git рекомендуется использовать [Git для Windows] или [GitHub для Windows].</span><span class="sxs-lookup"><span data-stu-id="add33-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="add33-125">При использовании Visual Studio, можно использовать поддержку hello интеграции Git.</span><span class="sxs-lookup"><span data-stu-id="add33-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="add33-126">Мы также рекомендуем установить [инструменты Python 2.2 для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="add33-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="add33-127">Это не обязательно, но если у вас [Visual Studio], включая hello освободить Visual Studio Community 2013 или Visual Studio Express 2013 для Web, а затем это даст значительные среду IDE Python.</span><span class="sxs-lookup"><span data-stu-id="add33-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="add33-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="add33-128">Mac/Linux</span></span>
<span data-ttu-id="add33-129">У вас должны быть установлены Python и Git. Убедитесь, что у вас установлена версия Python 2.7 или 3.4.</span><span class="sxs-lookup"><span data-stu-id="add33-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="add33-130">Создание веб-приложения на портале Azure hello</span><span class="sxs-lookup"><span data-stu-id="add33-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="add33-131">Hello первым шагом при создании приложения является toocreate hello веб-приложения через hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="add33-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="add33-132">Войдите на портал Azure hello и щелкните hello **NEW** кнопки в левом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="add33-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="add33-133">Щелкните **Интернет + мобильные устройства**.</span><span class="sxs-lookup"><span data-stu-id="add33-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="add33-134">В поле поиска hello введите «python».</span><span class="sxs-lookup"><span data-stu-id="add33-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="add33-135">В результатах поиска hello, выберите **термосе**, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="add33-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="add33-136">Настройте приложение новый термосе hello, таких как создание нового плана служб приложений и новую группу ресурсов для него.</span><span class="sxs-lookup"><span data-stu-id="add33-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="add33-137">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="add33-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="add33-138">Настроить публикацию Git для только что созданный веб-приложения в соответствии с инструкциями hello в [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="add33-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="add33-139">Обзор приложений</span><span class="sxs-lookup"><span data-stu-id="add33-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="add33-140">Содержимое репозитория Git</span><span class="sxs-lookup"><span data-stu-id="add33-140">Git repository contents</span></span>
<span data-ttu-id="add33-141">Ниже приведен обзор hello файлов, которые можно найти в hello исходный репозиторий Git, который мы будем клонировать в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="add33-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="add33-142">Основными источниками для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="add33-142">Main sources for hello application.</span></span>  <span data-ttu-id="add33-143">Состоит из 3 страниц (index, about, contact) с макетом главной страницы.</span><span class="sxs-lookup"><span data-stu-id="add33-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="add33-144">Использует такое статическое содержимое и сценарии, как bootstrap, jquery, modernizr и respond.</span><span class="sxs-lookup"><span data-stu-id="add33-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="add33-145">Поддержка локального сервера разработки.</span><span class="sxs-lookup"><span data-stu-id="add33-145">Local development server support.</span></span> <span data-ttu-id="add33-146">Используйте это приложение hello toorun локально.</span><span class="sxs-lookup"><span data-stu-id="add33-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="add33-147">Файлы проекта для использования со [средствами Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="add33-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="add33-148">Прокси-сервер IIS для виртуальных сред и поддержки удаленной отладки PTVS.</span><span class="sxs-lookup"><span data-stu-id="add33-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="add33-149">Внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="add33-149">External packages needed by this application.</span></span> <span data-ttu-id="add33-150">скрипт развертывания Hello будет pip hello пакетов установки, перечисленные в этом файле.</span><span class="sxs-lookup"><span data-stu-id="add33-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="add33-151">Файлы конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="add33-151">IIS configuration files.</span></span>  <span data-ttu-id="add33-152">скрипт развертывания Hello будет использовать соответствующий web.x.y.config hello и скопируйте его в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="add33-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="add33-153">Дополнительные файлы — настройка развертывания</span><span class="sxs-lookup"><span data-stu-id="add33-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="add33-154">Дополнительные файлы — среда выполнения Python</span><span class="sxs-lookup"><span data-stu-id="add33-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="add33-155">Дополнительные файлы на сервере</span><span class="sxs-lookup"><span data-stu-id="add33-155">Additional files on server</span></span>
<span data-ttu-id="add33-156">Некоторые файлы на сервере hello существует, но не добавляются toohello репозитории.</span><span class="sxs-lookup"><span data-stu-id="add33-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="add33-157">Эти отчеты создаются с hello сценария развертывания.</span><span class="sxs-lookup"><span data-stu-id="add33-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="add33-158">Файл конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="add33-158">IIS configuration file.</span></span>  <span data-ttu-id="add33-159">Создается из файла web.x.y.config при каждом развертывании.</span><span class="sxs-lookup"><span data-stu-id="add33-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="add33-160">Виртуальная среда Python.</span><span class="sxs-lookup"><span data-stu-id="add33-160">Python virtual environment.</span></span>  <span data-ttu-id="add33-161">Если совместимые виртуальная среда уже не существует в приложение hello, созданные во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="add33-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="add33-162">Пакеты, перечисленные в requirements.txt являются pip установлен, но pip пропустит установки, если hello пакеты уже установлены.</span><span class="sxs-lookup"><span data-stu-id="add33-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="add33-163">Hello следующие 3 рассматриваются как tooproceed с hello веб-разработки приложений в разделе 3 различных сред:</span><span class="sxs-lookup"><span data-stu-id="add33-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="add33-164">Windows, со средствами Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="add33-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="add33-165">Windows с командной строкой;</span><span class="sxs-lookup"><span data-stu-id="add33-165">Windows, with command line</span></span>
* <span data-ttu-id="add33-166">Mac и Linux с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="add33-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="add33-167">Развертывание веб-приложений — Windows — средства Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="add33-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="add33-168">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="add33-168">Clone hello repository</span></span>
<span data-ttu-id="add33-169">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="add33-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="add33-170">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="add33-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="add33-171">Привет открыть файл решения (SLN-файл), включенный в корне репозитория hello hello.</span><span class="sxs-lookup"><span data-stu-id="add33-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="add33-172">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="add33-172">Create virtual environment</span></span>
<span data-ttu-id="add33-173">Теперь мы создадим виртуальную среду для локальной разработки веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="add33-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="add33-174">Щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add Virtual Environment...** (Добавить виртуальную среду...).</span><span class="sxs-lookup"><span data-stu-id="add33-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="add33-175">Убедитесь, что имя hello среды hello `env`.</span><span class="sxs-lookup"><span data-stu-id="add33-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="add33-176">Выберите базовый интерпретатор hello.</span><span class="sxs-lookup"><span data-stu-id="add33-176">Select hello base interpreter.</span></span>  <span data-ttu-id="add33-177">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="add33-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="add33-178">Убедитесь, что параметр hello toodownload и установки пакетов.</span><span class="sxs-lookup"><span data-stu-id="add33-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="add33-179">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="add33-179">Click **Create**.</span></span>  <span data-ttu-id="add33-180">Это создание виртуальной среды hello и установка зависимостей, перечисленных в requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="add33-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="add33-181">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="add33-181">Run using development server</span></span>
<span data-ttu-id="add33-182">Нажмите клавишу F5 toostart отладки и веб-браузере откроется автоматически toohello страница выполняется локально.</span><span class="sxs-lookup"><span data-stu-id="add33-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="add33-183">Можно установить точки останова в hello источников, окна контрольных значений используйте hello и т. д.  . В разделе hello [средства Python для Visual Studio документации] Дополнительные сведения о hello различных функций.</span><span class="sxs-lookup"><span data-stu-id="add33-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="add33-184">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="add33-184">Make changes</span></span>
<span data-ttu-id="add33-185">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="add33-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="add33-186">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="add33-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="add33-187">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="add33-187">Install more packages</span></span>
<span data-ttu-id="add33-188">Зависимости приложений могут не ограничиваться Python и Flask.</span><span class="sxs-lookup"><span data-stu-id="add33-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="add33-189">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="add33-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="add33-190">tooinstall пакета, щелкните правой кнопкой мыши виртуальную среду hello и выберите пункт **установить пакет Python**.</span><span class="sxs-lookup"><span data-stu-id="add33-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="add33-191">Например, пакет Azure SDK для Python, который предоставляет вам доступ tooAzure хранилище, service bus и другим службам Azure ввести hello tooinstall `azure`:</span><span class="sxs-lookup"><span data-stu-id="add33-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="add33-192">Щелкните правой кнопкой мыши в виртуальной среде hello и выберите **создания requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="add33-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="add33-193">Зафиксируйте hello изменения toorequirements.txt toohello репозитории.</span><span class="sxs-lookup"><span data-stu-id="add33-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="add33-194">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="add33-194">Deploy tooAzure</span></span>
<span data-ttu-id="add33-195">Щелкните tootrigger развертывания **синхронизации** или **Push**.</span><span class="sxs-lookup"><span data-stu-id="add33-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="add33-196">При синхронизации выполняется как принудительная отправка, так и применение по запросу.</span><span class="sxs-lookup"><span data-stu-id="add33-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="add33-197">Hello первого развертывания может потребоваться некоторое время, как он создаст в виртуальной среде, пакетов установки, и т. д.</span><span class="sxs-lookup"><span data-stu-id="add33-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="add33-198">Visual Studio не показывает ход выполнения развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="add33-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="add33-199">При желании вывода hello tooreview разделе hello на [Устранение неполадок - развертывания](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="add33-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="add33-200">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="add33-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="add33-201">Разработка веб-приложения — Windows — командная строка</span><span class="sxs-lookup"><span data-stu-id="add33-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="add33-202">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="add33-202">Clone hello repository</span></span>
<span data-ttu-id="add33-203">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный.</span><span class="sxs-lookup"><span data-stu-id="add33-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="add33-204">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="add33-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="add33-205">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="add33-205">Create virtual environment</span></span>
<span data-ttu-id="add33-206">Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория).</span><span class="sxs-lookup"><span data-stu-id="add33-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="add33-207">Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.</span><span class="sxs-lookup"><span data-stu-id="add33-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="add33-208">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="add33-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="add33-209">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="add33-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="add33-210">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="add33-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="add33-211">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="add33-211">Install any external packages required by your application.</span></span> <span data-ttu-id="add33-212">Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:</span><span class="sxs-lookup"><span data-stu-id="add33-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="add33-213">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="add33-213">Run using development server</span></span>
<span data-ttu-id="add33-214">Приложение hello под сервером разработки можно запустить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="add33-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="add33-215">Hello консоли появится URL-адрес hello и прослушивает порт hello server:</span><span class="sxs-lookup"><span data-stu-id="add33-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="add33-216">Откройте браузер toothat URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="add33-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="add33-217">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="add33-217">Make changes</span></span>
<span data-ttu-id="add33-218">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="add33-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="add33-219">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="add33-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="add33-220">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="add33-220">Install more packages</span></span>
<span data-ttu-id="add33-221">Зависимости приложений могут не ограничиваться Python и Flask.</span><span class="sxs-lookup"><span data-stu-id="add33-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="add33-222">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="add33-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="add33-223">Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:</span><span class="sxs-lookup"><span data-stu-id="add33-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="add33-224">Убедитесь, что requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="add33-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="add33-225">Применить изменения hello:</span><span class="sxs-lookup"><span data-stu-id="add33-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="add33-226">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="add33-226">Deploy tooAzure</span></span>
<span data-ttu-id="add33-227">tootrigger развертывание принудительной hello изменяет tooAzure:</span><span class="sxs-lookup"><span data-stu-id="add33-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="add33-228">Вы увидите выходные данные hello hello скрипт развертывания, включая создание виртуальной среды, установки пакетов, создания файла конфигурации Web.config.</span><span class="sxs-lookup"><span data-stu-id="add33-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="add33-229">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="add33-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="add33-230">Разработка веб-приложения — Mac/Linux — командная строка</span><span class="sxs-lookup"><span data-stu-id="add33-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="add33-231">Клон hello репозитория</span><span class="sxs-lookup"><span data-stu-id="add33-231">Clone hello repository</span></span>
<span data-ttu-id="add33-232">Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный.</span><span class="sxs-lookup"><span data-stu-id="add33-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="add33-233">Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="add33-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="add33-234">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="add33-234">Create virtual environment</span></span>
<span data-ttu-id="add33-235">Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория).</span><span class="sxs-lookup"><span data-stu-id="add33-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="add33-236">Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.</span><span class="sxs-lookup"><span data-stu-id="add33-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="add33-237">Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="add33-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="add33-238">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="add33-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="add33-239">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="add33-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="add33-240">или pyvenv env</span><span class="sxs-lookup"><span data-stu-id="add33-240">or pyvenv env</span></span>

<span data-ttu-id="add33-241">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="add33-241">Install any external packages required by your application.</span></span> <span data-ttu-id="add33-242">Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:</span><span class="sxs-lookup"><span data-stu-id="add33-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="add33-243">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="add33-243">Run using development server</span></span>
<span data-ttu-id="add33-244">Приложение hello под сервером разработки можно запустить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="add33-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="add33-245">Hello консоли появится URL-адрес hello и прослушивает порт hello server:</span><span class="sxs-lookup"><span data-stu-id="add33-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="add33-246">Откройте браузер toothat URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="add33-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="add33-247">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="add33-247">Make changes</span></span>
<span data-ttu-id="add33-248">Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.</span><span class="sxs-lookup"><span data-stu-id="add33-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="add33-249">После тестирования изменений, их можно сохранить toohello репозитории:</span><span class="sxs-lookup"><span data-stu-id="add33-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="add33-250">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="add33-250">Install more packages</span></span>
<span data-ttu-id="add33-251">Зависимости приложений могут не ограничиваться Python и Flask.</span><span class="sxs-lookup"><span data-stu-id="add33-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="add33-252">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="add33-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="add33-253">Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:</span><span class="sxs-lookup"><span data-stu-id="add33-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="add33-254">Убедитесь, что requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="add33-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="add33-255">Применить изменения hello:</span><span class="sxs-lookup"><span data-stu-id="add33-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="add33-256">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="add33-256">Deploy tooAzure</span></span>
<span data-ttu-id="add33-257">tootrigger развертывание принудительной hello изменяет tooAzure:</span><span class="sxs-lookup"><span data-stu-id="add33-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="add33-258">Вы увидите выходные данные hello hello скрипт развертывания, включая создание виртуальной среды, установки пакетов, создания файла конфигурации Web.config.</span><span class="sxs-lookup"><span data-stu-id="add33-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="add33-259">Обзор изменения tooview toohello URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="add33-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="add33-260">Устранение неполадок — установка пакета</span><span class="sxs-lookup"><span data-stu-id="add33-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="add33-261">Устранение неполадок — виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="add33-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="add33-262">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="add33-262">Next Steps</span></span>
<span data-ttu-id="add33-263">Выполните эти ссылки toolearn Дополнительные сведения о термосе и инструменты Python для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="add33-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="add33-264">[Документация по Flask]</span><span class="sxs-lookup"><span data-stu-id="add33-264">[Flask Documentation]</span></span>
* <span data-ttu-id="add33-265">[средства Python для Visual Studio документации]</span><span class="sxs-lookup"><span data-stu-id="add33-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="add33-266">Дополнительную информацию об использовании табличного хранилища Azure и MongoDB см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="add33-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="add33-267">[Использование Flask и MongoDB в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="add33-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="add33-268">[Flask и хранилище таблиц Azure с использованием инструментов Python Tools для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="add33-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="add33-269">Дополнительные сведения см. также: hello [центре разработчиков Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="add33-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="add33-270">Изменения</span><span class="sxs-lookup"><span data-stu-id="add33-270">What's changed</span></span>
* <span data-ttu-id="add33-271">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="add33-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Использование Flask и MongoDB в Azure с помощью инструментов Python для Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask и хранилище таблиц Azure с использованием инструментов Python Tools для Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

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
[Документация по Flask]: http://flask.pocoo.org/ 

