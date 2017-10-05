---
title: "Создание веб-приложений с помощью Flask в Azure"
description: "В учебнике описывается, как запустить веб-приложение на языке Python в Azure."
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
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="69ce1-103">Создание веб-приложений с помощью Flask в Azure</span><span class="sxs-lookup"><span data-stu-id="69ce1-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="69ce1-104">В этом учебнике описывается, как начать работу с языком Python в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="69ce1-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="69ce1-105">Служба веб-приложений предоставляет ограниченное бесплатное размещение приложений, а также возможности их быстрого развертывания и использования языка Python.</span><span class="sxs-lookup"><span data-stu-id="69ce1-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="69ce1-106">По мере роста приложения его можно перевести на платное размещение и интегрировать во все другие службы Azure.</span><span class="sxs-lookup"><span data-stu-id="69ce1-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="69ce1-107">Вы создадите приложение с помощью веб-платформы Flask (ознакомьтесь с другими версиями этого руководства для платформ [Django](web-sites-python-create-deploy-django-app.md) и [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="69ce1-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="69ce1-108">Затем вы создадите веб-сайт из коллекции Azure, настроите развертывание через Git и локально клонируете репозиторий.</span><span class="sxs-lookup"><span data-stu-id="69ce1-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="69ce1-109">После этого вы запустите приложение локально, внесете в него изменения, зафиксируете их и отправите в Azure.</span><span class="sxs-lookup"><span data-stu-id="69ce1-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="69ce1-110">В этом учебнике показано, как выполнить вышеуказанные действия в Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="69ce1-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="69ce1-111">Если вы хотите приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="69ce1-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="69ce1-112">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="69ce1-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="69ce1-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="69ce1-113">Prerequisites</span></span>
* <span data-ttu-id="69ce1-114">Windows, Mac или Linux</span><span class="sxs-lookup"><span data-stu-id="69ce1-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="69ce1-115">Python 2.7 или 3.4</span><span class="sxs-lookup"><span data-stu-id="69ce1-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="69ce1-116">setuptools, pip, virtualenv (только для Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="69ce1-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="69ce1-117">Git</span><span class="sxs-lookup"><span data-stu-id="69ce1-117">Git</span></span>
* <span data-ttu-id="69ce1-118">[средствами Python для Visual Studio][средствами Python для Visual Studio] (PTVS) (необязательно).</span><span class="sxs-lookup"><span data-stu-id="69ce1-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="69ce1-119">**Примечание.** Публикация TFS в настоящее время для проектов Python не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="69ce1-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="69ce1-120">Windows</span><span class="sxs-lookup"><span data-stu-id="69ce1-120">Windows</span></span>
<span data-ttu-id="69ce1-121">Если у вас еще не установлен Python 2.7 или 3.4 (32-разрядная версия), рекомендуется сначала установить [пакет SDK для Azure для Python 2.7] или [пакет SDK для Azure для Python 3.4] с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="69ce1-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="69ce1-122">При этом выполняется установка 32-разрядной версии Python (для установки на хост-компьютерах Azure), setuptools, pip, virtualenv, и т. д.</span><span class="sxs-lookup"><span data-stu-id="69ce1-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="69ce1-123">Python также можно скачать с веб-сайта [python.org].</span><span class="sxs-lookup"><span data-stu-id="69ce1-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="69ce1-124">Для Git рекомендуется использовать [Git для Windows] или [GitHub для Windows].</span><span class="sxs-lookup"><span data-stu-id="69ce1-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="69ce1-125">При использовании Visual Studio можно использовать интегрированную поддержку Git.</span><span class="sxs-lookup"><span data-stu-id="69ce1-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="69ce1-126">Мы также рекомендуем установить [инструменты Python 2.2 для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="69ce1-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="69ce1-127">Это необязательно, но, если у вас есть [Visual Studio], например бесплатная версия Visual Studio Community 2013 или Visual Studio Express 2013 для Web, вы получите отличную интегрированную среду разработки Python.</span><span class="sxs-lookup"><span data-stu-id="69ce1-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="69ce1-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="69ce1-128">Mac/Linux</span></span>
<span data-ttu-id="69ce1-129">У вас должны быть установлены Python и Git. Убедитесь, что у вас установлена версия Python 2.7 или 3.4.</span><span class="sxs-lookup"><span data-stu-id="69ce1-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="69ce1-130">Создание веб-приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="69ce1-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="69ce1-131">Первым делом нужно создать веб-приложение на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="69ce1-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="69ce1-132">Войдите на портал Azure и нажмите кнопку **СОЗДАТЬ** в нижнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="69ce1-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="69ce1-133">Щелкните **Интернет + мобильные устройства**.</span><span class="sxs-lookup"><span data-stu-id="69ce1-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="69ce1-134">В поле поиска введите "python".</span><span class="sxs-lookup"><span data-stu-id="69ce1-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="69ce1-135">В результатах поиска выберите **Flask**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="69ce1-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="69ce1-136">Настройте новое приложение Flask, например создайте новый план службы приложений и новую группу ресурсов для него.</span><span class="sxs-lookup"><span data-stu-id="69ce1-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="69ce1-137">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="69ce1-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="69ce1-138">Настройте публикацию Git для вновь созданного веб-приложения, следуя инструкциям из статьи [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="69ce1-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="69ce1-139">Обзор приложений</span><span class="sxs-lookup"><span data-stu-id="69ce1-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="69ce1-140">Содержимое репозитория Git</span><span class="sxs-lookup"><span data-stu-id="69ce1-140">Git repository contents</span></span>
<span data-ttu-id="69ce1-141">Ниже приведен обзор файлов, которые можно найти в исходном репозитории Git. Мы клонируем его в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="69ce1-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="69ce1-142">Основные источники для приложения.</span><span class="sxs-lookup"><span data-stu-id="69ce1-142">Main sources for the application.</span></span>  <span data-ttu-id="69ce1-143">Состоит из 3 страниц (index, about, contact) с макетом главной страницы.</span><span class="sxs-lookup"><span data-stu-id="69ce1-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="69ce1-144">Использует такое статическое содержимое и сценарии, как bootstrap, jquery, modernizr и respond.</span><span class="sxs-lookup"><span data-stu-id="69ce1-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="69ce1-145">Поддержка локального сервера разработки.</span><span class="sxs-lookup"><span data-stu-id="69ce1-145">Local development server support.</span></span> <span data-ttu-id="69ce1-146">Используется для локального запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="69ce1-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="69ce1-147">Файлы проекта для использования со [средствами Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="69ce1-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="69ce1-148">Прокси-сервер IIS для виртуальных сред и поддержки удаленной отладки PTVS.</span><span class="sxs-lookup"><span data-stu-id="69ce1-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="69ce1-149">Внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="69ce1-149">External packages needed by this application.</span></span> <span data-ttu-id="69ce1-150">Сценарий развертывания установит пакеты, указанные в этом файле, с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="69ce1-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="69ce1-151">Файлы конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="69ce1-151">IIS configuration files.</span></span>  <span data-ttu-id="69ce1-152">Сценарий развертывания использует соответствующий web.x.y.config и скопирует его с именем web.config.</span><span class="sxs-lookup"><span data-stu-id="69ce1-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="69ce1-153">Дополнительные файлы — настройка развертывания</span><span class="sxs-lookup"><span data-stu-id="69ce1-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="69ce1-154">Дополнительные файлы — среда выполнения Python</span><span class="sxs-lookup"><span data-stu-id="69ce1-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="69ce1-155">Дополнительные файлы на сервере</span><span class="sxs-lookup"><span data-stu-id="69ce1-155">Additional files on server</span></span>
<span data-ttu-id="69ce1-156">Некоторые файлы размещены на сервере, но не добавляются в репозиторий git.</span><span class="sxs-lookup"><span data-stu-id="69ce1-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="69ce1-157">Такие файлы создаются с помощью сценария развертывания.</span><span class="sxs-lookup"><span data-stu-id="69ce1-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="69ce1-158">Файл конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="69ce1-158">IIS configuration file.</span></span>  <span data-ttu-id="69ce1-159">Создается из файла web.x.y.config при каждом развертывании.</span><span class="sxs-lookup"><span data-stu-id="69ce1-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="69ce1-160">Виртуальная среда Python.</span><span class="sxs-lookup"><span data-stu-id="69ce1-160">Python virtual environment.</span></span>  <span data-ttu-id="69ce1-161">Создается при развертывании, если совместимая виртуальная среда еще не создана в приложении.</span><span class="sxs-lookup"><span data-stu-id="69ce1-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="69ce1-162">Пакеты, указанные в файле requirements.txt, устанавливаются с помощью pip. Однако если они уже установлены, pip не будет выполнять установку.</span><span class="sxs-lookup"><span data-stu-id="69ce1-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="69ce1-163">В следующих 3 разделах описывается разработка веб-приложения в 3 разных средах:</span><span class="sxs-lookup"><span data-stu-id="69ce1-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="69ce1-164">Windows, со средствами Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="69ce1-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="69ce1-165">Windows с командной строкой;</span><span class="sxs-lookup"><span data-stu-id="69ce1-165">Windows, with command line</span></span>
* <span data-ttu-id="69ce1-166">Mac и Linux с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="69ce1-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="69ce1-167">Развертывание веб-приложений — Windows — средства Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="69ce1-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="69ce1-168">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="69ce1-168">Clone the repository</span></span>
<span data-ttu-id="69ce1-169">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="69ce1-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="69ce1-170">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="69ce1-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="69ce1-171">Откройте файл решения (SLN-файл), который содержится в корневой папке репозитория.</span><span class="sxs-lookup"><span data-stu-id="69ce1-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="69ce1-172">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="69ce1-172">Create virtual environment</span></span>
<span data-ttu-id="69ce1-173">Теперь мы создадим виртуальную среду для локальной разработки веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="69ce1-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="69ce1-174">Щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add Virtual Environment...** (Добавить виртуальную среду...).</span><span class="sxs-lookup"><span data-stu-id="69ce1-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="69ce1-175">Убедитесь, что имя среды — `env`.</span><span class="sxs-lookup"><span data-stu-id="69ce1-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="69ce1-176">Выберите базовый интерпретатор.</span><span class="sxs-lookup"><span data-stu-id="69ce1-176">Select the base interpreter.</span></span>  <span data-ttu-id="69ce1-177">Убедитесь, что используется та же версия Python, которая выбрана для веб-приложения (в файле runtime.txt или в колонке **Параметры приложения** веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="69ce1-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="69ce1-178">Убедитесь, что установлен флажок для скачивания и установки пакетов.</span><span class="sxs-lookup"><span data-stu-id="69ce1-178">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="69ce1-179">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="69ce1-179">Click **Create**.</span></span>  <span data-ttu-id="69ce1-180">Таким образом будет создана виртуальная среда и установлены зависимости из файла requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="69ce1-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="69ce1-181">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="69ce1-181">Run using development server</span></span>
<span data-ttu-id="69ce1-182">Нажмите клавишу F5, чтобы начать отладку, и браузер автоматически откроет страницу, запущенную локально.</span><span class="sxs-lookup"><span data-stu-id="69ce1-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="69ce1-183">Можно установить точки останова в источниках, использовать окна контрольных значений и т. д.  Дополнительные сведения о различных функциях см. в [документации по средствам Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="69ce1-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="69ce1-184">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="69ce1-184">Make changes</span></span>
<span data-ttu-id="69ce1-185">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="69ce1-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="69ce1-186">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="69ce1-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="69ce1-187">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="69ce1-187">Install more packages</span></span>
<span data-ttu-id="69ce1-188">Зависимости приложений могут не ограничиваться Python и Flask.</span><span class="sxs-lookup"><span data-stu-id="69ce1-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="69ce1-189">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="69ce1-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="69ce1-190">Чтобы установить пакет, щелкните правой кнопкой мыши в виртуальной среде и выберите **Установить пакет Python**.</span><span class="sxs-lookup"><span data-stu-id="69ce1-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="69ce1-191">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине и другим службам Azure, введите `azure`:</span><span class="sxs-lookup"><span data-stu-id="69ce1-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="69ce1-192">Щелкните правой кнопкой мыши в виртуальной среде и выберите **Создать файл requirements.txt** , чтобы обновить файл requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="69ce1-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="69ce1-193">Затем сохраните внесенные в этот файл изменения в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="69ce1-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="69ce1-194">Развернуть в Azure</span><span class="sxs-lookup"><span data-stu-id="69ce1-194">Deploy to Azure</span></span>
<span data-ttu-id="69ce1-195">Чтобы запустить развертывание, щелкните **Синхронизировать** или **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="69ce1-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="69ce1-196">При синхронизации выполняется как принудительная отправка, так и применение по запросу.</span><span class="sxs-lookup"><span data-stu-id="69ce1-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="69ce1-197">Первое развертывание может занять некоторое время, необходимое для создания виртуальной среды, установку пакетов и т. д.</span><span class="sxs-lookup"><span data-stu-id="69ce1-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="69ce1-198">В Visual Studio не отображается ход выполнения развертывания.</span><span class="sxs-lookup"><span data-stu-id="69ce1-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="69ce1-199">Сведения о том, как можно просмотреть результат, см. в разделе [Устранение неполадок — развертывание](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="69ce1-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="69ce1-200">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="69ce1-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="69ce1-201">Разработка веб-приложения — Windows — командная строка</span><span class="sxs-lookup"><span data-stu-id="69ce1-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="69ce1-202">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="69ce1-202">Clone the repository</span></span>
<span data-ttu-id="69ce1-203">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure, а затем добавьте репозиторий Azure в качестве удаленного.</span><span class="sxs-lookup"><span data-stu-id="69ce1-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="69ce1-204">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="69ce1-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="69ce1-205">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="69ce1-205">Create virtual environment</span></span>
<span data-ttu-id="69ce1-206">Давайте создадим новую виртуальную среду для разработки (не добавляйте ее в репозиторий).</span><span class="sxs-lookup"><span data-stu-id="69ce1-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="69ce1-207">Виртуальные среды на языке Python нельзя перемещать, поэтому каждому разработчику, работающему над приложением, будет необходимо создать такую среду локально.</span><span class="sxs-lookup"><span data-stu-id="69ce1-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="69ce1-208">Убедитесь, что используется та же версия Python, которая выбрана для веб-приложения (в файле runtime.txt или в колонке **Параметры приложения** веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="69ce1-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="69ce1-209">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="69ce1-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="69ce1-210">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="69ce1-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="69ce1-211">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="69ce1-211">Install any external packages required by your application.</span></span> <span data-ttu-id="69ce1-212">Чтобы установить пакеты в своей виртуальной среде, вы можете использовать файл requirements.txt в корне репозитория:</span><span class="sxs-lookup"><span data-stu-id="69ce1-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="69ce1-213">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="69ce1-213">Run using development server</span></span>
<span data-ttu-id="69ce1-214">Вы можете запустить приложение на сервере разработки с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="69ce1-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="69ce1-215">В консоли отобразится URL-адрес и порт, который прослушивает сервер:</span><span class="sxs-lookup"><span data-stu-id="69ce1-215">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="69ce1-216">Далее откройте браузер и введите этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="69ce1-216">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="69ce1-217">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="69ce1-217">Make changes</span></span>
<span data-ttu-id="69ce1-218">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="69ce1-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="69ce1-219">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="69ce1-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="69ce1-220">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="69ce1-220">Install more packages</span></span>
<span data-ttu-id="69ce1-221">Зависимости приложений могут не ограничиваться Python и Flask.</span><span class="sxs-lookup"><span data-stu-id="69ce1-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="69ce1-222">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="69ce1-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="69ce1-223">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине, а также другим службам Azure, введите:</span><span class="sxs-lookup"><span data-stu-id="69ce1-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="69ce1-224">Обязательно обновите файл requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="69ce1-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="69ce1-225">Примените изменения:</span><span class="sxs-lookup"><span data-stu-id="69ce1-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="69ce1-226">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="69ce1-226">Deploy to Azure</span></span>
<span data-ttu-id="69ce1-227">Чтобы запустить развертывание, принудительно отправьте эти изменения в Azure:</span><span class="sxs-lookup"><span data-stu-id="69ce1-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="69ce1-228">Отобразятся выходные данные сценария развертывания, а также создание виртуальной среды, установку пакетов, и создание файла web.config.</span><span class="sxs-lookup"><span data-stu-id="69ce1-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="69ce1-229">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="69ce1-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="69ce1-230">Разработка веб-приложения — Mac/Linux — командная строка</span><span class="sxs-lookup"><span data-stu-id="69ce1-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="69ce1-231">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="69ce1-231">Clone the repository</span></span>
<span data-ttu-id="69ce1-232">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure, а затем добавьте репозиторий Azure в качестве удаленного.</span><span class="sxs-lookup"><span data-stu-id="69ce1-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="69ce1-233">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="69ce1-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="69ce1-234">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="69ce1-234">Create virtual environment</span></span>
<span data-ttu-id="69ce1-235">Давайте создадим новую виртуальную среду для разработки (не добавляйте ее в репозиторий).</span><span class="sxs-lookup"><span data-stu-id="69ce1-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="69ce1-236">Виртуальные среды на языке Python нельзя перемещать, поэтому каждому разработчику, работающему над приложением, будет необходимо создать такую среду локально.</span><span class="sxs-lookup"><span data-stu-id="69ce1-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="69ce1-237">Убедитесь, что используется та же версия Python, которая выбрана для веб-приложения (в файле runtime.txt или в колонке **Параметры приложения** веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="69ce1-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="69ce1-238">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="69ce1-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="69ce1-239">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="69ce1-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="69ce1-240">или pyvenv env</span><span class="sxs-lookup"><span data-stu-id="69ce1-240">or pyvenv env</span></span>

<span data-ttu-id="69ce1-241">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="69ce1-241">Install any external packages required by your application.</span></span> <span data-ttu-id="69ce1-242">Чтобы установить пакеты в своей виртуальной среде, вы можете использовать файл requirements.txt в корне репозитория:</span><span class="sxs-lookup"><span data-stu-id="69ce1-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="69ce1-243">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="69ce1-243">Run using development server</span></span>
<span data-ttu-id="69ce1-244">Вы можете запустить приложение на сервере разработки с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="69ce1-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="69ce1-245">В консоли отобразится URL-адрес и порт, который прослушивает сервер:</span><span class="sxs-lookup"><span data-stu-id="69ce1-245">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="69ce1-246">Далее откройте браузер и введите этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="69ce1-246">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="69ce1-247">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="69ce1-247">Make changes</span></span>
<span data-ttu-id="69ce1-248">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="69ce1-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="69ce1-249">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="69ce1-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="69ce1-250">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="69ce1-250">Install more packages</span></span>
<span data-ttu-id="69ce1-251">Зависимости приложений могут не ограничиваться Python и Flask.</span><span class="sxs-lookup"><span data-stu-id="69ce1-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="69ce1-252">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="69ce1-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="69ce1-253">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине, а также другим службам Azure, введите:</span><span class="sxs-lookup"><span data-stu-id="69ce1-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="69ce1-254">Обязательно обновите файл requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="69ce1-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="69ce1-255">Примените изменения:</span><span class="sxs-lookup"><span data-stu-id="69ce1-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="69ce1-256">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="69ce1-256">Deploy to Azure</span></span>
<span data-ttu-id="69ce1-257">Чтобы запустить развертывание, принудительно отправьте эти изменения в Azure:</span><span class="sxs-lookup"><span data-stu-id="69ce1-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="69ce1-258">Отобразятся выходные данные сценария развертывания, а также создание виртуальной среды, установку пакетов, и создание файла web.config.</span><span class="sxs-lookup"><span data-stu-id="69ce1-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="69ce1-259">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="69ce1-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="69ce1-260">Устранение неполадок — установка пакета</span><span class="sxs-lookup"><span data-stu-id="69ce1-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="69ce1-261">Устранение неполадок — виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="69ce1-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="69ce1-262">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69ce1-262">Next Steps</span></span>
<span data-ttu-id="69ce1-263">Используйте следующие ссылки, чтобы узнать больше о средствах Flask и Python для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69ce1-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="69ce1-264">[Документация по Flask]</span><span class="sxs-lookup"><span data-stu-id="69ce1-264">[Flask Documentation]</span></span>
* <span data-ttu-id="69ce1-265">[документации по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="69ce1-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="69ce1-266">Дополнительную информацию об использовании табличного хранилища Azure и MongoDB см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="69ce1-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="69ce1-267">[Использование Flask и MongoDB в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="69ce1-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="69ce1-268">[Flask и хранилище таблиц Azure с использованием инструментов Python Tools для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="69ce1-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="69ce1-269">Дополнительные сведения см. в [центре по разработке для Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="69ce1-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="69ce1-270">Изменения</span><span class="sxs-lookup"><span data-stu-id="69ce1-270">What's changed</span></span>
* <span data-ttu-id="69ce1-271">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="69ce1-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="69ce1-272">[Использование Flask и MongoDB в Azure с помощью инструментов Python для Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span><span class="sxs-lookup"><span data-stu-id="69ce1-272">[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span></span>
<span data-ttu-id="69ce1-273">[Flask и хранилище таблиц Azure с использованием инструментов Python Tools для Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="69ce1-273">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="69ce1-274">[пакет SDK для Azure для Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="69ce1-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="69ce1-275">[пакет SDK для Azure для Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="69ce1-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="69ce1-276">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="69ce1-276">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="69ce1-277">[Git для Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="69ce1-277">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="69ce1-278">[GitHub для Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="69ce1-278">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="69ce1-279">[средствами Python для Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="69ce1-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="69ce1-280">[инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="69ce1-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="69ce1-281">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="69ce1-281">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="69ce1-282">[документации по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="69ce1-282">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="69ce1-283">[Документация по Flask]: http://flask.pocoo.org/</span><span class="sxs-lookup"><span data-stu-id="69ce1-283">[Flask Documentation]: http://flask.pocoo.org/</span></span> 

