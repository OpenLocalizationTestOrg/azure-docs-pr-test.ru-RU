---
title: "приложение в Azure RemoteApp aaaPublish | Документы Microsoft"
description: "Узнайте, как toopublish приложения и ресурсы в Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>Как toopublish приложения в удаленных приложений RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

После создания коллекции RemoteApp необходимо приложения hello toopublish или ресурсы необходимо toomake доступны для пользователей. Hello образы шаблонов, предоставленного с подпиской достаточно нескольких приложений публикации по умолчанию - tooshare hello другие приложения, необходимо toopublish их.

> [!NOTE]
> Требуется tooupdate приложения? Вам потребуется слишком[обновление образа hello](remoteapp-update.md) первой.
> 
> 

На hello **публикации** hello портала, нажмите кнопку **публикации**. Можно либо добавить приложение из образа шаблона **запустить** меню или укажите приложение hello hello путь toowhere устанавливается на образ шаблона hello. Если выбрать tooadd hello **запустить** меню, выберите из списка hello toopublish приложения hello. Если приложение toohello tooprovide hello путь, введите имя для приложения hello и toohello приложение hello путь. Используйте переменные пути hello - например, «% systemdrive %» вместо «c:\".

> [!NOTE]
> Если требуется tooadd приложения hello **запустить** меню, необходимо toohave *добавлены toohello этого приложения **запустить** меню образ шаблона.* В противном случае RemoteApp будет доступна только в том, что *—* на hello **запустить** меню и будет спутать. 
> 
> toomake убедиться, что приложение установлено в hello **запустить** меню, поместите файл ярлыка - **.lnk** — в папке Menu\Programs %systemdrive%\ProgramData\Microsoft\Windows\Start hello.
> 
> Если вы забыли toohello приложения hello tooadd **запустить** меню при создании шаблона hello, выберите приложение toohello tooadd hello пути. (или создайте образ шаблона заново, что потребует больше усилий).
> 
> 

