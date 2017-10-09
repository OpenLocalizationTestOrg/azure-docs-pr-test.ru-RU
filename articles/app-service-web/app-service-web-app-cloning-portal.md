---
title: "aaaWeb клонирования приложения с помощью портала Azure"
description: "Узнайте, как tooclone toonew вашего веб-приложения веб-приложений с помощью портала Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Клонирование приложений службы приложений Azure с помощью портала Azure
Hello клонирования в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) Здравствуйте, позволяет легко создать копию существующего веб-приложения только что созданный tooa приложения в другом регионе или в одном регионе. Это позволит клиентам toodeploy количество приложений в разных регионах быстро и легко.

В настоящее время клонирование приложений поддерживается только в планах службы приложений уровня Premium. новый компонент использует Hello hello же ограничения, как средство резервного копирования приложений Web, в разделе [резервное копирование веб-приложения в службе приложений Azure](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Клонирование существующего приложения
Hello веб-приложения должна быть запущена в hello **Premium** режим toocreate клон hello веб-приложения.

1. В hello [портала Azure](https://portal.azure.com/), откройте колонку веб-приложения.
2. Щелкните **Средства**. Затем в hello **средства** колонка, щелкните **клонирование приложений**.
   
    ![][1]
   
   > [!NOTE]
   > Если веб-приложение hello уже не hello **Premium** режиме, вы получите сообщение, указывающее режимы hello поддерживается для клонирования приложения. На этом этапе, что у вас есть hello параметр tooselect **обновление**.
   > 
   > 
3. В hello **клонирование приложений** колонки введите имя нового веб-приложения hello, группа ресурсов и план служб приложений. Также hello пользователь будет toochoose, может ли tooclone ряд параметров источника веб-приложения или нет.
   
    ![][2]
4. После нажатия кнопки **создания** платформы hello начнет работать на Создание клона hello исходного веб-приложения.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Клонирование существующих приложений tooan среды службы приложений
В hello **клонирование приложений** колонке hello клиента имеется параметр toochoose hello пул приложений в существующей среде службы приложений.

## <a name="current-restrictions"></a>Существующие ограничения
Эта функция в настоящее время находится в предварительной версии, новые возможности tooadd Корпорация Майкрософт работает со временем, hello после списка являются hello известные ограничения в текущей поддержки hello клонирования приложения на портале Azure:

* Параметры диспетчера трафика Azure не клонируются.
* Параметры автоматического масштабирования не клонируются
* Параметры расписания резервного копирования не клонируются
* Параметры виртуальных сетей не клонируются
* Подробные сведения о приложении не настраиваются автоматически на веб-приложения hello назначения
* Параметры простой авторизации не клонируются
* Расширение Kudu не клонируется
* Правила TiP не клонируются
* Содержимое базы данных не клонируется.

### <a name="references"></a>Ссылки
* [Клонирование веб-приложения с помощью PowerShell](app-service-web-app-cloning.md)
* [Резервное копирование веб-приложений в службе приложений Azure](web-sites-backup.md)
* [Как tooCreate среды службы приложений](app-service-web-how-to-create-an-app-service-environment.md)
* [Создание веб-приложения в среде служб приложений](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Введение tooApp среды службы](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
