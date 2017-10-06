---
title: "aaaProvisioning приложений с использованием фильтров области | Документы Microsoft"
description: "Узнайте, как области toouse фильтрует объекты tooprevent в приложениях, поддерживающих Автоматическая подготовка пользователей из фактически идет подготовка, если объект не удовлетворяет необходимым требованиям бизнеса."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Подготовка приложений на основе атрибутов с использованием фильтров области
Цель этого раздела Hello — как toouse области фильтров toodefine основанное на атрибутах правила, определяющие, какие пользователи имеют tooexplain подготовить toohello приложения.

## <a name="clauses-and-scope-groups"></a>Предложения и группы областей
![Фильтр области действия][1] 

Фильтры области действия определяются одной или несколькими **группами областей**, каждая из которых содержит одно или несколько **предложений**. toosee hello предложения для определенной группы областей, разверните ее, щелкнув hello стрелка влево toohello имя_группы hello.

Объект **предложение** определяет, какие пользователи имеют право toopass через hello фильтр области, оценивая атрибуты каждого пользователя. Например может потребоваться одно предложение, требующее, пользователя «состояние» атрибута равно Нью-Йорке, поэтому только пользователи из Московской подготавливаются в приложение hello.

![Имя группы областей][2] 

Каждый **группы областей** начинается с одного обязательно **предложение**, как показано на снимке экрана приветствия выше. Это предложение просто указывает, что этот пользователь hello необходимо назначить toohello приложения до его оценки по фильтрам области. Это предложение нельзя удалить или изменить.

Можно добавить новые предложения или группы областей, нажав соответствующую кнопку "hello". Каждой группе областей можно присвоить имя, изменив ее свойство **Имя группы областей** .

## <a name="how-scoping-filters-are-evaluated"></a>Оценка по фильтрам области
Во время инициализации, мы тестируем каждого назначенного пользователя по вашей области toodetermine фильтры, если этот пользователь заслуживает toohello приложения access. Можно рассматривать как тест, который должен быть передан в порядке для hello пользователя tooavoid был отфильтрован каждого предложения. 

Если имеется несколько групп областей, каждый пользователь должен попасть по крайней мере один из них tooaccess приложения hello. Внутри каждой группы областей, тем не менее, hello пользователь должен передать toopass каждого предложения эту группу областей. 

Другими словами, можно представить группы областей как логическая или можно представить hello предложения в них, как и логическая. Например рассмотрим hello фильтр ниже области.

![Имя группы областей][3]  

В соответствии с toothis фильтр области, пользователи должны удовлетворять hello следующие критерии, toobe подготовки:

1. Должны быть назначены toohello приложения.
2. Они должны работать в отдел разработок hello
3. они должны работать в Сан-Франциско или в Канаде.

## <a name="related-articles"></a>Связанные статьи
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Автоматизировать подготовку пользователей и их отзыва tooSaaS приложений](active-directory-saas-app-provisioning.md)
* [Настройка сопоставления атрибутов для подготовки пользователей](active-directory-saas-customizing-attribute-mappings.md)
* [Запись выражений для сопоставления атрибутов](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Уведомления о подготовке учетных записей](active-directory-saas-account-provisioning-notifications.md)
* [С помощью SCIM tooenable автоматическую подготовку пользователей и групп из Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Список учебников по tooIntegrate приложений SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
