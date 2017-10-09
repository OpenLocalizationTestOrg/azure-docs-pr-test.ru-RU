---
title: "aaaCertificate средств автоматизации Azure | Документы Microsoft"
description: "Сертификаты могут быть безопасно сохранены в службе автоматизации Azure, они могли быть доступны модули Runbook или tooauthenticate конфигурации DSC для Azure и ресурсы сторонних поставщиков.  В этой статье подробно описывается hello сертификатов и как toowork с ними в текстовых и графических разработки."
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
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="b7eb8-104">Сертификация активов в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="b7eb8-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="b7eb8-105">Сертификаты могут быть безопасно сохранены в службе автоматизации Azure, чтобы они могли быть доступны модули Runbook или конфигурации DSC с помощью hello **Get AzureRmAutomationRmCertificate** действия для ресурсов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="b7eb8-106">Это позволяет вам toocreate Runbook и конфигураций DSC, которые используют сертификаты для проверки подлинности или добавляет их tooAzure и сторонних поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="b7eb8-107">Безопасные средства в службе автоматизации Azure включают учетные данные, сертификаты, подключения и зашифрованные переменные.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="b7eb8-108">Эти ресурсы шифруются и хранятся в hello автоматизации Azure, используя уникальный ключ, который создается для каждой учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="b7eb8-109">Ключ шифруется главным сертификатом и хранится в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="b7eb8-110">Перед сохранением безопасного ресурса, hello ключ для учетной записи автоматизации hello расшифровывается с помощью шаблона сертификата hello и затем использовать tooencrypt hello активов.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="b7eb8-111">Командлеты Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7eb8-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="b7eb8-112">командлеты Hello в следующей таблице hello, используемые toocreate и управлять ресурсами сертификатов автоматизации с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="b7eb8-113">Они поставляются как часть hello [модуля Azure PowerShell](../powershell-install-configure.md) доступный для использования в Runbook автоматизации и конфигураций DSC.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="b7eb8-114">Командлеты</span><span class="sxs-lookup"><span data-stu-id="b7eb8-114">Cmdlets</span></span>|<span data-ttu-id="b7eb8-115">Описание</span><span class="sxs-lookup"><span data-stu-id="b7eb8-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="b7eb8-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="b7eb8-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="b7eb8-117">Извлекает сведения о toouse сертификата в конфигурации DSC или runbook.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="b7eb8-118">Из действия Get-AutomationCertificate можно извлечь только сам сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="b7eb8-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="b7eb8-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="b7eb8-120">Создает сертификат в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="b7eb8-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="b7eb8-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="b7eb8-122">Удаляет сертификат из службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="b7eb8-123">Создает сертификат в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="b7eb8-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="b7eb8-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="b7eb8-125">Задает свойства hello для существующего сертификата, включая Отправка файла сертификата hello и параметр hello пароль для PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="b7eb8-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="b7eb8-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="b7eb8-127">Отправка сертификата службы для hello указан облачной службы.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="b7eb8-128">Создание нового сертификата</span><span class="sxs-lookup"><span data-stu-id="b7eb8-128">Creating a new certificate</span></span>

<span data-ttu-id="b7eb8-129">При создании нового сертификата, загруженный CER или PFX файл tooAzure автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="b7eb8-130">Если пометить hello сертификат как экспортируемый, можно перенести его из хранилища сертификатов службы автоматизации Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="b7eb8-131">Если он не может быть экспортирован, затем он может использоваться только для подписи в пределах hello runbook или конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="b7eb8-132">toocreate новый сертификат с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b7eb8-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="b7eb8-133">Из учетной записи автоматизации, нажмите кнопку hello **активы** плитки приветствия tooopen **активы** колонку.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="b7eb8-134">Щелкните hello **сертификаты** плитки приветствия tooopen **сертификаты** колонку.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="b7eb8-135">Нажмите кнопку **Добавление сертификата** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="b7eb8-136">Введите имя для сертификата hello в hello **имя** поле.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="b7eb8-137">Нажмите кнопку **выберите файл** под **загрузить файл сертификата** toobrowse файл CER или PFX.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="b7eb8-138">Если выбран PFX-файл, укажите пароль и ли ему должен быть разрешен toobe экспортированы.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="b7eb8-139">Нажмите кнопку **создать** toosave hello нового сертификата актива.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="b7eb8-140">toocreate новый сертификат с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7eb8-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="b7eb8-141">Hello следующем примере показано, как toocreate новый автоматизации сертификатов и пометить его экспортируемым.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="b7eb8-142">Вследствие этого импортируется существующий PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="b7eb8-143">Использование сертификата</span><span class="sxs-lookup"><span data-stu-id="b7eb8-143">Using a certificate</span></span>

<span data-ttu-id="b7eb8-144">Необходимо использовать hello **Get-AutomationCertificate** toouse действия сертификата.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="b7eb8-145">Нельзя использовать hello [Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) командлета, поскольку он возвращает сведения о ресурсе сертификата hello, а не самого сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="b7eb8-146">Пример текстового Runbook</span><span class="sxs-lookup"><span data-stu-id="b7eb8-146">Textual runbook sample</span></span>

<span data-ttu-id="b7eb8-147">Привет, следующий пример кода показывает, как tooadd tooa сертификата облачной службы в модуле runbook.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="b7eb8-148">В этом образце hello пароль извлекается из зашифрованной переменной автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="b7eb8-149">Пример графического Runbook</span><span class="sxs-lookup"><span data-stu-id="b7eb8-149">Graphical runbook sample</span></span>

<span data-ttu-id="b7eb8-150">Добавить **Get-AutomationCertificate** tooa графический runbook, щелкнув сертификат hello в области библиотеки hello графического редактора hello и выбрав **добавить toocanvas**.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Добавление сертификата toohello холста](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="b7eb8-152">Hello следующем рисунке показан пример использование сертификата в графический runbook.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="b7eb8-153">Это hello примера, показанного выше для добавления сертификата tooa облачной службы из текстовой runbook.</span><span class="sxs-lookup"><span data-stu-id="b7eb8-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="b7eb8-154">Пример графической разработки</span><span class="sxs-lookup"><span data-stu-id="b7eb8-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="b7eb8-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7eb8-155">Next steps</span></span>

- <span data-ttu-id="b7eb8-156">tooperform разработан toolearn больше о работе с ссылки toocontrol hello логический поток действий runbook, см. в разделе [ссылки в графический разработки](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="b7eb8-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
