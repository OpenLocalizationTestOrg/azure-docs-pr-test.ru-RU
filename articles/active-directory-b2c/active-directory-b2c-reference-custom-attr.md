---
title: "Azure Active Directory B2C: настраиваемые атрибуты | Документация Майкрософт"
description: "Как toouse пользовательские атрибуты в Azure Active Directory B2C toocollect сведения о потребителей"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Azure Active Directory B2C: Используйте настраиваемые атрибуты toocollect информацию о потребителей
Каталог Azure Active Directory (Azure AD) B2C поставляется со встроенным набором информации (атрибутов): "Given Name", "Surname", "City", "Postal Code" и т. д. Однако каждый потребительском приложении имеет уникальные требования, на какие атрибуты toogather от объектов-получателей. С Azure AD B2C можно расширить набор атрибутов, хранящихся на каждой учетной записи потребителя hello. Можно создать настраиваемые атрибуты для hello [портал Azure](https://portal.azure.com/) и использовать его в вашей организации доступа к Интернету политики, как показано ниже. Можно также чтение и запись данных атрибутов с помощью hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Настраиваемые атрибуты используют [расширения схемы каталога API Graph Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Создание настраиваемого атрибута
1. [Выполните эти действия toonavigate toohello B2C функции колонку на портал Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Щелкните **Атрибуты пользователя**.
3. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
4. Укажите **имя** для hello настраиваемого атрибута (например, «ShoeSize») и при необходимости **описание**. Щелкните **Создать**.
   
   > [!NOTE]
   > Только Здравствуйте, «String» **тип данных** в настоящее время доступна.
   > 
   > 

Настраиваемый атрибут Hello теперь доступен в списке hello **атрибуты пользователя**и для использования в вашей организации доступа к Интернету политики.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Использование настраиваемого атрибута в политике регистрации
1. [Выполните эти действия toonavigate toohello B2C функции колонку на портал Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Щелкните **Политики регистрации**.
3. Tooopen вашей регистрации политики (например, «B2C_1_SiUp») щелкните его. Нажмите кнопку **изменить** hello верхней части колонки hello.
4. Нажмите кнопку **регистрации атрибуты** и выберите hello настраиваемого атрибута (например, «ShoeSize»). Нажмите кнопку **ОК**.
5. Нажмите кнопку **утверждений приложения** и выберите hello настраиваемого атрибута. Нажмите кнопку **ОК**.
6. Нажмите кнопку **Сохранить** hello верхней части колонки hello.

Можно использовать функцию «Запуск» hello на hello политики tooverify hello возможности использования. Теперь следует в список атрибутов, собранные во время регистрации потребителя hello. в разделе «ShoeSize» и отображается в приложение hello маркера tooyour отправлен назад.

## <a name="notes"></a>Примечания
* Помимо политик регистрации, настраиваемые атрибуты также можно использовать в политиках регистрации и входа в систему и в политиках изменения профилей.
* В отношении настраиваемых атрибутов действует известное ограничение. Только для созданных hello первый раз, он используется в любую политику, а не при его добавлении toohello список **атрибуты пользователя**.

