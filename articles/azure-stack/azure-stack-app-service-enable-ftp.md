---
title: "aaaEnable FTP в службе приложений Azure стек | Документы Microsoft"
description: "Действия toocomplete tooenable FTP в службе приложений Azure стеке"
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
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9c02da6362085fdd9f8d285da04efe85cf352398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a><span data-ttu-id="d50ef-103">Включение FTP в службе приложений в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d50ef-103">Enable FTP in App Service on Azure Stack</span></span>

<span data-ttu-id="d50ef-104">После успешного развертывания службы приложений Azure стек при желании публикации tooenable FTP, чтобы клиенты можно отправить свои файлы приложения и содержимого, существуют некоторые дополнительные действия, требующие toobe завершена.</span><span class="sxs-lookup"><span data-stu-id="d50ef-104">Once you have successfully deployed App Service on Azure Stack if you wish tooenable FTP publishing, so that your tenants can upload their application files and content, there are some additional steps that need toobe completed.</span></span>  <span data-ttu-id="d50ef-105">В будущих выпусках эти действия будут выполняться автоматически.</span><span class="sxs-lookup"><span data-stu-id="d50ef-105">In future releases these steps will be automated.</span></span>

> [!NOTE]
> <span data-ttu-id="d50ef-106">Эти шаги должен выполнить администратор службы или предприятия, чтобы настроить службу приложения в поставщике ресурсов Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d50ef-106">These steps are for Service or Enterprise Administrators configuring an App Service on Azure Stack Resource Provider.</span></span>

## <a name="enable-ftp"></a><span data-ttu-id="d50ef-107">Включение FTP</span><span class="sxs-lookup"><span data-stu-id="d50ef-107">Enable FTP</span></span>

1.  <span data-ttu-id="d50ef-108">Войдите в портал Azure стека toohello под Здравствуйте, администратор службы.</span><span class="sxs-lookup"><span data-stu-id="d50ef-108">Log in toohello Azure Stack portal as hello service administrator.</span></span>
2.  <span data-ttu-id="d50ef-109">Обзор слишком**сетевых интерфейсов** и выберите hello **FTP-NIC** под **группы ресурсов** - **AppService локальной**.</span><span class="sxs-lookup"><span data-stu-id="d50ef-109">Browse too**Network interfaces** and select hello **FTP-NIC** under **Resource Group** - **AppService-LOCAL**.</span></span> <span data-ttu-id="d50ef-110">![Сетевые интерфейсы Azure Stack][1]</span><span class="sxs-lookup"><span data-stu-id="d50ef-110">![Azure Stack Network Interfaces][1]</span></span>
3.  <span data-ttu-id="d50ef-111">Примечание hello **общедоступный IP-адрес** из hello **FTP-NIC**.</span><span class="sxs-lookup"><span data-stu-id="d50ef-111">Note hello **Public IP Address** of hello **FTP-NIC**.</span></span> 
<span data-ttu-id="d50ef-112">![Сведения о сетевом интерфейсе Azure Stack][2]</span><span class="sxs-lookup"><span data-stu-id="d50ef-112">![Azure Stack Network Interface Details][2]</span></span>
4.  <span data-ttu-id="d50ef-113">Затем найдите слишком**виртуальные машины** и выберите hello **FTP0 ВМ**.</span><span class="sxs-lookup"><span data-stu-id="d50ef-113">Next Browse too**Virtual Machines** and select hello **FTP0-VM**.</span></span> <span data-ttu-id="d50ef-114">![Виртуальные машины Azure Stack][3]</span><span class="sxs-lookup"><span data-stu-id="d50ef-114">![Azure Stack Virtual Machines][3]</span></span>
5.  <span data-ttu-id="d50ef-115">Откройте сеанс удаленного рабочего стола toohello виртуальной Машины с помощью hello **Connect** сеанса toohello кнопки и входа в систему с использованием учетных данных администратора hello, заданным во время развертывания службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d50ef-115">Open a remote desktop session toohello VM using hello **Connect** button and login toohello session using hello Administrator credentials you set during App Service deployment.</span></span>  
<span data-ttu-id="d50ef-116">![Сведения о виртуальных машинах Azure Stack][4]</span><span class="sxs-lookup"><span data-stu-id="d50ef-116">![Azure Stack Virtual Machine Details][4]</span></span>
6.  <span data-ttu-id="d50ef-117">Откройте **Диспетчер Internet Information Service (IIS)** на hello FTP виртуальной Машины (VM для FTP0).</span><span class="sxs-lookup"><span data-stu-id="d50ef-117">Open **Internet Information Service (IIS) Manager** on hello FTP VM (FTP0-VM).</span></span>
7.  <span data-ttu-id="d50ef-118">В разделе **Sites** (Узлы) выберите **Hosting FTP Site** (Размещение узла FTP).</span><span class="sxs-lookup"><span data-stu-id="d50ef-118">Under **Sites** select **Hosting FTP Site**.</span></span>
8.  <span data-ttu-id="d50ef-119">Щелкните **FTP Firewall Support** (Поддержка брандмауэра FTP).</span><span class="sxs-lookup"><span data-stu-id="d50ef-119">Open **FTP Firewall Support**.</span></span> <span data-ttu-id="d50ef-120">![Диспетчер служб IIS на виртуальной машине FTP0-VM][5]</span><span class="sxs-lookup"><span data-stu-id="d50ef-120">![IIS Manager on App Service FTP0-VM][5]</span></span>
9.  <span data-ttu-id="d50ef-121">Введите hello общедоступный IP-адрес FTP-NIC hello и нажмите кнопку **применить** ![поддержка брандмауэра FTP диспетчера IIS][6]</span><span class="sxs-lookup"><span data-stu-id="d50ef-121">Enter hello Public IP Address of hello FTP-NIC and click **Apply** ![IIS Manager FTP Firewall Support][6]</span></span>

