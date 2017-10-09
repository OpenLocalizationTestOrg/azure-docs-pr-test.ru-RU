---
title: "aaaConfigure Azure учетная запись запуска от | Документы Microsoft"
description: "Этот учебник поможет выполнить hello создания, тестирования и пример использования проверки подлинности субъекта безопасности в службе автоматизации Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "имя субъекта-службы, SetSPN, проверка подлинности Azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени
В этой статье показано, как tooconfigure автоматизации Azure учетной записи в hello портал Azure. toodo таким образом, используйте hello Запуск от имени учетной записи компонента tooauthenticate runbooks управление ресурсами в диспетчер ресурсов Azure и управления службами Azure.

При создании учетной записи автоматизации в hello портал Azure автоматически создавать две учетные записи:

* Учетная запись запуска от имени. Эта учетная запись создает субъект-службу в Azure Active Directory (Azure AD) и сертификат, Присваивает hello участника доступом на основе ролей (RBAC), управляющему ресурсы диспетчера ресурсов с помощью Runbook.
* Классическая учетная запись запуска от имени. Этой учетной записи отправляет сертификат управления, который будет использоваться toomanage управления службами или классические ресурсы с помощью модулей Runbook.

Требуется создание автоматической учетной записи упрощает процесс hello для вас и помогает быстро начать создание и развертывание toosupport модули Runbook автоматизации.

Используя учетную запись запуска от имени и классическую учетную запись, вы можете:

* Предоставить tooauthenticate стандартизованного Azure при управлении диспетчера ресурсов или ресурсов для службы управления из модулей Runbook в hello портал Azure.
* Автоматизация hello Использование глобальных Runbook, которые можно настроить в Azure предупреждения.

> [!NOTE]
> Hello [Azure integration функцию](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) с автоматизацией глобального модули Runbook требуется учетная запись автоматизации, для которой настроена учетная запись запуска от имени и классический учетной записи запуска. Можно выбрать учетную запись автоматизации, который уже определен учетные записи запуска от имени и классический запуска от имени или toocreate можно выбрать учетную запись автоматизации.
>  

В этой статье показано, как toocreate учетной записи автоматизации из hello портал Azure, обновить учетную запись службы автоматизации с помощью Azure PowerShell, управление конфигурацией учетной записи hello и проходить проверку подлинности в модули Runbook.

Перед началом создания учетной записи автоматизации, он toounderstand смысл и рассмотрите hello ниже:

* Создание учетной записи автоматизации не влияет на учетные записи автоматизации, могут уже созданных в классическом hello или модели развертывания диспетчера ресурсов.
* Hello процесс работает только для учетных записей автоматизации, создаваемые в hello портал Azure. Попытка toocreate учетную запись из классического портала Azure hello конфигурации учетной записи запуска от имени для hello не реплицируются.
* Если уже имеется Runbook и ресурсов (например, расписаниями и переменные) в месте toomanage классические ресурсы, и требуется tooauthenticate модулей Runbook с hello новой классический запуска от имени учетной записи, выполните одно из следующих hello.

  * toocreate классический запуска от имени учетной записи, следуйте инструкциям hello в разделе «Управление вашей учетной записи запуска от» hello. 
  * tooupdate существующей учетной записи, используйте hello PowerShell сценария в разделе «Обновление учетной записи автоматизации с помощью PowerShell» hello.
