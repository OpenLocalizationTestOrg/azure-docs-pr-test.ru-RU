---
title: "кластер aaaHPC пакет с Azure Active Directory | Документы Microsoft"
description: "Узнайте, как кластер toointegrate 2016 пакета HPC в Azure с помощью Azure Active Directory"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Управление кластером пакета HPC в Azure с помощью Azure Active Directory
[Пакет Microsoft HPC 2016](https://technet.microsoft.com/library/cc514029) поддерживает интеграцию с [Azure Active Directory](../../active-directory/index.md) (Azure AD) для администраторов, развертывающих кластер пакета HPC в Azure.



Выполните действия hello в этой статье для hello следующие задачи верхнего уровня. 
* Интеграция кластера пакета HPC с клиентом Azure AD.
* Планирование заданий кластера HPC в Azure и управление ими. 

Интеграция решения кластера HPC Pack в Azure AD соответствует toointegrate стандартные действия, другие приложения и службы. В этой статье предполагается, что вы знакомы с основами пользовательского управления в Azure AD. Дополнительные сведения и фона в разделе hello [документации Azure Active Directory](../../active-directory/index.md) и hello следующем разделе.

## <a name="benefits-of-integration"></a>Преимущества интеграции


Azure Active Directory (Azure AD) представляет собой несколькими клиентами облачных каталогами и удостоверениями, предоставляющий доступ единого входа (SSO) toocloud решения.

Интеграция кластере HPC Pack в Azure AD может помочь достичь следующих целей hello:

* Удалите hello традиционных контроллера домена Active Directory из кластера HPC Pack hello. Это может помочь снизить затраты на обслуживание hello кластера в том случае, если это не требуется для вашей компании и ускорить процесс развертывания hello hello.
* Использовать hello следующие преимущества, которые попадают в Azure AD:
    *   Единый вход 
    *   С помощью локальных AD удостоверения для hello кластера HPC Pack в Azure 

    ![Среда Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Предварительные требования
* **Кластер пакета HPC 2016, развернутый на виртуальных машинах Azure.** Дополнительные сведения см. в статье [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md) (Развертывание кластера пакета HPC 2016 в Azure). Требуется DNS-имя головного узла hello hello и hello учетные данные администратора кластера для выполнения шагов hello в этой статье.

  > [!NOTE]
  > Интеграция Azure Active Directory не поддерживается в версиях пакета HPC до версии HPC 2016.



* **Клиентский компьютер** -требуется Windows или Windows Server клиентского компьютера слишком запущена HPC Pack клиентских служебных программ. Если требуется только toouse hello HPC Pack веб-портала или API-интерфейса REST toosubmit задания, можно использовать любой клиентский компьютер по своему усмотрению.

* **Клиентские служебные программы пакета HPC** -установки на клиентском компьютере hello, доступные из центра загрузки Майкрософт hello hello бесплатный установочный пакет с помощью клиентских служебных программ пакета HPC hello.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>Шаг 1: Регистрация сервера кластера HPC hello с клиентом Azure AD
1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Нажмите кнопку **Active Directory** в hello в левом меню и нажмите кнопку hello нужный каталог в вашей подписке. Необходимо иметь разрешение tooaccess ресурсы в каталоге hello.
3. Щелкните **Пользователи** и убедитесь, что уже создана или настроена учетная запись пользователя.
4. Щелкните **Приложения** > **Добавить** и выберите команду **Добавить приложение, разрабатываемое моей организацией**. Введите следующую информацию в мастере hello hello:
    * **Имя** — HPCPackClusterServer.
    * **Тип** — выберите **Веб-приложение и/или веб-API**.
    * **URL-адрес входа**- hello базовый URL-адрес для образца hello, который по умолчанию`https://hpcserver`
    * **URI кода приложения** - `https://<Directory_name>/<application_name>`. Замените `<Directory_name`> с hello полное имя вашего клиента Azure AD, например, `hpclocal.onmicrosoft.com`и замените `<application_name>` с именем hello были выбраны.

5. После добавления приложение hello щелкните **Настройка**. Настройте hello следующие свойства:
    * Для параметра **Приложение является мультитенантным** укажите значение **Да**.
    * Выберите **Да** для **назначения пользователя. приложение требуется tooaccess**.

6. Щелкните **Сохранить**. После того, как сохранение будет завершено, щелкните **Управление манифестом**. Это действие скачивает файл нотации объектов JavaScript (JSON) манифеста приложения. Изменить манифест загружаются hello, найдя hello `appRoles` установку и добавление hello следующие роли приложения:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Сохраните файл hello. Hello портала щелкните **управление манифеста** > **отправить манифест**. Затем вы можете передать hello измененного манифест.
8. Щелкните **Пользователи**, выберите пользователя и щелкните **Назначить**. Назначьте один из hello доступные роли (HpcUsers или HpcAdminMirror) toohello пользователя. Повторите этот шаг, с помощью дополнительных пользователей в каталоге hello. Общие сведения о пользователях кластера см. в статье [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx) (Управление пользователями кластера).

   > [!NOTE] 
   > toomanage пользователей, мы рекомендуем использовать колонки предварительной версии Azure Active Directory hello в hello [портал Azure](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>Этап 2: Регистрация клиента кластера HPC hello с клиентом Azure AD

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Нажмите кнопку **Active Directory** в hello в левом меню и нажмите кнопку hello нужный каталог в вашей подписке. Необходимо иметь разрешение tooaccess ресурсы в каталоге hello.
3. Щелкните **Приложения** > **Добавить** и выберите команду **Добавить приложение, разрабатываемое моей организацией**. Введите следующую информацию в мастере hello hello:

    * **Имя** — HPCPackClusterClient.
    * **Тип** — выберите **Native Client Apllication** (Собственное клиентское приложение).
    * **URI перенаправления** - `http://hpcclient`.

4. После добавления приложение hello щелкните **Настройка**. Копировать hello **идентификатор клиента** значение и сохраните его. Оно понадобится позже при настройке приложения.

5. В **разрешения приложений tooother**, нажмите кнопку **добавить приложение**. Поиск и добавление приложения HpcPackClusterServer hello (созданного на шаге 1).

6. В hello **делегированные разрешения** раскрывающийся список, выберите **HpcClusterServer доступа**. Нажмите кнопку **Сохранить**.


## <a name="step-3-configure-hello-hpc-cluster"></a>Шаг 3: Настройка кластера HPC hello

1. Подключите головного узла HPC Pack 2016 toohello в Azure.

2. Запустите HPC PowerShell.

3. Выполните следующую команду hello.

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    где:

    * `AADTenant`Указывает имя клиента Azure AD hello, такие как`hpclocal.onmicrosoft.com`
    * `AADClientAppId`Указывает идентификатор hello клиента для приложения hello, созданный на шаге 2.

4. Перезапустите службу HpcSchedulerStateful hello.

    В кластере с несколькими головного узла можно выполнить следующие команды PowerShell hello головного узла tooswitch hello первичной реплике для службы HpcSchedulerStateful hello hello:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>Шаг 4: Управление и отправлять задания с приветствия клиента

tooinstall hello HPC Pack клиентские служебные программы на компьютере, загрузить файлы установки HPC Pack 2016 (полная установка) из центра загрузки Майкрософт hello. При установке hello, выберите вариант установки hello для hello **клиентских служебных программ пакета HPC**.

hello сертификат, используемый во время установки tooprepare hello клиентский компьютер, [настройка кластера HPC](hpcpack-2016-cluster.md) на клиентском компьютере hello. Использовать стандартные Windows сертификатов управления процедуры tooinstall hello открытый сертификат toohello **Сертификаты — текущий пользователь** > **доверенные корневые центры сертификации** хранения. 

Теперь можно выполнять команды hello пакета HPC или использовать графический Интерфейс диспетчера заданий HPC Pack hello toosubmit и управление заданиями кластера с помощью учетной записи hello Azure AD. Параметры отправки задания. в разделе [tooan HPC отправки заданий HPC Pack кластер в Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> При запуске кластера HPC Pack toohello tooconnect в Azure для hello впервые, откроется всплывающие окна. Введите ваш toolog учетные данные Azure AD в. токен Hello сохраняется в кэше. Более поздние версии кластера toohello подключений в Azure используйте hello в кэше маркер, если не снят изменения проверки подлинности или hello в кэше.
>
  
Например после выполнения предыдущих шагов hello, можно запросить для заданий с локального клиента следующим образом:

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Полезные командлеты для отправки заданий с интеграцией Azure AD 

### <a name="manage-hello-local-token-cache"></a>Управление локальным кэшем токенов hello

HPC Pack 2016 предоставляет два новых командлета HPC PowerShell toomanage hello локального маркера кэша. Их можно использовать для отправки заданий в неинтерактивном режиме. См. следующий пример hello.

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Задать hello учетные данные для отправки заданий с помощью учетной записи hello Azure AD 

В некоторых случаях может потребоваться задания hello toorun записью кластера HPC hello (присоединенных к домену кластер HPC, запуск от имени пользователя в одном домене, не присоединенных к домену кластер HPC, запуск от имени одного локального пользователя на головном узле hello).

1. Используйте следующие учетные данные hello tooset команды hello:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. Затем отправьте задание hello следующим образом. Hello задания или задачи в разделе выполняется $localUser на hello вычислительных узлов.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Если `–Credential` не указан с `Submit-HpcJob`, hello задания или задачи выполняется локальный пользователь сопоставленных как hello учетной записи Azure AD. (кластер HPC hello создает локального пользователя с hello одинаковые имена, как hello задачу hello toorun учетной записи Azure AD).
    
3. Задайте расширенные данные для учетной записи Azure AD hello. Это полезно при выполнении задания MPI на узлах Linux с помощью учетной записи hello Azure AD.

   * Задайте расширенные данные для hello саму учетную запись Azure AD

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Укажите подробные сведения и выполните задание от имени пользователя кластера HPC
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

