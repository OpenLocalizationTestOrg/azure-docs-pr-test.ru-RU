---
title: "Учебник aaaPython термосе web приложения для Azure Cosmos DB | Документы Microsoft"
description: "Просмотрите базы данных учебник по использованию Azure Cosmos DB toostore и доступ к данным из термосе Python веб-приложения, размещенные в Azure. Найдите решения для разработки приложений."
keywords: "Разработка приложений, Python Flask, веб-приложение Python, разработка веб-приложения Python"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="30805-105">Создание веб-приложения Python Flask с использованием Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="30805-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30805-106">.NET</span><span class="sxs-lookup"><span data-stu-id="30805-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="30805-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="30805-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="30805-108">Java</span><span class="sxs-lookup"><span data-stu-id="30805-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="30805-109">Python</span><span class="sxs-lookup"><span data-stu-id="30805-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="30805-110">Этот учебник показывает, как веб-приложения, размещенные в Azure toouse Azure Cosmos DB toostore и доступ к данным из Python и предполагает, что имеются некоторые опыта работы с Python и веб-сайты Azure.</span><span class="sxs-lookup"><span data-stu-id="30805-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="30805-111">В этом учебнике по базам данных рассматриваются следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="30805-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="30805-112">Создание и подготовка учетной записи Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="30805-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="30805-113">Создание приложения Python Flask.</span><span class="sxs-lookup"><span data-stu-id="30805-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="30805-114">Подключение tooand с помощью Cosmos DB из веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="30805-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="30805-115">Развертывание приложения tooAzure hello web.</span><span class="sxs-lookup"><span data-stu-id="30805-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="30805-116">Выполнив этот учебник, вы создадите простое приложение голосования, которое позволяет вам toovote для опроса.</span><span class="sxs-lookup"><span data-stu-id="30805-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![Снимок экрана: hello голосования приложения, созданные с учебником базы данных](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="30805-118">Предварительные требования для учебника по базам данных</span><span class="sxs-lookup"><span data-stu-id="30805-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="30805-119">Перед выполнением инструкции hello в этой статье, следует убедиться, что имеется hello установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="30805-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="30805-120">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="30805-120">An active Azure account.</span></span> <span data-ttu-id="30805-121">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="30805-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="30805-122">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30805-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="30805-123">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="30805-123">OR</span></span> 

    <span data-ttu-id="30805-124">Локальная установка hello [DB эмулятор Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="30805-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="30805-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="30805-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="30805-126">[Инструменты Python для Visual Studio](https://github.com/Microsoft/PTVS/)</span><span class="sxs-lookup"><span data-stu-id="30805-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="30805-127">[Пакет Microsoft Azure SDK для Python 2.7](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="30805-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="30805-128">[Python 2.7.13](https://www.python.org/downloads/windows/)</span><span class="sxs-lookup"><span data-stu-id="30805-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="30805-129">При установке Python 2.7 для hello первый раз, убедитесь, что на экране настройки Python 2.7.13 hello, вы выбрали **добавить python.exe tooPath**.</span><span class="sxs-lookup"><span data-stu-id="30805-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Снимок экрана настройки Python 2.7.11 hello, требующие tooPath python.exe tooselect добавить](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="30805-131">[Компилятор Microsoft Visual C++ для Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266)</span><span class="sxs-lookup"><span data-stu-id="30805-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="30805-132">Шаг 1. Создание учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="30805-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="30805-133">Давайте сначала создадим учетную запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="30805-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="30805-134">Если уже есть учетная запись, или при использовании hello эмулятор DB Cosmos Azure для этого учебника, можно пропустить слишком[шаг 2: Создание нового веб-приложения Python термосе](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="30805-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="30805-135">Теперь мы рассмотрим как фоновый toocreate новое веб-приложение термосе Python из hello.</span><span class="sxs-lookup"><span data-stu-id="30805-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="30805-136">Шаг 2. Создание веб-приложения Python Flask</span><span class="sxs-lookup"><span data-stu-id="30805-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="30805-137">В Visual Studio в hello **файл** меню выберите пункт слишком**New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="30805-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="30805-138">Hello **новый проект** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="30805-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="30805-139">Hello левой панели разверните **шаблоны** и затем **Python**, а затем нажмите кнопку **Web**.</span><span class="sxs-lookup"><span data-stu-id="30805-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="30805-140">Выберите **термосе веб-проекта** hello центральной панели, а затем в hello **имя** введите **учебника**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="30805-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="30805-141">Помните, что имена пакетов Python должны быть прописными буквами, как описано в hello [руководстве по стилю для кода Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="30805-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="30805-142">Для этих новых tooPython термосе это платформа разработки веб-приложений, поможет вам быстрее создавать веб-приложения в Python.</span><span class="sxs-lookup"><span data-stu-id="30805-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Снимок окна hello новый проект в Visual Studio с Python, выделенная на hello слева, Python термосе веб-проекта, выбранного в середине hello и учебник hello имя в поле "имя" hello](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="30805-144">В hello **средства Python для Visual Studio** окно, нажмите кнопку **установка в виртуальной среде**.</span><span class="sxs-lookup"><span data-stu-id="30805-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Снимок экрана учебника hello базы данных - средства Python для Visual Studio окно](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="30805-146">В hello **добавьте виртуальной среды** окна, могут принимать значения по умолчанию hello и использования Python 2.7 в качестве базовой среды hello, поскольку PyDocumentDB в настоящее время не поддерживает Python 3.x и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="30805-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="30805-147">При этом устанавливаются необходимые hello Python виртуальную среду для проекта.</span><span class="sxs-lookup"><span data-stu-id="30805-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Снимок экрана учебника hello базы данных - средства Python для Visual Studio окно](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="30805-149">Отображает окно вывода Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` успешно при установке среды hello.</span><span class="sxs-lookup"><span data-stu-id="30805-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="30805-150">Шаг 3: Изменение веб-приложение hello термосе Python</span><span class="sxs-lookup"><span data-stu-id="30805-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="30805-151">Добавление проекта tooyour пакеты Python термосе hello</span><span class="sxs-lookup"><span data-stu-id="30805-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="30805-152">После настройки проекта потребуется tooadd hello необходимые термосе пакетов tooyour проекта, включая pydocumentdb hello пакета Python для DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="30805-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="30805-153">В обозревателе решений откройте файл hello с именем **requirements.txt** и замените содержимое hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="30805-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="30805-154">Сохранить hello **requirements.txt** файла.</span><span class="sxs-lookup"><span data-stu-id="30805-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="30805-155">В обозревателе решений щелкните элемент **env** правой кнопкой мыши и выберите пункт **Install from requirements.txt** (Установить из файла requirements.txt).</span><span class="sxs-lookup"><span data-stu-id="30805-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Снимок экрана, показывающий env (Python 2.7), выбранных при установке из requirements.txt, выделяются в списке hello](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="30805-157">После успешной установки hello в окне вывода отображает hello следующее:</span><span class="sxs-lookup"><span data-stu-id="30805-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="30805-158">В редких случаях могут появиться ошибки в окне вывода hello.</span><span class="sxs-lookup"><span data-stu-id="30805-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="30805-159">В этом случае проверьте ошибки hello связанные toocleanup.</span><span class="sxs-lookup"><span data-stu-id="30805-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="30805-160">Иногда не удается выполнить очистку hello, но по-прежнему будет успешной установки hello (прокрутки вверх tooverify окно вывода hello это).</span><span class="sxs-lookup"><span data-stu-id="30805-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="30805-161">Можно проверить установку, [проверка hello виртуальной среды](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="30805-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="30805-162">Если не удалось установить hello, но hello проверка прошла успешно, это toocontinue ОК.</span><span class="sxs-lookup"><span data-stu-id="30805-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="30805-163">Проверка hello виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="30805-163">Verify hello virtual environment</span></span>
<span data-ttu-id="30805-164">Убедимся, что все установлено правильно.</span><span class="sxs-lookup"><span data-stu-id="30805-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="30805-165">Постройте решение hello, нажав клавиши **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="30805-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="30805-166">После успешного построения hello, запустите hello веб-сайт, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="30805-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="30805-167">Это запускается сервер разработки термосе hello и запускает веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="30805-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="30805-168">Должны появиться после страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="30805-168">You should see hello following page.</span></span>
   
    ![Hello пустой термосе Python веб-разработки проекта отображается в браузере](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="30805-170">Остановить отладку hello веб-сайт, нажав клавишу **Shift**+**F5** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30805-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="30805-171">Создание определений базы данных, коллекции и документа</span><span class="sxs-lookup"><span data-stu-id="30805-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="30805-172">Теперь давайте создадим приложение для голосования, добавив новые файлы и обновив остальные.</span><span class="sxs-lookup"><span data-stu-id="30805-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="30805-173">В обозревателе решений щелкните правой кнопкой мыши hello **учебника** проекта, нажмите кнопку **добавить**, а затем нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="30805-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="30805-174">Выберите **пустой файл Python** и имя файла hello **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="30805-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="30805-175">Добавьте следующие файл forms.py toohello кода hello, а затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="30805-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="30805-176">Добавьте необходимые hello imports tooviews.py</span><span class="sxs-lookup"><span data-stu-id="30805-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="30805-177">В обозревателе решений разверните hello **учебника** папку и откройте hello **views.py** файла.</span><span class="sxs-lookup"><span data-stu-id="30805-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="30805-178">Добавить после импорта инструкций toohello вверху hello hello **views.py** файла, после чего сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="30805-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="30805-179">Эти импортировать Cosmos DB PythonSDK и hello термосе пакетов.</span><span class="sxs-lookup"><span data-stu-id="30805-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="30805-180">Создание базы данных, коллекции и документа</span><span class="sxs-lookup"><span data-stu-id="30805-180">Create database, collection, and document</span></span>
* <span data-ttu-id="30805-181">В по-прежнему **views.py**, добавить следующий код toohello конец файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="30805-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="30805-182">Это обеспечивает создание hello базы данных, используемой формы hello.</span><span class="sxs-lookup"><span data-stu-id="30805-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="30805-183">Не удаляйте из существующего кода hello в **views.py**.</span><span class="sxs-lookup"><span data-stu-id="30805-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="30805-184">Просто добавьте этот элемент toohello.</span><span class="sxs-lookup"><span data-stu-id="30805-184">Simply append this toohello end.</span></span>

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="30805-185">Чтение базы данных, коллекции и документа и отправка формы</span><span class="sxs-lookup"><span data-stu-id="30805-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="30805-186">В по-прежнему **views.py**, добавить следующий код toohello конец файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="30805-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="30805-187">Это заботится настройки формы hello, чтения hello базы данных, коллекции и документа.</span><span class="sxs-lookup"><span data-stu-id="30805-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="30805-188">Не удаляйте из существующего кода hello в **views.py**.</span><span class="sxs-lookup"><span data-stu-id="30805-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="30805-189">Просто добавьте этот элемент toohello.</span><span class="sxs-lookup"><span data-stu-id="30805-189">Simply append this toohello end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a><span data-ttu-id="30805-190">Создать hello HTML-файлы</span><span class="sxs-lookup"><span data-stu-id="30805-190">Create hello HTML files</span></span>
1. <span data-ttu-id="30805-191">В обозревателе решений в hello **учебника** hello щелкните папку правой **шаблоны** папку, нажмите кнопку **добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="30805-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="30805-192">Выберите **HTML-страницу**, а затем в поле введите имя hello **create.html**.</span><span class="sxs-lookup"><span data-stu-id="30805-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="30805-193">Повторите шаги 1 и 2 toocreate двух дополнительных файлов HTML: results.html и vote.html.</span><span class="sxs-lookup"><span data-stu-id="30805-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="30805-194">Добавьте следующий код слишком hello**create.html** в hello `<body>` элемента.</span><span class="sxs-lookup"><span data-stu-id="30805-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="30805-195">В нем будет отображаться сообщение о создании новой базы данных, коллекции и документа.</span><span class="sxs-lookup"><span data-stu-id="30805-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="30805-196">Добавьте следующий код слишком hello**results.html** в hello `<body`> элемент.</span><span class="sxs-lookup"><span data-stu-id="30805-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="30805-197">Он отображает результаты hello hello опроса.</span><span class="sxs-lookup"><span data-stu-id="30805-197">It displays hello results of hello poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="30805-198">Добавьте следующий код слишком hello**vote.html** в hello `<body`> элемент.</span><span class="sxs-lookup"><span data-stu-id="30805-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="30805-199">Он отображает hello опроса и принимает hello голоса.</span><span class="sxs-lookup"><span data-stu-id="30805-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="30805-200">О регистрации hello голосов, hello управление передается через tooviews.py, где мы распознает приведения голос hello и добавить документ hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="30805-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="30805-201">В hello **шаблоны** папка, замените содержимое hello **index.html** hello следующее.</span><span class="sxs-lookup"><span data-stu-id="30805-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="30805-202">Это служит hello стартовая страница для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="30805-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="30805-203">Добавить файл конфигурации и изменить hello \_ \_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="30805-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="30805-204">В обозревателе решений щелкните правой кнопкой мыши hello **учебника** проекта, нажмите кнопку **добавить**, нажмите кнопку **новый элемент**выберите **пустой файл Python**, а затем Имя файла hello **config.py**.</span><span class="sxs-lookup"><span data-stu-id="30805-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="30805-205">Этот файл необходим для работы форм в Flask.</span><span class="sxs-lookup"><span data-stu-id="30805-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="30805-206">Его можно использовать tooprovide секретный ключ.</span><span class="sxs-lookup"><span data-stu-id="30805-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="30805-207">В этом учебнике секретный ключ не требуется.</span><span class="sxs-lookup"><span data-stu-id="30805-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="30805-208">Добавьте следующее hello tooconfig.py код, вам потребуется значения hello tooalter **DOCUMENTDB\_узла** и **DOCUMENTDB\_ключ** hello следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="30805-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="30805-209">В hello [портал Azure](https://portal.azure.com/), перейдите toohello **ключей** колонки, щелкнув **Обзор**, **учетных записей Azure Cosmos DB**, дважды щелкните имя hello из hello toouse учетной записи, а затем нажмите кнопку hello **ключей** кнопку в hello **Essentials** области.</span><span class="sxs-lookup"><span data-stu-id="30805-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="30805-210">В hello **ключей** колонки, hello копирования **URI** значение и вставьте его в hello **config.py** файл как значение hello для hello **DOCUMENTDB\_узла**  свойство.</span><span class="sxs-lookup"><span data-stu-id="30805-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="30805-211">Вернитесь на портал Azure, в hello hello **ключей** колонке значение hello копирования hello **первичного ключа** или hello **вторичный ключ**и вставьте его в hello **config.py**  файл как значение hello для hello **DOCUMENTDB\_ключ** свойство.</span><span class="sxs-lookup"><span data-stu-id="30805-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="30805-212">В hello  **\_ \_init\_\_.py** файла, добавление следующей строкой hello.</span><span class="sxs-lookup"><span data-stu-id="30805-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="30805-213">Таким образом, содержимое hello hello файла:</span><span class="sxs-lookup"><span data-stu-id="30805-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="30805-214">После добавления всех файлов hello, обозреватель решений должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="30805-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Снимок экрана: hello окно обозревателя решений Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="30805-216">Шаг 4. Локальный запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="30805-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="30805-217">Постройте решение hello, нажав клавиши **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="30805-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="30805-218">После успешного построения hello, запустите hello веб-сайт, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="30805-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="30805-219">На экране появится следующее hello.</span><span class="sxs-lookup"><span data-stu-id="30805-219">You should see hello following on your screen.</span></span>
   
    ![Здравствуйте, Python + Cosmos DB голосования приложения Azure отображается в веб-браузере снимок экрана](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="30805-221">Нажмите кнопку **Create/Clear hello базы данных с правом голоса** базы данных toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="30805-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![Снимок экрана: hello создать страницу веб-приложения hello — сведения о разработке](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="30805-223">Затем нажмите кнопку **Голосовать** и сделайте свой выбор.</span><span class="sxs-lookup"><span data-stu-id="30805-223">Then, click **Vote** and select your option.</span></span>
   
    ![Снимок экрана: hello веб-приложения с голосования осуществлены вопрос](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="30805-225">Для каждого голос, приведении он увеличивает на единицу счетчик соответствующие hello.</span><span class="sxs-lookup"><span data-stu-id="30805-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Снимок экрана: hello результаты показано страницы голос hello](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="30805-227">Остановите отладку проекта hello, нажав клавиши Shift + F5.</span><span class="sxs-lookup"><span data-stu-id="30805-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="30805-228">Шаг 5: Развертывание приложения tooAzure hello web</span><span class="sxs-lookup"><span data-stu-id="30805-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="30805-229">Теперь, когда полное приложение hello правильно работать с Cosmos DB мы будем toodeploy этот tooAzure.</span><span class="sxs-lookup"><span data-stu-id="30805-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="30805-230">Щелкните правой кнопкой мыши проект hello в обозревателе решений (Убедитесь, что вы не еще выполняется локально) и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="30805-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Снимок экрана приветствия учебника, выбранного в обозревателе решений, с помощью параметра hello публикации выделен](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="30805-232">В hello **публикации** установите флажок **службу приложений Microsoft Azure**выберите **создать новый**, а затем нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="30805-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Снимок экрана окна hello публикации веб-сайта с выделенной службу приложений Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="30805-234">В hello **Создание приложения службы** диалогового окна введите имя hello веб-приложения вместе с вашей **подписки**, **группы ресурсов**, и **план служб приложений** , нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="30805-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Снимок экрана окна приложения Microsoft Azure окне приветствия](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="30805-236">Через несколько секунд Visual Studio завершит публикацию вашего приложения и запустит браузер, где вы увидите свое творение, запущенное в Azure!</span><span class="sxs-lookup"><span data-stu-id="30805-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Снимок экрана окна приложения Microsoft Azure окне приветствия](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="30805-238">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="30805-238">Troubleshooting</span></span>
<span data-ttu-id="30805-239">Если это первый Python приложение hello после выполнения на компьютере, убедитесь, что hello следующих папок (или эквивалентная Установка расположения hello) включаются в переменной путь:</span><span class="sxs-lookup"><span data-stu-id="30805-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="30805-240">Если появляется сообщение об ошибке на странице голос, а название проекта что-то отличное от **учебника**, убедитесь, что  **\_ \_init\_\_.py** Исправьте имя проекта в строку hello hello ссылки: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="30805-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30805-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30805-241">Next steps</span></span>
<span data-ttu-id="30805-242">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="30805-242">Congratulations!</span></span> <span data-ttu-id="30805-243">Просто завершения первого Python веб-приложения с помощью Cosmos DB и публикации его tooAzure.</span><span class="sxs-lookup"><span data-stu-id="30805-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="30805-244">Мы регулярно обновляем и улучшаем эту статью на основе ваших отзывов.</span><span class="sxs-lookup"><span data-stu-id="30805-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="30805-245">Один раз после завершения учебника hello, проверьте с помощью кнопки в hello верхней и нижней части этой страницы с правом голоса hello и быть tooinclude убедиться, что ваши отзывы о какие улучшения вы хотите сделать toosee.</span><span class="sxs-lookup"><span data-stu-id="30805-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="30805-246">Если вы хотите нам toocontact напрямую, если вам свободного tooinclude адрес вашей электронной почты в комментарии.</span><span class="sxs-lookup"><span data-stu-id="30805-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="30805-247">tooadd дополнительные функциональные возможности tooyour веб-приложение hello просмотрите API-интерфейса в hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="30805-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="30805-248">Дополнительные сведения о Azure, Visual Studio и Python, в разделе hello [центре разработчиков Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="30805-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="30805-249">Дополнительные руководства термосе Python см. [hello термосе мегабайт-учебнике часть I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="30805-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
