---
title: "Соединитель Domino aaaLotus | Документы Microsoft"
description: "В этой статье описывается как tooconfigure Microsoft Lotus Domino соединителя."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Технический справочник по соединителю Lotus Domino
В этой статье описывается hello соединителя Lotus Domino. статья Hello относится toohello следующие продукты:

* Microsoft Identity Manager 2016 (MIM2016);
* Forefront Identity Manager 2010 R2 (FIM2010R2).
  * Необходимо установить исправление 4.1.3671.0 или более позднюю версию ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Для MIM2016 и FIM2010R2, hello соединителя доступен для загрузки из hello [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-lotus-domino-connector"></a>Общие сведения о hello соединителя Lotus Domino
Hello соединителя Lotus Domino включает службу синхронизации hello toointegrate с IBM Lotus Domino сервера.

С точки зрения высокого уровня hello текущий выпуск соединителя hello поддерживаются hello следующие атрибуты:

| Функция | Поддержка |
| --- | --- |
| Подключенный источник данных |Сервер:  <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>Клиент:<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| Сценарии |<li>Управление жизненным циклом объекта</li><li>Управление группами</li><li>Управление паролями</li> |
| Операции |<li>Полный импорт и импорт изменений</li><li>экспорт.</li><li>Установка и изменение пароля HTTP</li> |
| Схема |<li>Пользователь (перемещаемый пользователь, контакт (лица без сертификата))</li><li>Группа</li><li>Ресурс (ресурс, комната, собрание по сети)</li><li>База данных для приема писем</li><li>Динамическое обнаружение атрибутов для поддерживаемых объектов</li> |

соединителя Lotus Domino Hello использует клиент toocommunicate hello Lotus Notes с сервера Lotus Domino. В результате этой зависимости поддерживаемый клиент Lotus Notes должен устанавливаться на сервер синхронизации hello. взаимодействие Hello hello клиента и сервера hello реализуется с помощью интерфейса hello взаимодействие .NET Lotus Notes (Interop.domino.dll). Этот интерфейс упрощает hello связь между платформы Microsoft.NET hello и Lotus Notes клиента и поддерживает доступ tooLotus Domino документов и представлений. Для импорта изменений можно также собственного интерфейса hello C++ используется (в зависимости от метода импорта дельта hello выбран).

### <a name="prerequisites"></a>Предварительные требования
Прежде чем использовать hello соединитель, убедитесь, что у вас есть следующие необходимые компоненты на сервере синхронизации hello hello:

* Microsoft .NET Framework, начиная с версии 4.5.2.
* Hello Lotus Notes клиент должен быть установлен на сервера синхронизации
* Hello соединителя Lotus Domino требует hello по умолчанию Lotus Domino LDAP схемы базы данных (schema.nsf) toobe присутствует на сервере каталога Domino hello. Если он отсутствует, его можно установить, запустив или перезапуск службы hello LDAP на сервере Domino hello.

### <a name="connected-data-source-permissions"></a>Права на доступ к подключенному источнику данных
tooperform любой hello поддерживается задачи в соединителя Lotus Domino, необходимо быть членом следующих групп:

* администраторы с правами полного доступа;
* Администраторы
* администраторы базы данных.

Hello следующей таблице перечислены hello разрешения, необходимые для каждой операции.

| Операция | Права доступа |
| --- | --- |
| Импорт |<li>Чтение общедоступных документов</li><li> Полный администратор доступа (Если вы являетесь членом группы администраторов на полный доступ, автоматически получает tooin hello действующие права доступа ACL.)</li> |
| Экспорт и установка пароля |Действующие права доступа:  <li>Создание документов</li><li>Удаление документов</li><li>Чтение общедоступных документов</li><li>Написание общедоступных документов</li><li>Репликация или копирование документов</li>Для операции экспорта необходимо также hello следующих ролей: <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>Прямые операции и AdminP
Операции toohello Domino каталога перейдите непосредственно или через hello AdminP обработки. Hello следующих таблицах перечислены все поддерживаемые объекты, операции и, если это применимо, hello относятся методом реализации:

**Основная адресная книга**

| Объект | Создание | Блокировка изменений | Удалить |
| --- | --- | --- | --- |
| Person |AdminP |Напрямую |AdminP |
| Группа |AdminP |Напрямую |AdminP |
| База данных для входящих писем |Напрямую |Напрямую |Напрямую |
| Ресурс |AdminP |Напрямую |AdminP |

**Вторичная адресная книга**

| Объект | Создание | Блокировка изменений | Удалить |
| --- | --- | --- | --- |
| Person |Недоступно |Напрямую |Напрямую |
| Группа |Напрямую |Напрямую |Напрямую |
| База данных для входящих писем |Напрямую |Напрямую |Напрямую |
| Ресурс |Недоступно |Недоступно |Недоступно |

При создании ресурса создается документ Notes. Аналогично при удалении ресурса hello заметках удаляется.

### <a name="ports-and-protocols"></a>Порты и протоколы
Клиент IBM Lotus Notes и серверы Domino взаимодействуют с использованием протокола удаленного вызова процедур Notes (NRPC), реализуемого через TCP/IP. номер порта по умолчанию Hello 1352, однако может изменить администратором Domino hello.

### <a name="not-supported"></a>Не поддерживается
Текущий выпуск соединителя Lotus Domino hello hello не поддерживаются Hello следующие операции:

* Перемещение почтовых ящиков между серверами.

## <a name="create-a-new-connector"></a>Создание нового соединителя
### <a name="client-software-installation-and-configuration"></a>Установка и настройка клиентского программного обеспечения
Lotus Notes должны быть установлены на сервере hello **перед** hello, где установлен соединитель.

Выберите вариант **Single User Install**(Установка для одного пользователя). по умолчанию Hello **установить многопользовательский** не работает.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

На странице функции hello, устанавливать только hello требуется Lotus Notes компонентов и **единого входа клиента**. Единый вход является обязательным для hello соединитель toobe может toolog на сервере toohello Domino.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**Примечание:** начала Lotus Notes после с пользователем, который находится на hello сервере hello учетной записи можно использовать как hello учетная запись службы соединителя. Также можно сделайте убедиться, что клиент Lotus Notes hello tooclose на сервере hello. Она не может быть запущена на hello же время hello соединителя пытается tooconnect toohello Domino сервера.

### <a name="create-connector"></a>Создание соединителя
tooCreate соединителя Lotus Domino в **служба синхронизации** выберите **агент управления** и **создать**. Выберите hello **Lotus Domino (Майкрософт)** соединителя.  
![Создание соединителя](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

Если вашей версии службы синхронизации предлагает возможность tooconfigure hello **архитектура**, убедитесь, что соединитель hello задается toorun значение по умолчанию tooits в **процесс**.

### <a name="connectivity"></a>Соединение
На странице приветствия подключения необходимо указать имя сервера Lotus Domino hello и введите учетные данные для входа hello.  
![Соединение](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

Свойство сервера Domino Hello поддерживает два формата hello имя сервера:

* имя_сервера;
* имя_сервера/имя_каталога.

Hello **имя_сервера/имя_каталога** является предпочтительным форматом hello для этого атрибута, так как он обеспечивает быстрый ответ при контакты соединителя hello hello Domino Server.

Hello при условии, что UserID файл хранится в базе данных конфигурации hello hello службы синхронизации.

Для параметра **Delta Import** (Разностный импорт) доступны следующие значения:

* **None**. Hello соединитель не выполняет любых изменений импортов.
* **Add/Update** (Добавление и обновление). Hello соединитель выполняет разностный Импорт добавьте и операции обновления. Операции удаления выполняются только при выбранном значении **Full Import** (Полный импорт). Эта операция использует взаимодействие .net hello.
* **Add/Update/Delete** (Добавление, обновление и удаление). Hello соединитель выполняет разностный импорт добавление, обновление и удаление операций. Эта операция использует собственные интерфейсы C++ hello.

В **параметры схемы** у вас есть hello следующие параметры:

* **Default-Schema** (Схема по умолчанию). Hello соединителя обнаруживает hello схемы с сервера Domino hello. Выбирается параметр по умолчанию hello.
* **DSML-Schema**(Схема DSML) — используется только в том случае, если сервер Domino не предоставляет доступ к схеме. Используется, только если сервер Domino hello не предоставлять доступ к схеме hello. Затем можно создать файл DSML со схемой hello и импортировать его вместо. в документации по [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml).

Если нажать кнопку "Далее", проверяются hello идентификатор пользователя и пароль параметры конфигурации.

### <a name="global-parameters"></a>Глобальные параметры
На странице приветствия глобальные параметры настройки часового пояса hello и импорта hello и операции по экспорту.  
![Глобальные параметры](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

Hello **часовым поясом сервера Domino** параметр определяет расположение hello сервера Domino.

Этот параметр конфигурации является обязательным toosupport **разностный Импорт** операции, так как она позволяет служба синхронизации hello определение изменений между двумя двух последних imports hello.

>[!Note]
Начиная с hello марта 2017 г. обновление hello глобальные параметры экрана содержит mail toodelete hello hello параметра пользовательской базы данных во время удаления пользователя hello.

![Удаление почтового ящика пользователя](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>Параметры и метод выполнения импорта
Hello **выполнить полный импорт по** имеет следующие параметры:

* Поиск
* View (Просмотр) (рекомендуемое значение).

**Поиск** — по индексам в Domino, но чаще всего, hello индексы не обновляются в режиме реального времени и hello данные, возвращаемые с сервера hello не всегда правильно работает. Для системы с большим количеством изменений такой вариант не лучший, так как он может иногда отображать ложные данные. Тем не менее метод **Search** (Поиск) выполняется быстрее, чем метод **View** (Просмотр).

**Представление** является hello рекомендуемый параметр, поскольку она имеет правильное состояние hello данных. Он немного медленнее, чем метод поиска.

#### <a name="creation-of-virtual-contact-objects"></a>Создание виртуальных контактных объектов
Hello **разрешить создание \_объект контакт** имеет следующие параметры:

* None
* Non-Reference Values (Значения, не являющиеся ссылками).
* Reference and Non-Reference Values (Значения, являющиеся и не являющиеся ссылками).

В Domino атрибуты этих ссылок может содержать множество разных форматов tooreference другие объекты. различных вариантов может toorepresent toobe hello соединителя реализует \_обратитесь к объектам, также известный как **виртуального контактов** (VC). Эти объекты создаются, их можно соединить объекты tooexisting MV или защищен как новые объекты. Благодаря этому они могут сохранять ссылки на атрибуты.

При включении этого параметра и не hello содержимое ссылочный атрибут в формате DN \_создания объекта контакта. Например, атрибут членства в группе может содержать SMTP-адреса. Это также возможно toohave короткого имени и другие атрибуты представить в атрибуты этих ссылок. В таком случае выберите вариант **Non-Reference Values**(Значения, не являющиеся ссылками). Такая настройка является наиболее распространенные приветствия для реализаций Domino.

Lotus Domino настроенных toohave отдельный адрес электронной с разными именами различающееся представляющий hello одного объекта, создать возможные tooalso \_обратитесь в службу объекты для всех значений ссылки, найденные в адресную книгу. Для этого сценария выберите hello **ссылки и значения не ссылка** параметр.

При наличии нескольких значений в атрибуте hello **FullName** в Domino, затем также требуется создание hello tooenable виртуального контактов, ссылки может быть разрешено. Например, этот атрибут может иметь несколько значений после объединения или разъединения. Установите флажок hello **включить... FullName has multiple values** (Разрешить несколько значений для FullName).

Соединяя правильные атрибуты hello hello \_объекта контакта будут присоединены к домену toohello MV объекта.

Эти объекты имеют VC =\_контакт добавлен tootheir DN.

#### <a name="import-settings-conflict-object"></a>Параметры импорта — конфликтующий объект
**Исключение конфликтующего объекта**

В больших Domino реализацию возможно, что несколько объектов имеют hello таким же доменным Именем из-за проблем с tooreplication. В этих случаях соединителя hello увидит два объекта с таким же доменным Именем, но разные UniversalIDs. Этот конфликт вызовет временный объект создается в пространство соединителя hello. Hello соединителя можно игнорировать hello объекты, которые были выбраны в Domino как жертвы репликации. Hello рекомендуется tookeep, этот флажок установлен.

#### <a name="export-settings"></a>Параметры экспорта
Если hello параметр **AdminP использовать для обновления ссылок** не выбран, то при экспорте ссылочные атрибуты, например член, прямой вызов и не использует процесс AdminP hello. Этот параметр следует используйте только при AdminP не было настроенных toomaintain ссылочной целостности.

#### <a name="routing-information"></a>Сведения о маршрутизации
В Domino возможно, что сведения о маршрутах, внедренных в качестве суффикса toohello DN у ссылочный атрибут. Например, может содержать атрибут элемента hello в группе **CN =example/organization@ABC**. суффикс Hello @ABC — сведения о маршрутизации hello. сведения о маршрутизации Hello используется системой Domino toosend сообщения электронной почты toohello правильный Domino, которая может быть системы в другой организации. В поле сведения о маршрутизации hello можно указать hello маршрутизации суффиксов, используемых в организации hello в области hello соединителя. Если одно из следующих значений находится в качестве суффикса в ссылочный атрибут, сведения о маршрутизации hello удаляется из ссылки hello. Если суффикс маршрутизации hello на значение ссылки не может быть сопоставленная tooone эти значения указаны, \_создания объекта контакта. Эти \_были созданы объекты "Контакт" **RO = @<RoutingSuffix>**  вставлена hello DN. Для этих \_объекты "Контакт" hello, следующие атрибуты, также добавлены присоединение tooa реальным объектом, при необходимости tooallow: \_routingName, \_contactName, \_displayName и UniversalID.

#### <a name="additional-address-books"></a>Дополнительные адресные книги
Если у вас **directory помощь** установлен, который предоставляет имя hello дополнительный адрес электронной, а затем можно вручную ввести эти книги.

#### <a name="multivalued-transformation"></a>Многозначные преобразования
Многие атрибуты в Lotus Domino являются многозначными. Hello соответствующих атрибутов метавселенной обычно один табличное значение. Настроив hello импорта и hello параметр операции экспорта, включить toohelp hello соединителя с переводом hello необходимых атрибутов влияет hello.

**Экспорт**  
параметр операции экспорта Hello поддерживает два режима:

* Append item (Добавить элемент).
* Replace item (Заменить элемент).

**Заменить элемент** — при выборе этого параметра всегда соединителя hello remove hello текущие значения атрибута hello в Domino и замените hello предоставленных значений. предоставленный Hello табличные значения может быть однозначными или несколькими значениями.

Пример: атрибут помощника hello объекта person имеет hello следующие значения:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf;
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf.

Если с именем нового помощника **David Alexander** — назначены toothis объекта person, hello получается:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf.

**Добавление элемента** — при выборе этого параметра соединителя hello сохраняет hello существующие значения для атрибута hello в Domino и вставить новые значения в начале hello hello данных списка.

Пример: атрибут помощника hello объекта person имеет hello следующие значения:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf;
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf.

Если с именем нового помощника **David Alexander** — назначены toothis объекта person, hello получается:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf.
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf;
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf.

**Импорт**  
параметр операции импорта Hello поддерживает два режима:

* значение по умолчанию
* Многозначные tooSingle значение

**По умолчанию** — при выборе параметра по умолчанию hello, все значения всех hello атрибуты импортируются.

**Многозначные tooSingle значение** — при выборе этого параметра многозначный атрибут преобразуется в однозначного атрибута. Если существует более одного значения, используется значение hello в верхней части hello (это значение обычно равно также hello последняя версия).

Пример: атрибут помощника hello объекта person имеет hello следующие значения:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf.
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf;
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf.

Hello самые последние обновления toothis атрибут является **David Alexander**. Поскольку параметр операции импорта hello tooMultivalued tooSingle значение, соединитель импортирует только **David Alexander** в пространство соединителя hello.

Hello логику tooconvert многозначных атрибутов в атрибуты с одним значением не применяется атрибут члена группы toohello и toohello лица полное имя атрибута.

Он также tooconfigure можно импортировать и экспортировать правила преобразования для многозначных атрибутов каждого атрибута, как глобальные правила исключения toohello. tooconfigure этот параметр, введите [objecttype]. [attributename] в hello **импорта списка исключений атрибут** и **экспортировать список исключений атрибут** текстовые поля. Например если ввести Person.Assistant и hello глобальный флаг имеет значение tooimport все значения, только первое значение hello импортируется помощник hello.

#### <a name="certifiers"></a>Заверители
Соединителем hello отобразятся все устройства организации или организации. toobe может tooexport лица объекты toohello основной адрес книги, certifier с ее пароль не требуется.

Если все certifiers hello тем же паролем, hello **пароль для всех Certifers** может использоваться. Затем можно ввести здесь пароль hello и только указать файл certifier hello.

Если импортировать только, затем у вас toospecify любой certifiers.

### <a name="configure-provisioning-hierarchy"></a>Настройка иерархии подготовки
При настройке соединителя Lotus Domino hello, пропустите это диалоговое окно. соединителя Lotus Domino Hello не поддерживает подготовку иерархии.  
![Иерархия подготовки](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>Настройка разделов и иерархий
При настройке разделов и иерархий, необходимо выбрать основной адрес книги hello, называется NAB=names.nsf. В дополнение к этому toohello основной адрес книги, можно выбрать дополнительный адрес электронной, если они существуют.  
![Разделы](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>Выбор атрибутов
При настройке атрибутов следует выбрать все атрибуты, которые начинаются с префикса **\_MMS\_**. Эти атрибуты обязательны при подготовке новых объектов tooLotus Domino

![Атрибуты](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>Управление жизненным циклом объекта
В этом разделе Обзор различных объектов hello в Domino.

### <a name="person-objects"></a>Объекты Person
Hello объекта person представляет пользователей в организации и подразделения. Также атрибуты по умолчанию toohello Здравствуйте, администратор Domino можно добавлять настраиваемые атрибуты объекта Person tooa. Объект Person должен содержать все обязательные атрибуты, это базовое требование. Полный список обязательных атрибутов см. в разделе [Свойства Lotus Notes](#lotus-notes-properties). tooregister объект person hello следующие предварительные условия должны быть выполнены.

* необходимо, Hello адресную книгу (names.nsf) был определен и он должен быть hello основной адрес книги.
* Необходимо быть hello O/OU certifier идентификатор и hello пароль tooregister конкретного пользователя hello организации и подразделения.
* Для объекта Person необходимо определить набор свойств Lotus Notes. Эти свойства используются для инициализации объекта person hello. Дополнительные сведения см. в разделе hello раздел под названием [свойства Lotus Notes](#lotus-notes-properties) далее в этом документе.
* Hello исходного пароля HTTP для пользователя — это атрибут и набора во время инициализации.
* Hello объекта person должен быть одним из hello следующие три поддерживаемые типы:
  1. Обычный пользователь с почтовым файлом и файлом идентификатора пользователя.
  2. Перемещаемый пользователь (обычный пользователь со всеми файлами перемещаемых баз данных).
  3. Контакт (пользователь без файла идентификатора).

Лиц (за исключением контактов) дальнейшей могут группироваться в нам и International пользователей, в соответствии с определением hello значение hello \_MMS\_IDRegType свойство. Этим пользователям использовать tooaccess клиента Notes hello серверы Lotus Domino, имеют идентификатор заметки и документа человека. Для пользователей, которые используют Notes Mail, также создается файл электронной почты. Hello пользователь должен быть зарегистрированных toobecome active. Дополнительные сведения можно найти в разделе 

* [Настройка пользователей Notes](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [Регистрация пользователей](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [Управление пользователями](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [Переименование пользователей](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

Все эти операции выполняются в Lotus Domino и затем импортировать в службы синхронизации hello.

### <a name="resources-and-rooms"></a>Ресурсы и комнаты
Ресурс — это другой тип базы данных в Lotus Domino. Ресурсы могут быть представлены переговорными с таким оборудованием, как проекторы. Существует подтипы поддерживаемые соединителя Lotus Domino ресурсов, которые определяются hello атрибута типа ресурса.

| Тип ресурса | Атрибут типа ресурса |
| --- | --- |
| Комната |1 |
| Ресурс (другое) |2 |
| Собрания по сети |3 |

Hello toowork тип ресурса для объекта hello следующих условий.

* База данных резервирования ресурсов должна уже существовать на сервере подключен hello Domino
* Hello сайта уже определено для hello ресурсов

База данных Hello резервирования ресурсов содержит три типа документов.

* профиль сайта;
* Ресурс
* резервирование.

Дополнительные сведения о настройке резервирования ресурсов базы данных см. в разделе [при настройке базы данных резервирования ресурсов hello](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html).

**Создание, обновление и удаление ресурсов**  
Hello операций Create, Update и Delete выполняется путем соединителя Lotus Domino hello в базе данных hello резервирования ресурсов. Ресурсы создаются как документы в Names.nsf (то есть hello основной адрес книги). Дополнительные сведения об изменении и удалении ресурсов см. в разделе [Editing and deleting Resource documents](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html) (Изменение и удаление документов ресурсов).

**Операции импорта и экспорта ресурсов**  
Hello ресурсы могут быть импортированных tooand, экспортированные из служба синхронизации hello, как и любой другой тип объекта. Привет, выберите тип объекта в качестве ресурса во время настройки. Для успешного экспорта нужно указать тип ресурса, базу данных конференции и имя сайта.

### <a name="mail-in-databases"></a>Базы данных для приема писем
Почты базы данных является базой данных, разработанные tooreceive электронных писем. Это почтовый ящик Lotus Domino, который не связан с конкретной учетной записью Lotus Domino (т. е. не имеет файл идентификатора и пароль). База данных для приема писем имеет связанный уникальный идентификатор пользователя (short name) и собственный адрес электронной почты.

Если нужно создать отдельный почтовый ящик с собственным адресом электронной почты, который будут совместно использовать несколько пользователей (например, group@contoso.com), следует создать базу данных для приема писем. почтовый ящик toothis доступа Hello осуществляется через его управления список управления Доступом, который содержит имена hello hello заметки пользователей, которые допускаются почтовых ящиков tooopen hello.

Список атрибутов, требуется hello, в разделе hello вызывается [обязательных атрибутов](#mandatory-attributes) далее в этой статье.

Когда база данных спроектированный tooreceive почты, документ Mail в базе данных создается в Lotus Domino. Этот документ должен присутствовать в каталоге Domino каждого сервера, в которой хранятся копии базы данных hello. Процесс создания документов базы данных для приема писем подробно описан в разделе [Creating a Mail-In Database document](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html)(Создание документа базы данных для приема писем).

Перед созданием базы данных по почте, hello база данных должна уже существовать (должен быть создан администратором Lotus) на сервере Domino hello.

### <a name="group-management"></a>Управление группами
Подробный обзор hello Lotus Domino группы управления можно получить из hello следующие ресурсы:

* [Использование групп](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [Создание группы](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [Создание и изменение групп](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [Управление группами](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [Переименование группы](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>Управление паролями
Для зарегистрированного пользователя Lotus Domino существует два типа паролей:

1. Пароль пользователя (хранится в файле User.id).
2. Пароль HTTP (для доступа через Интернет).

соединителя Lotus Domino Hello поддерживает только операции с паролем HTTP.

Управление паролями tooperform, следует включить управление паролями для соединителя hello в hello конструктор агента управления. Управление паролями tooenable, выберите **включить управление паролями** на hello **Настройка расширений** странице диалогового окна.  
![Configure Extensions](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

Поддержка соединителя Lotus Domino Hello следующие операции с Интернет-пароль:

* Задать пароль: Пароль набора задает новый пароль, Интернета HTTP пользователя hello в Domino. По умолчанию hello учетной записи также разблокирован. Hello разблокировать флаг предоставляется hello WMI в интерфейсе hello подсистема синхронизации.
* Изменение пароля: В этом случае пользователь может потребоваться пароль hello toochange или — запрос toochange пароль после указанного времени. Для этой операции tootake месте как (hello старый и новый пароль hello) являются обязательными. После изменения в Lotus Domino обновляется hello новый пароль.

Дополнительные сведения можно найти в разделе 

* [С помощью функции блокировки Интернет hello](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [Управление паролями доступа через Интернет](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>Справочная информация
В этом разделе перечислены как атрибут описания и требования к атрибутам для соединителя Lotus Domino hello.

### <a name="lotus-notes-properties"></a>Свойства Lotus Notes
При подготовке каталога Lotus Domino tooyour объектов лица вашей объекты должны иметь определенный набор свойств с определенными значениями заполнен. Эти значения необходимы только для операций создания объектов.

Hello следующей таблице перечислены эти свойства и их описание.

| Свойство | Описание |
| --- | --- |
| \_MMS_AltFullName |Hello альтернативный полное имя пользователя. |
| \_MMS_AltFullNameLanguage |Hello toobe язык, используемый для указания альтернативного hello полное имя пользователя. |
| \_MMS_CertDaysToExpire |Срок действия истекает Hello количество дней от hello текущую дату перед hello сертификата. Если не указан, hello по умолчанию используется два года из hello текущую дату. |
| \_MMS_Certifier |Свойство, содержащее имя организационной иерархии hello hello certifier. Например: OU=OrganizationUnit,O=Org,C=Country. |
| \_MMS_IDPath |Если свойство hello пуст, пользователь идентификации файл не создается локально на приветствия сервера синхронизации. Если свойство hello содержит имя файла, файл идентификатор пользователя создается в папке madata hello. Свойство Hello также может содержать полный путь. |
| \_MMS_IDRegType |Пользователей можно классифицировать как контакты, пользователи США и международные пользователи. Hello следующей таблице перечислены возможные значения hello. <li>0 — контакт.</li><li>1 — пользователь США.</li><li>2 — международный пользователь.</li> |
| \_MMS_IDStoreType |Обязательное свойство для пользователей США и международных пользователей. Свойство Hello содержит целочисленное значение, указывающее ли hello Идентификация пользователя хранится как вложение в hello заметки адресной книге или в файле mail hello человека. Если файл идентификатор пользователя hello вложения в адресной книге hello, его можно создать при необходимости в файле с \_MMS_IDPath. <li>Пусто — файл идентификатора хранится в хранилище идентификаторов или такого файла нет (используется для контактов).</li><li> 1 — вложение в адресной книге hello заметки. Hello \_MMS_Password свойство необходимо задать для файлов идентификации пользователя, вложения</li><li>2 — идентификатор хранится в файле электронной почты пользователя. Hello \_MMS_UseAdminP необходимо задать toofalse toolet hello mail создан файл во время регистрации пользователя hello. Hello \_MMS_Password свойству необходимо присвоить для идентификации файлов пользователя.</li> |
| \_MMS_MailQuotaSizeLimit |Hello число мегабайт, разрешенные для hello электронной почты файл базы данных. |
| \_MMS_MailQuotaWarningThreshold |число мегабайт, разрешенные для hello электронной почты файл базы данных, прежде чем создается предупреждение, Hello. |
| \_MMS_MailTemplateName |файл шаблона Hello по электронной почте, файл электронной почты пользователя используется toocreate hello. Если указан шаблон, hello почтовый файл создается с использованием указанного шаблона hello. Если шаблон не указан, файл шаблона по умолчанию hello — файл используется toocreate hello. |
| \_MMS_OU |Необязательное свойство, которое является имя Подразделения hello под hello certifier. Это свойство должно быть пустым для контактов. |
| \_MMS_Password |Обязательное свойство для пользователей. Свойство Hello содержит hello пароль для файла идентификации hello hello объекта. |
| \_MMS_UseAdminP |Свойство должно быть tootrue набор, если должен быть создан файл mail hello hello AdminP процессом на сервере Domino hello (toohello асинхронный процесс экспорта). Если свойство имеет значение toofalse, hello почты файл создается с hello Domino пользователя (в синхронном режиме в процессе экспорта hello). |

Пользователь с файлом связанный код, hello \_MMS_Password свойство должно содержать значение. Для доступа к электронной почте через клиент Lotus Notes hello hello MailServer и MailFile свойства пользователя должно содержать значение.

tooaccess электронной почты через веб-браузер, hello следующие свойства должны содержать значения:

* MailFile - обязательное свойство, содержащее hello путь на сервере Lotus Domino hello, где хранится файл mail hello.
* MailServer - обязательное свойство, содержащее имя сервера Lotus Domino hello hello. Это значение является именем toouse hello при создании файла почты hello Lotus Domino сервера hello.
* HTTPPassword - необязательное свойство, которое содержит пароль доступа к Web hello hello объекта.

tooaccess Здравствуйте Domino сервера без возможности почты, hello HTTPPassword свойство должно содержать значение. Здравствуйте, свойство MailFile и hello MailServer свойство может быть пустым.

С \_MMS_ IDStoreType (идентификатор магазина в файле Mail), 2 = hello MailSystem свойство NotesRegistrationclass имеет значение tooREG_MAILSYSTEM_INOTES (3).

### <a name="mandatory-attributes"></a>Обязательные атрибуты
соединителя Lotus Domino Hello главным образом поддерживает следующие типы объектов (типов документов):

* Группа
* База данных для приема писем
* Person
* Контакт (лицо без заверителя)
* Ресурс

В этом разделе перечислены hello атрибуты, которые являются обязательными для каждого сервера Domino tooa tooexport поддерживаемых объектов.

| Тип объекта | Обязательные атрибуты |
| --- | --- |
| Группа |<li>ListName</li> |
| База данных для приема почты |<li>FullName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Person |<li>LastName</li><li>MailFile</li><li>ShortName</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| Контакт (лицо без заверителя) |<li>\_MMS_IDRegType</li> |
| Ресурс |<li>FullName</li><li>ResourceType</li><li>ConfDB</li><li>ResourceCapacity</li><li>Сайт</li><li>displayName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>Распространенные проблемы и вопросы
### <a name="schema-detection-does-not-work"></a>Не работает определение схемы
Схема hello может toodetect toobe, это необходимо, что этот файл schema.nsf hello присутствует на сервере Domino hello. Этот файл отображается, только если на сервере hello установлен LDAP. Если схемы hello не удается обнаружить, проверьте следующие hello.

* файл schema.nsf Hello, находятся в корневой папке сервера Domino hello hello
* Hello пользователем файл schema.nsf hello toosee разрешений.
* Принудительно выполнять перезагрузку сервера LDAP hello. Откройте **Lotus Domino консоли** и использовать **ReloadSchema сообщить LDAP** команда tooreload hello схемы.

### <a name="not-all-secondary-address-books-are-visible"></a>Отображаются не все дополнительные адресные книги.
Hello соединителя Domino основан на hello функции **Directory помощь** toobe может toofind hello дополнительный адрес электронной. Если hello дополнительный адрес электронной пропущены, проверить, если [Directory помощь](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) включен и настроен на приветствия сервера Domino.

### <a name="custom-attributes-in-domino"></a>Настраиваемые атрибуты для Domino
Существует несколько способов в схеме hello tooextend Domino, она появляется в качестве настраиваемого атрибута к использованию по hello соединителя.

**Способ 1. Расширение схемы Lotus Domino**

1. Создать копию шаблона каталога Domino {PUBNAMES. НФПК}, следуя [эти действия](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (не Настройка каталога IBM Lotus Domino по умолчанию hello шаблона):
2. Шаблон каталога копирования Domino Привет открыть {CONTOSO. Шаблон НФПК}, который был создан в конструкторе Domino и выполните следующие действия:
   * Щелкните Shared Elements (Общие элементы) и разверните подчиненные формы.
   * Дважды щелкните подчиненной InheritableSchema ${ObjectName} ({ObjectName} где hello имя класса структурного объекта по умолчанию hello, например: лица).
   * Имя атрибута hello требуется tooadd в схему {MyPersonAtrribute} и соответствующий атрибут toothat. Создать поле, выберите hello **создать** меню и выберите **поле** меню.
   * В поле hello задайте его свойства, выбрав его тип, стиль, размер, шрифт и другие связанные параметры в поле «свойства».
   * Атрибут hello Keep таким же значением по умолчанию как hello имя, заданное для этого атрибута (например, если имя атрибута MyPersonAttribute, оставьте значение по умолчанию hello с hello таким же именем).
   * Сохраните подчиненной InheritableSchema hello ${ObjectName} с обновленными значениями.
3. Замените hello шаблона каталога Domino {PUBNAMES. НФПК} с новый настраиваемый шаблон hello {CONTOSO. НФПК}, следуя [эти действия](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
4. Закройте Domino администратора и откройте hello toorestart Domino консоли службы LDAP и tooReload hello схемы LDAP:
   * В консоли Domino, вставьте команду «hello» в **Domino команда** текст зарегистрирована служба LDAP hello toorestart - [перезапустить задачу LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
   * схемы LDAP tooreload команда сообщить LDAP - сообщить ReloadSchema LDAP
5. Откройте администратор Domino и выберите вкладку toosee людей и групп добавляется атрибут отражается в domino добавить пользователя.
6. Откройте schema.nsf на вкладке **Файлы** и убедитесь, что добавленный атрибут отражается в классе объекта LDAP dominoPerson.

**Способ 2: Создайте auxClass с настраиваемого атрибута и свяжите с классом hello объекта**

1. Создать копию шаблона каталога Domino {PUBNAMES. НФПК}, следуя [эти действия](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (никогда не Настройка каталога IBM Lotus Domino по умолчанию hello шаблона):
2. Шаблон каталога копирования Domino Привет открыть {CONTOSO. Шаблон НФПК}, который был создан в конструкторе Domino.
3. В левой области hello выберите общего кода, а затем подчиненные формы.
4. Щелкните New Subform (Создать подчиненную форму).
5. Здравствуйте, следующие свойства hello toospecify для нового подчиненной hello:
   * Открыв новый подчиненной hello, выберите макет - подчиненной свойства
   * Далее toohello свойство Name, введите имя для класса вспомогательный объект hello — например, TestSubform.
   * Безопасность hello параметры «Включить в подчиненной Insert... диалогового окна»
   * Снимите флажок свойства Options hello «Отрисовки, проходят через HTML в заметках».
   * Оставьте hello, другие же hello свойства и закрыть окно свойств подчиненной hello.
   * Сохраните и закройте новый подчиненной hello.
6. Здравствуйте, следующие tooadd класса вспомогательный объект hello toodefine поля:
   * Откройте hello подчиненную форму, которую вы создали.
   * Выберите Create (Создать) и Field (Поле).
   * Далее tooName вкладки основы hello поля диалогового окна «hello», укажите любое имя, например: {MyPersonTestAttribute}.
   * В поле hello задайте его свойства, выбрав тип, стиль, размер, шрифт и связанных свойств.
   * Атрибут hello Keep таким же значением по умолчанию как hello имя, заданное для этого атрибута (например, если имя атрибута MyPersonTestAttribute, оставьте значение по умолчанию hello с hello таким же именем).
   * Сохраните подчиненной hello с обновленными значениями и hello следующие:
     * В левой области hello выберите общего кода, а затем подчиненные формы
     * Выберите новый подчиненной hello и выберите узор - свойства разработки.
     * На вкладке hello третий слева hello и выберите **распространить этот запрет изменения структуры**.
7. Откройте подчиненной ExtensibleSchema ${ObjectName}, (где {ObjectName} — имя hello класса структурного объекта по умолчанию hello, например – лица).
8. Добавление ресурса выберите hello подчиненной (созданный, например – TestSubform) и сохраните подчиненной ExtensibleSchema hello ${ObjectName}.
9. Замените hello шаблона каталога Domino {PUBNAMES. НФПК} с новый настраиваемый шаблон hello {CONTOSO. НФПК}, следуя [эти действия](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
10. Закройте Domino администратора и откройте hello toorestart Domino консоли службы LDAP и tooReload hello схемы LDAP:
    * В консоли Domino, вставьте команду «hello» в **Domino команда** текст зарегистрирована служба LDAP hello toorestart - [перезапустить задачу LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
    * Команда tooreload схемы LDAP LDAP сообщить **сообщить LDAP ReloadSchema**.
11. Откройте администратор Domino и выберите вкладку toosee людей и групп добавлен атрибут отражается в domino добавить пользователя (под другим табуляции).
12. Откройте Schema.nsf на вкладке **Files** (Файлы) и убедитесь, что добавленный атрибут отражается в дополнительном классе объекта LDAP TestSubform.

**Способ 3: Добавление hello настраиваемого атрибута toohello ExtensibleObject класса**

1. Открытие файла {Schema.nsf}, помещенных в корневом каталоге hello
2. Выберите классы объектов LDAP из меню слева hello в **все документы схемы** и нажмите кнопку **Добавление объекта класса** кнопки:
3. Укажите имя LDAP в виде hello {zzzExtensibleSchema} (где zzz — имя hello класса структурного объекта по умолчанию hello, например лица). Например схема hello tooextend для объекта класса Person, укажите имя LDAP {PersonExtensibleSchema}.
4. Укажите имя класса главный объект, для которого требуется tooextend hello схемы. Например tooextend hello схемы для объекта класса Person, укажите имя класса объекта вышестоящий {dominoPerson}:
5. Укажите допустимый идентификатор Объекта соответствующей toohello класс объекта.
6. Выберите расширенные или пользовательских атрибутов в списке обязательный или необязательный атрибут типа поля в соответствии с требованием hello:
7. После добавления необходимых атрибутов toohello ExtensibleObjectClass, нажмите кнопку **сохранить и закрыть**.
8. Будет создан класс ExtensibleObjectClass с расширенными атрибутами для соответствующего класса объектов по умолчанию.

## <a name="troubleshooting"></a>Устранение неполадок
* Сведения о как ведение журнала tooenable tootroubleshoot hello соединителя разделе hello [как трассировка ETW для соединителей tooEnable](http://go.microsoft.com/fwlink/?LinkId=335731).
