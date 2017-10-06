---
title: "шлюз данных в локальной aaaInstall | Документы Microsoft"
description: "Узнайте, как tooinstall и настройте локальный шлюз данных."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="38e92-103">Установка и настройка локального шлюза данных</span><span class="sxs-lookup"><span data-stu-id="38e92-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="38e92-104">Локальный шлюз данных является обязательным, если один или несколько серверов Azure Analysis Services в hello же региона подключения tooon локальные источники данных.</span><span class="sxs-lookup"><span data-stu-id="38e92-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="38e92-105">toolearn Дополнительные сведения о шлюзе hello. в разделе [локального шлюза данных](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="38e92-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38e92-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="38e92-106">Prerequisites</span></span>
<span data-ttu-id="38e92-107">**Минимальные требования:**</span><span class="sxs-lookup"><span data-stu-id="38e92-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="38e92-108">.NET Framework 4.5;</span><span class="sxs-lookup"><span data-stu-id="38e92-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="38e92-109">64-разрядная версия Windows 7 / Windows Server 2008 R2 (или более новой версии).</span><span class="sxs-lookup"><span data-stu-id="38e92-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="38e92-110">**Рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="38e92-110">**Recommended:**</span></span>

* <span data-ttu-id="38e92-111">8-ядерный ЦП;</span><span class="sxs-lookup"><span data-stu-id="38e92-111">8 Core CPU</span></span>
* <span data-ttu-id="38e92-112">8 ГБ ОЗУ;</span><span class="sxs-lookup"><span data-stu-id="38e92-112">8 GB Memory</span></span>
* <span data-ttu-id="38e92-113">64-разрядная версия Windows 2012 R2 (или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="38e92-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="38e92-114">**Важные сведения:**</span><span class="sxs-lookup"><span data-stu-id="38e92-114">**Important considerations:**</span></span>

* <span data-ttu-id="38e92-115">Во время установки Регистрация шлюза в Azure выбирается hello регион по умолчанию для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="38e92-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="38e92-116">Вы можете выбрать другой регион.</span><span class="sxs-lookup"><span data-stu-id="38e92-116">You can choose a different region.</span></span> <span data-ttu-id="38e92-117">При наличии серверов в нескольких регионах необходимо установить шлюз для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="38e92-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="38e92-118">Невозможно установить шлюз Hello на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="38e92-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="38e92-119">На одном компьютере можно установить только один шлюз.</span><span class="sxs-lookup"><span data-stu-id="38e92-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="38e92-120">Hello шлюз можно установите на компьютере, который остается на и не переходит в toosleep.</span><span class="sxs-lookup"><span data-stu-id="38e92-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="38e92-121">Не устанавливайте шлюз hello в сети через беспроводное соединение подключенных tooyour.</span><span class="sxs-lookup"><span data-stu-id="38e92-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="38e92-122">Это может стать причиной снижения производительности.</span><span class="sxs-lookup"><span data-stu-id="38e92-122">Performance can be diminished.</span></span>


## <span data-ttu-id="38e92-123"><a name="download"></a>Загрузка</span><span class="sxs-lookup"><span data-stu-id="38e92-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="38e92-124">Загрузите шлюз hello</span><span class="sxs-lookup"><span data-stu-id="38e92-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="38e92-125"><a name="install"></a>Установка</span><span class="sxs-lookup"><span data-stu-id="38e92-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="38e92-126">Запустите программу установки.</span><span class="sxs-lookup"><span data-stu-id="38e92-126">Run setup.</span></span>

2. <span data-ttu-id="38e92-127">Выберите расположение, примите условия hello и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="38e92-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Расположение для установки и условия лицензии](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="38e92-129">Установите флажок **On-premises data gateway (recommended)** (Локальный шлюз данных (рекомендуется)).</span><span class="sxs-lookup"><span data-stu-id="38e92-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="38e92-130">Azure Analysis Services не поддерживает личный режим.</span><span class="sxs-lookup"><span data-stu-id="38e92-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Выбор типа шлюза](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="38e92-132">Введите учетную запись toosign в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="38e92-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="38e92-133">Учетная запись Hello должна быть в вашего клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38e92-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="38e92-134">Эта учетная запись используется для hello администратору шлюза.</span><span class="sxs-lookup"><span data-stu-id="38e92-134">This account is used for hello gateway administrator.</span></span> 

   ![Введите учетную запись toosign в tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="38e92-136">Если выполнить вход с учетной записью домена, он будет сопоставлен tooyour учетную запись организации в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38e92-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="38e92-137">Администратор шлюза hello hello будет использоваться учетной записью вашей организации.</span><span class="sxs-lookup"><span data-stu-id="38e92-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="38e92-138"><a name="register"></a>Регистрация</span><span class="sxs-lookup"><span data-stu-id="38e92-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="38e92-139">В порядке toocreate ресурс шлюза в Azure необходимо зарегистрировать локальный экземпляр hello, установленный с hello облачной службе шлюза.</span><span class="sxs-lookup"><span data-stu-id="38e92-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="38e92-140">Выберите **Регистрация нового шлюза на этом компьютере**.</span><span class="sxs-lookup"><span data-stu-id="38e92-140">Select **Register a new gateway on this computer**.</span></span>

    ![регистрация;](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="38e92-142">Введите имя и ключ восстановления для шлюза.</span><span class="sxs-lookup"><span data-stu-id="38e92-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="38e92-143">По умолчанию hello шлюз использует область по умолчанию для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="38e92-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="38e92-144">Если вам требуется tooselect другой регион, выберите **Смена региона**.</span><span class="sxs-lookup"><span data-stu-id="38e92-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![регистрация;](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="38e92-146"><a name="create-resource"></a>Создание ресурса шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="38e92-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="38e92-147">После установки и регистрации шлюза необходимо toocreate ресурсов шлюза в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="38e92-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="38e92-148">Вход tooAzure с hello же учетная запись, используемая при регистрации шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="38e92-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="38e92-149">На портале Azure щелкните **Create a new service** (Создать службу) > **Enterprise Integration** (Интеграция Enterprise) > **Локальный шлюз данных** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="38e92-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Создание ресурса шлюза](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="38e92-151">В разделе **Create connection gateway** (Создать шлюз для подключения) введите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="38e92-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="38e92-152">**Имя.** Введите имя для вашего ресурса шлюза.</span><span class="sxs-lookup"><span data-stu-id="38e92-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="38e92-153">**Подписки**: выберите hello tooassociate подписки Azure с этим ресурсом шлюза.</span><span class="sxs-lookup"><span data-stu-id="38e92-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="38e92-154">Это подписка должна быть hello серверы находятся в одной подписке.</span><span class="sxs-lookup"><span data-stu-id="38e92-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="38e92-155">Подписка по умолчанию Hello основан на hello учетная запись Azure, который использовался toosign в.</span><span class="sxs-lookup"><span data-stu-id="38e92-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="38e92-156">**Группа ресурсов.** Создайте группу ресурсов Azure или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="38e92-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="38e92-157">**Расположение**: регистрации шлюза в области выберите hello.</span><span class="sxs-lookup"><span data-stu-id="38e92-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="38e92-158">**Установка имя**: Если для установки шлюза еще не выбрана, выберите hello шлюз зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="38e92-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="38e92-159">Когда все будет готово, нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="38e92-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="38e92-160"><a name="connect-servers"></a>Подключение серверов toohello шлюза ресурсов</span><span class="sxs-lookup"><span data-stu-id="38e92-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="38e92-161">В обзоре сервера Azure Analysis Services щелкните **Локальный шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="38e92-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Подключение сервера toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="38e92-163">В **выбрать локальный шлюз данных tooconnect**, выберите ресурс шлюза и нажмите кнопку **подключение шлюза**.</span><span class="sxs-lookup"><span data-stu-id="38e92-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Подключение сервера toogateway ресурсов](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="38e92-165">Если шлюз не отображается в списке hello, сервер не скорее всего, в hello же регионе, что область hello, указанные при регистрации шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="38e92-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="38e92-166">Вот и все.</span><span class="sxs-lookup"><span data-stu-id="38e92-166">That's it.</span></span> <span data-ttu-id="38e92-167">Если требуются tooopen порты или выполнять устранение неполадок будет убедиться, что toocheck out [локального шлюза данных](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="38e92-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38e92-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38e92-168">Next steps</span></span>
* [<span data-ttu-id="38e92-169">Управление службами Analysis Services</span><span class="sxs-lookup"><span data-stu-id="38e92-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="38e92-170">Получение данных из служб Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="38e92-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
