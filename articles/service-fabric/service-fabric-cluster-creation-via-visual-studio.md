---
title: "Настройка кластера Service Fabric с помощью Visual Studio | Документация Майкрософт"
description: "Описание настройки кластера Service Fabric с помощью шаблона Azure Resource Manager, созданного с использованием проекта группы ресурсов Azure в Visual Studio"
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
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="b8262-103">Настройка кластера Service Fabric с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8262-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="b8262-104">В этой статье описывается настройка кластера Azure Service Fabric с помощью Visual Studio и шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b8262-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="b8262-105">Для создания шаблона мы будем использовать проект группы ресурсов Azure Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8262-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="b8262-106">После создания шаблона его можно развернуть напрямую в Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8262-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="b8262-107">Его также можно использовать из сценария или в ходе процесса непрерывной интеграции (CI).</span><span class="sxs-lookup"><span data-stu-id="b8262-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="b8262-108">Создание шаблона кластера Service Fabric с помощью проекта группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b8262-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="b8262-109">Чтобы начать работу, откройте Visual Studio и создайте проект группы ресурсов Azure (он доступен в папке **Облако** ).</span><span class="sxs-lookup"><span data-stu-id="b8262-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![Диалоговое окно "Новый проект" с выбранным проектом группы ресурсов Azure][1]

