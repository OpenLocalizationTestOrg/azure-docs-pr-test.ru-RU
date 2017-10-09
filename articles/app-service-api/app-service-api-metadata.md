---
title: "метаданные приложения API службы aaaApp для API обнаружения и создания кода | Документы Microsoft"
description: "Узнайте, как использовать Swagger метаданные toofacilitate API обнаружения и создания кода в приложениях API в службе приложений Azure."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>Метаданные приложений API службы приложений для обнаружения API и создания кода
Поддержка метаданных API [Swagger 2.0](http://swagger.io/) встроена в приложения API службы приложений. Нет toouse Swagger, но если она используется, можно воспользоваться преимуществами компоненты приложения API, облегчающие обнаружение и использование.   

## <a name="swagger-endpoint"></a>Конечная точка Swagger
Можно указать конечную точку, которая предоставляет метаданные Swagger 2.0 JSON для приложения API в свойстве API приложение hello. Конечная точка Hello может быть относительным toohello базовый URL-адрес приложения hello API или абсолютный URL-адрес. Вне приложения hello API может указывать абсолютный URL-адреса. 

Большое количество подчиненных клиентов (для примера, создание кода в Visual Studio и PowerApps «Добавить API» потока), hello URL-адрес должен быть общедоступным (не защищены пользователя или службы проверки подлинности). Это означает, что если вы используете проверку подлинности службы приложений и определения API hello tooexpose из в само приложение, необходимо параметр toouse проверки подлинности, который позволяет анонимный трафика tooreach API. Дополнительные сведения см. в статье [Проверка подлинности и авторизация для приложений API службы приложений](app-service-api-authentication.md).

### <a name="portal-blade"></a>Колонка портала
В hello [портал Azure](https://portal.azure.com/) hello конечной точки URL-адреса, которые могут видеть и изменении hello **определения API** колонку.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Свойство диспетчера ресурсов Azure
Можно также настроить URL-адрес определения hello API для приложения API с помощью [обозреватель ресурсов](https://resources.azure.com/) или [шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) в средства командной строки, таких как [Azure PowerShell](/powershell/azureps-cmdlets-docs)и hello [Azure CLI](../cli-install-nodejs.md). 

В **обозреватель ресурсов**, go слишком**подписки > {подписки} > resourceGroups > {группы ресурсов} > поставщики > Microsoft.Web > сайтов > {сайта} > config > web**, и вы увидите hello `apiDefinition` свойство:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Пример шаблона Azure Resource Manager, который задает hello `apiDefinition` свойство, откройте hello [azuredeploy.json файла в список дел пример приложения hello](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Найдите раздел hello hello шаблона, который выглядит как показанный выше образец JSON hello.

### <a name="default-value"></a>Значение по умолчанию
При использовании Visual Studio toocreate приложения API конечной точки для определения hello API автоматически устанавливается toohello базовый URL-адрес приложения hello API плюс `/swagger/docs/v1`. URL-адрес по умолчанию hello, hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) пакет NuGet использует метаданные Swagger tooserve динамически создаются для проекта веб-API ASP.NET. 

## <a name="code-generation"></a>Создание кода
Одно из преимуществ hello интеграцию Swagger в приложения Azure API — автоматическое создание кода. Созданные классы клиентских стала проще toowrite код, который вызывает приложение API.

Клиентский код для приложения API можно создать с помощью Visual Studio или из командной строки hello. Сведения о как клиент toogenerate классы в Visual Studio для проекта веб-API ASP.NET см. в разделе [приступить к работе с API приложений и ASP.NET](app-service-api-dotnet-get-started.md#codegen). Сведения о как toodo его из hello командной строки для всех поддерживаемых языков см. в разделе файла readme hello hello [Azure/autorest](https://github.com/azure/autorest) репозитория в GitHub.com.

## <a name="next-steps"></a>Дальнейшие действия
Пошаговое руководство по созданию, развертыванию и использованию приложений API см. в статье [Приступая к работе с приложениями API в службе приложений Azure](app-service-api-dotnet-get-started.md).

При использовании службы управления API Azure в приложениях API можно использовать tooimport метаданных Swagger API в службе управления API. Дополнительные сведения см. в разделе [как tooimport hello определение API и операций в службе управления API Azure](../api-management/api-management-howto-import-api.md). 

