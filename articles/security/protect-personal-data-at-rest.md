---
title: "aaaAzure защитить личные данные хранятся с шифрованием | Документы Microsoft"
description: "В этой статье входит в серию, помогая использование Azure tooprotect личных данных"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="5dec5-103">Технологии шифрования Azure. Защита неактивных персональных данных с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="5dec5-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="5dec5-104">Эта статья поможет вам освоить и использовать данные toosecure технологии Azure шифрование при хранении.</span><span class="sxs-lookup"><span data-stu-id="5dec5-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="5dec5-105">Шифрование статических данных очень важно как лучший подход tooprotect конфиденциальных или личных данных, а также соответствие toomeet и требования к конфиденциальности данных.</span><span class="sxs-lookup"><span data-stu-id="5dec5-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="5dec5-106">Шифрование неактивных — спроектированный tooprevent hello злоумышленником доступа к данным, hello без шифрования, гарантируя hello, данные шифруются при на диске.</span><span class="sxs-lookup"><span data-stu-id="5dec5-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="5dec5-107">Сценарий</span><span class="sxs-lookup"><span data-stu-id="5dec5-107">Scenario</span></span> 

<span data-ttu-id="5dec5-108">Большой прогулка по организации, штаб-квартира компании в США, hello развернут расписаниям toooffer его операций в hello морская, балтийские компании seas, а также hello Британские острова.</span><span class="sxs-lookup"><span data-stu-id="5dec5-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="5dec5-109">toosupport эти усилия, он получил несколько небольших строк прогулка по в Италии, Германии, Дания и hello Великобритания</span><span class="sxs-lookup"><span data-stu-id="5dec5-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="5dec5-110">Hello компания использует Microsoft Azure toostore корпоративных данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="5dec5-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="5dec5-111">Это может включать сотрудников и/или сведения о заказчике такие как:</span><span class="sxs-lookup"><span data-stu-id="5dec5-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="5dec5-112">адреса;</span><span class="sxs-lookup"><span data-stu-id="5dec5-112">addresses</span></span>
- <span data-ttu-id="5dec5-113">номера телефонов;</span><span class="sxs-lookup"><span data-stu-id="5dec5-113">phone numbers</span></span>
- <span data-ttu-id="5dec5-114">идентификационные номера налогоплательщиков;</span><span class="sxs-lookup"><span data-stu-id="5dec5-114">tax identification numbers</span></span>
- <span data-ttu-id="5dec5-115">медицинские сведения</span><span class="sxs-lookup"><span data-stu-id="5dec5-115">medical information</span></span>
- <span data-ttu-id="5dec5-116">данные кредитной карты.</span><span class="sxs-lookup"><span data-stu-id="5dec5-116">credit card information</span></span>

<span data-ttu-id="5dec5-117">Hello компании должны защищать конфиденциальность hello данных сотрудников и клиентов во время внесения данных доступны toothose отделов, которым она необходима.</span><span class="sxs-lookup"><span data-stu-id="5dec5-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="5dec5-118">(например, отделах заработной платы и бронирования).</span><span class="sxs-lookup"><span data-stu-id="5dec5-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="5dec5-119">Строка Hello прогулка по также хранится большой базы данных вознаграждения и постоянных элементов программы, содержат персональные данные tootrack связи с клиентами, текущие и прошлые.</span><span class="sxs-lookup"><span data-stu-id="5dec5-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="5dec5-120">Проблема</span><span class="sxs-lookup"><span data-stu-id="5dec5-120">Problem statement</span></span>

<span data-ttu-id="5dec5-121">Hello компании должны защищать hello конфиденциальность личных данных сотрудников и клиентов во время внесения данных доступны toothose отделов, в которых он нужен (например, отделы заработной платы и резервирования).</span><span class="sxs-lookup"><span data-stu-id="5dec5-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="5dec5-122">Эти личные данные хранятся вне центра обработки данных, управляемых корпоративной hello, а не в физический контроль hello компании.</span><span class="sxs-lookup"><span data-stu-id="5dec5-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="5dec5-123">Цель компании</span><span class="sxs-lookup"><span data-stu-id="5dec5-123">Company goal</span></span>

