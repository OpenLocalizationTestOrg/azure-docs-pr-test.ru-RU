---
title: "aaaHow toouse hello Azure ведомый подключаемого модуля в непрерывной интеграции Hudson | Документы Microsoft"
description: "Описывает, как подчиненного подключаемого модуля в непрерывной интеграции Hudson toouse hello Azure."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="82495-103">Как toouse hello Azure подчиненного подключаемого модуля в непрерывной интеграции Hudson</span><span class="sxs-lookup"><span data-stu-id="82495-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="82495-104">Hello Azure ведомый подключаемого модуля для Hudson включает узлы ведомый tooprovision в Azure при построении выполнения распределенных.</span><span class="sxs-lookup"><span data-stu-id="82495-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="82495-105">Установка hello Azure ведомый подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="82495-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="82495-106">В hello Hudson панели мониторинга щелкните **управление Hudson**.</span><span class="sxs-lookup"><span data-stu-id="82495-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="82495-107">В hello **управление Hudson** щелкните **управление подключаемыми модулями**.</span><span class="sxs-lookup"><span data-stu-id="82495-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="82495-108">Нажмите кнопку hello **доступно** вкладки.</span><span class="sxs-lookup"><span data-stu-id="82495-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="82495-109">Нажмите кнопку **поиска** и тип **Azure** toolimit hello список toorelevant подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="82495-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="82495-110">В случае tooscroll через hello список доступных подключаемых модулей, вы найдете hello Azure ведомый подключаемого модуля в разделе hello **управления кластером и распределенных построения** раздела hello **другие** вкладку.</span><span class="sxs-lookup"><span data-stu-id="82495-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="82495-111">Установите флажок hello для **подключаемый модуль Azure ведомый**.</span><span class="sxs-lookup"><span data-stu-id="82495-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="82495-112">Щелкните **Install**(Установить).</span><span class="sxs-lookup"><span data-stu-id="82495-112">Click **Install**.</span></span>
7. <span data-ttu-id="82495-113">Перезапустите Hudson.</span><span class="sxs-lookup"><span data-stu-id="82495-113">Restart Hudson.</span></span>

<span data-ttu-id="82495-114">Теперь, "hello" подключаемый модуль установлен, hello дальнейшие действия будет tooconfigure hello подключаемого модуля с помощью профиля подписки Azure и toocreate шаблона, который будет использоваться при создании hello виртуальной Машины для узла ведомый hello.</span><span class="sxs-lookup"><span data-stu-id="82495-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="82495-115">Настройка hello Azure ведомый подключаемого модуля с помощью профиля подписки</span><span class="sxs-lookup"><span data-stu-id="82495-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="82495-116">Профиль подписки также назывались tooas параметры публикации, XML-файл, содержащий ваши учетные данные и Дополнительные сведения, вам потребуется toowork с Azure в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="82495-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="82495-117">tooconfigure hello Azure ведомый подключаемый модуль, необходимо:</span><span class="sxs-lookup"><span data-stu-id="82495-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="82495-118">идентификатор подписки;</span><span class="sxs-lookup"><span data-stu-id="82495-118">Your subscription id</span></span>
* <span data-ttu-id="82495-119">сертификат управления подпиской.</span><span class="sxs-lookup"><span data-stu-id="82495-119">A management certificate for your subscription</span></span>

