---
title: "Доступ к Azure Resource Manager с помощью MSI виртуальной машины Windows"
description: "В рамках этого руководства вы узнаете, как получить доступ к Azure Resource Manager с помощью управляемого удостоверения службы (MSI) виртуальной машины Windows."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: bryanla
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/20/2017
ms.author: bryanla
ms.openlocfilehash: b5ba403c4e152770eeacb32d4a8d1980cf039396
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="use-a-windows-vm-managed-service-identity-msi-to-access-resource-manager"></a>Доступ к Resource Manager с помощью управляемого удостоверения службы (MSI) виртуальной машины Windows

[!INCLUDE[preview-notice](../../includes/active-directory-msi-preview-notice.md)]

В этой статье описывается активация управляемого удостоверения службы (MSI) виртуальной машины Windows и его использование для получения доступа к API Azure Resource Manager. Управляемыми удостоверениями службы автоматически управляет Azure. Они позволяют проходить аутентификацию в службах, поддерживающих аутентификацию Azure AD, без указания учетных данных в коде. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Активация MSI на виртуальной машине Windows. 
> * Предоставление виртуальной машине доступа к группе ресурсов в Azure Resource Manager. 
> * Получение маркера доступа с помощью удостоверения виртуальной машины и вызов Azure Resource Manager с его помощью.

## <a name="prerequisites"></a>Технические условия

[!INCLUDE [msi-qs-configure-prereqs](../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../includes/active-directory-msi-tut-prereqs.md)]