## <a name="validate-hello-enabling-of-ftp"></a><span data-ttu-id="d50ef-122">Проверка включения hello FTP</span><span class="sxs-lookup"><span data-stu-id="d50ef-122">Validate hello enabling of FTP</span></span>

1.  <span data-ttu-id="d50ef-123">Войдите в toohello портала Azure стека либо hello администратором службы или клиента.</span><span class="sxs-lookup"><span data-stu-id="d50ef-123">Log in toohello Azure Stack portal as either hello service administrator or as a tenant.</span></span>
2.  <span data-ttu-id="d50ef-124">Обзор слишком**службы приложений** и выберите Web, мобильных или создания приложения API.</span><span class="sxs-lookup"><span data-stu-id="d50ef-124">Browse too**App Services** and select a Web, Mobile, or API App you have created.</span></span> <span data-ttu-id="d50ef-125">![Службы приложений][7]</span><span class="sxs-lookup"><span data-stu-id="d50ef-125">![App Services][7]</span></span>
3.  <span data-ttu-id="d50ef-126">В приложении hello сведения Обратите внимание hello **имя узла FTP** и **имя пользователя FTP или развертывание**.</span><span class="sxs-lookup"><span data-stu-id="d50ef-126">In hello application details note hello **FTP Hostname** and **FTP/deployment username**.</span></span> <span data-ttu-id="d50ef-127">![Сведения о приложении службы приложений][8]</span><span class="sxs-lookup"><span data-stu-id="d50ef-127">![App Service App Details][8]</span></span>
> [!NOTE]
> <span data-ttu-id="d50ef-128">Если вы не видите запись под **имя пользователя FTP или развертывание**, необходимо иметь учетные данные развертывания tooset hello предварительного использования hello **учетные данные развертывания** колонку.</span><span class="sxs-lookup"><span data-stu-id="d50ef-128">If you do not see an entry under **FTP/deployment username**, you need tooset hello Deployment credentials first using hello **Deployment Credentials** Blade.</span></span>

4.  <span data-ttu-id="d50ef-129">Откройте проводник Windows, введите имя узла hello FTP в файл hello в адресной строке, например ftp://ftp.appservice.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="d50ef-129">Open Windows Explorer, enter hello FTP hostname into hello file address bar for example, ftp://ftp.appservice.azurestack.local</span></span>
5.  <span data-ttu-id="d50ef-130">При появлении запроса введите hello **учетные данные развертывания** записанное на шаге 3, если была включена функция hello вы увидите список каталогов содержимое приложения для hello приложения службы.</span><span class="sxs-lookup"><span data-stu-id="d50ef-130">When prompted enter hello **Deployment credentials** you noted in step 3, if hello feature has been enabled you will see a directory listing of hello app service application's contents.</span></span> <span data-ttu-id="d50ef-131">![Список файлов FTP][9]</span><span class="sxs-lookup"><span data-stu-id="d50ef-131">![FTP File Listing][9]</span></span>
<!--Image references-->
[1]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png
[2]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png
[3]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png
[4]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png
[5]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png
[6]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png
[7]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png
[8]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png
[9]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png
