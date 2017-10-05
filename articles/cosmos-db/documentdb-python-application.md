---
title: "Руководство по веб-приложению Python Flask для Azure Cosmos DB | Документация Майкрософт"
description: "Изучите руководство по использованию Azure Cosmos DB для хранения и применения данных из веб-приложения Python Flask, размещенного в Azure. Найдите решения для разработки приложений."
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
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="9e0cd-105">Создание веб-приложения Python Flask с использованием Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9e0cd-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e0cd-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9e0cd-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="9e0cd-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="9e0cd-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="9e0cd-108">Java</span><span class="sxs-lookup"><span data-stu-id="9e0cd-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="9e0cd-109">Python</span><span class="sxs-lookup"><span data-stu-id="9e0cd-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="9e0cd-110">В этом руководстве показан пример использования службы Azure Cosmos DB для хранения данных и доступа к ним из веб-приложения Python, размещенного в Azure. Чтобы эффективно пользоваться этим руководством, нужен некоторый опыт использования Python и веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-110">This tutorial shows you how to use Azure Cosmos DB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="9e0cd-111">В этом учебнике по базам данных рассматриваются следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="9e0cd-112">Создание и подготовка учетной записи Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="9e0cd-113">Создание приложения Python Flask.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="9e0cd-114">Подключение и использование Cosmos DB из веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-114">Connecting to and using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="9e0cd-115">Развертывание веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-115">Deploying the web application to Azure.</span></span>

