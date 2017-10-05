---
title: "Начало работы с API отчетов Azure AD на классическом портале Azure AD | Документация Майкрософт"
description: "Как начать работу с API отчетов Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a>Начало работы с API отчетов Azure Active Directory на классическом портале Azure AD
*Эта тема входит в состав [руководства по отчетам Azure Active Directory](active-directory-reporting-guide.md).*

Azure Active Directory предоставляет разнообразные отчеты. Данные этих отчетов могут быть очень полезными для приложений, например систем SIEM, а также инструментов аудита и бизнес-аналитики. Интерфейсы API отчетов Azure AD предоставляют программный доступ к данным с помощью набора интерфейсов API на базе REST. Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.

В этой статье содержатся сведения, необходимые для начала работы с интерфейсами API отчетов Azure AD.
В следующем разделе представлены дополнительные сведения об использовании интерфейсов API аудита и входа. Дополнительные сведения о других интерфейсах API см. в статье [Отчеты и события (предварительная версия)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview).

Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, обратитесь в [службу поддержки по инструментам создания отчетов AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="learning-map"></a>Карта обучения
1. **Подготовка.** Перед тестированием примеров API нужно выполнить [предварительные требования для доступа к API отчетов Azure AD](active-directory-reporting-api-prerequisites.md).
2. **Изучение.** Ознакомьтесь с интерфейсами API отчетов:
   
   * [Использование примеров для API аудита](active-directory-reporting-api-audit-samples.md) 
   * [Использование примеров для API отчетов о действиях при входе](active-directory-reporting-api-sign-in-activity-samples.md)
3. **Настройка.** Создайте свое решение: 
   
   * [Справочник по использованию API аудита](active-directory-reporting-api-audit-reference.md) 
   * [Справочник по использованию API отчетов о действиях при входе](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a>Дальнейшие действия
Если вы хотите просмотреть все доступные конечные точки API Graph Azure AD, перейдите по адресу [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).

