---
title: "aaaEnable Enterprise State Roaming в Azure Active Directory | Документы Microsoft"
description: "Часто задаваемые вопросы о параметрах Enterprise State Roaming для устройств Windows. Enterprise State Roaming пользователям предоставляются унифицированного интерфейса на своих устройствах Windows и снижает hello время, необходимое для настройки нового устройства."
services: active-directory
keywords: "службу Enterprise state roaming облака windows как tooenable enterprise состояние роуминга"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Включение службы Enterprise State Roaming в Azure Active Directory
Enterprise State Roaming — доступные tooany организация с подпиской Premium Azure Active Directory (Azure AD). Дополнительные сведения о том, как tooget подписка на Azure AD, в разделе hello [страницу продукта Azure AD](https://azure.microsoft.com/services/active-directory).

При включении Enterprise State Roaming вашей организации будет автоматически предоставлено лицензий для свободного, ограниченного использования подписки tooAzure Rights Management. Это бесплатная подписка — это ограниченная tooencrypting и расшифровки enterprise параметры и данные приложений, синхронизированы hello службы Enterprise State Roaming; требуется платная подписка toouse hello все возможности управления правами Azure.

После получения подписки Azure AD Premium, выполните эти действия, tooenable Enterprise State Roaming.

1. Toohello входа классический портал Azure.
2. В левой части экрана приветствия выберите **ACTIVE DIRECTORY**и выберите каталог hello, для которого требуется tooenable Enterprise State Roaming.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Go toohello **Настройка** вкладки в верхней части hello.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Прокрутите страницу приветствия и выберите **пользователи могут СИНХРОНИЗИРОВАТЬ параметры и данные КОРПОРАТИВНЫХ Приложений**, а затем нажмите кнопку **Сохранить**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Для параметров tooroam устройства Windows 10 с помощью службы Enterprise State Roaming hello hello устройство должно проверять подлинность с помощью удостоверения Azure AD. Для устройств, которые будут присоединены к домену tooAzure AD hello первичного входа пользователя является удостоверение hello Azure AD, поэтому никаких дополнительных настроек не требуется. Для устройств, использующих традиционной локальной Active Directory, hello ИТ-администратору необходимо [подключения tooAzure hello устройств, присоединенных к домену AD, для Windows 10 возникает](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Хранилище данных синхронизации
Enterprise State Roaming данные размещаются в одном или нескольких [регионах Azure](https://azure.microsoft.com/regions/) , лучше ли со значением страны или региона hello в экземпляре Azure Active Directory hello. Данные Enterprise State Roaming разделяются на три основных географических региона: Северная Америка, EMEA (Европа, Ближний Восток и Африка) и APAC (Азия, Тихоокеанский регион и Австралия). Enterprise State Roaming данных для клиента hello расположен локально с hello географический регион и не реплицируются в разных регионах.  Например пользователям более tooone набор значение их страны или региона, EMEA стран, как «Франция» или «Замбия» будет иметь свои данные размещается в одном или hello Azure регионах в Европе.  Пользователи, присвоения значений страны или региона в Azure AD tooone стран Северной Америки, как «США» или «Канада» будет иметь свои данные размещаются в один или несколько hello Azure регионами hello США.  Пользователи, присвоения значений страны или региона в Azure AD tooone стран Азиатско-Тихоокеанском РЕГИОНЕ, как «Australia» или «Новая Зеландия» будет иметь свои данные размещаются в один или несколько hello регионах Azure в Азии.  Южная Америка стран и Антарктике данных будет размещаться в один или несколько регионов Azure в США hello.  значение страны или региона Hello задается как часть процесса создания каталога Azure AD hello и впоследствии нельзя изменить. 

Чтобы получить дополнительные сведения о расположении хранилища данных, отправьте запрос в службу [поддержки Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Управление службой Enterprise State Roaming
Глобальные администраторы Azure AD можно включить и отключить Enterprise State Roaming в hello классический портал Azure.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Глобальные администраторы могут ограничить групп безопасности toospecific параметры синхронизации.

Глобальные администраторы также можно просмотреть отчет о состоянии синхронизации на пользователя устройства, выбрав конкретного пользователя в экземпляре Active Directory hello **пользователей** списка и щелкнув **устройств** и выбрать представление **Устройства, синхронизирующие параметры и данные корпоративных приложений**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Хранение данных
TooAzure данными, синхронизированными через Enterprise State Roaming будут храниться бессрочно, пока выполняется операция удаления вручную или hello данных является определяется toobe устаревшей. 

**Явное удаление:** при администратором Azure удаляет пользователя или каталог или администратор явно запрашивает, данные будут удалены toobe hello данные будут удалены.

* **Удаление пользователя**: при удалении пользователя в Azure AD, учетной записи пользователя hello перемещаемых данных будет помечена для удаления и будут удалены между 90 дней too180. 
* **Удаление каталога**. Весь каталог в Azure AD можно удалить всего в несколько щелчков. Все данные параметры hello, связанные с, каталог будет помечена для удаления и между 90 дней too180 будут удалены. 
* **На запрос удаления**: hello Azure AD администратор планирует toomanually удаления данных конкретного пользователя или параметры данных, Здравствуйте, администратор может заполняют заявку [поддержки Azure](https://azure.microsoft.com/support/). 

**Устаревшие данные удаления**: данные, которые не осуществлялся для одного года («hello срок хранения») будет рассматриваться как устаревшая и может быть удален из Azure. срок хранения Hello является toochange субъекта, но не будут меньше, чем 90 дней. устаревшие данные Hello может быть определенный ряд параметров Windows и приложений и все параметры для пользователя. Например:

* Если устройства не обращаться к коллекции отдельные параметры (например, приложение удаляется с устройства hello или группы параметров, таких как «Тема» отключен для всех устройств пользователя), то эту коллекцию устаревают истечении срока хранения hello и может быть удалены. 
* Если пользователь отключил параметры синхронизации на всех своих устройствах, ни один из данных параметров hello будет осуществляться, и все данные параметры hello для этого пользователя, устаревают и могут быть удалены после периода хранения hello. 
* Если каталог Azure AD Здравствуйте, администратор включит Enterprise State Roaming для hello весь каталог, затем все пользователи, каталог будет остановить синхронизацию параметров, а также все данные параметры для всех пользователей устаревают и могут быть удалены после периода хранения hello. 

**Удалить восстановления данных**: hello политики хранения данных не является настраиваемым. После hello данных был удален без возможности восстановления, его нельзя будет восстановить. Тем не менее очень важно, toonote, hello данные параметры могут быть удалены только из Azure не hello устройства конечного пользователя. Если устройство подсоединении службы Enterprise State Roaming toohello, параметры hello будет снова синхронизированы и хранящихся в Azure.

## <a name="related-topics"></a>Связанные разделы
* [Обзор службы Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Часто задаваемые вопросы о перемещении параметров и данных](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Group Policy and MDM settings for settings sync (Параметры групповой политики и управления мобильными устройствами)](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Справочник по перемещаемым параметрам в Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Устранение неполадок](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
