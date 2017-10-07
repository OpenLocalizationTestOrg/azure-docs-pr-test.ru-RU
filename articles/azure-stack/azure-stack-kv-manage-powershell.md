---
title: "aaaManage хранилище ключей Azure стека с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toomanage хранилище ключей Azure стека с помощью PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 37adddf8da02766559f4d61134a9d5ce47377da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a>Управление хранилищем ключей Azure стека с помощью PowerShell

Эта статья поможет вам получить toocreate работы и управление хранилищем ключей Azure стека с помощью PowerShell. командлеты PowerShell ключ хранилища Hello, описанных в этой статье доступны как часть hello Azure PowerShell SDK. Hello следующих разделах описаны командлеты PowerShell hello, которые требуется toocreate хранилища, хранения и управлять криптографические ключи и секретные данные, а также разрешают операции tooinvoke пользователи или приложения в хранилище hello. 

## <a name="prerequisites"></a>Предварительные требования
* [Установка PowerShell Azure стека.](azure-stack-powershell-install.md)  
* Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей hello.  
* Пользователи должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей hello. 
* [Настройка среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a>Включите вашу подписку клиента для операций хранилища

Прежде чем можно выполнять все операции с хранилищем ключей, необходимо tooensure которой включены подписки клиента операций в хранилище. tooverify запуска hello следующую команду:

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
**Выходные данные**

Если подписки включены предупреждения об операциях хранилища, hello выходных данных отображается «RegistrationState» равно «Зарегистрированные» для всех типов ресурсов хранилища ключей.

![Состояние регистрации](media/azure-stack-kv-manage-powershell/image1.png)

Если это не так hello, вызовите hello, следующая команда tooregister службы хранилища ключей hello в подписке:

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

**Выходные данные**

При успешном выполнении регистрации hello hello следующие выходные данные возвращаются в:

![Регистрация](media/azure-stack-kv-manage-powershell/image2.png)

Hello следующих разделах предполагается, что служба хранилища ключей зарегистрирована в рамках подписки пользователя hello. При вызове команды хранилища ключей, если возникли ошибка - «hello подписки не зарегистрированного toouse пространством имен "Microsoft.KeyVault», убедитесь, что имеется [включен поставщика ресурсов хранилища ключей hello](#enable-your-tenant-subscription-for-vault-operations) согласно инструкциям, приведенным Приведенные выше.

## <a name="create-a-key-vault"></a>Создайте хранилище ключей. 

Прежде чем создавать хранилища ключей, создайте группу ресурсов, чтобы все хранилища ключей, касающиеся ресурсы находятся в группе ресурсов. Используйте hello, следующая команда toocreate новую группу ресурсов.

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

**Выходные данные**

![Создание группы ресурсов](media/azure-stack-kv-manage-powershell/image3.png)

Теперь воспользуйтесь hello **New AzureRMKeyVault** toocreate команда хранилища ключей в группе ресурсов hello, которое было создано ранее. Эта команда считывает три имя группы ресурсов обязательные параметры, имя хранилища ключей и географическое расположение. 

Выполните следующие команды toocreate hello хранилища ключей:

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
**Выходные данные**

![новый кв](media/azure-stack-kv-manage-powershell/image4.png)

выходные данные этой команды Hello отображает свойства hello hello хранилища ключей, который вы создали. Когда приложение получает доступ к этому хранилищу, он использует hello **URI хранилища** свойства, показанного в выходных данных hello. Например, здесь хранилище hello URI является **https://vault01.vault.local.azurestack.external**. Приложений, взаимодействующих с этим хранилищем ключей через REST API необходимо использовать этот URI.

В развертывании на основе служб федерации Active Directory при создании хранилища ключей с помощью PowerShell, может появиться предупреждение об ошибке «политика доступа не установлена. Не пользователя или приложения имеет toouse разрешение доступа к этим хранилищем». tooresolve эту проблему, задайте политику доступа для hello хранилища с помощью hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) команды:

```PowerShell
# Obtain hello security identifier(SID) of hello active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set hello key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a>Управление ключами и секретов

После создания хранилища, используйте следующие шаги toocreate hello и управление ими ключи и секретные данные в хранилище hello.

### <a name="create-a-key"></a>Создание ключа

Используйте hello **Add-AzureKeyVaultKey** команды toocreate или импортируйте программное обеспечение защищенного ключа в хранилище ключей. 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
Hello **назначения** используется параметр toospecify разделу hello — защищенного программного обеспечения. Если ключ hello успешно создана, hello команда выводит hello подробные сведения о hello ключ создан.

**Выходные данные**

![Новый ключ](media/azure-stack-kv-manage-powershell/image5.png)

Теперь можно создать ссылку hello ключ создан с помощью URI-адрес. Если при создании или импорте ключ, который имеет совпадает с именем существующего ключа, со значениями hello, заданные в новый ключ hello обновляется hello исходного ключа.  Доступ к предыдущей версии hello с помощью конкретной версии hello URI hello ключа. Например, 

* Используйте **https://vault10.vault.local.azurestack.external:443, ключи/key01** tooalways получить текущую версию hello  
* Используйте **https://vault010.vault.local.azurestack.external:443/ключи/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget этой конкретной версии

### <a name="get-a-key"></a>Получить ключ

Используйте hello **Get-AzureKeyVaultKey** команды tooread ключ и сведения о нем.

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a>Создание секрета

Используйте hello **AzureKeyVaultSecret набор** команду toocreate или обновление секрета в хранилище. Секрет создается в том случае, если он еще не существует, а новая версия секрета hello создается в том случае, если он уже существует.

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

**Выходные данные**

![Создание секрета](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a>Получить секрет

Используйте hello **Get AzureKeyVaultSecret** tooread команда секрет в хранилище ключей. Эта команда может возвращать все или некоторые версии секрета. 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

После создания ключи и секретные коды, вы можете разрешить внешние приложения toouse их.

## <a name="authorize-an-application-toouse-a-key-or-secret"></a>Авторизовать приложение toouse ключа или секрета

tooauthorize приложения tooaccess ключа или секрета в hello ключа хранилища, используйте hello **Set-AzureRmKeyVaultAccessPolicy** команды.
Например если имя хранилища — ContosoKeyVault и hello приложения вы хотите tooauthorize имеет идентификатор клиента 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed. Выполните следующие команды tooauthorize hello приложения hello. Кроме того, можно указать hello **PermissionsToKeys** параметр tooset разрешения для пользователя, приложения или группы безопасности:

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

Если требуется tooauthorize этой же tooread секреты приложения в хранилище, выполните следующий командлет hello:

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a>Дальнейшие действия
* [Развертывание виртуальной Машины с помощью пароля, хранящихся в хранилище ключей](azure-stack-kv-deploy-vm-with-secret.md)  
* [Развертывание виртуальной Машины с сертификатом, который хранится в хранилище ключей](azure-stack-kv-push-secret-into-vm.md) 
