---
title: "Управление доступом на основе aaaRole в службе автоматизации Azure | Документы Microsoft"
description: "Контроль доступа на основе ролей (RBAC) Azure обеспечивает управление доступом к ресурсам Azure. В этой статье описывается как tooset копирование RBAC в службе автоматизации Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "автоматизация RBAC, контроль доступа на основе ролей, RBAC Azure"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Управление доступом на основе ролей в службе автоматизации Azure
## <a name="role-based-access-control"></a>Контроль доступа на основе ролей
Контроль доступа на основе ролей (RBAC) Azure обеспечивает управление доступом к ресурсам Azure. С помощью [RBAC](../active-directory/role-based-access-control-configure.md), можно разделить обязанностей в вашу рабочую группу и предоставить только hello объем toousers доступа, группы и приложения, что они должны tooperform свою работу. С помощью портала Azure hello, средств командной строки Azure или API управления Azure toousers может быть предоставлен доступ, на основе ролей.

## <a name="rbac-in-automation-accounts"></a>Управление доступом в учетных записях автоматизации
В службе автоматизации Azure доступ предоставляется путем назначения hello соответствующие RBAC роли toousers, группы и приложения в области действия учетных записей автоматизации hello. Встроенные роли, включенные в учетной записи автоматизации Здравствуйте, следующие:  

| **Роль** | **Описание** |
|:--- |:--- |
| Владелец |роль владельца Hello позволяет tooall доступ к ресурсам и действий в рамках учетной записи автоматизации, включая предоставление доступа tooother пользователей, групп и приложений toomanage hello учетной записи автоматизации. |
| Участник |роль участника Hello позволяет toomanage все, кроме изменение другого пользователя получить доступ к учетной записи автоматизации tooan разрешения. |
| читатель. |роль модуля чтения Hello позволяет tooview всех ресурсов hello объекта автоматизации учетной записи, но не может вносить изменения. |
| Оператор службы автоматизации |роль Hello оператор автоматизации позволяет tooperform таких задач как запуска, остановки, приостановки, возобновления и планирования заданий. Эта роль является полезным, если вы хотите tooprotect вашей учетной записи автоматизации ресурсы, такие как активы учетных данных и модулей Runbook, просматривать и изменять, но они по-прежнему Разрешать членам группы tooexecute вашей организации. |
| Администратор доступа пользователей |роли администратора пользователей доступ Hello позволяет учетные записи автоматизации tooAzure toomanage пользователю доступ. |

> [!NOTE]
> Вы не можете предоставить доступ права tooa конкретных модуль или модули Runbook, только toohello ресурсы и действия в пределах hello учетной записи автоматизации.  
> 
> 

В этой статье мы поможет вам выполнить как tooset копирование RBAC в службе автоматизации Azure. Но сначала давайте take ближе просмотрите hello отдельные разрешения предоставленный toohello участника, средства чтения, оператора автоматизации и администратор доступа пользователя, чтобы мы получить хорошее представление о перед предоставлением всем права учетной записи автоматизации toohello.  Отсутствие знаний может привести к непредвиденным и нежелательным последствиям.     

## <a name="contributor-role-permissions"></a>Разрешения для роли участника
Hello следующей таблице представлены hello специфические действия, которые может выполнять роль участника hello в автоматизации.

| **Тип ресурса** | **чтение** | **запись** | **Удалить** | **Другие действия** |
|:--- |:--- |:--- |:--- |:--- |
| Учетная запись службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Ресурс сертификатов службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Ресурс подключений службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Ресурс типа подключения службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Ресурс учетных данных службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Ресурс расписания службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Ресурс переменных службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Настройка требуемого состояния службы автоматизации | | | |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |
| Тип ресурсов гибридной рабочей роли Runbook |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Задание службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |
| Поток заданий службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Расписание заданий службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Модуль службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |
| Runbook службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |
| Черновик Runbook службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |
| Задание тестирования черновика Runbook службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |
| Объект webhook службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Разрешения роли читателя
Hello следующей таблице представлены hello специфические действия, которые может выполнять роль чтения hello автоматизации.

| **Тип ресурса** | **чтение** | **запись** | **Удалить** | **Другие действия** |
|:--- |:--- |:--- |:--- |:--- |
| Классический администратор подписки |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Блокировка управления |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Разрешение |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Операции с поставщиками |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Назначение роли |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Определение роли |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Разрешения роли оператора службы автоматизации
Hello следующей таблице представлены hello определенные действия, которые могут быть выполнены по роли оператора автоматизации hello в автоматизации.

