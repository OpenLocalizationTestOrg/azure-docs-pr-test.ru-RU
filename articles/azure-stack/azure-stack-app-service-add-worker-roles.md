---
title: "aaaScale out рабочих ролей в службы приложений — стек Azure | Документы Microsoft"
description: "Подробные инструкции для масштабирования службы приложений Azure стека"
services: azure-stack
documentationcenter: 
author: kathm
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: kathm
ms.openlocfilehash: 252b4a531655e38f3a3747f8a04b16fc6303f9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a><span data-ttu-id="60fbe-103">Службы приложений Azure стеке: Добавление дополнительных рабочих ролей</span><span class="sxs-lookup"><span data-stu-id="60fbe-103">App Service on Azure Stack: Adding more worker roles</span></span> 

<span data-ttu-id="60fbe-104">Этот документ содержит инструкции о том, как tooscale приложения службы в рабочих ролях Azure стека.</span><span class="sxs-lookup"><span data-stu-id="60fbe-104">This document provides instructions about how tooscale App Service on Azure Stack worker roles.</span></span> <span data-ttu-id="60fbe-105">Он содержит инструкции по созданию дополнительных рабочих ролей toosupport приложений любого размера.</span><span class="sxs-lookup"><span data-stu-id="60fbe-105">It contains steps for creating additional worker roles toosupport applications of any size.</span></span>

> [!NOTE]
> <span data-ttu-id="60fbe-106">Если в вашей среде подтверждения Концепции стек Azure не более 96 ГБ ОЗУ возможно затруднений при добавлении дополнительной емкости.</span><span class="sxs-lookup"><span data-stu-id="60fbe-106">If your Azure Stack POC Environment does not have more than 96-GB RAM you may have difficulties adding additional capacity.</span></span>

<span data-ttu-id="60fbe-107">Службы приложений Azure стеке, по умолчанию поддерживает бесплатных и общих рабочих уровнях.</span><span class="sxs-lookup"><span data-stu-id="60fbe-107">App Service on Azure Stack, by default, supports free and shared worker tiers.</span></span> <span data-ttu-id="60fbe-108">tooadd другие рабочие уровни tooadd требуются дополнительные рабочие роли.</span><span class="sxs-lookup"><span data-stu-id="60fbe-108">tooadd other worker tiers, you need tooadd more worker roles.</span></span>

