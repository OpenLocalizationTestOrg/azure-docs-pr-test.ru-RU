---
title: "Azure AD Connect: экземпляры службы синхронизации | Документация Майкрософт"
description: "На этой странице приводятся специальные рекомендации для экземпляров Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect: специальные рекомендации для экземпляров
Чаще всего используется Azure AD Connect с hello world wide экземпляром Azure AD и Office 365. Но существуют и другие экземпляры, и они имеют другие требования к URL-адресам и прочие особенности.

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud Germany
Hello [Германия Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) sovereign облако, обслуживаемой немецком данных доверенного лица.

| Tooopen URL-адреса в прокси-сервера |
| --- |
| \*.microsoftonline.de |
| \*.windows.net |
| +Списки отзыва сертификатов |

Когда вы войдете в клиенте Azure AD tooyour, необходимо использовать учетную запись в домене onmicrosoft.de hello.

В настоящее время не присутствует в Германии Microsoft Cloud hello функции:

* Служба **Azure AD Connect Health** недоступна.
* **Автоматические обновления** недоступны.
* **Компонент обратной записи паролей** доступен в предварительной версии в Azure AD Connect версии 1.1.570.0 и более поздних.
* Другие службы Azure AD Premium недоступны.

## <a name="microsoft-azure-government-cloud"></a>Облако Microsoft Azure для государственных организаций
Hello [облако Microsoft Azure для государственных](https://azure.microsoft.com/features/gov/) облако для государственных организаций США.

Это облако поддерживается в более ранних выпусках DirSync. Сборки 1.1.180 Azure AD Connect hello следующего поколения облака hello поддерживается. Это поколение используется только для США на основе конечных точек и имеют разные списки tooopen URL-адреса в прокси-сервер.

| Tooopen URL-адреса в прокси-сервера |
| --- |
| \*.microsoftonline.com |
| \*.microsoftonline.us |
| \*.gov.us.microsoftonline.com |
| +Списки отзыва сертификатов |

Azure AD Connect не может обнаружить tooautomatically, клиент Azure AD находится в облаке государственных hello. Вместо этого необходимо hello tootake при установке Azure AD Connect следующие действия.

1. Запустите установку hello Azure AD Connect.
2. При появлении hello первую страницу, где должны tooaccept hello лицензионного соглашения, не продолжайте, но оставьте работы мастера установки hello.
3. Запустите редактор реестра и изменить раздел реестра hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello значение `2`.
4. Вернитесь в мастер установки toohello Azure AD Connect, принять лицензионное соглашение hello и продолжить. Во время установки, убедитесь, что hello toouse **пользовательской конфигурации** путь установки (и не экспресс-установки). Затем продолжите установку hello обычным образом.

В настоящее время не присутствует в облако Microsoft Azure для государственных hello функции:

* Служба **Azure AD Connect Health** недоступна.
* **Автоматические обновления** недоступны.
* **Компонент обратной записи паролей** доступен в предварительной версии в Azure AD Connect версии 1.1.570.0 и более поздних.
* Другие службы Azure AD Premium недоступны.

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