<span data-ttu-id="9e0cd-116">В ходе учебника вы создадите простое веб-приложение для голосования, позволяющее проводить голосование на выборах.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-116">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![Снимок экрана: веб-приложение для голосования, созданное с помощью этого учебника](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="9e0cd-118">Предварительные требования для учебника по базам данных</span><span class="sxs-lookup"><span data-stu-id="9e0cd-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="9e0cd-119">Перед выполнением инструкций, приведенных в этой статье, следует убедиться, что установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="9e0cd-119">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="9e0cd-120">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-120">An active Azure account.</span></span> <span data-ttu-id="9e0cd-121">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9e0cd-122">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="9e0cd-123">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="9e0cd-123">OR</span></span> 

    <span data-ttu-id="9e0cd-124">Локальная установка [эмулятора Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="9e0cd-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="9e0cd-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="9e0cd-126">[Инструменты Python для Visual Studio](https://github.com/Microsoft/PTVS/)</span><span class="sxs-lookup"><span data-stu-id="9e0cd-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="9e0cd-127">[Пакет Microsoft Azure SDK для Python 2.7](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="9e0cd-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="9e0cd-128">[Python 2.7.13](https://www.python.org/downloads/windows/)</span><span class="sxs-lookup"><span data-stu-id="9e0cd-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9e0cd-129">Если вы устанавливаете Python 2.7 впервые, убедитесь, что на экране Customize Python 2.7.13 (Настройка Python 2.7.13) вы выбрали **Add python.exe to Path** (Добавить файл python.exe к пути).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-129">If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.13 screen, you select **Add python.exe to Path**.</span></span>
> 
> ![Снимок экрана: окно «Настройка Python 2.7.11», где необходимо добавить файл python.exe к пути](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="9e0cd-131">[Компилятор Microsoft Visual C++ для Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266)</span><span class="sxs-lookup"><span data-stu-id="9e0cd-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="9e0cd-132">Шаг 1. Создание учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9e0cd-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="9e0cd-133">Давайте сначала создадим учетную запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="9e0cd-134">Если у вас уже есть учетная запись или вы используете эмулятор Azure Cosmos DB в этом руководстве, можно перейти к разделу [Шаг 2. Создание веб-приложения Python Flask](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-134">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="9e0cd-135">Теперь мы рассмотрим создание веб-приложения Python Flask с нуля.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-135">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="9e0cd-136">Шаг 2. Создание веб-приложения Python Flask</span><span class="sxs-lookup"><span data-stu-id="9e0cd-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="9e0cd-137">В меню Visual Studio **Файл** выберите **Создать**, а затем щелкните **Проект**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="9e0cd-138">Откроется диалоговое окно **Новый проект** .</span><span class="sxs-lookup"><span data-stu-id="9e0cd-138">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="9e0cd-139">На панели слева разверните пункты **Шаблоны** и **Python**, а затем выберите **Веб**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-139">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="9e0cd-140">На центральной панели выберите **веб-проект Flask**, в поле **Имя** введите **tutorial**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-140">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="9e0cd-141">Помните, что в именах пакетов Python используется только нижний регистр, как описано в [руководстве по стилю для кода Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-141">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="9e0cd-142">Для тех, кто не знаком с Python Flask: это платформа, ускоряющая создание веб-приложений в Python.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-142">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Снимок экрана: окно нового проекта в Visual Studio с выделенным типом Python в левой части, выбранным веб-проектом Python Flask в центральной части и названием учебника в поле "Имя"](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="9e0cd-144">В окне **Инструменты Python для Visual Studio** щелкните **Install into a virtual environment** (Установить в виртуальной среде).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-144">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Снимок экрана: учебник — окно средств Python для Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="9e0cd-146">В окне **Add Virtual Environment** (Добавление виртуальной среды) вы можете принять значения по умолчанию и использовать Python 2.7 в качестве базовой среды (так как PyDocumentDB сейчас не поддерживает версию Python 3.x), а затем нажать кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-146">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="9e0cd-147">Для вашего проекта будет настроена требуемая виртуальная среда Python.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-147">This sets up the required Python virtual environment for your project.</span></span>
   
    ![Снимок экрана: учебник — окно средств Python для Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="9e0cd-149">Когда среда будет успешно установлена, в окне вывода отобразится сообщение `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.`</span><span class="sxs-lookup"><span data-stu-id="9e0cd-149">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="9e0cd-150">Шаг 3. Изменение веб-приложения Python Flask</span><span class="sxs-lookup"><span data-stu-id="9e0cd-150">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="9e0cd-151">Добавление пакетов Python Flask в проект</span><span class="sxs-lookup"><span data-stu-id="9e0cd-151">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="9e0cd-152">После настройки параметров проекта нужно добавить к нему ряд необходимых пакетов Flask, включая pydocumentdb — пакет Python для DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-152">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="9e0cd-153">В обозревателе решений откройте файл **requirements.txt** и замените его содержимое приведенным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-153">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
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
2. <span data-ttu-id="9e0cd-154">Сохраните файл **requirements.txt** .</span><span class="sxs-lookup"><span data-stu-id="9e0cd-154">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="9e0cd-155">В обозревателе решений щелкните элемент **env** правой кнопкой мыши и выберите пункт **Install from requirements.txt** (Установить из файла requirements.txt).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Снимок экрана: отображение env (Python 2.7) с выбранной командой "Установить из requirements.txt", выделенной в списке](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="9e0cd-157">После успешной установки в окне вывода отобразятся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="9e0cd-157">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="9e0cd-158">В редких случаях в окне вывода появляется ошибка.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-158">In rare cases, you might see a failure in the output window.</span></span> <span data-ttu-id="9e0cd-159">В этом случае проверьте, связана ли ошибка с очисткой.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-159">If this happens, check if the error is related to cleanup.</span></span> <span data-ttu-id="9e0cd-160">Иногда происходит сбой очистки, но установка все равно завершается успешно (прокрутите окно вывода вверх, чтобы убедиться в этом).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-160">Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this).</span></span> <span data-ttu-id="9e0cd-161">Чтобы определить успешность установки, воспользуйтесь [проверкой виртуальной среды](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-161">You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="9e0cd-162">Если установка завершилась ошибкой, но проверка прошла успешно, можно продолжать работу.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-162">If the installation failed but the verification is successful, it's OK to continue.</span></span>
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="9e0cd-163">Проверка виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="9e0cd-163">Verify the virtual environment</span></span>
<span data-ttu-id="9e0cd-164">Убедимся, что все установлено правильно.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="9e0cd-165">Выполните сборку решения, нажав клавиши **CTRL**+**SHIFT**+**B**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-165">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="9e0cd-166">После успешной сборки запустите веб-сайт, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-166">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="9e0cd-167">Будут запущены сервер разработки Flask и веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-167">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="9e0cd-168">Вы должны увидеть следующую страницу:</span><span class="sxs-lookup"><span data-stu-id="9e0cd-168">You should see the following page.</span></span>
   
    ![Пустой проект веб-приложения Python Flask отображается в браузере](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="9e0cd-170">Остановите отладку веб-сайта в Visual Studio. Для этого нажмите клавиши **SHIFT**+**F5**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-170">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="9e0cd-171">Создание определений базы данных, коллекции и документа</span><span class="sxs-lookup"><span data-stu-id="9e0cd-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="9e0cd-172">Теперь давайте создадим приложение для голосования, добавив новые файлы и обновив остальные.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="9e0cd-173">В обозревателе решений щелкните правой кнопкой мыши проект **tutorial**, выберите пункт **Добавить**, а затем щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-173">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="9e0cd-174">Выберите элемент **Empty Python File** (Пустой файл Python) и присвойте файлу имя **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-174">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="9e0cd-175">Добавьте следующий код в файл forms.py и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-175">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="9e0cd-176">Добавьте необходимые файлы импорта в views.py.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-176">Add the required imports to views.py</span></span>
1. <span data-ttu-id="9e0cd-177">В обозревателе решений разверните папку **tutorial** и откройте файл **views.py**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-177">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="9e0cd-178">Добавьте в начало файла **views.py** приведенные ниже инструкции import и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-178">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="9e0cd-179">Они выполнят импорт пакета SDK для Python и пакетов Flask Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-179">These import Cosmos DB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="9e0cd-180">Создание базы данных, коллекции и документа</span><span class="sxs-lookup"><span data-stu-id="9e0cd-180">Create database, collection, and document</span></span>
* <span data-ttu-id="9e0cd-181">Добавьте в конец файла **views.py** приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-181">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="9e0cd-182">Он отвечает за создание базы данных, используемой формой.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-182">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="9e0cd-183">Не удаляйте существующий код в файле **views.py**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-183">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="9e0cd-184">Просто переместите его в конец.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-184">Simply append this to the end.</span></span>

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="9e0cd-185">Чтение базы данных, коллекции и документа и отправка формы</span><span class="sxs-lookup"><span data-stu-id="9e0cd-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="9e0cd-186">Добавьте в конец файла **views.py** приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-186">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="9e0cd-187">Он служит для настройки формы, чтения базы данных, коллекции и документа.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-187">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="9e0cd-188">Не удаляйте существующий код в файле **views.py**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-188">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="9e0cd-189">Просто переместите его в конец.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-189">Simply append this to the end.</span></span>

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

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
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


### <a name="create-the-html-files"></a><span data-ttu-id="9e0cd-190">Создание HTML-файлов</span><span class="sxs-lookup"><span data-stu-id="9e0cd-190">Create the HTML files</span></span>
1. <span data-ttu-id="9e0cd-191">В обозревателе решений в папке **tutorial** щелкните правой кнопкой мыши папку **templates**, выберите пункт **Добавить**, а затем — **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-191">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="9e0cd-192">Выберите **HTML-страница**, а затем в поле "Имя" введите **create.html**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-192">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="9e0cd-193">Повторите шаги 1 и 2, чтобы создать два дополнительных HTML-файла: results.html и vote.html.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-193">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="9e0cd-194">Добавьте следующий код в файл **create.html** in the `<body>` .</span><span class="sxs-lookup"><span data-stu-id="9e0cd-194">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="9e0cd-195">В нем будет отображаться сообщение о создании новой базы данных, коллекции и документа.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="9e0cd-196">Добавьте следующий код в элемент `<body`>. файла **results.html**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-196">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="9e0cd-197">В нем будут отображаться результаты опроса.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-197">It displays the results of the poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
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
6. <span data-ttu-id="9e0cd-198">Добавьте следующий код в элемент `<body`>. файла **vote.html**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-198">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="9e0cd-199">В нем будет отображаться опрос и приниматься голоса.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-199">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="9e0cd-200">При регистрации голосов управление передается файлу views.py, в котором голоса будут учитываться и, соответственно, добавляться в документ.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-200">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="9e0cd-201">В папке **templates** замените содержимое файла **index.html** приведенным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-201">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="9e0cd-202">Он будет служить главной страницей приложения.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-202">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="9e0cd-203">Добавьте файл конфигурации и измените файл \_\_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="9e0cd-203">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="9e0cd-204">В обозревателе решений щелкните правой кнопкой мыши проект **tutorial**, выберите пункты **Добавить**, **Новый элемент** и **Empty Python File** (Пустой файл Python), а затем введите имя файла **config.py**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-204">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="9e0cd-205">Этот файл необходим для работы форм в Flask.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="9e0cd-206">Кроме того, его можно использовать для предоставления секретного ключа.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-206">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="9e0cd-207">В этом учебнике секретный ключ не требуется.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="9e0cd-208">Добавьте приведенный ниже код в файл config.py. На следующем этапе вам потребуется изменить значения свойств **DOCUMENTDB\_HOST** и **DOCUMENTDB\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-208">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="9e0cd-209">На [портале Azure](https://portal.azure.com/) перейдите в колонку **Ключи**, щелкните **Обзор**, **Azure Cosmos DB Accounts** (Учетные записи Azure Cosmos DB), дважды щелкните имя учетной записи и нажмите кнопку **Ключи** в области **Основные компоненты**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-209">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="9e0cd-210">В колонке **Ключи** скопируйте значение **URI** и вставьте его в файл **config.py** как значение для свойства **DOCUMENTDB\_HOST**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-210">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="9e0cd-211">Вернитесь на портал Azure, перейдите в колонку **Ключи**, скопируйте значение **первичного** или **вторичного ключа** и вставьте его в файл **config.py** как значение для свойства **DOCUMENTDB\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-211">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="9e0cd-212">В файл **\_\_init\_\_.py** добавьте приведенную ниже строку:</span><span class="sxs-lookup"><span data-stu-id="9e0cd-212">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="9e0cd-213">В результате содержимое файла будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="9e0cd-213">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="9e0cd-214">После добавления всех файлов обозреватель решений должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e0cd-214">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Снимок экрана: окно обозревателя решений Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="9e0cd-216">Шаг 4. Локальный запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9e0cd-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="9e0cd-217">Выполните сборку решения, нажав клавиши **CTRL**+**SHIFT**+**B**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-217">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="9e0cd-218">После успешной сборки запустите веб-сайт, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-218">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="9e0cd-219">На экране должно отображаться следующее:</span><span class="sxs-lookup"><span data-stu-id="9e0cd-219">You should see the following on your screen.</span></span>
   
    ![Снимок экрана: Python + приложение для голосования Azure Cosmos DB в веб-браузере](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="9e0cd-221">Щелкните **Создать или очистить базу данных голосования** , чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-221">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![Снимок экрана: страница создания веб-приложения — сведения о разработке](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="9e0cd-223">Затем нажмите кнопку **Голосовать** и сделайте свой выбор.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-223">Then, click **Vote** and select your option.</span></span>
   
    ![Снимок экрана: веб-приложение с заданным вопросом для голосования](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="9e0cd-225">Для каждого учтенного голоса будет увеличиваться соответствующий счетчик.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-225">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![Снимок экрана: страница с результатами голосования](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="9e0cd-227">Остановите отладку проекта, нажав клавиши SHIFT+F5.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-227">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure"></a><span data-ttu-id="9e0cd-228">Шаг 5. Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="9e0cd-228">Step 5: Deploy the web application to Azure</span></span>
<span data-ttu-id="9e0cd-229">Теперь, когда у вас есть готовое приложение и оно корректно работает в Cosmos DB, мы развернем его в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-229">Now that you have the complete application working correctly against Cosmos DB, we're going to deploy this to Azure.</span></span>

1. <span data-ttu-id="9e0cd-230">Правой кнопкой мыши щелкните проект в обозревателе решений (перед этим убедитесь, что он не запущен локально) и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-230">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Снимок экрана: проект tutorial, выбранный в обозревателе решений и с выделенным параметром "Опубликовать"](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="9e0cd-232">В диалоговом окне **Публикация** установите флажок **Служба приложений Microsoft Azure**, выберите **Создать** и нажмите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-232">In the **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Снимок экрана с диалоговым окном "Публикация веб-сайта" с выделенным флажком "Служба приложений Microsoft Azure"](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="9e0cd-234">В окне **Создать службу приложений** введите имя веб-приложения и соответствующую **подписку**, **группу ресурсов** и **план службы приложений**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-234">In the **Create App Service** dialog box, enter the name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Снимок экрана окна "Веб-приложения Microsoft Azure"](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="9e0cd-236">Через несколько секунд Visual Studio завершит публикацию вашего приложения и запустит браузер, где вы увидите свое творение, запущенное в Azure!</span><span class="sxs-lookup"><span data-stu-id="9e0cd-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Снимок экрана окна "Веб-приложения Microsoft Azure"](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="9e0cd-238">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="9e0cd-238">Troubleshooting</span></span>
<span data-ttu-id="9e0cd-239">Если это первое приложение Python, которое вы запускаете на компьютере, убедитесь, что следующие папки (или эквивалентные расположения установки) включены в переменную PATH:</span><span class="sxs-lookup"><span data-stu-id="9e0cd-239">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="9e0cd-240">Если на странице голосования появляется сообщение об ошибке, а имя проекта отличается от **tutorial**, убедитесь, что файл **\_\_init\_\_.py** ссылается на имя нужного проекта в строке `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e0cd-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e0cd-241">Next steps</span></span>
<span data-ttu-id="9e0cd-242">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="9e0cd-242">Congratulations!</span></span> <span data-ttu-id="9e0cd-243">Вы только что закончили свое первое веб-приложение на Python с помощью Cosmos DB и опубликовали его в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-243">You have just completed your first Python web application using Cosmos DB and published it to Azure.</span></span>

<span data-ttu-id="9e0cd-244">Мы регулярно обновляем и улучшаем эту статью на основе ваших отзывов.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="9e0cd-245">После завершения учебника воспользуйтесь кнопками голосования в верхней и нижней части страницы, а также оставьте отзыв о том, что следует улучшить по вашему мнению.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-245">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="9e0cd-246">Если вы хотите, чтобы мы связались с вами, укажите ваш электронный адрес в комментариях.</span><span class="sxs-lookup"><span data-stu-id="9e0cd-246">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="9e0cd-247">Чтобы узнать, как добавить дополнительные функции в веб-приложение, ознакомьтесь с доступными API в [пакете SDK для Python в Azure Cosmos DB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-247">To add additional functionality to your web application, review the APIs available in the [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="9e0cd-248">Дополнительные сведения об Azure, Visual Studio и Python см. в [центре по разработке для Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="9e0cd-248">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="9e0cd-249">Дополнительные руководства по Python Flask: [Мегаруководство по Flask, часть I. Привет, мир!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)</span><span class="sxs-lookup"><span data-stu-id="9e0cd-249">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
