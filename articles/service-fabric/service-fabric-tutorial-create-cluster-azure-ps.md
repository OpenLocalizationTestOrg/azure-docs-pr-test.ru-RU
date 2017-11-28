---
title: "кластер Service Fabric aaaCreate в Azure | Документы Microsoft"
description: "Узнайте, как toocreate Windows или Linux Service Fabric кластер в Azure с помощью PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="54e6a-103">Создание безопасного кластера в Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="54e6a-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="54e6a-104">В этом учебнике показано, как toocreate Service Fabric кластера (Windows или Linux) в Azure.</span><span class="sxs-lookup"><span data-stu-id="54e6a-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="54e6a-105">После завершения имеется кластер, работающими в облаке hello, можно развернуть приложение.</span><span class="sxs-lookup"><span data-stu-id="54e6a-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="54e6a-106">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="54e6a-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="54e6a-107">Создание защищенного кластера Service Fabric в Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="54e6a-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="54e6a-108">Безопасный hello кластера с помощью сертификата X.509</span><span class="sxs-lookup"><span data-stu-id="54e6a-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="54e6a-109">Подключите кластер toohello с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="54e6a-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="54e6a-110">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="54e6a-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54e6a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="54e6a-111">Prerequisites</span></span>
<span data-ttu-id="54e6a-112">Перед началом работы с этим руководством выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="54e6a-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="54e6a-113">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="54e6a-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="54e6a-114">Установка hello [модуля Service Fabric SDK и PowerShell](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="54e6a-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="54e6a-115">Установка hello [Azure Powershell версии 4.1 или более поздней версии модуля](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="54e6a-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="54e6a-116">После процедуры Hello создает Предварительный просмотр (одной виртуальной машины) для одного узла кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="54e6a-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="54e6a-117">кластер Hello защищен самозаверяющий сертификат, который получает создан вместе с кластера hello и затем помещается в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="54e6a-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="54e6a-118">Кластеры с одним узлом, не может быть масштабирована за одну виртуальную машину и предварительного просмотра кластеров не может быть toonewer обновленной версии.</span><span class="sxs-lookup"><span data-stu-id="54e6a-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="54e6a-119">toocalculate расходы, выполнив кластера Service Fabric в Azure используйте hello [калькулятор цен Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="54e6a-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="54e6a-120">Дополнительные сведения о создании кластеров Service Fabric см. в статье [Создание кластера Service Fabric в Azure с помощью Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="54e6a-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="54e6a-121">Создание кластера hello, с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="54e6a-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="54e6a-122">Загрузить локальную копию шаблона Azure Resource Manager hello и файл параметров hello hello [шаблона Azure Resource Manager для Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="54e6a-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="54e6a-123">*azuredeploy.JSON* — шаблон hello Azure Resource Manager, который определяет кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="54e6a-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="54e6a-124">*azuredeploy.Parameters.JSON* — это файл параметров для вас toocustomize hello кластерном развертывании.</span><span class="sxs-lookup"><span data-stu-id="54e6a-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="54e6a-125">Настроить следующие параметры в hello hello *azuredeploy.parameters.json* файл параметров:</span><span class="sxs-lookup"><span data-stu-id="54e6a-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="54e6a-126">Параметр</span><span class="sxs-lookup"><span data-stu-id="54e6a-126">Parameter</span></span>       | <span data-ttu-id="54e6a-127">Описание</span><span class="sxs-lookup"><span data-stu-id="54e6a-127">Description</span></span> | <span data-ttu-id="54e6a-128">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="54e6a-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="54e6a-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="54e6a-129">clusterLocation</span></span> | <span data-ttu-id="54e6a-130">кластер hello toodeploy toowhich регион Azure Hello.</span><span class="sxs-lookup"><span data-stu-id="54e6a-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="54e6a-131">*Например, westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="54e6a-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="54e6a-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="54e6a-132">clusterName</span></span>     | <span data-ttu-id="54e6a-133">Имя кластера hello требуется toocreate.</span><span class="sxs-lookup"><span data-stu-id="54e6a-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="54e6a-134">*Например, bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="54e6a-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="54e6a-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="54e6a-135">adminUserName</span></span>   | <span data-ttu-id="54e6a-136">Hello учетная запись локального администратора на виртуальных машинах hello кластера.</span><span class="sxs-lookup"><span data-stu-id="54e6a-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="54e6a-137">*Любое допустимое имя пользователя Windows Server*</span><span class="sxs-lookup"><span data-stu-id="54e6a-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="54e6a-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="54e6a-138">adminPassword</span></span>   | <span data-ttu-id="54e6a-139">Пароль учетной записи локального администратора hello на виртуальных машинах hello кластера.</span><span class="sxs-lookup"><span data-stu-id="54e6a-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="54e6a-140">*Любой допустимый пароль Windows Server*</span><span class="sxs-lookup"><span data-stu-id="54e6a-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="54e6a-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="54e6a-141">clusterCodeVersion</span></span> | <span data-ttu-id="54e6a-142">toorun версии Service Fabric Hello.</span><span class="sxs-lookup"><span data-stu-id="54e6a-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="54e6a-143">(255.255.X.255 — предварительные версии).</span><span class="sxs-lookup"><span data-stu-id="54e6a-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="54e6a-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="54e6a-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="54e6a-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="54e6a-145">vmInstanceCount</span></span> | <span data-ttu-id="54e6a-146">Hello количество виртуальных машин в кластере (может быть 1 или 3-99).</span><span class="sxs-lookup"><span data-stu-id="54e6a-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="54e6a-147">**1**</span><span class="sxs-lookup"><span data-stu-id="54e6a-147">**1**</span></span> | <span data-ttu-id="54e6a-148">*Для предварительной версии кластера укажите только одну виртуальную машину*</span><span class="sxs-lookup"><span data-stu-id="54e6a-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="54e6a-149">Откройте консоль PowerShell, tooAzure входа и выберите hello подписку, которую требуется toodeploy hello кластера в:</span><span class="sxs-lookup"><span data-stu-id="54e6a-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="54e6a-150">Создайте и зашифровать пароль для сертификата toobe hello, используемые Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="54e6a-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="54e6a-151">Создание кластера hello и свой сертификат, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="54e6a-151">Create hello cluster and its certificate by running hello following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="54e6a-152">Hello `-CertificateSubjectName` параметра должны быть выровнены с параметром Имя_кластера hello, указанный в файле параметров hello, также как hello toohello домена привязан регион Azure вы выбрали, например: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="54e6a-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="54e6a-153">После завершения настройки hello, он выводит сведения о кластере hello, созданные в Azure.</span><span class="sxs-lookup"><span data-stu-id="54e6a-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="54e6a-154">Также он копирует каталог hello кластера сертификат toohello - CertificateOutputFolder на hello путь, заданный для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="54e6a-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="54e6a-155">Необходимо, чтобы этот сертификат tooaccess Service Fabric Explorer и представление hello работоспособности кластера.</span><span class="sxs-lookup"><span data-stu-id="54e6a-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="54e6a-156">Запишите hello URL-адрес для кластера, который может быть примерно toohello URL-адреса: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="54e6a-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="54e6a-157">& Изменить сертификат hello доступ обозреватель Service Fabric</span><span class="sxs-lookup"><span data-stu-id="54e6a-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="54e6a-158">Дважды щелкните hello tooopen hello сертификатов мастера импорта сертификатов.</span><span class="sxs-lookup"><span data-stu-id="54e6a-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="54e6a-159">Использовать параметры по умолчанию, но убедитесь, что hello toocheck **Пометить ключ как экспортируемый.**</span><span class="sxs-lookup"><span data-stu-id="54e6a-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="54e6a-160">флажок в hello **защиты закрытого ключа** шаг.</span><span class="sxs-lookup"><span data-stu-id="54e6a-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="54e6a-161">Visual Studio требуется tooexport hello сертификат при настройке проверки подлинности кластера Fabric tooService реестра контейнера Azure далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="54e6a-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="54e6a-162">Теперь можно открыть обозреватель Service Fabric в браузере.</span><span class="sxs-lookup"><span data-stu-id="54e6a-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="54e6a-163">toodo таким образом, перейдите toohello **ManagementEndpoint** URL-адрес для кластера с помощью веб-браузер и hello выберите сертификат, который был сохранен на компьютере.</span><span class="sxs-lookup"><span data-stu-id="54e6a-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="54e6a-164">При открытии обозревателя Service Fabric появится сообщение об ошибке сертификата, так как используется самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="54e6a-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="54e6a-165">В Edge, у вас есть tooclick *сведения* и затем hello *перейдите на веб-странице toohello* ссылку.</span><span class="sxs-lookup"><span data-stu-id="54e6a-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="54e6a-166">В браузере Chrome, у вас есть tooclick *Дополнительно* и затем hello *Продолжить* ссылку.</span><span class="sxs-lookup"><span data-stu-id="54e6a-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="54e6a-167">Если происходит сбой создания кластера hello, всегда можно повторно hello команду, которая обновляет hello ресурсов, уже развернутых.</span><span class="sxs-lookup"><span data-stu-id="54e6a-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="54e6a-168">Если сертификат был создан в ходе развертывания не удалось hello, создается новый.</span><span class="sxs-lookup"><span data-stu-id="54e6a-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="54e6a-169">Создание кластера tootroubleshoot, в разделе [создание кластера Service Fabric с помощью диспетчера ресурсов Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="54e6a-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="54e6a-170">Подключите кластер безопасного toohello</span><span class="sxs-lookup"><span data-stu-id="54e6a-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="54e6a-171">Подключите кластер toohello с помощью модуля Service Fabric PowerShell hello, установленные с hello Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="54e6a-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="54e6a-172">Во-первых установите hello сертификат в хранилище персональных (Мои) hello hello текущего пользователя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="54e6a-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="54e6a-173">Выполните следующую команду PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="54e6a-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="54e6a-174">Теперь вы находитесь кластера безопасных готовы tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="54e6a-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="54e6a-175">Hello **Service Fabric** модуль PowerShell предоставляет многие командлеты для управления кластерами, приложениями и службами Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="54e6a-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="54e6a-176">Используйте hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) командлет tooconnect toohello безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="54e6a-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="54e6a-177">Здравствуйте, отпечаток сертификата и сведений о конечной точке соединения находятся в выходной hello из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="54e6a-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="54e6a-178">Убедитесь, что вы подключены, и hello кластера находится в работоспособном состоянии, с помощью hello [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) командлета.</span><span class="sxs-lookup"><span data-stu-id="54e6a-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="54e6a-179">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="54e6a-179">Clean up resources</span></span>

<span data-ttu-id="54e6a-180">Кластер состоит из других ресурсов Azure в дополнение к этому toohello сам ресурс кластера.</span><span class="sxs-lookup"><span data-stu-id="54e6a-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="54e6a-181">Hello простейший способ toodelete hello кластера и все ресурсы hello, которые он использует является группой ресурсов toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="54e6a-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="54e6a-182">Войдите в tooAzure и выберите hello идентификатор подписки, с которой необходимо tooremove hello кластера.</span><span class="sxs-lookup"><span data-stu-id="54e6a-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="54e6a-183">Идентификатор подписки можно найти в систему в toohello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="54e6a-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="54e6a-184">Удалите группу ресурсов hello и все ресурсы кластера hello, с помощью hello [командлет Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="54e6a-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="54e6a-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="54e6a-185">Next steps</span></span>
<span data-ttu-id="54e6a-186">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="54e6a-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="54e6a-187">Создание кластера Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="54e6a-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="54e6a-188">Безопасный hello кластера с помощью сертификата X.509</span><span class="sxs-lookup"><span data-stu-id="54e6a-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="54e6a-189">Подключите кластер toohello с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="54e6a-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="54e6a-190">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="54e6a-190">Remove a cluster</span></span>

<span data-ttu-id="54e6a-191">Затем переместить следующие учебника toolearn как toohello toodeploy существующего приложения.</span><span class="sxs-lookup"><span data-stu-id="54e6a-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="54e6a-192">Развертывание существующего приложения .NET с помощью Docker Compose</span><span class="sxs-lookup"><span data-stu-id="54e6a-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
