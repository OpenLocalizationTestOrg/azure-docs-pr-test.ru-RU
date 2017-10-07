---
title: "Гибридная идентификация: сравнение инструментов интеграции каталогов | Документация Майкрософт"
description: "Это является страница содержит полную таблицу, которая сравнивает hello различные инструменты интеграции каталогов, которые можно использовать для интеграции каталогов."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Сравнение инструментов интеграции каталогов гибридной идентификации
За годы hello инструменты интеграции каталогов hello увеличил и развитие.  Данный документ является toohelp предоставляют консолидированное представление сведений об этих средствах и сравнение функций hello, доступные в каждом.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect включает в себя компоненты hello и функциональные возможности, которые ранее были выпущены как Dirsync и AAD Sync. Эти средства больше не выполняется по отдельности, а также все последующие улучшения, которые будут включены в обновления tooAzure AD подключения, чтобы всегда знать, где tooget hello самые последние функциональные возможности.
> 
> Компоненты DirSync и Azure AD Sync являются устаревшими. Дополнительные сведения см. [здесь](active-directory-aadconnect-dirsync-deprecated.md).
> 
> 

С помощью следующего ключа по каждой из таблиц hello hello.

● — доступно сейчас;  
FR — в следующем выпуске;  
PP — в общедоступной предварительной версии.  

## <a name="on-premises-toocloud-synchronization"></a>TooCloud локальной синхронизации
| Функция | Подключение Azure Active Directory | Службы синхронизации Azure Active Directory (AAD Sync) | Средство синхронизации Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Подключение toosingle локального леса AD |● |● |● |● |● |
| Подключение toomultiple локальных лесов AD |● |● | |● |● |
| Подключение toomultiple локальных организаций Exchange |● | | | | |
| Подключение каталога LDAP в локальной toosingle |СВ | | |● |● |
| Подключение toomultiple локальным каталогам LDAP |СВ | | |● |● |
| Подключение tooon локальной AD и локальным каталогам LDAP |СВ | | |● |● |
| Подключения систем toocustom (т. е. SQL, Oracle, MySQL, и т. д.) |СВ | | |● |● |
| Синхронизация определенных клиентом атрибутов (расширения каталогов) |● | | | | |
| Подключение локальной tooon HR (т. е. SAP, Oracle eBusiness, PeopleSoft) |СВ | | |● |● |
| Поддерживает правила синхронизации FIM и соединители для подготовки tooon локальные системы. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>TooOn локальной синхронизацией облака
| Функция | Подключение Azure Active Directory | Службы синхронизации Azure Active Directory | Средство синхронизации Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Обратная запись устройств |● | |● | | |
| Обратная запись атрибутов (для гибридного развертывания Exchange) |● |● |● |● |● |
| Обратная запись объектов групп |● | | | | |
| Обратная запись паролей (от самостоятельного сброса пароля (SSPR) и смены пароля) |● |● | | | |

## <a name="authentication-feature-support"></a>Поддержка функции аутентификации
| Функция | Подключение Azure Active Directory | Службы синхронизации Azure Active Directory | Средство синхронизации Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Синхронизация паролей для одного локального леса AD |● |● |● | | |
| Синхронизация паролей для нескольких локальных лесов AD |● |● | | | |
| Единый вход с помощью федерации |● |● |● |● |● |
| Обратная запись паролей (от самостоятельного сброса пароля и смены пароля) |● |● | | | |

## <a name="set-up-and-installation"></a>Установка и настройка
| Функция | Подключение Azure Active Directory | Службы синхронизации Azure Active Directory | Средство синхронизации Azure Active Directory (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| Поддержка установки на контроллере домена |● |● |● | |
| Поддержка установки с помощью SQL Express |● |● |● | |
| Простота обновления из DirSync |● | | | |
| Локализация tooWindows Admin UX серверные языки |● |● |● | |
| Локализация tooWindows UX конечного пользователя серверные языки | | | |● |
| Поддержка Windows Server 2008 и Windows Server 2008 R2 |● для синхронизации, не для федерации |● |● |● |
| Поддержка Windows Server 2012 и Windows Server 2012 R2 |● |● |● |● |

## <a name="filtering-and-configuration"></a>Фильтрация и конфигурация
| Функция | Подключение Azure Active Directory | Службы синхронизации Azure Active Directory | Средство синхронизации Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Фильтрация по доменам и подразделениям |● |● |● |● |● |
| Фильтрация по значениям атрибутов объектов |● |● |● |● |● |
| Разрешить минимальный набор атрибутов toobe синхронизации (MinSync) |● |● | | | |
| Разрешить другую службу шаблоны toobe применения потоков атрибутов |● |● | | | |
| Допускает удаление атрибутов из потока от AD tooAzure AD |● |● | | | |
| Разрешение дополнительной настройки потоков атрибутов |● |● | |● |● |

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

