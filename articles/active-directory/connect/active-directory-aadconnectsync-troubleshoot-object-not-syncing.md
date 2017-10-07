---
title: "Объект, который не выполняют синхронизацию tooAzure AD aaaTroubleshoot | Документы Microsoft"
description: "Устранение неполадок, поэтому объект не выполняют синхронизацию tooAzure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>Устранение неполадок объект, который не выполняют синхронизацию tooAzure AD

Если объект не синхронизировано как ожидаемый tooAzure AD, его можно из-за несколько причин. Если вы получили сообщение электронной почты ошибки из Azure AD или вы видите hello ошибку в Azure AD Connect Health, считываются [Устранение ошибок при экспорте](active-directory-aadconnect-troubleshoot-sync-errors.md) вместо него. Но если нужно устранить проблему, когда hello объекта не содержится в Azure AD, затем в этом разделе для вас. Он описывает, как синхронизировать toofind ошибки в компоненте локальной hello Azure AD Connect.

ошибки toofind hello, будет toolook в нескольких разных местах в hello следующий порядок:

1. Hello [журналы операций](#operations) для поиска ошибки, зарегистрированные в модуле hello синхронизации во время импорта и синхронизации.
2. Hello [пространство соединителя](#connector-space-object-properties) поиска отсутствующих объектов и ошибок синхронизации.
3. Hello [метавселенной](#metaverse-object-properties) для выявления ошибок, связанных с данными.

Прежде чем выполнять эти действия, запустите [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

## <a name="operations"></a>Операции
Вкладка "операции" Hello в hello Synchronization Service Manager является начало Устранение неполадок. Вкладка "операции" Hello показывает результаты hello из самой последней операции hello.  
![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

верхняя половина Hello содержатся все фрагменты в хронические порядке. По умолчанию hello журнала операций хранит сведения о hello последние семь дней, но этот параметр можно изменить с помощью hello [планировщика](active-directory-aadconnectsync-feature-scheduler.md). Требуется toolook любое выполнение, отображают состояние успеха. Вы можете изменить сортировку, щелкая заголовки hello hello.

Hello **состояние** столбец является наиболее важную информацию о hello и отображает hello наиболее серьезной проблемы для запуска. Вот наиболее распространенные состояния hello в порядке приоритета tooinvestigate краткая сводка (где * указания нескольких строк возможна ошибка).

| Состояние | Комментарий |
| --- | --- |
| stopped-* |не удалось запустить Hello. Например если hello удаленной системы не работает и не удается связаться с. |
| stopped-error-limit |Обнаружено более 5000 ошибок. Запустите Hello автоматически остановлена из-за toohello большое количество ошибок. |
| completed-\*-errors |Hello выполнение завершилось, но имеются ошибки (не более 5000), которые должны быть рассмотрены. |
| completed-\*-warnings |Запустите Hello завершена, но некоторые данные не находится в состоянии ожидается hello. Если обнаружены ошибки, такое сообщение обычно является указателем. Пока вы не исправили ошибки, не следует рассматривать предупреждения. |
| Успешное завершение |Проблемы отсутствуют. |

При выборе строки нижней hello обновляет сведения hello tooshow этого запуска. toohello расстояние слева от нижней hello, может возникнуть фраза про список **шаг #**. Он отображается, только если у вас в лесу несколько доменов, где каждый домен представлен шагом. Hello доменное имя можно найти под заголовком hello **секции**. В разделе **статистики синхронизации**, можно найти дополнительные сведения о hello число изменений, которые были обработаны. Можно щелкнуть tooget ссылки hello список объектов hello изменен. Если у вас есть объекты с ошибкой, они отображаются в разделе **Synchronization Errors**(Ошибки синхронизации).

### <a name="troubleshoot-errors-in-operations-tab"></a>Устранение ошибок на вкладке "Operations" (Операции)
![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
При наличии ошибок обоих hello объекта в ошибках и сама ошибка hello являются ссылками, предоставить дополнительные сведения.

Запуск, щелкнув строку hello ошибки (**синхронизации правило ошибка функция — запуск** рисунке hello). Сначала предоставляется обзор hello объекта. toosee hello фактической ошибки, нажмите кнопку "hello" **трассировка стека**. Эта трассировка предоставляет уровня отладки для hello ошибки.

Щелкнуть правой кнопкой мыши в hello **стека вызова** выберите **выбрать все**, и **копирования**. Можно скопировать стек hello и просмотрите ошибки hello в любом редакторе, таком как Блокнот.

* Если ошибка hello из **SyncRulesEngine**, стек вызовов hello сначала получает список всех атрибутов hello объекта. Прокрутите вниз, пока не появится заголовок hello **InnerException = >**.  
  ![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  Строка Hello после показано hello ошибки. На приведенном выше рисунке hello ошибка hello: от пользовательские компании Fabrikam правила синхронизации создана.

Если сама ошибка hello не предоставляет достаточно сведений, является toolook времени на сами данные hello. Можно щелкнуть ссылку hello с идентификатором hello объекта и продолжения устранения hello [импортированный объект пространства соединителя](#cs-import).

## <a name="connector-space-object-properties"></a>Свойства объекта пространства соединителя
Если у вас все ошибки, обнаруженные в hello [операции](#operations) вкладку, а затем hello следующим шагом является объект пространства соединителя hello toofollow из Active Directory, метавселенной toohello и tooAzure AD. В этот путь должен находиться где проблема hello.

### <a name="search-for-an-object-in-hello-cs"></a>Поиск объекта в hello CS

В **Synchronization Service Manager**, нажмите кнопку **соединители**, выберите hello Соединитель Active Directory и **поиска пространства соединителя**.

В **область**выберите **RDN** (при необходимости toosearch hello атрибута CN) или **DN или привязки** (при необходимости toosearch на атрибут distinguishedName hello). Введите значение и нажмите кнопку **Search** (Поиск).  
![Поиск в пространстве соединителя](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Если не удается найти hello объекта вы ищете, то он может были отфильтрованы с [фильтрации на основе домена](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) или [фильтрации на основе Подразделения](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Чтение hello [настроить фильтрацию](active-directory-aadconnectsync-configure-filtering.md) tooverify раздела, hello фильтрации настроен правильно.

Другим полезным поиска — tooselect hello соединителя Azure AD в **область** выберите **ожидания импорта**и выберите hello **добавить** флажок. При таком поиске отображаются все синхронизируемые в Azure AD объекты, которые не могут быть связаны с локальным объектом.  
![Поиск потерянного объекта в пространстве соединителя](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
Эти объекты были созданы другим модулем синхронизации или модулем синхронизации с другими настройками фильтрации. Это представление является списком **потерянных объектов**, управление которыми больше не осуществляется. Этот список изучите и рассмотрите возможность удаления этих объектов с помощью hello [Azure AD PowerShell](http://aka.ms/aadposh) командлетов.

### <a name="cs-import"></a>Импорт в пространстве соединителя
При открытии объекта cs, существует несколько вкладок в верхней hello. Hello **импорта** вкладке отображается данных hello промежуточное после импорта.  
![Объект пространства соединителя](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
Hello **старое значение** показывает, что в настоящее время хранится в Connect и hello **новое значение** то, что был получен из исходной системы hello и еще не были применены. Если возникает ошибка hello объекта, изменения не обрабатываются.

**Ошибка**  
![Объект пространства соединителя](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
Hello **ошибка синхронизации** вкладка отображается только при наличии проблемы с объектом hello. Дополнительные сведения см. в разделе [Устранение ошибок на вкладке "Operations" (Операции)](#troubleshoot-errors-in-operations-tab).

### <a name="cs-lineage"></a>Журнал преобразований пространства соединителя
Вкладка журнала обращений и преобразований Hello демонстрирует, как объект пространства соединителя hello объекта метавселенной связанные toohello. Вы увидите импортируются hello соединителя последнее изменение по сравнению с hello подключенной системы и какие данные toopopulate правил, применяемых в hello метавселенной.  
![Журнал преобразований пространства соединителя](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
В hello **действия** столбца, вы увидите один **Входящие** правило синхронизации с действием hello **подготовки**. Что означает, что при условии, что этот объект пространства соединителя присутствует, hello объекта метавселенной остается. Если вместо этого приведен список hello правила синхронизации правила синхронизации с направлением **исходящие** и **подготовки**, это означает, что данный объект удаляется при удалении объекта метавселенной hello.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
Вы также увидите на hello **PasswordSync** столбец, который hello пространство соединителя входящих могут способствовать пароль toohello изменения с момента одно правило синхронизации имеет значение hello **True**. Затем этот пароль отправляется tooAzure AD через исходящее правило hello.

На вкладке журнала обращений и преобразований hello метавселенной toohello можно получить, щелкнув [свойства объекта метавселенной](#mv-attributes).

Внизу hello все вкладки находятся две кнопки: **предварительного просмотра** и **журнала**.

### <a name="preview"></a>Предварительный просмотр
Предварительный просмотр страницы приветствия представляет один объект toosynchronize используется один. Оно полезно в том случае, если необходимо устранить некоторые правила синхронизации пользовательских, должен toosee hello эффект изменения с одним объектом. Можно выбрать нужный режим: **Full Sync** (Полная синхронизация) и **Delta sync** (Синхронизация изменений). Можно также выбрать между **создать предварительный просмотр**, изменение hello только что сохраняет в памяти, и **зафиксировать предварительного просмотра**, который обновлен метавселенной hello и все этапы изменяет tootarget пространств соединителей.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
Можно было проверить hello объекта и какое правило применяется для конкретного атрибута потока.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>Журнал
Страница журнала Hello — состояния синхронизации пароля используется toosee hello и журнала. Дополнительные сведения см. в статье [Устранение неполадок синхронизации паролей с помощью службы синхронизации Azure AD Connect](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="metaverse-object-properties"></a>Свойства объекта метавселенной
Это обычно лучше toostart поиска из источника hello Active Directory [пространство соединителя](#connector-space). Однако можно также запустить поиск из метавселенной hello.

### <a name="search-for-an-object-in-hello-mv"></a>Поиск объекта в hello MV
В **Synchronization Service Manager** щелкните **Metaverse Search** (Поиск в метавселенной). Создайте запрос, что вы знаете, находит hello пользователя. Можно искать по распространенным атрибутам, таким как accountName (sAMAccountName) или userPrincipalName. Дополнительные сведения см. в статье [Синхронизация Azure AD Connect: Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui-mvsearch.md).
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

В hello **результатов поиска** окно, нажмите кнопку hello объекта.

Если вы не нашли hello объекта, затем он еще не достиг hello метавселенной. Продолжить toosearch для hello объекта в Active Directory hello [пространство соединителя](#connector-space-object-properties). Возможно, возникла ошибка синхронизации, который блокирует hello объекта из ближайшие метавселенной toohello либо может быть применен фильтр.

### <a name="mv-attributes"></a>Атрибуты метавселенной
На вкладке атрибуты hello отображаются значения hello и какой разъема, влияющая его.  
![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

Если объект не синхронизировано, затем просмотрите следующие атрибуты в метавселенной hello hello:
- Является атрибутом hello **cloudFiltered** присутствовать и иметь слишком**true**? Если является, то он были отфильтрованы согласно указаниям toohello [фильтрации на основе атрибута](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering).
- Является атрибутом hello **sourceAnchor** присутствует? Если нет, то есть у вас топология леса ресурсов учетной записи? Если объект идентифицируется как связанный (атрибут hello **msExchRecipientTypeDetails** имеет значение hello 2), то hello sourceAnchor предоставляется лесом hello лес с действующей учетной записью Active Directory. Убедитесь в том, что был импортирован и правильно синхронизированы hello основной учетной записи. Hello основной учетной записи должна быть указана в hello [соединители](#mv-connectors) для hello объекта.

### <a name="mv-connectors"></a>Соединители метавселенной
Hello соединители вкладке отображаются все пространства соединителя, имеющих hello объекта представления.  
![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
Необходимо иметь соединитель для:

- Каждый пользователь hello леса Active Directory будут представлены в. (это представление может содержать объекты foreignSecurityPrincipals и Contact);
- соединителя в Azure AD.

Отсутствующие tooAzure hello соединителя AD считываются [атрибуты MV](#MV-attributes) tooverify hello критериям подготовить tooAzure AD.

Эта вкладка также позволяет toonavigate toohello [объект пространства соединителя](#connector-space-object-properties). Выберите строку и щелкните **Свойства**.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
