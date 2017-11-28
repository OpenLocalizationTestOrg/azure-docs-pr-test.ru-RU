---
title: "агенты ВМ Azure aaaUse для непрерывная интеграция с Jenkins."
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
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="df434-103">Использование агентов виртуальных машин для непрерывной интеграции с Jenkins.</span><span class="sxs-lookup"><span data-stu-id="df434-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="df434-104">Это краткое руководство показывает, как toouse hello toocreate подключаемый модуль агента ВМ Jenkins агент Linux (Ubuntu) по запросу в Azure.</span><span class="sxs-lookup"><span data-stu-id="df434-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df434-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="df434-105">Prerequisites</span></span>

<span data-ttu-id="df434-106">toocomplete краткого руководства:</span><span class="sxs-lookup"><span data-stu-id="df434-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="df434-107">Если главный Jenkins еще нет можно начать с hello [шаблон решения](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="df434-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="df434-108">См. слишком[создании субъекта-службы Azure с помощью Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) Если вы еще не участника-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="df434-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="df434-109">Установка подключаемого модуля агентов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="df434-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="df434-110">При запуске из hello [шаблон решения](install-jenkins-solution-template.md), подключаемый модуль агента ВМ Azure hello устанавливается в базе данных master Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="df434-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="df434-111">В противном случае установка hello **агента ВМ** подключаемого модуля из панели мониторинга Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="df434-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="df434-112">Настроить подключаемый модуль hello</span><span class="sxs-lookup"><span data-stu-id="df434-112">Configure hello plugin</span></span>

* <span data-ttu-id="df434-113">Панели мониторинга Jenkins hello, нажмите кнопку **Jenkins управления -> Настройка системы ->**.</span><span class="sxs-lookup"><span data-stu-id="df434-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="df434-114">Прокрутите toohello внизу страницы hello и найдите раздел hello с раскрывающимся hello **Добавление нового облака**.</span><span class="sxs-lookup"><span data-stu-id="df434-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="df434-115">Меню "hello" выберите **агенты ВМ Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="df434-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="df434-116">Выберите существующую учетную запись из раскрывающегося списка hello учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="df434-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="df434-117">tooadd новый **субъекта-службы Microsoft Azure,** введите hello следующие значения: идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="df434-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Учетные данные Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="df434-119">Нажмите кнопку **Проверьте конфигурацию** toomake правильность конфигурации профиля hello.</span><span class="sxs-lookup"><span data-stu-id="df434-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="df434-120">Сохранить конфигурацию hello и продолжить toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="df434-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="df434-121">Конфигурация шаблона</span><span class="sxs-lookup"><span data-stu-id="df434-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="df434-122">Общая конфигурация</span><span class="sxs-lookup"><span data-stu-id="df434-122">General configuration</span></span>
<span data-ttu-id="df434-123">Настройте шаблон для использования toodefine агента ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="df434-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="df434-124">Нажмите кнопку **добавить** tooadd шаблона.</span><span class="sxs-lookup"><span data-stu-id="df434-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="df434-125">Введите имя нового шаблона.</span><span class="sxs-lookup"><span data-stu-id="df434-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="df434-126">Для метки hello введите «ubuntu.»</span><span class="sxs-lookup"><span data-stu-id="df434-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="df434-127">Эта метка используется во время настройки задания hello.</span><span class="sxs-lookup"><span data-stu-id="df434-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="df434-128">Выберите нужный регион hello со списком «hello».</span><span class="sxs-lookup"><span data-stu-id="df434-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="df434-129">Выберите hello желаемый размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="df434-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="df434-130">Укажите имя учетной записи хранилища Azure hello, или оставьте имя по умолчанию hello пустой toouse «jenkinsarmst».</span><span class="sxs-lookup"><span data-stu-id="df434-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="df434-131">Укажите срок хранения hello в минутах.</span><span class="sxs-lookup"><span data-stu-id="df434-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="df434-132">Этот параметр определяет hello число минут ожидания Jenkins перед автоматическое удаление неактивных агента.</span><span class="sxs-lookup"><span data-stu-id="df434-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="df434-133">Укажите 0, если не требуется toobe простоя агентов, удаляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="df434-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![Общая конфигурация](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="df434-135">Конфигурация образа</span><span class="sxs-lookup"><span data-stu-id="df434-135">Image configuration</span></span>

