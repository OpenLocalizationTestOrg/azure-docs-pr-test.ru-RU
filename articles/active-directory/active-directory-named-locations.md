---
title: "aaaNamed расположения в Azure Active Directory | Документы Microsoft"
description: "Настроив с именем расположения, можно избежать необходимости IP адресов, которые принадлежат вашей организации к созданию ложных положительных результатов для hello невозможно местоположений tooatypical тип событий риска."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Именованные расположения в Azure Active Directory

С hello с именем расположения функция Azure Active Directory можно пометить доверенные диапазоны IP-адресов в вашей организации. В вашей среде, можно использовать именованные папки в контексте hello обнаружение hello [риск события](active-directory-reporting-risk-events.md). функция Hello помогает снизить количество hello обнаруженную ложных положительных результатов для hello *tooatypical невозможно местоположений* тип событий риска. 

## <a name="configuration"></a>Конфигурация

tooconfigure именованное расположение:

1. Войдите в toohello [портал Azure](https://portal.azure.com) роли глобального администратора.

2. Hello левой панели щелкните **Azure Active Directory**.

    ![Hello Azure Active Directory ссылку в левой области hello](./media/active-directory-named-locations/01.png)

3. На hello **Azure Active Directory** колонки в hello **безопасности** щелкните **условного доступа**.

    ![Hello условным доступом команды](./media/active-directory-named-locations/05.png)


4. На hello **условного доступа** колонки в hello **управление** щелкните **расположения с именем**.

    ![Команда расположения именованных Hello](./media/active-directory-named-locations/06.png)


5. На hello **с именем расположения** колонка, щелкните **новое расположение**.

    ![Новая команда расположение Hello](./media/active-directory-named-locations/07.png)


6. На hello **New** колонке hello следующие:

    ![Новая колонка Hello](./media/active-directory-named-locations/08.png)

    а. В hello **имя** введите имя для данного именованного местоположения.

    b. В hello **диапазоны IP-адресов** введите диапазон IP-адресов. диапазон IP-адресов Hello должен toobe в hello *бесклассовой междоменной маршрутизации* формате (CIDR).  

    c. Щелкните **Создать**.



## <a name="what-you-should-know"></a>Необходимая информация

**Массового обновления**: при создании или обновлении именованных расположений для массового обновления, можно передать или загрузить CSV-файл с hello IP-диапазонов. Передача добавляет hello IP-диапазонов в списке toohello hello файла вместо перезаписи список hello.

![Привет, отправка и загрузка ссылок](./media/active-directory-named-locations/09.png)


**Ограничения**: можно определить один tooeach диапазона, назначенного IP из них не более 60 именованных расположений. Если имеется только один именованный расположения, настроенного для него можно определить too500 диапазоны IP.


## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о событиях риска в разделе [событий риска Azure Active Directory](active-directory-reporting-risk-events.md).

