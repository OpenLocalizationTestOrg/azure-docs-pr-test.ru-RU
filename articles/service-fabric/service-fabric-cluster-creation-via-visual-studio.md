---
title: "aaaSetting кластера Service Fabric, с помощью Visual Studio | Документы Microsoft"
description: "Описывает, каким образом tooset копирование Service Fabric кластера с помощью шаблона Azure Resource Manager, созданные проекта группы ресурсов Azure в Visual Studio"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="1e163-103">Настройка кластера Service Fabric с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e163-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="1e163-104">В этой статье описывается, как tooset копирование Azure Service Fabric кластера с помощью шаблона диспетчера ресурсов Azure и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e163-104">This article describes how tooset up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="1e163-105">Мы будем использовать шаблона Visual Studio Azure проекта группы ресурсов toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-105">We will use a Visual Studio Azure resource group project toocreate hello template.</span></span> <span data-ttu-id="1e163-106">После создания шаблона hello, его можно развернуть tooAzure прямо из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e163-106">After hello template has been created, it can be deployed directly tooAzure from Visual Studio.</span></span> <span data-ttu-id="1e163-107">Его также можно использовать из сценария или в ходе процесса непрерывной интеграции (CI).</span><span class="sxs-lookup"><span data-stu-id="1e163-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="1e163-108">Создание шаблона кластера Service Fabric с помощью проекта группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="1e163-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="1e163-109">tooget к работе, откройте Visual Studio создайте проект группы ресурсов Azure (она доступна в hello **облака** папки):</span><span class="sxs-lookup"><span data-stu-id="1e163-109">tooget started, open Visual Studio and create an Azure resource group project (it is available in hello **Cloud** folder):</span></span>

![Диалоговое окно "Новый проект" с выбранным проектом группы ресурсов Azure][1]

