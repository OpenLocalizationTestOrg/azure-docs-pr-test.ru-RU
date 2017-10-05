---
title: "Известные сети на классическом портале Azure | Документация Майкрософт"
description: "Настроив известные сети, вы избавитесь от ситуации, при которой IP-адреса вашей организации попадают в отчеты \"Операции входа из нескольких географических регионов\" и \"Операции входа с IP-адресов с подозрительными действиями\"."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a>Известные сети

> [!div class="op_single_selector"]
> * [классический портал Azure](active-directory-known-networks.md)
> * [Портал Azure](active-directory-known-networks-azure-portal.md)
> 
> 


Вы можете использовать отчеты об использовании и получении доступа Azure Active Directory, чтобы получить информацию о целостности и безопасности каталога вашей организации. C помощью этой информации администратор каталога может более точно определить источники возможных угроз безопасности, что позволяет правильно спланировать их устранение.

Возможна ситуация, при которой в отчеты "*Операции входа из нескольких географических регионов*" и "*Входы с IP-адресов с подозрительными действиями*" могут ошибочно попасть IP-адреса, фактически принадлежащие вашей организации. 

Например, это может произойти, когда: 

* пользователь в офисе в Бостоне удаленно подключился к центру обработки данных в Сан-Франциско, что привело к появлению отчета "Операции входа из нескольких географических регионов"; 
* пользователь вашей организации пытается войти несколько раз, указывая неправильный пароль, что приводит к появлению отчета "Операции входа с IP-адресов с подозрительными действиями". 

Чтобы в таких случаях не создавались ложные отчеты системы безопасности, следует добавить известные диапазоны IP-адресов в список общедоступных IP-адресов вашей организации.    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a>Чтобы добавить диапазоны IP-адресов в список общедоступных IP-адресов вашей организации, выполните следующие действия.

1. Войдите в [портал управления Azure](https://manage.windowsazure.com).

2. В левой панели щелкните **Active Directory**. 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-01.png)

3. На вкладке **Каталог** выберите требуемый каталог.

4. В верхнем меню щелкните **Настроить**. 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-02.png)

5. На вкладке "Настройка" перейдите в **диапазоны общедоступных IP-адресов вашей организации**. 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-03.png)

6. Щелкните **Добавьте известные диапазоны IP-адресов**.

7. Добавьте диапазоны адресов в появившемся диалоговом окне и нажмите кнопку "Проверить". 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-04.png)

**Дополнительные ресурсы:**

* [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md)
* [Операции входа с IP-адресов с подозрительными действиями](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Операции входа из нескольких географических регионов](active-directory-reporting-sign-ins-from-multiple-geographies.md)

