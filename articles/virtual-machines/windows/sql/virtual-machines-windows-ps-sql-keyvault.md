---
title: "aaaIntegrate хранилища ключей с SQL Server на виртуальных машинах Windows в Azure (диспетчера ресурсов) | Документы Microsoft"
description: "Узнайте, как tooautomate hello конфигурация шифрования SQL Server для использования с хранилищем ключей Azure. Этот раздел объясняет, как toouse интеграция хранилища ключей Azure с виртуальными машинами SQL Server создавать с помощью диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="9dfdc-104">Настройка интеграции Azure Key Vault для SQL Server на виртуальных машинах Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="9dfdc-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9dfdc-105">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="9dfdc-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="9dfdc-106">Классический</span><span class="sxs-lookup"><span data-stu-id="9dfdc-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9dfdc-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="9dfdc-107">Overview</span></span>
<span data-ttu-id="9dfdc-108">Существует несколько функций шифрования SQL Server, например [прозрачное шифрование данных (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [шифрование на уровне столбцов (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) и [шифрование резервной копии](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="9dfdc-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="9dfdc-109">Эти формы шифрования требуют toomanage и хранения hello криптографических ключей, который используется для шифрования.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="9dfdc-110">Hello службы хранилища ключей Azure (AKV) — спроектированный tooimprove hello безопасности и управления из этих ключей в расположении высокой надежности и безопасности.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="9dfdc-111">Hello [соединителя SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) позволяет SQL Server toouse эти ключи из хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="9dfdc-112">При работе с приложением SQL Server с локальной машины, существует, [действия можно выполнить tooaccess хранилище ключей Azure с локального компьютера SQL Server](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="9dfdc-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="9dfdc-113">Но для SQL Server в виртуальных машинах Azure, вы можете сэкономить время с помощью hello *интеграция хранилища ключей Azure* компонентов.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="9dfdc-114">Если эта функция включена, автоматически устанавливает hello соединителя SQL Server, настраивает tooaccess поставщика расширенного управления Ключами hello хранилище ключей Azure и создает tooallow hello учетных данных вы tooaccess вашего хранилища.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="9dfdc-115">Если был рассмотрен hello инструкциям hello упомянутых выше локальной документации, вы увидите, что эта функция автоматизирует шаги 2 и 3.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="9dfdc-116">Единственное Hello по-прежнему необходимо toodo вручную — хранилище ключей toocreate hello и ключи.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="9dfdc-117">После этого выполняется автоматически hello всю настройку ВМ SQL.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="9dfdc-118">После завершения программы установки эту функцию можно выполнить toobegin инструкции T-SQL, шифрование баз данных или резервного копирования, как обычно.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="9dfdc-119">Включение и настройка интеграции AKV</span><span class="sxs-lookup"><span data-stu-id="9dfdc-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="9dfdc-120">Интеграцию AKV можно включить во время подготовки или настроить ее для существующих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="9dfdc-121">Новые виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="9dfdc-121">New VMs</span></span>
<span data-ttu-id="9dfdc-122">При подготовке новой виртуальной машины SQL Server с помощью диспетчера ресурсов hello портал Azure предоставляет tooenable шаг интеграцию хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="9dfdc-123">функция хранилища ключей Azure Hello доступна только для hello Enterprise, Developer и Evaluation выпусками SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Интеграция SQL с хранилищем ключей Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="9dfdc-125">Подробное пошаговое руководство подготовки см. в разделе [подготовки виртуальной машины SQL Server в портале Azure hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="9dfdc-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="9dfdc-126">Существующие виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="9dfdc-126">Existing VMs</span></span>
<span data-ttu-id="9dfdc-127">Выберите существующую виртуальную машину SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="9dfdc-128">Затем выберите hello **конфигурации SQL Server** раздел hello **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Интеграция AKV SQL для существующих виртуальных машин](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="9dfdc-130">В hello **конфигурации SQL Server** колонка, щелкните hello **изменить** кнопку в hello разделе автоматическое хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![Настройка интеграции AKV SQL для существующих виртуальных машин](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="9dfdc-132">По завершении нажмите кнопку hello **ОК** кнопку внизу hello hello **конфигурации SQL Server** toosave колонке изменения.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="9dfdc-133">Можно также настроить интеграцию AKV с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="9dfdc-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="9dfdc-134">Чтобы получить дополнительные сведения, ознакомьтесь с [шаблоном быстрого запуска Azure для интеграции с хранилищем ключей Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="9dfdc-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