<span data-ttu-id="82495-120">Эти сведения можно найти в [профиле подписки].</span><span class="sxs-lookup"><span data-stu-id="82495-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="82495-121">Ниже приведен пример профиля подписки.</span><span class="sxs-lookup"><span data-stu-id="82495-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="82495-122">Получив профиле подписки, выполните эти шаги tooconfigure hello Azure ведомый подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="82495-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="82495-123">В hello Hudson панели мониторинга щелкните **управление Hudson**.</span><span class="sxs-lookup"><span data-stu-id="82495-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="82495-124">Щелкните **Configure System**(Настройка системы).</span><span class="sxs-lookup"><span data-stu-id="82495-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="82495-125">Прокрутите вниз hello toofind страницы приветствия **облака** раздела.</span><span class="sxs-lookup"><span data-stu-id="82495-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="82495-126">Щелкните **Add new cloud > Microsoft Azure** (Добавить новое облако > Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="82495-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![добавление нового облака][add new cloud]
   
    <span data-ttu-id="82495-128">При этом будут отображены поля hello, где требуется tooenter сведениях о подписке.</span><span class="sxs-lookup"><span data-stu-id="82495-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![настройка профиля][configure profile]
5. <span data-ttu-id="82495-130">Скопировать hello ИД подписки и управления сертификат профиля подписки и вставьте их в соответствующие поля hello.</span><span class="sxs-lookup"><span data-stu-id="82495-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="82495-131">При копировании hello ИД подписки и управления сертификат, **не** используйте кавычки hello, заключите hello значения.</span><span class="sxs-lookup"><span data-stu-id="82495-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="82495-132">Щелкните **Verify configuration**(Проверить конфигурацию).</span><span class="sxs-lookup"><span data-stu-id="82495-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="82495-133">После проверки конфигурации hello щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="82495-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="82495-134">Настройка шаблона виртуальной машины для hello Azure ведомый подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="82495-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="82495-135">Шаблон виртуальной машины определяет параметры hello hello подключаемый модуль будет использовать toocreate подчиненного узла в Azure.</span><span class="sxs-lookup"><span data-stu-id="82495-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="82495-136">В следующие шаги hello будут созданы шаблон для Виртуальной машине Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="82495-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="82495-137">В hello Hudson панели мониторинга щелкните **управление Hudson**.</span><span class="sxs-lookup"><span data-stu-id="82495-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="82495-138">Щелкните **Configure System**(Настройка системы).</span><span class="sxs-lookup"><span data-stu-id="82495-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="82495-139">Прокрутите вниз hello toofind страницы приветствия **облака** раздела.</span><span class="sxs-lookup"><span data-stu-id="82495-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="82495-140">В рамках hello **облака** найдите **добавить шаблон виртуальной машины Azure** и нажмите кнопку hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="82495-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![добавление шаблона виртуальной машины][add vm template]
5. <span data-ttu-id="82495-142">Укажите имя облачной службы в hello **имя** поля.</span><span class="sxs-lookup"><span data-stu-id="82495-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="82495-143">Если имя hello ссылается tooan существующей облачной службы, службы будут подготовлены hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="82495-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="82495-144">В противном случае Azure создаст новую службу.</span><span class="sxs-lookup"><span data-stu-id="82495-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="82495-145">В hello **описание** введите текст, описывающий шаблон hello, вы создаете.</span><span class="sxs-lookup"><span data-stu-id="82495-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="82495-146">Эти сведения будут использоваться только в информационных целях и при подготовке виртуальной машины не учитываются.</span><span class="sxs-lookup"><span data-stu-id="82495-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="82495-147">В hello **метки** введите **linux**.</span><span class="sxs-lookup"><span data-stu-id="82495-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="82495-148">Эта метка используется tooidentify hello шаблон, который вы создаете и впоследствии используется tooreference hello шаблона при создании задания Hudson.</span><span class="sxs-lookup"><span data-stu-id="82495-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="82495-149">Выберите регион, где будут создаваться hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="82495-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="82495-150">Выберите соответствующий размер виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="82495-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="82495-151">Укажите учетную запись хранилища, где будут создаваться hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="82495-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="82495-152">Убедитесь, что он находится в hello же регионе, что hello облачной службы, вы будете использовать.</span><span class="sxs-lookup"><span data-stu-id="82495-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="82495-153">Если требуется новый toobe хранилища создана, это поле можно оставить пустым.</span><span class="sxs-lookup"><span data-stu-id="82495-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="82495-154">Время хранения указывает hello количество минут, прежде чем Hudson удаляет ведомый простоя.</span><span class="sxs-lookup"><span data-stu-id="82495-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="82495-155">Оставьте значение по умолчанию hello 60.</span><span class="sxs-lookup"><span data-stu-id="82495-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="82495-156">В **использование**, выберите hello соответствующее условие, если будет использоваться этот подчиненный узел.</span><span class="sxs-lookup"><span data-stu-id="82495-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="82495-157">На этом этапе выберите вариант **Utilize this node as much as possible**(Использовать этот узел постоянно).</span><span class="sxs-lookup"><span data-stu-id="82495-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="82495-158">На этом этапе в форму будет выглядеть напоминает toothis:</span><span class="sxs-lookup"><span data-stu-id="82495-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![настройка шаблона][template config]
13. <span data-ttu-id="82495-160">В **семейства или идентификатор** у вас есть toospecify какие образ системы будет установлено на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="82495-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="82495-161">Выберите образ из списка семейств или укажите пользовательский вариант.</span><span class="sxs-lookup"><span data-stu-id="82495-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="82495-162">Tooselect из списка семейств изображение, введите hello первого символа (с учетом регистра) имя семейства hello изображения.</span><span class="sxs-lookup"><span data-stu-id="82495-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="82495-163">Например, если вы введете **U** , появится список семейств Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="82495-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="82495-164">После выбора из списка hello Jenkins будет использовать последнюю версию этого образ системы на основе этого семейства hello при подготовке виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="82495-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![список семейств ОС][OS family list]
    
     <span data-ttu-id="82495-166">При наличии пользовательского изображения вместо этого нужно toouse, введите имя hello этого настраиваемого образа.</span><span class="sxs-lookup"><span data-stu-id="82495-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="82495-167">Имена пользовательских изображений не отображаются в списке, у вас есть что tooensure, hello имя введено правильно.</span><span class="sxs-lookup"><span data-stu-id="82495-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="82495-168">В этом учебнике введите **U** toobring список изображений Ubuntu и выберите **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="82495-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="82495-169">В поле **Launch method** (Способ запуска) выберите **SSH**.</span><span class="sxs-lookup"><span data-stu-id="82495-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="82495-170">Скопируйте приведенный ниже сценарий hello и включите в hello **сценарий Init** поля.</span><span class="sxs-lookup"><span data-stu-id="82495-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="82495-171">Hello **сценарий Init** будет выполняться после создания ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="82495-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="82495-172">В этом примере hello скрипт устанавливает Java, git и ant.</span><span class="sxs-lookup"><span data-stu-id="82495-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="82495-173">В hello **Username** и **пароль** введите предпочтительные значения для учетной записи администратора hello, который будет создан на ВМ.</span><span class="sxs-lookup"><span data-stu-id="82495-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="82495-174">Щелкните **Проверка шаблона** toocheck, если выбраны параметры hello являются допустимыми.</span><span class="sxs-lookup"><span data-stu-id="82495-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="82495-175">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="82495-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="82495-176">Создание задания Hudson, выполняемого в подчиненном узле в Azure</span><span class="sxs-lookup"><span data-stu-id="82495-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="82495-177">В этом разделе вы узнаете, как создать задачу Hudson, которая должна выполняться в подчиненном узле в Azure.</span><span class="sxs-lookup"><span data-stu-id="82495-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="82495-178">В hello Hudson панели мониторинга щелкните **новое задание**.</span><span class="sxs-lookup"><span data-stu-id="82495-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="82495-179">Введите имя для задания hello, который вы создаете.</span><span class="sxs-lookup"><span data-stu-id="82495-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="82495-180">Выберите тип задания hello **задание программного обеспечения освободить стиль сборки**.</span><span class="sxs-lookup"><span data-stu-id="82495-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="82495-181">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="82495-181">Click **OK**.</span></span>
5. <span data-ttu-id="82495-182">На странице конфигурации задания hello, выберите **ограничение, когда этот проект может быть выполнена**.</span><span class="sxs-lookup"><span data-stu-id="82495-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="82495-183">Выберите **узел и метки меню** и выберите **linux** (указываются эту метку при создании шаблона виртуальной машины hello в предыдущем разделе hello).</span><span class="sxs-lookup"><span data-stu-id="82495-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="82495-184">В hello **построения** щелкните **добавить шаг сборки** и выберите **выполнение оболочки**.</span><span class="sxs-lookup"><span data-stu-id="82495-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="82495-185">Изменить hello следующий скрипт, заменив **{имя учетной записи github}**, **{имя_проекта}**, и **{каталог проекта}** с соответствующие значения и вставьте hello изменить скрипт в hello текстовое поле, которое отображается.</span><span class="sxs-lookup"><span data-stu-id="82495-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="82495-186">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="82495-186">Click on **Save**.</span></span>
10. <span data-ttu-id="82495-187">В панели мониторинга Hudson hello, найдите только что созданную задание hello и щелкните hello **запланировать построения** значок.</span><span class="sxs-lookup"><span data-stu-id="82495-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="82495-188">Hudson будет затем создайте подчиненного узла, используя шаблон hello, созданный в предыдущем разделе hello и выполнить скрипт hello, указанное на шаге hello сборки для выполнения этой задачи.</span><span class="sxs-lookup"><span data-stu-id="82495-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82495-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82495-189">Next Steps</span></span>
<span data-ttu-id="82495-190">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure].</span><span class="sxs-lookup"><span data-stu-id="82495-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[профиле подписки]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

