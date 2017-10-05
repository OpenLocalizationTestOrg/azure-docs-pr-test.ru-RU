---
title: "Часто задаваемые вопросы о масштабируемых наборах виртуальных машин Azure | Документация Майкрософт"
description: "Ответы на часто задаваемые вопросы о масштабируемых наборах виртуальных машин."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: f320dd5d1f8c99317792f4ae9e09bc5adaf79e25
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="9dd63-103">Часто задаваемые вопросы о масштабируемых наборах виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="9dd63-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="9dd63-104">Ответы на часто задаваемые вопросы о масштабируемых наборах виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd63-104">Get answers to frequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="9dd63-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="9dd63-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="9dd63-106">Существуют ли рекомендации по автомасштабированию Azure?</span><span class="sxs-lookup"><span data-stu-id="9dd63-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="9dd63-107">Рекомендации по автомасштабированию виртуальных компонентов см. в [этой статье](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="9dd63-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="9dd63-108">Где можно найти имена метрик на основе узла, используемые в процессе автомасштабирования?</span><span class="sxs-lookup"><span data-stu-id="9dd63-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="9dd63-109">Имена метрик на основе узла, используемые в процессе автомасштабирования, перечислены в статье [Метрики, поддерживаемые Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="9dd63-110">Существуют ли какие-либо образцы автомасштабирования на основе раздела или длины очереди служебной шины Azure?</span><span class="sxs-lookup"><span data-stu-id="9dd63-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="9dd63-111">Да.</span><span class="sxs-lookup"><span data-stu-id="9dd63-111">Yes.</span></span> <span data-ttu-id="9dd63-112">Образцы автомасштабирования на основе раздела или длины очереди служебной шины Azure см. в статье [Общие метрики автомасштабирования Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="9dd63-113">Для очереди служебной шины используйте следующий код JSON:</span><span class="sxs-lookup"><span data-stu-id="9dd63-113">For a Service Bus queue, use the following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="9dd63-114">Для очереди хранилища используйте следующий код JSON:</span><span class="sxs-lookup"><span data-stu-id="9dd63-114">For a storage queue, use the following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="9dd63-115">Замените примеры значений соответствующими универсальными кодами ресурсов (URI).</span><span class="sxs-lookup"><span data-stu-id="9dd63-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="9dd63-116">Следует ли выполнять автомасштабирование с использованием метрик на основе узла или с применением расширения диагностики?</span><span class="sxs-lookup"><span data-stu-id="9dd63-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="9dd63-117">Вы можете создать на виртуальной машине конфигурацию автомасштабирования с использованием метрик уровня узла или метрик на основе гостевой ОС.</span><span class="sxs-lookup"><span data-stu-id="9dd63-117">You can create an autoscale setting on a VM to use host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="9dd63-118">Список поддерживаемых метрик см. в статье [Общие метрики автомасштабирования Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="9dd63-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="9dd63-119">Полное определение конфигурации масштабируемых наборов см. в статье [Расширенная настройка автомасштабирования с помощью шаблонов Resource Manager для масштабируемых наборов виртуальных машин](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="9dd63-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="9dd63-120">В этой конфигурации используется метрика ЦП уровня узла и метрика количества сообщений.</span><span class="sxs-lookup"><span data-stu-id="9dd63-120">The sample uses the host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="9dd63-121">Как можно задать правила оповещений в масштабируемом наборе виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="9dd63-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="9dd63-122">Оповещения на основе метрик в масштабируемых наборах виртуальных машин можно создать с помощью PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9dd63-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="9dd63-123">Дополнительные сведения см. в разделе [Создание правил генерации оповещений](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) и [Работа с оповещениями](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="9dd63-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="9dd63-124">Идентификатор целевого ресурса масштабируемого набора виртуальных машин выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9dd63-124">The TargetResourceId of the virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="9dd63-125">/subscriptions/идентификатор_подписки/resourceGroups/группа_ресурсов/providers/Microsoft.Compute/virtualMachineScaleSets/имя_набора.</span><span class="sxs-lookup"><span data-stu-id="9dd63-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="9dd63-126">В качестве метрики, для которой будут устанавливаться оповещения, можно выбрать любой счетчик производительности виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9dd63-126">You can choose any VM performance counter as the metric to set an alert for.</span></span> <span data-ttu-id="9dd63-127">Дополнительные сведения см. в разделе [Метрики гостевой ОС для виртуальных машин под управлением Windows, развернутых с помощью Resource Manager](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) и [Метрики гостевой ОС для виртуальных машин под управлением Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) статьи [Общие метрики автомасштабирования Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in the [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="9dd63-128">Как можно задать параметры автомасштабирования в масштабируемом наборе виртуальных машин с помощью PowerShell?</span><span class="sxs-lookup"><span data-stu-id="9dd63-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="9dd63-129">Дополнительные сведения о настройке параметров автомасштабирования в масштабируемом наборе виртуальных машин с помощью PowerShell см. в [этой записи блога](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-129">To set up autoscale on a virtual machine scale set by using PowerShell, see the blog post [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="9dd63-130">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="9dd63-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-to-the-vm-how-do-i-provision-a-virtual-machine-scale-set-to-run-a-website-where-the-ssl-for-the-website-is-shipped-securely-from-a-certificate-configuration-the-common-certificate-rotation-operation-would-be-almost-the-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-to-do-this"></a><span data-ttu-id="9dd63-131">Как осуществляется безопасная отправка сертификата на виртуальную машину?</span><span class="sxs-lookup"><span data-stu-id="9dd63-131">How do I securely ship a certificate to the VM?</span></span> <span data-ttu-id="9dd63-132">Как подготовить масштабируемый набор виртуальных машин к запуску веб-сайта, где SSL для веб-сайта безопасно отправляется из конфигурации сертификата?</span><span class="sxs-lookup"><span data-stu-id="9dd63-132">How do I provision a virtual machine scale set to run a website where the SSL for the website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="9dd63-133">(Обычная операция смены сертификатов практически такая же, как и операция обновления конфигурации.) Существует ли пример того, как это можно сделать?</span><span class="sxs-lookup"><span data-stu-id="9dd63-133">(The common certificate rotation operation would be almost the same as a configuration update operation.) Do you have an example of how to do this?</span></span> 

<span data-ttu-id="9dd63-134">Чтобы безопасно отправить сертификат на виртуальную машину, вы можете установить сертификат клиента из хранилища ключей непосредственно в хранилище сертификатов Windows.</span><span class="sxs-lookup"><span data-stu-id="9dd63-134">To securely ship a certificate to the VM, you can install a customer certificate directly into a Windows certificate store from the customer's key vault.</span></span>

<span data-ttu-id="9dd63-135">Используйте следующий код JSON:</span><span class="sxs-lookup"><span data-stu-id="9dd63-135">Use the following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="9dd63-136">Этот код поддерживает операционные системы Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="9dd63-136">The code supports Windows and Linux.</span></span>

<span data-ttu-id="9dd63-137">Дополнительные сведения см. в разделе о [создании и обновлении масштабируемого набора виртуальных машин](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="9dd63-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="9dd63-138">Пример самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="9dd63-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="9dd63-139">Создайте самозаверяющий сертификат в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="9dd63-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="9dd63-140">Используйте следующие команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9dd63-140">Use the following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="9dd63-141">Таким образом вы получите входные данные для шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd63-141">This command gives you the input for the Azure Resource Manager template.</span></span>

    <span data-ttu-id="9dd63-142">Пример создания самозаверяющего сертификата в хранилище ключей см. в статье [Сценарии защиты кластера Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-142">For an example of how to create a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="9dd63-143">Измените шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd63-143">Change the Resource Manager template.</span></span>

    <span data-ttu-id="9dd63-144">Добавьте это свойство в раздел **virtualMachineProfile** как часть ресурса масштабируемого набора виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="9dd63-144">Add this property to **virtualMachineProfile**, as part of the virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-to-use-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="9dd63-145">Можно ли определить пару ключей SSH, используемых в процессе проверки подлинности SSH с помощью масштабируемого набора виртуальных машин Linux, развернутого из шаблона Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="9dd63-145">Can I specify an SSH key pair to use for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="9dd63-146">Да.</span><span class="sxs-lookup"><span data-stu-id="9dd63-146">Yes.</span></span> <span data-ttu-id="9dd63-147">В этом случае REST API для **osProfile** и стандартной виртуальной машины аналогичен.</span><span class="sxs-lookup"><span data-stu-id="9dd63-147">The REST API for **osProfile** is similar to the standard VM REST API.</span></span> 

<span data-ttu-id="9dd63-148">Включите раздел **osProfile** в свой шаблон:</span><span class="sxs-lookup"><span data-stu-id="9dd63-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="9dd63-149">Этот блок JSON используется в [шаблоне быстрого запуска 101-vm-sshkey на сайте GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9dd63-149">This JSON block is used in [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="9dd63-150">Раздел osProfile также используется в [шаблоне быстрого запуска grelayhost.json](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="9dd63-150">The OS profile also is used in [the grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="9dd63-151">Дополнительные сведения см. в разделе о [создании и обновлении масштабируемого набора виртуальных машин](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="9dd63-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="9dd63-152">Как удалить устаревшие сертификаты?</span><span class="sxs-lookup"><span data-stu-id="9dd63-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="9dd63-153">Чтобы удалить устаревший сертификат, его необходимо удалить из списка сертификатов в хранилище.</span><span class="sxs-lookup"><span data-stu-id="9dd63-153">To remove deprecated certificates, remove the old certificate from the vault certificates list.</span></span> <span data-ttu-id="9dd63-154">Не удаляйте сертификаты, которые вы хотите оставить на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9dd63-154">Leave all the certificates that you want to remain on your computer in the list.</span></span> <span data-ttu-id="9dd63-155">В этом случае сертификат не удаляется со всех виртуальных машин,</span><span class="sxs-lookup"><span data-stu-id="9dd63-155">This does not remove the certificate from all your VMs.</span></span> <span data-ttu-id="9dd63-156">но он и не добавляется на новые виртуальные машины, созданные в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="9dd63-156">It also does not add the certificate to new VMs that are created in the virtual machine scale set.</span></span> 

<span data-ttu-id="9dd63-157">Чтобы удалить сертификат из имеющихся виртуальных машин, напишите расширение пользовательского скрипта, которое позволяет удалить сертификат из хранилища сертификатов вручную.</span><span class="sxs-lookup"><span data-stu-id="9dd63-157">To remove the certificate from existing VMs, write a custom script extension to manually remove the certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-the-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-to-store-the-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="9dd63-158">Как во время подготовки внедрить имеющийся открытый ключ SSH на уровень SSH масштабируемого набора виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="9dd63-158">How do I inject an existing SSH public key into the virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="9dd63-159">Я хочу сохранить значения открытых ключей SSH в Azure Key Vault, чтобы затем использовать их в своем шаблоне Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd63-159">I want to store the SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="9dd63-160">Если вы устанавливаете на виртуальные машины только открытый ключ SSH, его не нужно отправлять в Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9dd63-160">If you are providing the VMs only with a public SSH key, you don't need to put the public keys in Key Vault.</span></span> <span data-ttu-id="9dd63-161">Открытые ключи не являются секретом.</span><span class="sxs-lookup"><span data-stu-id="9dd63-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="9dd63-162">При создании виртуальной машины Linux открытые ключи SSH можно указать в обычном текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="9dd63-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="9dd63-163">Имя элемента конфигурации Linux</span><span class="sxs-lookup"><span data-stu-id="9dd63-163">linuxConfiguration element name</span></span> | <span data-ttu-id="9dd63-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="9dd63-164">Required</span></span> | <span data-ttu-id="9dd63-165">Тип</span><span class="sxs-lookup"><span data-stu-id="9dd63-165">Type</span></span> | <span data-ttu-id="9dd63-166">Описание</span><span class="sxs-lookup"><span data-stu-id="9dd63-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="9dd63-167">ssh</span><span class="sxs-lookup"><span data-stu-id="9dd63-167">ssh</span></span> | <span data-ttu-id="9dd63-168">Нет</span><span class="sxs-lookup"><span data-stu-id="9dd63-168">No</span></span> | <span data-ttu-id="9dd63-169">Коллекция</span><span class="sxs-lookup"><span data-stu-id="9dd63-169">Collection</span></span> | <span data-ttu-id="9dd63-170">Указывает конфигурацию ключа SSH для операционной системы Linux.</span><span class="sxs-lookup"><span data-stu-id="9dd63-170">Specifies the SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="9dd63-171">path</span><span class="sxs-lookup"><span data-stu-id="9dd63-171">path</span></span> | <span data-ttu-id="9dd63-172">Да</span><span class="sxs-lookup"><span data-stu-id="9dd63-172">Yes</span></span> | <span data-ttu-id="9dd63-173">string</span><span class="sxs-lookup"><span data-stu-id="9dd63-173">String</span></span> | <span data-ttu-id="9dd63-174">Указывает путь к файлу Linux, где должны храниться ключи SSH или сертификат.</span><span class="sxs-lookup"><span data-stu-id="9dd63-174">Specifies the Linux file path where the SSH keys or certificate should be located</span></span>
<span data-ttu-id="9dd63-175">keyData</span><span class="sxs-lookup"><span data-stu-id="9dd63-175">keyData</span></span> | <span data-ttu-id="9dd63-176">Да</span><span class="sxs-lookup"><span data-stu-id="9dd63-176">Yes</span></span> | <span data-ttu-id="9dd63-177">Строка</span><span class="sxs-lookup"><span data-stu-id="9dd63-177">String</span></span> | <span data-ttu-id="9dd63-178">Указывает открытый ключ SSH в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="9dd63-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="9dd63-179">Пример см. в [шаблоне быстрого запуска 101-vm-sshkey на сайте GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9dd63-179">For an example, see [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-the-same-key-vault-i-see-the-following-message"></a><span data-ttu-id="9dd63-180">При выполнении команды `Update-AzureRmVmss` после добавления нескольких сертификатов из одного хранилища ключей отображается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="9dd63-180">When I run `Update-AzureRmVmss` after adding more than one certificate from the same key vault, I see the following message:</span></span>
 
><span data-ttu-id="9dd63-181">Update-AzureRmVmss: список секретов содержит повторяющиеся экземпляры /subscriptions/<идентификатор_моей_подписки>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, которые запрещены.</span><span class="sxs-lookup"><span data-stu-id="9dd63-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="9dd63-182">Такая ситуация может произойти при попытке повторно добавить то же хранилище вместо использования нового сертификата хранилища для имеющегося исходного хранилища.</span><span class="sxs-lookup"><span data-stu-id="9dd63-182">This can happen if you try to re-add the same vault instead of using a new vault certificate for the existing source vault.</span></span> <span data-ttu-id="9dd63-183">Команда `Add-AzureRmVmssSecret` не работает должным образом при добавлении дополнительных секретов.</span><span class="sxs-lookup"><span data-stu-id="9dd63-183">The `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="9dd63-184">Чтобы добавить дополнительные секреты из одного хранилища ключей, обновите список $vmss.properties.osProfile.secrets[0].vaultCertificates.</span><span class="sxs-lookup"><span data-stu-id="9dd63-184">To add more secrets from the same key vault, update the $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="9dd63-185">Ожидаемую структуру входных данных см. в разделе о [создании и обновлении масштабируемого набора виртуальных машин](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="9dd63-185">For the expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="9dd63-186">Сначала найдите секрет в объекте масштабируемого набора виртуальных машин, который находится в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="9dd63-186">Find the secret in the virtual machine scale set object that is in the key vault.</span></span> <span data-ttu-id="9dd63-187">Затем добавьте ссылку на сертификат (URL-адрес и имя хранилища секретов) в список, связанный с хранилищем.</span><span class="sxs-lookup"><span data-stu-id="9dd63-187">Then, add your certificate reference (the URL and the secret store name) to the list associated with the vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="9dd63-188">Сейчас вы не можете удалить сертификаты из виртуальной машины через API-интерфейс масштабируемого набора виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9dd63-188">Currently, you cannot remove certificates from VMs by using the virtual machine scale set API.</span></span>
>

<span data-ttu-id="9dd63-189">На новые виртуальные машины старый сертификат добавляться не будет,</span><span class="sxs-lookup"><span data-stu-id="9dd63-189">New VMs will not have the old certificate.</span></span> <span data-ttu-id="9dd63-190">но на развернутых виртуальных машинах, где он уже установлен, этот сертификат останется.</span><span class="sxs-lookup"><span data-stu-id="9dd63-190">However, VMs that have the certificate and which are already deployed will have the old certificate.</span></span>
 
### <a name="can-i-push-certificates-to-the-virtual-machine-scale-set-without-providing-the-password-when-the-certificate-is-in-the-secret-store"></a><span data-ttu-id="9dd63-191">Можно ли, не указывая пароль, отправить сертификат в масштабируемый набор виртуальных машин, если он находится в хранилище секретов?</span><span class="sxs-lookup"><span data-stu-id="9dd63-191">Can I push certificates to the virtual machine scale set without providing the password, when the certificate is in the secret store?</span></span>

<span data-ttu-id="9dd63-192">Пароли не нужно жестко определять в скриптах.</span><span class="sxs-lookup"><span data-stu-id="9dd63-192">You do not need to hard-code passwords in scripts.</span></span> <span data-ttu-id="9dd63-193">Их можно динамически извлечь на основе разрешений, используемых для выполнения скрипта развертывания.</span><span class="sxs-lookup"><span data-stu-id="9dd63-193">You can dynamically retrieve passwords with the permissions you use to run the deployment script.</span></span> <span data-ttu-id="9dd63-194">При выполнении скрипта, который перемещает сертификат из хранилища секретов в хранилище ключей, команда `get certificate`, выполняемая в хранилище секретов, также возвращает пароль для доступа к PFX-файлу.</span><span class="sxs-lookup"><span data-stu-id="9dd63-194">If you have a script that moves a certificate from the secret store key vault, the secret store `get certificate` command also outputs the password of the .pfx file.</span></span>
 
### <a name="how-does-the-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-the-sourcevault-value-when-i-have-to-specify-the-absolute-uri-for-a-certificate-by-using-the-certificateurl-property"></a><span data-ttu-id="9dd63-195">Как работает свойство Secrets в разделе virtualMachineProfile.osProfile масштабируемого набора виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="9dd63-195">How does the Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="9dd63-196">Зачем нужно указывать исходное хранилище при определении абсолютного URI сертификата с использованием свойства certificateUrl?</span><span class="sxs-lookup"><span data-stu-id="9dd63-196">Why do I need the sourceVault value when I have to specify the absolute URI for a certificate by using the certificateUrl property?</span></span> 

<span data-ttu-id="9dd63-197">В свойстве Secrets профиля ОС должна находиться ссылка на сертификат службы удаленного управления Windows (WinRM).</span><span class="sxs-lookup"><span data-stu-id="9dd63-197">A Windows Remote Management (WinRM) certificate reference must be present in the Secrets property of the OS profile.</span></span> 

<span data-ttu-id="9dd63-198">Указав исходное хранилище, вы сможете применить политики списка управления доступом (ACL), определенные в модели облачной службы Azure пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dd63-198">The purpose of indicating the source vault is to enforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="9dd63-199">Если его не указать, пользователи без необходимых разрешений смогут развертывать или использовать секреты в хранилище ключей с помощью поставщика вычислительных ресурсов (CRP).</span><span class="sxs-lookup"><span data-stu-id="9dd63-199">If the source vault isn't specified, users who do not have permissions to deploy or access secrets to a key vault would be able to through a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="9dd63-200">Политики ACL применяются даже к еще не созданным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="9dd63-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="9dd63-201">Если указать неправильный идентификатор исходного хранилища, но допустимый URL-адрес хранилища ключей, при опросе операции отобразится ошибка.</span><span class="sxs-lookup"><span data-stu-id="9dd63-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll the operation.</span></span>
 
### <a name="if-i-add-secrets-to-an-existing-virtual-machine-scale-set-are-the-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="9dd63-202">При добавлении секретов в имеющийся масштабируемый набор они применяются ко всем виртуальным машинам или только к новым?</span><span class="sxs-lookup"><span data-stu-id="9dd63-202">If I add secrets to an existing virtual machine scale set, are the secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="9dd63-203">Сертификаты добавляются на все виртуальные машины, в том числе на имеющиеся.</span><span class="sxs-lookup"><span data-stu-id="9dd63-203">Certificates are added to all your VMs, even preexisting ones.</span></span> <span data-ttu-id="9dd63-204">Если для свойства upgradePolicy масштабируемого набора виртуальных машин задано значение **manual**, сертификат добавляется в процессе обновления виртуальной машины вручную.</span><span class="sxs-lookup"><span data-stu-id="9dd63-204">If your virtual machine scale set upgradePolicy property is set to **manual**, the certificate is added to the VM when you perform a manual update on the VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="9dd63-205">Куда следует поместить сертификаты виртуальных машин Linux?</span><span class="sxs-lookup"><span data-stu-id="9dd63-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="9dd63-206">Дополнительные сведения о развертывании сертификатов виртуальных машин Linux из хранилища ключей, управляемого клиентом, см. в [этой записи блога](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-206">To learn how to deploy certificates for Linux VMs, see [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-to-a-new-certificate-object"></a><span data-ttu-id="9dd63-207">Как добавить новый сертификат хранилища в новый объект сертификата?</span><span class="sxs-lookup"><span data-stu-id="9dd63-207">How do I add a new vault certificate to a new certificate object?</span></span>

<span data-ttu-id="9dd63-208">Чтобы добавить сертификат хранилища в имеющийся секрет, используйте приведенный ниже пример сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9dd63-208">To add a vault certificate to an existing secret, see the following PowerShell example.</span></span> <span data-ttu-id="9dd63-209">Используйте только один объект секрета.</span><span class="sxs-lookup"><span data-stu-id="9dd63-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-to-certificates-if-you-reimage-a-vm"></a><span data-ttu-id="9dd63-210">Что происходит с сертификатами после пересоздания образа виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="9dd63-210">What happens to certificates if you reimage a VM?</span></span>

<span data-ttu-id="9dd63-211">После пересоздания образа виртуальной машины сертификаты удаляются.</span><span class="sxs-lookup"><span data-stu-id="9dd63-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="9dd63-212">В рамках этого процесса полностью удаляется диск ОС.</span><span class="sxs-lookup"><span data-stu-id="9dd63-212">Reimaging deletes the entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-the-key-vault"></a><span data-ttu-id="9dd63-213">Что происходит после удаления сертификата из хранилища ключей?</span><span class="sxs-lookup"><span data-stu-id="9dd63-213">What happens if you delete a certificate from the key vault?</span></span>

<span data-ttu-id="9dd63-214">Если удалить секрет из хранилища ключей и отменить выделение всех виртуальных машин с помощью команды `stop deallocate`, а затем снова запустить этот процесс, произойдет сбой.</span><span class="sxs-lookup"><span data-stu-id="9dd63-214">If the secret is deleted from the key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="9dd63-215">Этот сбой связан с тем, что CRP не может получить секреты из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9dd63-215">The failure occurs because the CRP needs to retrieve the secrets from the key vault, but it cannot.</span></span> <span data-ttu-id="9dd63-216">В этом случае вы можете удалить сертификаты из модели масштабируемого набора виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9dd63-216">In this scenario, you can delete the certificates from the virtual machine scale set model.</span></span> 

<span data-ttu-id="9dd63-217">Компонент CRP не сохраняет секреты клиента.</span><span class="sxs-lookup"><span data-stu-id="9dd63-217">The CRP component does not persist customer secrets.</span></span> <span data-ttu-id="9dd63-218">При выполнении команды `stop deallocate` для всех виртуальных машин в масштабируемом наборе кэш удаляется.</span><span class="sxs-lookup"><span data-stu-id="9dd63-218">If you run `stop deallocate` for all VMs in the virtual machine scale set, the cache is deleted.</span></span> <span data-ttu-id="9dd63-219">В этом случае секреты извлекаются из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9dd63-219">In this scenario, secrets are retrieved from the key vault.</span></span>

<span data-ttu-id="9dd63-220">Эта проблема не влияет на масштабирование, так как в Azure Service Fabric хранится кэшированная копия секрета (в модели с одним клиентом Fabric).</span><span class="sxs-lookup"><span data-stu-id="9dd63-220">You don't encounter this problem when scaling out because there is a cached copy of the secret in Azure Service Fabric (in the single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-to-specify-the-exact-location-for-the-certificate-url-httpsname-of-the-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="9dd63-221">Почему нужно указать точное расположение URL-адреса сертификата (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), как указано в статье [Сценарии защиты кластера Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="9dd63-221">Why do I have to specify the exact location for the certificate URL (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="9dd63-222">В соответствии с документацией по Azure Key Vault, если версия секрета не указана, REST API получения секрета должен вернуть последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="9dd63-222">The Azure Key Vault documentation states that the Get Secret REST API should return the latest version of the secret if the version is not specified.</span></span>
 
<span data-ttu-id="9dd63-223">Метод</span><span class="sxs-lookup"><span data-stu-id="9dd63-223">Method</span></span> | <span data-ttu-id="9dd63-224">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="9dd63-224">URL</span></span>
--- | ---
<span data-ttu-id="9dd63-225">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="9dd63-225">GET</span></span> | <span data-ttu-id="9dd63-226">https://mykeyvault.vault.azure.net/secrets/{имя_секрета}/{версия_секрета}?api-version={версия_API}</span><span class="sxs-lookup"><span data-stu-id="9dd63-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="9dd63-227">Замените параметры {*имя_секрета*} и {*версия_секрета*} именем и версией секрета, которую необходимо получить.</span><span class="sxs-lookup"><span data-stu-id="9dd63-227">Replace {*secret-name*} with the name, and replace {*secret-version*} with the version of the secret you want to retrieve.</span></span> <span data-ttu-id="9dd63-228">Версию секрета можно не указывать.</span><span class="sxs-lookup"><span data-stu-id="9dd63-228">The secret version might be excluded.</span></span> <span data-ttu-id="9dd63-229">В этом случае извлекается текущая версия.</span><span class="sxs-lookup"><span data-stu-id="9dd63-229">In that case, the current version is retrieved.</span></span>
  
### <a name="why-do-i-have-to-specify-the-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="9dd63-230">Почему при использовании Key Vault необходимо указать версию сертификата?</span><span class="sxs-lookup"><span data-stu-id="9dd63-230">Why do I have to specify the certificate version when I use Key Vault?</span></span>

<span data-ttu-id="9dd63-231">Указание версии сертификата в Key Vault позволяет пользователям понять, какой сертификат развернут на их виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="9dd63-231">The purpose of the Key Vault requirement to specify the certificate version is to make it clear to the user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="9dd63-232">Если вы создаете виртуальную машину, а затем обновляете секрет в хранилище ключей, новый сертификат не загружается на виртуальные машины,</span><span class="sxs-lookup"><span data-stu-id="9dd63-232">If you create a VM and then update your secret in the key vault, the new certificate is not downloaded to your VMs.</span></span> <span data-ttu-id="9dd63-233">но ссылка на него отображается. При создании виртуальных машин на них устанавливается новый секрет.</span><span class="sxs-lookup"><span data-stu-id="9dd63-233">But your VMs appear to reference it, and new VMs get the new secret.</span></span> <span data-ttu-id="9dd63-234">Чтобы избежать этого, необходимо добавить ссылку на версию секрета.</span><span class="sxs-lookup"><span data-stu-id="9dd63-234">To avoid this, you are required to reference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-to-us-as-cer-public-keys-what-is-the-recommended-approach-for-deploying-these-certificates-to-a-virtual-machine-scale-set"></a><span data-ttu-id="9dd63-235">Моя группа работает с несколькими сертификатами, добавленными как файлы сертификата открытого ключа (CER-файлы).</span><span class="sxs-lookup"><span data-stu-id="9dd63-235">My team works with several certificates that are distributed to us as .cer public keys.</span></span> <span data-ttu-id="9dd63-236">Какой метод вы рекомендуете использовать для развертывания этих сертификатов в масштабируемом наборе виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="9dd63-236">What is the recommended approach for deploying these certificates to a virtual machine scale set?</span></span>

<span data-ttu-id="9dd63-237">Чтобы развернуть файлы сертификата открытого ключа (CER-файлы) в масштабируемый набор виртуальных машин, вы можете создать PFX-файл, содержащий только CER-файлы.</span><span class="sxs-lookup"><span data-stu-id="9dd63-237">To deploy .cer public keys to a virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="9dd63-238">Для этого используйте параметр `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="9dd63-238">To do this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="9dd63-239">Например, отправьте CER-файл как объект x509Certificate2 в C# и PowerShell, а затем вызовите метод X509Certificate.Export.</span><span class="sxs-lookup"><span data-stu-id="9dd63-239">For example, load the .cer file as an x509Certificate2 object in C# or PowerShell, and then call the method.</span></span> 

<span data-ttu-id="9dd63-240">Дополнительные сведения о методе X509Certificate.Export см. в [этой статье](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="9dd63-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-to-pass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="9dd63-241">Я не вижу параметр для передачи сертификатов в виде строк в формате Base64.</span><span class="sxs-lookup"><span data-stu-id="9dd63-241">I do not see an option for users to pass in certificates as base64 strings.</span></span> <span data-ttu-id="9dd63-242">Большинство других поставщиков ресурсов предоставляют этот параметр.</span><span class="sxs-lookup"><span data-stu-id="9dd63-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="9dd63-243">Чтобы выполнить эмуляцию передачи сертификата в виде строки в формате Base64, можно извлечь последнюю версию URL-адреса в шаблоне Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd63-243">To emulate passing in a certificate as a base64 string, you can extract the latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="9dd63-244">Включите в шаблон Resource Manager следующее свойство JSON:</span><span class="sxs-lookup"><span data-stu-id="9dd63-244">Include the following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-to-wrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="9dd63-245">Нужно ли помещать сертификаты в объекты JSON в хранилищах ключей?</span><span class="sxs-lookup"><span data-stu-id="9dd63-245">Do I have to wrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="9dd63-246">В масштабируемых наборах и на виртуальных машинах сертификаты нужно помещать в объекты JSON.</span><span class="sxs-lookup"><span data-stu-id="9dd63-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="9dd63-247">Мы также поддерживаем тип содержимого application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="9dd63-247">We also support the content type application/x-pkcs12.</span></span> <span data-ttu-id="9dd63-248">Инструкции по использованию application/x-pkcs12 см. в записи блога об [использовании PFX-сертификатов в Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="9dd63-249">Сейчас мы не поддерживаем CER-файлы.</span><span class="sxs-lookup"><span data-stu-id="9dd63-249">We currently do not support .cer files.</span></span> <span data-ttu-id="9dd63-250">Чтобы использовать CER-файлы, экспортируйте их в PFX-контейнеры.</span><span class="sxs-lookup"><span data-stu-id="9dd63-250">To use .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="9dd63-251">Соответствие нормативным требованиям</span><span class="sxs-lookup"><span data-stu-id="9dd63-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="9dd63-252">Соответствуют ли масштабируемые наборы виртуальных машин требованиям стандарта PCI?</span><span class="sxs-lookup"><span data-stu-id="9dd63-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="9dd63-253">Масштабируемые наборы виртуальных машин представляют собой тонкий слой API поверх поставщика вычислительных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9dd63-253">Virtual machine scale sets are a thin API layer on top of the CRP.</span></span> <span data-ttu-id="9dd63-254">Оба компонента входят в состав вычислительной платформы в дереве службы Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd63-254">Both components are part of the compute platform in the Azure service tree.</span></span>

<span data-ttu-id="9dd63-255">С точки зрения соответствия масштабируемые наборы виртуальных машин являются основной частью вычислительной платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd63-255">From a compliance perspective, virtual machine scale sets are a fundamental part of the Azure compute platform.</span></span> <span data-ttu-id="9dd63-256">Они используют те же группы, средства, процессы, методы развертывания, элементы управления безопасностью, JIT-компиляцию, возможности мониторинга, оповещения и т. д., что и поставщик вычислительных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9dd63-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with the CRP itself.</span></span> <span data-ttu-id="9dd63-257">Масштабируемые наборы виртуальных машин соответствуют требованиям сферы платежных карт, так как поставщик вычислительных ресурсов является частью аттестации по требованиям Стандарта безопасности данных в сфере платежных карт (PCI DSS).</span><span class="sxs-lookup"><span data-stu-id="9dd63-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because the CRP is part of the current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="9dd63-258">Дополнительные сведения см. в [центре управления безопасностью Майкрософт](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="9dd63-258">For more information, see [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="9dd63-259">расширения.</span><span class="sxs-lookup"><span data-stu-id="9dd63-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="9dd63-260">Как удалить расширение масштабируемого набора виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="9dd63-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="9dd63-261">Чтобы удалить расширение масштабируемого набора виртуальных машин, используйте следующий пример сценария PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9dd63-261">To delete a virtual machine scale set extension, use the following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="9dd63-262">Значение параметра extensionName находится в строке `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="9dd63-262">You can find the extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="9dd63-263">Существует ли пример шаблона масштабируемого набора виртуальных машин, который интегрируется с Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="9dd63-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="9dd63-264">Пример шаблона масштабируемого набора виртуальных машин, который интегрируется с Operations Management Suite, см. во втором примере статьи о [развертывании кластера Azure Service Fabric и включении мониторинга с помощью Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="9dd63-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see the second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-to-run-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-to-fail-what-can-i-do-to-fix-this"></a><span data-ttu-id="9dd63-265">Похоже, что расширения выполняются в масштабируемых наборах виртуальных машин одновременно.</span><span class="sxs-lookup"><span data-stu-id="9dd63-265">Extensions seem to run in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="9dd63-266">В результате этого выполнение операции настраиваемого расширения скриптов завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="9dd63-266">This causes my custom script extension to fail.</span></span> <span data-ttu-id="9dd63-267">Как это исправить?</span><span class="sxs-lookup"><span data-stu-id="9dd63-267">What can I do to fix this?</span></span>

<span data-ttu-id="9dd63-268">Дополнительные сведения о виртуализации расширений в масштабируемых наборах виртуальных машин см. в [этой статье](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-268">To learn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-the-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="9dd63-269">Как сбросить пароль виртуальных машин в масштабируемом наборе?</span><span class="sxs-lookup"><span data-stu-id="9dd63-269">How do I reset the password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="9dd63-270">Чтобы сбросить пароль виртуальных машин в масштабируемом наборе, используйте расширения доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9dd63-270">To reset the password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="9dd63-271">Используйте следующий пример сценария PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9dd63-271">Use the following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-to-all-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="9dd63-272">Как добавить расширение для всех виртуальных машин в масштабируемом наборе?</span><span class="sxs-lookup"><span data-stu-id="9dd63-272">How do I add an extension to all VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="9dd63-273">Если политика обновления настроена на **автоматическое** обновление, при повторном развертывании шаблона новые свойства расширения применяются на всех виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="9dd63-273">If update policy is set to **automatic**, redeploying the template with the new extension properties updates all VMs.</span></span>

<span data-ttu-id="9dd63-274">Если политика обновления настроена на обновление **вручную**, сначала обновите расширение, а затем вручную обновите все экземпляры на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="9dd63-274">If update policy is set to **manual**, first update the extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-the-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-the-vms-not-match-the-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-the-scripts-that-are-currently-configured-on-the-virtual-machine-scale-set-executed-or-are-the-scripts-that-were-configured-when-the-vm-was-first-created-used"></a><span data-ttu-id="9dd63-275">Если обновить расширения, связанные с имеющимся масштабируемым набором, повлияет ли это на имеющиеся виртуальные машины?</span><span class="sxs-lookup"><span data-stu-id="9dd63-275">If the extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="9dd63-276">(То есть *не* перестанут ли виртуальные машины соответствовать требованиям модели масштабируемого набора виртуальных машин?) Или они игнорируются?</span><span class="sxs-lookup"><span data-stu-id="9dd63-276">(That is, will the VMs *not* match the virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="9dd63-277">После пересоздания образа или восстановления имеющейся машины будут ли выполняться скрипты, настроенные в настоящее время в масштабируемом наборе, или будут использоваться скрипты, настроенные при первом создании машины виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="9dd63-277">When an existing machine is service-healed or reimaged, are the scripts that are currently configured on the virtual machine scale set executed, or are the scripts that were configured when the VM was first created used?</span></span>

<span data-ttu-id="9dd63-278">Если обновляется определение расширения в модели масштабируемого набора виртуальных машин, а для свойства upgradePolicy задано значение **automatic**, обновляются и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="9dd63-278">If the extension definition in the virtual machine scale set model is updated and the upgradePolicy property is set to **automatic**, it updates the VMs.</span></span> <span data-ttu-id="9dd63-279">Если для свойства upgradePolicy задано значение **manual**, расширения помечаются как несоответствующие требованиям модели.</span><span class="sxs-lookup"><span data-stu-id="9dd63-279">If the upgradePolicy property is set to **manual**, extensions are flagged as not matching the model.</span></span> 

<span data-ttu-id="9dd63-280">Если виртуальная машина восстановлена, она рассматривается как прошедшая перезагрузку, и расширения повторно не запускаются.</span><span class="sxs-lookup"><span data-stu-id="9dd63-280">If an existing VM is service-healed, it appears as a reboot, and the extensions are not rerun.</span></span> <span data-ttu-id="9dd63-281">Пересоздание образа напоминает замену диска ОС на исходный образ.</span><span class="sxs-lookup"><span data-stu-id="9dd63-281">If it is reimaged, it's like replacing the OS drive with the source image.</span></span> <span data-ttu-id="9dd63-282">В этом случае запускаются все специализации, например расширения, из последней модели.</span><span class="sxs-lookup"><span data-stu-id="9dd63-282">Any specialization from the latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-to-an-azure-ad-domain"></a><span data-ttu-id="9dd63-283">Как присоединить масштабируемый набор виртуальных машин к домену Azure Active Directory (Azure AD)?</span><span class="sxs-lookup"><span data-stu-id="9dd63-283">How do I join a virtual machine scale set to an Azure AD domain?</span></span>

<span data-ttu-id="9dd63-284">Чтобы присоединить масштабируемый набор виртуальных машин к домену Azure AD, можно определить расширение.</span><span class="sxs-lookup"><span data-stu-id="9dd63-284">To join a virtual machine scale set to an Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="9dd63-285">Чтобы определить расширение, используйте свойство JsonADDomainExtension.</span><span class="sxs-lookup"><span data-stu-id="9dd63-285">To define an extension, use the JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-to-install-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="9dd63-286">Расширение масштабируемого набора виртуальных машин пытается установить что-то, требующее перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="9dd63-286">My virtual machine scale set extension is trying to install something that requires a reboot.</span></span> <span data-ttu-id="9dd63-287">Например, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools".</span><span class="sxs-lookup"><span data-stu-id="9dd63-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="9dd63-288">Если расширение масштабируемого набора виртуальных машин пытается установить что-то, требующее перезагрузки, вы можете использовать расширение настройки требуемого состояния службы автоматизации Azure (Automation DSC).</span><span class="sxs-lookup"><span data-stu-id="9dd63-288">If your virtual machine scale set extension is trying to install something that requires a reboot, you can use the Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="9dd63-289">При использовании операционной системы Windows Server 2012 R2 Azure запрашивает установку и перезагрузку Windows Management Framework (WMF) 5.0, а затем выполняет настройку.</span><span class="sxs-lookup"><span data-stu-id="9dd63-289">If the operating system is Windows Server 2012 R2, Azure pulls in the Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with the configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="9dd63-290">Как включить антивредоносную программу в масштабируемом наборе виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="9dd63-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="9dd63-291">Чтобы включить антивредоносную программу в масштабируемом наборе виртуальных машин, используйте следующий пример сценария PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9dd63-291">To turn on antimalware on your virtual machine scale set, use the following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve the most recent version number of the extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-to-execute-a-custom-script-thats-hosted-in-a-private-storage-account-the-script-runs-successfully-when-the-storage-is-public-but-when-i-try-to-use-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="9dd63-292">Мне нужно выполнить настраиваемый скрипт, размещенный в учетной записи частного хранилища.</span><span class="sxs-lookup"><span data-stu-id="9dd63-292">I need to execute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="9dd63-293">При использовании общедоступного хранилища скрипт выполняется успешно, но когда я использую подписанный URL-адрес, он завершается сбоем</span><span class="sxs-lookup"><span data-stu-id="9dd63-293">The script runs successfully when the storage is public, but when I try to use a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="9dd63-294">и отображается следующее сообщение об ошибке: "Отсутствуют обязательные параметры для допустимой подписи коллективного доступа".</span><span class="sxs-lookup"><span data-stu-id="9dd63-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="9dd63-295">В локальном браузере проблемы с подписанным URL-адресом и ссылкой не возникали.</span><span class="sxs-lookup"><span data-stu-id="9dd63-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="9dd63-296">Чтобы выполнить настраиваемый скрипт, размещенный в учетной записи частного хранилища, настройте защищенные параметры с использованием имени и ключа учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9dd63-296">To execute a custom script that's hosted in a private storage account, set up protected settings with the storage account key and name.</span></span> <span data-ttu-id="9dd63-297">Дополнительные сведения см. в статье [Расширение Custom Script в ОС Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="9dd63-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="9dd63-298">Сеть</span><span class="sxs-lookup"><span data-stu-id="9dd63-298">Networking</span></span>
 
### <a name="is-it-possible-to-assign-a-network-security-group-nsg-to-a-scale-set-so-that-it-will-apply-to-all-the-vm-nics-in-the-set"></a><span data-ttu-id="9dd63-299">Можно ли назначить группу безопасности сети масштабируемому набору, чтобы она применялась ко всем сетевым картам виртуальных машин в наборе?</span><span class="sxs-lookup"><span data-stu-id="9dd63-299">Is it possible to assign a Network Security Group (NSG) to a scale set, so that it will apply to all the VM NICs in the set?</span></span>

<span data-ttu-id="9dd63-300">Да.</span><span class="sxs-lookup"><span data-stu-id="9dd63-300">Yes.</span></span> <span data-ttu-id="9dd63-301">Группу безопасности сети можно применить непосредственно к масштабируемому набору, указав ее в разделе networkInterfaceConfigurations сетевого профиля.</span><span class="sxs-lookup"><span data-stu-id="9dd63-301">A Network Security Group can be applied directly to a scale set by referencing it in the networkInterfaceConfigurations section of the network profile.</span></span> <span data-ttu-id="9dd63-302">Пример:</span><span class="sxs-lookup"><span data-stu-id="9dd63-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-the-same-subscription-and-same-region"></a><span data-ttu-id="9dd63-303">Как переключить виртуальный IP-адрес для масштабируемого набора виртуальных машин в той же подписке и в том же регионе?</span><span class="sxs-lookup"><span data-stu-id="9dd63-303">How do I do a VIP swap for virtual machine scale sets in the same subscription and same region?</span></span>

<span data-ttu-id="9dd63-304">Если у вас есть два масштабируемых набора виртуальных машин с внешними интерфейсами Azure Load Balancer и они находятся в одной подписке и регионе, можно освободить общедоступные IP-адреса в одном из них и назначить их другому.</span><span class="sxs-lookup"><span data-stu-id="9dd63-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in the same subscription and region, you could deallocate the public IP addresses from each one, and assign to the other.</span></span> <span data-ttu-id="9dd63-305">Пример приведен в статье [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Переключение виртуальных IP-адресов: развертывание по схеме "blue-green" в Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="9dd63-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="9dd63-306">Это подразумевает задержку, так как ресурсы освобождаются и выделяются на уровне сети.</span><span class="sxs-lookup"><span data-stu-id="9dd63-306">This does imply a delay though as the resources are deallocated/allocated at the network level.</span></span> <span data-ttu-id="9dd63-307">Другой, более быстрый вариант — воспользоваться шлюзом приложений Azure с двумя серверными пулами и правилом маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="9dd63-307">A faster option is to use Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="9dd63-308">Также можно разместить приложение в [службе приложений Azure](https://azure.microsoft.com/en-us/services/app-service/), которая обеспечивает быстрое переключение между промежуточными и рабочими слотами.</span><span class="sxs-lookup"><span data-stu-id="9dd63-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-to-use-for-static-private-ip-address-allocation"></a><span data-ttu-id="9dd63-309">Как указать диапазон частных IP-адресов для выделения статических частных IP-адресов?</span><span class="sxs-lookup"><span data-stu-id="9dd63-309">How do I specify a range of private IP addresses to use for static private IP address allocation?</span></span>

<span data-ttu-id="9dd63-310">IP-адреса выбираются из указанной подсети.</span><span class="sxs-lookup"><span data-stu-id="9dd63-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="9dd63-311">При выделении IP-адресов масштабируемого набора виртуальных машин всегда используется динамический метод, но это не означает, что эти IP-адреса можно изменить.</span><span class="sxs-lookup"><span data-stu-id="9dd63-311">The allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="9dd63-312">В этом случае под динамическим методом подразумевается, что вам не нужно указывать IP-адрес в запросе PUT.</span><span class="sxs-lookup"><span data-stu-id="9dd63-312">In this case, "dynamic" only means that you do not specify the IP address in a PUT request.</span></span> <span data-ttu-id="9dd63-313">Укажите статический набор на основе подсети.</span><span class="sxs-lookup"><span data-stu-id="9dd63-313">Specify the static set by using the subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-to-an-existing-azure-virtual-network"></a><span data-ttu-id="9dd63-314">Как развернуть масштабируемый набор виртуальных машин в имеющейся виртуальной сети Azure?</span><span class="sxs-lookup"><span data-stu-id="9dd63-314">How do I deploy a virtual machine scale set to an existing Azure virtual network?</span></span> 

<span data-ttu-id="9dd63-315">Чтобы развернуть масштабируемый набор виртуальных машин в имеющейся виртуальной сети Azure, используйте [этот шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="9dd63-315">To deploy a virtual machine scale set to an existing Azure virtual network, see [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-the-ip-address-of-the-first-vm-in-a-virtual-machine-scale-set-to-the-output-of-a-template"></a><span data-ttu-id="9dd63-316">Как добавить IP-адрес первой виртуальной машины в масштабируемом наборе к выходным данным шаблона?</span><span class="sxs-lookup"><span data-stu-id="9dd63-316">How do I add the IP address of the first VM in a virtual machine scale set to the output of a template?</span></span>

<span data-ttu-id="9dd63-317">Дополнительные сведения о добавлении IP-адреса первой виртуальной машины в масштабируемом наборе к выходным данным шаблона см. в ответе на вопрос о [получении частных IP-адресов VMSS](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="9dd63-317">To add the IP address of the first VM in a virtual machine scale set to the output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="9dd63-318">Можно ли использовать масштабируемые наборы с ускоренной сетью?</span><span class="sxs-lookup"><span data-stu-id="9dd63-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="9dd63-319">Да.</span><span class="sxs-lookup"><span data-stu-id="9dd63-319">Yes.</span></span> <span data-ttu-id="9dd63-320">Чтобы использовать ускоренную сеть, в настройках networkInterfaceConfigurations масштабируемого набора задайте для параметра enableAcceleratedNetworking значение true.</span><span class="sxs-lookup"><span data-stu-id="9dd63-320">To use accelerated networking, set enableAcceleratedNetworking to true in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="9dd63-321">Например: </span><span class="sxs-lookup"><span data-stu-id="9dd63-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-the-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="9dd63-322">Как настроить DNS-серверы, используемые масштабируемым набором?</span><span class="sxs-lookup"><span data-stu-id="9dd63-322">How can I configure the DNS servers used by a scale set?</span></span>

<span data-ttu-id="9dd63-323">Чтобы создать масштабируемый набор виртуальных машин с пользовательской конфигурацией DNS, добавьте пакет JSON dnsSettings в раздел networkInterfaceConfigurations конфигурации масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="9dd63-323">To create a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="9dd63-324">Пример:</span><span class="sxs-lookup"><span data-stu-id="9dd63-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-to-assign-a-public-ip-address-to-each-vm"></a><span data-ttu-id="9dd63-325">Как настроить масштабируемый набор, чтобы назначать общедоступный IP-адрес каждой виртуальной машине?</span><span class="sxs-lookup"><span data-stu-id="9dd63-325">How can I configure a scale set to assign a public IP address to each VM?</span></span>

<span data-ttu-id="9dd63-326">Чтобы создать масштабируемый набор виртуальных машин, назначающий общедоступный IP-адрес каждой виртуальной машине, убедитесь, что версия API ресурса Microsoft.Compute/virtualMAchineScaleSets — 2017-03-30, и добавьте пакет JSON _publicipaddressconfiguration_ в раздел ipConfigurations конфигурации масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="9dd63-326">To create a VM scale set that assigns a public IP address to each VM, make sure the API version of the Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet to the scale set ipConfigurations section.</span></span> <span data-ttu-id="9dd63-327">Пример:</span><span class="sxs-lookup"><span data-stu-id="9dd63-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-to-work-with-multiple-application-gateways"></a><span data-ttu-id="9dd63-328">Можно ли настроить масштабируемый набор для работы с несколькими шлюзами приложений?</span><span class="sxs-lookup"><span data-stu-id="9dd63-328">Can I configure a scale set to work with multiple Application Gateways?</span></span>

<span data-ttu-id="9dd63-329">Да.</span><span class="sxs-lookup"><span data-stu-id="9dd63-329">Yes.</span></span> <span data-ttu-id="9dd63-330">Можно добавить идентификаторы ресурсов для нескольких серверных пулов адресов шлюза приложений в список _applicationGatewayBackendAddressPools_ в разделе _ipConfigurations_ сетевого профиля масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="9dd63-330">You can add the resource id's for multiple Application Gateway backend address pools to the _applicationGatewayBackendAddressPools_ list in the _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="9dd63-331">Масштаб</span><span class="sxs-lookup"><span data-stu-id="9dd63-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="9dd63-332">В каких случаях следует создавать масштабируемый набор с одной виртуальной машиной или без них?</span><span class="sxs-lookup"><span data-stu-id="9dd63-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="9dd63-333">Одна из причин заключается в использовании эластичных свойств масштабируемого набора виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9dd63-333">One reason to create a virtual machine scale set with fewer than two VMs would be to use the elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="9dd63-334">Например, вы можете развернуть масштабируемый набор без виртуальных машин, чтобы определить инфраструктуру, не платя за выполнение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9dd63-334">For example, you could deploy a virtual machine scale set with zero VMs to define your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="9dd63-335">Затем при развертывании виртуальных машин вы можете увеличить емкость масштабируемого набора в соответствии с количеством рабочих экземпляров.</span><span class="sxs-lookup"><span data-stu-id="9dd63-335">Then, when you are ready to deploy VMs, increase the “capacity” of the virtual machine scale set to the production instance count.</span></span>

<span data-ttu-id="9dd63-336">Вторая причина заключается в том, что в масштабируемом наборе выполняются операции, не учитывающие доступность в таком же смысле, что и группы доступности с отдельными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="9dd63-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="9dd63-337">Масштабируемые наборы виртуальных машин позволяют работать с взаимозаменяемыми недифференцированными единицами вычислений.</span><span class="sxs-lookup"><span data-stu-id="9dd63-337">Virtual machine scale sets give you a way to work with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="9dd63-338">Это единообразие является ключевым преимуществом при выборе между масштабируемыми наборами виртуальных машин и группами доступности.</span><span class="sxs-lookup"><span data-stu-id="9dd63-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="9dd63-339">Многие рабочие нагрузки без отслеживания состояния не учитывают отдельные единицы.</span><span class="sxs-lookup"><span data-stu-id="9dd63-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="9dd63-340">Если рабочая нагрузка снижается, вы можете уменьшить масштаб до одной единицы вычисления, а при увеличении нагрузки — снова увеличить количество этих единиц.</span><span class="sxs-lookup"><span data-stu-id="9dd63-340">If the workload drops, you can scale down to one compute unit, and then scale up to many when the workload increases.</span></span>

### <a name="how-do-i-change-the-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="9dd63-341">Как изменить количество виртуальных машин в масштабируемом наборе?</span><span class="sxs-lookup"><span data-stu-id="9dd63-341">How do I change the number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="9dd63-342">Дополнительные сведения об изменении количества виртуальных машин в масштабируемом наборе см. в [этой статье](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="9dd63-342">To change the number of VMs in a virtual machine scale set, see [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="9dd63-343">Как настроить пользовательские оповещения, отображающиеся при достижении определенных пороговых значений?</span><span class="sxs-lookup"><span data-stu-id="9dd63-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="9dd63-344">Обработкой оповещений при достижении определенных пороговых значений можно управлять несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="9dd63-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="9dd63-345">Например, вы можете определить настраиваемые объекты webhook.</span><span class="sxs-lookup"><span data-stu-id="9dd63-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="9dd63-346">Ниже приведен пример объекта webhook из шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd63-346">The following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="9dd63-347">В этом примере при достижении порогового значения оповещение отправляется на сайт Pagerduty.com.</span><span class="sxs-lookup"><span data-stu-id="9dd63-347">In this example, an alert goes to Pagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="9dd63-348">Установка исправлений и эксплуатация</span><span class="sxs-lookup"><span data-stu-id="9dd63-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="9dd63-349">Как создать масштабируемый набор в существующей группе ресурсов?</span><span class="sxs-lookup"><span data-stu-id="9dd63-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="9dd63-350">Создание масштабируемых наборов в существующей группе ресурсов на портале Azure пока невозможно, но можно указать существующую группу ресурсов при развертывании масштабируемого набора с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd63-350">Creating scale sets in an existing resource group is not yet possible from the Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="9dd63-351">Можно также указать существующую группу ресурсов при создании масштабируемого набора с помощью Azure PowerShell или интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="9dd63-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-to-another-resource-group"></a><span data-ttu-id="9dd63-352">Можно ли переместить масштабируемый набор другую группу ресурсов?</span><span class="sxs-lookup"><span data-stu-id="9dd63-352">Can we move a scale set to another resource group?</span></span>

<span data-ttu-id="9dd63-353">Да, ресурсы масштабируемого набора можно переместить в новую подписку или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9dd63-353">Yes, you can move scale set resources to a new subscription or resource group.</span></span>

### <a name="how-to-i-update-my-virtual-machine-scale-set-to-a-new-image-how-do-i-manage-patching"></a><span data-ttu-id="9dd63-354">Как обновить образ масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="9dd63-354">How to I update my virtual machine scale set to a new image?</span></span> <span data-ttu-id="9dd63-355">и как управлять установкой исправлений?</span><span class="sxs-lookup"><span data-stu-id="9dd63-355">How do I manage patching?</span></span>

<span data-ttu-id="9dd63-356">Дополнительные сведения об обновлении масштабируемого набора виртуальных машин и управлении установкой исправлений см. в [этой статье.](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set)</span><span class="sxs-lookup"><span data-stu-id="9dd63-356">To update your virtual machine scale set to a new image, and to manage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-the-reimage-operation-to-reset-a-vm-without-changing-the-image-that-is-i-want-reset-a-vm-to-factory-settings-rather-than-to-a-new-image"></a><span data-ttu-id="9dd63-357">Можно ли использовать операцию пересоздания образа, чтобы сбросить параметры виртуальной машины, не изменяя образ?</span><span class="sxs-lookup"><span data-stu-id="9dd63-357">Can I use the reimage operation to reset a VM without changing the image?</span></span> <span data-ttu-id="9dd63-358">(То есть я хочу сбросить параметры виртуальной машины к значениям по умолчанию, а не создавать новый образ.)</span><span class="sxs-lookup"><span data-stu-id="9dd63-358">(That is, I want reset a VM to factory settings rather than to a new image.)</span></span>

<span data-ttu-id="9dd63-359">Да. Операцию пересоздания образа можно использовать, чтобы сбросить параметры виртуальной машины, не изменяя образ.</span><span class="sxs-lookup"><span data-stu-id="9dd63-359">Yes, you can use the reimage operation to reset a VM without changing the image.</span></span> <span data-ttu-id="9dd63-360">Тем не менее, если масштабируемый набор виртуальных машин ссылается на образ платформы последней версии (значение `version = latest`), образ ОС виртуальной машины можно обновить на более позднюю версию при вызове операции `reimage`.</span><span class="sxs-lookup"><span data-stu-id="9dd63-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update to a later OS image when you call `reimage`.</span></span>

<span data-ttu-id="9dd63-361">Дополнительные сведения см. в статье об [управлении всеми виртуальными машинами в масштабируемом наборе](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="9dd63-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="9dd63-362">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="9dd63-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="9dd63-363">Как включить диагностику загрузки?</span><span class="sxs-lookup"><span data-stu-id="9dd63-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="9dd63-364">Чтобы включить диагностику загрузки, сначала создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="9dd63-364">To turn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="9dd63-365">Затем вставьте приведенный ниже блок JSON в раздел **virtualMachineProfile** масштабируемого набора виртуальных машин и обновите этот набор.</span><span class="sxs-lookup"><span data-stu-id="9dd63-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update the virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="9dd63-366">После создания виртуальной машины в свойстве InstanceView отобразятся сведения для снимка экрана и т. д.</span><span class="sxs-lookup"><span data-stu-id="9dd63-366">When a new VM is created, the InstanceView property of the VM shows the details for the screenshot, and so on.</span></span> <span data-ttu-id="9dd63-367">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="9dd63-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="9dd63-368">Свойства виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9dd63-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-the-fault-domain-for-each-of-the-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="9dd63-369">Как получить сведения о свойствах каждой виртуальной машины, не выполняя несколько вызовов?</span><span class="sxs-lookup"><span data-stu-id="9dd63-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="9dd63-370">Например, как можно получить сведения о домене сбоя для каждой из 100 виртуальных машин в масштабируемом наборе?</span><span class="sxs-lookup"><span data-stu-id="9dd63-370">For example, how would I get the fault domain for each of the 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="9dd63-371">Чтобы получить сведения о свойствах каждой виртуальной машины, не выполняя несколько вызовов, вы можете вызвать `ListVMInstanceViews`, выполнив запрос REST API `GET` к следующему универсальному коду ресурса:</span><span class="sxs-lookup"><span data-stu-id="9dd63-371">To get property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on the following resource URI:</span></span>

<span data-ttu-id="9dd63-372">/subscriptions/<идентификатор_подписки>/resourceGroups/<имя_группы_ресурсов>/providers/Microsoft.Compute/virtualMachineScaleSets/<имя_масштабируемого_набора>/virtualMachines?$expand=instanceView&$select=instanceView.</span><span class="sxs-lookup"><span data-stu-id="9dd63-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-to-different-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="9dd63-373">Можно ли передать разные аргументы расширения на разные виртуальные машины в масштабируемом наборе?</span><span class="sxs-lookup"><span data-stu-id="9dd63-373">Can I pass different extension arguments to different VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="9dd63-374">Нет. Вы не можете передать разные аргументы расширения на разные виртуальные машины в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="9dd63-374">No, you cannot pass different extension arguments to different VMs in a virtual machine scale set.</span></span> <span data-ttu-id="9dd63-375">Но расширения могут действовать на основе уникальных свойств виртуальной машины, на которых они выполняются, таких как имя машины.</span><span class="sxs-lookup"><span data-stu-id="9dd63-375">However, extensions can act based on the unique properties of the VM they are running on, such as on the machine name.</span></span> <span data-ttu-id="9dd63-376">Кроме того, расширения могут запрашивать метаданные экземпляра на сайте http://169.254.169.254, чтобы получить дополнительные сведения о виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9dd63-376">Extensions also can query instance metadata on http://169.254.169.254 to get more information about the VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="9dd63-377">Почему между именами виртуальных машин в масштабируемом наборе и их идентификаторами существуют пропуски?</span><span class="sxs-lookup"><span data-stu-id="9dd63-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="9dd63-378">Например, 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="9dd63-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="9dd63-379">Пропуски между именами виртуальных машин в масштабируемом наборе и их идентификаторами возникают, потому что для свойства **overprovision** масштабируемого набора задано стандартное значение **true**.</span><span class="sxs-lookup"><span data-stu-id="9dd63-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set to the default value of **true**.</span></span> <span data-ttu-id="9dd63-380">Если значение избыточной подготовки — **true**, создается большее количество виртуальных машин, чем запрашивалось.</span><span class="sxs-lookup"><span data-stu-id="9dd63-380">If overprovisioning is set to **true**, more VMs than requested are created.</span></span> <span data-ttu-id="9dd63-381">Лишние виртуальные машины удаляются.</span><span class="sxs-lookup"><span data-stu-id="9dd63-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="9dd63-382">Это позволит повысить надежность развертывания, но повлияет на связанные правила преобразования сетевых адресов и именования.</span><span class="sxs-lookup"><span data-stu-id="9dd63-382">In this case, you gain increased deployment reliability, but at the expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="9dd63-383">Для этого свойства можно задать значение **false**.</span><span class="sxs-lookup"><span data-stu-id="9dd63-383">You can set this property to **false**.</span></span> <span data-ttu-id="9dd63-384">На надежность развертывания небольших масштабируемых наборов это не окажет значительного влияния.</span><span class="sxs-lookup"><span data-stu-id="9dd63-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-the-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-the-vm-when-should-i-choose-one-over-the-other"></a><span data-ttu-id="9dd63-385">Какова разница между удалением виртуальной машины в масштабируемом наборе и отменой ее подготовки?</span><span class="sxs-lookup"><span data-stu-id="9dd63-385">What is the difference between deleting a VM in a virtual machine scale set and deallocating the VM?</span></span> <span data-ttu-id="9dd63-386">Как понять, что выбрать в том или ином сценарии?</span><span class="sxs-lookup"><span data-stu-id="9dd63-386">When should I choose one over the other?</span></span>

<span data-ttu-id="9dd63-387">Основное различие между удалением виртуальной машины в масштабируемом наборе и отменой ее подготовки заключается в том, что при отмене подготовки (`deallocate`) не удаляются виртуальные жесткие диски.</span><span class="sxs-lookup"><span data-stu-id="9dd63-387">The main difference between deleting a VM in a virtual machine scale set and deallocating the VM is that `deallocate` doesn’t delete the virtual hard disks (VHDs).</span></span> <span data-ttu-id="9dd63-388">При выполнении команды `stop deallocate` взимается плата за хранение.</span><span class="sxs-lookup"><span data-stu-id="9dd63-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="9dd63-389">Причины выбора того или иного варианта заключаются в следующем:</span><span class="sxs-lookup"><span data-stu-id="9dd63-389">You might use one or the other for one of the following reasons:</span></span>

- <span data-ttu-id="9dd63-390">Вы хотите прекратить платить за вычислительные ресурсы, но сохранить состояние диска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9dd63-390">You want to stop paying compute costs, but you want to keep the disk state of the VMs.</span></span>
- <span data-ttu-id="9dd63-391">Вы хотите запустить набор виртуальных машин быстрее, чем при развертывании масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="9dd63-391">You want to start a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="9dd63-392">Вы создали собственную подсистему автомасштабирования и хотите быстрее выполнить сквозное масштабирование (касательно этого сценария).</span><span class="sxs-lookup"><span data-stu-id="9dd63-392">Related to this scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="9dd63-393">У вас есть масштабируемый набор, неравномерно распределенный между доменами сбоя и обновления.</span><span class="sxs-lookup"><span data-stu-id="9dd63-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="9dd63-394">Причиной этого может быть выборочное удаление или удаление после избыточной подготовки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9dd63-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="9dd63-395">Чтобы равномерно распределить виртуальные машины между доменами сбоя и обновления, выполните команду `stop deallocate`, а затем — `start`.</span><span class="sxs-lookup"><span data-stu-id="9dd63-395">Running `stop deallocate` followed by `start` on the virtual machine scale set evenly distributes the VMs across fault domains or update domains.</span></span>

