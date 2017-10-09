---
title: "aaaAzure образцы CLI - службы приложений | Документы Microsoft"
description: "Примеры Azure CLI. Служба приложений"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Примеры Azure CLI

Hello следующей таблице представлены ссылки toobash сценариев, созданных с использованием hello Azure CLI.

| | |
|-|-|
|**Создание приложения**||
| [Создание веб-приложения и развертывание кода из GitHub](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Создает веб-приложение Azure и развертывает код из общедоступного репозитория GitHub. |
| [Создание веб-приложения с непрерывным развертыванием из GitHub](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| Создает веб-приложение Azure с непрерывной публикацией из репозитория GitHub, владельцем которого вы являетесь. |
| [Создание веб-приложения и развертывание кода из локального репозитория Git](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Создает веб-приложение Azure и настраивает отправку кода из локального репозитория Git. |
| [Создание веб-приложения и развертывание кода tooa промежуточной среде](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | Создает веб-приложение Azure со слотом развертывания для изменений промежуточного кода. |
| [Создание веб-приложения ASP.NET Core в контейнере Docker](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Создает веб-приложение Azure в Linux и загружает образ Docker из Docker Hub. |
|**Настройка приложения**||
| [Карта пользовательского домена tooa веб-приложения](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Создает веб-приложение Azure и сопоставляет tooit имя пользовательского домена. |
| [Привязка пользовательских веб-приложения tooa SSL сертификата](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Создает веб-приложение Azure и привязывает hello SSL-сертификат tooit имя пользовательского домена. |
|**Масштабирование приложения**||
| [Масштабирование веб-приложения вручную](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Создает веб-приложение Azure и масштабирует его по двум экземплярам. |
| [Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | Создает два веб-приложения Azure в двух разных географических регионах и делает их доступными через одну конечную точку с помощью диспетчера трафика Azure. |
|**Подключение приложения tooresources**||
| [Подключение web app tooa базы данных SQL](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Создает веб-приложение Azure и базы данных SQL, а затем добавляет параметры приложения toohello строки подключения hello базы данных. |
| [Подключение приложения web tooa учетной записи хранилища](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Создает веб-приложение Azure и учетной записи хранилища, а затем добавляет параметры приложения toohello строки подключения хранилища hello. |
| [Подключение веб-приложения tooa redis кэша](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Создает веб-приложение Azure и кэш redis, а затем добавляет hello redis подключения сведения toohello параметры приложения.) |
| [Подключение web app tooCosmos DB](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Создает веб-приложение Azure и Cosmos DB, а затем добавляет приложение hello Cosmos DB подключения сведения toohello параметры. |
|**Мониторинг приложения**||
| [Мониторинг веб-приложения с помощью журналов веб-сервера](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Создает веб-приложение Azure, ведение журнала для него и загружает hello журналы tooyour локального компьютера. |
| | |