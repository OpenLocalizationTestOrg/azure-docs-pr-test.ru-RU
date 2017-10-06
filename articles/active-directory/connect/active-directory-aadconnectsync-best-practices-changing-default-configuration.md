---
title: "Синхронизация Azure AD Connect: изменение конфигурации по умолчанию hello | Документы Microsoft"
description: "Предоставляет рекомендации по изменению конфигурации по умолчанию hello службы синхронизации Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Синхронизация Azure AD Connect: советы и рекомендации по изменению конфигурации по умолчанию hello
Цель этого раздела Hello — toodescribe поддерживаемые и неподдерживаемые изменения tooAzure AD Connect sync.

для большинства сред, которые синхронизации локальной Active Directory с Azure AD, Hello конфигурация, созданная Azure AD Connect работает «как есть». Однако в некоторых случаях это необходимые tooapply tooa toosatisfy конфигурации конкретной некоторых изменений требуется или требования.

## <a name="changes-toohello-service-account"></a>Учетная запись службы toohello изменения
Синхронизация Azure AD Connect работает под учетной записью службы, созданные мастером установки hello. Эта учетная запись службы содержит hello шифрования ключей toohello базе данных, при синхронизации. Он создается с длинного пароля 127 символов и hello пароль устанавливается toonot срока действия.

* Это **неподдерживаемый** toochange или сбросе hello пароль учетной записи службы hello. Это окончательно удаляет ключи шифрования hello и служба hello не является базой данных может tooaccess hello и не может toostart.

## <a name="changes-toohello-scheduler"></a>Изменения toohello планировщика
Начиная с выпусков hello из сборки 1.1 (февраль 2016) можно настроить hello [планировщика](active-directory-aadconnectsync-feature-scheduler.md) toohave различных синхронизации цикла чем по умолчанию hello 30 минут.

## <a name="changes-toosynchronization-rules"></a>Правила изменения tooSynchronization
Мастер установки Hello обеспечивает конфигурацию, которая должна toowork для наиболее распространенных сценариев hello. При необходимости настройки toohello toomake изменения, необходимо выполнить эти правила toostill имеют поддерживаемой конфигурации.

* Вы можете [изменить потоки атрибутов](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) Если hello потоков прямой атрибутов по умолчанию не подходят для вашей организации.
* Если требуется слишком[не будут поступать атрибут](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) и удалить существующий атрибут значения в Azure AD, то должны toocreate правило для этого сценария.
* [Отключайте ненужные правила синхронизации](#disable-an-unwanted-sync-rule) , вместо того чтобы их удалять. Удаленное правило будет снова создано во время обновления.
* слишком[изменить правило out-of-box](#change-an-out-of-box-rule), следует создать копию исходной hello правила и отключить правило out-of-box hello. Редактор правил синхронизации Hello приглашение и помогает.
* Экспортируйте свои пользовательские правила синхронизации с помощью hello редактор правил синхронизации. Hello предоставляет с помощью сценария PowerShell, можно использовать tooeasily повторно создать их в сценарии аварийного восстановления.

> [!WARNING]
> правила синхронизации out-of-box Hello имеют отпечаток. При внесении изменений правил toothese отпечаток hello больше не совпадают. При попытке tooapply нового выпуска Azure AD Connect, могут возникнуть проблемы в будущем hello. Создавать только такие изменения hello, как он описан в этой статье.

### <a name="disable-an-unwanted-sync-rule"></a>Отключайте ненужные правила синхронизации
Не удаляйте правило синхронизации из стандартной конфигурации. Оно будет создано заново при следующем обновлении.

В некоторых случаях конфигурацию, которая не работает для используемой топологии созданных приветствия мастера установки. Например если у вас есть топологии леса ресурсов учетной записи, но схемы расширенные hello hello учетной записи леса с схемы Exchange hello, правила для Exchange создаются для учетной записи hello и лесом ресурсов hello. В этом случае необходимо toodisable hello правило синхронизации для Exchange.

![Отключенное правило синхронизации](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

На приведенном выше рисунке hello приветствия мастера установки обнаружила старой схеме Exchange 2003 в лесу учетных записей hello. Это расширение схемы был добавлен до введения hello леса ресурсов в среде компании Fabrikam. tooensure атрибуты из старой реализации Exchange hello не синхронизированы, следует отключить правило синхронизации hello, как показано.

### <a name="change-an-out-of-box-rule"></a>внести изменения в стандартное правило
Hello только следует изменить правило out-of-box при при необходимости правилом присоединения toochange hello. Если вам требуется toochange поток атрибутов, необходимо создать правило синхронизации с более высокий приоритет, чем правила out-of-box hello. Здравствуйте, только необходимо практически tooclone правила — правило hello **в из AD — User Join**. Все прочие правила можно переопределить правилами с более высоким приоритетом.

При необходимости изменения tooan toomake out-of-box-правило, следует внести копию правило out-of-box hello и отключить исходное правило hello. Создайте правило клонированного toohello изменения hello. Эти действия которого запущено Hello редактор правил синхронизации. Открыв стандартное правило, вы увидите такое диалоговое окно:   
![Предупреждение стандартного правила](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Выберите **Да** toocreate копию hello правило. затем открывается клонированного правило Hello.  
![Клонированное правило](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

На это точная копия правило внесите любые tooscope необходимые изменения, объединения и преобразования.

## <a name="next-steps"></a>Дальнейшие действия
**Обзорные статьи**

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
