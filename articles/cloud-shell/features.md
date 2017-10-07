---
title: "возможности оболочки облака (Предварительная версия) aaaAzure | Документы Microsoft"
description: "Обзор функций Azure Cloud Shell."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Функции и средства Azure Cloud Shell
Azure облачной оболочки является toomanage взаимодействие на основе браузера оболочки и разработке ресурсов Azure.

Облако оболочки предлагает браузер, доступный, предварительно настроенных качества оболочки для управления ресурсами Azure без издержек hello установки, управления версиями, и обслуживание компьютера самостоятельно.

Cloud Shell подготавливает компьютеры по запросу, в результате чего состояние компьютера не сохраняется между сеансами. Поскольку Cloud Shell создана для интерактивных сеансов, оболочки автоматически завершают работу после 20 минут бездействия.

## <a name="bash-in-cloud-shell"></a>Bash в Cloud Shell
### <a name="tools"></a>Средства
|Категория   |Имя   |
|---|---|
|Интерпретатор оболочки Linux|Bash<br> sh               |
|Инструменты Azure            |[Azure CLI 2.0](https://github.com/Azure/azure-cli) и [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard)     |
|Текстовые редакторы           |vim<br> nano<br> emacs       |
|Система управления версиями         |git                    |
|Инструменты сборки            |make<br> maven<br> npm<br> pip         |
|Контейнеры             |[Docker CLI](https://github.com/docker/cli)/[Компьютер Docker](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Draft](https://github.com/Azure/draft)<br> [Интерфейс командной строки DC/OS](https://github.com/dcos/dcos-cli)         |
|Базы данных              |Клиент MySQL<br> Клиент PostgreSQL<br> [Служебная программа sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Другие                  |Клиент iPython<br> [Интерфейс командной строки Cloud Foundry](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Поддержка языков
|язык   |Version (версия)   |
|---|---|
|.NET       |1.01       |
|Go         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 и 3.5 (по умолчанию)|

## <a name="secure-automatic-authentication"></a>Безопасная автоматическая аутентификация
Облако оболочки безопасно и автоматически выполняет проверку подлинности доступа к учетной записи для hello Azure CLI 2.0.

## <a name="azure-files-persistence"></a>Сохраняемость файлов Azure
Поскольку Cloud Shell выделяется по запросу с использованием временного компьютера, файлы за пределами каталога $Home и сведения о состоянии компьютера не сохраняются между сеансами.
файлы toopersist во всех сеансах обходов оболочки облака через подключение файла Azure отправляемого при первом запуске.
По завершении настройки Cloud Shell будет автоматически присоединять хранилище для всех будущих сеансов.

[Дополнительные сведения о присоединении tooCloud общие папки файлов Azure оболочки.](persisting-shell-storage.md)

## <a name="next-steps"></a>Дальнейшие действия
[Краткое руководство по Cloud Shell](quickstart.md) <br>
[Подробное описание Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) <br>