## <a name="sign-in-to-azure"></a>Вход в Azure
Войдите на портал Azure по адресу [https://portal.azure.com](https://portal.azure.com).

## <a name="create-a-windows-virtual-machine-in-a-new-resource-group"></a>Создание виртуальной машины Windows в новой группе ресурсов

В рамках этого руководства мы создадим виртуальную машину Windows.  Вы также можете активировать MSI на имеющейся виртуальной машине.

1.  Щелкните **Создать** в верхнем левом углу портала Azure.
2.  Выберите **Вычисления**, а затем — **Windows Server 2016 Datacenter**. 
3.  Введите сведения о виртуальной машине. **Имя пользователя** и **пароль**, созданные здесь, используются для входа на виртуальную машину.
4.  В раскрывающемся списке выберите нужную **подписку** для виртуальной машины.
5.  Чтобы выбрать новую **группу ресурсов**, в которой вы хотите создать виртуальную машину, щелкните **Создать**. По завершении нажмите кнопку **ОК**.
6.  Выберите размер виртуальной машины. Чтобы просмотреть дополнительные размеры, выберите **Просмотреть все** или измените фильтр **Supported disk type** (Поддерживаемые типы диска). На странице параметров оставьте значения по умолчанию и нажмите кнопку **OK**.

    ![Замещающий текст](media/msi-tutorial-windows-vm-access-arm/msi-windows-vm.png)

## <a name="enable-msi-on-your-vm"></a>Активация MSI на виртуальной машине 

MSI на виртуальной машине позволяет получить маркеры доступа из Azure AD без необходимости указывать в коде учетные данные. Активация MSI указывает Azure создать управляемое удостоверение для виртуальной машины. На самом деле активация MSI необходима для установки расширения виртуальной машины MSI и непосредственно активации MSI в Azure Resource Manager.

1.  Выберите **виртуальную машину**, на которой нужно активировать MSI.  
2.  В левой области навигации щелкните **Конфигурация**. 
3.  Появится страница **Managed Service Identity** (Управляемое удостоверение службы). Чтобы зарегистрировать и активировать MSI, нажмите кнопку **Да**. Чтобы удалить удостоверение, нажмите кнопку "Нет". 
4.  Нажмите кнопку **Сохранить**, чтобы сохранить конфигурацию.  
    ![Замещающий текст](media/msi-tutorial-linux-vm-access-arm/msi-linux-extension.png)

5. Если вы хотите проверить расширения на этой виртуальной машине, щелкните **Расширения**. Если удостоверение MSI активировано, вы увидите в списке **ManagedIdentityExtensionforWindows**.

    ![Замещающий текст](media/msi-tutorial-windows-vm-access-arm/msi-windows-extension.png)

## <a name="grant-your-vm-access-to-a-resource-group-in-resource-manager"></a>Предоставление виртуальной машине доступа к группе ресурсов в Resource Manager
С помощью MSI код может получить маркеры доступа, чтобы пройти аутентификацию и получить доступ к ресурсам, поддерживающим аутентификацию Azure AD.  Azure Resource Manager поддерживает аутентификацию Azure AD.  Сначала нам необходимо предоставить этому удостоверению виртуальной машины доступ к ресурсу в Resource Manager, в этом случае — к группе ресурсов, в которой находится виртуальная машина.  

1.  Перейдите на вкладку **Группы ресурсов**. 
2.  Выберите определенную **группу ресурсов**, созданную ранее для **виртуальной машины Windows**. 
3.  Перейдите к элементу **Управление доступом (IAM)** на панели слева. 
4.  Щелкните **Добавить**, чтобы добавить новое назначение роли **виртуальной машине Windows**.  В поле **Роль** выберите **Читатель**. 
5.  В раскрывающемся списке далее в поле **Назначение доступа к** выберите ресурс **Виртуальная машина**. 
6.  Проверьте, чтобы в раскрывающемся списке **Подписка** была выбрана нужная подписка. В поле **Группа ресурсов** выберите **Все группы ресурсов**. 
7.  И наконец, в поле **Выбрать** выберите свою виртуальную машину Windows в раскрывающемся списке, а затем нажмите кнопку **Сохранить**.

    ![Замещающий текст](media/msi-tutorial-windows-vm-access-arm/msi-windows-permissions.png)

## <a name="get-an-access-token-using-the-vm-identity-and-use-it-to-call-azure-resource-manager"></a>Получение маркера доступа с помощью удостоверения виртуальной машины и вызов Azure Resource Manager с его помощью. 

На этом этапе понадобится использовать **PowerShell**.  Если эта среда не установлена, загрузите ее [отсюда](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1). 

1.  На портале перейдите к разделу **Виртуальные машины**, выберите свою виртуальную машину Windows и в разделе **Обзор** щелкните **Подключить**. 
2.  Введите **имя пользователя** и **пароль**, добавленные при создании виртуальной машины Windows. 
3.  Теперь, когда создано **подключение к удаленному рабочему столу** с виртуальной машиной, откройте **PowerShell** в удаленном сеансе. 
4.  С помощью команды Invoke-WebRequest PowerShell сделайте запрос к локальной конечной точке MSI, чтобы получить маркер доступа к Azure Resource Manager.

    ```powershell
       $response = Invoke-WebRequest -Uri http://localhost:50342/oauth2/token -Method GET -Body @{resource="https://management.azure.com/"} -Headers @{Metadata="true"}
    ```
    
    > [!NOTE]
    > Значение параметра resource должно точно совпадать со значением, которое будет использоваться в Azure AD. Если используется идентификатор ресурса Resource Manager, добавьте косую черту после универсального кода ресурса (URI).
    
    Затем извлеките полный ответ, который хранится в виде форматированной строки JSON в объекте $response. 
    
    ```powershell
    $content = $response.Content | ConvertFrom-Json
    ```
    Затем извлеките маркер доступа из ответа.
    
    ```powershell
    $ArmToken = $content.access_token
    ```
    
    Теперь вызовите Azure Resource Manager с использованием маркера доступа. В этом примере мы также используем команду Invoke-WebRequest PowerShell для вызова Azure Resource Manager и включаем маркер доступа в заголовок авторизации.
    
    ```powershell
    (Invoke-WebRequest -Uri https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>?api-version=2016-06-01 -Method GET -ContentType "application/json" -Headers @{ Authorization ="Bearer $ArmToken"}).content
    ```
    > [!NOTE] 
    > URL-адрес чувствителен к регистру, поэтому должен использоваться тот же регистр, который использовался, когда вы присваивали имя группе ресурсов. Проверьте, чтобы в resourceGroups обязательно использовался символ "G" (прописная буква).
        
    Следующая команда возвращает сведения о группе ресурсов:

    ```powershell
    {"id":"/subscriptions/98f51385-2edc-4b79-bed9-7718de4cb861/resourceGroups/DevTest","name":"DevTest","location":"westus","properties":{"provisioningState":"Succeeded"}}
    ```

## <a name="related-content"></a>Связанная информация

- Общие сведения об MSI см. в разделе [Управляемое удостоверение службы (MSI) для Azure Active Directory](../active-directory/msi-overview.md).

Оставляйте свои замечания и пожелания в разделе ниже. Они помогают нам улучшать содержимое веб-сайта.