<span data-ttu-id="5dec5-124">Как часть стратегии безопасности многоуровневый глубокой обороны это tooensure цель компании, что все источники данных, которые содержат персональные данные зашифрованы, включая находящиеся в Облачное хранилище.</span><span class="sxs-lookup"><span data-stu-id="5dec5-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="5dec5-125">Если несанкционированный лиц прибыль доступа toohello личных данных, ее необходимо в форме, которая сделает его может быть прочитан.</span><span class="sxs-lookup"><span data-stu-id="5dec5-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="5dec5-126">Шифрование должно быть простым или прозрачным для пользователей и администраторов.</span><span class="sxs-lookup"><span data-stu-id="5dec5-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="5dec5-127">Решения</span><span class="sxs-lookup"><span data-stu-id="5dec5-127">Solutions</span></span>

<span data-ttu-id="5dec5-128">Службы Azure предоставляют несколько средств и технологий toohelp защиты личных данных неактивные путем его шифрования.</span><span class="sxs-lookup"><span data-stu-id="5dec5-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="5dec5-129">Хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="5dec5-129">Azure Key Vault</span></span>

<span data-ttu-id="5dec5-130">[Хранилище ключей Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) обеспечивает безопасное хранение для hello ключей используется tooencrypt данные хранятся на служб Azure и hello рекомендуется ключа хранилища и управления ими.</span><span class="sxs-lookup"><span data-stu-id="5dec5-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="5dec5-131">Управление ключами шифрования — это основные toosecuring хранимые данные.</span><span class="sxs-lookup"><span data-stu-id="5dec5-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="5dec5-132">Как использовать хранилище ключей Azure tooprotect ключи шифрования персональные данные?</span><span class="sxs-lookup"><span data-stu-id="5dec5-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="5dec5-133">toouse хранилище ключей Azure, вы должны подписки tooan учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="5dec5-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="5dec5-134">Кроме того, необходимо установить Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dec5-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="5dec5-135">Шаги включают использование следующих hello toodo командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dec5-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="5dec5-136">Подключение tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="5dec5-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="5dec5-137">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="5dec5-137">Create a key vault</span></span>

