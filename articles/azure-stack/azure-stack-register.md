---
title: "aaaRegister стек Azure | Документы Microsoft"
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
ms.openlocfilehash: 3a3c8e82bec3e1e26ecfe591ecc27b2b91f6f91e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a>Регистрация стек Azure с подпиской Azure

Для развертываний Azure Active Directory с Azure toodownload элементы marketplace из Azure и tooset commerce данные обратно reporting tooMicrosoft можно зарегистрировать стек Azure. 

> [!NOTE]
>Регистрация рекомендуется, так как он позволяет tootest важные стек Azure функциональных возможностей, таких как синдикации marketplace и отчеты об использовании. После регистрации Azure стека вариантом применения является commerce tooAzure отчета. Его можно просматривать в подписке hello, использованный для регистрации. Пользователей Azure стека пакет средств разработки, не будете платить за все они сообщают об использовании.
>


## <a name="get-azure-subscription"></a>Получить подписку Azure

Перед регистрацией стек Azure с помощью Azure, необходимо иметь:

- Идентификатор подписки Hello для подписки Azure. Идентификатор hello tooget, вход tooAzure, нажмите кнопку **дополнительные службы** > **подписки**, щелкните подписку hello требуется toouse и в разделе **Essentials** вы можете найти hello **идентификатор подписки**. Китай, Германии и нам облака государственных подписок в настоящее время не поддерживаются.
- Здравствуйте, имя пользователя и пароль учетной записи, которая является владельцем подписки hello (поддерживаются учетные записи MSA/2FA)
- Hello Azure Active Directory для hello подписки Azure. Наведя аватара в верхнем правом углу hello hello портал Azure можно найти этот каталог в Azure. 
- Зарегистрированные hello поставщика ресурсов Azure стека (hello в разделе **Регистрация поставщика ресурсов Azure стека** ниже, в разделе подробные сведения)

Если нет подписки Azure, удовлетворяющее этим требованиям, вы можете [создать бесплатную учетную запись Azure здесь](https://azure.microsoft.com/en-us/free/?b=17.06). Регистрация стек Azure влечет за собой без затрат на подписки Azure.



## <a name="register-azure-stack-resource-provider-in-azure"></a>Регистрация поставщика ресурсов Azure стека в Azure
> [!NOTE] 
> Этот шаг требуется только один раз выполнить в среде Azure стека toobe.
>

1. Запуск интегрированной среды Сценариев Powershell от имени администратора.
2. Вход toohello учетная запись Azure, который является владельцем hello подписки Azure с параметром - EnvironmentName значение слишком «Облачной».
3. Регистрация поставщика ресурсов Azure hello «Microsoft.AzureStack».

Пример: 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a>Зарегистрировать стек Azure в Azure

> [!NOTE]
>На главном компьютере hello необходимо выполнить следующие действия.
>

1. [Установите PowerShell для Azure стека](azure-stack-powershell-install.md). 
2. Копировать hello [RegisterWithAzure.ps1 сценарий](https://go.microsoft.com/fwlink/?linkid=842959) tooa папку (например, C:\Temp).
3. Запуск интегрированной среды Сценариев PowerShell от имени администратора.    
4. Запустите сценарий RegisterWithAzure.ps1 hello, заменив hello следующие местозаполнители:
    - *YourAccountName* является владельцем hello hello подписки Azure
    - *YourID* — идентификатор подписки Azure hello, что требуется toouse tooregister стек Azure
    - *YourDirectory* — имя вашего клиента Azure Active Directory, ваша подписка Azure является частью hello.

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    Например:
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. В hello два запроса нажмите клавишу ВВОД.
6. В окне приветствия всплывающих входа введите учетные данные подписки Azure.

## <a name="verify-hello-registration"></a>Проверка регистрации hello

1. Войдите в портал администратора toohello (https://adminportal.local.azurestack.external).
2. Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавьте из Azure**.
3. Если отображается список элементов, доступный в Azure (таких как WordPress) активацию прошла успешно.

## <a name="next-steps"></a>Дальнейшие действия

[Подключение tooAzure стека](azure-stack-connect-azure-stack.md)

