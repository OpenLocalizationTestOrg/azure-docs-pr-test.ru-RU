---
title: "Создание веб-приложений на Python с помощью Bottle в Azure"
description: "Учебник, в котором вы ознакомитесь с запуском веб-приложения Python в веб-приложениях службы приложений Azure."
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
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="e53d6-103">Создание веб-приложений с помощью Bottle в Azure</span><span class="sxs-lookup"><span data-stu-id="e53d6-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="e53d6-104">В этом учебнике описывается, как начать работу с языком Python в веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="e53d6-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="e53d6-105">Служба веб-приложений предоставляет ограниченное бесплатное размещение приложений, а также возможности их быстрого развертывания и использования языка Python.</span><span class="sxs-lookup"><span data-stu-id="e53d6-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="e53d6-106">По мере роста приложения его можно перевести на платное размещение и интегрировать во все другие службы Azure.</span><span class="sxs-lookup"><span data-stu-id="e53d6-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="e53d6-107">Вы создадите веб-приложение с использованием веб-платформы Bottle (ознакомьтесь с другими версиями этого руководства для платформ [Django](web-sites-python-create-deploy-django-app.md) и [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="e53d6-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="e53d6-108">Вы можете создать веб-приложение из Azure Marketplace, настроить развертывание Git и локально клонировать репозиторий.</span><span class="sxs-lookup"><span data-stu-id="e53d6-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="e53d6-109">Затем вы сможете запускать веб-приложение локально, вносить изменения, фиксировать и отправлять их в [веб-приложения службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e53d6-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="e53d6-110">В этом учебнике показано, как выполнить вышеуказанные действия в Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="e53d6-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="e53d6-111">Если вы хотите приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="e53d6-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e53d6-112">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="e53d6-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e53d6-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e53d6-113">Prerequisites</span></span>
* <span data-ttu-id="e53d6-114">Windows, Mac или Linux</span><span class="sxs-lookup"><span data-stu-id="e53d6-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="e53d6-115">Python 2.7 или 3.4</span><span class="sxs-lookup"><span data-stu-id="e53d6-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="e53d6-116">setuptools, pip, virtualenv (только для Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="e53d6-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="e53d6-117">Git</span><span class="sxs-lookup"><span data-stu-id="e53d6-117">Git</span></span>
* <span data-ttu-id="e53d6-118">[инструменты Python 2.2 для Visual Studio][инструменты Python 2.2 для Visual Studio] (PTVS) (Примечание. Необязательный компонент.)</span><span class="sxs-lookup"><span data-stu-id="e53d6-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="e53d6-119">**Примечание.** Публикация TFS в настоящее время для проектов Python не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e53d6-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="e53d6-120">Windows</span><span class="sxs-lookup"><span data-stu-id="e53d6-120">Windows</span></span>
<span data-ttu-id="e53d6-121">Если у вас еще не установлен Python 2.7 или 3.4 (32-разрядная версия), рекомендуется сначала установить [пакет SDK для Azure для Python 2.7] или [пакет SDK для Azure для Python 3.4] с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="e53d6-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="e53d6-122">При этом выполняется установка 32-разрядной версии Python (для установки на хост-компьютерах Azure), setuptools, pip, virtualenv, и т. д.</span><span class="sxs-lookup"><span data-stu-id="e53d6-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="e53d6-123">Python также можно скачать с веб-сайта [python.org].</span><span class="sxs-lookup"><span data-stu-id="e53d6-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="e53d6-124">Для Git рекомендуется использовать [Git для Windows] или [GitHub для Windows].</span><span class="sxs-lookup"><span data-stu-id="e53d6-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="e53d6-125">При использовании Visual Studio можно использовать интегрированную поддержку Git.</span><span class="sxs-lookup"><span data-stu-id="e53d6-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="e53d6-126">Мы также рекомендуем установить [инструменты Python 2.2 для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="e53d6-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="e53d6-127">Это необязательно, но, если у вас есть [Visual Studio], например бесплатная версия Visual Studio Community 2013 или Visual Studio Express 2013 для Web, вы получите отличную интегрированную среду разработки Python.</span><span class="sxs-lookup"><span data-stu-id="e53d6-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="e53d6-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="e53d6-128">Mac/Linux</span></span>
<span data-ttu-id="e53d6-129">У вас должны быть установлены Python и Git. Убедитесь, что у вас установлена версия Python 2.7 или 3.4.</span><span class="sxs-lookup"><span data-stu-id="e53d6-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="e53d6-130">Создание веб-приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="e53d6-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="e53d6-131">Первым делом нужно создать веб-приложение на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e53d6-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="e53d6-132">Войдите на портал Azure и нажмите кнопку **СОЗДАТЬ** в нижнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="e53d6-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="e53d6-133">В поле поиска введите "python".</span><span class="sxs-lookup"><span data-stu-id="e53d6-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="e53d6-134">В результатах поиска выберите **Bottle**, затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e53d6-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="e53d6-135">Настройте новое приложение Bottle, например создайте новый план службы приложений и новую группу ресурсов для него.</span><span class="sxs-lookup"><span data-stu-id="e53d6-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="e53d6-136">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e53d6-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="e53d6-137">Настройте публикацию Git для вновь созданного веб-приложения, следуя инструкциям из статьи [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="e53d6-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="e53d6-138">Обзор приложений</span><span class="sxs-lookup"><span data-stu-id="e53d6-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="e53d6-139">Содержимое репозитория Git</span><span class="sxs-lookup"><span data-stu-id="e53d6-139">Git repository contents</span></span>
<span data-ttu-id="e53d6-140">Ниже приведен обзор файлов, которые можно найти в исходном репозитории Git. Мы клонируем его в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="e53d6-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="e53d6-141">Основные источники для приложения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-141">Main sources for the application.</span></span> <span data-ttu-id="e53d6-142">Состоит из 3 страниц (index, about, contact) с макетом главной страницы.</span><span class="sxs-lookup"><span data-stu-id="e53d6-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="e53d6-143">Использует такое статическое содержимое и сценарии, как bootstrap, jquery, modernizr и respond.</span><span class="sxs-lookup"><span data-stu-id="e53d6-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="e53d6-144">Поддержка локального сервера разработки.</span><span class="sxs-lookup"><span data-stu-id="e53d6-144">Local development server support.</span></span> <span data-ttu-id="e53d6-145">Используется для локального запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="e53d6-146">Файлы проекта для использования со [средствами Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="e53d6-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="e53d6-147">Прокси-сервер IIS для виртуальных сред и поддержки удаленной отладки PTVS.</span><span class="sxs-lookup"><span data-stu-id="e53d6-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="e53d6-148">Внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-148">External packages needed by this application.</span></span> <span data-ttu-id="e53d6-149">Сценарий развертывания установит пакеты, указанные в этом файле, с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="e53d6-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="e53d6-150">Файлы конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="e53d6-150">IIS configuration files.</span></span> <span data-ttu-id="e53d6-151">Сценарий развертывания использует соответствующий web.x.y.config и скопирует его с именем web.config.</span><span class="sxs-lookup"><span data-stu-id="e53d6-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="e53d6-152">Дополнительные файлы — настройка развертывания</span><span class="sxs-lookup"><span data-stu-id="e53d6-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="e53d6-153">Дополнительные файлы — среда выполнения Python</span><span class="sxs-lookup"><span data-stu-id="e53d6-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="e53d6-154">Дополнительные файлы на сервере</span><span class="sxs-lookup"><span data-stu-id="e53d6-154">Additional files on server</span></span>
<span data-ttu-id="e53d6-155">Некоторые файлы размещены на сервере, но не добавляются в репозиторий git.</span><span class="sxs-lookup"><span data-stu-id="e53d6-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="e53d6-156">Такие файлы создаются с помощью сценария развертывания.</span><span class="sxs-lookup"><span data-stu-id="e53d6-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="e53d6-157">Файл конфигурации IIS.</span><span class="sxs-lookup"><span data-stu-id="e53d6-157">IIS configuration file.</span></span> <span data-ttu-id="e53d6-158">Создается из файла web.x.y.config при каждом развертывании.</span><span class="sxs-lookup"><span data-stu-id="e53d6-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="e53d6-159">Виртуальная среда Python.</span><span class="sxs-lookup"><span data-stu-id="e53d6-159">Python virtual environment.</span></span> <span data-ttu-id="e53d6-160">Создается при развертывании, если совместимая виртуальная среда еще не создана для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="e53d6-161">Пакеты, указанные в файле requirements.txt, устанавливаются с помощью pip. Однако если они уже установлены, pip не будет выполнять установку.</span><span class="sxs-lookup"><span data-stu-id="e53d6-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="e53d6-162">В следующих 3 разделах описывается разработка веб-приложения в 3 разных средах:</span><span class="sxs-lookup"><span data-stu-id="e53d6-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="e53d6-163">Windows, со средствами Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e53d6-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="e53d6-164">Windows с командной строкой;</span><span class="sxs-lookup"><span data-stu-id="e53d6-164">Windows, with command line</span></span>
* <span data-ttu-id="e53d6-165">Mac и Linux с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="e53d6-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="e53d6-166">Развертывание веб-приложений — Windows — инструменты Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e53d6-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="e53d6-167">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="e53d6-167">Clone the repository</span></span>
<span data-ttu-id="e53d6-168">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e53d6-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="e53d6-169">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="e53d6-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="e53d6-170">Откройте файл решения (SLN-файл), который содержится в корневой папке репозитория.</span><span class="sxs-lookup"><span data-stu-id="e53d6-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="e53d6-171">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="e53d6-171">Create virtual environment</span></span>
<span data-ttu-id="e53d6-172">Теперь мы создадим виртуальную среду для локальной разработки веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e53d6-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="e53d6-173">Щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add Virtual Environment...** (Добавить виртуальную среду...).</span><span class="sxs-lookup"><span data-stu-id="e53d6-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="e53d6-174">Убедитесь, что имя среды — `env`.</span><span class="sxs-lookup"><span data-stu-id="e53d6-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="e53d6-175">Выберите базовый интерпретатор.</span><span class="sxs-lookup"><span data-stu-id="e53d6-175">Select the base interpreter.</span></span> <span data-ttu-id="e53d6-176">Убедитесь, что используется та же версия Python, которая выбрана для веб-приложения (в файле runtime.txt или в колонке **Параметры приложения** веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="e53d6-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="e53d6-177">Убедитесь, что установлен флажок для скачивания и установки пакетов.</span><span class="sxs-lookup"><span data-stu-id="e53d6-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="e53d6-178">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e53d6-178">Click **Create**.</span></span> <span data-ttu-id="e53d6-179">Таким образом будет создана виртуальная среда и установлены зависимости из файла requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="e53d6-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="e53d6-180">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="e53d6-180">Run using development server</span></span>
<span data-ttu-id="e53d6-181">Нажмите клавишу F5, чтобы начать отладку, и браузер автоматически откроет страницу, запущенную локально.</span><span class="sxs-lookup"><span data-stu-id="e53d6-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="e53d6-182">Можно установить точки останова в источниках, использовать окна контрольных значений и т. д. Дополнительные сведения о различных функциях см. в [документации по средствам Python для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="e53d6-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="e53d6-183">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="e53d6-183">Make changes</span></span>
<span data-ttu-id="e53d6-184">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="e53d6-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="e53d6-185">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="e53d6-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="e53d6-186">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="e53d6-186">Install more packages</span></span>
<span data-ttu-id="e53d6-187">Зависимости приложений могут не ограничиваться Python и Bottle.</span><span class="sxs-lookup"><span data-stu-id="e53d6-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="e53d6-188">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="e53d6-188">You can install additional packages using pip.</span></span> <span data-ttu-id="e53d6-189">Чтобы установить пакет, щелкните правой кнопкой мыши в виртуальной среде и выберите **Установить пакет Python**.</span><span class="sxs-lookup"><span data-stu-id="e53d6-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="e53d6-190">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине и другим службам Azure, введите `azure`:</span><span class="sxs-lookup"><span data-stu-id="e53d6-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="e53d6-191">Щелкните правой кнопкой мыши в виртуальной среде и выберите **Создать файл requirements.txt** , чтобы обновить файл requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="e53d6-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="e53d6-192">Затем сохраните внесенные в этот файл изменения в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="e53d6-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="e53d6-193">Развернуть в Azure</span><span class="sxs-lookup"><span data-stu-id="e53d6-193">Deploy to Azure</span></span>
<span data-ttu-id="e53d6-194">Чтобы запустить развертывание, щелкните **Синхронизировать** или **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="e53d6-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="e53d6-195">При синхронизации выполняется как принудительная отправка, так и применение по запросу.</span><span class="sxs-lookup"><span data-stu-id="e53d6-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="e53d6-196">Первое развертывание может занять некоторое время, необходимое для создания виртуальной среды, установку пакетов и т. д.</span><span class="sxs-lookup"><span data-stu-id="e53d6-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="e53d6-197">В Visual Studio не отображается ход выполнения развертывания.</span><span class="sxs-lookup"><span data-stu-id="e53d6-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="e53d6-198">Сведения о том, как можно просмотреть результат, см. в разделе [Устранение неполадок — развертывание](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="e53d6-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="e53d6-199">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="e53d6-200">Разработка веб-приложения — Windows — командная строка</span><span class="sxs-lookup"><span data-stu-id="e53d6-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="e53d6-201">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="e53d6-201">Clone the repository</span></span>
<span data-ttu-id="e53d6-202">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure, а затем добавьте репозиторий Azure в качестве удаленного.</span><span class="sxs-lookup"><span data-stu-id="e53d6-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="e53d6-203">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="e53d6-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="e53d6-204">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="e53d6-204">Create virtual environment</span></span>
<span data-ttu-id="e53d6-205">Давайте создадим новую виртуальную среду для разработки (не добавляйте ее в репозиторий).</span><span class="sxs-lookup"><span data-stu-id="e53d6-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="e53d6-206">Виртуальные среды на языке Python нельзя перемещать, поэтому каждому разработчику, работающему над приложением, будет необходимо создать такую среду локально.</span><span class="sxs-lookup"><span data-stu-id="e53d6-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="e53d6-207">Убедитесь, что используется та же версия Python, которая была выбрана для вашего веб-приложения (в файле runtime.txt или в колонке "Параметры приложения" веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="e53d6-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="e53d6-208">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="e53d6-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="e53d6-209">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="e53d6-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="e53d6-210">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-210">Install any external packages required by your application.</span></span> <span data-ttu-id="e53d6-211">Чтобы установить пакеты в своей виртуальной среде, вы можете использовать файл requirements.txt в корне репозитория:</span><span class="sxs-lookup"><span data-stu-id="e53d6-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="e53d6-212">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="e53d6-212">Run using development server</span></span>
<span data-ttu-id="e53d6-213">Вы можете запустить приложение на сервере разработки с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e53d6-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="e53d6-214">В консоли отобразится URL-адрес и порт, который прослушивает сервер:</span><span class="sxs-lookup"><span data-stu-id="e53d6-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="e53d6-215">Далее откройте браузер и введите этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e53d6-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="e53d6-216">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="e53d6-216">Make changes</span></span>
<span data-ttu-id="e53d6-217">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="e53d6-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="e53d6-218">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="e53d6-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="e53d6-219">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="e53d6-219">Install more packages</span></span>
<span data-ttu-id="e53d6-220">Зависимости приложений могут не ограничиваться Python и Bottle.</span><span class="sxs-lookup"><span data-stu-id="e53d6-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="e53d6-221">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="e53d6-221">You can install additional packages using pip.</span></span> <span data-ttu-id="e53d6-222">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине, а также другим службам Azure, введите:</span><span class="sxs-lookup"><span data-stu-id="e53d6-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="e53d6-223">Обязательно обновите файл requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="e53d6-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="e53d6-224">Примените изменения:</span><span class="sxs-lookup"><span data-stu-id="e53d6-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="e53d6-225">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="e53d6-225">Deploy to Azure</span></span>
<span data-ttu-id="e53d6-226">Чтобы запустить развертывание, принудительно отправьте эти изменения в Azure:</span><span class="sxs-lookup"><span data-stu-id="e53d6-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="e53d6-227">Отобразятся выходные данные сценария развертывания, а также создание виртуальной среды, установку пакетов, и создание файла web.config.</span><span class="sxs-lookup"><span data-stu-id="e53d6-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="e53d6-228">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="e53d6-229">Разработка веб-приложения — Mac/Linux — командная строка</span><span class="sxs-lookup"><span data-stu-id="e53d6-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="e53d6-230">Клонирование репозитория</span><span class="sxs-lookup"><span data-stu-id="e53d6-230">Clone the repository</span></span>
<span data-ttu-id="e53d6-231">Сначала клонируйте репозиторий, используя URL-адрес на портале Azure, а затем добавьте репозиторий Azure в качестве удаленного.</span><span class="sxs-lookup"><span data-stu-id="e53d6-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="e53d6-232">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="e53d6-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="e53d6-233">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="e53d6-233">Create virtual environment</span></span>
<span data-ttu-id="e53d6-234">Давайте создадим новую виртуальную среду для разработки (не добавляйте ее в репозиторий).</span><span class="sxs-lookup"><span data-stu-id="e53d6-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="e53d6-235">Виртуальные среды на языке Python нельзя перемещать, поэтому каждому разработчику, работающему над приложением, будет необходимо создать такую среду локально.</span><span class="sxs-lookup"><span data-stu-id="e53d6-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="e53d6-236">Убедитесь, что используется та же версия Python, которая выбрана для веб-приложения (в файле runtime.txt или в колонке "Параметры приложения" веб-приложения на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="e53d6-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="e53d6-237">Для Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="e53d6-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="e53d6-238">Для Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="e53d6-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="e53d6-239">или pyvenv env</span><span class="sxs-lookup"><span data-stu-id="e53d6-239">or pyvenv env</span></span>

<span data-ttu-id="e53d6-240">Установите все внешние пакеты, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-240">Install any external packages required by your application.</span></span> <span data-ttu-id="e53d6-241">Чтобы установить пакеты в своей виртуальной среде, вы можете использовать файл requirements.txt в корне репозитория:</span><span class="sxs-lookup"><span data-stu-id="e53d6-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="e53d6-242">Запуск приложения на сервере разработки</span><span class="sxs-lookup"><span data-stu-id="e53d6-242">Run using development server</span></span>
<span data-ttu-id="e53d6-243">Вы можете запустить приложение на сервере разработки с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e53d6-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="e53d6-244">В консоли отобразится URL-адрес и порт, который прослушивает сервер:</span><span class="sxs-lookup"><span data-stu-id="e53d6-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="e53d6-245">Далее откройте браузер и введите этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e53d6-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="e53d6-246">Внесение изменений</span><span class="sxs-lookup"><span data-stu-id="e53d6-246">Make changes</span></span>
<span data-ttu-id="e53d6-247">Теперь вы можете поэкспериментировать, внося изменения в исходные коды и/или шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="e53d6-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="e53d6-248">После тестирования изменений их необходимо сохранить в репозитории Git:</span><span class="sxs-lookup"><span data-stu-id="e53d6-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="e53d6-249">Установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="e53d6-249">Install more packages</span></span>
<span data-ttu-id="e53d6-250">Зависимости приложений могут не ограничиваться Python и Bottle.</span><span class="sxs-lookup"><span data-stu-id="e53d6-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="e53d6-251">С помощью pip можно установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="e53d6-251">You can install additional packages using pip.</span></span> <span data-ttu-id="e53d6-252">Например, чтобы установить пакет SDK для Azure для Python, который предоставляет доступ к службе хранилища Azure, служебной шине, а также другим службам Azure, введите:</span><span class="sxs-lookup"><span data-stu-id="e53d6-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="e53d6-253">Обязательно обновите файл requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="e53d6-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="e53d6-254">Примените изменения:</span><span class="sxs-lookup"><span data-stu-id="e53d6-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="e53d6-255">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="e53d6-255">Deploy to Azure</span></span>
<span data-ttu-id="e53d6-256">Чтобы запустить развертывание, принудительно отправьте эти изменения в Azure:</span><span class="sxs-lookup"><span data-stu-id="e53d6-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="e53d6-257">Отобразятся выходные данные сценария развертывания, а также создание виртуальной среды, установку пакетов, и создание файла web.config.</span><span class="sxs-lookup"><span data-stu-id="e53d6-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="e53d6-258">Перейдите по URL-адресу Azure, чтобы просмотреть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="e53d6-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="e53d6-259">Устранение неполадок — установка пакета</span><span class="sxs-lookup"><span data-stu-id="e53d6-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="e53d6-260">Устранение неполадок — виртуальная среда</span><span class="sxs-lookup"><span data-stu-id="e53d6-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="e53d6-261">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e53d6-261">Next Steps</span></span>
<span data-ttu-id="e53d6-262">Используйте следующие ссылки, чтобы узнать больше о средствах Bottle и Python для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e53d6-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="e53d6-263">[Документация по работе с Bottle]</span><span class="sxs-lookup"><span data-stu-id="e53d6-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="e53d6-264">[документации по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e53d6-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="e53d6-265">Дополнительную информацию об использовании табличного хранилища Azure и MongoDB см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="e53d6-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="e53d6-266">[Использование Bottle и MongoDB в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e53d6-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="e53d6-267">[Использование Bottle и табличного хранилища Azure в Azure с помощью инструментов Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e53d6-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e53d6-268">Изменения</span><span class="sxs-lookup"><span data-stu-id="e53d6-268">What's changed</span></span>
* <span data-ttu-id="e53d6-269">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e53d6-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="e53d6-270">[Использование Bottle и MongoDB в Azure с помощью инструментов Python для Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="e53d6-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="e53d6-271">[Использование Bottle и табличного хранилища Azure в Azure с помощью инструментов Python для Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="e53d6-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="e53d6-272">[пакет SDK для Azure для Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="e53d6-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="e53d6-273">[пакет SDK для Azure для Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="e53d6-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="e53d6-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="e53d6-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="e53d6-275">[Git для Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="e53d6-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="e53d6-276">[GitHub для Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="e53d6-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="e53d6-277">[средствами Python для Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="e53d6-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="e53d6-278">[инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="e53d6-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="e53d6-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="e53d6-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="e53d6-280">[документации по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="e53d6-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="e53d6-281">[Документация по работе с Bottle]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="e53d6-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