<span data-ttu-id="1e163-111">Можно создать новое решение Visual Studio для этого проекта или добавить его в существующее решение tooan.</span><span class="sxs-lookup"><span data-stu-id="1e163-111">You can create a new Visual Studio solution for this project or add it tooan existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="1e163-112">Если отсутствует hello проекта группы ресурсов Azure в узле hello облака, у вас hello установленный пакет SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="1e163-112">If you do not see hello Azure resource group project under hello Cloud node, you do not have hello Azure SDK installed.</span></span> <span data-ttu-id="1e163-113">Запустите установщик веб-платформы ([установить сейчас](http://www.microsoft.com/web/downloads/platform.aspx) Если это еще не сделано) и выполните поиск «Azure SDK для .NET» и установите версию hello, которая совместима с версией Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e163-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install hello version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="1e163-114">После нажатия кнопки "ОК" hello, Visual Studio запросит tooselect hello диспетчера ресурсов шаблон toocreate:</span><span class="sxs-lookup"><span data-stu-id="1e163-114">After you hit hello OK button, Visual Studio will ask you tooselect hello Resource Manager template you want toocreate:</span></span>

![Диалоговое окно "Выбор шаблона Azure" с выбранным шаблоном кластера Service Fabric][2]

<span data-ttu-id="1e163-116">Выберите шаблон кластера Service Fabric hello и попаданий hello ОК кнопку еще раз.</span><span class="sxs-lookup"><span data-stu-id="1e163-116">Select hello Service Fabric Cluster template and hit hello OK button again.</span></span> <span data-ttu-id="1e163-117">Теперь создан проект Hello и hello шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1e163-117">hello project and hello Resource Manager template have now been created.</span></span>

## <a name="prepare-hello-template-for-deployment"></a><span data-ttu-id="1e163-118">Подготовка к развертыванию hello шаблона</span><span class="sxs-lookup"><span data-stu-id="1e163-118">Prepare hello template for deployment</span></span>
<span data-ttu-id="1e163-119">До шаблона hello развернутой toocreate hello кластера, необходимо указать значения для параметров шаблона требуется hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-119">Before hello template is deployed toocreate hello cluster, you must provide values for hello required template parameters.</span></span> <span data-ttu-id="1e163-120">Эти значения параметров считываются из hello `ServiceFabricCluster.parameters.json` файл, который находится в hello `Templates` папки проекта группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-120">These parameter values are read from hello `ServiceFabricCluster.parameters.json` file, which is in hello `Templates` folder of hello resource group project.</span></span> <span data-ttu-id="1e163-121">Откройте файл hello и предоставить hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="1e163-121">Open hello file and provide hello following values:</span></span>

| <span data-ttu-id="1e163-122">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="1e163-122">Parameter name</span></span> | <span data-ttu-id="1e163-123">Описание</span><span class="sxs-lookup"><span data-stu-id="1e163-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e163-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="1e163-124">adminUserName</span></span> |<span data-ttu-id="1e163-125">Hello имя учетной записи администратора hello Service Fabric компьютеров (узлов).</span><span class="sxs-lookup"><span data-stu-id="1e163-125">hello name of hello administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="1e163-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="1e163-126">certificateThumbprint</span></span> |<span data-ttu-id="1e163-127">Здравствуйте, отпечаток сертификата hello, обеспечивающую безопасность кластера hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-127">hello thumbprint of hello certificate that secures hello cluster.</span></span> |
| <span data-ttu-id="1e163-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="1e163-128">sourceVaultResourceId</span></span> |<span data-ttu-id="1e163-129">Hello *идентификатор ресурса* из хранилища ключей hello, где hello, обеспечивающую безопасность кластера hello сертификат.</span><span class="sxs-lookup"><span data-stu-id="1e163-129">hello *resource ID* of hello key vault where hello certificate that secures hello cluster is stored.</span></span> |
| <span data-ttu-id="1e163-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="1e163-130">certificateUrlValue</span></span> |<span data-ttu-id="1e163-131">URL-адрес Hello hello сертификат безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="1e163-131">hello URL of hello cluster security certificate.</span></span> |

<span data-ttu-id="1e163-132">шаблон диспетчера ресурсов структуры в Visual Studio службы Hello создает безопасный кластера, защищенного с помощью сертификата.</span><span class="sxs-lookup"><span data-stu-id="1e163-132">hello Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="1e163-133">Этот сертификат идентифицируется hello последние три параметра шаблона (`certificateThumbprint`, `sourceVaultValue`, и `certificateUrlValue`), и он должен присутствовать в **хранилище ключей Azure**.</span><span class="sxs-lookup"><span data-stu-id="1e163-133">This certificate is identified by hello last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="1e163-134">Дополнительные сведения о как toocreate hello сертификат безопасности кластера см. в разделе [сценарии безопасности кластера Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) статьи.</span><span class="sxs-lookup"><span data-stu-id="1e163-134">For more information on how toocreate hello cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-hello-cluster-name"></a><span data-ttu-id="1e163-135">(Необязательно) измените имя кластера hello</span><span class="sxs-lookup"><span data-stu-id="1e163-135">Optional: change hello cluster name</span></span>
<span data-ttu-id="1e163-136">У каждого кластера Service Fabric есть имя.</span><span class="sxs-lookup"><span data-stu-id="1e163-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="1e163-137">При создании кластера Fabric в Azure определяет, имя кластера (а также hello регион Azure) hello имя системы доменных имен (DNS) для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-137">When a Fabric cluster is created in Azure, cluster name determines (together with hello Azure region) hello Domain Name System (DNS) name for hello cluster.</span></span> <span data-ttu-id="1e163-138">Например, если имя кластера `myBigCluster`и hello местоположение (регион Azure) группы ресурсов hello, где будет размещаться новый кластер hello Восток США, hello DNS-имя кластера hello будет `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1e163-138">For example, if you name your cluster `myBigCluster`, and hello location (Azure region) of hello resource group that will host hello new cluster is East US, hello DNS name of hello cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="1e163-139">По умолчанию имя кластера hello автоматически создается и становится уникальной путем присоединения префикс «кластер» tooa случайных суффикс.</span><span class="sxs-lookup"><span data-stu-id="1e163-139">By default hello cluster name is generated automatically and made unique by attaching a random suffix tooa "cluster" prefix.</span></span> <span data-ttu-id="1e163-140">Это делает шаблон hello очень легко toouse как часть **непрерывной интеграции** системы (CI).</span><span class="sxs-lookup"><span data-stu-id="1e163-140">This makes it very easy toouse hello template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="1e163-141">Toouse определенное имя для кластера, это может применяться tooyou задайте значение hello hello `clusterName` переменных в файле шаблона диспетчера ресурсов hello (`ServiceFabricCluster.json`) имя выбранного tooyour.</span><span class="sxs-lookup"><span data-stu-id="1e163-141">If you want toouse a specific name for your cluster, one that is meaningful tooyou, set hello value of hello `clusterName` variable in hello Resource Manager template file (`ServiceFabricCluster.json`) tooyour chosen name.</span></span> <span data-ttu-id="1e163-142">Это первая переменная hello, определенный в этом файле.</span><span class="sxs-lookup"><span data-stu-id="1e163-142">It is hello first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="1e163-143">Добавление общедоступных портов приложения (необязательно)</span><span class="sxs-lookup"><span data-stu-id="1e163-143">Optional: add public application ports</span></span>
<span data-ttu-id="1e163-144">Вы также можете toochange hello приложения открытые порты для hello кластера перед ее развертыванием.</span><span class="sxs-lookup"><span data-stu-id="1e163-144">You may also want toochange hello public application ports for hello cluster before you deploy it.</span></span> <span data-ttu-id="1e163-145">По умолчанию шаблон hello открывает только два открытых TCP-порты (80 и 8081).</span><span class="sxs-lookup"><span data-stu-id="1e163-145">By default, hello template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="1e163-146">Если требуется несколько приложений, измените определение подсистемы балансировки нагрузки Azure hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-146">If you need more for your applications, modify hello Azure Load Balancer definition in hello template.</span></span> <span data-ttu-id="1e163-147">Определение Hello хранится в файле основного шаблона hello (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="1e163-147">hello definition is stored in hello main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="1e163-148">Откройте этот файл и выполните поиск `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="1e163-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="1e163-149">Каждый порт связан с тремя артефактами.</span><span class="sxs-lookup"><span data-stu-id="1e163-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="1e163-150">Шаблон переменной, определяющей hello номер порта TCP для hello порта:</span><span class="sxs-lookup"><span data-stu-id="1e163-150">A template variable that defines hello TCP port value for hello port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="1e163-151">Объект *проверки* , определяющий, как часто и как долго hello балансировки нагрузки Azure пытается toouse конкретный узел Service Fabric перед переходом на другой через tooanother один.</span><span class="sxs-lookup"><span data-stu-id="1e163-151">A *probe* that defines how frequently and for how long hello Azure load balancer attempts toouse a specific Service Fabric node before failing over tooanother one.</span></span> <span data-ttu-id="1e163-152">Hello зонды являются частью hello ресурсов подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1e163-152">hello probes are part of hello Load Balancer resource.</span></span> <span data-ttu-id="1e163-153">Вот определение hello пробы для hello первый порт приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1e163-153">Here is hello probe definition for hello first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="1e163-154">Объект *правило балансировки нагрузки* , объединяет порт hello и hello проверки, который позволит Балансировка нагрузки по набору узлов кластера Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="1e163-154">A *load-balancing rule* that ties together hello port and hello probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="1e163-155">При планировании кластера toohello toodeploy приложения hello требуются дополнительные порты, их можно добавить путем создания дополнительной проверки и определения правил балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1e163-155">If hello applications that you plan toodeploy toohello cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="1e163-156">Дополнительные сведения о том, как toowork с подсистемой балансировки нагрузки Azure посредством шаблонов диспетчера ресурсов. в разделе [приступить к созданию внутренней подсистемы балансировки нагрузки с помощью шаблона](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="1e163-156">For more information on how toowork with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-hello-template-by-using-visual-studio"></a><span data-ttu-id="1e163-157">Развертывание hello шаблона с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e163-157">Deploy hello template by using Visual Studio</span></span>
<span data-ttu-id="1e163-158">После сохранения всех hello значения обязательного параметра в`ServiceFabricCluster.param.dev.json` файла будут готовы toodeploy hello шаблона и создание кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1e163-158">After you have saved all hello required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready toodeploy hello template and create your Service Fabric cluster.</span></span> <span data-ttu-id="1e163-159">Щелкните правой кнопкой мыши проект группы ресурсов hello в обозревателе решений Visual Studio и выберите **развертывание | Новое развертывание...** . Если необходимо, Visual Studio будет отображать hello **развертывание tooResource группы** диалоговое окно, запрашивающее tooauthenticate tooAzure:</span><span class="sxs-lookup"><span data-stu-id="1e163-159">Right-click hello resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show hello **Deploy tooResource Group** dialog box, asking you tooauthenticate tooAzure:</span></span>

![Диалоговое окно tooResource Группа развертывания][3]

<span data-ttu-id="1e163-161">диалоговое окно «Hello» позволяет выбрать существующую группу ресурсов диспетчера ресурсов для кластера hello и предоставляет параметр toocreate hello новый.</span><span class="sxs-lookup"><span data-stu-id="1e163-161">hello dialog box lets you choose an existing Resource Manager resource group for hello cluster and gives you hello option toocreate a new one.</span></span> <span data-ttu-id="1e163-162">Обычно становится toouse смысл отдельной группе ресурсов кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1e163-162">It normally makes sense toouse a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="1e163-163">После нажатия кнопки hello развертывание Visual Studio предложит вам значения параметров шаблона tooconfirm hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-163">After you hit hello Deploy button, Visual Studio will prompt you tooconfirm hello template parameter values.</span></span> <span data-ttu-id="1e163-164">Попаданий hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="1e163-164">Hit hello **Save** button.</span></span> <span data-ttu-id="1e163-165">Один параметр не имеет постоянного значения: hello пароль учетной записи администратора для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-165">One parameter does not have a persisted value: hello administrative account password for hello cluster.</span></span> <span data-ttu-id="1e163-166">Visual Studio по запросу для одного необходимо tooprovide значение пароля.</span><span class="sxs-lookup"><span data-stu-id="1e163-166">You need tooprovide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="1e163-167">Начиная с версии Azure SDK 2.9, Visual Studio поддерживает чтение паролей из **хранилища ключей Azure** во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="1e163-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="1e163-168">В диалоговом окне Параметры шаблона hello Обратите внимание, что hello `adminPassword` текстовом поле параметра имеет маленький значок «ключ» на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="1e163-168">In hello template parameters dialog notice that hello `adminPassword` parameter text box has a little "key" icon on hello right.</span></span> <span data-ttu-id="1e163-169">Этот значок позволяет tooselect существующие секрета хранилища ключей как hello пароля администратора для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-169">This icon allows you tooselect an existing key vault secret as hello administrative password for hello cluster.</span></span> <span data-ttu-id="1e163-170">Просто убедитесь, что toofirst разрешить доступ к диспетчеру ресурсов Azure для шаблона-развертывания в hello Дополнительные политики доступа к хранилищу ключей.</span><span class="sxs-lookup"><span data-stu-id="1e163-170">Just make sure toofirst enable Azure Resource Manager access for template deployment in hello Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="1e163-171">Вы можете отслеживать ход выполнения процесса развертывания hello в окне вывода Visual Studio hello hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-171">You can monitor hello progress of hello deployment process in hello Visual Studio output window.</span></span> <span data-ttu-id="1e163-172">После завершения развертывания шаблона hello на новый кластер: toouse Готово!</span><span class="sxs-lookup"><span data-stu-id="1e163-172">Once hello template deployment is completed, your new cluster is ready toouse!</span></span>

> [!NOTE]
> <span data-ttu-id="1e163-173">Если PowerShell никогда не используется tooadminister Azure на основе машины hello, используется в данный момент, toodo необходимо немного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="1e163-173">If PowerShell was never used tooadminister Azure from hello machine that you are using now, you need toodo a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="1e163-174">Включить скрипты, запустив hello PowerShell [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) команды.</span><span class="sxs-lookup"><span data-stu-id="1e163-174">Enable PowerShell scripting by running hello [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="1e163-175">Для компьютеров разработчиков обычно устанавливается политика "Без ограничений".</span><span class="sxs-lookup"><span data-stu-id="1e163-175">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="1e163-176">Решите, будет ли tooallow сбор диагностических данных из команд Azure PowerShell и запустите [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) или [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) при необходимости.</span><span class="sxs-lookup"><span data-stu-id="1e163-176">Decide whether tooallow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="1e163-177">Это позволит избежать вывода ненужных запросов во время развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="1e163-177">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="1e163-178">Если имеются ошибки, воспользуйтесь toohello [портал Azure](https://portal.azure.com/) и группе ресурсов Привет открыть, было выполнено развертывание.</span><span class="sxs-lookup"><span data-stu-id="1e163-178">If there are any errors, go toohello [Azure portal](https://portal.azure.com/) and open hello resource group that you deployed to.</span></span> <span data-ttu-id="1e163-179">Нажмите кнопку **все параметры**, нажмите кнопку **развертываний** в колонке параметров hello.</span><span class="sxs-lookup"><span data-stu-id="1e163-179">Click **All settings**, then click **Deployments** on hello settings blade.</span></span> <span data-ttu-id="1e163-180">Здесь будут находиться подробные диагностические сведения о неудачном развертывании группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1e163-180">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="1e163-181">Кластеров Service Fabric требуется определенное количество узлов toobe toomaintain доступности и сохранить состояние - ссылка tooas «поддержания кворума».</span><span class="sxs-lookup"><span data-stu-id="1e163-181">Service Fabric clusters require a certain number of nodes toobe up toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="1e163-182">Таким образом, она будет безопасно tooshut строя все машины hello в кластере hello пока сначала выполнить [полного резервного копирования состояния](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="1e163-182">Therefore, it is not safe tooshut down all of hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1e163-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e163-183">Next steps</span></span>
* [<span data-ttu-id="1e163-184">Дополнительные сведения о настройке кластера Service Fabric, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="1e163-184">Learn about setting up Service Fabric cluster using hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="1e163-185">Узнайте, как toomanage и развертывать приложения Service Fabric, с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e163-185">Learn how toomanage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
