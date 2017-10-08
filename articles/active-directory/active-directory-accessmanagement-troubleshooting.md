---
title: "aaaTroubleshooting динамическое членство для групп | Документы Microsoft"
description: "Советы по устранению неполадок динамического членства в группах в Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Устранение неполадок, связанных с динамическим членством в группах
**Я настроил правило в группе, но обновления не членства в группе hello**<br/>Убедитесь, что hello **делегированное управление группами** установлено слишком**Да** в hello **Настройка** вкладки. Вы увидите этот параметр только в том случае, если вы вошли как назначается toowhom пользователю лицензию Azure Active Directory Premium. Проверка значений hello для атрибутов пользователей на правило hello: имеются пользователи, которые удовлетворяют правилу hello?

**Я настроил правило, но теперь будут удалены существующие члены правила hello hello**<br/>Это ожидаемое поведение. При изменении или включении правила, будут удалены существующие члены группы hello. Hello пользователей, возвращаемых на основе оценки правила hello добавляются как члены группы toohello.     

**Я не вижу мгновенного изменения членства, когда добавляю или изменяю правило. Почему?**<br/>Специальная оценка членства выполняется периодически в асинхронном фоновом процессе. Как долго принимает hello процесса определяется hello число пользователей в группы hello, созданных в результате правило hello размер вашего каталога и hello. Как правило каталоги при небольшом количестве пользователей увидеть изменения членства в группе hello менее чем через несколько минут. Каталоги с большим числом пользователей может занять 30 минут или дольше toopopulate.

### <a name="next-steps"></a>Дальнейшие действия
В следующих статьях содержатся дополнительные сведения об Azure Active Directory.

* [Управление tooresources доступ с помощью групп Azure Active Directory](active-directory-manage-groups.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Что такое Microsoft Azure Active Directory](active-directory-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
