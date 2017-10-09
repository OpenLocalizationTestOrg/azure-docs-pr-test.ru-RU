---
title: "aaaConnectors в hello пользовательского интерфейса Azure AD Synchronization Service Manager | Документы Microsoft"
description: "Понимать hello Synchronization Service Manager на вкладке hello соединители для Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>Использование соединителей с hello Azure AD Connect Sync Service Manager

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

Вкладка соединители Hello — используется toomanage, которой подключен модуль синхронизации hello всех систем.

## <a name="connector-actions"></a>Действия соединителя
| Действие | Комментарий |
| --- | --- |
| Создание |Не используйте. Для подключения лесов tooadditional AD, используйте мастер установки hello. |
| Свойства |Используется для фильтрации доменов и подразделений. |
| [Удалить](#delete) |Используется tooeither удаление данных hello hello соединителя пробел или toodelete подключения tooa леса. |
| [Настройка профилей выполнения](#configure-run-profiles) |За исключением домена, фильтрации, ничего не tooconfigure здесь. Это действие можно использовать профили запуска toosee уже настроен. |
| Выполнить |Использовать toostart одного раза запуска профиля. |
| Остановить |Останавливает соединитель, на котором в настоящее время запущен профиль. |
| Экспортировать соединитель |Не используйте. |
| Импортировать соединитель |Не используйте. |
| Обновить соединитель |Не используйте. |
| Обновить схему |Обновляет кэшированные схемы hello. Это предпочтительный toouse hello вариант в мастере установки hello вместо этого, поскольку также обновлений синхронизировать правила. |
| [Пространство поиска соединителя](#search-connector-space) |Используемых объектов toofind и слишком[выполните объект и его данные через систему hello](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Удалить
Действие delete Hello используется для двух разных целей.  
![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

Здравствуйте, параметр **удалить только пространство соединителя** удаляет все данные, но оставить hello конфигурации.

Здравствуйте, параметр **удалить соединители и места** удаляет данные hello и конфигурации hello. Этот параметр используется в том случае, если больше не требуется tooconnect tooa леса.

Оба варианта синхронизировать все объекты и обновить объекты метавселенной hello. Это действие является длительной операцией.

### <a name="configure-run-profiles"></a>Настройка профилей выполнения
Этот параметр позволяет hello toosee запуска профилей, настроенных для соединителя.

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Пространство поиска соединителя
Действие пространства соединителя Hello поиска является полезным toofind объектов и устранения неполадок данных.

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Начните с выбора **пространства**. Можно выполнить поиск на основе данных (RDN различающееся имя, привязка, поддерева) или состояния hello объекта (все другие параметры).  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
Если, к примеру, выполняется поиск в поддереве, вы получаете все объекты в одном подразделении.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
В этой сетке можно выбрать объект, выберите **свойства**, и [следовать ей](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) из пространства соединителя источника hello через метавселенной hello и toohello целевого пространства соединителя.

### <a name="changing-hello-ad-ds-account-password"></a>Изменение пароля учетной записи hello AD DS
При изменении пароля учетной записи hello hello служба синхронизации не будет tooon локальные изменения могут tooimport или экспорта AD.   Возможны следующие hello.

- шаг Hello импорта и экспорта для hello соединителя AD завершится ошибкой «нет-start-учетные данные».
- В средстве просмотра событий Windows журнал событий приложения hello содержит ошибку с Идентификатором 6000 событий и сообщений «hello toorun управления агента «contoso.com» не удалось, так как hello учетные данные были заданы неверно.»

tooresolve hello выполните обновление учетной записи пользователя hello AD DS с помощью следующих hello:


1. Запустите hello Synchronization Service Manager (служба → НАЧАЛА синхронизации).
</br>![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Go toohello **соединители** вкладки.
3. Выберите hello соединителя AD, являющийся hello настроенных toouse учетной записи службы AD DS.
4. В разделе "Действия" выберите **Свойства**.
5. В всплывающем диалоговом окне приветствия выберите подключение tooActive леса:
6. Имя леса Hello указывает hello соответствующего в локальной среде AD.
7. имя пользователя Hello Указывает учетную запись доменных служб Active Directory hello AD, используемый для синхронизации.
8. Введите в текстовом поле пароля hello hello новый пароль для учетной записи hello AD DS ![Azure AD подключения синхронизации шифрования ключа служебной программы](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. Нажмите кнопку ОК toosave hello новый пароль и перезапустите hello служба синхронизации tooremove hello старый пароль из кэша памяти.



## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
