---
title: "aaaAzure службы структуры Docker составления Preview"
description: "Azure Service Fabric принимает Docker Compose toomake формат его проще существующие контейнеры tooorchestrate с помощью Service Fabric. Сейчас эта возможность доступна в предварительной версии."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Поддержка приложения Docker Compose в Azure Service Fabric (предварительная версия)

Docker использует hello [docker compose.yml](https://docs.docker.com/compose) файла для определения нескольких контейнера приложений. toomake он просто для пользователей, знакомых с Docker tooorchestrate существующие контейнера приложения в Azure Service Fabric, мы включили поддержку предварительной версии Docker Compose изначально hello платформы. Платформа Service Fabric может принять файлы `docker-compose.yml` версии 3 и более поздней. 

Так как эта поддержка доступна в режиме предварительной версии, поддерживается только подмножество директив Compose. Например, обновления приложений не поддерживаются. Но вы всегда можете вместо обновления приложений удалить и развернуть их.

toouse это предварительного просмотра, создания кластера с версии 5.7 или более среда выполнения Service Fabric hello через портал Azure, наряду с соответствующего пакета SDK для hello hello. 

> [!NOTE]
> Эта функция доступна в режиме предварительной версии и не поддерживается в рабочей среде.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Развертывание файла Docker Compose в Service Fabric

Hello следующие команды создают приложения Service Fabric (с именем `fabric:/TestContainerApp` в предшествующих пример hello), которые можно отслеживать и управлять подобно любому другому приложению Service Fabric. Можно использовать имя указанного приложения hello запросов о работоспособности.

### <a name="use-powershell"></a>Использование PowerShell

Создание приложения составления структуры службы из файла docker compose.yml, выполнив следующую команду в PowerShell hello:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`и `RegistryPassword` ссылаться toohello контейнер реестра, имя пользователя и пароль. После завершения приложения hello, можно проверить его состояние с помощью hello следующую команду:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete hello создания приложения с помощью PowerShell, выполните следующую команду hello.

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Использование интерфейса командной строки Service Fabric (sfctl)

Кроме того можно использовать следующую команду для обновления структуры CLI hello:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

После создания приложения hello, можно проверить его состояние с помощью hello следующую команду:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

hello toodelete создания приложения, используйте hello следующую команду:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Поддерживаемые директивы Compose

Данная Предварительная версия поддерживает подмножество параметров конфигурации hello в формат версии 3 Создание сообщения hello, включая hello следующих примитивов:

* Services > Deploy > Replicas
* Services > Deploy > Placement > Constraints
* Services > Deploy > Resources > Limits
    * -cpu-shares
    * -memory
    * -memory-swap
* Services > Commands
* Services > Environment
* Services > Ports
* Services > Image
* Services > Isolation (только для Windows)
* Services > Logging > Driver
* Services > Logging > Driver > Options
* Volume & Deploy > Volume

Настройка кластера hello для принудительного применения ограничения ресурсов, как описано в [ресурсами Service Fabric](service-fabric-resource-governance.md). Другие директивы Docker Compose не поддерживаются в этой предварительной версии.

## <a name="servicednsname-computation"></a>Вычисление ServiceDnsName

Если задать в файле составление имя службы hello представляет полное доменное имя (то есть, он содержит точкой [.]), DNS-имя hello, зарегистрированные с помощью Service Fabric `<ServiceName>` (включая точку hello). В противном случае каждый сегмент пути в имени приложения hello становится метка домена в hello DNS-имя службы, с hello становится метка домена верхнего уровня hello первый сегмент пути.

Например, если hello указано имя приложения — `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` бы hello зарегистрированное имя DNS.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Различия между моделью приложений Compose (определение экземпляра) и Service Fabric (определение типа)

Файл docker-compose.yml описывает набор контейнеров, доступных для развертывания, в том числе их свойства и конфигурации.
Например файл hello может содержать переменные среды и порты. Также можно указать параметры развертывания, например ограничения размещения, ограничения ресурсов и DNS-имен в файле docker compose.yml hello.

Hello [модель приложения Service Fabric](service-fabric-application-model.md) службы использует типы и типы приложений, где можно иметь несколько экземпляров приложения hello того же типа. Например, можно создать по одному экземпляру приложения на клиента. Эта модель на основе типа поддерживает несколько версий hello одного типа приложения, который регистрируется с помощью среды выполнения hello.

Например, клиента объект может быть создан с типом 1.0 AppTypeA приложения, а клиент Б может иметь другое приложение, экземпляр которого создается без hello того же типа и версии. Определения типов приложений hello в манифестах приложения hello и укажите имя и развертывания параметров приложения hello, при создании приложения hello.

Несмотря на то, что эта модель обеспечивает гибкость, мы также планируете toosupport модель развертывания проще, основанного на экземпляре, где типы являются неявными из файла манифеста hello. В этой модели каждое приложение получает собственный независимый манифест. Мы предварительно рассматриваем это действие, добавляя поддержку docker-compose.yml, в котором используется формат развертывания на основе экземпляра.

## <a name="next-steps"></a>Дальнейшие действия

* Ознакомьтесь со статьей hello [модели приложения Service Fabric](service-fabric-application-model.md)
* [Azure Service Fabric command line](service-fabric-cli.md) (Интерфейс командной строки Azure Service Fabric)
