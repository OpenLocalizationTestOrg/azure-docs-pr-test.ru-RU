---
title: "aaaCreate участника-службы для Azure стека | Документы Microsoft"
description: "Описывает способ toocreate нового участника службы, который может использоваться с элементом управления доступом на основе hello в tooresources доступа toomanage диспетчера ресурсов Azure."
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: f090ceed941abe9255bc35ec966bc43df3bb2955
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provide-applications-access-tooazure-stack"></a>Предоставить доступ приложений tooAzure стека
При приложения должен toodeploy доступа или настроить ресурсами с помощью диспетчера ресурсов Azure в стек Azure, вы создаете субъект-служба, являющийся учетных данных для приложения.  Затем можно делегировать только hello необходимые разрешения toothat участника-службы.  

Например, возможно, средство управления конфигурации, которое использует Azure Resource Manager tooinventory ресурсов Azure.  В этом случае можно создать участника службы, предоставления роли участника службы toothat чтения hello и ограничить hello конфигурации управления средство tooread доступ только. 

Субъекты-службы, которые приложение hello предпочтительным toorunning в своих собственных учетных данных, так как:

* Можно назначить участника службы toohello разрешения, отличаются от разрешений учетной записи. Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.
* У вас приложение hello toochange учетные данные при изменении ваши обязанности.
* При выполнении сценария автоматической можно использовать проверку подлинности сертификата tooautomate.  

## <a name="getting-started"></a>Приступая к работе

В зависимости от способа развертывания Azure стека начните с создания участника службы.  Этот документ поможет создать участника-службы для обоих [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) и [Services(AD FS) федерации Active Directory](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).  После создания hello участника-службы, набор tooboth общие шаги AD FS и Azure Active Directory используются слишком[делегировать разрешения](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello роли.     

## <a name="create-service-principal-for-azure-ad"></a>Создание участника службы для Azure AD

Если вы развернули стек Azure, с помощью Azure AD как хранилище удостоверений hello, можно создать участников службы, так же, как и для Azure.  В этом разделе показано, как tooperform hello проходит через портал hello.  Убедитесь, что hello [Azure AD разрешения, необходимые](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) перед началом.

### <a name="create-service-principal"></a>Создание субъекта-службы
В этом разделе создается приложение (субъекта-службы) в Azure AD, который будет представлять приложение.

1. Войдите в tooyour учетную запись Azure через hello [портал Azure](https://portal.azure.com).
2. Выберите **Azure Active Directory** > **регистрации приложения** > **добавить**   
3. Укажите имя и URL-адрес для приложения hello. Выберите либо **веб-приложения и API** или **собственного** для типа приложения hello требуется toocreate. После задания значения hello, выберите **создать**.

Вы создали субъекта-службы для приложения.

### <a name="get-credentials"></a>Получить учетные данные
Программным способом входа в систему используется идентификатор hello для приложения и ключ проверки подлинности. те значения, tooget hello используйте следующие шаги:

1. В Active Directory в разделе **регистрации приложений** выберите нужное приложение.

2. Копировать hello **идентификатор приложения** и сохранить ее в коде приложения. Здравствуйте, приложения hello [образцы приложений](#sample-applications) значение toothis, что идентификатор hello клиента см. раздел.

     ![Идентификатор клиента](./media/azure-stack-create-service-principal/image12.png)
3. Выберите ключ проверки подлинности toogenerate **ключей**.

4. Введите описание ключа hello и длительность для ключа hello. Затем нажмите кнопку **Сохранить**.

После сохранения ключа hello, отображается значение hello hello ключа. Скопируйте это значение невозможно, поскольку ключ может tooretrieve hello позже. Значение ключа hello предоставить toosign идентификатор приложения hello как приложение hello. Сохраните значение ключа hello, где приложение может вернуть их.

![сохраненный ключ](./media/azure-stack-create-service-principal/image15.png)


После завершения продолжить слишком[назначение роли приложения](azure-stack-create-service-principals.md#assign-role-to-service-principal).

## <a name="create-service-principal-for-ad-fs"></a>Создание участника службы для AD FS
При развертывании Azure стека с AD FS можно использовать PowerShell toocreate участника службы, назначение роли для доступа и входа с PowerShell, с использованием указанного удостоверения.

### <a name="before-you-begin"></a>Перед началом работы

[Загрузите необходимые toowork hello средства с Azure стека tooyour локального компьютера.](azure-stack-powershell-download.md)

### <a name="import-hello-identity-powershell-module"></a>Модуль PowerShell идентификаторов hello импорта
После загрузки средства hello, перейдите в папку toohello загрузки и импорт модуля PowerShell идентификаторов hello с помощью hello следующую команду:

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

При импорте модуля hello, может появиться сообщение об ошибке: «AzureStack.Connect.psm1 не имеет цифровой подписи. Hello сценарий не будет выполняться в системе hello». tooresolve эту проблему, задайте tooallow политики выполнения сценария hello, выполнив следующую команду в сеансе PowerShell с повышенными привилегиями hello:

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-hello-service-principal"></a>Создать hello участника-службы
Можно создать субъект-службу, выполнив следующие hello команды, выполняющего убедиться, что hello tooupdate *DisplayName* параметр:
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a>Назначение роли
Один раз hello при создании участника службы, необходимо [назначить его tooa роли](azure-stack-create-service-principals.md#assign-role-to-service-principal)

### <a name="sign-in-through-powershell"></a>Войти с помощью PowerShell
После был назначен роли, вы сможете войти в tooAzure стека с помощью субъекта-службы hello с hello следующую команду:

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-tooservice-principal"></a>Назначение роли участника tooservice
tooaccess ресурсам в подписке, необходимо назначить роль tooa приложения hello. Решите, какую роль представляет hello нужные разрешения для приложения hello. toolearn о hello доступным ролям, в разделе [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).

Можно установить область hello на уровне hello hello подписки, группы ресурсов или ресурсов. Разрешения, наследуемые toolower уровни области действия. Например для добавления роли модуля чтения toohello приложения для группы ресурсов есть может считать группы ресурсов hello и все ресурсы, которые он содержит.

1. На портале Azure стека hello перейти на уровень toohello области, в которых надо tooassign hello приложению. Например, tooassign роль в области hello подписки, выберите **подписки**. Или же вы можете выбрать группу ресурсов либо отдельный ресурс.

2. Выберите приложение hello tooassign hello определенной подписки (группа ресурсов или ресурсов) для.

     ![выбрать подписку для назначения](./media/azure-stack-create-service-principal/image16.png)

3. Выберите **Управление доступом (IAM)**.

     ![выбрать доступ](./media/azure-stack-create-service-principal/image17.png)

4. Выберите **Добавить**.

5. Выберите роль hello нужно tooassign toohello приложения.

6. Найдите приложение и выберите его.

7. Выберите **ОК** toofinish назначение роли hello. Вы видите приложение hello списка пользователей, назначенных роли tooa для данной области.

Теперь, создания участника службы и назначить роль, можно начать с помощью этого в рамках вашего приложения tooaccess ресурсы Azure стека.  

## <a name="next-steps"></a>Дальнейшие действия

[Добавление пользователей для служб федерации Active Directory](azure-stack-add-users-adfs.md)
[управлять разрешениями пользователей](azure-stack-manage-permissions.md)