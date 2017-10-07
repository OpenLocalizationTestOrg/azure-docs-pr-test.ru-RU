---
title: "часто задаваемые вопросы о задает aaaAzure масштабирования виртуальных машин | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о наборы масштабирования виртуальных машин."
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
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="5a0df-103">Часто задаваемые вопросы о масштабируемых наборах виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="5a0df-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="5a0df-104">Ответы задает toofrequently вопросы и ответы о масштабирования виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0df-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="5a0df-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="5a0df-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="5a0df-106">Существуют ли рекомендации по автомасштабированию Azure?</span><span class="sxs-lookup"><span data-stu-id="5a0df-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="5a0df-107">Рекомендации по автомасштабированию виртуальных компонентов см. в [этой статье](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="5a0df-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="5a0df-108">Где можно найти имена метрик на основе узла, используемые в процессе автомасштабирования?</span><span class="sxs-lookup"><span data-stu-id="5a0df-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="5a0df-109">Имена метрик на основе узла, используемые в процессе автомасштабирования, перечислены в статье [Метрики, поддерживаемые Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="5a0df-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="5a0df-110">Существуют ли какие-либо образцы автомасштабирования на основе раздела или длины очереди служебной шины Azure?</span><span class="sxs-lookup"><span data-stu-id="5a0df-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="5a0df-111">Да.</span><span class="sxs-lookup"><span data-stu-id="5a0df-111">Yes.</span></span> <span data-ttu-id="5a0df-112">Образцы автомасштабирования на основе раздела или длины очереди служебной шины Azure см. в статье [Общие метрики автомасштабирования Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="5a0df-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="5a0df-113">Для очереди Service Bus используйте следующий JSON hello:</span><span class="sxs-lookup"><span data-stu-id="5a0df-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="5a0df-114">Для очереди службы хранилища используйте следующий JSON hello:</span><span class="sxs-lookup"><span data-stu-id="5a0df-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="5a0df-115">Замените примеры значений соответствующими универсальными кодами ресурсов (URI).</span><span class="sxs-lookup"><span data-stu-id="5a0df-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="5a0df-116">Следует ли выполнять автомасштабирование с использованием метрик на основе узла или с применением расширения диагностики?</span><span class="sxs-lookup"><span data-stu-id="5a0df-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="5a0df-117">Можно создать параметров автоматического масштабирования для метрик уровня узла виртуальных Машин toouse или гостевой ОС на базе метрики.</span><span class="sxs-lookup"><span data-stu-id="5a0df-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="5a0df-118">Список поддерживаемых метрик см. в статье [Общие метрики автомасштабирования Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="5a0df-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="5a0df-119">Полное определение конфигурации масштабируемых наборов см. в статье [Расширенная настройка автомасштабирования с помощью шаблонов Resource Manager для масштабируемых наборов виртуальных машин](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="5a0df-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="5a0df-120">Образец Hello использует метрики ЦП на уровне узла hello и метрики число сообщений.</span><span class="sxs-lookup"><span data-stu-id="5a0df-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="5a0df-121">Как можно задать правила оповещений в масштабируемом наборе виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="5a0df-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="5a0df-122">Оповещения на основе метрик в масштабируемых наборах виртуальных машин можно создать с помощью PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5a0df-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="5a0df-123">Дополнительные сведения см. в разделе [Создание правил генерации оповещений](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) и [Работа с оповещениями](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="5a0df-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="5a0df-124">Hello идентификатором TargetResourceId набора масштабирования виртуальной машины hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5a0df-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="5a0df-125">/subscriptions/идентификатор_подписки/resourceGroups/группа_ресурсов/providers/Microsoft.Compute/virtualMachineScaleSets/имя_набора.</span><span class="sxs-lookup"><span data-stu-id="5a0df-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="5a0df-126">Можно выбрать любого счетчика производительности виртуальной Машины как метрики tooset hello оповещение для.</span><span class="sxs-lookup"><span data-stu-id="5a0df-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="5a0df-127">Дополнительные сведения см. в разделе [показатели гостевой ОС для виртуальных машин на основе диспетчера ресурсов Windows](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) и [показатели гостевой ОС для ВМ Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) в hello [общих метрик автоматическое масштабирование Azure монитор](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)статьи.</span><span class="sxs-lookup"><span data-stu-id="5a0df-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="5a0df-128">Как можно задать параметры автомасштабирования в масштабируемом наборе виртуальных машин с помощью PowerShell?</span><span class="sxs-lookup"><span data-stu-id="5a0df-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="5a0df-129">tooset копирование автомасштабирования на значение с помощью PowerShell, масштабирования виртуальных машин см. hello блога [как задать tooan автомасштабирования tooadd масштабирования виртуальной машины Azure](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="5a0df-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="5a0df-130">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="5a0df-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="5a0df-131">Как безопасно выдать сертификат toohello виртуальной Машины?</span><span class="sxs-lookup"><span data-stu-id="5a0df-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="5a0df-132">Как подготовить toorun набор масштабирования виртуальной машины веб-сайт, где hello SSL для веб-сайта hello поставляется безопасно из конфигурации сертификата?</span><span class="sxs-lookup"><span data-stu-id="5a0df-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="5a0df-133">(hello распространенная операция смены сертификата может быть практически hello такой же, как операция обновления настройки.) У вас есть пример toodo это?</span><span class="sxs-lookup"><span data-stu-id="5a0df-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="5a0df-134">toosecurely отправить сертификат toohello виртуальной Машины, можно установить сертификат клиента непосредственно в хранилище сертификатов Windows из хранилища ключей hello клиента.</span><span class="sxs-lookup"><span data-stu-id="5a0df-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="5a0df-135">Используйте следующие JSON hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-135">Use hello following JSON:</span></span>

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

<span data-ttu-id="5a0df-136">Код Hello поддерживает Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="5a0df-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="5a0df-137">Дополнительные сведения см. в разделе о [создании и обновлении масштабируемого набора виртуальных машин](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a0df-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="5a0df-138">Пример самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="5a0df-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="5a0df-139">Создайте самозаверяющий сертификат в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="5a0df-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="5a0df-140">Используйте следующие команды PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="5a0df-141">Это команда дает hello входных данных для шаблона Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="5a0df-142">Пример toocreate самозаверяющий сертификат в хранилище ключей, в статье [сценарии безопасности кластера Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="5a0df-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="5a0df-143">Изменение шаблона диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="5a0df-144">Это свойство добавлено слишком**virtualMachineProfile**, как часть hello ресурса набора масштабирования виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="5a0df-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

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
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="5a0df-145">Можно указать toouse пару ключей SSH для проверки подлинности SSH с набор из шаблона диспетчера ресурсов масштабирования виртуальных машин Linux?</span><span class="sxs-lookup"><span data-stu-id="5a0df-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="5a0df-146">Да.</span><span class="sxs-lookup"><span data-stu-id="5a0df-146">Yes.</span></span> <span data-ttu-id="5a0df-147">Hello API-интерфейса REST для **osProfile** — примерно toohello Стандартная виртуальная машина API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="5a0df-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="5a0df-148">Включите раздел **osProfile** в свой шаблон:</span><span class="sxs-lookup"><span data-stu-id="5a0df-148">Include **osProfile** in your template:</span></span>

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
 
<span data-ttu-id="5a0df-149">Этот блок JSON используется в [GitHub краткого hello 101 ВМ ключа SSH шаблона](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="5a0df-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="5a0df-150">Hello профиль ОС также используется в [grelayhost.json hello GitHub быстрого запуска шаблона](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="5a0df-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="5a0df-151">Дополнительные сведения см. в разделе о [создании и обновлении масштабируемого набора виртуальных машин](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="5a0df-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="5a0df-152">Как удалить устаревшие сертификаты?</span><span class="sxs-lookup"><span data-stu-id="5a0df-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="5a0df-153">tooremove рекомендуется использовать сертификаты, hello удалить старый сертификат из списка сертификатов hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="5a0df-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="5a0df-154">Оставьте все сертификаты hello требуется tooremain на компьютере, в списке hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="5a0df-155">Этот сертификат не будет удален hello из всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a0df-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="5a0df-156">Он также добавляет сертификат hello toonew виртуальных машин, которые создаются в наборе масштабирования виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="5a0df-157">tooremove hello сертификат из существующих виртуальных машин, написать сценарий пользовательские расширения toomanually remove hello сертификаты из хранилища сертификатов.</span><span class="sxs-lookup"><span data-stu-id="5a0df-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="5a0df-158">Как вставить существующий открытый ключ SSH в hello виртуальной машины шкалы набор SSH слоя во время инициализации?</span><span class="sxs-lookup"><span data-stu-id="5a0df-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="5a0df-159">Я toostore hello SSH открытого ключа значений в хранилище ключей Azure и затем использовать их в шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a0df-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="5a0df-160">Если вы указываете hello виртуальные машины только с помощью открытого ключа SSH, нет необходимости tooput hello открытых ключей в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="5a0df-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="5a0df-161">Открытые ключи не являются секретом.</span><span class="sxs-lookup"><span data-stu-id="5a0df-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="5a0df-162">При создании виртуальной машины Linux открытые ключи SSH можно указать в обычном текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="5a0df-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

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
 
<span data-ttu-id="5a0df-163">Имя элемента конфигурации Linux</span><span class="sxs-lookup"><span data-stu-id="5a0df-163">linuxConfiguration element name</span></span> | <span data-ttu-id="5a0df-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5a0df-164">Required</span></span> | <span data-ttu-id="5a0df-165">Тип</span><span class="sxs-lookup"><span data-stu-id="5a0df-165">Type</span></span> | <span data-ttu-id="5a0df-166">Описание</span><span class="sxs-lookup"><span data-stu-id="5a0df-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="5a0df-167">ssh</span><span class="sxs-lookup"><span data-stu-id="5a0df-167">ssh</span></span> | <span data-ttu-id="5a0df-168">Нет</span><span class="sxs-lookup"><span data-stu-id="5a0df-168">No</span></span> | <span data-ttu-id="5a0df-169">Коллекция</span><span class="sxs-lookup"><span data-stu-id="5a0df-169">Collection</span></span> | <span data-ttu-id="5a0df-170">Указывает hello конфигурации ключа SSH для ОС Linux.</span><span class="sxs-lookup"><span data-stu-id="5a0df-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="5a0df-171">path</span><span class="sxs-lookup"><span data-stu-id="5a0df-171">path</span></span> | <span data-ttu-id="5a0df-172">Да</span><span class="sxs-lookup"><span data-stu-id="5a0df-172">Yes</span></span> | <span data-ttu-id="5a0df-173">Строка</span><span class="sxs-lookup"><span data-stu-id="5a0df-173">String</span></span> | <span data-ttu-id="5a0df-174">Указывает путь к файлу Linux hello где hello ключи SSH или сертификат должен быть расположен</span><span class="sxs-lookup"><span data-stu-id="5a0df-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="5a0df-175">keyData</span><span class="sxs-lookup"><span data-stu-id="5a0df-175">keyData</span></span> | <span data-ttu-id="5a0df-176">Да</span><span class="sxs-lookup"><span data-stu-id="5a0df-176">Yes</span></span> | <span data-ttu-id="5a0df-177">Строка</span><span class="sxs-lookup"><span data-stu-id="5a0df-177">String</span></span> | <span data-ttu-id="5a0df-178">Указывает открытый ключ SSH в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="5a0df-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="5a0df-179">Пример см. в разделе [GitHub краткого hello 101 ВМ ключа SSH шаблона](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="5a0df-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="5a0df-180">При запуске `Update-AzureRmVmss` после добавления более одного сертификата из hello ключ хранилища, я вижу hello следующего сообщения:</span><span class="sxs-lookup"><span data-stu-id="5a0df-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="5a0df-181">Update-AzureRmVmss: список секретов содержит повторяющиеся экземпляры /subscriptions/<идентификатор_моей_подписки>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, которые запрещены.</span><span class="sxs-lookup"><span data-stu-id="5a0df-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="5a0df-182">Это может произойти при попытке toore-добавить hello же хранилища вместо использования нового сертификата хранилища для существующей исходное хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="5a0df-183">Hello `Add-AzureRmVmssSecret` команда не работает правильно при добавлении дополнительных секретные данные.</span><span class="sxs-lookup"><span data-stu-id="5a0df-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="5a0df-184">tooadd дополнительные секретные данные из hello же хранилище ключей, список $vmss.properties.osProfile.secrets[0].vaultCertificates hello обновления.</span><span class="sxs-lookup"><span data-stu-id="5a0df-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="5a0df-185">Hello ожидалось входной структуре, см. в разделе [создания или обновления виртуальной машины установите](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a0df-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="5a0df-186">Найти секрет hello в объект набора масштабирования виртуальной машины hello в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="5a0df-187">Затем можно добавить список toohello Справочник (hello URL-адрес и имя секрета хранилища hello) сертификат, связанный с хранилищем hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="5a0df-188">В настоящее время невозможно удалить сертификаты из виртуальных машин с помощью API набор масштабирования виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="5a0df-189">Новые виртуальные машины не будет иметь Здравствуй, старый сертификат.</span><span class="sxs-lookup"><span data-stu-id="5a0df-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="5a0df-190">Однако виртуальные машины, имеют сертификат hello и который уже развернут будет Здравствуй, старый сертификат.</span><span class="sxs-lookup"><span data-stu-id="5a0df-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="5a0df-191">Можно передать набор без указания пароля hello, в том случае, когда сертификат hello в секретное хранилище hello масштабирования виртуальных машин toohello сертификаты?</span><span class="sxs-lookup"><span data-stu-id="5a0df-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="5a0df-192">Код toohard пароли в сценариях не обязательно.</span><span class="sxs-lookup"><span data-stu-id="5a0df-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="5a0df-193">Можно динамически получить пароли с разрешениями hello с помощью сценария развертывания toorun hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="5a0df-194">Если у вас есть скрипт, который перемещает сертификат из хранилища ключей секретное хранилище hello, hello секретное хранилище `get certificate` команда также выводит пароль hello hello PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="5a0df-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="5a0df-195">Как hello секреты свойство virtualMachineProfile.osProfile для масштабирования виртуальных машин задать работы?</span><span class="sxs-lookup"><span data-stu-id="5a0df-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="5a0df-196">Почему при работе с toospecify hello абсолютный URI на сертификат с помощью свойства certificateUrl hello должны hello sourceVault значение?</span><span class="sxs-lookup"><span data-stu-id="5a0df-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="5a0df-197">Ссылку на сертификат удаленного управления Windows (WinRM) должен присутствовать в hello секреты свойство hello профиль ОС.</span><span class="sxs-lookup"><span data-stu-id="5a0df-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="5a0df-198">Hello, указывающее, hello исходное хранилище предназначено политики управления доступом управления доступом tooenforce, имеющихся в модели пользователя облачной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0df-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="5a0df-199">Если не указана hello исходное хранилище, пользователей, которые не имеют разрешения доступа или toodeploy секреты tooa хранилище ключей будет может toothrough вычислений ресурсов поставщика (CRP).</span><span class="sxs-lookup"><span data-stu-id="5a0df-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="5a0df-200">Политики ACL применяются даже к еще не созданным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="5a0df-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="5a0df-201">Если указан неверный исходный идентификатор хранилища, но URL-адрес допустимого ключа хранилища, сообщение об ошибке при опросе hello операции.</span><span class="sxs-lookup"><span data-stu-id="5a0df-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="5a0df-202">Если добавить tooan секреты существующего набора масштабирования виртуальных машин, секреты hello вводится в существующих виртуальных машин или только на новые?</span><span class="sxs-lookup"><span data-stu-id="5a0df-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="5a0df-203">Сертификаты добавляются tooall виртуальные машины, даже те существующая.</span><span class="sxs-lookup"><span data-stu-id="5a0df-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="5a0df-204">Если ваш масштабирования виртуальной машины задано свойство upgradePolicy задано слишком**вручную**, hello добавления сертификата toohello виртуальной Машины при выполнении обновления вручную для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5a0df-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="5a0df-205">Куда следует поместить сертификаты виртуальных машин Linux?</span><span class="sxs-lookup"><span data-stu-id="5a0df-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="5a0df-206">как toodeploy для виртуальных машин Linux, см. toolearn [развертывание tooVMs сертификаты из хранилища ключей с управлением клиентом](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="5a0df-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="5a0df-207">Как добавить новые хранилища сертификатов tooa сертификат объекта?</span><span class="sxs-lookup"><span data-stu-id="5a0df-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="5a0df-208">tooadd хранилище секрета существующих сертификатов tooan, см. следующий пример PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="5a0df-209">Используйте только один объект секрета.</span><span class="sxs-lookup"><span data-stu-id="5a0df-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="5a0df-210">Что если toocertificates пересоздать виртуальной Машины?</span><span class="sxs-lookup"><span data-stu-id="5a0df-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="5a0df-211">После пересоздания образа виртуальной машины сертификаты удаляются.</span><span class="sxs-lookup"><span data-stu-id="5a0df-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="5a0df-212">Преобразует весь диск ОС удалений hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="5a0df-213">Что произойдет, если удалить сертификат из хранилища ключей hello?</span><span class="sxs-lookup"><span data-stu-id="5a0df-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="5a0df-214">Если секрет hello удаляется из хранилища ключей hello и затем запустить `stop deallocate` для всех виртуальных машин и затем запустите их снова, возникнет ошибка.</span><span class="sxs-lookup"><span data-stu-id="5a0df-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="5a0df-215">Hello произошел сбой, так как hello CRP необходим tooretrieve hello секретов из хранилища ключей hello, но он не может.</span><span class="sxs-lookup"><span data-stu-id="5a0df-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="5a0df-216">В этом случае можно удалить из модели набора масштабирования виртуальной машины hello hello сертификаты.</span><span class="sxs-lookup"><span data-stu-id="5a0df-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="5a0df-217">компонент CRP Hello не сохраняет секреты клиента.</span><span class="sxs-lookup"><span data-stu-id="5a0df-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="5a0df-218">При запуске `stop deallocate` для всех виртуальных машин в наборе масштабирования виртуальных машин hello hello кэш удаляется.</span><span class="sxs-lookup"><span data-stu-id="5a0df-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="5a0df-219">В этом сценарии секретные данные извлекаются из хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="5a0df-220">Эта проблема не встречаются при горизонтальное масштабирование, так как отсутствует кэшированная копия секрета hello в Azure Service Fabric (в модели структуры одного клиента hello).</span><span class="sxs-lookup"><span data-stu-id="5a0df-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="5a0df-221">Почему у toospecify hello точное расположение URL-адрес сертификата hello (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), как указано в [сценарии безопасности кластера Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="5a0df-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="5a0df-222">Документация по хранилищу ключей Azure Hello состояний, получить секрет API-интерфейса REST должен возвращать hello последнюю версию секрета hello, если не указана версия hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="5a0df-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="5a0df-223">Метод</span><span class="sxs-lookup"><span data-stu-id="5a0df-223">Method</span></span> | <span data-ttu-id="5a0df-224">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="5a0df-224">URL</span></span>
--- | ---
<span data-ttu-id="5a0df-225">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="5a0df-225">GET</span></span> | <span data-ttu-id="5a0df-226">https://mykeyvault.vault.azure.net/secrets/{имя_секрета}/{версия_секрета}?api-version={версия_API}</span><span class="sxs-lookup"><span data-stu-id="5a0df-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="5a0df-227">Замените {*имя секрета*} с именем hello и замените {*версии секрета*} с версией hello секрет hello требуется tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="5a0df-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="5a0df-228">может быть исключено Hello версию секрета.</span><span class="sxs-lookup"><span data-stu-id="5a0df-228">hello secret version might be excluded.</span></span> <span data-ttu-id="5a0df-229">В этом случае будет получена текущая версия hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="5a0df-230">Почему у toospecify hello сертификата версии при использовании хранилища ключей?</span><span class="sxs-lookup"><span data-stu-id="5a0df-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="5a0df-231">Hello hello версии хранилища ключей требование toospecify hello сертификат предназначен toomake снимите toohello пользователя какие сертификат развертывается на их виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="5a0df-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="5a0df-232">При создании виртуальной Машины и обновите ваш секрет в хранилище ключей hello, новый сертификат hello не загруженные tooyour виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a0df-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="5a0df-233">Но tooreference и новые виртуальные машины могут получать новый секрет hello отображаются виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="5a0df-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="5a0df-234">tooavoid, являются обязательным tooreference версию секрета.</span><span class="sxs-lookup"><span data-stu-id="5a0df-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="5a0df-235">Моя группа работает с несколькими сертификаты, распространяемые toous как открытые ключи CER-файл.</span><span class="sxs-lookup"><span data-stu-id="5a0df-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="5a0df-236">Что такое рекомендованный подход для развертывания этих сертификатов набора масштабирования виртуальных машин tooa hello</span><span class="sxs-lookup"><span data-stu-id="5a0df-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="5a0df-237">toodeploy .cer открытые ключи tooa масштабный набор виртуальных машин, можно создать в PFX-файл, который содержит только файлы CER-файл.</span><span class="sxs-lookup"><span data-stu-id="5a0df-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="5a0df-238">toodo это, используйте `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="5a0df-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="5a0df-239">Например загрузить hello CER-файл как объект x509Certificate2 в C# или PowerShell, а затем вызывайте метод hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="5a0df-240">Дополнительные сведения о методе X509Certificate.Export см. в [этой статье](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="5a0df-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="5a0df-241">Отсутствует параметр для toopass пользователей в сертификатах как строки в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="5a0df-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="5a0df-242">Большинство других поставщиков ресурсов предоставляют этот параметр.</span><span class="sxs-lookup"><span data-stu-id="5a0df-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="5a0df-243">tooemulate, передавая сертификата в виде строки base64, можно извлечь hello последние версии URL-адрес в шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a0df-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="5a0df-244">Следующие hello следующие свойства JSON в шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a0df-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="5a0df-245">Имеются ли в объектах JSON в хранилищах ключей toowrap сертификаты?</span><span class="sxs-lookup"><span data-stu-id="5a0df-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="5a0df-246">В масштабируемых наборах и на виртуальных машинах сертификаты нужно помещать в объекты JSON.</span><span class="sxs-lookup"><span data-stu-id="5a0df-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="5a0df-247">Кроме того, поддерживается тип содержимого hello приложения/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="5a0df-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="5a0df-248">Инструкции по использованию application/x-pkcs12 см. в записи блога об [использовании PFX-сертификатов в Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="5a0df-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="5a0df-249">Сейчас мы не поддерживаем CER-файлы.</span><span class="sxs-lookup"><span data-stu-id="5a0df-249">We currently do not support .cer files.</span></span> <span data-ttu-id="5a0df-250">toouse CER-файлами, экспортировать их в контейнеры PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="5a0df-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="5a0df-251">Соответствие нормативным требованиям</span><span class="sxs-lookup"><span data-stu-id="5a0df-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="5a0df-252">Соответствуют ли масштабируемые наборы виртуальных машин требованиям стандарта PCI?</span><span class="sxs-lookup"><span data-stu-id="5a0df-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="5a0df-253">Наборы масштабирования виртуальной машины — это тонкий слой API на основе hello CRP.</span><span class="sxs-lookup"><span data-stu-id="5a0df-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="5a0df-254">Оба компонента являются частью платформы вычислений hello в hello Azure дерева служб.</span><span class="sxs-lookup"><span data-stu-id="5a0df-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="5a0df-255">С точки зрения соответствия наборы масштабирования виртуальных машин являются основной частью платформы hello вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0df-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="5a0df-256">Они совместно используют команды, средства, процессы, методологии развертывания, управления безопасностью, just-in-time (JIT) компиляции, мониторинга, предупреждений и т. д с CRP hello сам.</span><span class="sxs-lookup"><span data-stu-id="5a0df-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="5a0df-257">Наборы масштабирования виртуальных машин, индустрии платежных карт (PCI)-совместимые, так как hello CRP является частью текущего PCI данных безопасности стандартной (DSS) аттестации hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="5a0df-258">Дополнительные сведения см. в разделе [hello Центр управления безопасностью Microsoft](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="5a0df-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="5a0df-259">расширения.</span><span class="sxs-lookup"><span data-stu-id="5a0df-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="5a0df-260">Как удалить расширение масштабируемого набора виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="5a0df-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="5a0df-261">toodelete масштабирования виртуальных машин установите расширение hello используйте следующий пример PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5a0df-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="5a0df-262">Можно найти значение extensionName hello в `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="5a0df-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="5a0df-263">Существует ли пример шаблона масштабируемого набора виртуальных машин, который интегрируется с Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="5a0df-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="5a0df-264">Для примера шаблона, которое интегрируется с Operations Management Suite набора масштабирования виртуальных машин, см. во втором примере hello в [развертывание кластера Azure Service Fabric и включите наблюдение с помощью аналитики журналов](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="5a0df-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="5a0df-265">Расширения кажутся toorun параллельно на наборы масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a0df-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="5a0df-266">В этом случае Мой toofail расширение пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="5a0df-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="5a0df-267">Что можно делать toofix это?</span><span class="sxs-lookup"><span data-stu-id="5a0df-267">What can I do toofix this?</span></span>

<span data-ttu-id="5a0df-268">toolearn о виртуализации расширения в наборы масштабирования виртуальных машин, в разделе [расширения виртуализации в наборы масштабирования виртуальной машины Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="5a0df-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="5a0df-269">Как сбросить пароль hello для виртуальных машин в моей масштабный набор виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="5a0df-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="5a0df-270">пароль hello tooreset для виртуальных машин в вашей масштабирования виртуальных машин необходимо задать, использовать расширения access ВМ.</span><span class="sxs-lookup"><span data-stu-id="5a0df-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="5a0df-271">Используйте следующий пример PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-271">Use hello following PowerShell example:</span></span>

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
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="5a0df-272">Как добавить расширение tooall виртуальных машин в моей масштабный набор виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="5a0df-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="5a0df-273">Если политика обновления задано слишком**автоматического**, повторного развертывания шаблона hello с новыми свойствами расширения hello обновляет все виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="5a0df-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="5a0df-274">Если политика обновления задано слишком**вручную**, сначала обновить расширение hello и вручную обновить все экземпляры в виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="5a0df-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="5a0df-275">Если обновляются hello расширения, связанные с существующего набора масштабирования виртуальной машины, существующие виртуальные машины в затронутых?</span><span class="sxs-lookup"><span data-stu-id="5a0df-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="5a0df-276">(То есть виртуальные машины будут hello *не* модели набора масштабирования виртуальной машины hello соответствия?) Или они игнорируются?</span><span class="sxs-lookup"><span data-stu-id="5a0df-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="5a0df-277">Когда существующей машины восстанавливаются службы, или повторного создания образа, hello скрипты, которые в настоящий момент на выполнении набора масштабирования виртуальных машин hello или являются hello скрипты, которые были настроены при использовании hello создания виртуальной Машины?</span><span class="sxs-lookup"><span data-stu-id="5a0df-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="5a0df-278">Если определение расширения hello в масштабирования виртуальных машин hello обновить модель и hello upgradePolicy задано слишком**автоматического**, он обновляет виртуальные машины hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="5a0df-279">Если свойство upgradePolicy hello задано слишком**вручную**, расширения, помечаются как не соответствует модели hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="5a0df-280">Если существующей виртуальной Машины восстанавливаются службы, он отображается как перезагрузка и расширения hello не выполняют повторный запуск.</span><span class="sxs-lookup"><span data-stu-id="5a0df-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="5a0df-281">При его повторном создании это как замены диска ОС hello hello исходного образа.</span><span class="sxs-lookup"><span data-stu-id="5a0df-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="5a0df-282">Все специализации из последней модели hello, такие как расширения, выполняются.</span><span class="sxs-lookup"><span data-stu-id="5a0df-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="5a0df-283">Как присоединить к домену tooan Azure AD набор масштабирования виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="5a0df-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="5a0df-284">toojoin домена Azure Active Directory (Azure AD) tooan набор масштабирования виртуальной машины, можно определить расширение.</span><span class="sxs-lookup"><span data-stu-id="5a0df-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="5a0df-285">toodefine расширения, используйте свойство JsonADDomainExtension hello:</span><span class="sxs-lookup"><span data-stu-id="5a0df-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="5a0df-286">Расширения набора масштабирования виртуальной машины пытается tooinstall то, что требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="5a0df-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="5a0df-287">Например, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools".</span><span class="sxs-lookup"><span data-stu-id="5a0df-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="5a0df-288">Если расширения набора масштабирования виртуальной машины пытается tooinstall то, что требует перезагрузки, можно использовать расширение hello Azure автоматизации настройки требуемого состояния (DSC службы автоматизации).</span><span class="sxs-lookup"><span data-stu-id="5a0df-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="5a0df-289">Если hello операционная система Windows Server 2012 R2, Azure запрашивает в программе установки Windows Management Framework (WMF) 5.0 hello, перезагрузки, а затем продолжает hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5a0df-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="5a0df-290">Как включить антивредоносную программу в масштабируемом наборе виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="5a0df-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="5a0df-291">tooturn для защиты от вредоносных программ на шкале виртуальной машине установлена, следует использовать hello следующий пример PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5a0df-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="5a0df-292">Мне нужна tooexecute пользовательского скрипта, который размещен в личной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5a0df-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="5a0df-293">Hello скрипт успешно запускается, если открытый hello хранилища, но при попытке toouse подпись общего доступа (SAS), происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="5a0df-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="5a0df-294">и отображается следующее сообщение об ошибке: "Отсутствуют обязательные параметры для допустимой подписи коллективного доступа".</span><span class="sxs-lookup"><span data-stu-id="5a0df-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="5a0df-295">В локальном браузере проблемы с подписанным URL-адресом и ссылкой не возникали.</span><span class="sxs-lookup"><span data-stu-id="5a0df-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="5a0df-296">tooexecute пользовательского скрипта, который размещен в личной учетной записи хранения, задать параметры защищенного hello ключ учетной записи хранилища и имя.</span><span class="sxs-lookup"><span data-stu-id="5a0df-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="5a0df-297">Дополнительные сведения см. в статье [Расширение Custom Script в ОС Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="5a0df-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="5a0df-298">Сеть</span><span class="sxs-lookup"><span data-stu-id="5a0df-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="5a0df-299">Это возможно tooassign задать шкалу tooa группы безопасности сети (NSG), таким образом, он будет применить hello tooall сетевых адаптеров виртуальной Машины в наборе hello?</span><span class="sxs-lookup"><span data-stu-id="5a0df-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="5a0df-300">Да.</span><span class="sxs-lookup"><span data-stu-id="5a0df-300">Yes.</span></span> <span data-ttu-id="5a0df-301">Группы безопасности сети можно применять непосредственно задать масштаб tooa обратившись в разделе интерфейса hello hello сетевых профилей.</span><span class="sxs-lookup"><span data-stu-id="5a0df-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="5a0df-302">Пример:</span><span class="sxs-lookup"><span data-stu-id="5a0df-302">Example:</span></span>

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

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="5a0df-303">Как это сделать Операцию переключения наборы масштабирования виртуальных машин в hello же подписке и одном регионе?</span><span class="sxs-lookup"><span data-stu-id="5a0df-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="5a0df-304">При наличии двух виртуальных масштабирования машины задает с интерфейсных подсистемы балансировки нагрузки Azure, и они находятся в hello ту же подписку и регион, можно освободить hello общих IP-адресов из каждого из них и назначить toohello других.</span><span class="sxs-lookup"><span data-stu-id="5a0df-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="5a0df-305">Пример приведен в статье [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Переключение виртуальных IP-адресов: развертывание по схеме "blue-green" в Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="5a0df-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="5a0df-306">Это подразумевает задержку на то, что как hello ресурсы освобождены выделенной на уровне сети hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="5a0df-307">Более быстрый параметр — toouse шлюза приложения Azure с двумя внутренние пулы и правила маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="5a0df-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="5a0df-308">Также можно разместить приложение в [службе приложений Azure](https://azure.microsoft.com/en-us/services/app-service/), которая обеспечивает быстрое переключение между промежуточными и рабочими слотами.</span><span class="sxs-lookup"><span data-stu-id="5a0df-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="5a0df-309">Как указать диапазон частных toouse IP адресов для статического выделения частных IP-адресов?</span><span class="sxs-lookup"><span data-stu-id="5a0df-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="5a0df-310">IP-адреса выбираются из указанной подсети.</span><span class="sxs-lookup"><span data-stu-id="5a0df-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="5a0df-311">метод распределения Hello IP-адресов, набор масштабирования виртуальной машины всегда «динамических», но это не значит, что можно изменить эти IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="5a0df-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="5a0df-312">В этом случае «динамических» означает только что hello IP-адрес не указан в запросе PUT.</span><span class="sxs-lookup"><span data-stu-id="5a0df-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="5a0df-313">Укажите статический hello устанавливается с помощью подсети hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="5a0df-314">Развертывание виртуальной машины шкалы набор tooan существующей виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="5a0df-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="5a0df-315">toodeploy масштабирования виртуальных машин задайте tooan существующей виртуальной сети Azure см. в разделе [развертывание виртуальной машины шкалы набор tooan существующей виртуальной сети](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="5a0df-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="5a0df-316">Как добавить IP-адрес hello hello первая виртуальная машина в масштабирования виртуальных машин установите toohello выходные данные шаблона?</span><span class="sxs-lookup"><span data-stu-id="5a0df-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="5a0df-317">первая виртуальная машина в виртуальной машине шкалы набор toohello выходных данных шаблона, в разделе tooadd hello IP-адрес hello [ARM: получение VMSS частных IP-адресов](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="5a0df-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="5a0df-318">Можно ли использовать масштабируемые наборы с ускоренной сетью?</span><span class="sxs-lookup"><span data-stu-id="5a0df-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="5a0df-319">Да.</span><span class="sxs-lookup"><span data-stu-id="5a0df-319">Yes.</span></span> <span data-ttu-id="5a0df-320">toouse accelerated сети, задать enableAcceleratedNetworking tootrue в шкалу набора конфигураций сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5a0df-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="5a0df-321">Например: </span><span class="sxs-lookup"><span data-stu-id="5a0df-321">E.g.</span></span>
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

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="5a0df-322">Как настроить hello DNS-серверы, используемые набором масштабирования</span><span class="sxs-lookup"><span data-stu-id="5a0df-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="5a0df-323">toocreate набора масштабирования виртуальных Машин с пользовательской конфигурацией DNS, добавить шкалу dnsSettings пакета JSON toohello задать раздел конфигураций сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5a0df-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="5a0df-324">Пример:</span><span class="sxs-lookup"><span data-stu-id="5a0df-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="5a0df-325">Как настроить tooassign набор масштабирования открытый IP адрес tooeach виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5a0df-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="5a0df-326">toocreate набор масштабирования виртуальных Машин, назначается открытый IP адрес tooeach виртуальной Машины, убедитесь, что версия hello API hello Microsoft.Compute/virtualMAchineScaleSets ресурсов 2017 г., 03, 30 и добавить _publicipaddressconfiguration_ пакетов JSON задать масштаб toohello раздел IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5a0df-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="5a0df-327">Пример:</span><span class="sxs-lookup"><span data-stu-id="5a0df-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="5a0df-328">Можно настроить набор масштабирования toowork с несколькими шлюзы приложений</span><span class="sxs-lookup"><span data-stu-id="5a0df-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="5a0df-329">Да.</span><span class="sxs-lookup"><span data-stu-id="5a0df-329">Yes.</span></span> <span data-ttu-id="5a0df-330">Можно добавить hello ресурсов идентификаторы для нескольких пулов toohello адрес шлюза приложений серверной _applicationGatewayBackendAddressPools_ списка в hello _IP-конфигураций_ раздел набора масштабирования сетевой профиль.</span><span class="sxs-lookup"><span data-stu-id="5a0df-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="5a0df-331">Масштаб</span><span class="sxs-lookup"><span data-stu-id="5a0df-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="5a0df-332">В каких случаях следует создавать масштабируемый набор с одной виртуальной машиной или без них?</span><span class="sxs-lookup"><span data-stu-id="5a0df-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="5a0df-333">Одна из причин toocreate набора масштабирования виртуальных машин с менее двух виртуальных машин будет иметь значение toouse hello эластичной параметров масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a0df-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="5a0df-334">Например можно развернуть набор масштабирования виртуальной машины с нуля toodefine виртуальных машин инфраструктуры без оплаты виртуальной Машине под управлением затрат.</span><span class="sxs-lookup"><span data-stu-id="5a0df-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="5a0df-335">Затем когда вы будете готовы toodeploy виртуальных машин, увеличьте hello «емкость» hello набор масштабирования виртуальной машины toohello число экземпляров рабочей.</span><span class="sxs-lookup"><span data-stu-id="5a0df-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="5a0df-336">Вторая причина заключается в том, что в масштабируемом наборе выполняются операции, не учитывающие доступность в таком же смысле, что и группы доступности с отдельными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="5a0df-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="5a0df-337">Наборы масштабирования виртуальной машины предоставляют способ toowork с форматными вычислительных единиц, которые взаимозаменяемые.</span><span class="sxs-lookup"><span data-stu-id="5a0df-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="5a0df-338">Это единообразие является ключевым преимуществом при выборе между масштабируемыми наборами виртуальных машин и группами доступности.</span><span class="sxs-lookup"><span data-stu-id="5a0df-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="5a0df-339">Многие рабочие нагрузки без отслеживания состояния не учитывают отдельные единицы.</span><span class="sxs-lookup"><span data-stu-id="5a0df-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="5a0df-340">Удаляет hello рабочей нагрузки, можно масштабировать tooone единица измерения вычислений и затем масштабировать toomany при увеличении рабочей нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="5a0df-341">Как изменить hello число виртуальных машин в наборе масштабирования виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="5a0df-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="5a0df-342">toochange hello число виртуальных машин в наборе масштабирования виртуальных машин в разделе [изменить количество экземпляров hello набора масштабирования виртуальных машин](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="5a0df-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="5a0df-343">Как настроить пользовательские оповещения, отображающиеся при достижении определенных пороговых значений?</span><span class="sxs-lookup"><span data-stu-id="5a0df-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="5a0df-344">Обработкой оповещений при достижении определенных пороговых значений можно управлять несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="5a0df-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="5a0df-345">Например, вы можете определить настраиваемые объекты webhook.</span><span class="sxs-lookup"><span data-stu-id="5a0df-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="5a0df-346">Следующий пример веб-перехватчика Hello взят из шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a0df-346">hello following webhook example is from a Resource Manager template:</span></span>

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

<span data-ttu-id="5a0df-347">В этом примере оповещение становится tooPagerduty.com при достижении порогового значения.</span><span class="sxs-lookup"><span data-stu-id="5a0df-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="5a0df-348">Установка исправлений и эксплуатация</span><span class="sxs-lookup"><span data-stu-id="5a0df-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="5a0df-349">Как создать масштабируемый набор в существующей группе ресурсов?</span><span class="sxs-lookup"><span data-stu-id="5a0df-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="5a0df-350">Создание набора масштабирования в существующий ресурс группы еще невозможно из hello портал Azure, но при развертывании шкалу на основе шаблона диспетчера ресурсов Azure можно указать существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a0df-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="5a0df-351">Можно также указать существующую группу ресурсов при создании масштабируемого набора с помощью Azure PowerShell или интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="5a0df-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="5a0df-352">Мы можно переместить группы ресурсов tooanother набора масштабирования?</span><span class="sxs-lookup"><span data-stu-id="5a0df-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="5a0df-353">Да, можно переместить шкалы набор ресурсов tooa новую подписку или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a0df-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="5a0df-354">Обновления tooI Мой масштабирования виртуальных машин установлены tooa новый образ?</span><span class="sxs-lookup"><span data-stu-id="5a0df-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="5a0df-355">и как управлять установкой исправлений?</span><span class="sxs-lookup"><span data-stu-id="5a0df-355">How do I manage patching?</span></span>

<span data-ttu-id="5a0df-356">tooupdate вашей виртуальной машины в наборе tooa нового образа и toomanage исправлений, в разделе [обновление набора масштабирования виртуальных машин](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="5a0df-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="5a0df-357">Можно использовать tooreset операции hello повторное создание образа виртуальной Машины без изменения образа hello</span><span class="sxs-lookup"><span data-stu-id="5a0df-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="5a0df-358">(То есть, требуется сбросить параметры виртуальной Машины toofactory вместо tooa нового изображения.)</span><span class="sxs-lookup"><span data-stu-id="5a0df-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="5a0df-359">Да, можно использовать tooreset операции hello повторное создание образа виртуальной Машины без изменения образа hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="5a0df-360">Тем не менее, если задать масштаб вашей виртуальной машины ссылается на образ платформы с `version = latest`, ВМ можно обновить tooa образа ОС более поздней версии при вызове `reimage`.</span><span class="sxs-lookup"><span data-stu-id="5a0df-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="5a0df-361">Дополнительные сведения см. в статье об [управлении всеми виртуальными машинами в масштабируемом наборе](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="5a0df-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="5a0df-362">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="5a0df-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="5a0df-363">Как включить диагностику загрузки?</span><span class="sxs-lookup"><span data-stu-id="5a0df-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="5a0df-364">tooturn на Диагностика загрузки, во-первых, создайте учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="5a0df-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="5a0df-365">Затем поместите этот блок JSON в наборе масштабирования виртуальных машин **virtualMachineProfile**и обновить набор масштабирования виртуальной машины hello:</span><span class="sxs-lookup"><span data-stu-id="5a0df-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="5a0df-366">При создании новой виртуальной Машины hello свойство InstanceView hello виртуальных Машин показывает данные hello для экрана приветствия и т. д.</span><span class="sxs-lookup"><span data-stu-id="5a0df-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="5a0df-367">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="5a0df-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="5a0df-368">Свойства виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5a0df-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="5a0df-369">Как получить сведения о свойствах каждой виртуальной машины, не выполняя несколько вызовов?</span><span class="sxs-lookup"><span data-stu-id="5a0df-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="5a0df-370">Например как бы заставить домен сбоя hello для каждого hello 100 виртуальных машин в моей масштабный набор виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="5a0df-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="5a0df-371">сведения о свойстве tooget для каждой виртуальной Машины без несколько вызовов, можно вызвать `ListVMInstanceViews` , выполнив REST API `GET` на hello, следуя ресурса (URI):</span><span class="sxs-lookup"><span data-stu-id="5a0df-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="5a0df-372">/subscriptions/<идентификатор_подписки>/resourceGroups/<имя_группы_ресурсов>/providers/Microsoft.Compute/virtualMachineScaleSets/<имя_масштабируемого_набора>/virtualMachines?$expand=instanceView&$select=instanceView.</span><span class="sxs-lookup"><span data-stu-id="5a0df-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="5a0df-373">Можно передавать аргументы другое расширение toodifferent виртуальные машины в наборе масштабирования виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="5a0df-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="5a0df-374">Нет, нельзя передавать аргументы другое расширение toodifferent виртуальные машины набора масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a0df-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="5a0df-375">Тем не менее расширения может действовать на основе уникальных свойств hello hello ВМ работают для, такого как имя машины hello.</span><span class="sxs-lookup"><span data-stu-id="5a0df-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="5a0df-376">Расширения также можно запрашивать метаданные экземпляра на http://169.254.169.254 tooget Дополнительные сведения о hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5a0df-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="5a0df-377">Почему между именами виртуальных машин в масштабируемом наборе и их идентификаторами существуют пропуски?</span><span class="sxs-lookup"><span data-stu-id="5a0df-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="5a0df-378">Например, 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="5a0df-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="5a0df-379">Существуют пропуски между ВМ идентификаторы и имена компьютеров виртуальной Машины набора масштабирования виртуальной машины, поскольку вашей виртуальной машины в наборе **избыточной подготовки** задано значение по умолчанию toohello **true**.</span><span class="sxs-lookup"><span data-stu-id="5a0df-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="5a0df-380">Если избыток задано слишком**true**, больше виртуальных машин, чем запрошено создаются.</span><span class="sxs-lookup"><span data-stu-id="5a0df-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="5a0df-381">Лишние виртуальные машины удаляются.</span><span class="sxs-lookup"><span data-stu-id="5a0df-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="5a0df-382">В этом случае получить развертывания повысить надежность, но за счет hello смежных именования и смежных сетевых адресов (NAT) правила.</span><span class="sxs-lookup"><span data-stu-id="5a0df-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="5a0df-383">Это свойство можно задать слишком**false**.</span><span class="sxs-lookup"><span data-stu-id="5a0df-383">You can set this property too**false**.</span></span> <span data-ttu-id="5a0df-384">На надежность развертывания небольших масштабируемых наборов это не окажет значительного влияния.</span><span class="sxs-lookup"><span data-stu-id="5a0df-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="5a0df-385">Что такое hello различие между удалением виртуальной Машины в наборе масштабирования виртуальных машин и освобождение hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5a0df-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="5a0df-386">Когда один над другим hello выбрать?</span><span class="sxs-lookup"><span data-stu-id="5a0df-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="5a0df-387">Hello основное различие между удалением виртуальной Машины в наборе масштабирования виртуальных машин и освобождение hello виртуальной Машины, звучит `deallocate` не приводит к удалению hello виртуальные жесткие диски (VHD).</span><span class="sxs-lookup"><span data-stu-id="5a0df-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="5a0df-388">При выполнении команды `stop deallocate` взимается плата за хранение.</span><span class="sxs-lookup"><span data-stu-id="5a0df-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="5a0df-389">Может использовать один или другой — для одного из следующих причин hello hello:</span><span class="sxs-lookup"><span data-stu-id="5a0df-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="5a0df-390">Требуется toostop дополнительные затраты на вычислений, но желательно состояние диска hello tookeep hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a0df-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="5a0df-391">Вы хотите toostart набор виртуальных машин гораздо быстрее, чем можно развернуть масштаб набора масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a0df-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="5a0df-392">Связанные toothis сценарий, вы могли создать собственный механизм автоматического масштабирования и хотите быстрее шкалы начала до конца.</span><span class="sxs-lookup"><span data-stu-id="5a0df-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="5a0df-393">У вас есть масштабируемый набор, неравномерно распределенный между доменами сбоя и обновления.</span><span class="sxs-lookup"><span data-stu-id="5a0df-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="5a0df-394">Причиной этого может быть выборочное удаление или удаление после избыточной подготовки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a0df-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="5a0df-395">Под управлением `stop deallocate` следуют `start` на виртуальной машине hello равномерно наборе масштабирования распределяет виртуальные машины hello домены сбоя и доменах обновления.</span><span class="sxs-lookup"><span data-stu-id="5a0df-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

