---
title: "aaaCustomizing сопоставления атрибутов Azure AD | Документы Microsoft"
description: "Узнать, какие сопоставления атрибутов для приложений SaaS в Azure Active Directory как их можно изменить tooaddress бизнеса требуется."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Настройка сопоставлений атрибутов для подготовки пользователей для приложений SaaS в Azure Active Directory
Microsoft Azure AD обеспечивает поддержку для приложений SaaS сторонних toothird Salesforce, Google Apps и другие подготовки пользователей. Если у вас есть подготовки пользователей для приложений SaaS сторонних разработчиков, hello портала управления Azure определяет значения его атрибутов в форме конфигурации, называемой «сопоставление атрибутов».

Существует набор предварительно настроенных сопоставлений атрибутов между объектами пользователей Azure AD и каждого приложения SaaS. Некоторые приложения управляют другими типами объектов, такими как группы или контакты. <br> 
 Можно настроить в соответствии с потребностями бизнеса tooyour сопоставления атрибута по умолчанию hello. Это означает, что можно изменить или удалить существующие сопоставления атрибутов или создать новые.

На портале hello Azure AD, эту функцию можно открыть, щелкнув **сопоставления** конфигурации в разделе **Provisioning** в hello **управление** раздел  **Корпоративное приложение**.


![Salesforce][5] 

Щелкнув **сопоставления** конфигурации, открывается hello связанные **сопоставление атрибута** колонку.  
Существуют сопоставления атрибутов, необходимых для приложения SaaS toofunction правильно. Обязательные атрибуты hello **удалить** компонент недоступен.


![Salesforce][6]  

В приведенном выше примере hello, вы увидите, что hello **Username** атрибут управляемого объекта в Salesforce заполняется hello **userPrincipalName** значение hello связанный объект Azure Active Directory.

Щелкнув сопоставление, вы можете настроить **Сопоставления атрибутов**. При этом откроется hello **изменение атрибута** колонку.

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>Основные сведения о типах сопоставления атрибутов
С помощью сопоставлений атрибутов можно управлять заполнением атрибутов в сторонних приложениях SaaS. Поддерживаются четыре типа сопоставлений.

* **Прямой** — hello целевой атрибут заполняется значением атрибута связанного объекта hello hello в Azure AD.
* **Константа** — hello целевой атрибут заполняется определенной строки были выбраны.
* **Выражение** -hello целевой атрибут заполняется на основе hello результата выражения like скрипта. 
  Дополнительные сведения см. в статье [Запись выражений для сопоставления атрибутов в Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).
* **Нет** -hello целевой атрибут оставляется без изменений. Однако hello целевой атрибут пуст, заполняется значением по умолчанию hello, указываемое.

В дополнение toothese четырех основных типов сопоставлений атрибутов, настраиваемые сопоставления атрибутов поддерживают концепцию hello необязательный **по умолчанию** назначения значений. значение по умолчанию Hello гарантирует, что целевой атрибут заполняется со значением, если нет значения ни в Azure AD, ни hello целевого объекта. Самая обычная конфигурация Hello — tooleave этом пустым.


## <a name="understanding-attribute-mapping-properties"></a>Основные сведения о свойствах сопоставления атрибутов

В предыдущем разделе hello уже были введено toohello атрибута сопоставления типа свойства.
В свойстве toothis сложения сопоставления атрибутов также поддерживают hello следующие атрибуты:

- **Исходный атрибут** -атрибут пользователя hello из исходной системы hello (например: Azure Active Directory).
- **Целевой атрибут** — атрибут пользователя hello в целевой системе hello (например: ServiceNow).
- **Сопоставления объектов с помощью этого атрибута** — ли это сопоставление можно использовать toouniquely идентификации пользователей между исходной и целевой системами hello. Обычно устанавливается на hello userPrincipalName или атрибут mail в Azure AD, как правило, сопоставленного поля имени пользователя tooa в целевом приложении.
- **Приоритет сопоставления** — возможность указания нескольких атрибутов сопоставления. Если существует несколько, они вычисляются в порядке hello, определенные по этому полю. Как только соответствие найдено, дальнейшие атрибуты сопоставления не вычисляются.
- **Применить это сопоставление**
    - **Всегда** — применить это сопоставление как при создании, так и при обновлении пользователей
    - **Только при создании** — применить это сопоставление только при создании пользователей


## <a name="what-you-should-know"></a>Необходимая информация

Процесс синхронизации в Microsoft Azure AD реализован очень эффективно. Во время цикла синхронизации в инициализированной среде обрабатываются только объекты, требующие обновления. Обновление сопоставлений атрибутов оказывает влияние на производительность hello цикла синхронизации. Обновление настройки сопоставления атрибута toohello требует всех toobe управляемых объектов вычислены. Это рекомендуемый лучший подход tookeep hello число последовательных изменений сопоставлений атрибутов tooyour как минимум.

## <a name="next-steps"></a>Дальнейшие действия

* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Автоматизация пользователя подготовки и отзыва tooSaaS приложений](active-directory-saas-app-provisioning.md)
* [Запись выражений для сопоставления атрибутов](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Фильтры области для подготовки пользователей](active-directory-saas-scoping-filters.md)
* [С помощью SCIM tooenable автоматическую подготовку пользователей и групп из Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Уведомления о подготовке учетных записей](active-directory-saas-account-provisioning-notifications.md)
* [Список учебников по tooIntegrate приложений SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

