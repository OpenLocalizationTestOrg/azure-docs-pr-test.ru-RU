---
title: "Доменные службы Azure Active Directory: включение поддержки службы профилей пользователей SharePoint | Документация Майкрософт"
description: "Настроить синхронизацию доменных служб Active Directory Azure управляемые домены toosupport профиль для сервера SharePoint"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>Настройка синхронизации профиля toosupport управляемый домен для сервера SharePoint
Сервер SharePoint содержит службу профилей пользователей, которая используется для синхронизации профилей пользователей. tooset копирование hello службой профилей пользователей, соответствующие разрешения должны toobe, предоставленные в домене Active Directory. Дополнительные сведения см. в статье [Предоставление доменным службам Active Directory разрешений для синхронизации профилей в SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).

В этой статье объясняется, как доменные службы Azure AD управляемые домены toodeploy hello синхронизации профилей пользователей SharePoint Server службу можно настроить.

## <a name="hello-aad-dc-service-accounts-group"></a>Группа «Учетные записи службы контроллера домена AAD» Hello
Группа безопасности с именем "**учетных записей служб контроллер домена AAD**" можно использовать в организационную единицу hello «Пользователи» на управляемый домен. Можно найти эту группу в hello **Active Directory — пользователи и компьютеры** оснастки MMC на управляемый домен.

![Группа безопасности "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

Члены этой группы безопасности, делегированные hello следующие права:
- Привилегия «Репликация изменений каталога» Hello в корневом каталоге hello DSE из hello управляемого домена.
- Hello права «Репликация изменений каталога» в контексте именования конфигурации hello (cn = контейнера конфигурации) домена с управляемыми hello.

Эта группа безопасности также является членом встроенной группы «hello» **пред-Windows 2000 доступ**.

![Группа безопасности "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>Включить к управляемому домену toosupport синхронизации профиля пользователя на сервере SharePoint
Можно добавить hello учетная запись, используемая для toohello синхронизации профиля пользователя SharePoint **учетных записей служб контроллер домена AAD** группы. В результате учетная запись синхронизации hello получает соответствующие права доступа tooreplicate изменения toohello каталог. Это действие позволяет toowork синхронизации профиля пользователя SharePoint Server правильно.

![Добавление участников в группу "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Добавление участников в группу "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>Похожий контент
* [Предоставление доменным службам Active Directory разрешений для синхронизации профилей в SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)
