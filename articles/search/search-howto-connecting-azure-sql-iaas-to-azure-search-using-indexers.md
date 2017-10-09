---
title: "tooAzure подключение виртуальной Машины aaaSQL поиска | Документы Microsoft"
description: "Включение шифрования соединений и настройте hello брандмауэра tooallow подключений tooSQL сервера на из индексатор поиска Azure в Azure виртуальные машины (VM)."
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Настройте подключение между tooSQL индексатор поиска Azure Server на Виртуальной машине Azure
Как отмечалось в [tooAzure подключении базы данных SQL Azure поиск с помощью индексаторов](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), создание индексаторов для **SQL Server на виртуальных машинах Azure** (или **виртуальных машин SQL Azure** сокращенно) — поддерживаемые службы поиска Azure, но есть несколько необходимых компонентов, связанных с безопасностью tootake заботиться о первом. 

**Длительность:** сертификат около 30 минут, при условии, что вы уже установлен на hello виртуальной Машины.

## <a name="enable-encrypted-connections"></a>Активация зашифрованных подключений
Для службы поиска Azure требуется зашифрованный канал для всех запросов индексатора, выполняемых через общедоступное Интернет-подключение. В этом разделе перечислены шаги toomake hello эту работу.

1. Проверьте свойства hello имени субъекта hello tooverify сертификат hello hello полное доменное имя (FQDN) hello виртуальной Машине Azure. Можно использовать средства, подобного CertUtils или hello свойства hello tooview оснастки сертификатов. Hello полное доменное имя можно получить из колонки для hello виртуальной Машины службы Essentials раздела, hello **адрес общедоступный IP-адрес или DNS-имя метки** в hello [портал Azure](https://portal.azure.com/).
   
   * Для виртуальных машин, созданных с помощью более новой hello **диспетчера ресурсов** шаблона, полное доменное имя hello форматируется как `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Для более старых виртуальные машины, созданные как **классический** ВМ hello представляется в формате полного доменного ИМЕНИ `<your-cloud-service-name.cloudapp.net>`. 
2. Настройте сертификат hello toouse SQL Server, с помощью редактора реестра (regedit) hello. 
   
    Несмотря на то, что диспетчер конфигурации SQL Server часто используется для данной задачи, его нельзя использовать в этом сценарии. Он не найдете hello импортированный сертификат, так как полное доменное имя виртуальной Машины в Azure hello hello не соответствует hello полное доменное имя, по расчету hello (он определяет домен hello как hello локального компьютера или toowhich hello сетевого домена, которому он присоединен) виртуальной Машины. Если имена не совпадают, используйте сертификат hello toospecify regedit.
   
   * В редакторе реестра перейдите в раздел реестра toothis: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Hello `[MSSQL13.MSSQLSERVER]` часть варьируется в зависимости от версии и имя экземпляра. 
   * Задайте значение hello hello **сертификат** ключа toohello **отпечаток** hello SSL-сертификата, импортированные toohello виртуальной Машины.
     
     Существует несколько способов tooget hello отпечатка пальца, некоторые лучше, чем другие. При копировании из hello **сертификаты** оснастки MMC, вы, вероятно, получат невидимой начинайте [как описано в этой статье поддержка](https://support.microsoft.com/kb/2023869/), который приводит к ошибке при попытке соединение. Для этой проблемы существует несколько обходных решений. простой Hello превышает toobackspace, а затем повторите ввод первого символа hello hello отпечаток tooremove hello первый символ в поле значение ключа hello в regedit. Кроме того можно использовать отпечаток hello toocopy другой инструмент.
3. Предоставьте разрешения учетной записи службы toohello. 
   
    Убедитесь, что предоставлено соответствующее разрешение на hello закрытый ключ сертификата SSL hello hello учетной записи службы SQL Server. Если пренебречь этим шагом, то SQL Server не запустится. Можно использовать hello **сертификаты** оснастки или **CertUtils** для выполнения этой задачи.
4. Перезапустите службу SQL Server hello.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>Настройка подключения к SQL Server в hello виртуальной Машины
После настройки hello зашифрованные соединения, необходимые для поиска Azure, существует встроенная функция tooSQL действия дополнительная настройка сервера на виртуальных машинах Azure. Если вы еще не сделали этого, hello следующим шагом является toofinish конфигурации, с помощью либо один из следующих статей:

* Для **диспетчера ресурсов** виртуальной Машины, в разделе [подключения tooa виртуальной машины SQL Server в Azure с помощью диспетчера ресурсов](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* Для **классический** виртуальной Машины, в разделе [подключения виртуальной машины SQL Server в Azure Classic tooa](../virtual-machines/windows/classic/sql-connect.md).

В частности, просмотрите раздел hello в каждой статье «подключение через hello Интернета».

## <a name="configure-hello-network-security-group-nsg"></a>Настройка hello группы безопасности сети (NSG)
Не является необычным tooconfigure hello NSG и соответствующая конечная точка Azure или список управления доступом (ACL) toomake сторон доступного tooother вашей виртуальной Машине Azure. Скорее всего, вы сделали это перед tooallow собственные tooyour tooconnect логику приложения виртуальной Машины SQL Azure. Оно ничем не отличается для поиска Azure подключения tooyour виртуальной Машины SQL Azure. 

Приведенные ниже ссылки Hello предоставляют инструкции NSG конфигурации для развертывания виртуальной Машины. Используйте эти инструкции tooACL конечной точки службы поиска Azure на основе IP-адреса.

> [!NOTE]
> Основные сведения см. в статье [Группа безопасности сети](../virtual-network/virtual-networks-nsg.md).
> 
> 

* Для **диспетчера ресурсов** виртуальной Машины, в разделе [как toocreate Nsg для развертываний ARM](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* Для **классический** виртуальной Машины, в разделе [как toocreate Nsg для развертываний классический](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

IP-адресация может представлять несколько задач, которые обходятся легко в том случае, если вам известно о hello проблема и возможные решения. остальные разделы Hello содержатся рекомендации по обработке адреса связанных tooIP проблемы в hello ACL.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Ограничения IP-адрес службы поиска доступ toohello
Настоятельно рекомендуется ограничить hello доступа toohello IP-адрес службы поиска в hello ACL, вместо внесения в открытую tooany запросы на подключение виртуальных машин SQL Azure. Вы можете легко найти hello IP адрес, с помощью проверки связи hello полное доменное имя (например, `<your-search-service-name>.search.windows.net`) службы поиска.

#### <a name="managing-ip-address-fluctuations"></a>Управление колебаниями IP-адреса
Если служба поиска имеет только одна единица поиска (то есть одной реплики и одной секции), hello IP-адрес изменится во время перезапуска службы сопоставление делает недействительными существующие ACL с IP-адрес службы поиска.

Одним из способов tooavoid hello последующие подключения ошибка является toouse более чем одной реплики и одной секции в поиске Azure. Это повышает hello затрат, но также позволяет решить проблему адресным hello. В службе поиска Azure IP-адреса не меняются при наличии более чем одной единицы поиска.

Второй подход — toofail подключения tooallow hello, а затем перенастроить hello списки управления доступом в hello NSG. В среднем toochange IP адреса можно ожидать каждые несколько недель. Для пользователей, которые нечасто выполняют управляемую индексацию, этот подход может быть эффективным.

Третий способ реальную (но не безопасным) является toospecify hello диапазон IP-адресов hello регион Azure, где предоставляется службой поиска. Список диапазонов IP-адресов, из которых tooAzure ресурсы выделяются общих IP-адресов Hello опубликованы по адресу [диапазоны IP-центра обработки данных Azure](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Включить hello поиска Azure портала IP-адресов
При использовании hello Azure портала toocreate индексатор портала логику поиска Azure также должна tooyour доступа к виртуальной Машине SQL Azure во время создания. Чтобы найти IP-адреса портала службы поиска Azure, можно выполнить проверку связи с `stamp2.search.ext.azure.com`.

## <a name="next-steps"></a>Дальнейшие действия
С конфигурацией из hello способом можно теперь указать SQL Server на виртуальной Машине Azure как источник данных hello для индексатор поиска Azure. В разделе [tooAzure подключении базы данных SQL Azure поиск с помощью индексаторов](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) для получения дополнительной информации.

