---
title: "Использование агентов виртуальных машин для непрерывной интеграции с Jenkins."
description: "Агенты виртуальных машин Azure в качестве подчиненных модулей Jenkins."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 0b22a559fbc03158a6d4398603d1a7d2874d7b67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="21efd-103">Использование агентов виртуальных машин для непрерывной интеграции с Jenkins.</span><span class="sxs-lookup"><span data-stu-id="21efd-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="21efd-104">В этом кратком руководстве объясняется, как с помощью подключаемого модуля агентов виртуальных машин Azure для Jenkins создать в Azure агент Linux (Ubuntu) по запросу.</span><span class="sxs-lookup"><span data-stu-id="21efd-104">This quickstart shows how to use the Jenkins Azure VM Agents plugin to create an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21efd-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="21efd-105">Prerequisites</span></span>

<span data-ttu-id="21efd-106">Ниже указаны требования для работы с руководством.</span><span class="sxs-lookup"><span data-stu-id="21efd-106">To complete this quickstart:</span></span>

* <span data-ttu-id="21efd-107">Если главный модуль Jenkins еще не создан, можно начать с [шаблона решения](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="21efd-107">If you do not already have a Jenkins master, you can start with the [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="21efd-108">Если у вас еще нет субъекта-службы Azure, см. статью [Создание субъекта-службы Azure с помощью Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="21efd-108">Refer to [Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="21efd-109">Установка подключаемого модуля агентов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="21efd-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="21efd-110">Если вы начали с [шаблона решения](install-jenkins-solution-template.md), подключаемый модуль агентов виртуальных машин Azure устанавливается в главном модуле Jenkins.</span><span class="sxs-lookup"><span data-stu-id="21efd-110">If you start from the [Solution Template](install-jenkins-solution-template.md), the Azure VM Agent plugin is installed in the Jenkins master.</span></span>

<span data-ttu-id="21efd-111">Если нет, установите подключаемый модуль **агентов виртуальных машин** с панели мониторинга Jenkins.</span><span class="sxs-lookup"><span data-stu-id="21efd-111">Otherwise, install the **Azure VM Agents** plugin from within the Jenkins dashboard.</span></span>

## <a name="configure-the-plugin"></a><span data-ttu-id="21efd-112">Настройка подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="21efd-112">Configure the plugin</span></span>

* <span data-ttu-id="21efd-113">На панели мониторинга Jenkins последовательно выберите элементы **Manage Jenkins (Управление Jenkins) -> Configure System (Настройка системы) ->**.</span><span class="sxs-lookup"><span data-stu-id="21efd-113">Within the Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="21efd-114">Прокрутите до нижней части страницы и найдите раздел с раскрывающимся списком **Add new cloud** (Добавление нового облака).</span><span class="sxs-lookup"><span data-stu-id="21efd-114">Scroll to the bottom of the page and find the section with the dropdown **Add new cloud**.</span></span> <span data-ttu-id="21efd-115">В меню выберите **Microsoft Azure VM Agents** (Агенты виртуальных машин Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="21efd-115">From the menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="21efd-116">Выберите существующую учетную запись из раскрывающегося списка учетных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="21efd-116">Select an existing account from the Azure Credentials dropdown.</span></span>  <span data-ttu-id="21efd-117">Чтобы добавить новый **субъект-службу Microsoft Azure**, введите следующие значения: идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="21efd-117">To add a new **Microsoft Azure Service Principal,** enter the following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Учетные данные Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="21efd-119">Нажмите кнопку **Verify configuration** (Проверить конфигурацию), чтобы убедиться в правильности конфигурации профиля.</span><span class="sxs-lookup"><span data-stu-id="21efd-119">Click **Verify configuration** to make sure that the profile configuration is correct.</span></span>
* <span data-ttu-id="21efd-120">Сохраните конфигурацию и перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="21efd-120">Save the configuration, and continue to the next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="21efd-121">Конфигурация шаблона</span><span class="sxs-lookup"><span data-stu-id="21efd-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="21efd-122">Общая конфигурация</span><span class="sxs-lookup"><span data-stu-id="21efd-122">General configuration</span></span>
<span data-ttu-id="21efd-123">Настройте шаблон для определения агента виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="21efd-123">Next, configure a template for use to define an Azure VM agent.</span></span> 

* <span data-ttu-id="21efd-124">Нажмите кнопку **Добавить**, чтобы добавить шаблон.</span><span class="sxs-lookup"><span data-stu-id="21efd-124">Click **Add** to add a template.</span></span> 
* <span data-ttu-id="21efd-125">Введите имя нового шаблона.</span><span class="sxs-lookup"><span data-stu-id="21efd-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="21efd-126">В поле метки введите ubuntu.</span><span class="sxs-lookup"><span data-stu-id="21efd-126">For the label, enter  "ubuntu."</span></span> <span data-ttu-id="21efd-127">Эта метка используется во время настройки задания.</span><span class="sxs-lookup"><span data-stu-id="21efd-127">This label is used during the job configuration.</span></span>
* <span data-ttu-id="21efd-128">Выберите нужный регион в поле со списком.</span><span class="sxs-lookup"><span data-stu-id="21efd-128">Select the desired region from the combo box.</span></span>
* <span data-ttu-id="21efd-129">Выберите нужный размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="21efd-129">Select the desired VM size.</span></span>
* <span data-ttu-id="21efd-130">Укажите имя учетной записи хранения Azure или оставьте это поле пустым, чтобы по умолчанию использовать значение jenkinsarmst.</span><span class="sxs-lookup"><span data-stu-id="21efd-130">Specify the Azure Storage account name or leave it blank to use the default name "jenkinsarmst."</span></span>
* <span data-ttu-id="21efd-131">Укажите период удержания в минутах.</span><span class="sxs-lookup"><span data-stu-id="21efd-131">Specify the retention time in minutes.</span></span> <span data-ttu-id="21efd-132">Этот параметр определяет время ожидания (в минутах) Jenkins перед автоматическим удалением неактивного агента.</span><span class="sxs-lookup"><span data-stu-id="21efd-132">This setting defines the number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="21efd-133">Укажите 0, если не хотите, чтобы неактивные агенты удалялись автоматически.</span><span class="sxs-lookup"><span data-stu-id="21efd-133">Specify 0 if you do not want idle agents to be deleted automatically.</span></span>

![Общая конфигурация](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="21efd-135">Конфигурация образа</span><span class="sxs-lookup"><span data-stu-id="21efd-135">Image configuration</span></span>

<span data-ttu-id="21efd-136">Чтобы создать агент Linux (Ubuntu), выберите **Image reference** (Ссылка на образ) и используйте в качестве примера указанную ниже конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="21efd-136">To create a Linux (Ubuntu) agent, select **Image reference** and use the following configuration as an example.</span></span> <span data-ttu-id="21efd-137">Последние поддерживаемые образы Azure см. в [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1).</span><span class="sxs-lookup"><span data-stu-id="21efd-137">Refer to [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for the latest Azure supported images.</span></span>

* <span data-ttu-id="21efd-138">Издатель образа: Canonical</span><span class="sxs-lookup"><span data-stu-id="21efd-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="21efd-139">Предложение образа: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="21efd-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="21efd-140">Номер SKU образа: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="21efd-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="21efd-141">Версия образа виртуальной машины: последняя</span><span class="sxs-lookup"><span data-stu-id="21efd-141">Image version: latest</span></span>
* <span data-ttu-id="21efd-142">Тип ОС: Linux</span><span class="sxs-lookup"><span data-stu-id="21efd-142">OS Type: Linux</span></span>
* <span data-ttu-id="21efd-143">Метод запуска: SSH</span><span class="sxs-lookup"><span data-stu-id="21efd-143">Launch method: SSH</span></span>
* <span data-ttu-id="21efd-144">Укажите учетные данные администратора</span><span class="sxs-lookup"><span data-stu-id="21efd-144">Provide an admin credentials</span></span>
* <span data-ttu-id="21efd-145">При использовании скрипта инициализации виртуальной машины введите:</span><span class="sxs-lookup"><span data-stu-id="21efd-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Конфигурация образа](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="21efd-147">Нажмите кнопку **Verify Template** (Проверить шаблон) для проверки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="21efd-147">Click **Verify Template** to verify the configuration.</span></span>
* <span data-ttu-id="21efd-148">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="21efd-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="21efd-149">Создание задания в Jenkins</span><span class="sxs-lookup"><span data-stu-id="21efd-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="21efd-150">На панели мониторинга Jenkins щелкните элемент **New Item**(Создать элемент).</span><span class="sxs-lookup"><span data-stu-id="21efd-150">Within the Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="21efd-151">Введите имя, выберите **Freestyle project** (Универсальный проект) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21efd-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="21efd-152">На вкладке **General** (Общие сведения) выберите Restrict where project can be run (Ограничения для запуска проекта) и введите для выражения метки значение ubuntu.</span><span class="sxs-lookup"><span data-stu-id="21efd-152">In the **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="21efd-153">Теперь в раскрывающемся списке отображается надпись ubuntu.</span><span class="sxs-lookup"><span data-stu-id="21efd-153">You now see "ubuntu" in the dropdown.</span></span>
* <span data-ttu-id="21efd-154">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="21efd-154">Click **Save**.</span></span>

![Настройка задания](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="21efd-156">Сборка нового проекта</span><span class="sxs-lookup"><span data-stu-id="21efd-156">Build your new project</span></span>

* <span data-ttu-id="21efd-157">Вернитесь на панель мониторинга Jenkins.</span><span class="sxs-lookup"><span data-stu-id="21efd-157">Go back to the Jenkins dashboard.</span></span>
* <span data-ttu-id="21efd-158">Щелкните правой кнопкой мыши созданное задание и выберите команду **Build now** (Собрать).</span><span class="sxs-lookup"><span data-stu-id="21efd-158">Right-click the new job you created, then click **Build now**.</span></span> <span data-ttu-id="21efd-159">Сборка запущена.</span><span class="sxs-lookup"><span data-stu-id="21efd-159">A build is kicked off.</span></span> 
* <span data-ttu-id="21efd-160">По завершении сборки перейдите к окну **Console output** (Вывод на консоль).</span><span class="sxs-lookup"><span data-stu-id="21efd-160">Once the build is complete, go to **Console output**.</span></span> <span data-ttu-id="21efd-161">Вы увидите, что сборка выполнена в Azure удаленно.</span><span class="sxs-lookup"><span data-stu-id="21efd-161">You see that the build was performed remotely on Azure.</span></span>

![Вывод на консоль](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="21efd-163">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="21efd-163">Reference</span></span>

* <span data-ttu-id="21efd-164">Пятничное видео Azure: [Continuous Integration with Jenkins Using Azure VM Agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Непрерывная интеграция с Jenkins при помощи агентов виртуальных машин Azure)</span><span class="sxs-lookup"><span data-stu-id="21efd-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="21efd-165">Сведения о поддержке и параметры конфигурации: [вики-сайт по использованию подключаемого модуля Jenkins с агентами виртуальных машин Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="21efd-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

