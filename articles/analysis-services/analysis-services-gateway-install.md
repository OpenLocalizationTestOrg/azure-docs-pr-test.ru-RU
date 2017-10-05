---
title: "Установка локального шлюза данных | Документация Майкрософт"
description: "Узнайте, как установить и настроить локальный шлюз данных."
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
ms.openlocfilehash: 6ef296fb98478be9240f0231c8ad39cd2a0af995
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="18eef-103">Установка и настройка локального шлюза данных</span><span class="sxs-lookup"><span data-stu-id="18eef-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="18eef-104">Локальный шлюз данных является обязательным, когда один или несколько серверов Azure Analysis Services в том же регионе подключаются к локальным источникам данных.</span><span class="sxs-lookup"><span data-stu-id="18eef-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in the same region connect to on-premises data sources.</span></span> <span data-ttu-id="18eef-105">Дополнительные сведения о шлюзе см. в разделе [Установка локального шлюза](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="18eef-105">To learn more about the gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18eef-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18eef-106">Prerequisites</span></span>
<span data-ttu-id="18eef-107">**Минимальные требования:**</span><span class="sxs-lookup"><span data-stu-id="18eef-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="18eef-108">.NET Framework 4.5;</span><span class="sxs-lookup"><span data-stu-id="18eef-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="18eef-109">64-разрядная версия Windows 7 / Windows Server 2008 R2 (или более новой версии).</span><span class="sxs-lookup"><span data-stu-id="18eef-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="18eef-110">**Рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="18eef-110">**Recommended:**</span></span>

* <span data-ttu-id="18eef-111">8-ядерный ЦП;</span><span class="sxs-lookup"><span data-stu-id="18eef-111">8 Core CPU</span></span>
* <span data-ttu-id="18eef-112">8 ГБ ОЗУ;</span><span class="sxs-lookup"><span data-stu-id="18eef-112">8 GB Memory</span></span>
* <span data-ttu-id="18eef-113">64-разрядная версия Windows 2012 R2 (или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="18eef-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="18eef-114">**Важные сведения:**</span><span class="sxs-lookup"><span data-stu-id="18eef-114">**Important considerations:**</span></span>

* <span data-ttu-id="18eef-115">Во время установки и регистрации шлюза в Azure выбирается регион по умолчанию для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="18eef-115">During setup, when registering your gateway with Azure, the default region for your subscription is selected.</span></span> <span data-ttu-id="18eef-116">Вы можете выбрать другой регион.</span><span class="sxs-lookup"><span data-stu-id="18eef-116">You can choose a different region.</span></span> <span data-ttu-id="18eef-117">При наличии серверов в нескольких регионах необходимо установить шлюз для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="18eef-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="18eef-118">Шлюз нельзя устанавливать на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="18eef-118">The gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="18eef-119">На одном компьютере можно установить только один шлюз.</span><span class="sxs-lookup"><span data-stu-id="18eef-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="18eef-120">Устанавливайте шлюз на компьютере, который не выключается и не переходит в спящий режим.</span><span class="sxs-lookup"><span data-stu-id="18eef-120">Install the gateway on a computer that remains on and does not go to sleep.</span></span>
* <span data-ttu-id="18eef-121">Не устанавливайте шлюз на компьютере, подключенном к сети с помощью беспроводного соединения.</span><span class="sxs-lookup"><span data-stu-id="18eef-121">Do not install the gateway on a computer wirelessly connected to your network.</span></span> <span data-ttu-id="18eef-122">Это может стать причиной снижения производительности.</span><span class="sxs-lookup"><span data-stu-id="18eef-122">Performance can be diminished.</span></span>


## <span data-ttu-id="18eef-123"><a name="download"></a>Загрузка</span><span class="sxs-lookup"><span data-stu-id="18eef-123"><a name="download"></a>Download</span></span>
 <span data-ttu-id="18eef-124">[Скачайте шлюз](https://aka.ms/azureasgateway).</span><span class="sxs-lookup"><span data-stu-id="18eef-124">[Download the gateway](https://aka.ms/azureasgateway)</span></span>

## <span data-ttu-id="18eef-125"><a name="install"></a>Установка</span><span class="sxs-lookup"><span data-stu-id="18eef-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="18eef-126">Запустите программу установки.</span><span class="sxs-lookup"><span data-stu-id="18eef-126">Run setup.</span></span>

2. <span data-ttu-id="18eef-127">Выберите расположение, примите условия соглашения и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="18eef-127">Select a location, accept the terms, and then click **Install**.</span></span>

   ![Расположение для установки и условия лицензии](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="18eef-129">Установите флажок **On-premises data gateway (recommended)** (Локальный шлюз данных (рекомендуется)).</span><span class="sxs-lookup"><span data-stu-id="18eef-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="18eef-130">Azure Analysis Services не поддерживает личный режим.</span><span class="sxs-lookup"><span data-stu-id="18eef-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Выбор типа шлюза](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="18eef-132">Введите данные учетной записи для входа в Azure.</span><span class="sxs-lookup"><span data-stu-id="18eef-132">Enter an account to sign in to Azure.</span></span> <span data-ttu-id="18eef-133">Учетная запись должна быть у вашего Azure Active Directory клиента.</span><span class="sxs-lookup"><span data-stu-id="18eef-133">The account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="18eef-134">Эта учетная запись используется для администратора шлюза.</span><span class="sxs-lookup"><span data-stu-id="18eef-134">This account is used for the gateway administrator.</span></span> 

   ![Введение данных учетной записи для входа в Azure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="18eef-136">При входе с использованием учетной записи домена она будет сопоставлена с учетной записью организации в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18eef-136">If you sign in with a domain account, it will be mapped to your organizational account in Azure AD.</span></span> <span data-ttu-id="18eef-137">Учетная запись вашей организации будет использоваться как администратор шлюза.</span><span class="sxs-lookup"><span data-stu-id="18eef-137">Your organizational account will be used as the the gateway administrator.</span></span>

## <span data-ttu-id="18eef-138"><a name="register"></a>Регистрация</span><span class="sxs-lookup"><span data-stu-id="18eef-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="18eef-139">Чтобы создать ресурс шлюза в Azure, необходимо зарегистрировать локальный экземпляр, установленный с помощью облачной службы шлюза.</span><span class="sxs-lookup"><span data-stu-id="18eef-139">In order to create a gateway resource in Azure, you must register the local instance you installed with the Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="18eef-140">Выберите **Регистрация нового шлюза на этом компьютере**.</span><span class="sxs-lookup"><span data-stu-id="18eef-140">Select **Register a new gateway on this computer**.</span></span>

    ![регистрация;](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="18eef-142">Введите имя и ключ восстановления для шлюза.</span><span class="sxs-lookup"><span data-stu-id="18eef-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="18eef-143">По умолчанию шлюз использует регион, установленный по умолчанию для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="18eef-143">By default, the gateway uses your subscription's default region.</span></span> <span data-ttu-id="18eef-144">Если вам необходим другой регион, выберите **Смена региона**.</span><span class="sxs-lookup"><span data-stu-id="18eef-144">If you need to select a different region, select **Change Region**.</span></span>

   ![регистрация;](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="18eef-146"><a name="create-resource"></a>Создание ресурса шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="18eef-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="18eef-147">После установки и регистрации шлюза необходимо создать ресурс шлюза в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="18eef-147">After you've installed and registered your gateway, you need to create a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="18eef-148">Войдите в Azure с помощью учетной записи, использованной при регистрации шлюза.</span><span class="sxs-lookup"><span data-stu-id="18eef-148">Sign in to Azure with the same account you used when registering the gateway.</span></span>

1. <span data-ttu-id="18eef-149">На портале Azure щелкните **Create a new service** (Создать службу) > **Enterprise Integration** (Интеграция Enterprise) > **Локальный шлюз данных** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="18eef-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Создание ресурса шлюза](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="18eef-151">В разделе **Create connection gateway** (Создать шлюз для подключения) введите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="18eef-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="18eef-152">**Имя.** Введите имя для вашего ресурса шлюза.</span><span class="sxs-lookup"><span data-stu-id="18eef-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="18eef-153">**Подписка.** Выберите подписку Azure, связанную с вашим ресурсом шлюза.</span><span class="sxs-lookup"><span data-stu-id="18eef-153">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="18eef-154">Это должна быть используемая для серверов подписка.</span><span class="sxs-lookup"><span data-stu-id="18eef-154">This subscription should be the same subscription your servers are in.</span></span>
   
      <span data-ttu-id="18eef-155">Подписка по умолчанию основана на учетной записи Azure, которая использовалась для входа.</span><span class="sxs-lookup"><span data-stu-id="18eef-155">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="18eef-156">**Группа ресурсов.** Создайте группу ресурсов Azure или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="18eef-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="18eef-157">**Местоположение.** Выберите регион, в котором зарегистрирован шлюз.</span><span class="sxs-lookup"><span data-stu-id="18eef-157">**Location**: Select the region you registered your gateway in.</span></span>

    * <span data-ttu-id="18eef-158">**Имя установки.** Если установка шлюза еще не выбрана, выберите зарегистрированный ранее шлюз.</span><span class="sxs-lookup"><span data-stu-id="18eef-158">**Installation Name**: If your gateway installation isn't already selected, select the gateway registered.</span></span> 

    <span data-ttu-id="18eef-159">Когда все будет готово, нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="18eef-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="18eef-160"><a name="connect-servers"></a>Подключение серверов к ресурсу шлюза</span><span class="sxs-lookup"><span data-stu-id="18eef-160"><a name="connect-servers"></a>Connect servers to the gateway resource</span></span>

1. <span data-ttu-id="18eef-161">В обзоре сервера Azure Analysis Services щелкните **Локальный шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="18eef-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Подключение сервера к шлюзу](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="18eef-163">В окне **Pick an On-Premises Data Gateway to connect** (Выбрать локальный шлюз данных для подключения) выберите ресурс шлюза и щелкните **Connect selected gateway** (Подключить выбранный шлюз).</span><span class="sxs-lookup"><span data-stu-id="18eef-163">In **Pick an On-Premises Data Gateway to connect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Подключение сервера к ресурсу шлюза](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="18eef-165">Если шлюз не отображается в списке, сервер, вероятно, находится не в том же районе, что и регионы, указанные при регистрации шлюза.</span><span class="sxs-lookup"><span data-stu-id="18eef-165">If your gateway does not appear in the list, your server is likely not in the same region as the region you specified when registering the gateway.</span></span> 

<span data-ttu-id="18eef-166">Вот и все.</span><span class="sxs-lookup"><span data-stu-id="18eef-166">That's it.</span></span> <span data-ttu-id="18eef-167">Если необходимо открывать порты или устранять неполадки, требуется извлечь [локальный шлюз данных](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="18eef-167">If you need to open ports or do any troubleshooting, be sure to check out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18eef-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18eef-168">Next steps</span></span>
* [<span data-ttu-id="18eef-169">Управление службами Analysis Services</span><span class="sxs-lookup"><span data-stu-id="18eef-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="18eef-170">Получение данных из служб Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="18eef-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
