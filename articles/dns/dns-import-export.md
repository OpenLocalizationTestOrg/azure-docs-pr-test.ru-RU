---
title: "aaaImport и доменной зоны экспорта файла tooAzure DNS с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooimport экспорта DNS зоны и файл tooAzure DNS с помощью Azure CLI 1.0"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Импорт и экспорт в файл зоны DNS, с помощью hello Azure CLI 1.0 

В этой статье рассматриваются как tooimport и экспорт файлов зоны DNS с помощью Azure DNS hello Azure CLI 1.0.

## <a name="introduction-toodns-zone-migration"></a>Введение tooDNS зоны миграции

Файл зоны DNS является файлом, содержащим сведения о каждой записи доменных имен (DNS) в зоне hello. Он соответствует стандартному формату и позволяет передавать записи DNS в системы DNS. С помощью файла зоны — это быстрый, надежный и удобный способ tootransfer зоны DNS в или из Azure DNS.

Azure DNS поддерживает импорт и экспорт файлов зоны с помощью hello Azure командной строки (CLI). Импорт файла зоны **не** в настоящее время поддерживается через Azure PowerShell или портал Azure hello.

Hello Azure CLI 1.0 является кросс платформенных средство командной строки для управления службами Azure. Он доступен для платформ Windows, Mac и Linux hello из hello [страницу загрузок Azure](https://azure.microsoft.com/downloads/). Кроссплатформенная поддержка важна для импорта и экспорта файлов зоны, поскольку hello наиболее распространенные программного обеспечения имя сервера [ПРИВЯЗКИ](https://www.isc.org/downloads/bind/), как правило, работает на платформе Linux.

> [!NOTE]
> В настоящее время существует две версии hello Azure CLI. Версия CLI1.0 основана на Node.js, и ее команды начинаются с "azure".
> Версия CLI2.0 основана на Python, и ее команды начинаются с "az". Хотя в обеих версиях поддерживается импорт файла зоны, рекомендуется использовать команды CLI1.0 hello, как описано на этой странице.

## <a name="obtain-your-existing-dns-zone-file"></a>Получение существующего файла зоны DNS

Прежде чем импортировать файл зоны DNS в Azure DNS, необходимо tooobtain копию файла зоны hello. Источник Hello этого файла зависит от того, где в настоящее время размещены hello зоны DNS.

* Если вашей зоны DNS размещена служба партнеров (например регистратора доменных имен, выделенных поставщика услуг размещения DNS или альтернативный облачного поставщика), службы должен предоставить файл зоны DNS hello toodownload hello возможности.
* Если ваш зоны DNS находится в системе DNS Windows, устанавливается в папку по умолчанию hello файлов зоны hello **%systemroot%\system32\dns**. файл зоны tooeach полный путь Hello также показывает hello **Общие** hello консоли DNS.
* Если ваш зоны DNS размещается с помощью ПРИВЯЗКИ, расположение hello hello файл зоны для каждой зоны указано в файле конфигурации ПРИВЯЗКИ hello **named.conf**.

> [!NOTE]
> Файлы зоны, скачанные с GoDaddy, слегка нестандартного формата. Требуется toocorrect прежде чем импортировать эти файлы зоны Azure DNS.
>
> DNS-имена в hello RDATA каждой записи DNS задаются в виде полных имен, но они не имеют завершающей «.» Это означает, что другие системы DNS интерпретируют их как относительные имена. Требуется tooedit hello зоны файл tooappend hello завершение». «tootheir имена, прежде чем импортировать их в Azure DNS.
>
> Например, запись CNAME «www 3600 в домене contoso.com CNAME» hello должны изменяться слишком «www 3600 CNAME в contoso.com».
> (с точкой в конце).

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Импорт файла зоны DNS в Azure DNS

Импорт файла зоны создает зону в Azure DNS, если таковая не существует. Если зона hello уже существует, hello наборов записей в файл зоны hello должны быть объединены с существующие наборы записей hello.

### <a name="merge-behavior"></a>Поведение объединения

* По умолчанию объединяются существующие и новые наборы записей. Одинаковые записи в рамках объединенного набора записей дедуплицируются.
* Кроме того, указав hello `--force` , то hello заменяет процесс импорта задает существующей записи с новые наборы записей. Существующие наборы записей, у которых нет соответствующей записи в файл импортированных зоны hello не удаляется.
* При слиянии наборов записей hello toolive (TTL) уже существующих наборов записей используется время. Когда `--force` — используется, hello TTL hello новый набор записей используется.
* Параметры зоны (SOA) начала (за исключением `host`) взяты из файла зоны импортированных hello, независимо от того, следует ли всегда `--force` используется. Аналогичным образом для записи сервера имен hello на вершине зоны hello, hello TTL всегда берется из файла импортированного зоны hello.
* Импортированные записи CNAME не заменяет существующие CNAME записи с точно такое же имя, если hello hello `--force` указан параметр.
* Когда возникает конфликт между запись CNAME и другую запись hello одинаковые имена, но разные введите (независимо от того, что существует или новые), hello существующую запись сохраняется. Это зависит от использования hello `--force`.

### <a name="additional-information-about-importing"></a>Дополнительная информация об импорте

Hello следующие примечания предоставляют дополнительные технические сведения о зоне hello процессе импорта.

* Hello `$TTL` директива является необязательным, и он поддерживается. Если аргумент `$TTL` дается директивы, импорт без явного TTL по умолчанию tooa TTL 3600 секунд. Если две записи в hello того же набора записей укажите разные TTLs, используется меньшее значение hello.
* Hello `$ORIGIN` директива является необязательным, и он поддерживается. Если аргумент `$ORIGIN` имеет значение по умолчанию hello hello имя зоны, как указано в командной строке hello является значение, используемое (плюс завершение hello «.»).
* Hello `$INCLUDE` и `$GENERATE` директивы не поддерживаются.
* Поддерживаются такие типы записей: A, AAAA, CNAME, MX, NS, SOA, SRV и TXT.
* Hello начальной записи автоматически создается системой Azure DNS при создании зоны. При импорте файла зоны, все параметры SOA, взяты из файла зоны hello *за исключением* hello `host` параметра. Этот параметр использует значение hello, предоставляемое Azure DNS. Это, поскольку этот параметр необходимо указывать toohello первичный сервер имен, предоставляемые Azure DNS.
* Hello запись сервера доменных имен на вершине зоны hello также создается автоматически системой Azure DNS при создании зоны hello. Только hello TTL этого набора записей импортируется. Эти записи содержат имена серверов имя hello, предоставляемые Azure DNS. данные записи Hello hello значения, содержащиеся в файле импортированных зоны hello не перезаписывается.
* Общедоступная предварительная версия Azure DNS поддерживает только записи типа TXT с одной строкой. Состоящее из нескольких строк записи TXT быть объединенное и усеченное too255 символов.

### <a name="cli-format-and-values"></a>Формат и значения CLI

Hello объекта hello Azure CLI команда tooimport зоны DNS выглядит следующим образом:

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Значения:

* `<resource group>`— Имя группы ресурсов hello hello hello зоны в Azure DNS.
* `<zone name>`— Имя зоны hello hello.
* `<zone file name>`— путь и имя hello зоны файл toobe импортированы hello.

Если зоны с таким именем не существует в группе ресурсов hello, он создается автоматически. Если hello зона уже существует, hello импортированной записи наборы объединяются с существующие наборы записей. toooverwrite hello существующие наборы записей, используйте hello `--force` параметр.

Формат hello tooverify файл зоны без импорта фактически, используйте hello `--parse-only` параметр.

### <a name="step-1-import-a-zone-file"></a>Шаг 1. Импорт файла зоны

файл зоны для зоны hello tooimport **contoso.com**.

1. Войдите в tooyour подписки Azure с помощью hello Azure CLI 1.0.

    ```azurecli
    azure login
    ```

2. Выберите подписку hello место toocreate вашей новой зоны DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS — это только для диспетчера ресурсов служба Azure, поэтому hello Azure CLI должны быть выключены tooResource режим диспетчера.

    ```azurecli
    azure config mode arm
    ```

4. Прежде чем использовать службу Azure DNS hello, необходимо зарегистрировать поставщика ресурсов Microsoft.Network из подписки toouse hello. (Эта операция выполняется один раз для каждой подписки).

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Если у еще его нет, необходимо также toocreate группу ресурсов диспетчера ресурсов.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. зоны hello tooimport **contoso.com** из файла hello **contoso.com.txt** в зоне DNS в группе ресурсов hello **myresourcegroup**, выполните команду hello `azure network dns zone import`.<BR>Эта команда загружает файл зоны hello и проанализировать его. Команда Hello выполняет ряд команд на hello Azure службы toocreate hello зоны DNS и задает все записи hello в зоне hello. Команда Hello сообщает о ходе выполнения в окне консоли hello, а также все ошибки и предупреждения. Из-за создания наборов записей в последовательности, может занять несколько минут tooimport большой файл.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>Шаг 2. Проверьте hello зоны

tooverify hello зоны DNS после импорта файла hello, можно использовать один из следующих методов hello:

* Список записей hello можно, используя следующую команду Azure CLI hello:

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* Список записей hello можно с помощью командлета PowerShell hello `Get-AzureRmDnsRecordSet`.
* Можно использовать `nslookup` tooverify разрешение имен для записей hello. Поскольку еще не делегировать зону hello, вам потребуется toospecify hello правильный Azure DNS-серверами, явным образом. Hello следующий пример иллюстрирует, как имена серверов имя hello tooretrieve назначает toohello зоны. ИТ также показано, как запись hello tooquery «www» с помощью `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>Шаг 3. Обновление делегирования DNS

После подтверждения что hello зоны импортированы правильно, необходимо tooupdate hello DNS делегирования toopoint toohello Azure серверами DNS. Дополнительные сведения см. в статье hello [обновить делегирование DNS hello](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Экспорт файла зоны DNS из Azure DNS

Hello объекта hello Azure CLI команда tooimport зоны DNS выглядит следующим образом:

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Значения:

* `<resource group>`— Имя группы ресурсов hello hello hello зоны в Azure DNS.
* `<zone name>`— Имя зоны hello hello.
* `<zone file name>`— путь и имя hello зоны файл toobe экспортировать hello.

Как с помощью импорта зоны hello, необходимо сначала toosign в, выберите подписку и настройте режим диспетчера ресурсов toouse hello Azure CLI.

### <a name="tooexport-a-zone-file"></a>tooexport файл зоны

1. Войдите в tooyour подписки Azure с помощью hello Azure CLI.

    ```azurecli
    azure login
    ```

2. Выберите подписку hello место toocreate вашей зоны DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. DNS Azure является исключительно службой диспетчера ресурсов Azure. Hello Azure CLI должен быть в режиме коммутируемые tooResource диспетчера.

    ```azurecli
    azure config mode arm
    ```

4. Существующая зона Azure DNS hello tooexport **contoso.com** в группе ресурсов **myresourcegroup** файл toohello **contoso.com.txt** (в текущей папке hello), запустите `azure network dns zone export`. Эта команда вызывает hello tooenumerate служба Azure DNS наборов записей в зоне hello и экспортировать hello результаты tooa совместимость ПРИВЯЗКИ зоны.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
