---
title: "гибкий пул Azure SQL пример перемещения базы данных SQL aaaCLI | Документы Microsoft"
description: "Azure CLI пример сценария toomove базы данных SQL в пуле эластичных БД SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a>Использовать toomove CLI из базы данных Azure SQL в пуле эластичных БД SQL

В этом примере сценария Azure CLI создает два пула эластичных и перемещает базу данных Azure SQL из одного гибкий пул SQL в другой гибкий пул SQL и затем перемещает hello базы данных вне уровня производительности для одной базы данных Azure tooa эластичного пула. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Очистка развертывания

После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Создает логический сервер, на котором размещена база данных или эластичный пул. |
| [az sql elastic-pools create](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Создает пул эластичных БД в логическом сервере hello. |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#create) | Создает на логическом сервере отдельную базу данных или базу данных в составе пула. |
| [az sql db update](https://docs.microsoft.com/cli/azure/sql/db#update) | Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Удаляет группу ресурсов со всеми вложенными ресурсами. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные образцы сценариев CLI базы данных SQL можно найти в hello [документации по базе данных SQL Azure](../sql-database-cli-samples.md).


