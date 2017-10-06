---
title: "изображение Azure RemoteApp aaaCreate | Документы Microsoft"
description: "Дополнительные сведения о параметрах hello, доступные для создания образов для Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Создание образа Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Azure RemoteApp использует приложения hello toohold изображения, используемые совместно с пользователями. (Мы получить изображение и использовать его виртуальных машин toocreate -, вот что hello доступ при входе в Azure RemoteApp.) toocreate коллекцию Azure RemoteApp с выбор приложений облачной или гибридной, сначала нужно создать изображение с этими приложениями, которые установлены. Создайте коллекцию, которая использует этот образ, назначить пользователей toohello коллекции и публикации приложений toothose пользователей.

Создавать и использовать образы можно различными способами. Hello basic [требование](remoteapp-imagereqs.md) для изображения является ОС Windows Server 2012 R2 и установлена роль узла сеансов удаленных рабочих столов (RDSH) hello. Выполнение этого требования стоит рассмотреть подробнее.

Имеются следующие параметры, когда речь заходит tooimages hello.

* Можно импортировать и использовать [образ на базе виртуальной машины Azure](remoteapp-image-on-azurevm.md). Это хороший вариант для бизнес-приложений, для которых нужно настраивать собственные параметры. Вы можете настроить hello toowork изображения для приложения hello.
* Можно [создать и отправить собственный образ](remoteapp-create-custom-image.md). Этот вариант подходит для ситуации, когда у вас уже есть образ, который вы используете в локальном развертывании служб удаленных рабочих столов.
* Можно использовать один из hello [образы шаблонов](remoteapp-images.md) подписаны RemoteApp. Эти изображения создаются и обслуживается сотрудникам RemoteApp hello и содержать некоторые стандартные приложения (например, пакет Office hello), которые можно сделать доступными tooyour пользователей. Обратите внимание, что только hello Office 365 Профессиональная, а также образ можно использовать в производственной среде.

Независимо от того, где получить изображение или как создать, будет необходимо убедиться, что вы понимаете hello toomake [требований приложений](remoteapp-appreqs.md) tooensure приложения хорошо работает в удаленных приложений RemoteApp. Затем hello следующим шагом является toocreate [облака](remoteapp-create-cloud-deployment.md) или [гибридных](remoteapp-create-hybrid-deployment.md) коллекции.

