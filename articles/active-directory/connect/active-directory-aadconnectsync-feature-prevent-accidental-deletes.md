---
title: "Синхронизация Azure AD Connect: предотвращение случайного удаления | Документация Майкрософт"
description: "В этом разделе описывается hello предотвратить возможность случайного удаления (предотвращает случайное удаление) в Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Синхронизация Azure AD Connect: предотвращение случайного удаления
В этом разделе описывается hello предотвратить возможность случайного удаления (предотвращает случайное удаление) в Azure AD Connect.

При установке Azure AD Connect, предотвращения случайных удалений включена по умолчанию и настроенные toonot разрешить экспорт с более чем 500 операций удаления. Этот компонент является спроектированный tooprotect вас от случайного конфигурации меняется и изменяет tooyour локального каталога, которые могут повлиять на множество пользователей и других объектов.

## <a name="what-is-prevent-accidental-deletes"></a>Предотвращение случайного удаления
Распространенные сценарии включают следующие:

* Изменяет слишком[фильтрации](active-directory-aadconnectsync-configure-filtering.md) там, где весь [Подразделение](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) или [домена](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) не выбран.
* удаление всех объектов в подразделении;
* Подразделение переименовывается, поэтому все объекты считаются toobe за пределы области действия синхронизации.

значение по умолчанию Hello 500 объектов можно изменить с помощью PowerShell с помощью `Enable-ADSyncExportDeletionThreshold`. Необходимо настроить этот размер hello значение toofit вашей организации. Поскольку hello планировщика синхронизации запускается каждые 30 минут, значение hello — hello количество удалений, видны в течение 30 минут.

При наличии слишком много toobe удаления промежуточных экспортированы tooAzure AD, а затем hello экспорта и будет выдано сообщение электронной почты следующим образом:

![Сообщение электронной почты "Предотвращение случайного удаления"](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *(Контактное лицо по техническим вопросам), здравствуйте! (Время) hello удостоверения службы синхронизации обнаружил, что hello число удалений превышает пороговое значение удаления настроенного hello для (имя организации). В рамках этого запуска синхронизации удостоверений для удаления было отправлено всего (число) об. Это достигнуто или превышено пороговое значение hello настроен удаления объектов (число). Просим вас tooprovide подтверждения, которые эти удаленные элементы должны быть обработаны, прежде чем мы продолжится. См. в разделе hello предотвращает случайное удаление Дополнительные сведения об ошибке hello, перечисленные в этом сообщении электронной почты.*
>
> 

Можно также просмотреть состояние hello `stopped-deletion-threshold-exceeded` при просмотре в hello **диспетчер службы синхронизации** пользовательского интерфейса для экспорта профиля hello.
![Предотвращение случайного удаления в пользовательском интерфейсе Synchronization Service Manager](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

Если эта ситуация оказалась непредвиденной, выясните причину и выполните все действия для ее устранения. объекты, которые являются об удалении toobe toosee hello следующие:

1. Запуск **служба синхронизации** из меню "Пуск" hello.
2. Go слишком**соединители**.
3. Выберите hello соединитель с типом **Azure Active Directory**.
4. В разделе **действия** toohello вправо, выберите **поиска пространства соединителя**.
5. В всплывающем под hello **область**выберите **отключен, поскольку** и выберите время в прошлом hello. Щелкните **Search**(Поиск). Эта страница содержит представление всех объектов о toobe удалены. Нажав каждого элемента, можно получить дополнительные сведения об объекте hello. Можно также щелкнуть **параметр столбца** tooadd дополнительные атрибуты toobe видимым в сетке hello.

![Пространство поиска соединителя](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

При необходимости удаления hello затем hello следующие:

1. tooretrieve hello текущее пороговое значение удаления, запустите командлет PowerShell hello `Get-ADSyncExportDeletionThreshold`. Укажите имя учетной записи и пароль глобального администратора Azure AD. значение по умолчанию Hello равно 500.
2. tootemporarily отключите защиту и включите эти операции удаления проходят, запустите командлет PowerShell hello: `Disable-ADSyncExportDeletionThreshold`. Укажите имя учетной записи и пароль глобального администратора Azure AD.
   ![Учетные данные](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. С hello соединителя Azure Active Directory по-прежнему выбран, выберите действие hello **запуска** и выберите **Экспорт**.
4. hello toore включить защиту, выполните командлет PowerShell hello: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`. Замените значение hello, которое вы заметили при извлечении hello текущее пороговое значение удаления 500. Укажите имя учетной записи и пароль глобального администратора Azure AD.

## <a name="next-steps"></a>Дальнейшие действия
**Обзорные статьи**

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
