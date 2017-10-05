---
title: "Развертывание шаблонов с помощью командной строки в стеке Azure | Документы Microsoft"
description: "Сведения об использовании интерфейса кросс платформенных командной строки (CLI) для развертывания шаблонов Azure стека."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: cd1b61899ead7b4e86a81125841c1b37d019280b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-in-azure-stack-using-the-command-line"></a>Развертывание шаблонов в Azure Stack с помощью командной строки
Использование командной строки для развертывания пакета средств разработки Azure стека шаблонов диспетчера ресурсов Azure. Шаблоны диспетчера ресурсов Azure, развертывание и предоставление все ресурсы для приложения в один, согласованной операции.

## <a name="before-you-begin"></a>Перед началом работы
 - [Установка и подключение](azure-stack-connect-cli.md) стек Azure с помощью Azure CLI
 - Загрузите файлы *azuredeploy.json* и *azuredeploy.parameters.json* из [Создание шаблона пример учетной записи хранилища](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).
 
## <a name="deploy-template"></a>Развертывание шаблона
Перейдите к папке, где эти файлы были загружены и выполните следующую команду для развертывания шаблона:

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

Эта команда выполняет развертывание шаблона в группу ресурсов **cliRG** в расположение по умолчанию для проверки Концепции стек Azure.

## <a name="validate-template-deployment"></a>Проверка шаблона-развертывания
Чтобы просмотреть эту группу ресурсов и учетную запись хранения, используйте следующие команды.

    azure group list

    azure storage account list

## <a name="next-steps"></a>Дальнейшие действия
[Управление разрешениями пользователей](azure-stack-manage-permissions.md)

