---
title: "aaaAdd новую учетную запись клиента Azure стека в Azure Active Directory | Документы Microsoft"
description: "После развертывания пакета средств разработки Microsoft Azure стека, необходимо по крайней мере один toocreate клиента учетной записи пользователя, поэтому можно изучить hello клиентского портала."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: f0cd380d4fc0b52f4e5f6f0c9ef80d3dd0d64443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a>Добавление новой учетной записи клиента Azure Stack в Azure Active Directory
После [развертывание hello Azure стека Development Kit](azure-stack-run-powershell-script.md), потребуется учетной записью клиента, поэтому вы можете анализировать hello портала клиента и протестируйте свои предложения и планы. Можно создать учетную запись с [с помощью портала Azure "hello"](#create-an-azure-stack-tenant-account-using-the-azure-portal) или [с помощью PowerShell](#create-an-azure-stack-tenant-account-using-powershell).

## <a name="create-an-azure-stack-tenant-account-using-hello-azure-portal"></a>Создать учетную запись клиента Azure стека с помощью портала Azure hello
Необходимо иметь подписку Azure toouse hello портал Azure.

1. Войдите в слишком[Azure](http://manage.windowsazure.com).
2. На левой навигационной панели Microsoft Azure щелкните **Active Directory**.
3. В список каталогов hello щелкните каталог hello должны toouse для стека Azure или создайте новую.
4. На странице каталога щелкните **Пользователи**.
5. Нажмите кнопку **Добавить пользователя**.
6. В hello **добавить пользователя** мастера в hello **тип пользователя** выберите **новый пользователь в вашей организации**.
7. В hello **имя пользователя** введите имя пользователя hello.
8. В hello  **@**  выберите соответствующую запись hello.
9. Щелкните стрелку hello.
10. В hello **профиля пользователя** на странице приветствия мастера введите команду **имя**, **Фамилия**, и **отображаемое имя**.
11. В hello **роли** выберите **пользователя**.
12. Щелкните стрелку hello.
13. На hello **получение временного пароля** щелкните **создать**.
14. Копировать hello **новый пароль**.
15. Войдите в tooMicrosoft Azure с новой учетной записью hello. Изменение пароля hello при появлении запроса.
16. Войдите в слишком`https://portal.local.azurestack.external` с hello новой учетной записи toosee hello портала клиента.

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a>Создание учетной записи клиента Azure Stack с помощью PowerShell
Если у вас нет подписки Azure, нельзя использовать hello Azure портала tooadd учетной записью клиента. В этом случае можно вместо этого использовать hello Azure Active Directory модуля для Windows PowerShell.

> [!NOTE]
> При использовании учетной записи Майкрософт (Live ID) toodeploy пакет средств разработки стек Azure нельзя использовать учетную запись клиента toocreate AAD PowerShell. 
> 
> 

1. Установка hello [Microsoft Online Services помощник по входу для ИТ-специалистов RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).
2. Установка hello [Azure Active Directory модуля для Windows PowerShell (64-разрядная версия)](http://go.microsoft.com/fwlink/p/?linkid=236297) и откройте его.
3. Выполните следующие командлеты hello.

    ```powershell
    # Provide hello AAD credential you use toodeploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with hello initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. Войдите в tooMicrosoft Azure с новой учетной записью hello. Изменение пароля hello при появлении запроса.
2. Войдите в слишком`https://portal.local.azurestack.external` с hello новой учетной записи toosee hello портала клиента.

