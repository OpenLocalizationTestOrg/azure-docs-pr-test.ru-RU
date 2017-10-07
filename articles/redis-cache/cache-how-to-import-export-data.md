---
title: "aaaImport и экспорт данных в кэше Redis для Azure | Документы Microsoft"
description: "Узнайте, как tooimport и экспорт данных tooand из хранилища больших двоичных объектов с экземплярами кэша Redis для Azure premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a>Импорт и экспорт данных в кэше Redis для Azure
Импорт и экспорт является операцией управления данных кэша Redis для Azure, позволяющий tooimport данных в кэше Redis для Azure или экспорта данных из кэша Redis для Azure, Импорт и экспорт моментального снимка Redis кэша базы данных (RDB) из большого двоичного объекта tooa premium кэша в Azure Учетная запись хранения. 

- **Экспорт** -можно экспортировать вашей tooa моментальные снимки RDB кэша Redis Azure страничного большого двоичного объекта.
- **Импорт**. Моментальные снимки в формате RDB можно импортировать в кэш Redis для Azure из страничного или блочного BLOB-объекта.

Импорт и экспорт позволяет toomigrate между различными экземплярами кэша Redis для Azure или заполнения кэша hello с данными, перед использованием.

В этой статье содержатся сведения для импорта и экспорта данных с помощью кэша Redis для Azure и предоставляет ответы на hello toocommonly вопросы и ответы.

> [!IMPORTANT]
> Функция импорта/экспорта находится на этапе предварительной версии и доступна только для кэшей [категории "Премиум"](cache-premium-tier-intro.md) .
>
>

## <a name="import"></a>Импорт
Импорт может быть используется toobring Redis совместимые RDB файлы с любого сервера Redis под управлением какой-либо облаке или в среде, включая Redis под управлением Linux, Windows или любого поставщика облачных служб, таких как Amazon Web Services и другие. Импорт данных — простой способ toocreate кэша заполнены данными. Во время процесса импорта hello кэша Redis для Azure hello RDB файлы загружаются из хранилища Azure в память и вставляет hello ключи в кэш hello.