* tooauthenticate с помощью hello новый запуск от имени учетной записи и классический запуска как автоматизации необходимо существующие модули Runbook с hello пример кода, приведенный в разделе hello toomodify [примеры кода проверки подлинности](#authentication-code-examples).

    >[!NOTE]
    >Hello учетная запись запуска от имени — для проверки подлинности с помощью участника службы на основе сертификатов hello ресурсы диспетчера ресурсов. для проверки подлинности в службе управления ресурсами с сертификатом управления — Hello классический запись запуска от имени.

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Создание учетной записи автоматизации из hello портал Azure
В этом разделе создайте учетную запись службы автоматизации Azure из hello портал Azure, который в свою очередь, создает учетную запись запуска от имени и классический учетной записи запуска.

>[!NOTE]
>toocreate учетной записи автоматизации, необходимо быть членом роли администраторов службы hello или соадминистратором подписки hello, который предоставляет доступ toohello подписки. Кроме того, вы должны добавить подписку toothat пользователя экземпляром по умолчанию Active Directory. Hello не обязательно toobe назначенный привилегированной роли.
>
>Если вы не является членом экземпляра Active Directory hello подписки до добавления роли toohello соадминистратора подписки hello, вы будете добавлять tooActive каталог как Гость. В этом случае вы получите «у вас разрешения toocreate...» Предупреждение, hello **Добавление учетной записи автоматизации** колонку.
>
>Пользователи, добавленные в роль соадминистратора toohello сначала можно удалить из экземпляра Active Directory hello подписки и повторно добавлен toomake их полный пользователя в Active Directory. tooverify таких ситуаций с hello **Azure Active Directory** область в Azure портал, выбрав hello **пользователей и групп**, выбрав **всех пользователей** и после выбора Hello конкретного пользователя, при выборе **профиль**. Здравствуйте, значение hello **тип пользователя** атрибут профиля hello пользователи не должны быть равны **гостевой**.
>

1. Войдите в портал Azure с учетную запись, которая является членом роли администраторов подписки hello и соадминистратором подписки hello toohello.

2. Выберите элемент **Учетные записи службы автоматизации**.

3. На hello **учетные записи автоматизации** колонка, щелкните **добавить**.
Hello **Добавление учетной записи автоматизации** открывает колонку.

 ![Колонка «Добавить учетную запись автоматизации» Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > Если ваша учетная запись не является членом роли администраторов подписки hello и соадминистратором подписки hello, hello следующие предупреждения отображается на hello **Добавление учетной записи автоматизации** колонки:
   >
   >![Предупреждение в колонке "Добавление учетной записи службы автоматизации"](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. На hello **Добавление учетной записи автоматизации** колонки в hello **имя** введите имя для учетной записи автоматизации.

5. Если у вас есть несколько подписок, hello следующие:

    а. В разделе **подписки**, укажите один для новой учетной записи hello.

    b. В разделе **Группа ресурсов** щелкните **Создать** или **Использовать существующую**.

    c. В разделе **Расположение** выберите расположение центра обработки данных Azure.

6. В разделе **Создать учетную запись запуска от имени Azure** выберите **Да** и нажмите кнопку **Создать**.

   > [!NOTE]
   > При выборе не toocreate hello запуска от имени учетной записи, выбрав **нет**, выводится предупреждающее сообщение hello **Добавление учетной записи автоматизации** колонку. Несмотря на то, что hello учетная запись создается в hello портал Azure, он не имеет соответствующего удостоверение проверки подлинности в вашей классический или службы каталогов подписки для диспетчера ресурсов. Таким образом учетная запись hello имеет tooresources нет доступа в вашей подписке. В этом случае модули runbook, ссылающиеся на эту учетную запись, не смогут проходить проверку подлинности и выполнять задачи, используя ресурсы в соответствующих моделях развертывания.
   >
   > ![Предупреждающее сообщение в колонке «Добавить учетную запись автоматизации» hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > Кроме того поскольку hello участника-службы не создается, не назначена роль участника hello.
   >

7. Пока Azure создает учетную запись автоматизации hello, можно отслеживать ход выполнения hello в **уведомления** меню "hello".

### <a name="resources"></a>Ресурсы
Если hello учетную запись автоматизации успешно создана, некоторые ресурсы создаются автоматически. ресурсы Hello, приведены в hello, следующие две таблицы:

#### <a name="run-as-account-resources"></a>Ресурсы учетной записи запуска от имени

| Ресурс | Описание |
| --- | --- |
| Модуль Runbook AzureAutomationTutorial | Пример графический runbook, показано, как tooauthenticate с помощью hello учетная запись запуска от имени и получает все ресурсы диспетчера ресурсов hello. |
| Модуль Runbook AzureAutomationTutorialScript | Пример runbook PowerShell, который демонстрирует, как tooauthenticate с помощью hello учетная запись запуска от имени и возвращает все ресурсы диспетчера ресурсов hello. |
| AzureRunAsCertificate | Hello активов сертификат, который создается автоматически при создании учетной записи автоматизации или использовать hello следующий сценарий PowerShell для существующей учетной записи. Hello сертификата позволяет tooauthenticate с Azure, чтобы ресурсы диспетчера ресурсов Azure можно управлять из модулей Runbook. Hello сертификат имеет время существования в один год. |
| AzureRunAsConnection | ресурс подключения Hello, который создается автоматически при создании учетной записи автоматизации или использовать сценарий PowerShell hello существующей учетной записи. |

#### <a name="classic-run-as-account-resources"></a>Ресурсы классической учетной записи запуска от имени

| Ресурс | Описание |
| --- | --- |
| Модуль Runbook AzureClassicAutomationTutorial | Пример графический runbook, возвращает все виртуальные машины hello, которые создаются с помощью hello классической модели развертывания в подписке с помощью hello классический запуска от имени учетной записи (сертификат), а затем записывает имя виртуальной Машины hello и состояние. |
| Модуль Runbook AzureClassicAutomationTutorialScript | Пример runbook PowerShell, который получает все hello классические ВМ в подписке с помощью hello классический запуска от имени учетной записи (сертификат), а затем записывает hello имя виртуальной Машины и состояния. |
| AzureClassicRunAsCertificate | активов Hello автоматически создается сертификат, используйте tooauthenticate с Azure, чтобы вы могли управлять Azure классические ресурсы из модулей Runbook. Hello сертификат имеет время существования в один год. |
| AzureClassicRunAsConnection | средство автоматически созданное подключение Hello использовать tooauthenticate с Azure, чтобы вы могли управлять Azure классические ресурсы из модулей Runbook. |

## <a name="verify-run-as-authentication"></a>Тестирование проверки подлинности с помощью учетной записи запуска от имени
Выполните tooconfirm небольшой тест, который может успешно проверить подлинность с помощью hello новую учетную запись запуска.

1. Hello портал Azure откройте hello учетной записи автоматизации, которое было создано ранее.

2. Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.

3. Выберите hello **AzureAutomationTutorialScript** runbook, а затем нажмите кнопку **запустить** toostart hello runbook. происходят следующие события Hello:
 * Объект [задание runbook](automation-runbook-execution.md) создания hello **задания** колонке отображается, и состояние задания hello в hello **Сводка заданий** плитки.
 * состояние задания Hello начинается **в очереди**, означает, что он ожидает runbook worker в доступных toobecome облака hello.
 * состояние Hello становится **запуск** когда исполнитель утверждений hello задания.
 * состояние Hello становится **под управлением** при запуске hello runbook.
 * Задание runbook hello закончит работу, вы увидите состояние **завершено**.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee Здравствуйте подробные результаты hello runbook, щелкните hello **вывода** плитки.  
Hello **вывода** колонке отображается отображение этого модуля hello успешно проверку подлинности и возвращается список всех ресурсов, доступных в группе ресурсов hello.

5. Закрыть hello **вывода** toohello tooreturn колонке **Сводка заданий** колонку.

6. Закрыть hello **Сводка заданий** колонки и соответствующими hello **AzureAutomationTutorialScript** колонки runbook.

## <a name="verify-classic-run-as-authentication"></a>Тестирование проверки подлинности классической учетной записи запуска от имени
Выполните небольшой аналогичные тестирования tooconfirm, вы можете успешно проверять подлинность с помощью hello новой классический запуска от имени учетной записи.

1. Hello портал Azure откройте hello учетной записи автоматизации, которое было создано ранее.

2. Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.

3. Выберите hello **AzureClassicAutomationTutorialScript** runbook, а затем нажмите кнопку **запустить** слишком запустить hello runbook. происходят следующие события Hello:

 * Объект [задание runbook](automation-runbook-execution.md) создания hello **задания** колонке отображается, и состояние задания hello в hello **Сводка заданий** плитки.
 * состояние задания Hello начинается **в очереди**, означает, что он ожидает runbook worker в доступных toobecome облака hello.
 * состояние Hello становится **запуск** когда исполнитель утверждений hello задания.
 * состояние Hello становится **под управлением** при запуске hello runbook.
 * Задание runbook hello закончит работу, вы увидите состояние **завершено**.

    ![Тестирование модуля Runbook субъекта безопасности](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee Здравствуйте подробные результаты hello runbook, щелкните hello **вывода** плитки.  
Hello **вывода** колонке отображается отображение этого модуля hello успешно проверку подлинности и возвращается список всех классических ВМ в подписке hello.

5. Закрыть hello **вывода** toohello tooreturn колонке **Сводка заданий** колонку.

6. Закрыть hello **Сводка заданий** колонки и соответствующими hello **AzureAutomationTutorialScript** колонки runbook.

## <a name="managing-your-run-as-account"></a>Управление учетной записью запуска от имени
В некоторый момент до истечения срока действия учетной записи автоматизации, потребуется сертификат toorenew hello. Если вы считаете, что был скомпрометирован, hello учетная запись запуска от имени, можно удалить и создать его повторно. В этом разделе рассматриваются как tooperform этих операций.

### <a name="self-signed-certificate-renewal"></a>Обновление самозаверяющего сертификата
Hello самозаверяющий сертификат, созданный для hello учетная запись запуска от имени истекает один год после даты создания hello. Его можно обновить в любое время до истечения его срока действия. При обновлении, hello текущего действительного сертификата — зависимых tooensure, что все модули Runbook, помещаются в очередь до или активно работает и что аутентификации hello учетная запись запуска от имени, не подвергаются отрицательно. Hello сертификат остается действительным до истечения срока ее.

> [!NOTE]
> Если вы настроили ваш автоматизации Запуск от имени учетной записи toouse сертификат, выданный центром сертификации предприятия и использовать этот параметр, hello корпоративный сертификат будет заменен самозаверяющий сертификат.

toorenew hello сертификатов, hello следующие:

1. Откройте в hello портал Azure, учетная запись автоматизации hello.

2. На hello **учетной записи автоматизации** колонки в hello **свойства учетной записи** панели в разделе **параметры учетной записи**выберите **учетные записи запуска от**.

    ![Область свойств учетной записи службы автоматизации](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. На hello **учетные записи запуска от** свойства колонке выберите либо hello Запуск от имени учетной записи или hello классический запуска от имени, требуется сертификат toorenew hello.

4. На hello **свойства** колонке hello выбранную учетную запись, нажмите кнопку **продления сертификата**.

    ![Обновление сертификата для учетной записи запуска от имени](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. При продлении сертификата hello, отслеживания хода hello под **уведомления** меню "hello".

### <a name="delete-a-run-as-or-classic-run-as-account"></a>Удаление учетной записи запуска от имени или классической учетной записи запуска от имени
В этом разделе описываются как toodelete и повторного создания учетной записи запуска от имени или классический Запуск от имени. После выполнения этого действия сохраняется hello учетной записи автоматизации. После удаления учетной записи запуска от имени или классический запуска от имени, повторно создать его hello портал Azure.

1. Откройте в hello портал Azure, учетная запись автоматизации hello.

2. На hello **учетной записи автоматизации** колонке hello учетной записи «свойства» выберите **учетные записи запуска от**.

3. На hello **учетные записи запуска от** колонку свойств, выберите либо hello Запуск от имени учетной записи или классический запуска от имени учетной записи, которые должны toodelete. Затем на hello **свойства** колонке hello выбранную учетную запись, нажмите кнопку **удалить**.

 ![Удаление учетной записи запуска от имени](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Во время удаления учетной записи hello, отслеживания хода hello под **уведомления** меню "hello".

5. После удаления учетной записи hello, его можно повторно создать на hello **учетные записи запуска от** колонку свойств, выбрав hello создать параметр **Azure учетная запись запуска от имени**.

 ![Повторно создать hello автоматизации Запуск от имени учетной записи](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>Неправильные настройки
Некоторые элементы конфигурации, необходимые для hello toofunction учетная запись запуска от имени или классический Запуск от имени правильно может была удалена или создана неправильно во время начальной настройки. Hello элементы включают:

* ресурс сертификата,
* ресурс подключения,
* Учетная запись запуска от имени был удален из роли участника hello
* субъект-служба или приложение-служба в Azure AD,

В предыдущем hello и другие экземпляры неправильной настройки, приветствия учетной записи автоматизации обнаруживает hello изменяет и отображает состояние *неполный* на hello **учетные записи запуска от** колонку свойств для hello Учетная запись.

![Сообщение о том, что настройка учетной записи запуска от имени не завершена](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

При выборе hello запись запуска от имени учетной записи Здравствуйте, **свойства** отображаются hello следующие сообщение об ошибке:

![Предупреждение о том, что настройка учетной записи запуска от имени не завершена](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

Позволяет быстро устранить эти проблемы учетная запись запуска от имени, удаления и повторного создания учетной записи hello.

## <a name="update-your-automation-account-by-using-powershell"></a>Обновление учетной записи службы автоматизации с помощью PowerShell
Можно использовать существующую учетную запись автоматизации PowerShell tooupdate, если:

* Создание учетной записи автоматизации, но отклонить toocreate hello запуска от имени учетной записи.
* Ресурсы диспетчера ресурсов автоматизации toomanage учетной записи уже используется, и требуется tooupdate hello tooinclude hello запуска от имени учетной записи для проверки подлинности runbook.
* Учетная запись автоматизации toomanage классические ресурсы уже используется и нужно tooupdate его toouse hello классический запуска от имени учетной записи вместо создания новой учетной записи и переход к tooit Runbook и активов.   
* Требуется toocreate запуска от имени, а классические учетной записи запуска с помощью сертификата, выданного вашего центра сертификации предприятия (ЦС).

сценарий Hello имеет hello следующие предварительные требования:

* Hello сценарий может выполняться только в Windows 10 и Windows Server 2016 с модулями Azure Resource Manager 2.01 и более поздней версии. Более ранние версии Windows не поддерживаются.
* Azure PowerShell 1.0 или более поздней версии. Сведения о выпуске hello PowerShell 1.0 см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
* Учетная запись автоматизации, на которую ссылается как значение hello для hello *— AutomationAccountName* и *- ApplicationDisplayName* параметры в следующем скрипте PowerShell hello.

tooget hello значения для *SubscriptionID*, *ResourceGroup*, и *AutomationAccountName*, которой являются обязательными параметрами для скриптов hello, hello следующие:
1. В hello портал Azure, выберите учетную запись автоматизации на hello **учетной записи автоматизации** колонки, а затем выберите **все параметры**. 
2. На hello **все параметры** колонки в разделе **параметры учетной записи**выберите **свойства**. 
3. Запишите значения hello на hello **свойства** колонку.

![колонку «Свойства» учетной записи автоматизации Hello](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>Создание сценария PowerShell для учетной записи запуска от имени
Этот сценарий PowerShell поддерживает hello конфигурации.

* создание учетной записи запуска от имени с использованием самозаверяющего сертификата;
* создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата;
* создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата;
* Создайте учетную запись запуска от имени и классический учетной записи запуска с помощью самозаверяющего сертификата в облако Azure для государственных hello.

В зависимости от hello параметров настройки при выборе hello скрипт создает hello следующих элементов.

**Для учетной записи запуска от имени:**

* Создает Azure AD приложения toobe экспортируются вместе с любой hello самозаверяющий или enterprise открытый ключ сертификата, создает основной учетной записи службы для приложения hello в Azure AD и назначает hello роль участника для учетной записи hello в существующую подписка. Можно изменить этот параметр tooOwner или любая другая роль. Дополнительные сведения см. в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).
* Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureRunAsCertificate* в hello указана учетная запись автоматизации. Hello активов сертификат содержит закрытый ключ сертификата hello, используемого приложением hello Azure AD.
* Создает ресурс подключения автоматизации с именем *AzureRunAsConnection* в hello указана учетная запись автоматизации. ресурс-контейнер подключений Hello содержит идентификатор приложения hello, идентификатора клиента, идентификатор подписки и отпечаток сертификата.

**Для классической учетной записи запуска от имени Azure:**

* Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureClassicRunAsCertificate* в hello указана учетная запись автоматизации. Hello активов сертификат содержит закрытый ключ сертификата hello используемый сертификат управления hello.
* Создает ресурс подключения автоматизации с именем *AzureClassicRunAsConnection* в hello указана учетная запись автоматизации. ресурс-контейнер подключений Hello содержит имя подписки hello, идентификатор подписки и имя актива сертификатов.

>[!NOTE]
> При выборе любой из параметров для создания классических запуска от имени учетной записи, после выполнения сценария hello передачи hello открытый сертификат управления (CER-файл с расширением) toohello хранения для подписки hello этой учетной записи автоматизации hello был создан в.
> 

tooexecute Здравствуйте сценарий и передать сертификат hello, hello следующие:

1. Сохраните следующий сценарий на компьютере hello. В этом примере, сохраните его с именем файла hello *New RunAsAccount.ps1*.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. На компьютере откройте меню **Пуск** и запустите с повышенными правами **Windows PowerShell**.

3. Из hello повышенными оболочка командной строки PowerShell, toohello откройте папку, содержащую hello скрипт, созданный на шаге 1.

4. Выполните сценарий hello, используя значения параметров hello hello конфигурации, требуемую.

    **Создание учетной записи запуска от имени с использованием самозаверяющего сертификата**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Создание учетной записи запуска от имени и классический учетной записи запуска с помощью самозаверяющего сертификата в облако Azure для государственных hello**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > После выполнения сценария hello, появится запрос tooauthenticate с Azure. Войдите с учетной записью, которая является членом роли администраторов подписки hello и соадминистратором подписки hello.
    >
    >

После успешного выполнения сценария hello Обратите внимание hello следующее:
* При создании классического учетной записи запуска с общей самозаверяющего сертификата (CER-файл), hello скрипт создает и сохраняет его toohello в папке временных файлов на компьютере в пользовательском профиле hello *%USERPROFILE%\AppData\Local\Temp*, мы использовали сеанс PowerShell tooexecute hello.
* Если вы создали классическую учетную запись запуска от имени с использованием открытого корпоративного сертификата (CER-файл), используйте этот сертификат. Следуйте инструкциям hello [передачи toohello сертификата API управления классический портал Azure](../azure-api-management-certs.md)и последующей проверки hello конфигурации учетных данных с ресурсами службы управления с помощью hello [пример кода tooauthenticate с ресурсами службы управления](#sample-code-to-authenticate-with-service-management-resources). 
* Если вы уже сделали *не* создания классических учетной записи запуска, проверки подлинности в ресурсах диспетчера ресурсов и проверка конфигурации hello учетных данных с помощью hello [пример кода для проверки подлинности с помощью службы управления ресурсы](#sample-code-to-authenticate-with-resource-manager-resources).

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>Образец кода tooauthenticate с ресурсами диспетчера ресурсов
Можно использовать следующие hello обновлен пример кода, взяты из hello *AzureAutomationTutorialScript* пример runbook, tooauthenticate с помощью hello запуска от имени учетной записи toomanage диспетчера ресурсов ресурсов с помощью модулей Runbook.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

toohelp вы tooeasily работы между несколькими подписками, hello скрипт включает два дополнительных строк кода, поддерживающие создание ссылок на контекст подписки. Переменная ресурса с именем *SubscriptionId* содержит идентификатор hello hello подписки. После hello `Add-AzureRmAccount` инструкции командлет hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) командлет устанавливается с набором параметров hello *- SubscriptionId*. Если имя переменной hello слишком универсален, можно зашифрованного tooinclude префикс или использовать другой именования toomake соглашение о его проще tooidentify. Кроме того, можно использовать набор параметров hello *- SubscriptionName* вместо *- SubscriptionId* с соответствующей переменной активов.

Здравствуйте, командлет, который используется для проверки подлинности в hello runbook `Add-AzureRmAccount`, использует hello *ServicePrincipalCertificate* набор параметров. Проверяет подлинность с помощью hello службы субъекта сертификата, не hello учетные данные.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>Образец кода tooauthenticate с ресурсами службы управления
Можно использовать следующий код обновленный образец, который будет взято из hello hello *AzureClassicAutomationTutorialScript* пример runbook, tooauthenticate с помощью hello классический запуска от имени учетной записи toomanage классические ресурсы с вашей модули Runbook.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>Дальнейшие действия
* [Объекты приложения и субъекта-службы в Azure Active Directory](../active-directory/active-directory-application-objects.md)
* [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md)
* [Общие сведения о сертификатах для облачных служб Azure](../cloud-services/cloud-services-certs-create.md)
