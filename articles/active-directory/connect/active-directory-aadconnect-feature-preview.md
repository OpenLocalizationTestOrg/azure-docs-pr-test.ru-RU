---
title: "Azure AD Connect: предварительные версии компонентов | Документация Майкрософт"
description: "В этой статье более подробно описаны функции Azure AD Connect, находящиеся на этапе предварительной версии."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Дополнительная информация о функциях в предварительной версии
В этом разделе описывается, как toouse функции в настоящее время в предварительной версии.

## <a name="group-writeback"></a>Обратная запись групп
параметр Hello для обратной записи групп в дополнительных компонентов позволяет toowriteback **группы Office 365** tooa леса с установленным Exchange. Это группа, который управляется всегда в облаке hello. Если у вас есть локальные версии Exchange, затем можно написать обратно эти tooon локальные группы, пользователи, имеющие почтовый ящик в локальной среде Exchange можно отправлять и получать сообщения электронной почты из следующих групп.

Дополнительные сведения о группах Office 365 и как toouse их можно найти [здесь](http://aka.ms/O365g).

Группа Office 365 представлена в виде группы рассылки в локальной среде AD DS. Ваш локальный сервер Exchange должен быть на Exchange 2013 с накопительным обновлением 8 (выпущенной в март 2015 г.) или Exchange 2016 toorecognize этот новый тип группы.

**Заметки во время предварительного просмотра hello**

* в настоящее время атрибут книги адрес Hello не заполняется в режиме предварительного просмотра hello. Без этого атрибута hello группы не отображается в глобальном списке адресов hello. Здравствуйте, наиболее простым способом toopopulate этот атрибут является командлетом Exchange PowerShell hello toouse `update-recipient`.
* Лес, схемы Exchange hello, допустимых целевых объектов для групп. Если Exchange не обнаружено, то обратной записи групп не возможных tooenable.
* В настоящее время поддерживаются развертывания организаций Exchange только с одним лесом. При наличии более чем одной организации на локальной организации Exchange, необходимо локальное решение GALSync для этих групп tooappear в в других лесах.
* функция обратной записи группы Hello не обрабатывает группы безопасности или группы рассылки.

> [!NOTE]
> Подписки tooAzure AD Premium является обязательным для обратной записи групп.
> 
>

## <a name="user-writeback"></a>Обратная запись пользователей
> [!IMPORTANT]
> Hello Предварительная версия функции обратной записи пользователя был удален в hello августа 2015 г. обновление tooAzure AD Connect. Если вы включили ее, следует отключить эту функцию.
>
>

## <a name="next-steps"></a>Дальнейшие действия
Продолжите [выборочную установку Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
