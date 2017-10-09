---
title: "Синхронизация aaaAzure AD Connect служб компонентов и конфигурации | Документы Microsoft"
description: "Описываются функциональные возможности службы синхронизации Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Функции службы синхронизации Azure AD Connect
функция синхронизации Hello Azure AD Connect состоит из двух компонентов:

* Hello локальный компонент с именем **синхронизации Azure AD Connect**, который также называется **модуль синхронизации**.
* Hello службы, размещенные в Azure AD, также известный как **служба синхронизации Azure AD Connect**

В этом разделе объясняется, как hello следующие функции для hello **служба синхронизации Azure AD Connect** работы и как можно настроить их с помощью Windows PowerShell.

Эти параметры настраиваются при hello [Azure Active Directory модуля для Windows PowerShell](http://aka.ms/aadposh). Он загружается и устанавливается отдельно от Azure AD Connect. Hello командлеты, описанные в этом разделе были представлены в hello [марта 2016 г (сборка 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Если у вас hello командлеты, описанные в этом разделе или они не создают hello же привести, а затем убедитесь, что при запуске hello последнюю версию.

Конфигурация toosee hello в вашем каталоге Azure AD, запустите `Get-MsolDirSyncFeatures`.  
![Результат вызова командлета Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Многие из этих параметров могут быть изменены только службой Azure AD Connect.

Hello следующие параметры могут быть настроены с `Set-MsolDirSyncFeature`:

| DirSyncFeature | Комментарий |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Позволяет toojoin объектов userPrincipalName в адресе tooprimary SMTP сложения. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Позволяет hello hello синхронизации ядра tooupdate атрибут userPrincipalName управляемых лицензированных пользователей (нефедеративных). |

После включения функции отключить ее нельзя.

> [!NOTE]
> С 24 августа 2016 года hello функция *повторяющийся атрибут устойчивости* включена по умолчанию для новых Azure каталогов AD. Эта функция будет постепенно активирована и включена для каталогов, созданных до этой даты. Если каталог имеет о tooget эта функция включена, вы получите уведомление по электронной почте.
> 
> 

Hello следующие параметры настраиваются для Azure AD Connect и не может изменяться функцией `Set-MsolDirSyncFeature`:

| DirSyncFeature | Комментарий |
| --- | --- |
| DeviceWriteback |[Azure AD Connect: включение обратной записи устройств](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Синхронизация Azure AD Connect: расширения каталогов](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Позволяет toobe атрибут на карантин, если он является копией другого объекта, а не сбой hello весь объект во время экспорта. |
| PasswordSync |[Реализация синхронизации паролей с помощью службы Azure AD Connect Sync](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Предварительная версия. Обратная запись групп](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |Сейчас не поддерживается. |

## <a name="duplicate-attribute-resiliency"></a>Устойчивость повторяющихся атрибутов
Вместо завершения ошибкой tooprovision объекты с повторяющимися именами участников-пользователей, / proxyAddresses, hello дублирования атрибута «карантин» и назначается временное значение. После устранения конфликта hello, hello временный элемент представляет имя участника-пользователя автоматически изменен toohello соответствующее значение. Дополнительные сведения см. в статье [Синхронизация удостоверений и устойчивость повторяющихся атрибутов](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>Мягкое сопоставление атрибута userPrincipalName
Если эта функция включена, soft-match включена для имени участника-пользователя в дополнение toohello [основной SMTP-адрес](https://support.microsoft.com/kb/2641663), который всегда включен. Soft-match используется toomatch существующих пользователей облака — в Azure AD с помощью локальных пользователей.

Если вам требуется toomatch локальных учетных записей AD с существующие учетные записи, созданные в облаке hello и вы не используете Exchange Online, а затем эта возможность полезна. В этом сценарии обычно не нужно атрибут причина hello tooset SMTP в облаке hello.

Эта функция по умолчанию включена для создаваемых каталогов Azure AD. Чтобы увидеть, включена ли эта функция, выполните следующую команду:  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Если эта функция отключена для вашего каталога Azure AD, ее можно включить, выполнив следующую команду:  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>Синхронизация обновлений атрибута userPrincipalName
Исторически атрибут UserPrincipalName toohello обновления, с помощью службы синхронизации hello из локальной был заблокирован, если выполняются оба из следующих условий:

* Hello пользователя управляется (нефедеративных).
* пользователь Hello не назначена лицензия.

Дополнительные сведения см. в разделе [пользователя не совпадают имена в Office 365, Azure или Intune hello локального имени участника-пользователя или альтернативному имени пользователя](https://support.microsoft.com/kb/2523192).

Включение этой функции позволяет hello синхронизации ядра tooupdate hello userPrincipalName, измененные в локальной среде и использовать синхронизацию паролей при. Если используется федерация, эта функция не будет работать.

Эта функция по умолчанию включена для создаваемых каталогов Azure AD. Чтобы увидеть, включена ли эта функция, выполните следующую команду:  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Если эта функция отключена для вашего каталога Azure AD, ее можно включить, выполнив следующую команду:  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

После включения этой функции существующие значения атрибут userPrincipalName останутся неизменными. При следующей смене hello userPrincipalName атрибут локальных hello обычный разностной синхронизации пользователей обновит hello имени участника-пользователя.  

## <a name="see-also"></a>См. также
* [Службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