| **Тип ресурса** | **чтение** | **запись** | **Удалить** | **Другие действия** |
|:--- |:--- |:--- |:--- |:--- |
| Учетная запись службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ресурс сертификатов службы автоматизации | | | | |
| Ресурс подключений службы автоматизации | | | | |
| Ресурс типа подключения службы автоматизации | | | | |
| Ресурс учетных данных службы автоматизации | | | | |
| Ресурс расписания службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | |
| Ресурс переменных службы автоматизации | | | | |
| Настройка требуемого состояния службы автоматизации | | | | |
| Тип ресурсов гибридной рабочей роли Runbook | | | | |
| Задание службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |
| Поток заданий службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Расписание заданий службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | |
| Модуль службы автоматизации | | | | |
| Runbook службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Черновик Runbook службы автоматизации | | | | |
| Задание тестирования черновика Runbook службы автоматизации | | | | |
| Объект webhook службы автоматизации | | | | |

Для получения дополнительных сведений hello [действия оператора автоматизации](../active-directory/role-based-access-built-in-roles.md#automation-operator) списки hello действия, поддерживаемые роли оператора hello автоматизации на учетную запись автоматизации hello и его ресурсам.

## <a name="user-access-administrator-role-permissions"></a>Разрешения роли администратора доступа пользователей
Hello следующей таблице представлены hello определенные действия, которые могут быть выполнены по роли Администратор доступа пользователя hello в автоматизации.

| **Тип ресурса** | **чтение** | **запись** | **Удалить** | **Другие действия** |
|:--- |:--- |:--- |:--- |:--- |
| Учетная запись службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ресурс сертификатов службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ресурс подключений службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ресурс типа подключения службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ресурс учетных данных службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ресурс расписания службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ресурс переменных службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Настройка требуемого состояния службы автоматизации | | | | |
| Тип ресурсов гибридной рабочей роли Runbook |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Задание службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Поток заданий службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Расписание заданий службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Модуль службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Runbook службы автоматизации Azure |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Черновик Runbook службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Задание тестирования черновика Runbook службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Объект webhook службы автоматизации |![Зеленый индикатор](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Настройки RBAC для учетной записи службы автоматизации с помощью портала Azure
1. Войдите в toohello [портала Azure](https://portal.azure.com/) и открыть учетную запись автоматизации из колонки hello учетные записи автоматизации.  
2. Щелкните hello **доступа** контроля на hello правом верхнем углу. При этом откроется hello **пользователей** колонки, где можно добавлять новых пользователей, групп и приложений toomanage ваша учетная запись автоматизации и просмотр существующих ролей, которые можно настроить для hello учетной записи автоматизации.  
   
   ![Кнопка доступа](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Администраторы подписки** уже существует как пользователь по умолчанию hello. Группа active directory Администраторы подписки Hello включает администраторов службы hello и co-administrator(s) для подписки Azure. Здравствуйте, администратор службы является hello владельцем подписки Azure и его ресурсы и будет иметь роль владельца hello унаследованы для учетных записей автоматизации hello слишком. Это означает, что доступ hello **Inherited** для **Администраторы службы и соадминистраторы** подписки и его **назначено** для всех hello другим пользователям. Нажмите кнопку **Администраторы подписки** tooview более подробные сведения об их разрешения.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Добавление нового пользователя и назначение роли
1. Колонка "пользователи" hello, щелкните **добавить** tooopen hello **колонке доступа Add** где можно добавить пользователя, группы или приложения и назначить toothem роли.  
   
   ![Добавить пользователя](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Выберите роль из списка доступных ролей hello. Мы выберет hello **чтения** роли, но можно выбрать любую из доступных hello встроенных ролей, которые поддерживает учетную запись автоматизации или любой пользовательской роли, которые были определены.  
   
   ![Выбрать роль](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Щелкните **Добавление пользователей** tooopen hello **Добавление пользователей** колонку. При добавлении любого toomanage пользователей, групп или приложений перечислены подписки, а затем этих пользователей и их можно выбрать tooadd доступа. Если нет, все пользователи в списке, или если вы заинтересованы в добавлении пользователь hello не указан, нажмите кнопку **пригласить** tooopen hello **пригласить гостя** колонки, где вы можете пригласить пользователя с действительной учетной записи Майкрософт адрес электронной почты, например Outlook.com, OneDrive или Xbox Live идентификаторы. После ввода hello адрес электронной почты пользователя hello щелкните **выберите** tooadd hello пользователя и нажмите кнопку **ОК**. 
   
   ![Добавление пользователей](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Теперь вы увидите добавляется пользователь hello toohello **пользователей** колонка с hello **чтения** ролью.  
   
   ![Список пользователей](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   Можно также назначить пользователя роли toohello из hello **ролей** колонку. 
4. Нажмите кнопку **ролей** из колонки tooopen hello пользователей hello **колонке ролей**. В этой колонке можно просмотреть hello имя роли hello, hello числа пользователей и группы, назначенные toothat роли.
   
    ![Назначение роли из колонки пользователей](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Управление доступом на основе ролей может устанавливаться только на уровне учетной записи автоматизации hello, а не на любой ресурс ниже hello учетной записи автоматизации.
   > 
   > 
   
    Можно назначить несколько ролей tooa пользователя, группы или приложения. Например, если мы добавим hello **оператор автоматизации** роли, а также hello **роль модуля чтения** toohello пользователя, а затем они могут просматривать все ресурсы автоматизации hello, а также выполнять задания runbook hello. Вы можете развернуть tooview hello раскрывающийся список пользователей роли, назначенные toohello.  
   
    ![Просмотр нескольких ролей](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Удаление пользователя
Вы можете удалить hello разрешение на доступ для пользователя, который не управляет hello учетной записи автоматизации или который больше не работает в организации hello. Следующие являются hello tooremove действия пользователя: 

1. Из hello **пользователей** колонки, назначение ролей выберите hello обратиться в tooremove.
2. Нажмите кнопку hello **удалить** кнопку в колонке сведения назначения hello.
3. Нажмите кнопку **Да** tooconfirm удаления. 
   
   ![Удаление пользователей](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Пользователь с назначенной ролью
Когда роль tooa, пользователь входит на tootheir учетной записи автоматизации, они могут просматривать теперь hello владелец учетной записи, перечисленной в списке hello **каталоги по умолчанию**. В порядке tooview hello учетной записи автоматизации, они были добавлены они необходимо перейти в каталог по умолчанию каталог toohello hello по умолчанию владельцем.  

![Каталог по умолчанию](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Возможности для пользователя с ролью оператора службы автоматизации
Когда пользователь, являющийся назначается представления роли оператора автоматизации toohello hello учетной записи автоматизации, которые им назначены, они могут только просмотр списка hello модулей Runbook, заданий и расписаний созданы в hello учетной записи автоматизации, но не могут просматривать их определения. Их можно запускать, останавливать, приостановить, возобновить сведения и осуществлять запланировать задание runbook hello. Hello пользователь не будет иметь доступа к ресурсам автоматизации tooother например конфигураций гибридных рабочих групп или узлы DSC.  

![Нет доступа к tooresourcres](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Когда hello пользователь выбирает hello runbook, hello команд tooview hello источника или изменить модуль runbook hello не предоставляются как роли оператора автоматизации hello не разрешает доступ toothem.  

![Нет доступа к tooedit runbook](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

Hello пользователь будет иметь доступ tooview и toocreate расписания, но не будет иметь доступ tooany другой тип ресурса.  

![Нет доступа к tooassets](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Этот пользователь также не имеет связанные с runbook веб-доступа tooview hello привязок

![Нет доступа к toowebhooks](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Настройки RBAC для учетной записи службы автоматизации с помощью Azure PowerShell
Доступ на основе ролей также может быть настроенный tooan учетной записи автоматизации с помощью следующих hello [командлетов Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).

• Командлет [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) выводит список всех ролей RBAC, доступных в Azure Active Directory. Можно использовать эту команду, а также hello **имя** toolist свойство Здравствуйте, все действия, которые могут быть выполнены для определенной роли.  
    **Пример**  
    ![Получение определения роли](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) списки назначений роли Azure AD RBAC на hello указан области. Без параметров эта команда возвращает все назначения ролей hello, сделанные на узле hello подписки. Используйте hello **ExpandPrincipalGroups** назначения доступа toolist параметра для hello указанного пользователя, а также группы hello hello пользователь является членом.  
    **Пример:** используйте hello следующая команда toolist, все пользователи hello и их роли в рамках учетной записи автоматизации.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Получение назначения роли](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [New AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign toousers, группы и приложения tooa определенной области доступа.  
    **Пример:** используйте hello следующая команда tooassign hello оператором «автоматизация» роль пользователя, в области действия учетных записей автоматизации hello.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Новое назначение роли](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Используйте [AzureRmRoleAssignment удаление](https://msdn.microsoft.com/library/mt603781.aspx) tooremove доступа для указанного пользователя, группы или приложений из определенной области.  
    **Пример:** используйте hello следующая команда tooremove hello пользователя из роли «Автоматизации оператор» hello в области действия учетных записей автоматизации hello.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

В hello выше примерах замените **входа идентификатор**, **идентификатор подписки**, **имя группы ресурсов** и **имя учетной записи автоматизации** с вашей сведения об учетной записи. Выберите **Да** при запросе tooconfirm перед продолжением tooremove назначение роли пользователя.   

## <a name="next-steps"></a>Дальнейшие действия
* Сведения о различных способов tooconfigure RBAC для автоматизации Azure, см. в разделе слишком[управление RBAC с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).
* Дополнительные сведения о различных способов toostart runbook см. в разделе [запуск runbook](automation-starting-a-runbook.md)
* Сведения о типах другим модулем runbook, см. в разделе слишком[типов runbook службы автоматизации Azure](automation-runbook-types.md)

