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
# <a name="connect-tooazure-stack"></a>Подключение tooAzure стека

ресурсы toomanage toohello пакет средств разработки стек Azure необходимо подключиться. Шаги hello сведения этого раздела требуется пакет средств разработки toohello tooconnect. Можно использовать либо hello следующие варианты подключения:

* [Удаленный рабочий стол](#connect-with-remote-desktop): позволяет быстро выполнить подключение из пакета средств разработки hello один параллельных пользователю.
* [Виртуальную частную сеть (VPN)](#connect-with-vpn): позволяет несколько одновременных пользователей подключения от клиентов за пределами инфраструктуры Azure стека hello (требует настройки).

## <a name="connect-tooazure-stack-with-remote-desktop"></a>Подключение удаленного рабочего стола tooAzure стека
К удаленному рабочему столу параллельных однопользовательском позволяет работать с портала toomanage ресурсы hello.

1. Откройте подключение к удаленному рабочему столу и подключите toohello пакет средств разработки. Введите **AzureStack\AzureStackAdmin** как hello имя пользователя и пароль администратора hello, указанный во время настройки Azure стека.  

2. На компьютере комплект средств для разработки hello, откройте диспетчер сервера, нажмите кнопку **локального сервера**, отключите усиленной безопасности Internet Explorer, а затем закройте диспетчер сервера.

3. пользователь hello tooopen [портала](azure-stack-key-features.md#portal), слишком перехода (https://portal.local.azurestack.external/) и выполните вход с использованием учетных данных пользователя. Здравствуйте, администратор tooopen [портала](azure-stack-key-features.md#portal), перейдите в слишком (https://adminportal.local.azurestack.external/) и вход с помощью hello Azure Active Directory учетные данные, указанные во время установки.

## <a name="connect-tooazure-stack-with-vpn"></a>Подключение tooAzure стека с помощью VPN

Можно установить разбиение туннель виртуальной частной сети (VPN) подключение tooan пакет средств разработки Azure стека. Через hello VPN-подключение получить доступ к порталу администрирования hello, пользовательский портал и локально установлены средства, такие как Visual Studio и ресурсы Azure стека toomanage PowerShell. В обоих Directory(AAD) Active Azure поддерживается VPN-подключение и Services(AD FS) федерации Active Directory на основе развертываний. VPN-подключений включить tooconnect tooAzure несколько клиентов стека в hello то же время. 

> [!NOTE] 
> Это VPN-подключение не поддерживает подключение tooAzure стека инфраструктуры виртуальных машин. 

### <a name="prerequisites"></a>Предварительные требования

* Установка [совместимый Azure PowerShell Azure стека](azure-stack-powershell-install.md) на локальном компьютере.  
* Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md). 

### <a name="configure-vpn-connectivity"></a>Настройка подключения VPN

toocreate набора разработки toohello подключение VPN, откройте сеанс PowerShell с повышенными привилегиями из локального компьютера под управлением Windows и выполнения hello, выполнив сценарий (Убедитесь, что tooupdate hello hello значения IP-адреса адрес и пароль для вашей среды):

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

Если настроить hello завершается успешно, вы увидите **azurestack** в списке VPN-подключений.

![Сетевые подключения](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-tooazure-stack"></a>Подключение tooAzure стека

Подключения toohello стека Azure экземпляра с помощью любого из следующих двух методов hello:  

* С помощью hello `Connect-AzsVpn ` команды: 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  При появлении запроса доверия hello Azure стека узла и установить сертификат hello от **AzureStackCertificateAuthority** в хранилище сертификатов локального компьютера. (hello может отобразиться под окном сеанса PowerShell hello). 

* Открытие локального компьютера **параметры сети** > **VPN** > щелкните **azurestack** > **подключения**. Hello знак в строке введите имя пользователя hello (AzureStack\AzureStackAdmin) и пароль hello.

### <a name="test-hello-vpn-connectivity"></a>Тест hello VPN-подключение

соединение портала tootest hello, откройте веб-браузер и перейдите tooeither hello пользовательского портала (https://portal.local.azurestack.external/) или портал администратора hello (https://adminportal.local.azurestack.external/), вход и создать ресурсы.  

## <a name="next-steps"></a>Дальнейшие действия

[Делает доступной tooyour виртуальных машин пользователей стек Azure](azure-stack-tutorial-tenant-vm.md)

