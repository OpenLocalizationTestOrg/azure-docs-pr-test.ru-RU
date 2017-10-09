---
title: "развертывание службы приложений Azure стеке aaaBefore | Документы Microsoft"
description: "Toocomplete действия перед развертыванием службы приложений Azure стеке"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: fad758232ef2795105036640c2a26abf3fa2c3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a><span data-ttu-id="98498-103">Перед началом работы со службой приложения на стек Azure</span><span class="sxs-lookup"><span data-stu-id="98498-103">Before you get started with App Service on Azure Stack</span></span>

<span data-ttu-id="98498-104">Необходимо несколько элементов tooinstall службе приложений Azure в стеке Azure:</span><span class="sxs-lookup"><span data-stu-id="98498-104">You need a few items tooinstall Azure App Service on Azure Stack:</span></span>

- <span data-ttu-id="98498-105">Завершено развертывание hello [пакет средств разработки Azure стека](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="98498-105">A completed deployment of hello [Azure Stack development kit](azure-stack-run-powershell-script.md).</span></span>
- <span data-ttu-id="98498-106">Недостаточно места в системе Azure стека для небольшого развертывания службы приложений Azure стек.</span><span class="sxs-lookup"><span data-stu-id="98498-106">Enough space in your Azure Stack system for a small deployment of App Service on Azure Stack.</span></span>  <span data-ttu-id="98498-107">Hello обязательные пространства — примерно 20 ГБ пространства на диске.</span><span class="sxs-lookup"><span data-stu-id="98498-107">hello required space is roughly 20 GB of disk space.</span></span>
- <span data-ttu-id="98498-108">Образ виртуальной Машины Windows Server для использования при создании виртуальных машин для службы приложений Azure стек.</span><span class="sxs-lookup"><span data-stu-id="98498-108">A Windows Server VM image for use when you create virtual machines for App Service on Azure Stack.</span></span>
- <span data-ttu-id="98498-109">[Сервер, на котором выполняется SQL Server](#SQL-Server).</span><span class="sxs-lookup"><span data-stu-id="98498-109">[A server that's running SQL Server](#SQL-Server).</span></span>

>[!NOTE] 
> <span data-ttu-id="98498-110">Здравствуйте, следующие действия *все* вступят в силу на хост-компьютере hello Azure стека.</span><span class="sxs-lookup"><span data-stu-id="98498-110">hello following steps *all* take place on hello Azure Stack host machine.</span></span>

<span data-ttu-id="98498-111">hello PowerShell интегрированная среда сценариев (ISE) toodeploy поставщик ресурсов должен запускаться от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="98498-111">toodeploy a resource provider, you must run hello PowerShell Integrated Scripting Environment (ISE) as an administrator.</span></span> <span data-ttu-id="98498-112">По этой причине необходимо tooallow файлы cookie и JavaScript в профиле Internet Explorer hello использовать toosign в tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="98498-112">For this reason, you need tooallow cookies and JavaScript in hello Internet Explorer profile that you use toosign in tooAzure Active Directory.</span></span>

## <a name="turn-off-internet-explorer-enhanced-security"></a><span data-ttu-id="98498-113">Отключите в Internet Explorer Усиленная безопасность</span><span class="sxs-lookup"><span data-stu-id="98498-113">Turn off Internet Explorer enhanced security</span></span>

1.  <span data-ttu-id="98498-114">Войдите в компьютер для комплекта средств для разработки toohello стека Azure как **AzureStack или администратор**, а затем откройте **диспетчера сервера**.</span><span class="sxs-lookup"><span data-stu-id="98498-114">Sign in toohello Azure Stack development kit machine as **AzureStack/administrator**, and then open **Server Manager**.</span></span>

2.  <span data-ttu-id="98498-115">Отключить **конфигурация усиленной безопасности Internet Explorer** для администраторов и пользователей.</span><span class="sxs-lookup"><span data-stu-id="98498-115">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

3.  <span data-ttu-id="98498-116">Войдите в компьютер для комплекта средств для разработки toohello стека Azure с правами администратора, а затем откройте **диспетчера сервера**.</span><span class="sxs-lookup"><span data-stu-id="98498-116">Sign in toohello Azure Stack development kit machine as an administrator, and then open **Server Manager**.</span></span>

4.  <span data-ttu-id="98498-117">Отключить **конфигурация усиленной безопасности Internet Explorer** для администраторов и пользователей.</span><span class="sxs-lookup"><span data-stu-id="98498-117">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

## <a name="enable-cookies"></a><span data-ttu-id="98498-118">Разрешить файлы cookie</span><span class="sxs-lookup"><span data-stu-id="98498-118">Enable cookies</span></span>

1.  <span data-ttu-id="98498-119">Выберите **запустить** > **все приложения** > **стандартные Windows**.</span><span class="sxs-lookup"><span data-stu-id="98498-119">Select **Start** > **All apps** > **Windows accessories**.</span></span> <span data-ttu-id="98498-120">Щелкните правой кнопкой мыши **Internet Explorer** > **дополнительные** > **запустить с правами администратора**.</span><span class="sxs-lookup"><span data-stu-id="98498-120">Right-click **Internet Explorer** > **More** > **Run as an administrator**.</span></span>

2.  <span data-ttu-id="98498-121">Если появится запрос, выберите **безопасности рекомендуется использовать**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="98498-121">If you're prompted, select **Use recommended security**, and then select **OK**.</span></span>

3.  <span data-ttu-id="98498-122">В Internet Explorer выберите **средства** (значок шестеренки hello) > **обозревателя** > **конфиденциальности** > **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="98498-122">In Internet Explorer, select **Tools** (hello gear icon) > **Internet Options** > **Privacy** > **Advanced**.</span></span>

4.  <span data-ttu-id="98498-123">Нажмите кнопку **Advanced** (Дополнительно).</span><span class="sxs-lookup"><span data-stu-id="98498-123">Select **Advanced**.</span></span> <span data-ttu-id="98498-124">Убедитесь, что оба **Accept** флажки.</span><span class="sxs-lookup"><span data-stu-id="98498-124">Make sure that both **Accept** check boxes are selected.</span></span> <span data-ttu-id="98498-125">Выберите **ОК** дважды.</span><span class="sxs-lookup"><span data-stu-id="98498-125">Select **OK** twice.</span></span>

5.  <span data-ttu-id="98498-126">Закройте Internet Explorer и перезапустите hello интегрированной среды Сценариев PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="98498-126">Close Internet Explorer, and restart hello PowerShell ISE as an administrator.</span></span>

## <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="98498-127">Установите PowerShell для Azure стека</span><span class="sxs-lookup"><span data-stu-id="98498-127">Install PowerShell for Azure Stack</span></span>

<span data-ttu-id="98498-128">tooinstall PowerShell для Azure стека, следуйте указаниям hello [установите PowerShell](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="98498-128">tooinstall PowerShell for Azure Stack, follow hello steps in [Install PowerShell](azure-stack-powershell-install.md).</span></span>

## <a name="use-visual-studio-with-azure-stack"></a><span data-ttu-id="98498-129">Использование Visual Studio с стек Azure</span><span class="sxs-lookup"><span data-stu-id="98498-129">Use Visual Studio with Azure Stack</span></span>

<span data-ttu-id="98498-130">toouse Visual Studio с стек Azure, следуйте указаниям hello [установите Visual Studio](azure-stack-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="98498-130">toouse Visual Studio with Azure Stack, follow hello steps in [Install Visual Studio](azure-stack-install-visual-studio.md).</span></span>

## <a name="add-a-windows-server-2016-vm-image-tooazure-stack"></a><span data-ttu-id="98498-131">Добавьте tooAzure образа виртуальной Машины Windows Server 2016 стека</span><span class="sxs-lookup"><span data-stu-id="98498-131">Add a Windows Server 2016 VM image tooAzure Stack</span></span>

<span data-ttu-id="98498-132">Поскольку службы приложений развертывает число виртуальных машин, требуется образ виртуальной Машины Windows Server 2016 в стек Azure.</span><span class="sxs-lookup"><span data-stu-id="98498-132">Because App Service deploys a number of virtual machines, it requires a Windows Server 2016 VM image in Azure Stack.</span></span> <span data-ttu-id="98498-133">tooinstall образ виртуальной Машины, выполните действия hello в [добавить образ виртуальной машины по умолчанию](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="98498-133">tooinstall a VM image, follow hello steps in [Add a default virtual machine image](azure-stack-add-default-image.md).</span></span>

## <span data-ttu-id="98498-134"><a name="SQL-Server"></a>SQL Server</span><span class="sxs-lookup"><span data-stu-id="98498-134"><a name="SQL-Server"></a>SQL Server</span></span>

<span data-ttu-id="98498-135">Службы приложений Azure стеке требуется доступ tooa SQL Server экземпляр toocreate и узла две базы данных toorun hello поставщик ресурсов службы приложений.</span><span class="sxs-lookup"><span data-stu-id="98498-135">App Service on Azure Stack requires access tooa SQL Server instance toocreate and host two databases toorun hello App Service resource provider.</span></span>  <span data-ttu-id="98498-136">Следует выбрать toodeploy ВМ SQL Server в стеке Azure, он должен иметь значение слишком уровня подключения SQL hello**открытый**.</span><span class="sxs-lookup"><span data-stu-id="98498-136">Should you choose toodeploy a SQL Server VM on Azure Stack it must have hello SQL connectivity level set too**Public**.</span></span>  <span data-ttu-id="98498-137">Вы можете toouse экземпляр SQL Server hello при завершении параметры hello в hello службы приложений Azure стека установщика.</span><span class="sxs-lookup"><span data-stu-id="98498-137">You can choose hello SQL Server instance toouse when you complete hello options in hello App Service on Azure Stack installer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98498-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98498-138">Next steps</span></span>

- <span data-ttu-id="98498-139">[Установить поставщик ресурсов службы приложения hello](azure-stack-app-service-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="98498-139">[Install hello App Service resource provider](azure-stack-app-service-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