<span data-ttu-id="df434-136">Выберите toocreate агент Linux (Ubuntu) **изображения ссылку** и hello используется следующая конфигурация в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="df434-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="df434-137">См. слишком[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello Azure последние поддерживаемые изображения.</span><span class="sxs-lookup"><span data-stu-id="df434-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="df434-138">Издатель образа: Canonical</span><span class="sxs-lookup"><span data-stu-id="df434-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="df434-139">Предложение образа: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="df434-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="df434-140">Номер SKU образа: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="df434-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="df434-141">Версия образа виртуальной машины: последняя</span><span class="sxs-lookup"><span data-stu-id="df434-141">Image version: latest</span></span>
* <span data-ttu-id="df434-142">Тип ОС: Linux</span><span class="sxs-lookup"><span data-stu-id="df434-142">OS Type: Linux</span></span>
* <span data-ttu-id="df434-143">Метод запуска: SSH</span><span class="sxs-lookup"><span data-stu-id="df434-143">Launch method: SSH</span></span>
* <span data-ttu-id="df434-144">Укажите учетные данные администратора</span><span class="sxs-lookup"><span data-stu-id="df434-144">Provide an admin credentials</span></span>
* <span data-ttu-id="df434-145">При использовании скрипта инициализации виртуальной машины введите:</span><span class="sxs-lookup"><span data-stu-id="df434-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Конфигурация образа](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="df434-147">Нажмите кнопку **Проверка шаблона** tooverify hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df434-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="df434-148">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df434-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="df434-149">Создание задания в Jenkins</span><span class="sxs-lookup"><span data-stu-id="df434-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="df434-150">Панели мониторинга Jenkins hello, нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="df434-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="df434-151">Введите имя, выберите **Freestyle project** (Универсальный проект) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="df434-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="df434-152">В hello **Общие** вкладки, выберите «Ограничить, где проект может работать» и тип «ubuntu» в выражении метки.</span><span class="sxs-lookup"><span data-stu-id="df434-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="df434-153">Теперь отображается «ubuntu» в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="df434-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="df434-154">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df434-154">Click **Save**.</span></span>

![Настройка задания](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="df434-156">Сборка нового проекта</span><span class="sxs-lookup"><span data-stu-id="df434-156">Build your new project</span></span>

* <span data-ttu-id="df434-157">Вы можете вернуться toohello Jenkins мониторинга.</span><span class="sxs-lookup"><span data-stu-id="df434-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="df434-158">Создать новое задание hello щелкните правой кнопкой мыши, нажмите кнопку **сборки теперь**.</span><span class="sxs-lookup"><span data-stu-id="df434-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="df434-159">Сборка запущена.</span><span class="sxs-lookup"><span data-stu-id="df434-159">A build is kicked off.</span></span> 
* <span data-ttu-id="df434-160">После завершения построения hello go слишком**вывод на консоль**.</span><span class="sxs-lookup"><span data-stu-id="df434-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="df434-161">Вы увидите, что сборки hello удаленно выполнялась в Azure.</span><span class="sxs-lookup"><span data-stu-id="df434-161">You see that hello build was performed remotely on Azure.</span></span>

![Вывод на консоль](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="df434-163">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="df434-163">Reference</span></span>

* <span data-ttu-id="df434-164">Пятничное видео Azure: [Continuous Integration with Jenkins Using Azure VM Agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Непрерывная интеграция с Jenkins при помощи агентов виртуальных машин Azure)</span><span class="sxs-lookup"><span data-stu-id="df434-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="df434-165">Сведения о поддержке и параметры конфигурации: [вики-сайт по использованию подключаемого модуля Jenkins с агентами виртуальных машин Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="df434-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

