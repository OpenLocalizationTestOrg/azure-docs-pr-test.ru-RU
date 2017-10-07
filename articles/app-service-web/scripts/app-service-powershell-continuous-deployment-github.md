---
title: "Пример сценария PowerShell - aaaAzure Создание веб-приложения с непрерывным развертыванием из GitHub | Документы Microsoft"
description: "Пример сценария Azure PowerShell для создания веб-приложения с непрерывным развертыванием из GitHub."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a>Создание веб-приложения с непрерывным развертыванием из GitHub

Этот пример скрипта создает веб-приложение в службе приложений со связанными ресурсами, а затем настраивает непрерывное развертывание из репозитория GitHub. Дополнительные сведения о развертывании GitHub без непрерывного развертывания см. в статье [Создание веб-приложения и развертывание кода из GitHub](app-service-powershell-deploy-github.md).

При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview). Кроме того, убедитесь в следующем.

- Соединение с Azure был создан с помощью hello `az login` команды.
- код приложения Hello находится в открытые или закрытые репозитории GitHub, что вы являетесь владельцем.
- Вы [создали маркер доступа в учетной записи GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Создает план службы приложений. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Создает веб-приложение. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/set-azurermresource) | Изменяет ресурс в группе ресурсов. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).

Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).
