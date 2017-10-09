---
title: "aaaConnect tooAzure стек | Документы Microsoft"
description: "Дополнительные сведения о том, как tooconnect стек Azure"
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
ms.openlocfilehash: 8a940245fbcc8795d26b694df66824f0eb1dc3ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-stack"></a><span data-ttu-id="4d6e9-103">Подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="4d6e9-103">Connect tooAzure Stack</span></span>

<span data-ttu-id="4d6e9-104">ресурсы toomanage toohello пакет средств разработки стек Azure необходимо подключиться.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-104">toomanage resources, you must connect toohello Azure Stack Development Kit.</span></span> <span data-ttu-id="4d6e9-105">Шаги hello сведения этого раздела требуется пакет средств разработки toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-105">This topic details hello steps required tooconnect toohello development kit.</span></span> <span data-ttu-id="4d6e9-106">Можно использовать либо hello следующие варианты подключения:</span><span class="sxs-lookup"><span data-stu-id="4d6e9-106">You can use either of hello following connection options:</span></span>

* <span data-ttu-id="4d6e9-107">[Удаленный рабочий стол](#connect-with-remote-desktop): позволяет быстро выполнить подключение из пакета средств разработки hello один параллельных пользователю.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from hello development kit.</span></span>
* <span data-ttu-id="4d6e9-108">[Виртуальную частную сеть (VPN)](#connect-with-vpn): позволяет несколько одновременных пользователей подключения от клиентов за пределами инфраструктуры Azure стека hello (требует настройки).</span><span class="sxs-lookup"><span data-stu-id="4d6e9-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of hello Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-tooazure-stack-with-remote-desktop"></a><span data-ttu-id="4d6e9-109">Подключение удаленного рабочего стола tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="4d6e9-109">Connect tooAzure Stack with Remote Desktop</span></span>
<span data-ttu-id="4d6e9-110">К удаленному рабочему столу параллельных однопользовательском позволяет работать с портала toomanage ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-110">With a Remote Desktop connection, a single concurrent user can work with hello portal toomanage resources.</span></span>

1. <span data-ttu-id="4d6e9-111">Откройте подключение к удаленному рабочему столу и подключите toohello пакет средств разработки.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-111">Open a Remote Desktop Connection and connect toohello development kit.</span></span> <span data-ttu-id="4d6e9-112">Введите **AzureStack\AzureStackAdmin** как hello имя пользователя и пароль администратора hello, указанный во время настройки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-112">Enter **AzureStack\AzureStackAdmin** as hello username, and hello administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="4d6e9-113">На компьютере комплект средств для разработки hello, откройте диспетчер сервера, нажмите кнопку **локального сервера**, отключите усиленной безопасности Internet Explorer, а затем закройте диспетчер сервера.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-113">From hello development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="4d6e9-114">пользователь hello tooopen [портала](azure-stack-key-features.md#portal), слишком перехода (https://portal.local.azurestack.external/) и выполните вход с использованием учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-114">tooopen hello user [portal](azure-stack-key-features.md#portal), navigate too(https://portal.local.azurestack.external/) and sign in using user credentials.</span></span> <span data-ttu-id="4d6e9-115">Здравствуйте, администратор tooopen [портала](azure-stack-key-features.md#portal), перейдите в слишком (https://adminportal.local.azurestack.external/) и вход с помощью hello Azure Active Directory учетные данные, указанные во время установки.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-115">tooopen hello administrator [portal](azure-stack-key-features.md#portal), navigate too(https://adminportal.local.azurestack.external/) and sign in using hello Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-tooazure-stack-with-vpn"></a><span data-ttu-id="4d6e9-116">Подключение tooAzure стека с помощью VPN</span><span class="sxs-lookup"><span data-stu-id="4d6e9-116">Connect tooAzure Stack with VPN</span></span>

<span data-ttu-id="4d6e9-117">Можно установить разбиение туннель виртуальной частной сети (VPN) подключение tooan пакет средств разработки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-117">You can establish a split tunnel Virtual Private Network (VPN) connection tooan Azure Stack Development Kit.</span></span> <span data-ttu-id="4d6e9-118">Через hello VPN-подключение получить доступ к порталу администрирования hello, пользовательский портал и локально установлены средства, такие как Visual Studio и ресурсы Azure стека toomanage PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-118">Through hello VPN connection, you can access hello administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell toomanage Azure Stack resources.</span></span> <span data-ttu-id="4d6e9-119">В обоих Directory(AAD) Active Azure поддерживается VPN-подключение и Services(AD FS) федерации Active Directory на основе развертываний.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-119">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="4d6e9-120">VPN-подключений включить tooconnect tooAzure несколько клиентов стека в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-120">VPN connections enable multiple clients tooconnect tooAzure Stack at hello same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="4d6e9-121">Это VPN-подключение не поддерживает подключение tooAzure стека инфраструктуры виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-121">This VPN connection does not provide connectivity tooAzure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="4d6e9-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4d6e9-122">Prerequisites</span></span>

* <span data-ttu-id="4d6e9-123">Установка [совместимый Azure PowerShell Azure стека](azure-stack-powershell-install.md) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-123">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="4d6e9-124">Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="4d6e9-124">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="4d6e9-125">Настройка подключения VPN</span><span class="sxs-lookup"><span data-stu-id="4d6e9-125">Configure VPN connectivity</span></span>

<span data-ttu-id="4d6e9-126">toocreate набора разработки toohello подключение VPN, откройте сеанс PowerShell с повышенными привилегиями из локального компьютера под управлением Windows и выполнения hello, выполнив сценарий (Убедитесь, что tooupdate hello hello значения IP-адреса адрес и пароль для вашей среды):</span><span class="sxs-lookup"><span data-stu-id="4d6e9-126">toocreate a VPN connection toohello development kit, open an elevated PowerShell session from your local Windows-based computer and run hello following script (make sure tooupdate hello hello IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import hello Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add hello development kit computer’s host IP address & certificate authority (CA) toohello list of trusted hosts. Make sure tooupdate hello hello IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for hello local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="4d6e9-127">Если настроить hello завершается успешно, вы увидите **azurestack** в списке VPN-подключений.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-127">If hello set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Сетевые подключения](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-tooazure-stack"></a><span data-ttu-id="4d6e9-129">Подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="4d6e9-129">Connect tooAzure Stack</span></span>

<span data-ttu-id="4d6e9-130">Подключения toohello стека Azure экземпляра с помощью любого из следующих двух методов hello:</span><span class="sxs-lookup"><span data-stu-id="4d6e9-130">Connect toohello Azure Stack instance by using either of hello following two methods:</span></span>  

* <span data-ttu-id="4d6e9-131">С помощью hello `Connect-AzsVpn ` команды:</span><span class="sxs-lookup"><span data-stu-id="4d6e9-131">By using hello `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="4d6e9-132">При появлении запроса доверия hello Azure стека узла и установить сертификат hello от **AzureStackCertificateAuthority** в хранилище сертификатов локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-132">When prompted, trust hello Azure Stack host and install hello certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="4d6e9-133">(hello может отобразиться под окном сеанса PowerShell hello).</span><span class="sxs-lookup"><span data-stu-id="4d6e9-133">(hello prompt might appear behind hello PowerShell session window).</span></span> 

* <span data-ttu-id="4d6e9-134">Открытие локального компьютера **параметры сети** > **VPN** > щелкните **azurestack** > **подключения**.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-134">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="4d6e9-135">Hello знак в строке введите имя пользователя hello (AzureStack\AzureStackAdmin) и пароль hello.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-135">At hello sign-in prompt, enter hello username (AzureStack\AzureStackAdmin) and hello password.</span></span>

### <a name="test-hello-vpn-connectivity"></a><span data-ttu-id="4d6e9-136">Тест hello VPN-подключение</span><span class="sxs-lookup"><span data-stu-id="4d6e9-136">Test hello VPN connectivity</span></span>

<span data-ttu-id="4d6e9-137">соединение портала tootest hello, откройте веб-браузер и перейдите tooeither hello пользовательского портала (https://portal.local.azurestack.external/) или портал администратора hello (https://adminportal.local.azurestack.external/), вход и создать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4d6e9-137">tootest hello portal connection, open an Internet browser and navigate tooeither hello user portal (https://portal.local.azurestack.external/) or hello administrator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4d6e9-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d6e9-138">Next steps</span></span>

[<span data-ttu-id="4d6e9-139">Делает доступной tooyour виртуальных машин пользователей стек Azure</span><span class="sxs-lookup"><span data-stu-id="4d6e9-139">Make virtual machines available tooyour Azure Stack users</span></span>](azure-stack-tutorial-tenant-vm.md)

