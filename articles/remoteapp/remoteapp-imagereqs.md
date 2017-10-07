---
title: "требования изображения RemoteApp aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello требования для создания образов toobe использовать Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Требования к образам Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Azure RemoteApp использует toohost образа Windows Server 2012 R2 все программы hello требуется tooshare с вашими пользователями. toocreate пользовательского образа, можно начать с существующего образа или [создайте новую](remoteapp-create-custom-image.md).

> [!TIP]
> Вы знаете hello, к Azure RemoteApp подписки обеспечивает доступ tooa образа Windows Server 2012 R2 в коллекции виртуальных Машин Azure, которые можно использовать toocreate образ шаблона? [Узнайте об этом подробнее](remoteapp-image-on-azurevm.md).  
> 
> 

Существуют следующие требования Hello для hello образ, который можно загрузить для использования с Azure RemoteApp.

* Пользовательские приложения не хранить данные локально на изображении hello. Эти образы не имеют состояний и должны содержать только приложения.
* изображение Hello не содержит данных, которые могут быть потеряны.
* размер образа Hello должно быть кратно МБ. При попытке tooupload изображение, которое не является точным кратным hello отправка завершается ошибкой.
* Hello размер изображения должен быть 127 ГБ или меньше.
* он должен быть помещен в VHD-файл (файлы VHDX в настоящее время не поддерживаются).
* Hello виртуального жесткого диска не должен быть виртуальной машины поколения 2.
* Hello виртуального жесткого диска может быть фиксированного размера или динамически расширяемых. Динамически расширяемый виртуальный жесткий ДИСК рекомендуется, так как он принимает tooAzure tooupload меньше времени, чем файл VHD фиксированного размера.
* Hello диск должен быть инициализирован с помощью стиля разделов hello основная загрузочная запись (MBR). Hello стилем разделов таблицы Разделов GUID разделов не поддерживается.
* Hello виртуальный жесткий ДИСК должен содержать одной установке Windows Server 2012 R2. Он может содержать несколько томов, но только один из них может содержать установку Windows.
* необходимо установить роль узла сеансов удаленных рабочих столов (RDSH) Hello и возможности рабочего стола hello.
* Hello роли посредника подключений к удаленному рабочему столу необходимо *не* установить.
* необходимо отключить Hello шифрованной файловой системы (EFS).
* Hello изображение должно быть обработанной командой Sysprep, используя параметры hello **/oobe / generalize/shutdown** (hello, не используйте **/mode:vm** параметр).
* Отправка VHD из цепочки моментальных снимков не поддерживается.

Сведения о создании образов для Azure RemoteApp см. в статье [Создание образа Azure RemoteApp](remoteapp-imageoptions.md).

