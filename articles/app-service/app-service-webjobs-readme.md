---
title: "aaaWebJobs в службе приложений Azure"
description: "Узнайте, как проверяет toobuild toorun фона веб-заданий, взаимодействовать со службами, такими как хранилища и Service Bus и создавать запланированные задачи."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a>Использование веб-заданий в службе приложений Azure
В этой статье ссылки ресурсов toodocumentation о toouse веб-заданий Azure и hello Azure SDK веб-заданий. Веб-задания Azure предоставляют простой способ toorun сценариев или программ в качестве фоновые процессы на [веб-приложений служб приложения](http://go.microsoft.com/fwlink/?LinkId=529714). Можно загружать и запускать исполняемые файлы, например cmd, bat, exe (.NET), ps1, sh, php, py, js и jar. Эти программы могут работать как веб-задания по расписанию (cron) или постоянно.

Hello SDK веб-заданий упрощает проще toouse хранилища Azure. Hello SDK веб-задания имеет привязку и триггер систему, которая работает с хранилища больших двоичных объектов Microsoft Azure, очередей и таблиц, а также очереди Service Bus.

Создание, развертывание веб-заданий и управление ими средствами Visual Studio не вызовет проблем. Веб-задания можно создавать из шаблонов, публиковать их и управлять ими (запуск/остановка/мониторинг/jnkflrf).

панель мониторинга веб-заданий Hello в hello портал Azure предоставляет возможности управления, которые обеспечивают полный контроль над hello выполнение веб-заданий, включая hello возможность tooinvoke отдельные функции в веб-заданий. панель мониторинга Hello также отображает функции среды выполнения и вывода.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

