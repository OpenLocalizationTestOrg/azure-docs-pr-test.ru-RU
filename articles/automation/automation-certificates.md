---
title: "Ресурсы-контейнеры сертификатов в службе автоматизации Azure | Документация Майкрософт"
description: "Сертификаты можно безопасно сохранить в службе автоматизации Azure, чтобы к ним могли обращаться модули Runbook или конфигурации DSC для прохождения аутентификации при доступе к ресурсам Azure и сторонних производителей.  В этой статье подробно рассматриваются сертификаты и работа с ними при создании текстовых и графических модулей."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="5a62a-104">Сертификация активов в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5a62a-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="5a62a-105">Сертификаты можно безопасно сохранить в службе автоматизации Azure, чтобы к ним могли обращаться модули Runbook или конфигурации DSC с помощью действия **Get-AzureRmAutomationRmCertificate** для ресурсов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5a62a-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="5a62a-106">Это позволяет создавать модули Runbook и конфигурации DSC, которые используют сертификаты для проверки подлинности или добавляют их в ресурсы Azure либо сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="5a62a-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="5a62a-107">Безопасные средства в службе автоматизации Azure включают учетные данные, сертификаты, подключения и зашифрованные переменные.</span><span class="sxs-lookup"><span data-stu-id="5a62a-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="5a62a-108">Эти ресурсы шифруются и хранятся в службе автоматизации Azure с помощью уникального ключа, который создается для каждой учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5a62a-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="5a62a-109">Ключ шифруется главным сертификатом и хранится в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5a62a-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="5a62a-110">Перед сохранением защищенного ресурса ключ учетной записи службы автоматизации дешифруется с помощью главного сертификата и используется для шифрования ресурса.</span><span class="sxs-lookup"><span data-stu-id="5a62a-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="5a62a-111">Командлеты Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a62a-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="5a62a-112">Командлеты, представленные в следующей таблице, используются для создания ресурсов сертификата службы автоматизации и управления ими с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a62a-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="5a62a-113">Они входят в состав [модуля Azure PowerShell](../powershell-install-configure.md) , доступного в модулях Runbook и конфигурациях DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5a62a-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="5a62a-114">Командлеты</span><span class="sxs-lookup"><span data-stu-id="5a62a-114">Cmdlets</span></span>|<span data-ttu-id="5a62a-115">Описание</span><span class="sxs-lookup"><span data-stu-id="5a62a-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="5a62a-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="5a62a-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="5a62a-117">Извлекает сведения о сертификате для использования в модуле Runbook или в конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="5a62a-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="5a62a-118">Сам сертификат можно извлечь только с помощью действия Get-AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="5a62a-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="5a62a-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="5a62a-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="5a62a-120">Создает сертификат в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5a62a-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="5a62a-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="5a62a-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="5a62a-122">Удаляет сертификат из службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5a62a-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="5a62a-123">Создает сертификат в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5a62a-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="5a62a-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="5a62a-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="5a62a-125">Задает свойства для существующего сертификата, включая отправку файла сертификата и задание пароля для PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="5a62a-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="5a62a-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="5a62a-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="5a62a-127">Отправляет сертификат службы в заданную облачную службу.</span><span class="sxs-lookup"><span data-stu-id="5a62a-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="5a62a-128">Создание нового сертификата</span><span class="sxs-lookup"><span data-stu-id="5a62a-128">Creating a new certificate</span></span>

<span data-ttu-id="5a62a-129">При создании нового сертификата в службу автоматизации Azure передается CER- или PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="5a62a-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="5a62a-130">Если пометить сертификат как экспортируемый, его можно будет переместить из хранилища сертификатов службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5a62a-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="5a62a-131">Если он не экспортируемый, то он будет использоваться только для подписи в модуле Runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="5a62a-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="5a62a-132">Создание нового сертификата на портале Azure</span><span class="sxs-lookup"><span data-stu-id="5a62a-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="5a62a-133">В учетной записи службы автоматизации щелкните плитку **Ресурсы**, чтобы открыть колонку **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="5a62a-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="5a62a-134">Щелкните плитку **Сертификаты**, чтобы открыть колонку **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="5a62a-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="5a62a-135">Щелкните **Добавить сертификат** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="5a62a-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="5a62a-136">Введите имя сертификата в поле **Имя** .</span><span class="sxs-lookup"><span data-stu-id="5a62a-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="5a62a-137">Щелкните **Выбрать файл** в разделе **Отправка файла сертификата** и перейдите к CER- или PFX-файлу.</span><span class="sxs-lookup"><span data-stu-id="5a62a-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="5a62a-138">Если выбран PFX-файл, введите пароль и укажите, разрешен ли экспорт сертификата.</span><span class="sxs-lookup"><span data-stu-id="5a62a-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="5a62a-139">Щелкните **Создать** для сохранения нового ресурса сертификата.</span><span class="sxs-lookup"><span data-stu-id="5a62a-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="5a62a-140">Создание нового сертификата с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a62a-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="5a62a-141">В примере, приведенном ниже, демонстрируется, как создать сертификат службы автоматизации и пометить его как экспортируемый.</span><span class="sxs-lookup"><span data-stu-id="5a62a-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="5a62a-142">Вследствие этого импортируется существующий PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="5a62a-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="5a62a-143">Использование сертификата</span><span class="sxs-lookup"><span data-stu-id="5a62a-143">Using a certificate</span></span>

<span data-ttu-id="5a62a-144">Чтобы использовать сертификат, необходимо применить действие **Get-AutomationCertificate** .</span><span class="sxs-lookup"><span data-stu-id="5a62a-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="5a62a-145">Нельзя использовать командлет [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx), так как он возвращает сведения о ресурсе сертификата, но не сам сертификат.</span><span class="sxs-lookup"><span data-stu-id="5a62a-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="5a62a-146">Пример текстового Runbook</span><span class="sxs-lookup"><span data-stu-id="5a62a-146">Textual runbook sample</span></span>

<span data-ttu-id="5a62a-147">В следующем примере кода показано, как добавить сертификат из Runbook в облачную службу.</span><span class="sxs-lookup"><span data-stu-id="5a62a-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="5a62a-148">В этом примере пароль извлекается из зашифрованной переменной службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5a62a-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="5a62a-149">Пример графического Runbook</span><span class="sxs-lookup"><span data-stu-id="5a62a-149">Graphical runbook sample</span></span>

<span data-ttu-id="5a62a-150">Вы можете добавить **Get-AutomationCertificate** в графический компонент Runbook, щелкнув правой кнопкой мыши сертификат в области "Библиотека" графического редактора и выбрав пункт **Добавить на холст**.</span><span class="sxs-lookup"><span data-stu-id="5a62a-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![Добавление сертификата на холст](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="5a62a-152">На следующем рисунке показан пример использования сертификата в графическом Runbook.</span><span class="sxs-lookup"><span data-stu-id="5a62a-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="5a62a-153">Этот же пример был показан выше, он добавляет сертификат из текстового Runbook в облачную службу.</span><span class="sxs-lookup"><span data-stu-id="5a62a-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="5a62a-154">Пример графической разработки</span><span class="sxs-lookup"><span data-stu-id="5a62a-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="5a62a-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a62a-155">Next steps</span></span>

- <span data-ttu-id="5a62a-156">Дополнительные сведения о работе со связями, с помощью которых можно управлять логической последовательностью действий, выполняемых модулем Runbook, см. в [Связи и рабочий процесс](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="5a62a-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
