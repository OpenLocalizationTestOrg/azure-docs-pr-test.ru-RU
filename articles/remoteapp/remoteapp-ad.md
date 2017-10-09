---
title: "aaaAzure AD + требования Active Directory для Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooset копирование toowork Active Directory с Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Требования Azure AD + Active Directory для Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Для вашей коллекции Azure RemoteApp гибридного или облачной коллекции, которые должны toofederate, с помощью AD Connect необходимо следующее toodo hello.

### <a name="connect-azure-ad-and-active-directory"></a>Подключите Azure AD и Active Directory
Если требуется tooconnect вашего клиента Azure AD и вашей локальной среде Active Directory, используйте AD Connect. Он будет открыт только [4 щелчков](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello двух каталогов.

Примечание. Для гибридных коллекций требуется синхронизация службы каталогов.

### <a name="make-sure-your-domaincom-match"></a>Проверка соответствия @domain.com
Перед началом работы убедитесь, что hello имени участника-пользователя для вашей локальной совпадений леса hello суффикс домена Azure AD. 

После настройки hello суффикс домена UPN в Azure AD, все пользователи, входящие в Azure RemoteApp будет войдите в систему как «пользователь @<hello suffix you set up>.» Убедитесь, что пользователи могут также войти hello же user@suffix в локальном домене hello. В некоторых случаях можно задать одно доменное имя в Azure AD с указанием разных доменный суффикс для hello пользователя в локальной среде. В этом случае пользователи не будет возможности tooconnect tooany к домену компьютеры или ресурсы с помощью Azure RemoteApp.

Например, если настройка вашей суффикс домена UPN в Azure Active Directory как contoso.com, но некоторым пользователям на локальном или AD не настроенный toolog с @contoso.uk, то эти пользователи не смогут использовать toocorrectly может войти в коллекцию ARA hello. Пользователям должно быть имя участника-пользователя в AAD и AD hello одинаково для возможных toobe входа hello»

### <a name="create-objects-for-azure-remoteapp"></a>Создайте объекты для Azure RemoteApp
Необходимо также toocreate hello следующие объекты в локальной среде Active Directory:

* Учетная запись tooprovide доступа toodomain ресурсов службы для программ удаленных приложений RemoteApp, соединяя RDSH конечных точек toohello локальному домену.
* Организационное подразделение (OU) toocontain RemoteApp объектов компьютера. Hello Подразделения используются учетные записи hello tooisolate рекомендуется (но не обязательно) и политик, которые будут использоваться с RemoteApp.

Нужны оба этих объектов при создании коллекции RemoteApp, поэтому возвратят toodo убедиться, что следующие действия.

