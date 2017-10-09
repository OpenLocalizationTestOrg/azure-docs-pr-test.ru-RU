---
title: "сертификаты aaaManage в кластере Azure Service Fabric | Документы Microsoft"
description: "Описывает, как tooadd новых сертификатов, сертификат продолжения и удалить сертификат tooor из кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="e60fd-103">Добавление и удаление сертификатов для кластера Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="e60fd-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="e60fd-104">Рекомендуется ознакомиться с как Service Fabric используются сертификаты X.509 и ознакомьтесь с hello [кластера сценарии безопасности](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="e60fd-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="e60fd-105">Необходимо понять, что такое сертификат кластера и для чего он используется, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="e60fd-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="e60fd-106">Служба структуры позволяет указать два кластера сертификатов, первичной и вторичной реплике, при настройке сертификата безопасности во время создания кластера в добавление tooclient сертификаты.</span><span class="sxs-lookup"><span data-stu-id="e60fd-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="e60fd-107">См. слишком[создание кластера azure через портал](service-fabric-cluster-creation-via-portal.md) или [создание кластера azure посредством Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) для сведений о настройке их во время создания.</span><span class="sxs-lookup"><span data-stu-id="e60fd-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="e60fd-108">Если указать только один сертификат кластера во время создания, затем используется как основной сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="e60fd-109">После создания кластера можно добавить новый сертификат в качестве дополнительного.</span><span class="sxs-lookup"><span data-stu-id="e60fd-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="e60fd-110">Безопасный кластер всегда необходим сертификат по крайней мере один допустимый (не отозван и не истекшим сроком действия) кластера (основная или вторичная) развернуты (в противном случае hello кластер прекращает работу).</span><span class="sxs-lookup"><span data-stu-id="e60fd-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="e60fd-111">90 дней до истечения срока действия, достичь все действительные сертификаты hello возникнет предупреждение трассировки, а также событие предупреждения работоспособности на узле hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="e60fd-112">В настоящее время Service Fabric не отправляет какие-либо электронные сообщения или другие уведомления о данной теме.</span><span class="sxs-lookup"><span data-stu-id="e60fd-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="e60fd-113">Добавление сертификата получателя кластера с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="e60fd-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="e60fd-114">Невозможно добавить вторичный кластер сертификат через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="e60fd-115">У вас есть toouse Azure powershell для этого.</span><span class="sxs-lookup"><span data-stu-id="e60fd-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="e60fd-116">Далее в этом документе описывается процесс Hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="e60fd-117">Поменять местами с помощью портала hello сертификаты кластера hello</span><span class="sxs-lookup"><span data-stu-id="e60fd-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="e60fd-118">После того как развернута успешно сертификат получателя кластера, нужно tooswap hello основного и дополнительного, перейдите колонке toohello безопасности и выберите параметр «Переключение с основного» hello из hello контекстного меню tooswap hello вторичного сертификата с основной сертификат Hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![Переключение сертификатов][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="e60fd-120">Удаление сертификата кластера с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="e60fd-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="e60fd-121">Для безопасного кластера всегда потребуется по крайней мере один допустимый (не отозван и не истекшим сроком действия) сертификат (основная или вторичная) развернуты в противном случае hello кластер прекращает работу.</span><span class="sxs-lookup"><span data-stu-id="e60fd-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="e60fd-122">tooremove дополнительный сертификат не могут использоваться для безопасности кластера, колонке безопасности toohello перейдите и выберите hello «Delete» hello контекстном меню на дополнительный сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="e60fd-123">Если планируется tooremove hello сертификат, который помечен первичных, вам потребуется tooswap его с сначала hello получателя, а затем удалите hello получателя после завершения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="e60fd-124">Добавление дополнительного сертификата с помощью PowerShell для Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e60fd-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="e60fd-125">Эти шаги предполагают знакомы с принципами работы диспетчера ресурсов и развернут хотя бы одного Service Fabric кластера с помощью шаблона диспетчера ресурсов, а шаблон hello использования tooset hello кластера под рукой.</span><span class="sxs-lookup"><span data-stu-id="e60fd-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="e60fd-126">Предполагается также, что вы уверенно используете JSON.</span><span class="sxs-lookup"><span data-stu-id="e60fd-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="e60fd-127">Если вы ищете образец шаблона и параметров, которые можно использовать toofollow вдоль или в качестве отправной точки, затем загрузите его из этого [репозитория git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="e60fd-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="e60fd-128">Изменение шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e60fd-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="e60fd-129">Для удобства ниже вдоль пример 5-VM-1-NodeTypes-Secure_Step2.JSON содержит все изменения hello, уже им.</span><span class="sxs-lookup"><span data-stu-id="e60fd-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="e60fd-130">Образец Hello доступен на [репозитория git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="e60fd-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="e60fd-131">**Убедитесь, что toofollow все шаги hello**</span><span class="sxs-lookup"><span data-stu-id="e60fd-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="e60fd-132">**Шаг 1.** откройте hello шаблона диспетчера ресурсов, используемые toodeploy кластеризации.</span><span class="sxs-lookup"><span data-stu-id="e60fd-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="e60fd-133">(Если вы загрузили пример hello из hello выше репозитория, затем использовать 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy безопасного кластера, а затем откройте копию этого шаблона).</span><span class="sxs-lookup"><span data-stu-id="e60fd-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="e60fd-134">**Шаг 2.** добавить **два новых параметра** «secCertificateThumbprint» и «secCertificateUrlValue» типа «string» toohello раздел параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="e60fd-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="e60fd-135">Можно скопировать следующий фрагмент кода hello и добавить его toohello шаблона.</span><span class="sxs-lookup"><span data-stu-id="e60fd-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="e60fd-136">В зависимости от источника hello шаблона могут уже иметь эти определенные, в этом случае переместить toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="e60fd-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="e60fd-137">**Шаг 3.** внесение изменений toohello **Microsoft.ServiceFabric/clusters** ресурса, найдите определение ресурсов «Microsoft.ServiceFabric/clusters» hello в шаблон.</span><span class="sxs-lookup"><span data-stu-id="e60fd-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="e60fd-138">В разделе Свойства этого определения найдет «Сертификат» JSON тег, который выглядит примерно hello, следующий фрагмент JSON:</span><span class="sxs-lookup"><span data-stu-id="e60fd-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="e60fd-139">Добавьте новый тег thumbprintSecondary и присвойте ему значение [parameters('secCertificateThumbprint')].</span><span class="sxs-lookup"><span data-stu-id="e60fd-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="e60fd-140">Да, теперь hello определения ресурса должен выглядеть hello следующим образом (в зависимости от источника hello шаблона, он может не быть так же, как в приведенном ниже фрагменте hello).</span><span class="sxs-lookup"><span data-stu-id="e60fd-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="e60fd-141">Если требуется слишком**продолжения hello cert**, укажите в качестве первичного и перемещение hello текущая первичная дополнительный — hello новый сертификат.</span><span class="sxs-lookup"><span data-stu-id="e60fd-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="e60fd-142">Это приводит к hello смену текущей основной сертификат toohello новый сертификат в один шаг развертывания.</span><span class="sxs-lookup"><span data-stu-id="e60fd-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="e60fd-143">**Шаг 4.** вносить в них изменения слишком**все** hello **Microsoft.Compute/virtualMachineScaleSets** определения ресурсов - обнаружения ресурса Microsoft.Compute/virtualMachineScaleSets hello Определение.</span><span class="sxs-lookup"><span data-stu-id="e60fd-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="e60fd-144">Прокрутите toohello «издатель»: «Microsoft.Azure.ServiceFabric» в разделе «virtualMachineProfile».</span><span class="sxs-lookup"><span data-stu-id="e60fd-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="e60fd-145">В настройках издателя структуры службы hello вы увидите примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e60fd-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="e60fd-147">Добавить hello нового сертификата записи tooit</span><span class="sxs-lookup"><span data-stu-id="e60fd-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="e60fd-148">свойства Hello теперь должна выглядеть следующим образом</span><span class="sxs-lookup"><span data-stu-id="e60fd-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="e60fd-150">Если требуется слишком**продолжения hello cert**, укажите в качестве первичного и перемещение hello текущая первичная дополнительный — hello новый сертификат.</span><span class="sxs-lookup"><span data-stu-id="e60fd-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="e60fd-151">Это приводит к hello смену текущий сертификат toohello новый сертификат за один шаг развертывания.</span><span class="sxs-lookup"><span data-stu-id="e60fd-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="e60fd-152">свойства Hello теперь должна выглядеть следующим образом</span><span class="sxs-lookup"><span data-stu-id="e60fd-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="e60fd-154">**Шаг 5.** вносить изменения слишком**все** hello **Microsoft.Compute/virtualMachineScaleSets** определения ресурсов - обнаружения ресурса Microsoft.Compute/virtualMachineScaleSets hello Определение.</span><span class="sxs-lookup"><span data-stu-id="e60fd-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="e60fd-155">Прокрутите toohello «vaultCertificates»:, в разделе «OSProfile».</span><span class="sxs-lookup"><span data-stu-id="e60fd-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="e60fd-156">Должно отобразиться примерно следующее.</span><span class="sxs-lookup"><span data-stu-id="e60fd-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="e60fd-158">Добавьте hello secCertificateUrlValue tooit.</span><span class="sxs-lookup"><span data-stu-id="e60fd-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="e60fd-159">Используйте следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="e60fd-160">Hello, возникающие в Json должны выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e60fd-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="e60fd-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="e60fd-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="e60fd-162">Убедитесь, что содержать повторяющиеся шаги 4 и 5 для всех определений ресурсов Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello в шаблон.</span><span class="sxs-lookup"><span data-stu-id="e60fd-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="e60fd-163">Если пропустить один из них, hello сертификат будет не устанавливается на этом VMSS и будет привести к непредсказуемым результатам в кластере кластера hello выхода из строя (Если вы получаете действительные сертификаты не могут использовать этот кластер hello для обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="e60fd-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="e60fd-164">Поэтому прежде чем продолжать, проверьте все еще раз.</span><span class="sxs-lookup"><span data-stu-id="e60fd-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="e60fd-165">Изменение шаблона файла tooreflect hello новые параметры добавленную выше</span><span class="sxs-lookup"><span data-stu-id="e60fd-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="e60fd-166">При использовании образца hello из hello [репозитория git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow вместе, вы можете запустить toomake изменения в hello пример 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="e60fd-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="e60fd-167">Изменение параметра шаблона диспетчера ресурсов файл, добавить два новых параметра hello secCertificateThumbprint и secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="e60fd-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="e60fd-168">Развертывание шаблона tooAzure hello</span><span class="sxs-lookup"><span data-stu-id="e60fd-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="e60fd-169">Вы являются toodeploy теперь готовы к tooAzure шаблона.</span><span class="sxs-lookup"><span data-stu-id="e60fd-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="e60fd-170">Откройте командную строку Azure PowerShell версии не ниже 1.</span><span class="sxs-lookup"><span data-stu-id="e60fd-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="e60fd-171">Войдите в tooyour учетную запись Azure и выберите конкретную подписку azure hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="e60fd-172">Это важный шаг для людей, имеющих доступ toomore более одной подписки azure.</span><span class="sxs-lookup"><span data-stu-id="e60fd-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="e60fd-173">Тестирование toodeploying предыдущий шаблон hello его.</span><span class="sxs-lookup"><span data-stu-id="e60fd-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="e60fd-174">Используйте hello же группе ресурсов кластера в настоящее время развертыванием.</span><span class="sxs-lookup"><span data-stu-id="e60fd-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="e60fd-175">Развертывание группы ресурсов tooyour шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="e60fd-176">Используйте hello же группе ресурсов кластера в настоящее время развертыванием.</span><span class="sxs-lookup"><span data-stu-id="e60fd-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="e60fd-177">Выполните команду New-AzureRmResourceGroupDeployment hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="e60fd-178">Нет необходимости toospecify hello режиме, так как значение по умолчанию hello **добавочное**.</span><span class="sxs-lookup"><span data-stu-id="e60fd-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="e60fd-179">При выборе режима tooComplete можно случайно удалить ресурсы, не входящие в шаблон.</span><span class="sxs-lookup"><span data-stu-id="e60fd-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="e60fd-180">Поэтому не используйте этот режим данном сценарии.</span><span class="sxs-lookup"><span data-stu-id="e60fd-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="e60fd-181">Вот out пример hello заполненный же powershell.</span><span class="sxs-lookup"><span data-stu-id="e60fd-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="e60fd-182">После завершения развертывания hello подключения tooyour кластера с помощью нового сертификата hello и выполнять некоторые запросы.</span><span class="sxs-lookup"><span data-stu-id="e60fd-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="e60fd-183">Если вы не можете toodo.</span><span class="sxs-lookup"><span data-stu-id="e60fd-183">If you are able toodo.</span></span> <span data-ttu-id="e60fd-184">Затем можно удалить старый сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="e60fd-185">Если вы используете самозаверяющий сертификат, не забудьте tooimport их в локальное хранилище TrustedPeople сертификат.</span><span class="sxs-lookup"><span data-stu-id="e60fd-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="e60fd-186">Краткий справочник Вот hello команда tooconnect tooa безопасности кластера</span><span class="sxs-lookup"><span data-stu-id="e60fd-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="e60fd-187">Краткий справочник Вот работоспособности кластера tooget команда hello</span><span class="sxs-lookup"><span data-stu-id="e60fd-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="e60fd-188">Развертывание кластера toohello сертификаты приложений.</span><span class="sxs-lookup"><span data-stu-id="e60fd-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="e60fd-189">Можно использовать hello же шаги, как описано в шаги 5 выше toohave hello сертификаты, развернутых из keyvault toohello узлов.</span><span class="sxs-lookup"><span data-stu-id="e60fd-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="e60fd-190">Необходимо только определить и использовать другие параметры.</span><span class="sxs-lookup"><span data-stu-id="e60fd-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="e60fd-191">Добавление или удаление сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="e60fd-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="e60fd-192">В дополнение toohello кластера сертификаты можно добавить операции управления tooperform сертификаты клиента на кластере service fabric.</span><span class="sxs-lookup"><span data-stu-id="e60fd-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="e60fd-193">Вы можете добавлять сертификаты клиента двух типов: для администратора или только для чтения.</span><span class="sxs-lookup"><span data-stu-id="e60fd-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="e60fd-194">Они затем могут быть операции администрирования toohello доступа используется toocontrol и операций запросов на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="e60fd-195">По умолчанию hello кластера сертификаты добавляются toohello разрешенный список сертификатов администратора.</span><span class="sxs-lookup"><span data-stu-id="e60fd-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="e60fd-196">Количество сертификатов клиента не ограничено.</span><span class="sxs-lookup"><span data-stu-id="e60fd-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="e60fd-197">Каждый добавлении или удалении приводит кластера service fabric конфигурации обновления toohello</span><span class="sxs-lookup"><span data-stu-id="e60fd-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="e60fd-198">Добавление сертификатов клиента для администратора или только для чтения с помощью портала</span><span class="sxs-lookup"><span data-stu-id="e60fd-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="e60fd-199">Перейдите в колонку toohello безопасности и выберите hello «+ проверки подлинности» кнопки на колонки безопасности hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="e60fd-200">В колонке «Добавление проверки подлинности» hello выберите hello «Тип проверки подлинности» - «Client только для чтения» или «Администратор клиента»</span><span class="sxs-lookup"><span data-stu-id="e60fd-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="e60fd-201">Теперь выберите метод авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="e60fd-202">Это означает tooService структуры ли этот сертификат следует искать с помощью hello имени субъекта или отпечатка hello.</span><span class="sxs-lookup"><span data-stu-id="e60fd-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="e60fd-203">Как правило он не является методом обеспечения безопасности рекомендуется toouse hello авторизации имени субъекта.</span><span class="sxs-lookup"><span data-stu-id="e60fd-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![Добавление сертификата клиента][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="e60fd-205">Здравствуйте, удаление сертификатов клиента - администратора или только для чтения с помощью портала</span><span class="sxs-lookup"><span data-stu-id="e60fd-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="e60fd-206">tooremove дополнительный сертификат не могут использоваться для безопасности кластера, колонке безопасности toohello перейдите и выберите hello «Delete» hello контекстном меню на hello конкретного сертификата.</span><span class="sxs-lookup"><span data-stu-id="e60fd-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e60fd-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e60fd-207">Next steps</span></span>
<span data-ttu-id="e60fd-208">Дополнительные сведения об управлении кластерами доступны в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="e60fd-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="e60fd-209">Обновление кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e60fd-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="e60fd-210">Настройка доступа на основе ролей для клиентов</span><span class="sxs-lookup"><span data-stu-id="e60fd-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