3. <span data-ttu-id="5dec5-138">Добавление ключа или секрета toohello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5dec5-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="5dec5-139">Регистрация приложения, которые будет использовать хранилище ключей hello в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5dec5-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="5dec5-140">Авторизовать hello приложений toouse hello ключа или секрета</span><span class="sxs-lookup"><span data-stu-id="5dec5-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="5dec5-141">toocreate хранилища ключей, используйте командлет PowerShell New-AzureRmKeyVault hello.</span><span class="sxs-lookup"><span data-stu-id="5dec5-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="5dec5-142">Вы присвоите имя хранилища, имя группы ресурсов и географическое местоположение.</span><span class="sxs-lookup"><span data-stu-id="5dec5-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="5dec5-143">Имя хранилища hello будет использоваться при управлении ключами через другие командлеты.</span><span class="sxs-lookup"><span data-stu-id="5dec5-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="5dec5-144">Приложения, использующие хранилище hello через API-Интерфейс REST hello будет использовать хранилище hello URI.</span><span class="sxs-lookup"><span data-stu-id="5dec5-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="5dec5-145">Azure Key Vault предоставляет ключ с программной защитой. Вы также можете импортировать ключ, имеющийся в PFX-файле.</span><span class="sxs-lookup"><span data-stu-id="5dec5-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="5dec5-146">Можно также хранить секреты (пароли) в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="5dec5-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="5dec5-147">Можно также создать ключ в ваш локальный HSM и передачи tooHSMs в hello службы хранилища ключей без ключа hello, оставляя границ HSM hello.</span><span class="sxs-lookup"><span data-stu-id="5dec5-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="5dec5-148">Подробные инструкции по использованию хранилища ключей Azure, выполните шаги hello [Приступая к работе с хранилищем ключей Azure.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="5dec5-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="5dec5-149">Сведения о списке командлетов PowerShell, используемых с Azure Key Vault, см. в статье [Azure​RM.​Key​Vault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="5dec5-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="5dec5-150">Шифрование дисков Azure для Windows</span><span class="sxs-lookup"><span data-stu-id="5dec5-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="5dec5-151">[Шифрование дисков Azure для виртуальных машин IaaS под управлением Windows и Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) позволяет защитить неактивные персональные данные на виртуальных машинах Azure. Эта возможность интегрируется с Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5dec5-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="5dec5-152">Использует Azure шифрование диска [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) в Windows и [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) в Linux tooencrypt оба hello ОС и hello диски с данными.</span><span class="sxs-lookup"><span data-stu-id="5dec5-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="5dec5-153">Шифрование дисков Azure поддерживается в Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, а также клиентах Windows 8 и Windows 10.</span><span class="sxs-lookup"><span data-stu-id="5dec5-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="5dec5-154">Как использовать шифрование диска Azure tooprotect персональные данные?</span><span class="sxs-lookup"><span data-stu-id="5dec5-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="5dec5-155">toouse шифрование диска Azure требуется подписка tooan учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="5dec5-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="5dec5-156">tooenable Azure диск шифрования для Windows и виртуальных машин Linux hello следующие:</span><span class="sxs-lookup"><span data-stu-id="5dec5-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="5dec5-157">Укажите hello шаблона диспетчера ресурсов шифрования диска Azure, PowerShell или шифрование диска tooenable hello командной строки (CLI) и конфигурации шифрования.</span><span class="sxs-lookup"><span data-stu-id="5dec5-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="5dec5-158">Предоставление доступа toohello основы платформы Azure tooread hello шифрования из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5dec5-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="5dec5-159">Укажите Azure Active Directory (AAD) приложение удостоверения toowrite hello шифрования ключа материала tooyour хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5dec5-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="5dec5-160">Azure будет обновить hello виртуальных Машин и хранилища ключей конфигурации hello и настройка зашифрованных ВМ.</span><span class="sxs-lookup"><span data-stu-id="5dec5-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="5dec5-161">При настройке toosupport вашего хранилища ключей шифрования диска Azure можно добавить ключ ключа шифрования (ключ обмена Ключами) для повышения безопасности и резервного копирования toosupport зашифрованные виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5dec5-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="5dec5-162">Подробные инструкции для определенных сценариев развертывания и взаимодействия с пользователем см. в статье [Дисковое шифрование Azure для виртуальных машин IaaS под управлением Windows и Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="5dec5-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="5dec5-163">Шифрование службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="5dec5-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="5dec5-164">[Azure хранилища службы шифрования (SSE) для статических данных](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) помогает защитить и защиты вашего toomeet данных организации свои обязательства по безопасности и соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="5dec5-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="5dec5-165">Хранилище Azure автоматически шифрует данные с помощью toostorage предыдущих toopersisting шифрования AES 256-разрядный и расшифровывает его предыдущего tooretrieval.</span><span class="sxs-lookup"><span data-stu-id="5dec5-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="5dec5-166">Эта служба доступна для файлов и больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5dec5-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="5dec5-167">Как использовать шифрование службы хранилища tooprotect персональные данные?</span><span class="sxs-lookup"><span data-stu-id="5dec5-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="5dec5-168">Шифрование службы хранилища, tooenable hello следующие:</span><span class="sxs-lookup"><span data-stu-id="5dec5-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="5dec5-169">Войдите на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5dec5-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="5dec5-170">Выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="5dec5-170">Select a storage account.</span></span>

3. <span data-ttu-id="5dec5-171">В параметрах в разделе "hello" BLOB-объектов, выберите шифрования.</span><span class="sxs-lookup"><span data-stu-id="5dec5-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="5dec5-172">Установите шифрования hello раздела службы файлов.</span><span class="sxs-lookup"><span data-stu-id="5dec5-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="5dec5-173">После щелчка шифрования приветствия, можно включить или отключить шифрование службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="5dec5-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="5dec5-174">Новые данные будут зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="5dec5-174">New data will be encrypted.</span></span> <span data-ttu-id="5dec5-175">Данные в имеющихся файлах этой учетной записи хранения останутся незашифрованными.</span><span class="sxs-lookup"><span data-stu-id="5dec5-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="5dec5-176">После включения шифрования, скопируйте данные учетной записи хранилища toohello с помощью одного из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="5dec5-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="5dec5-177">Копирование больших двоичных объектов или файлов с hello [служебной программы командной строки AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="5dec5-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="5dec5-178">[Подключить общей папки SMB с помощью](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) , можно использовать программу, например файлы toocopy Robocopy.</span><span class="sxs-lookup"><span data-stu-id="5dec5-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="5dec5-179">Скопируйте большой двоичный объект или файл данных tooand из хранилища BLOB-объектов или между хранилища учетных записей с помощью [клиентских библиотек хранилища, такие как .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="5dec5-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="5dec5-180">Используйте [обозреватель хранилищ](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload BLOB-объектов учетной записи хранилища tooyour с включенным шифрованием.</span><span class="sxs-lookup"><span data-stu-id="5dec5-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="5dec5-181">Прозрачное шифрование данных</span><span class="sxs-lookup"><span data-stu-id="5dec5-181">Transparent Data Encryption</span></span>

<span data-ttu-id="5dec5-182">Прозрачное шифрование данных (TDE) является компонентом в SQL Azure, с помощью которого можно шифровать данные на обоих уровнях hello базы данных и сервера.</span><span class="sxs-lookup"><span data-stu-id="5dec5-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="5dec5-183">Эта функция теперь включена по умолчанию во всех новых базах данных.</span><span class="sxs-lookup"><span data-stu-id="5dec5-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="5dec5-184">Прозрачное шифрование данных выполняет в реальном времени ввода-вывода шифрование и дешифрование файлов данных и журналов hello.</span><span class="sxs-lookup"><span data-stu-id="5dec5-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="5dec5-185">Использование прозрачного шифрования данных tooprotect персональные данные</span><span class="sxs-lookup"><span data-stu-id="5dec5-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="5dec5-186">Прозрачное шифрование данных можно настроить через hello портал Azure с помощью API-интерфейса REST hello, или с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dec5-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="5dec5-187">tooenable прозрачное шифрование данных на существующей базы данных с помощью портала Azure hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="5dec5-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="5dec5-188">Посетите hello Azure портала в <https://portal.azure.com> и войдите с учетной записью администратора или участника Azure.</span><span class="sxs-lookup"><span data-stu-id="5dec5-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="5dec5-189">В hello слева щелкните tooBROWSE и выберите базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5dec5-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="5dec5-190">С базами данных SQL, выбранной в левой области hello выберите пользовательскую базу данных.</span><span class="sxs-lookup"><span data-stu-id="5dec5-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="5dec5-191">В колонке базы данных hello выберите все параметры.</span><span class="sxs-lookup"><span data-stu-id="5dec5-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="5dec5-192">В колонке параметров hello щелкните прозрачное шифрование часть tooopen hello прозрачное шифрование колонку.</span><span class="sxs-lookup"><span data-stu-id="5dec5-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="5dec5-193">В колонке шифрования данных hello переместить tooOn кнопка шифрования данных hello и нажмите кнопку Сохранить (в начале hello страницы приветствия) tooapply приветствия.</span><span class="sxs-lookup"><span data-stu-id="5dec5-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="5dec5-194">состояние шифрования Hello будет отображаться приблизительный ход выполнения hello hello прозрачное шифрование данных.</span><span class="sxs-lookup"><span data-stu-id="5dec5-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![Включение шифрования данных](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="5dec5-196">Инструкции по обнаружение tooenable прозрачного шифрования данных и сведения о расшифровке базы данных с защитой TDE и многое другое в статье hello [прозрачное шифрование данных с базой данных SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="5dec5-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="5dec5-197">Сводка</span><span class="sxs-lookup"><span data-stu-id="5dec5-197">Summary</span></span>

<span data-ttu-id="5dec5-198">Hello компании можно выполнить его задача шифрования персональные данные, хранящиеся в облаке Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5dec5-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="5dec5-199">Это можно сделать с помощью шифрования диска Azure слишком защитить всего тома.</span><span class="sxs-lookup"><span data-stu-id="5dec5-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="5dec5-200">Это может включать hello системные файлы и файлы данных, которые содержат персональные данные и другие конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="5dec5-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="5dec5-201">Azure шифрование службы хранилища может быть используется tooprotect персональные данные, хранящиеся в файлах и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5dec5-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="5dec5-202">К персональным данным, хранящимся в базе данных SQL Azure, можно применить прозрачное шифрование, которое обеспечивает защиту от несанкционированного доступа.</span><span class="sxs-lookup"><span data-stu-id="5dec5-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="5dec5-203">ключи hello tooprotect, используемые tooencrypt данные в Azure, hello компании можно использовать хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="5dec5-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="5dec5-204">Это упрощает процесс управления ключами hello и включает hello компании toomaintain управление ключами, которые обращаются к и шифрования личных данных.</span><span class="sxs-lookup"><span data-stu-id="5dec5-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dec5-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5dec5-205">Next steps</span></span>

- [<span data-ttu-id="5dec5-206">Руководство по устранению неполадок шифрования дисков Azure</span><span class="sxs-lookup"><span data-stu-id="5dec5-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="5dec5-207">Шифрование виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="5dec5-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="5dec5-208">Шифрование данных в Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5dec5-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="5dec5-209">Шифрование неактивных данных базы данных в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5dec5-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
