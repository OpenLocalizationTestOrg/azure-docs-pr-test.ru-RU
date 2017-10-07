---
title: "Синхронизация Azure AD Connect: общие сведения о синхронизации и ее настройка | Документация Майкрософт"
description: "Объясняет, как работает синхронизация Azure AD Connect и как toocustomize."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка
службы синхронизации Azure Active Directory Connect Hello (Azure AD Connect sync) является основным компонентом Azure AD Connect. Он отвечает за все операции hello, связанные toosynchronize идентификационных данных между локальной средой и Azure AD. Синхронизация Azure AD Connect — последователь hello DirSync, Azure AD Sync и Forefront Identity Manager с hello настроить соединитель Active Directory Azure.

В этом разделе — hello главной странице **синхронизации Azure AD Connect** (также называется **модуль синхронизации**) и списки ссылок tooall других tooit связанные разделы. Для ссылки tooAzure AD Connect, в разделе [интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

Служба синхронизации Hello состоит из двух компонентов, hello локальной **синхронизации Azure AD Connect** называется компонент и hello стороне службы в Azure AD **служба синхронизации Azure AD Connect**. Служба Hello распространено DirSync, Azure AD Sync и Azure AD Connect.

## <a name="azure-ad-connect-sync-topics"></a>Статьи, имеющие отношение к службе синхронизации Azure AD Connect
| Раздел | Она охватывает и когда tooread |
| --- | --- |
| **Знакомство со службой синхронизации Azure AD Connect** | |
| [Основные сведения об архитектуре hello](active-directory-aadconnectsync-understanding-architecture.md) |Для тех, кто, новый механизм синхронизации toohello и требуется toolearn об архитектуре hello и hello терминов, используемых. |
| [Технические концепции](active-directory-aadconnectsync-technical-concepts.md) |Сокращенная версия, архитектура раздела hello и кратко описывается hello терминов, используемых. |
| [Топологии Azure AD Connect.](active-directory-aadconnect-topologies.md) |Описывает hello различных топологий и сценариях hello синхронизации engine поддерживает. |
| **Настраиваемая конфигурация** | |
| [Попытку выполнения мастера установки hello](active-directory-aadconnectsync-installation-wizard.md) |Объясняется, какие параметры доступны при выполнении мастера установки hello Azure AD Connect. |
| [Знакомство с декларативной подготовкой](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |Описывает модель конфигурации hello вызывается декларативной подготовки. |
| [Знакомство с выражениями декларативной подготовки.](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |Описывается синтаксис hello hello язык выражений, используемых в декларативной подготовки. |
| [Основные сведения о настройке по умолчанию hello](active-directory-aadconnectsync-understanding-default-configuration.md) |Описывает правила out-of-box hello и конфигурация по умолчанию hello. Также описывает, как hello правила работают вместе для сценариев out-of-box toowork hello. |
| [Синхронизация Azure AD Connect: общее представление о пользователях и контактах](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Продолжает функционировать в предыдущем разделе hello и описание конфигурации пользователей и контактов, hello работы друг с другом, в частности в среде с несколькими лесами. |
| [Как toomake toohello изменение конфигурация по умолчанию](active-directory-aadconnectsync-change-the-configuration.md) |Описывается порядок обмена toomake общие tooattribute изменения конфигурации. |
| [Советы и рекомендации по изменению конфигурации по умолчанию hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Ограничения поддержки и для внесения изменений toohello out-of-box конфигурации. |
| [Настройка фильтрации](active-directory-aadconnectsync-configure-filtering.md) |Описываются различные варианты hello синхронизация toolimit которой объекты tooAzure AD и пошаговые инструкции tooconfigure эти параметры. |
| **Функции и сценарии** | |
| [Предотвращение случайного удаления](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Описывает hello *избежать случайного удаления* функции и как tooconfigure его. |
| [Планировщик](active-directory-aadconnectsync-feature-scheduler.md) |Описывает встроенные планировщика hello, который импорта, синхронизации и экспорт данных. |
| [Службы синхронизации Azure AD Connect: реализация синхронизации паролей](active-directory-aadconnectsync-implement-password-synchronization.md) |Описывает, как работает синхронизация паролей, как tooimplement и как toooperate и устранения неполадок. |
| [Обратная запись устройств](active-directory-aadconnect-feature-device-writeback.md) |Описывается, как работает обратная запись устройства в Azure AD Connect. |
| [Расширения каталогов](active-directory-aadconnectsync-feature-directory-extensions.md) |Описывает, как tooextend hello схемы Azure AD с собственные пользовательские атрибуты. |
| **Служба синхронизации** | |
| [Функции службы синхронизации Azure AD Connect](active-directory-aadconnectsyncservice-features.md) |Описывает hello на стороне службы синхронизации и как toochange синхронизировать параметры в Azure AD. |
| [Устойчивость повторяющихся атрибутов](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Описывает способ tooenable и использовать **userPrincipalName** и **proxyAddresses** устойчивости повторяющийся атрибут значения. |
| **Операции и пользовательский интерфейс** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |Описание пользовательского интерфейса диспетчера службы синхронизации, включая hello [операции](active-directory-aadconnectsync-service-manager-ui-operations.md), [соединители](active-directory-aadconnectsync-service-manager-ui-connectors.md), [конструктор метавселенной](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), и [поиска метавселенной](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) вкладок. |
| [Службы синхронизации Azure AD Connect: рабочие задачи и рекомендации](active-directory-aadconnectsync-operations.md) |Описание рабочих задач, например аварийного восстановления. |
| **Практическое руководство.** | |
| [Переустановить учетную запись hello Azure AD](active-directory-aadconnectsync-howto-azureadaccount.md) |Как tooreset hello hello службы учетная запись используется tooconnect из Azure AD Connect sync tooAzure AD. |
| **Дополнительные сведения и ссылки** | |
| [Порты](active-directory-aadconnect-ports.md) |Перечисляет, какие порты вы должны tooopen между подсистема синхронизации hello и локальных каталогов и Azure AD. |
| [Атрибуты, синхронизированные tooAzure Active Directory](active-directory-aadconnectsync-attributes-synchronized.md) |Список всех атрибутов, которые синхронизируются между локальной средой AD и Azure AD. |
| [Справочник по функциям](active-directory-aadconnectsync-functions-reference.md) |Список всех функций, доступных в рамках декларативной подготовки. |

## <a name="additional-resources"></a>дополнительные ресурсы.
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)

