---
title: "Соединитель aaaPowerShell | Документы Microsoft"
description: "В этой статье описывается как соединитель tooconfigure Microsoft Windows PowerShell."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Технический справочник по соединителю Windows PowerShell
В этой статье описывается hello соединитель Windows PowerShell. статья Hello относится toohello следующие продукты:

* Microsoft Identity Manager 2016 (MIM2016);
* Forefront Identity Manager 2010 R2 (FIM2010R2).
  * Необходимо установить исправление 4.1.3671.0 или более позднюю версию ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Для MIM2016 и FIM2010R2, hello соединителя доступен для загрузки из hello [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-powershell-connector"></a>Общие сведения о hello PowerShell соединителя
Hello соединителя PowerShell включает службы синхронизации hello toointegrate с внешними системами, которые предоставляют интерфейсы API, на основе Windows PowerShell. Соединитель Hello обеспечивает связь между hello возможности агента управления расширенного подключение с использованием вызова hello 2 framework (ECMA2) и Windows PowerShell. Дополнительные сведения о платформе framework ECMA hello см. в разделе hello [расширяемый Справочник агента управления подключения 2.2](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx).

### <a name="prerequisites"></a>Предварительные требования
Прежде чем использовать hello соединитель, убедитесь, что у вас есть следующие hello hello синхронизации сервера:

* Microsoft .NET Framework, начиная с версии 4.5.2.
* Windows PowerShell 2.0, 3.0 или 4.0.

Hello политику выполнения на сервере службы синхронизации hello должно быть hello соединителя настроенных tooallow toorun-сценариев Windows PowerShell. Если запуска соединителя hello hello скрипты имеют цифровую подпись, настройте политику выполнения hello, запустив следующую команду:  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>Создание нового соединителя
toocreate соединитель Windows PowerShell в службе синхронизации hello, необходимо указать ряд сценариев Windows PowerShell, выполните шаги hello, запрашиваемые hello службы синхронизации. В зависимости от источника данных hello подключения tooand hello функциональных возможностей зависит от hello скриптов, которые необходимо реализовать. В этом разделе описывается каждое hello скриптов, который может быть реализован и когда они необходимы.

Hello соединитель Windows PowerShell предназначены toostore каждого hello скриптов в базе данных службы синхронизации hello. Хотя toorun возможные сценарии, которые хранятся в файловой системе hello, это простой текст hello tooinsert каждого скрипта непосредственно в конфигурации соединителя toohello.

tooCreate соединитель PowerShell в **служба синхронизации** выберите **агент управления** и **создать**. Выберите hello **PowerShell (Майкрософт)** соединителя.

![Создание соединителя](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>Соединение
Укажите параметры конфигурации для подключения tooa удаленной системы. Эти значения безопасно хранятся по hello службы синхронизации и сделать доступной tooyour сценариев Windows PowerShell при запуске соединителя hello.

![Соединение](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

Можно настроить следующие параметры подключения hello.

**Соединение**

| Параметр | Значение по умолчанию | Назначение |
| --- | --- | --- |
| сервер; |<Blank> |Имя сервера, которое hello соединителя необходимо соединиться. |
| Домен |<Blank> |Домен toostore hello учетных данных для использования при запуске соединителя hello. |
| Пользователь |<Blank> |Имя пользователя toostore hello учетных данных для использования при запуске соединителя hello. |
| Пароль |<Blank> |Пароль toostore hello учетных данных для использования при запуске соединителя hello. |
| Выполнять олицетворение учетной записи соединителя |Ложь |Если значение равно true, служба синхронизации hello запускается hello сценариев Windows PowerShell в контексте hello hello учетные данные, предоставленные. Рекомендуется по возможности, что hello **$Credentials** tooeach передается параметр скрипт используется вместо олицетворения. Дополнительные сведения о дополнительных разрешений, необходимых toouse этот параметр, см. в разделе [дополнительная настройка для олицетворения](#additional-configuration-for-impersonation). |
| Загрузить профиль пользователя при олицетворении |Ложь |Указывает, что профиль пользователя Windows tooload hello hello соединителя учетных данных во время олицетворения пользователя. Если hello олицетворенного пользователя перемещаемого профиля, соединитель hello не загружает hello перемещаемого профиля. Дополнительные сведения о дополнительных разрешений, необходимых toouse этого параметра см. в разделе [дополнительная настройка для олицетворения](#additional-configuration-for-impersonation). |
| Тип входа при олицетворении |None |Тип входа при олицетворении. Дополнительные сведения см. в разделе hello [dwLogonType] [ dw] документации. |
| Только для подписанных сценариев |Ложь |Значение true, если соединитель hello Windows PowerShell проверяет, что каждый сценарий имеет действительную цифровую подпись. Если значение равно false, убедитесь в наличии политику выполнения Windows PowerShell служба синхронизации сервера hello RemoteSigned или неограниченный. |

**Общий модуль**  
Соединитель Hello позволяет toostore общий модуль Windows PowerShell в конфигурации hello. Соединитель hello сценарий, запускаемый hello модуль Windows PowerShell извлечь toohello файловой системы, чтобы его можно было импортировать каждый скрипт.

Для сценариев, импорт, экспорт и синхронизация паролей hello общий модуль является извлеченные toohello соединителя MAData папки. Для скриптов обнаружения схемы, проверки, иерархии и секции hello общий модуль является извлеченные toohello папке % TEMP %. В обоих случаях hello извлечь общий модуль с именем сценария в соответствии с toohello общее имя сценария модуля настройки.

tooload модуль вызывается FIMPowerShellConnectorModule.psm1 из папки MAData hello, используйте hello следующей инструкцией:`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

tooload модуль вызывается FIMPowerShellConnectorModule.psm1 из папки % TEMP % hello, используйте hello следующей инструкцией:`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**Проверка параметров**  
Hello скрипт проверки является необязательным сценарий Windows PowerShell, который можно использовать tooensure правильность параметров конфигурации соединителя, выдаваемых Здравствуйте, администратор. Проверка сервера, учетные данные для подключения и параметры подключения, общие способы использования скрипта проверки hello. Hello скрипт проверки вызывается после hello следующие вкладки и диалоговые окна будут изменены:

* Соединение
* Глобальные параметры
* Конфигурация секции

скрипт проверки Hello принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |Вкладка "Конфигурация" Hello или диалоговое окно, запустившего запрос на проверку hello. |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |

сценарий проверки Hello должны возвращать единый конвейер toohello ParameterValidationResult объекта.

**Обнаружение схемы**  
Hello сценарий обнаружения схемы является обязательным. Этот скрипт возвращает типы объектов hello, атрибутов и атрибутов, служба синхронизации используется при настройке правил потока атрибутов приветствия. Hello сценарий обнаружения схемы выполняется во время создания соединителя и заполняет hello соединитель схемы. Он также используется hello действие обновить схему в hello диспетчер службы синхронизации.

скрипт обнаружения схемы Hello принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |

сценарий Hello должны возвращать один [схемы] [ schema] toohello конвейер объектов. Объект схемы Hello состоит из [SchemaType] [ schemaT] объекты, представляющие типы объектов (например: пользователи и группы). Hello SchemaType объект содержит коллекцию [SchemaAttribute] [ schemaA] объектов, которые представляют Привет атрибутов (например: имя, фамилию и почтовый адрес) типа hello.

**Дополнительные параметры**  
Кроме того при toohello стандартных настроек конфигурации, можно определить дополнительные пользовательские параметры конфигурации, определенных toohello экземпляр hello соединителя. Эти параметры указываются в соединитель hello, секции, или выполнения шага уровни и доступных из hello соответствующий сценарий Windows PowerShell. Пользовательские параметры конфигурации могут храниться в базе данных службы синхронизации hello в формате обычного текста или может быть зашифрован. Служба синхронизации Hello автоматически шифрует и расшифровывает безопасную конфигурацию параметров, при необходимости.

toospecify настраиваемыми параметрами конфигурации, отдельные hello имя каждого параметра с запятой (,).

tooaccess настроек пользовательской конфигурации с помощью скрипта, необходимо суффикса имя hello с символа подчеркивания ( \_ ) и область hello параметра hello (Global, раздел или RunStep). Например tooaccess Здравствуйте параметр FileName глобальные, использовать этот фрагмент кода:`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>Возможности
Вкладка возможности Hello hello конструктор агента управления определяет поведение hello и функциональные возможности соединителя hello. Привет, выбранные на этой вкладке нельзя изменить после создания соединителя hello. В этой таблице перечислены параметры возможностей hello.

![Возможности](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| Функция | Описание |
| --- | --- |
| [Стиль различающегося имени][dnstyle] |Указывает, если соединитель hello поддерживает различающиеся имена и таким образом, что стиль. |
| [Тип экспорта][exportT] |Определяет тип объектов, представляемых сценарий экспорта toohello hello. <li>При изменении атрибута hello AttributeReplace — включает в себя полный набор значений для многозначного атрибута hello.</li><li>При изменении атрибута hello AttributeUpdate — включает в себя только hello дельты tooa многозначного атрибута.</li><li>MultivaluedReferenceAttributeUpdate — включает полный набор значений для не являющихся ссылками многозначных атрибутов и только изменения для многозначных ссылочных атрибутов.</li><li>ObjectReplace — включает все атрибуты объекта при изменении любого атрибута.</li> |
| [Нормализация данных][DataNorm] |Прежде чем они предоставляются tooscripts указывает, что hello синхронизации toonormalize привязки атрибуты службы. |
| [Подтверждение объекта][oconf] |Настраивает hello ожидающих поведение при импорте в hello службы синхронизации. <li>Обычный — поведение по умолчанию, который ожидает, что все экспортировать toobe изменения подтверждено посредством импорта</li><li>NoDeleteConfirmation — при удалении объекта ожидание импорта отсутствует.</li><li>NoAddAndDeleteConfirmation — при создании или удалении объекта ожидание импорта отсутствует.</li> |
| Использование DN как привязки |Если hello различающееся имя задан стиль tooLDAP, атрибут привязки hello hello пространства соединителя может быть hello различающееся имя. |
| Параллельная работа нескольких соединителей |Если этот флажок установлен, можно одновременно запустить несколько соединителей Windows PowerShell. |
| Разделы |Если флажок установлен, hello соединитель поддерживает несколько секций и обнаружение раздела. |
| Иерархия |Если флажок установлен, hello соединитель поддерживает иерархическую структуру стиль LDAP. |
| Включить импорт |Если флажок установлен, hello соединитель импортирует данные с помощью импорта скриптов. |
| Включить импорт изменений |Если флажок установлен, hello соединителя можно запросить, отклонений от hello импорта сценариев. |
| Включить экспорт |Если флажок установлен, соединитель hello экспортирует данные через скрипты экспортирования. |
| Включить полный экспорт |Если флажок установлен, hello экспортировать Экспорт пространство всего соединителя hello поддержки скриптов. toouse, также необходимо выбрать этот параметр, включите экспорта. |
| Без ссылочных значений на первом этапе экспорта |Если этот флажок установлен, ссылочные атрибуты экспортируются на втором этапе экспорта. |
| Включить переименование объекта |Если этот флажок установлен, различающиеся имена можно изменить. |
| Удаление и добавление как замена |Если этот флажок установлен, операции удаления и добавления экспортируются как одна операция замены. |
| Включить операции паролей |Если этот флажок установлен, поддерживаются сценарии синхронизации паролей. |
| Включить пароль для экспорта на первом этапе |Если флажок установлен, пароли, которые заданы во время подготовки экспортируются при создании hello объекта. |

### <a name="global-parameters"></a>Глобальные параметры
Hello глобальные параметры на вкладке hello конструктор агента управления позволяет сценариев Windows PowerShell hello tooconfigure под управлением соединителя hello. Можно также настроить глобальных значений для настроек пользовательской конфигурации, определенные на вкладке Подключение hello.

**Обнаружение секции**  
Секция — отдельное пространство имен в пределах одной общей схемы. Например, в Active Directory каждый домен представляет собой секцию в пределах одного леса. Секция — hello логическое группирование для импорта и экспорта. Импорт и экспорт разбиваются на секции по контексту, и все операции выполняются в этом контексте. Секции должны toorepresent иерархии в LDAP. Hello различающееся имя секции используется в tooverify импорта, что все возвращаемые объекты находятся в области действия hello секции. различающееся имя раздела Hello также используется во время инициализации из hello метавселенной toohello соединитель пространства toodetermine hello секции объект должен быть связан с во время экспорта.

скрипт обнаружения секции Hello принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |

Hello скрипт должна вернуть или один [секции] [ part] объекта или списка [T] секции объекты toohello конвейера.

**Обнаружение иерархии**  
сценарий обнаружения иерархии Hello используется только в том случае, когда hello возможность стиля различающееся имя LDAP. сценарий Hello — используется tooallow вы toobrowse и выберите набор контейнеров, считается в или за пределы области действия операции импорта и экспорта. сценарий Hello следует предоставлять только список узлов, которые являются непосредственными дочерними элементами hello корневой узел указан toohello скрипта.

скрипт обнаружения иерархии Hello принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |
| ParentNode |[HierarchyNode][hn] |корневой узел иерархии hello, под которой hello сценарий должен возвращать прямые потомки Hello. |

сценарий Hello должна вернуть или один дочерний объект HierarchyNode или список объектов toohello дочерних HierarchyNode конвейера [T].

#### <a name="import"></a>Импорт
Соединители, которые поддерживают операции импорта, должны реализовать три сценария.

**Начало импорта**  
Hello начать импорта сценарий выполняется в начале hello шага выполнения импорта. На этом этапе можно установить систему toohello исходного подключения и выполнить подготовительные шаги до импорта данных из hello подключения системы.

Hello начать импорт скрипт принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hello сценарий сообщает о hello тип секции импорта запуска (дельта или full), иерархии, водяного знака и ожидаемый размер. |
| Типы |[Schema][schema] |Схема для hello пространства соединителя, который импортируется. |

сценарий Hello должны возвращать один [OpenImportConnectionResults] [ oicres] объекта toohello конвейера, например:`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**Импорт данных**  
Hello импорта данных сценарий называется соединителем hello, пока скрипт hello указывает, что нет дополнительные tooimport данных. Соединитель Windows PowerShell Hello имеет размер страницы 9 999 объектов. Если скрипт возвращает более 9999 объектов для импорта, должна поддерживаться разбивка на страницы. Представляет соединитель Hello, с которой вызывается свойство пользовательские данные, можно использовать хранилище tooa водяного знака, чтобы каждый раз hello импорта данных скрипт, скрипт возобновляет импорта объектов, в котором она остановилась.

скрипт данных Hello импорта принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |Содержит hello водяного знака (CustomData), который может использоваться во время выгружаемого imports и импортирует изменений. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hello сценарий сообщает о hello тип секции импорта запуска (дельта или full), иерархии, водяного знака и ожидаемый размер. |
| Типы |[Schema][schema] |Схема для hello пространства соединителя, который импортируется. |

Hello Импорт данных скрипта необходимо написать списка [[CSEntryChange][csec]] toohello конвейер объектов. Эта коллекция состоит из атрибутов CSEntryChange, представляющих каждый импортируемый объект. При выполнении полного импорта эта коллекция должна содержать полный набор объектов CSEntryChange со всеми атрибутами для каждого объекта. Во время разностный Импорт hello объекта CSEntryChange должен содержать либо hello атрибут уровня дельты для каждого объекта tooimport или полное представление hello объекты, которые были изменены (режим замены).

**Окончание импорта**  
Hello определяется при окончании выполнения импорта hello выполняется hello окончания импорт сценария. Этот скрипт следует выполнять любые задачи очистки необходимые (например, закрыть соединения toosystems и отправки ответа toofailures).

Hello конец импорта сценарий получает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hello сценарий сообщает о hello тип секции импорта запуска (дельта или full), иерархии, водяного знака и ожидаемый размер. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Hello сценарий сообщает о hello причина, по которой был завершен Импорт hello. |

сценарий Hello должны возвращать один [CloseImportConnectionResults] [ cicres] объекта toohello конвейера, например:`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>экспорт.
Архитектура импорта идентичные toohello соединителя hello, соединителей, которые поддерживает экспорт должен реализовывать три скриптов.

**Начало экспорта**  
Hello начать экспорт сценарий выполняется в начале hello шага запуска экспорта. На этом этапе можно установить систему toohello исходного подключения и поведения подготовительные действия перед Экспорт данных toohello подключения системы.

Hello начать экспорт скрипт принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hello сценарий сообщает о hello тип запуска экспорта (дельта или full), секции, иерархии и ожидаемый размер. |
| Типы |[Schema][schema] |Схема для hello пространства соединителя, который экспортируется. |

сценарий Hello не должен возвращать любого toohello конвейера выходные данные.

**Экспорт данных**  
Служба синхронизации Hello вызов сценария Экспорт данных hello столько раз, при необходимости tooprocess всех отложенных операций экспорта. Пространство соединителя hello имеет дополнительные ожидающие операции экспорта, чем hello соединителя размер страницы, hello экспорта сценария данных может быть вызван несколько раз и возможно несколько раз для hello того же объекта.

скрипт данных Hello экспорта принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |
| CSEntries |IList[CSEntryChange][csec] |Список все hello объектов пространства соединителя с ожидающими toobe экспорты, обработанных в ходе этой передачи. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hello сценарий сообщает о hello тип запуска экспорта (дельта или full), секции, иерархии и ожидаемый размер. |
| Типы |[Schema][schema] |Схема для hello пространства соединителя, который экспортируется. |

Hello сценарий экспорта данных должны возвращать [PutExportEntriesResults] [ peeres] toohello конвейер объектов. Этот объект не требуются сведения результат tooinclude для каждого экспортированного соединителя, пока не произойдет ошибка или атрибут привязки toohello изменений. Например tooreturn конвейера toohello PutExportEntriesResults объекта:`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**Окончание экспорта**  
По завершении hello hello экспорта запускается, hello toorun окончания экспортировать скрипт. Этот скрипт следует выполнять любые задачи очистки необходимые (например, закрыть соединения toosystems и отправки ответа toofailures).

сценарий экспорта окончания Hello получает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hello сценарий сообщает о hello тип запуска экспорта (дельта или full), секции, иерархии и ожидаемый размер. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Hello сценарий сообщает о hello причина, по которой hello экспорта была прекращена. |

сценарий Hello не должен возвращать любого toohello конвейера выходные данные.

#### <a name="password-synchronization"></a>Синхронизация паролей
Соединители Windows PowerShell могут использоваться в качестве целевого объекта для изменения или сброса пароля.

скрипт пароль Hello принимает следующие параметры из соединителя hello hello:

| Имя | Тип данных | Описание |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [строка, [ConfigParameter][cp]] |Таблица параметров конфигурации для соединителя hello. |
| Учетные данные |[PSCredential][pscred] |Содержит все учетные данные, введенные администратором hello на вкладке Подключение hello. |
| Секция |[Секция][part] |Раздел каталога, hello CSEntry возможности. |
| CSEntry |[CSEntry][cse] |Элемент пространства соединителя для hello объекта, являющегося получил изменения пароля или сброса. |
| OperationType |Строка |Указывает, является ли операция hello сброса (**SetPassword**) или изменение (**ChangePassword**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Флаги, определяющие hello предназначено поведение при сбросе пароля. Этот параметр доступен, только если для OperationType установлено значение **SetPassword**. |
| OldPassword |Строка |Заполнение со старым паролем hello объекта для изменения пароля. Этот параметр доступен, только если для OperationType установлено значение **ChangePassword**. |
| NewPassword |Строка |Заполняется hello объекта новый пароль, который должен быть задан hello скрипта. |

Здравствуйте скрипт пароль является не ожидаемый tooreturn конвейер Windows PowerShell toohello все результаты. При возникновении ошибки в скрипте пароль hello hello сценария должны вызывать одно из следующих hello tooinform исключения службы синхронизации о проблеме hello hello.

* [PasswordPolicyViolationException] [ pwdex1] — Если hello пароль не соответствует политике паролей hello в системе подключен hello, создается исключение.
* [PasswordIllFormedException] [ pwdex2] — возникает, если пароль hello не является приемлемым для системы подключены hello.
* [PasswordExtension] [ pwdex3] — исключение для всех остальных ошибок в скрипте пароль hello.

## <a name="sample-connectors"></a>Образцы соединителей
Полный обзор соединители доступен образец hello. в разделе [Windows PowerShell соединителя образец соединителя коллекции][samp].

## <a name="other-notes"></a>Другие примечания
### <a name="additional-configuration-for-impersonation"></a>Дополнительные настройки для олицетворения
Предоставьте hello пользователя, олицетворенного hello следующие разрешения на сервере службы синхронизации hello:

Toohello доступ на чтение, следующие разделы реестра:

* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Software\Microsoft\PowerShell
* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Environment

hello toodetermine идентификатор безопасности (SID) hello служба синхронизации учетной записи службы, запустите следующие команды PowerShell hello:

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

Доступ для чтения toohello следующие папки файловой системы:

* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\Extensions;
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\ExtensionsCache;
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

Замените имя hello hello соединитель Windows PowerShell для местозаполнителя hello {свойство}.

## <a name="troubleshooting"></a>Устранение неполадок
* Сведения о как ведение журнала tooenable tootroubleshoot hello соединителя разделе hello [как трассировка ETW для соединителей tooEnable](http://go.microsoft.com/fwlink/?LinkId=335731).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
