---
title: "aaaAzure Обзор функций среды CLR | Документы Microsoft"
description: "Общие сведения о предварительной версии среды выполнения Azure функции hello"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Обзор среды выполнения Функций Azure

Hello среды выполнения функций Azure предлагает новый способ вы tootake преимуществами hello простоту и гибкость функции hello Azure программирования модели в локальной среде. Лежит hello же откройте корни источника, как функции Azure, среда выполнения функций Azure — tooprovide развернутые в локальной среде разработки почти те же возможности hello облачной службы.

![Портал предварительной версии среды выполнения Функций Azure][1]

Hello среды выполнения функций Azure позволяет вам функции Azure tooexperience перед фиксацией toohello облака. Таким образом активы кода hello построении можно выполнен переход с облаком toohello при миграции.  Среда выполнения Hello также открывает новые возможности, например ночью использование запасных вычислительной мощности hello процессов пакета toorun локальных компьютеров. Устройства также можно использовать в вашей организации tooconditionally отправки tooother системы данных, как в локальных и в облаке hello.

Hello среды выполнения функций Azure состоит из двух частей:
* роль управления средой выполнения Функций Azure;
* рабочая роль среды выполнения Функций Azure.

## <a name="azure-functions-management-role"></a>Роль управления Функциями Azure

Hello роль управления функции Azure предоставляет ведущее приложение для управления функциями в локальной hello. Эта роль выполняет следующие задачи hello.

* Размещение hello портала управления Azure функции, который является hello hello того же, вы видите в hello [портал Azure](https://portal.azure.com). Это позволяет разрабатывать функций в hello таким же способом, что и в hello портал Azure.
* Распределяет функции между несколькими рабочими ролями функций.
* Предоставляет конечную точку публикации, чтобы публиковать функции непосредственно из Microsoft Visual Studio.

## <a name="azure-functions-worker-role"></a>Рабочая роль Функций Azure

Hello Azure функции рабочей роли развертываются в контейнерах Windows, и это местом исполнения кода функции.  Вы можете развернуть в своей организации несколько рабочих ролей. Это ключевой метод, позволяющий клиентам использовать свободную вычислительную мощность.

## <a name="minimum-requirements"></a>Минимальные требования

tooget работы с hello функции среды выполнения Azure, необходимо иметь компьютер с **Windows Server 2016 или Центр обновления Windows 10 создатели** с доступом tooa **SQL Server** экземпляра.

## <a name="next-steps"></a>Дальнейшие действия

Установка hello [Предварительная версия среды выполнения функций Azure](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
