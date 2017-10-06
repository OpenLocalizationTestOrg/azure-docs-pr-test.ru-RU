---
title: "aaaAzure AD Connect в Германии облака Майкрософт"
description: "Azure AD Connect интегрирует локальные каталоги с Azure Active Directory. Это позволяет tooprovide общего удостоверения для приложений Office 365, Azure и SaaS интегрированы с Azure AD."
keywords: "Введение tooAzure AD Connect, общие сведения о Azure AD Connect, что такое Azure AD Connect установки active directory, Германии, черный леса"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Общедоступная предварительная версия Azure AD Connect в Microsoft Cloud для Германии
## <a name="introduction"></a>Введение
Azure AD Connect обеспечивает синхронизацию локальных каталогов Active Directory с каталогами Azure Active Directory.
В настоящее время многие сценарии hello в [Германия Microsoft Cloud](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) должна быть выполнена путем оператор hello. При использовании Microsoft Cloud Германии, необходимо помнить о следующих hello:

* Hello следующие URL-адреса должен быть открыт на прокси-сервер для синхронизации toooccur успешно:
  
  * *.microsoftonline.de
  * *.windows.net
  * * списки отзыва сертификатов.
* Когда вы войдете в каталоге Azure AD tooyour, необходимо использовать учетную запись в домене onmicrosoft.de hello.
* Привет, следующие функции будут недоступны.
  * Azure AD Connect Health
  * Автоматическое обновление
 
## <a name="download"></a>Загрузить
Azure AD Connect можно загрузить из колонки hello Azure AD Connect на портале hello.  Используйте инструкции hello ниже toolocate hello Azure AD Connect колонку.

### <a name="hello-azure-ad-connect-blade"></a>Hello Azure AD Connect колонку
После входа в портал Azure toohello hello следующие:

1. Go tooBrowse
2. Выберите Azure Active Directory.
3. Затем выберите Azure AD Connect.

Вы должны увидеть следующие hello.

![Колонка Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

Hello следующей таблице описаны возможности hello, показанные в колонке hello.

| Название | Описание |
| --- | --- |
| Состояние синхронизации |Сообщает, включена ли синхронизация. |
| Последняя синхронизация |Здравствуйте, время последней успешной синхронизации завершена. |
| Федеративные домены |Показывает количество hello федеративные домены, настроенные в данный момент. |

## <a name="installation"></a>Установка
tooinstall Azure AD Connect, вы можете использовать документацию hello [здесь](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Дополнительные функции и дополнительные сведения
Для начала ознакомьтесь со статьей [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md), чтобы получить подробные сведения и рекомендации по пользовательским и расширенным настройкам.  Эта страница содержит сведения и ссылки на руководство по tooadditional.

