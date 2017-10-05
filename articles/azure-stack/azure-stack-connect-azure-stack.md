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
ms.openlocfilehash: 44b167972ceffc8de48ae7560b85009a96378144
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-azure-stack"></a>Подключение к Azure Stack

Для управления ресурсами, необходимо подключиться к набору разработки Azure стека. В этом разделе описаны действия, требуемые для подключения к набору разработки. Можно использовать любой из следующих параметров подключения:

* [Удаленный рабочий стол](#connect-with-remote-desktop): позволяет быстро выполнить подключение из пакета средств разработки единого параллельных пользователю.
* [Виртуальную частную сеть (VPN)](#connect-with-vpn): позволяет несколько одновременных пользователей подключения от клиентов за пределами Azure стека инфраструктуры (требует настройки).

## <a name="connect-to-azure-stack-with-remote-desktop"></a>Подключиться к Azure стека с помощью удаленного рабочего стола
К удаленному рабочему столу параллельных однопользовательском позволяет работать с портала управления ресурсами.

1. Откройте подключение к удаленному рабочему столу и подключитесь к набору разработки. Введите **AzureStack\AzureStackAdmin** как имя пользователя и пароль администратора, указанный во время настройки Azure стека.  

2. С компьютера разработки пакета, откройте диспетчер сервера, щелкните **локального сервера**, отключите усиленной безопасности Internet Explorer, а затем закройте диспетчер сервера.

3. Чтобы открыть пользователь [портала](azure-stack-key-features.md#portal), перейдите к (https://portal.local.azurestack.external/) и выполните вход с помощью учетных данных пользователя. Открытие администратора [портала](azure-stack-key-features.md#portal), перейдите к (https://adminportal.local.azurestack.external/) и выполните вход с использованием учетных данных Azure Active Directory, указанные во время установки.

## <a name="connect-to-azure-stack-with-vpn"></a>Подключиться к Azure стека с помощью VPN

Туннель разбиение подключения виртуальной частной сети (VPN) для пакета средств разработки Azure стека можно создать. Через подключение VPN доступа к порталу администратора пользовательского портала и локально установлены средства, такие как Visual Studio и PowerShell для управления ресурсами Azure стека. В обоих Directory(AAD) Active Azure поддерживается VPN-подключение и Services(AD FS) федерации Active Directory на основе развертываний. VPN-подключений включить нескольких клиентов для подключения к Azure стека, в то же время. 

> [!NOTE] 
> Это VPN-подключение не поддерживает возможность подключения к инфраструктуре Azure стека виртуальных машин. 

### <a name="prerequisites"></a>Предварительные требования

* Установка [совместимый Azure PowerShell Azure стека](azure-stack-powershell-install.md) на локальном компьютере.  
* Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md). 

### <a name="configure-vpn-connectivity"></a>Настройка подключения VPN

Чтобы создать VPN-подключение к набору разработки, откройте сеанс PowerShell с повышенными привилегиями на локальном компьютере под управлением Windows и выполните следующий скрипт (Убедитесь, что для обновления значения IP адрес и пароль для вашей среды):

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

Если настройка выполнена успешно, вы увидите **azurestack** в списке VPN-подключений.

![Сетевые подключения](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a>Подключение к Azure Stack

Подключитесь к экземпляру стек Azure с помощью любого из следующих двух способов:  

* С помощью `Connect-AzsVpn ` команды: 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  При появлении запроса доверия стека Azure узла и установить сертификат от **AzureStackCertificateAuthority** в хранилище сертификатов локального компьютера. (может появиться запрос позади окна сеанса PowerShell). 

* Открытие локального компьютера **параметры сети** > **VPN** > щелкните **azurestack** > **подключения**. В командной строке входа введите имя пользователя (AzureStack\AzureStackAdmin) и пароль.

### <a name="test-the-vpn-connectivity"></a>Проверить подключение к VPN

Чтобы проверить соединение с портала, откройте браузер и перейдите на пользовательский портал (https://portal.local.azurestack.external/) или портал администратора (https://adminportal.local.azurestack.external/), вход и создание ресурсов.  

## <a name="next-steps"></a>Дальнейшие действия

[Доступность виртуальных машин для пользователей стек Azure](azure-stack-tutorial-tenant-vm.md)