<span data-ttu-id="b8262-111">Можно создать новое решение Visual Studio для данного проекта или добавить его в существующее решение.</span><span class="sxs-lookup"><span data-stu-id="b8262-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="b8262-112">Если проект группы ресурсов Azure не отображается в узле "Облако", значит у вас не установлен пакет SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="b8262-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="b8262-113">Запустите установщик веб-платформы ([установите его отсюда](http://www.microsoft.com/web/downloads/platform.aspx) , если еще этого не сделали), затем выполните поиск по фразе "пакет SDK Azure для .NET" и установите версию, совместимую с используемой версией Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8262-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="b8262-114">После нажатия кнопки OK Visual Studio предложит выбрать шаблон диспетчера ресурсов, который требуется создать:</span><span class="sxs-lookup"><span data-stu-id="b8262-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![Диалоговое окно "Выбор шаблона Azure" с выбранным шаблоном кластера Service Fabric][2]

<span data-ttu-id="b8262-116">Выберите шаблон "Кластер Service Fabric" и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="b8262-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="b8262-117">Проект и шаблон диспетчера ресурсов созданы.</span><span class="sxs-lookup"><span data-stu-id="b8262-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="b8262-118">Подготовка шаблона к развертыванию</span><span class="sxs-lookup"><span data-stu-id="b8262-118">Prepare the template for deployment</span></span>
<span data-ttu-id="b8262-119">Перед развертыванием шаблона для создания кластера необходимо указать значения для обязательных параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="b8262-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="b8262-120">Эти значения параметров считываются из файла `ServiceFabricCluster.parameters.json`, который находится в папке `Templates` проекта группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b8262-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="b8262-121">Откройте файл и укажите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="b8262-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="b8262-122">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="b8262-122">Parameter name</span></span> | <span data-ttu-id="b8262-123">Описание</span><span class="sxs-lookup"><span data-stu-id="b8262-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b8262-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="b8262-124">adminUserName</span></span> |<span data-ttu-id="b8262-125">Имя учетной записи администратора для компьютеров Service Fabric (узлов).</span><span class="sxs-lookup"><span data-stu-id="b8262-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="b8262-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="b8262-126">certificateThumbprint</span></span> |<span data-ttu-id="b8262-127">Отпечаток сертификата, который обеспечивает защиту кластера.</span><span class="sxs-lookup"><span data-stu-id="b8262-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="b8262-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="b8262-128">sourceVaultResourceId</span></span> |<span data-ttu-id="b8262-129">*Идентификатор ресурса* хранилища ключей, где хранится сертификат, который обеспечивает защиту кластера.</span><span class="sxs-lookup"><span data-stu-id="b8262-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="b8262-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="b8262-130">certificateUrlValue</span></span> |<span data-ttu-id="b8262-131">URL-адрес сертификата безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="b8262-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="b8262-132">Шаблон диспетчера ресурсов Service Fabric Visual Studio создает безопасный кластер, защищенный с помощью сертификата.</span><span class="sxs-lookup"><span data-stu-id="b8262-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="b8262-133">Этот сертификат определяется по трем последним параметрам шаблона (`certificateThumbprint`, `sourceVaultValue` и `certificateUrlValue`) и должен находиться в **хранилище ключей Azure**.</span><span class="sxs-lookup"><span data-stu-id="b8262-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="b8262-134">Дополнительные сведения о создании сертификата безопасности кластера см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric).</span><span class="sxs-lookup"><span data-stu-id="b8262-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="b8262-135">Изменение имени кластера (необязательно)</span><span class="sxs-lookup"><span data-stu-id="b8262-135">Optional: change the cluster name</span></span>
<span data-ttu-id="b8262-136">У каждого кластера Service Fabric есть имя.</span><span class="sxs-lookup"><span data-stu-id="b8262-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="b8262-137">При создании кластера Fabric в Azure имя кластера (вместе с регионом Azure) определяет имя системы доменных имен (DNS) для кластера.</span><span class="sxs-lookup"><span data-stu-id="b8262-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="b8262-138">Например, если имя кластера — `myBigCluster`, а группа ресурсов, в которой будет размещаться новый кластер, находится в регионе Azure "Восточная часть США", то DNS-имя кластера будет `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="b8262-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="b8262-139">По умолчанию имя кластера создается автоматически, и для того, чтобы оно было уникальным, к префиксу "cluster" добавляется случайный суффикс.</span><span class="sxs-lookup"><span data-stu-id="b8262-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="b8262-140">Это позволяет легко использовать шаблон в системе **непрерывной интеграции** (CI).</span><span class="sxs-lookup"><span data-stu-id="b8262-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="b8262-141">Если вы хотите использовать определенное осмысленное имя для кластера, задайте его в переменной `clusterName` в файле шаблона Resource Manager (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="b8262-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="b8262-142">Это первая переменная, определенная в этом файле.</span><span class="sxs-lookup"><span data-stu-id="b8262-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="b8262-143">Добавление общедоступных портов приложения (необязательно)</span><span class="sxs-lookup"><span data-stu-id="b8262-143">Optional: add public application ports</span></span>
<span data-ttu-id="b8262-144">Также можно изменить открытые порты приложений кластера перед его развертыванием.</span><span class="sxs-lookup"><span data-stu-id="b8262-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="b8262-145">По умолчанию в шаблоне открыты только два TCP-порта (80 и 8081).</span><span class="sxs-lookup"><span data-stu-id="b8262-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="b8262-146">Если вашим приложениям необходимо больше открытых портов, измените определение балансировщика нагрузки Azure в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="b8262-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="b8262-147">Определение хранится в файле основного шаблона (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="b8262-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="b8262-148">Откройте этот файл и выполните поиск `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="b8262-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="b8262-149">Каждый порт связан с тремя артефактами.</span><span class="sxs-lookup"><span data-stu-id="b8262-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="b8262-150">Переменная шаблона, который определяет значение TCP-порта для порта:</span><span class="sxs-lookup"><span data-stu-id="b8262-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="b8262-151">*Проба*, которая определяет, как часто и как долго балансировщик нагрузки Azure будет пытаться использовать конкретный узел Service Fabric до перехода на другой узел.</span><span class="sxs-lookup"><span data-stu-id="b8262-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="b8262-152">Пробы являются частью ресурса балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b8262-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="b8262-153">Далее приводится определение проверки для первого порта приложения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="b8262-153">Here is the probe definition for the first default application port:</span></span>
   
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
3. <span data-ttu-id="b8262-154">*Правило балансировки нагрузки* , которое связывает порт и пробу, которая включает балансировку нагрузки в наборе узлов кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b8262-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
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
   <span data-ttu-id="b8262-155">Если приложениям, которые вы хотите развернуть в кластере, нужны дополнительные порты, их можно добавить путем создания дополнительной проверки и определений правил балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b8262-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="b8262-156">Дополнительные сведения о работе с балансировщиком нагрузки Azure с помощью шаблонов Resource Manager см. в статье [Начало работы по созданию внутреннего балансировщика нагрузки с помощью шаблона](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="b8262-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="b8262-157">Развертывание шаблона с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8262-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="b8262-158">После сохранения всех обязательных параметров в файл`ServiceFabricCluster.param.dev.json` можно приступить к развертыванию шаблона и созданию кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b8262-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="b8262-159">Щелкните правой кнопкой мыши проект группы ресурсов в обозревателе решений Visual Studio и выберите **Развернуть &gt; Новое развертывание**.</span><span class="sxs-lookup"><span data-stu-id="b8262-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**.</span></span> <span data-ttu-id="b8262-160">В Visual Studio откроется диалоговое окно **Развертывание в группе ресурсов** с запросом на прохождение проверки подлинности в Azure (если необходимо).</span><span class="sxs-lookup"><span data-stu-id="b8262-160">If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![Диалоговое окно "Развертывание в группе ресурсов"][3]

<span data-ttu-id="b8262-162">В диалоговом окне можно выбрать существующую группу ресурсов диспетчера ресурсов для кластера или создать новую.</span><span class="sxs-lookup"><span data-stu-id="b8262-162">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="b8262-163">Как правило, для кластера Service Fabric целесообразно использовать отдельную группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b8262-163">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="b8262-164">После нажатия кнопки "Развернуть" Visual Studio предложит подтвердить значения параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="b8262-164">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="b8262-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b8262-165">Hit the **Save** button.</span></span> <span data-ttu-id="b8262-166">Один параметр не имеет сохраненного значения: это пароль учетной записи администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="b8262-166">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="b8262-167">Это значение необходимо указать, когда Visual Studio предложит это сделать.</span><span class="sxs-lookup"><span data-stu-id="b8262-167">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="b8262-168">Начиная с версии Azure SDK 2.9, Visual Studio поддерживает чтение паролей из **хранилища ключей Azure** во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="b8262-168">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="b8262-169">Обратите внимание, что в диалоговом окне параметров шаблона у текстового поля параметра `adminPassword` есть небольшой значок ключа справа.</span><span class="sxs-lookup"><span data-stu-id="b8262-169">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="b8262-170">Этот значок позволяет выбрать существующий секрет хранилища ключей в качестве пароля администратора кластера.</span><span class="sxs-lookup"><span data-stu-id="b8262-170">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="b8262-171">Сначала необходимо лишь разрешить доступ Azure Resource Manager для развертывания шаблона в разделе "Политики расширенного доступа" хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="b8262-171">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="b8262-172">Ход выполнения процесса развертывания можно отследить в окне выходных данных Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8262-172">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="b8262-173">После завершения развертывания шаблонов новый кластер готов к использованию!</span><span class="sxs-lookup"><span data-stu-id="b8262-173">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="b8262-174">Если среда PowerShell никогда не использовалась для администрирования Azure с компьютера, который используется в настоящий момент, необходимо выполнить некоторые служебные действия.</span><span class="sxs-lookup"><span data-stu-id="b8262-174">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="b8262-175">Включите поддержку сценариев PowerShell, выполнив команду [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b8262-175">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="b8262-176">Для компьютеров разработчиков обычно устанавливается политика "Без ограничений".</span><span class="sxs-lookup"><span data-stu-id="b8262-176">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="b8262-177">Решите, следует ли разрешить сбор диагностических данных от команд Azure PowerShell, и при необходимости выполните команды [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) или [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8262-177">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="b8262-178">Это позволит избежать вывода ненужных запросов во время развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="b8262-178">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="b8262-179">При появлении ошибок перейдите на [портал Azure](https://portal.azure.com/) и откройте группу ресурсов, в которую вы выполнили развертывание.</span><span class="sxs-lookup"><span data-stu-id="b8262-179">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="b8262-180">Выберите **Все параметры**, а затем **Развертывания** в колонке "Параметры".</span><span class="sxs-lookup"><span data-stu-id="b8262-180">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="b8262-181">Здесь будут находиться подробные диагностические сведения о неудачном развертывании группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b8262-181">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="b8262-182">Для кластеров Service Fabric требуется постоянное наличие определенного количества узлов, чтобы поддерживать доступность и сохранять состояние — это называется "поддержанием кворума".</span><span class="sxs-lookup"><span data-stu-id="b8262-182">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="b8262-183">Поэтому не рекомендуется завершать работу всех виртуальных машин в кластере, пока не будет выполнено [полное резервное копирование состояния](service-fabric-reliable-services-backup-restore.md), так как это может быть небезопасно.</span><span class="sxs-lookup"><span data-stu-id="b8262-183">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b8262-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8262-184">Next steps</span></span>
* [<span data-ttu-id="b8262-185">Узнайте больше о настройке кластера Service Fabric с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="b8262-185">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="b8262-186">Узнайте больше о развертывании приложений Service Fabric и управлении ими с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8262-186">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
