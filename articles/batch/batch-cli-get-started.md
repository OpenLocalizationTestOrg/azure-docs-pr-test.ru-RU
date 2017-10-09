---
title: "aaaGet работы с Azure CLI для пакета | Документы Microsoft"
description: "Получить краткое введение toohello пакетные команды в Azure CLI для управления ресурсами Azure пакетной службы"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Управление ресурсами пакетной службы с помощью Azure CLI

Hello Azure CLI 2.0 — это новый интерфейс командной строки Azure для управления ресурсами Azure. Его можно использовать в Windows, Linux и macOS. Azure CLI 2.0 оптимизирована для управления и администрирования из командной строки hello ресурсов Azure. Можно использовать toomanage hello Azure CLI, учетными записями пакетной службы Azure и toomanage ресурсы, такие как пулы, заданий и задач. С помощью hello Azure CLI, можно создать сценарий многие hello hello такие же задачи, выполняемые с помощью API-интерфейсы пакета, портал Azure и командлеты PowerShell для пакета.

В этой статье содержатся общие сведения об использовании [Azure CLI версии 2.0](https://docs.microsoft.com/cli/azure/overview) с пакетной службой. В разделе [Приступая к работе с Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Общие сведения об использовании hello CLI с Azure.

Корпорация Майкрософт рекомендует использовать последнюю версию hello hello Azure CLI, версии 2.0. Дополнительные сведения о ней см. в записи блога о [выпуске общедоступной версии Azure CLI 2.0](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).

## <a name="set-up-hello-azure-cli"></a>Настройка hello Azure CLI

tooinstall hello Azure CLI выполните hello действия, описанные в [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).

> [!TIP]
> Рекомендуется обновить установленную Azure CLI часто tootake преимуществами службы обновления и улучшения.
> 
> 

## <a name="command-help"></a>Справка по командам

Можно отобразить текст справки для всех команд в hello Azure CLI путем добавления `-h` toohello команды. Другие параметры следует опустить. Например:

* tooget справку для hello `az` , введите:`az -h`
* tooget список всех команд пакета в hello CLI, используйте:`az batch -h`
* tooget справку по созданию учетной записи пакета, введите:`az batch account create -h`

Если вы сомневаетесь, использовать hello `-h` справки tooget параметр командной строки на любую команду Azure CLI.

> [!NOTE]
> Более ранних версиях hello Azure CLI используется `azure` toopreface команду CLI. В версии 2.0 все команды теперь начинаются с приставки `az`. Быть убедиться, что tooupdate сценариев toouse hello новый синтаксис с версии 2.0.
>
>  

Кроме того, ссылаются toohello Azure CLI справочную документацию для сведений о [команды Azure CLI для пакета](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Вход в систему и проверки подлинности

toouse hello Azure CLI с использованием пакета, нужно toolog в и проверку подлинности. Существует два простых шагов toofollow:

1. **Войдите в Azure.** Вход в Azure дает доступ команд tooAzure диспетчера ресурсов, включая [обновления пакета управления](batch-management-dotnet.md) команд.  
2. **Войдите в учетную запись пакетной службы.** Вход в ваш пакет учетной записи позволяет получить доступ к командам tooBatch службы.   

### <a name="log-in-tooazure"></a>Войдите в tooAzure

Существует несколько способов toolog в Azure, подробно описаны в [войдите с помощью Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Интерактивный вход.](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in) Войти интерактивном режиме при выполнении команды Azure CLI самостоятельно hello командной строке.
2. [Вход с использованием субъекта-службы.](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal) Используйте этот способ, если вы выполняете команды Azure CLI из скрипта или приложения.

В целях hello данной статьи мы Показать как toolog в Azure интерактивном режиме. Тип [входа az](https://docs.microsoft.com/cli/azure/#login) hello в командной строке:

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

Hello `az login` команда возвращает токен, можно использовать tooauthenticate, как показано ниже. Следуйте инструкциям hello tooopen веб-страницы и отправка маркера tooAzure hello:

![Войдите в tooAzure](./media/batch-cli-get-started/az-login.png)

Примеры Hello, перечисленные в hello [образцы сценариев оболочки](#sample-shell-scripts) статьи также показать как toostart сеанс Azure CLI, интерактивный вход в Azure. После входа, можно вызвать toowork команд с ресурсами пакета управления, включая учетные записи пакета, ключи, пакеты приложений и квоты.  

### <a name="log-in-tooyour-batch-account"></a>Войдите в tooyour пакетной учетной записи

toouse hello Azure CLI toomanage пакет ресурсов, таких как пулы, заданий и задач, должны toolog в вашу учетную запись пакета и пройти проверку подлинности. использовать toolog в toohello пакетная служба hello [учетную запись для входа пакетного az](https://docs.microsoft.com/cli/azure/batch/account#login) команды. 

Проверку подлинности в учетной записи пакетной службы можно пройти двумя способами:

- **Проверка подлинности Azure Active Directory (Azure AD).** 

    Проверки подлинности в Azure AD является использование hello Azure CLI с использованием пакета по умолчанию hello и рекомендуется для большинства сценариев. 
    
    При входе в tooAzure интерактивном режиме, как описано в предыдущем разделе hello, учетные данные кэшируются, поэтому hello Azure CLI можно входа в систему tooyour пакетной учетной записи, используя те же учетные данные. При входе в tooAzure участника службы с помощью этих учетных данных, также используется toolog в tooyour пакетной учетной записи.

    Преимущество Azure AD заключается в том, что эта служба предоставляет управление доступом на основе ролей (RBAC). С RBAC доступа пользователя зависит от назначенной им роли, а не того, является ли они имеют hello ключи учетной записи. В этом случае управлять ключами не нужно. Вы просто назначаете роли RBAC, и Azure AD управляет параметрами доступа и проверки подлинности вместо вас.  

    Проверка подлинности с помощью Azure AD является обязательным, если вы создали учетной записью пакетной службы Azure с помощью режима выделения пула задать too'User подписки ". 

    toolog в tooyour пакетной учетной записи с помощью Azure AD, вызовите hello [учетную запись для входа пакетного az](https://docs.microsoft.com/cli/azure/batch/account#login) команды: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Проверка подлинности на основе общего ключа.**

    [Проверка подлинности с общим ключом](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) использует tooauthenticate команды Azure CLI для hello ключи доступ к учетной записи пакетной службы.

    При создании сценариев Azure CLI tooautomate вызывающий пакетные команды, можно использовать проверку подлинности Shared Key или основной службой Azure AD. В некоторых случаях проверку подлинности на основе общего ключа реализовать проще, чем создать субъект-службу.  

    toolog с помощью проверки подлинности Shared Key, включают hello `--shared-key-auth` hello командной строке:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

Примеры Hello, перечисленные в hello [образцы сценариев оболочки](#sample-shell-scripts) разделе показано, как toolog в вашу учетную запись пакета с hello Azure CLI с помощью Azure AD и общим ключом.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Использование шаблонов интерфейса командной строки для пакетной службы Azure и передачи файлов (предварительная версия)

Hello Azure CLI toorun пакетного задания узел узел можно использовать без написания кода. Пакетные файлы шаблона поддерживают создание пулов, заданий и задач с помощью hello Azure CLI. Можно также использовать входные файлы hello Azure CLI tooupload Задание учетной записи хранилища Azure toohello, связанной с hello учетная запись пакетной службы и загрузки выходных файлов задания из него. См. дополнительные сведения об [использовании шаблонов интерфейса командной строки для пакетной службы Azure и передаче файлов (предварительная версия)](batch-cli-templates.md).

## <a name="sample-shell-scripts"></a>Примеры скриптов оболочки

Примеры сценариев Hello перечислены в hello после Показать таблицу как toouse Azure CLI команды с помощью пакетной службы hello и общие задачи управления пакетной службы tooaccomplish. Эти примеры сценариев охватить многие hello команд, доступных в hello Azure CLI для пакета. 

| Скрипт | Примечания |
|---|---|
| [Создание учетной записи пакетной службы](./scripts/batch-cli-sample-create-account.md) | Создает учетную запись пакетной службы и связывает ее с учетной записью хранения. |
| [Добавление приложения](./scripts/batch-cli-sample-add-application.md) | Добавляет приложение и передает его упакованные двоичные файлы.|
| [Управление пулами пакетной службы](./scripts/batch-cli-sample-manage-pool.md) | Демонстрирует создание пулов, изменение размера пулов и управление ими. |
| [Выполнение задания и задач с помощью пакетной службы](./scripts/batch-cli-sample-run-job.md) | Демонстрирует выполнение задания и добавление задач. |

## <a name="json-files-for-resource-creation"></a>JSON-файлы для создания ресурса

При создании пакета ресурсы, такие как пулы и задания, можно указать файл JSON, содержащий конфигурации нового ресурса hello вместо передачи его параметров в виде параметров командной строки. Например:

```azurecli
az batch pool create my_batch_pool.json
```

Вы можете создать больше всего ресурсов пакета, используя только параметры командной строки, некоторые функции требуют указывать файл формата JSON, содержащий сведения о ресурсах hello. Например необходимо использовать файл JSON, если toospecify файлы ресурсов для задачи запуска.

hello toosee синтаксис JSON требуется toocreate ресурса см. в toohello [Справочник по API REST пакета] [ rest_api] документации. Каждый «добавить *тип ресурса*» раздела hello Справочник по REST API содержит примеры сценариев JSON для создания этого ресурса. Эти примеры сценариев JSON можно использовать как шаблоны для toouse файлы JSON с hello Azure CLI. Например, слишком относится hello toosee синтаксис JSON для создания пула[добавить учетную запись пула tooan][rest_add_pool].

Пример скрипта указания файла JSON см. в статье [Выполнение заданий в пакетной службе Azure с помощью Azure CLI](./scripts/batch-cli-sample-run-job.md).

> [!NOTE]
> При указании JSON-файла при создании ресурса, учитываются любые другие параметры, указываемые в командной строке hello для этого ресурса.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Эффективные запросы для ресурсов пакетной службы

Каждый тип ресурса пакетной службы поддерживает команду `list` , которая запрашивает учетную запись пакетной службы и предоставляет списки ресурсов заданного типа. Например можно составить список пулов hello в вашей учетной записи и hello задач задания:

```azurecli
az batch pool list
az batch task list --job-id job001
```

При выполнении запроса hello пакетная служба с `list` операции, можно указать toolimit hello OData предложение объем возвращаемых данных. Так как все фильтрация выполняется стороне сервера, только данные hello запросов пересекает hello сети. Использование пропускной способности toosave этих предложений (и поэтому время) при выполнении операции списка.

Hello следующей таблице описываются предложения hello OData, поддерживаемые hello пакетной службы.

| Предложение | Описание |
|---|---|
| `--select-clause [select-clause]` | Возвращает подмножество свойств для каждой сущности. |
| `--filter-clause [filter-clause]` | Возвращает только сущности, которые соответствуют hello указано выражение OData. |
| `--expand-clause [expand-clause]` | Получает сведения о сущности hello в базовой один вызов REST. Hello разверните предложение в настоящее время поддерживает только hello `stats` свойство. |

Для образца сценарии, показано, как toouse предложение OData см [запуска задания и задач с использованием пакета](./scripts/batch-cli-sample-run-job.md).

Дополнительные сведения о выполнении запросов эффективный списка с предложениями OData см. в разделе [эффективно запрашивать hello пакетной службы Azure](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Советы по устранению неполадок

Hello следующие советы могут помочь при устранении неполадок Azure CLI:

* Используйте `-h` tooget **текст справки** для любую команду CLI
* Используйте `-v` и `-vv` toodisplay **verbose** выходные данные команды. Здравствуйте, когда `-vv` флаг включен, hello Azure CLI отображает hello фактических запросов и ответов REST. Эти параметры удобно использовать для просмотра полного вывода ошибок.
* Можно просмотреть **команды выходные данные в формате JSON** с hello `--json` параметр. Например, параметр `az batch pool show pool001 --json` отображает свойства элемента pool001 в формате JSON. Можно скопировать и изменить этот toouse выходные данные в `--json-file` (см. [файлы JSON](#json-files) ранее в этой статье).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* Hello [форум по пакетной] [ batch_forum] отслеживается по членам команды в пакете. Задавайте вопросы на форуме, если у вас возникнут проблемы или вам потребуется справочная информация по какой-либо операции.

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о hello Azure CLI см. в разделе hello [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).
* Дополнительные сведения о ресурсах пакетной службы см. в статье [Разработка решений для крупномасштабных параллельных вычислений с использованием пакетной службы](batch-api-basics.md).
* Дополнительные сведения об использовании пулов toocreate шаблоны пакета, заданий и задач без написания кода см. в разделе [использовать шаблоны CLI пакета Azure и передача файлов (Предварительная версия)](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
