---
title: "aaaAdd пользователя tooyour коллекции Azure RemoteApp | Документы Microsoft"
description: "Узнайте, каким образом пользователи tooadd tooyour коллекции Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>Как tooadd tooyour пользователя коллекции Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Прежде чем пользователи можно просмотреть и использовать приложения в Azure RemoteApp, у вас есть toogrant их доступа к коллекции tooyour. Это простая часть hello: на hello **доступ пользователя** введите hello сведения об учетной записи для пользователя hello и нажмите кнопку флажок hello.

Какие данные учетной записи требуются? Зависит от типа hello коллекции был создан (облачной или гибридной) и при использовании Office 365 профессиональный плюс в этой коллекции.

## <a name="supported-user-identities"></a>Поддерживаемые удостоверения пользователей
типы другую коллекцию Hello (облако и гибридное) поддерживают, используя различные удостоверения пользователя для доступа к tooapplications.  

Для гибридной коллекции RemoteApp требуется tooset инфраструктуры домена Active Directory локально, а клиент Azure Active Directory с помощью интеграции каталога (и при необходимости единый вход). Кроме того вы должны toocreate некоторые объекты Active Directory из локального каталога hello.  

Для облака коллекции RemoteApp любой пользователь, имеющий поддерживает удостоверения Azure Active Directory могут быть предоставлены tooinclude tooRemoteApp доступ пользователя учетные записи Майкрософт.  См. в следующей таблице hello.

Пользователи Office 365 являются пользователями Azure Active Directory. При наличии у них гибридных, синхронизированных с каталогами учетных записей Azure Active Directory этим пользователям можно предоставить доступ путем гибридного развертывания RemoteApp.   

Эта таблица используется для быстрого перехода, для которого в коллекции и каковы требования к Active Directory hello поддерживается удостоверения.

| Учетные записи пользователей | Облако | Гибридная среда |
| --- | --- | --- |
| Учетная запись Майкрософт |Да |Нет |
| Azure Active Directory (Azure AD) | | |
| Только облако Azure AD |Да |Нет |
| ADsync с синхронизацией паролей |Да |Да |
| ADsync без синхронизации паролей |Да |Нет |
| ADsync с AD FS |Да |Да |
| [Сторонние поставщики удостоверений, поддерживаемые Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (например, Ping) |Да |Да |
| Multi-Factor Authentication |Да |Да |

[Узнайте больше](remoteapp-ad.md) о настройке Active Directory для RemoteApp.

> [!NOTE]
> Hello Azure Active Directory-пользователи должны принадлежать hello клиенте, связанном с вашей подпиской. (Можно просматривать и изменять подписки на hello **параметры** вкладка на портале hello. В разделе [клиента Azure Active Directory hello изменений, используемой RemoteApp](remoteapp-changetenant.md) подробнее.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Данные учетных записей пользователей для Office 365 профессиональный плюс
Если вы используете Office 365 профессиональный плюс образ шаблона hello в коллекции *или* при создании настраиваемого образа, который использует Office 365, можно только tooadd пользователей Azure Active Directory, которые имеются подписки Office 365 для hello домен по умолчанию подписки. Дополнительные сведения см. в статье [Использование Office с Azure RemoteApp](remoteapp-o365.md).

