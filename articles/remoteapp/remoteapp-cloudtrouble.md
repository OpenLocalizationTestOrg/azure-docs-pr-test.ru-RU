---
title: "RemoteApp облака aaaTroubleshoot коллекции — Создание | Документы Microsoft"
description: "Дополнительные сведения об удаленных приложений RemoteApp tootroubleshoot облачных сбои при создании коллекции"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Устранение неполадок при создании облачных коллекций RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Если возникают проблемы при создании облачной коллекции, просмотрите hello следующую информацию.

## <a name="your-image-is-invalid"></a>Недопустимый образ
При появлении сообщения, как «GoldImageInvalid», когда ожидается для Azure tooprovision вашей коллекции, это означает, что образ шаблона не соответствует hello [определенные требования изображения](remoteapp-imagereqs.md). Начинаем, читать их [требования](remoteapp-imagereqs.md), исправьте образ и повторите попытку коллекции toocreate.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>На портале управления Azure hello распространенных ошибок
    DNS server could not be reached
    ProvisioningTimeout

Часто сбои облачных коллекций происходят при создании из-за того, что вы используете настраиваемые образы.  Если вы используете коллекцию hello toocreate пользовательского образа появиться hello выше ошибки, проверьте hello, следующие действия:

* Убедитесь, что для этого настраиваемого образа hello загруженный образ требованиям.
* Чаще всего hello распространенная проблема связана, что это изображение hello не является правильно обработанной командой Sysprep.  
* Проверьте hello изображение может загружаться в Hyper-V или попробуйте создать ВМ IAAS непосредственно в вашей подписке Azure с помощью образа hello. В случае hello ВМ tooboot и не запускается, то обычно это означает, что не подготовлен этого настраиваемого образа hello.  Убедитесь, что hello пользовательский образ был создан после hello как toocreate шаблон пользовательского образа для удаленных приложений RemoteApp

При использовании одного из образов Microsoft hello, включенными в вашу подписку, попробуйте toocreate hello коллекции еще раз. Если hello проблема повторится, затем обратитесь в службу поддержки Майкрософт.

    PlatformImageTrialModeOnly

Если данная ошибка возникает это обычно означает, который был обновлен tooa Платная учетная запись, но вы пытаетесь toouse предоставленный Майкрософт образ, который действителен только при режиме пробной версии hello hello службы. В этом случае попробуйте toocreate вашей облачной коллекции еще раз, но будет убедиться, что toospecify hello нужного образа.

