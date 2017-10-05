---
title: "Регистрация стек Azure | Документы Microsoft"
description: "Azure стеком регистров с подпиской Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: f71ec571fee8e59ea9061cd619914b81a5bf701a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a>Регистрация стек Azure с подпиской Azure

Для развертываний Azure Active Directory можно зарегистрировать Azure стек Azure для загрузки элементов marketplace из Azure и настроить commerce данные отчетов обратно в корпорацию Майкрософт. 

> [!NOTE]
>Регистрация рекомендуется, так как он позволяет тестировать важные функции Azure стека, например синдикации marketplace и отчеты об использовании. После регистрации Azure стека для Azure commerce отчеты об использовании. Его можно просматривать в подписке, которая использовалась для регистрации. Пользователей Azure стека пакет средств разработки, не будете платить за все они сообщают об использовании.
>


## <a name="get-azure-subscription"></a>Получить подписку Azure

Перед регистрацией стек Azure с помощью Azure, необходимо иметь:

- Идентификатор подписки для подписки Azure. Для получения идентификатора, выполните вход в Azure, нажмите кнопку **дополнительные службы** > **подписки**, щелкните подписку, которую нужно использовать, а затем в разделе **Essentials** можно найти **Идентификатор подписки**. Китай, Германии и нам облака государственных подписок в настоящее время не поддерживаются.
- Имя пользователя и пароль учетной записи, которая является владельцем подписки (поддерживаются учетные записи MSA/2FA)
- Azure Active Directory для подписки Azure. Этот каталог можно найти в Azure, наведя на аватара в правом верхнем углу портала Azure. 
- Регистрации поставщика ресурсов Azure стека (в разделе **Регистрация поставщика ресурсов Azure стека** ниже, в разделе Подробности)

Если нет подписки Azure, удовлетворяющее этим требованиям, вы можете [создать бесплатную учетную запись Azure здесь](https://azure.microsoft.com/en-us/free/?b=17.06). Регистрация стек Azure влечет за собой без затрат на подписки Azure.



## <a name="register-azure-stack-resource-provider-in-azure"></a>Регистрация поставщика ресурсов Azure стека в Azure
> [!NOTE] 
> Этот шаг должен выполняться один раз в среде Azure стека.
>

1. Запуск интегрированной среды Сценариев Powershell от имени администратора.
2. Выполните вход с учетной записью Azure, которая является владельцем подписки Azure с параметром - EnvironmentName в «Облачной».
3. Регистрация поставщика ресурсов Azure «Microsoft.AzureStack».

Пример: 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a>Зарегистрировать стек Azure в Azure

> [!NOTE]
>На главном компьютере необходимо выполнить следующие действия.
>

1. [Установите PowerShell для Azure стека](azure-stack-powershell-install.md). 
2. Копировать [RegisterWithAzure.ps1 сценарий](https://go.microsoft.com/fwlink/?linkid=842959) папку (например, C:\Temp).
3. Запуск интегрированной среды Сценариев PowerShell от имени администратора.    
4. Запустите сценарий RegisterWithAzure.ps1, заменив следующие имена:
    - *YourAccountName* является владельцем подписки Azure
    - *YourID* идентификатор подписки Azure, которую требуется использовать для регистрации стек Azure
    - *YourDirectory* — имя вашего клиента Azure Active Directory, ваша подписка Azure является частью.

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    Например:
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. В двух запросов нажмите клавишу ВВОД.
6. В окне всплывающего входа введите учетные данные подписки Azure.

## <a name="verify-the-registration"></a>Проверьте регистрацию

1. Войдите в портал администратора (https://adminportal.local.azurestack.external).
2. Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавьте из Azure**.
3. Если отображается список элементов, доступный в Azure (таких как WordPress) активацию прошла успешно.

## <a name="next-steps"></a>Дальнейшие действия

[Подключение к Azure Stack](azure-stack-connect-azure-stack.md)

