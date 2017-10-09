---
title: "Синхронизация Azure AD Connect: включение корзины AD | Документация Майкрософт"
description: "В этом разделе рекомендует использование hello AD корзиной с Azure AD Connect."
services: active-directory
keywords: "корзина AD, случайное удаление, привязка к источнику"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Синхронизация Azure AD Connect: включение корзины AD
Рекомендуется включить hello AD Корзина для вашей локальной каталогов Active Directory, которые синхронизированные tooAzure AD. 

Если вы случайно удалены из локальной объектом пользователя AD и восстановить его с помощью функции hello Azure AD восстанавливает hello соответствующего объекта пользователя Azure AD.  Дополнительную информацию о hello AD корзиной tooarticle [Обзор сценария для восстановления удаленных объектов Active Directory](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Преимущества использования hello AD корзины.
Эта функция позволяет с восстановлением объекты пользователя Azure AD, выполнив hello ниже:

* Если вы случайно удалены из локальной объекта пользователя AD, hello соответствующего объекта пользователя Azure AD будет удалено в hello следующего цикла синхронизации. По умолчанию Azure AD хранит удалены hello объекта-пользователя Azure AD обратимо удаленные состояние в течение 30 дней.

* При наличии в локальной среде AD корзины функция включена, можно восстановить hello удалены локального объекта пользователя AD без изменения его значения источника привязки. Когда hello восстановить в локальной синхронизированным объектом пользователя AD tooAzure AD Azure AD будет восстановлена hello соответствующий обратимо удаленные объектом-пользователем Azure AD. Дополнительную информацию об атрибуте источника привязки tooarticle [Azure AD Connect: основные понятия разработки](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Если у вас в локальной среде AD включена функция Bin управления, может быть обязательным toocreate AD пользователя tooreplace hello удаленного объекта. Если служба синхронизации Azure AD Connect является настроенным toouse созданные системой AD (например, ObjectGuid) для атрибута источника привязки hello, hello вновь созданный объект пользователя AD будет не имеют hello одинаковые значения источника привязки как hello удаленный объект пользователя AD. Если hello вновь созданный объект пользователя AD синхронизированные tooAzure AD, Azure AD создает новый объект пользователя Azure AD, вместо восстановления обратимо удаленные hello объекта-пользователя Azure AD.

> [!NOTE]
> По умолчанию Azure AD хранит удаленные объекты пользователя Azure AD в состоянии обратимого удаления в течение 30 дней, прежде чем удалить их без возможности восстановления. Однако администраторы могут ускорить hello удаления таких объектов. После hello объекты удаляются без возможности восстановления, они больше не может быть восстановлен, даже если в локальном AD корзиной включен.



## <a name="next-steps"></a>Дальнейшие действия
**Обзорные статьи**

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)

* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
