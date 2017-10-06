---
title: "aaaAzure образец скрипта CLI - Создание учетной записи пакетного | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание учетной записи пакетной службы"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Создать пакетную учетную запись с hello Azure CLI

Этот сценарий создает учетную запись пакетной службы Azure и показано, как различные свойства учетной записи hello можно запрашивать и обновлены.

## <a name="prerequisites"></a>Предварительные требования

Установка hello Azure CLI с помощью hello следуйте инструкциям в hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы еще не выполнена.

## <a name="batch-account-sample-script"></a>Пример скрипта учетной записи пакетной службы

При создании учетной записи пакетной по умолчанию ее вычислительные узлы назначения внутренне hello пакетной службы. Выделенных вычислительных узлов будет субъекта tooa отдельное ядро квоту и может проверить подлинность учетной записи hello, или с помощью Shared Key учетные данные или Azure Active Dirctory токена.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Учетная запись пакетной службы с использованием примера скрипта подписки пользователя

Вы можете также выбрать toohave пакетного создания его вычислительных узлов в своей подписке Azure.
Учетные записи, которые распределяют вычислительные узлы в подписке должны пройти проверку подлинности посредством маркера Azure Active Directory и hello вычислительные узлы выделенной будут приниматься Квота вашей подписки. toocreate учетную запись в этом режиме один необходимо указать ссылку хранилище ключей при создании учетной записи hello.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Очистка развертывания

После выполнения любого из hello выше примеры сценариев запуска hello, следующая команда tooremove группы ресурсов и все связанные ресурсы (включая массовых учетных записей, учетных записей хранилища Azure и Azure хранилищ ключей).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello следующие команды toocreate группы ресурсов, пакетную учетную запись и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документации.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | Создает учетную запись пакетной hello.  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | Обновляет свойства hello пакетной учетной записи.  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | Извлекает сведения о hello указана учетная запись пакета.  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Получает ключи доступа hello hello указана учетная запись пакета.  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Подлинность hello указан пакетная учетная запись для дальнейшего взаимодействия CLI.  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Создание учетной записи хранения. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Создает хранилище ключей. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Измените политику безопасности hello hello указанного ключа хранилища. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Удаляет группу ресурсов со всеми вложенными ресурсами. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные образцы сценариев CLI пакета можно найти в hello [документации пакета Azure CLI](../batch-cli-samples.md).