> [!NOTE]
> Перед началом операции импорта hello, убедитесь, что файл базы данных Redis (RDB) или файлы загружаются в страницу или блочных BLOB-объектов в хранилище Azure, в hello же регионе и подписке, что экземпляр кэша Redis для Azure. Дополнительные сведения см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). При экспорте файла с помощью hello RDB [Azure Redis кэша Export](#export) функция, файл RDB уже хранится в страничный большой двоичный объект и готов к импорту.
>
>

1. tooimport один или несколько экспорта больших двоичных объектов кэша, [Обзор кэша tooyour](cache-configure.md#configure-redis-cache-settings) в hello портал Azure и нажмите кнопку **импорта данных** из hello **ресурсов меню**.

    ![Импорт данных][cache-import-data]
2. Нажмите кнопку **выберите копий** и выберите учетную запись хранения hello, содержащий данные tooimport hello.

    ![Выбор учетной записи хранения][cache-import-choose-storage-account]
3. Щелкните контейнер hello, содержащий данные tooimport hello.

    ![Выберите контейнер][cache-import-choose-container]
4. Выберите один или несколько tooimport большие двоичные объекты, нажав кнопку hello область toohello слева от имени большого двоичного объекта hello и нажмите кнопку **выберите**.

    ![Выберите BLOB-объекты][cache-import-choose-blobs]
5. Нажмите кнопку **импорта** процесс импорта toobegin hello.

   > [!IMPORTANT]
   > кэш Hello не доступны для клиентов кэша во время процесса импорта hello и удалить все существующие данные в кэше hello.
   >
   >

    ![Импорт][cache-import-blobs]

    Следующие уведомления hello из hello портал Azure, или просмотрев события hello в hello можно отслеживать ход выполнения операции импорта hello hello [журнал аудита](../azure-resource-manager/resource-group-audit.md).

    ![Ход выполнения импорта][cache-import-data-import-complete]

## <a name="export"></a>экспорт.
Экспорт позволяет tooexport hello данные, хранящиеся в кэш Azure Redis tooRedis совместимый RDB файлов. Можно использовать данные toomove этого компонента из одной tooanother экземпляр кэша Redis для Azure или tooanother сервера Redis. Во время процесса экспорта hello временный файл создается на hello виртуальной Машины, что узлы hello экземпляр сервера кэша Redis для Azure, а hello файл отправленного toohello, назначенные учетной записи хранилища. После завершения операции экспорта hello состояние успеха или сбоя hello временный файл удаляется.

1. tooexport hello текущее содержимое toostorage кэша hello, [Обзор кэша tooyour](cache-configure.md#configure-redis-cache-settings) в hello портал Azure и нажмите кнопку **экспортировать данные** из hello **ресурсов меню**.

    ![Выберите контейнер хранилища][cache-export-data-choose-storage-container]
2. Нажмите кнопку **выберите контейнер хранилища** и выберите учетную запись хранения требуемого hello. Учетная запись хранения Hello должна быть в hello одной подписке и регионе с кэшем.

   > [!IMPORTANT]
   > Функция экспорта работает со страничными BLOB-объектами, которые поддерживаются как классическими учетными записями хранения, так и учетными записями хранения Resource Manager, но пока не поддерживаются [учетными записями хранения BLOB-объектов](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).
   >
   >

    ![Учетная запись хранения][cache-export-data-choose-account]
3. Выберите требуемого hello контейнер больших двоичных объектов и нажмите кнопку **выберите**. Щелкните toouse новый контейнер **добавить контейнер** tooadd его первой, а затем выберите его из списка hello.

    ![Выберите контейнер хранилища][cache-export-data-container]
4. Введите значение **префикс имени большого двоичного объекта** и нажмите кнопку **Экспорт** toostart hello в процессе экспорта. префикс имени большого двоичного объекта Hello — используется tooprefix hello имена файлов, создаваемых этой операции экспорта.

    ![экспорт.][cache-export-data]

    Следующие уведомления hello из hello портал Azure, или просмотрев события hello в hello отследить ход выполнения hello операции экспорта hello [журнал аудита](../azure-resource-manager/resource-group-audit.md).

    ![Экспорт данных завершен][cache-export-data-export-complete]

    Кэши остаются доступными для использования в процессе экспорта hello.

## <a name="importexport-faq"></a>Часто задаваемые вопросы о функции импорта/экспорта
В этом разделе приведены часто задаваемые вопросы о функции импорта и экспорта hello.

* [В каких ценовых категориях можно функцию импорта/экспорта?](#what-pricing-tiers-can-use-importexport)
* [Можно ли импортировать данные с любого сервера Redis?](#can-i-import-data-from-any-redis-server)
* [Какие версии RDB-файлов можно импортировать?](#what-rdb-versions-can-i-import)
* [Доступен ли кэш во время операции импорта или экспорта?](#is-my-cache-available-during-an-importexport-operation)
* [Можно использовать функцию импорта/экспорта с кластером Redis?](#can-i-use-importexport-with-redis-cluster)
* [Как работает импорт и экспорт в базах данных с пользовательскими настройками?](#how-does-importexport-work-with-a-custom-databases-setting)
* [Чем отличается функция импорта/экспорта от сохраняемости Redis?](#how-is-importexport-different-from-redis-persistence)
* [Можно ли автоматизировать функцию импорта/экспорта с помощью PowerShell, интерфейса командной строки или других клиентов управления?](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [Возникла ошибка времени ожидания во время операции импорта или экспорта. Что это означает?](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [Я получил ошибку при экспорте tooAzure Мои данные хранилища больших двоичных объектов. Что произошло?](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>В каких ценовых категориях можно функцию импорта/экспорта?
Импорт и экспорт доступна только в ценовой категории premium hello.

### <a name="can-i-import-data-from-any-redis-server"></a>Можно ли импортировать данные с любого сервера Redis?
Да, кроме tooimporting данных, экспортированных из экземпляров кэша Redis для Azure, можно импортировать файлы RDB с любого сервера Redis под управлением какой-либо облака или среды, например поставщиков облачных служб, таких как Amazon Web Services, Windows или Linux. toodo это передачи hello RDB файла с сервера Redis требуемого hello в большой двоичный объект страницы или блок в учетной записи хранилища Azure, а затем импорт его в экземпляр кэша Redis для Azure premium. Например вы хотите tooexport hello данные из кэша рабочих и импортировать его в кэш, используемый как часть промежуточной среде для тестирования или миграции.

> [!IMPORTANT]
> toosuccessfully Импорт данных, экспортированных из Redis серверы, отличные от кэша Redis для Azure, когда с помощью страничного большого двоичного объекта, размер большого двоичного объекта страницы приветствия должна быть выровнена по границе 512 байт. Для образца кода tooperform требуемые байтов заполнения см. в разделе [пример страницы блога передачи](https://github.com/JimRoberts-MS/SamplePageBlobUpload).
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>Какие версии RDB-файлов можно импортировать?

Кэш Redis для Azure поддерживает импорт RDB-файлов вплоть до RDB версии 7.

### <a name="is-my-cache-available-during-an-importexport-operation"></a>Доступен ли кэш во время операции импорта или экспорта?
* **Экспорт** - кэши остаются доступными и продолжайте toouse кэша во время операции экспорта.
* **Импортировать** - кэши становятся недоступными после запуска операции импорта и станут доступны для использования после завершения операции импорта hello.

### <a name="can-i-use-importexport-with-redis-cluster"></a>Можно использовать функцию импорта/экспорта с кластером Redis?
Да, и вы можете выполнять импорт/экспорт между кластеризованным и некластеризованный кэшами. Так как кластер Redis [поддерживает только базу данных 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), данные в базах данных, отличных от 0, не импортируются. При импорте данных кластеризованный кэша, ключи hello перераспределяются между сегментами hello hello кластера.

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>Как работает импорт и экспорт в базах данных с пользовательскими настройками?
Некоторые ценовые категории имеют различные [баз данных ограничения](cache-configure.md#databases), поэтому существуют определенные рекомендации при импорте, если вы настроили пользовательское значение hello `databases` можно задать во время создания кэша.

* При импорте tooa ценовой категории с более низким `databases` предел от уровня hello, из которого был экспортирован:
  * Если вы используете hello количество по умолчанию `databases`, которая 16 для всех ценовых категорий, данные не теряются.
  * Если вы используете настраиваемое число `databases` , попадает в пределы hello для hello уровня toowhich при импорте, никакие данные не потеряны.
  * Если экспортированных данных содержит данные в базе данных, размер которой превышает ограничения hello hello новый уровень, hello данные из указанных выше баз данных не импортируются.

### <a name="how-is-importexport-different-from-redis-persistence"></a>Чем отличается функция импорта/экспорта от сохраняемости Redis?
Azure сохраняемости кэша Redis позволяет toopersist данные, хранящиеся в Redis tooAzure хранилища. При настройке сохраняемости кэша Redis для Azure сохраняет моментальный снимок кэша Redis hello в Redis toodisk двоичный формат, в зависимости от можно настроить интервал резервного копирования. В случае критического события, отключает hello первичный и реплика кэша hello кэширования данных восстанавливается автоматически с помощью hello самый последний моментальный снимок. Дополнительные сведения см. в разделе [как tooconfigure сохранения данных для кэша Redis Azure Premium](cache-how-to-premium-persistence.md).

Импорт / Экспорт позволяет toobring данных или экспорта из кэша Redis для Azure. Она не осуществляет настройку резервного копирования использует для восстановления механизм сохраняемости Redis.

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>Можно ли автоматизировать функцию импорта/экспорта с помощью PowerShell, интерфейса командной строки или других клиентов управления?
Да, PowerShell инструкции в разделе [tooimport кэш Redis](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) и [tooexport кэш Redis](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>Во время операции импорта/экспорта возникла ошибка времени ожидания. Что это означает?
Если остались на hello **импорта данных** или **Экспорт данных** колонке более 15 минут перед запуском операции hello появляется сообщение об ошибке с ошибки сообщения аналогичные toohello следующий пример:

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve по этой операции экспорта или импорта hello инициировать до истечения 15 минут.

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>Я получил ошибку при экспорте tooAzure Мои данные хранилища больших двоичных объектов. Что произошло?
Функция экспорта работает только с RDB-файлами, сохраненными в виде страничных BLOB-объектов. Другие типы больших двоичных объектов пока не поддерживаются, включая учетные записи хранилища BLOB-объектов с "горячим" и "холодным" уровнями. Дополнительные сведения см. в разделе [Учетные записи хранения BLOB-объектов](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).

## <a name="next-steps"></a>Дальнейшие действия
Узнайте, как toouse более "премиум" кэша функции.

* [Уровень Premium кэша Redis Azure toohello введение](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
