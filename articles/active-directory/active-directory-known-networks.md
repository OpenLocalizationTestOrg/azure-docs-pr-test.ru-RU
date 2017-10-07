---
title: "aaaKnown сетей в hello классический портал Azure | Документы Microsoft"
description: "Настроив известных сетей, можно избежать необходимости IP-адресов, которые принадлежат вашей организации, включенных в hello входы из нескольких географических регионов и входы с IP-адресов с подозрительной активности отчеты."
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
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>Известные сети

> [!div class="op_single_selector"]
> * [классический портал Azure](active-directory-known-networks.md)
> * [Портал Azure](active-directory-known-networks-azure-portal.md)
> 
> 


Можно использовать доступа Azure Active Directory и видимость toogain отчеты об использовании hello целостности и безопасности каталога вашей организации. С этой информацией администратор каталога может лучше определить, где могут возникнуть риски безопасности, чтобы их можно создать соответствующий план toomitigate этих рисков.

Возможно, что hello»*входа из нескольких географических регионов*«и»*входы с IP-адресов с подозрительными действиями*«отчеты неправильно флаг IP-адресов, которые принадлежат фактически вашей организация. 

Например, это может произойти, когда: 

* Пользователь в вашем офисе Бостоне вход в удаленно tooyour центр обработки данных в Сан-Франциско триггеры hello отчета «Входы из нескольких географических регионов» 
* Пользователь организации пытается подключиться через toosign несколько раз с помощью неправильного пароля триггеры hello отчета «Входы с IP-адресов с подозрительными действиями» 

сообщает этих случаях от создания пользователя в заблуждение безопасность tooprevent, следует добавить известных toohello список диапазонов IP-адресов вашей организации общедоступного IP-адреса.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>диапазоны tooadd общедоступный IP-адрес вашей организации, выполните следующие шаги hello.

1. Toohello входа [портала управления Azure](https://manage.windowsazure.com).

2. Hello левой панели щелкните **Active Directory**. 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-01.png)

3. В hello **каталога** вкладке, выберите свой каталог.

4. В меню в верхней части hello hello выберите **Настройка**. 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-02.png)

5. На вкладке "Настройка" hello, переход слишком**вашей организации общих IP-адресов** 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-03.png)

6. Щелкните **Добавьте известные диапазоны IP-адресов**.

7. Добавьте в hello появившемся диапазонов адресов и нажмите кнопку "Проверить" hello, после завершения. 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-04.png)

**Дополнительные ресурсы:**

* [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md)
* [Операции входа с IP-адресов с подозрительными действиями](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Операции входа из нескольких географических регионов](active-directory-reporting-sign-ins-from-multiple-geographies.md)

