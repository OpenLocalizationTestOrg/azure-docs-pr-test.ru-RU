---
title: "Подключиться к стек Azure | Документы Microsoft"
description: "Сведения о подключении стек Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3cebbfa6-819a-41e3-9f1b-14ca0a2aaba3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: sngun
ms.openlocfilehash: 914f2e5d10aa341cea5eba8c24c7c37610e6b626
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="connect-to-azure-stack"></a><span data-ttu-id="8eb8d-103">Подключение к Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8eb8d-103">Connect to Azure Stack</span></span>

<span data-ttu-id="8eb8d-104">Для управления ресурсами, необходимо подключиться к набору разработки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-104">To manage resources, you must connect to the Azure Stack Development Kit.</span></span> <span data-ttu-id="8eb8d-105">В этом разделе описаны действия, требуемые для подключения к набору разработки.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-105">This topic details the steps required to connect to the development kit.</span></span> <span data-ttu-id="8eb8d-106">Можно использовать любой из следующих параметров подключения:</span><span class="sxs-lookup"><span data-stu-id="8eb8d-106">You can use either of the following connection options:</span></span>

* <span data-ttu-id="8eb8d-107">[Удаленный рабочий стол](#connect-with-remote-desktop): позволяет быстро выполнить подключение из пакета средств разработки единого параллельных пользователю.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the development kit.</span></span>
* <span data-ttu-id="8eb8d-108">[Виртуальную частную сеть (VPN)](#connect-with-vpn): позволяет несколько одновременных пользователей подключения от клиентов за пределами Azure стека инфраструктуры (требует настройки).</span><span class="sxs-lookup"><span data-stu-id="8eb8d-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-to-azure-stack-with-remote-desktop"></a><span data-ttu-id="8eb8d-109">Подключиться к Azure стека с помощью удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="8eb8d-109">Connect to Azure Stack with Remote Desktop</span></span>
<span data-ttu-id="8eb8d-110">К удаленному рабочему столу параллельных однопользовательском позволяет работать с портала управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-110">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span></span>

1. <span data-ttu-id="8eb8d-111">Откройте подключение к удаленному рабочему столу и подключитесь к набору разработки.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-111">Open a Remote Desktop Connection and connect to the development kit.</span></span> <span data-ttu-id="8eb8d-112">Введите **AzureStack\AzureStackAdmin** как имя пользователя и пароль администратора, указанный во время настройки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-112">Enter **AzureStack\AzureStackAdmin** as the username, and the administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="8eb8d-113">С компьютера разработки пакета, откройте диспетчер сервера, щелкните **локального сервера**, отключите усиленной безопасности Internet Explorer, а затем закройте диспетчер сервера.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-113">From the development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="8eb8d-114">Чтобы открыть портал, перейдите к (https://portal.local.azurestack.external/) и выполните вход с помощью учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-114">To open the  portal, navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span></span>


## <a name="connect-to-azure-stack-with-vpn"></a><span data-ttu-id="8eb8d-115">Подключиться к Azure стека с помощью VPN</span><span class="sxs-lookup"><span data-stu-id="8eb8d-115">Connect to Azure Stack with VPN</span></span>

<span data-ttu-id="8eb8d-116">Туннель разбиение подключения виртуальной частной сети (VPN) для пакета средств разработки Azure стека можно создать.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-116">You can establish a split tunnel Virtual Private Network (VPN) connection to an Azure Stack Development Kit.</span></span> <span data-ttu-id="8eb8d-117">Через подключение VPN доступа к порталу администратора пользовательского портала и локально установлены средства, такие как Visual Studio и PowerShell для управления ресурсами Azure стека.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-117">Through the VPN connection, you can access the administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span></span> <span data-ttu-id="8eb8d-118">В обоих Directory(AAD) Active Azure поддерживается VPN-подключение и Services(AD FS) федерации Active Directory на основе развертываний.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-118">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="8eb8d-119">VPN-подключений включить нескольких клиентов для подключения к Azure стека, в то же время.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-119">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="8eb8d-120">Это VPN-подключение не поддерживает возможность подключения к инфраструктуре Azure стека виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-120">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="8eb8d-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8eb8d-121">Prerequisites</span></span>

* <span data-ttu-id="8eb8d-122">Установка [совместимый Azure PowerShell Azure стека](azure-stack-powershell-install.md) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-122">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="8eb8d-123">Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="8eb8d-123">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="8eb8d-124">Настройка подключения VPN</span><span class="sxs-lookup"><span data-stu-id="8eb8d-124">Configure VPN connectivity</span></span>

<span data-ttu-id="8eb8d-125">Чтобы создать VPN-подключение к набору разработки, откройте сеанс PowerShell с повышенными привилегиями на локальном компьютере под управлением Windows и выполните следующий скрипт (Убедитесь, что для обновления значения IP адрес и пароль для вашей среды):</span><span class="sxs-lookup"><span data-stu-id="8eb8d-125">To create a VPN connection to the development kit, open an elevated PowerShell session from your local Windows-based computer and run the following script (make sure to update the the IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import the Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add the development kit computer’s host IP address & certificate authority (CA) to the list of trusted hosts. Make sure to update the the IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for the local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="8eb8d-126">Если настройка выполнена успешно, вы увидите **azurestack** в списке VPN-подключений.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-126">If the set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Сетевые подключения](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a><span data-ttu-id="8eb8d-128">Подключение к Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8eb8d-128">Connect to Azure Stack</span></span>

<span data-ttu-id="8eb8d-129">Подключитесь к экземпляру стек Azure с помощью любого из следующих двух способов:</span><span class="sxs-lookup"><span data-stu-id="8eb8d-129">Connect to the Azure Stack instance by using either of the following two methods:</span></span>  

* <span data-ttu-id="8eb8d-130">С помощью `Connect-AzsVpn ` команды:</span><span class="sxs-lookup"><span data-stu-id="8eb8d-130">By using the `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="8eb8d-131">При появлении запроса доверия стека Azure узла и установить сертификат от **AzureStackCertificateAuthority** в хранилище сертификатов локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-131">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="8eb8d-132">(может появиться запрос позади окна сеанса PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8eb8d-132">(the prompt might appear behind the PowerShell session window).</span></span> 

* <span data-ttu-id="8eb8d-133">Открытие локального компьютера **параметры сети** > **VPN** > щелкните **azurestack** > **подключения**.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-133">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="8eb8d-134">В командной строке входа введите имя пользователя (AzureStack\AzureStackAdmin) и пароль.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-134">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span></span>

### <a name="test-the-vpn-connectivity"></a><span data-ttu-id="8eb8d-135">Проверить подключение к VPN</span><span class="sxs-lookup"><span data-stu-id="8eb8d-135">Test the VPN connectivity</span></span>

<span data-ttu-id="8eb8d-136">Чтобы проверить соединение с портала, откройте браузер и перейдите на портал пользователей (https://portal.local.azurestack.external/), вход и создание ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8eb8d-136">To test the portal connection, open an Internet browser and navigate to the user portal (https://portal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="8eb8d-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8eb8d-137">Next steps</span></span>