<span data-ttu-id="60fbe-109">Если вы не уверены, что было развернуто приложение службы по умолчанию hello в установке стек Azure, можно просмотреть дополнительные сведения в hello [службы приложений на обзор Azure стека](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60fbe-109">If you are not sure what was deployed with hello default App Service on Azure Stack installation, you can review additional information in hello [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>

<span data-ttu-id="60fbe-110">Существует два способа tooadd дополнительную емкость tooApp службы стек Azure:</span><span class="sxs-lookup"><span data-stu-id="60fbe-110">There are two ways tooadd additional capacity tooApp Service on Azure Stack:</span></span>
1.  <span data-ttu-id="60fbe-111">[Добавьте дополнительные рабочие процессы непосредственно из с внутри hello администратора поставщика ресурсов службы приложения](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span><span class="sxs-lookup"><span data-stu-id="60fbe-111">[Add additional workers directly from with within hello App Service Resource Provider Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span></span>
2.  <span data-ttu-id="60fbe-112">[Вручную создайте дополнительные виртуальные машины и добавьте их toohello поставщик ресурсов службы приложения](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span><span class="sxs-lookup"><span data-stu-id="60fbe-112">[Create additional VMs manually and add them toohello App Service Resource Provider](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span></span>

## <a name="add-additional-workers-directly-within-hello-app-service-resource-provider-admin"></a><span data-ttu-id="60fbe-113">Добавьте дополнительные рабочие процессы непосредственно в hello администратора поставщика ресурсов службы приложения.</span><span class="sxs-lookup"><span data-stu-id="60fbe-113">Add additional workers directly within hello App Service Resource Provider Admin.</span></span>

1.  <span data-ttu-id="60fbe-114">Войдите в систему toohello портала Azure стека как Здравствуйте, администратор службы;</span><span class="sxs-lookup"><span data-stu-id="60fbe-114">Log in toohello Azure Stack portal as hello service administrator;</span></span>
2.  <span data-ttu-id="60fbe-115">Обзор слишком**поставщиков ресурсов** и выберите hello **администратора поставщика ресурсов службы приложения**. ![Поставщики ресурсов стек Azure][1]</span><span class="sxs-lookup"><span data-stu-id="60fbe-115">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**. ![Azure Stack Resource Providers][1]</span></span>
3.  <span data-ttu-id="60fbe-116">Щелкните **Роли**.</span><span class="sxs-lookup"><span data-stu-id="60fbe-116">Click **Roles**.</span></span>  <span data-ttu-id="60fbe-117">Здесь можно просматривать разбивку hello развертывания роли приложения службы.</span><span class="sxs-lookup"><span data-stu-id="60fbe-117">Here you see hello breakdown of all App Service roles deployed.</span></span>
4.  <span data-ttu-id="60fbe-118">Выберите вариант hello **новый экземпляр роли** ![добавить новый экземпляр роли][2]</span><span class="sxs-lookup"><span data-stu-id="60fbe-118">Click hello option **New Role Instance** ![Add new role instance][2]</span></span>
5.  <span data-ttu-id="60fbe-119">В hello **новый экземпляр роли** колонки:</span><span class="sxs-lookup"><span data-stu-id="60fbe-119">In hello **New Role Instance** blade:</span></span>
    1. <span data-ttu-id="60fbe-120">Выберите количество дополнительных **экземпляры роли** хотелось бы tooadd.</span><span class="sxs-lookup"><span data-stu-id="60fbe-120">Choose how many additional **role instances** you would like tooadd.</span></span>  <span data-ttu-id="60fbe-121">В режиме предварительного просмотра hello не более 10.</span><span class="sxs-lookup"><span data-stu-id="60fbe-121">In hello preview, there is a maximum of 10.</span></span>
    2. <span data-ttu-id="60fbe-122">Выберите hello **тип роли**.</span><span class="sxs-lookup"><span data-stu-id="60fbe-122">Select hello **role type**.</span></span>  <span data-ttu-id="60fbe-123">В этой предварительной версии этот параметр является ограниченной tooWeb работника.</span><span class="sxs-lookup"><span data-stu-id="60fbe-123">In this preview, this option is limited tooWeb Worker.</span></span>
    3. <span data-ttu-id="60fbe-124">Выберите hello **рабочий уровень** хотелось бы toodeploy этот рабочий процесс, по умолчанию доступны: малый, средний, большой или Shared.</span><span class="sxs-lookup"><span data-stu-id="60fbe-124">Select hello **worker tier** you would like toodeploy this worker into, default choices are Small, Medium, Large, or Shared.</span></span>  <span data-ttu-id="60fbe-125">Если вы создали собственные рабочие уровни, ваш рабочий уровень также доступны для выбора.</span><span class="sxs-lookup"><span data-stu-id="60fbe-125">If, you have created your own worker tiers, your worker tiers will also be available for selection.</span></span>
    4. <span data-ttu-id="60fbe-126">Нажмите кнопку **ОК** toodeploy hello дополнительных рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="60fbe-126">Click **OK** toodeploy hello additional workers</span></span>
6.  <span data-ttu-id="60fbe-127">Службы приложений на стек Azure будет добавлен hello дополнительных виртуальных машин, их настройки, установить программное обеспечение для необходимых hello и пометить их как готовый после завершения этого процесса.</span><span class="sxs-lookup"><span data-stu-id="60fbe-127">App Service on Azure Stack will now add hello additional VMs, configure them, install all hello required software and mark them as ready when this process is complete.</span></span>  <span data-ttu-id="60fbe-128">Этот процесс может занять около 80 минут.</span><span class="sxs-lookup"><span data-stu-id="60fbe-128">This process can take approximately 80 minutes.</span></span>
7.  <span data-ttu-id="60fbe-129">Можно следить за ходом hello hello готовности hello новых работников, просмотрев hello работников в hello **ролей** колонку.</span><span class="sxs-lookup"><span data-stu-id="60fbe-129">You can monitor hello progress of hello readiness of hello new workers by viewing hello workers in hello **roles** blade.</span></span>

>[!NOTE]
>  <span data-ttu-id="60fbe-130">В этой предварительной версии hello интеграции новый экземпляр роли поток является ограниченной tooWorker ролей и развертывать виртуальные машины только размера A1.</span><span class="sxs-lookup"><span data-stu-id="60fbe-130">In this preview, hello integrated New Role Instance flow is limited tooWorker Roles and deploy VMs of size A1 only.</span></span>  <span data-ttu-id="60fbe-131">Мы будет расширение эту возможность в будущем выпуске.</span><span class="sxs-lookup"><span data-stu-id="60fbe-131">We will be expanding this capability in a future release.</span></span>

## <a name="manually-adding-additional-capacity-tooapp-service-on-azure-stack"></a><span data-ttu-id="60fbe-132">Вручную добавлять дополнительную емкость tooApp службы Azure стек.</span><span class="sxs-lookup"><span data-stu-id="60fbe-132">Manually adding additional capacity tooApp Service on Azure Stack.</span></span>

<span data-ttu-id="60fbe-133">Hello следующие шаги, необходимые tooadd дополнительные роли:</span><span class="sxs-lookup"><span data-stu-id="60fbe-133">hello following steps are required tooadd additional roles:</span></span>

1. [<span data-ttu-id="60fbe-134">Создание новой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="60fbe-134">Create a new virtual machine</span></span>](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [<span data-ttu-id="60fbe-135">Настройка виртуальной машины hello</span><span class="sxs-lookup"><span data-stu-id="60fbe-135">Configure hello virtual machine</span></span>](#step-2-configure-the-virtual-machine)
3. [<span data-ttu-id="60fbe-136">Настройка рабочей роли web hello на портале Azure стека hello</span><span class="sxs-lookup"><span data-stu-id="60fbe-136">Configure hello web worker role in hello Azure Stack portal</span></span>](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [<span data-ttu-id="60fbe-137">Настройка планах службы приложений</span><span class="sxs-lookup"><span data-stu-id="60fbe-137">Configure app service plans</span></span>](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-toosupport-hello-new-instance-size"></a><span data-ttu-id="60fbe-138">Шаг 1: Создание новой виртуальной Машины toosupport hello новый экземпляр размер</span><span class="sxs-lookup"><span data-stu-id="60fbe-138">Step 1: Create a new VM toosupport hello new instance size</span></span>
<span data-ttu-id="60fbe-139">Создание виртуальной машины, как описано в [в этой статье](azure-stack-provision-vm.md), обеспечивая следующих hello выбор производится:</span><span class="sxs-lookup"><span data-stu-id="60fbe-139">Create a virtual machine as described in [this article](azure-stack-provision-vm.md), ensuring that hello following selections are made:</span></span>

* <span data-ttu-id="60fbe-140">Имя пользователя и пароль: укажите hello же имя пользователя и пароль, предоставленные при установке службы приложений Azure стек.</span><span class="sxs-lookup"><span data-stu-id="60fbe-140">User name and password: Provide hello same user name and password you provided when you installed App Service on Azure Stack.</span></span>
* <span data-ttu-id="60fbe-141">Подписка: Используйте подписки поставщика по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="60fbe-141">Subscription: Use hello default provider subscription.</span></span>
* <span data-ttu-id="60fbe-142">Группа ресурсов: выберите **AppService локальной**.</span><span class="sxs-lookup"><span data-stu-id="60fbe-142">Resource group: Choose **AppService-LOCAL**.</span></span>

> [!NOTE]
> <span data-ttu-id="60fbe-143">Сохранение виртуальных машин hello для рабочих ролей в hello же группе ресурсов службы приложений Azure стек развертывается.</span><span class="sxs-lookup"><span data-stu-id="60fbe-143">Store hello virtual machines for worker roles in hello same resource group as App Service on Azure Stack is deployed to.</span></span> <span data-ttu-id="60fbe-144">(Это рекомендуется для этой версии.)</span><span class="sxs-lookup"><span data-stu-id="60fbe-144">(This is recommended for this release.)</span></span>
> 
> 

## <a name="step-2-configure-hello-virtual-machine"></a><span data-ttu-id="60fbe-145">Шаг 2: Настройка hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="60fbe-145">Step 2: Configure hello Virtual Machine</span></span>
<span data-ttu-id="60fbe-146">После завершения развертывания hello hello следующая конфигурация является обязательным toosupport hello web рабочей роли:</span><span class="sxs-lookup"><span data-stu-id="60fbe-146">Once hello deployment has completed, hello following configuration is required toosupport hello web worker role:</span></span>

1. <span data-ttu-id="60fbe-147">Обзор toohello **AppService локальной** группы ресурсов в портал hello и выберите hello новой машины, созданной на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="60fbe-147">Browse toohello **AppService-LOCAL** resource group in hello portal and select hello new machine you created in Step 1.</span></span>
2. <span data-ttu-id="60fbe-148">Щелкните "Подключить" в hello профиль виртуальной Машины колонке toodownload hello удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="60fbe-148">Click connect in hello VM blade toodownload hello remote desktop profile.</span></span>  <span data-ttu-id="60fbe-149">Откройте профиль hello tooopen tooyour сеанс удаленного рабочего стола виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60fbe-149">Open hello profile tooopen a remote desktop session tooyour VM.</span></span>
3. <span data-ttu-id="60fbe-150">Войдите в toohello виртуальной Машины с помощью hello имя пользователя и пароль, указанный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="60fbe-150">Log in toohello VM using hello username and password you specified in Step 1.</span></span>
4. <span data-ttu-id="60fbe-151">Откройте PowerShell, щелкнув hello **запустить** кнопку и введите PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60fbe-151">Open PowerShell by clicking hello **Start** button and typing PowerShell.</span></span> <span data-ttu-id="60fbe-152">Щелкните правой кнопкой мыши **PowerShell.exe**и выберите **Запуск от имени администратора** tooopen PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="60fbe-152">Right-click **PowerShell.exe**, and select **Run as administrator** tooopen PowerShell in administrator mode.</span></span>
5. <span data-ttu-id="60fbe-153">Копирование и вставка каждого hello, следующие команды (по одному за раз) в окне PowerShell hello и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="60fbe-153">Copy and paste each of hello following commands (one at a time) into hello PowerShell window, and press enter:</span></span>
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. <span data-ttu-id="60fbe-154">Закройте сеанс удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="60fbe-154">Close your remote desktop session.</span></span>
7. <span data-ttu-id="60fbe-155">Перезапустите hello ВМ с портала hello.</span><span class="sxs-lookup"><span data-stu-id="60fbe-155">Restart hello VM from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="60fbe-156">Это минимальные требования для службы приложений Azure стек.</span><span class="sxs-lookup"><span data-stu-id="60fbe-156">These are minimum requirements for App Service on Azure Stack.</span></span> <span data-ttu-id="60fbe-157">Они являются параметры по умолчанию hello hello образа Windows 2012 R2, входящий в состав Azure стека.</span><span class="sxs-lookup"><span data-stu-id="60fbe-157">They are hello default settings of hello Windows 2012 R2 image included with Azure Stack.</span></span> <span data-ttu-id="60fbe-158">инструкции Hello были предоставлены для дальнейшего использования, а также для тех, кто использовать другое изображение.</span><span class="sxs-lookup"><span data-stu-id="60fbe-158">hello instructions have been provided for future reference, and for those using a different image.</span></span>
> 
> 

## <a name="step-3-configure-hello-worker-role-in-hello-azure-stack-portal"></a><span data-ttu-id="60fbe-159">Шаг 3: Настройка hello рабочей роли на портале Azure стека hello</span><span class="sxs-lookup"><span data-stu-id="60fbe-159">Step 3: Configure hello worker role in hello Azure Stack portal</span></span>
1. <span data-ttu-id="60fbe-160">Привет открыть портал администратора службы hello на **ClientVM**.</span><span class="sxs-lookup"><span data-stu-id="60fbe-160">Open hello portal as hello service administrator on **ClientVM**.</span></span>
2. <span data-ttu-id="60fbe-161">Перейдите в слишком**поставщиков ресурсов** &gt; **администратора поставщика ресурсов службы приложения**.![ Администратор поставщика ресурсов службы приложений][3]</span><span class="sxs-lookup"><span data-stu-id="60fbe-161">Navigate too**Resource Providers** &gt; **App Service Resource Provider Admin**.![App Service Resource Provider Admin][3]</span></span>
3. <span data-ttu-id="60fbe-162">В колонке параметров hello щелкните **ролей**.![ Службы приложений ресурсов поставщика ролей][4]</span><span class="sxs-lookup"><span data-stu-id="60fbe-162">In hello settings blade, click **Roles**.![App Service Resource Provider Roles][4]</span></span>
4. <span data-ttu-id="60fbe-163">Нажмите кнопку **добавить экземпляр роли**.</span><span class="sxs-lookup"><span data-stu-id="60fbe-163">Click **Add Role Instance**.</span></span>
5. <span data-ttu-id="60fbe-164">В текстовом поле hello для **имя сервера** введите hello **IP-адрес** сервера hello, созданной ранее (на раздел 1).</span><span class="sxs-lookup"><span data-stu-id="60fbe-164">In hello textbox for **Server Name** enter hello **IP Address** of hello server you created earlier (in Section 1).</span></span>
6. <span data-ttu-id="60fbe-165">Выберите hello **тип роли** хотелось бы tooadd - контроллер, сервер управления, внешнего интерфейса, рабочего веб-процесса, издателя или файловый сервер.</span><span class="sxs-lookup"><span data-stu-id="60fbe-165">Select hello **Role Type** you would like tooadd - Controller, Management Server, Front End, Web Worker, Publisher, or File Server.</span></span>  <span data-ttu-id="60fbe-166">В этом случае выберите рабочего веб-процесса.</span><span class="sxs-lookup"><span data-stu-id="60fbe-166">In this instance, select Web Worker.</span></span>
7. <span data-ttu-id="60fbe-167">Нажмите кнопку hello **уровня** вы бы как toodeploy hello нового экземпляра слишком (небольшой, средний, большой или общего).</span><span class="sxs-lookup"><span data-stu-id="60fbe-167">Click hello **Tier** you would like toodeploy hello new instance too(small, medium, large, or shared).</span></span>  <span data-ttu-id="60fbe-168">Если вы создали собственные рабочие уровни они будут также доступны для выбора.</span><span class="sxs-lookup"><span data-stu-id="60fbe-168">If you have created your own worker tiers these will also be available for selection.</span></span>
8. <span data-ttu-id="60fbe-169">Нажмите кнопку **ОК.**</span><span class="sxs-lookup"><span data-stu-id="60fbe-169">Click **OK.**</span></span>
9. <span data-ttu-id="60fbe-170">Вернитесь к предыдущему окну toohello **ролей** представление</span><span class="sxs-lookup"><span data-stu-id="60fbe-170">Go back toohello **Roles** view</span></span>
10. <span data-ttu-id="60fbe-171">Щелкните toohello роли сочетания типа и рабочий уровень, назначенный на виртуальной Машине для соответствующей строки hello.</span><span class="sxs-lookup"><span data-stu-id="60fbe-171">Click hello row corresponding toohello Role Type and Worker Tier combination you assigned your VM to.</span></span>
11. <span data-ttu-id="60fbe-172">Найдите hello только что добавленное имя сервера.</span><span class="sxs-lookup"><span data-stu-id="60fbe-172">Look for hello Server Name you just added.</span></span> <span data-ttu-id="60fbe-173">Просмотрите столбец состояния hello и дождитесь toomove toohello следующий шаг hello состояние «Готово».</span><span class="sxs-lookup"><span data-stu-id="60fbe-173">Review hello status column, and wait toomove toohello next step until hello status is "Ready."</span></span> <span data-ttu-id="60fbe-174">Это может занять около 80 минут.</span><span class="sxs-lookup"><span data-stu-id="60fbe-174">This can take approximately 80 minutes.</span></span> <span data-ttu-id="60fbe-175">![Все готово для роли поставщика ресурсов службы приложений][5]</span><span class="sxs-lookup"><span data-stu-id="60fbe-175">![App Service Resource Provider Role Ready][5]</span></span>

## <a name="step-4-configure-app-service-plans"></a><span data-ttu-id="60fbe-176">Шаг 4: Настройка планах службы приложений</span><span class="sxs-lookup"><span data-stu-id="60fbe-176">Step 4: Configure app service plans</span></span>

1. <span data-ttu-id="60fbe-177">Войдите в портал toohello на hello ClientVM.</span><span class="sxs-lookup"><span data-stu-id="60fbe-177">Sign in toohello portal on hello ClientVM.</span></span>
2. <span data-ttu-id="60fbe-178">Перейдите в слишком**New** &gt; **мобильных и веб-**.</span><span class="sxs-lookup"><span data-stu-id="60fbe-178">Navigate too**New** &gt; **Web and Mobile**.</span></span>
3. <span data-ttu-id="60fbe-179">Выберите тип hello приложения хотелось бы toodeploy.</span><span class="sxs-lookup"><span data-stu-id="60fbe-179">Select hello type of application you would like toodeploy.</span></span>
4. <span data-ttu-id="60fbe-180">Укажите сведения hello для приложения hello, а затем выберите **план служб приложений или расположение**.</span><span class="sxs-lookup"><span data-stu-id="60fbe-180">Provide hello information for hello application, and then select **AppService Plan / Location**.</span></span>
    1. <span data-ttu-id="60fbe-181">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="60fbe-181">Click **Create New**.</span></span>
    2. <span data-ttu-id="60fbe-182">Создайте план, выбрав соответствующий hello ценовую категорию для плана hello.</span><span class="sxs-lookup"><span data-stu-id="60fbe-182">Create your plan, selecting hello corresponding pricing tier for hello plan.</span></span>

> [!NOTE]
> <span data-ttu-id="60fbe-183">Можно создать несколько планов, хотя в этой колонке.</span><span class="sxs-lookup"><span data-stu-id="60fbe-183">You can create multiple plans while on this blade.</span></span> <span data-ttu-id="60fbe-184">Перед развертыванием, тем не менее, убедитесь, что выбран подходящий план hello.</span><span class="sxs-lookup"><span data-stu-id="60fbe-184">Before you deploy, however, ensure you have selected hello appropriate plan.</span></span>
> 
> 

<span data-ttu-id="60fbe-185">Hello ниже показан пример hello доступны несколько ценовые категории по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="60fbe-185">hello following shows an example of hello multiple pricing tiers available by default.</span></span>  <span data-ttu-id="60fbe-186">Вы Обратите внимание, если нет доступных рабочих процессов для определенного рабочий уровень, hello параметр toochoose hello соответствующий Ценовая категория недоступна.</span><span class="sxs-lookup"><span data-stu-id="60fbe-186">You notice that if there are no available workers for a particular worker tier, hello option toochoose hello corresponding pricing tier is unavailable.</span></span>![Служба приложений Azure стека по умолчанию ценовые категории][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: ./media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png
