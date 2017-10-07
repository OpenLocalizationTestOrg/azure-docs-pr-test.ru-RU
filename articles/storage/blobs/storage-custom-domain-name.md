---
title: "aaaConfigure пользовательское доменное имя для конечной точки хранения больших двоичных объектов Azure | Документы Microsoft"
description: "Используйте собственную конечную точку каноническое имя (CNAME) toohello BLOB-объекта хранилища hello Azure портала toomap в учетной записи хранилища Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: bfee6d28039f389ba2e2ed6b28d43894b6e15469
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Настройка пользовательского доменного имени для конечной точки хранилища BLOB-объектов

Можно настроить пользовательский домен для доступа к BLOB-данным в учетной записи хранения Azure. Здравствуйте конечную точку по умолчанию для хранилища BLOB-объектов — `<storage-account-name>.blob.core.windows.net`. Если сопоставить домен и поддомен, например **www.contoso.com** toohello конечной точки большого двоичного объекта для вашей учетной записи хранилища, пользователям можно получить доступ к BLOB-объектов данных в вашей учетной записи хранилища с помощью этого домена.

> [!IMPORTANT]
> Служба хранилища Azure пока не поддерживает протокол HTTPS для личных доменов. Вы можете в настоящее время [использовать большие двоичные объекты tooaccess hello Azure CDN с применением пользовательских доменов по протоколу HTTPS](storage-https-custom-domain-cdn.md).
>

Hello следующей таблице показано несколько образец URL-адреса для данных blob в учетной записи хранилища с именем **mystorageaccount**. Пользовательский домен Hello зарегистрирован для учетной записи хранилища hello **www.contoso.com**:

| Тип ресурса | URL-адрес по умолчанию | URL-адрес личного домена |
| --- | --- | --- |
| Учетная запись хранения | http://mystorageaccount.blob.core.windows.net | http://www.contoso.com |
| BLOB-объект |http://mystorageaccount.blob.core.windows.net/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| Корневой контейнер | http://mystorageaccount.blob.core.windows.net/myblob или http://mystorageaccount.blob.core.windows.net/$root/myblob| http://www.contoso.com/myblob или http://www.contoso.com/$root/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>Прямое и промежуточное сопоставление доменов

Существует два способа toopoint конечной точки большого двоичного объекта toohello пользовательский домен для учетной записи: прямое CNAME сопоставление и с помощью hello *asverify* промежуточного поддомена.

### <a name="direct-cname-mapping"></a>Прямое сопоставление CNAME

метод Hello первый и самый простой, является toocreate запись каноническое имя (CNAME), которая сопоставляет домен и поддомен напрямую toohello конечной точки большого двоичного объекта. Запись CNAME является функцией системы (DNS) имя домена, которая сопоставляет исходный домен tooa целевой домен. В этом случае hello исходный домен является собственный домен и поддомен, например *www.contoso.com*. hello целевым доменом является конечной точки службы BLOB-объектов, например  *mystorageaccount.BLOB.Core.Windows.NET*.

прямой метод Hello охваченных [регистрация пользовательского домена](#register-a-custom-domain).

### <a name="intermediary-mapping-with-asverify"></a>Промежуточное сопоставление с помощью *asverify*

Второй метод Hello также использует записи CNAME, но сначала применяет специальные поддомен, распознаваемые простоя Azure tooavoid: **asverify**.

при его регистрации в hello Hello процесса сопоставления конечной точки большого двоичного объекта tooa пользовательского домена может привести к короткий период времени простоя для домена hello [портал Azure](https://portal.azure.com). Если личный домен в настоящее время поддерживает приложения с соглашения об уровне обслуживания (SLA), требующий нулевое время простоя, то можно использовать hello Azure *asverify* поддомен во время регистрации промежуточного шага. Этот промежуточный шаг гарантирует пользователи являются может tooaccess домена, а выполняется сопоставление hello DNS.

метод промежуточных Hello рассматривается в [регистрация пользовательского домена с помощью hello *asverify* поддомен](#register-a-custom-domain-using-the-asverify-subdomain).

## <a name="register-a-custom-domain"></a>Регистрация личного домена
Используйте tooregister этой процедуры вашего домена при наличии никаких проблем, о домене hello tooyour кратко недоступны пользователям, или в том случае, если пользовательский домен в настоящее время не размещено приложение.

Если пользовательский домен в настоящее время поддерживает приложение, которое не может иметь время простоя, следуйте процедуре hello, описанные в [регистрация пользовательского домена с помощью hello *asverify* поддомен](#register-a-custom-domain-using-the-asverify-subdomain).

tooconfigure пользовательского имени домена, необходимо создать новую запись CNAME в DNS. запись CNAME Hello определяет псевдоним для имени домена. В этом случае он преобразуется hello адрес конечной хранилища больших двоичных объектов toohello пользовательский домен для учетной записи.

Как правило, можно управлять параметрами DNS домена на веб-сайте регистратора домена. Каждый регистратор имеет похожие, но немного другой метод указания запись CNAME, но концепции hello Здравствуйте, таким же. Некоторые пакеты регистрации основного домена не предлагают конфигурации DNS, поэтому может потребоваться tooupgrade пакет регистрации домена перед созданием hello запись CNAME.

1. Перейдите tooyour учетной записи хранилища в hello [портал Azure](https://portal.azure.com).
1. В разделе **службы BLOB-ОБЪЕКТОВ** колонке hello меню, выберите **пользовательский домен** tooopen hello *пользовательский домен* колонку.
1. Войдите на веб-сайте регистратора домена tooyour и переход на страницу toohello управления DNS. Это может быть такой раздел, как **Доменное имя**, **DNS** или **Управление сервером доменных имен**.
1. Найдите раздел hello управления записями CNAME. Могут содержать дополнительные параметры страницы toogo tooan и искать слова hello **CNAME**, **псевдоним**, или **поддомены**.
1. Создайте запись CNAME и укажите псевдоним поддомена, например **www** или **photos**. Введите имя узла, который является конечной точки службы BLOB-объектов, в формате hello **mystorageaccount.blob.core.windows.net** (где *mystorageaccount* hello имя учетной записи). Имя toouse Hello узла отображается в элемент #1 hello *пользовательский домен* колонки в hello [портал Azure](https://portal.azure.com).
1. В поле текст hello в hello *пользовательский домен* колонки в hello [портал Azure](https://portal.azure.com), введите имя личного домена, включая поддомен hello hello. Например, если домен — **contoso.com** и ваш псевдоним поддомена — **www**, введите **www.contoso.com**. Если используется поддомен **фотографии**, введите **photos.contoso.com**. используется поддомен hello *необходимые*.
1. Выберите **Сохранить** на hello *пользовательский домен* tooregister колонки вашего домена. Если регистрация hello проходит успешно, вы увидите портала уведомление, что ваша учетная запись хранения успешно обновлен.

После новую запись CNAME распространяется через DNS, пользователям можно просмотреть данные больших двоичных объектов с помощью личного домена, при условии, что они имеют соответствующие разрешения hello.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Регистрация пользовательского домена с помощью hello *asverify* дочернего домена
Использование этой процедуры tooregister вашего домена при личного домена в настоящее время поддерживает приложения с соглашения об уровне ОБСЛУЖИВАНИЯ, который требуется существовать без простоев. Создав запись CNAME, которая указывает с `asverify.<subdomain>.<customdomain>` слишком`asverify.<storageaccount>.blob.core.windows.net`, можно предварительно зарегистрировать своего домена с Azure. Затем можно создать второй CNAME, которая указывает с `<subdomain>.<customdomain>` слишком`<storageaccount>.blob.core.windows.net`, тогда трафика tooyour пользовательского домена будет конечной точки расширенного tooyour больших двоичных объектов.

Hello **asverify** поддомен представляет собой специальный поддомен, распознаваемые Azure. Добавляя `asverify` tooyour собственный дочерний домен, чтобы разрешить Azure toorecognize вашего домена без изменения hello запись DNS для домена hello. При изменении hello запись DNS для домена hello, он будет иметь конечную точку большого двоичного объекта сопоставленных toohello без простоев.

1. Перейдите tooyour учетной записи хранилища в hello [портал Azure](https://portal.azure.com).
1. В разделе **службы BLOB-ОБЪЕКТОВ** колонке hello меню, выберите **пользовательский домен** tooopen hello *пользовательский домен* колонку.
1. Войдите на веб-сайте поставщика DNS tooyour и переход на страницу toohello управления DNS. Это может быть такой раздел, как **Доменное имя**, **DNS** или **Управление сервером доменных имен**.
1. Найдите раздел hello управления записями CNAME. Могут содержать дополнительные параметры страницы toogo tooan и искать слова hello **CNAME**, **псевдоним**, или **поддомены**.
1. Создайте новую запись CNAME и укажите псевдоним поддомена, который включает в себя hello *asverify* дочерний домен. Например, **asverify.www** или **asverify.photos**. Введите имя узла, который является конечной точки службы BLOB-объектов, в формате hello **asverify.mystorageaccount.blob.core.windows.net** (где **mystorageaccount** hello имя учетной записи). Имя toouse Hello узла отображается в элемент #2 hello *пользовательский домен* колонки в hello [портал Azure](https://portal.azure.com).
1. В поле текст hello в hello *пользовательский домен* колонки в hello [портал Azure](https://portal.azure.com), введите имя личного домена, включая поддомен hello hello. Не включайте *asverify*. Например, если домен — **contoso.com** и ваш псевдоним поддомена — **www**, введите **www.contoso.com**. Если используется поддомен **фотографии**, введите **photos.contoso.com**. поддомен hello не требуется.
1. Выберите hello **использовать непрямую проверку CNAME** флажок.
1. Выберите **Сохранить** на hello *пользовательский домен* tooregister колонки вашего домена. Если регистрация hello проходит успешно, вы увидите портала уведомление о том, что ваша учетная запись хранения успешно обновлен. На этом этапе пользовательский домен проверен Azure, но домен tooyour трафика еще не направляется tooyour учетной записи хранилища.
1. Вернитесь веб-сайте поставщика DNS tooyour и создайте другую запись CNAME, сопоставляющий конечной точки службы BLOB-объектов tooyour дочерний домен. Например, укажите поддомен hello в виде **www** или **фотографии** (без hello *asverify*), и имя узла как hello  **mystorageaccount.BLOB.Core.Windows.NET** (где **mystorageaccount** hello имя учетной записи). С помощью этого этапа регистрации hello своего пользовательского домена будет завершена.
1. Наконец, можно удалить запись CNAME hello, вы создали содержащего hello **asverify** дочерний домен, как она была нужна только в качестве промежуточного шага.

После новую запись CNAME распространяется через DNS, пользователям можно просмотреть данные больших двоичных объектов с помощью личного домена, при условии, что они имеют соответствующие разрешения hello.

## <a name="test-your-custom-domain"></a>Проверка личного домена

tooconfirm личного домена находится на самом деле сопоставлен tooyour конечной точки службы BLOB-объектов, создания большого двоичного объекта в открытый контейнер в вашей учетной записи хранилища. Затем в веб-браузере введите URI в hello следующая формата tooaccess hello blob:

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

Например, можно использовать следующие tooaccess URI веб-формы в hello hello **myforms** контейнера в hello **photos.contoso.com** пользовательский дочерний домен:

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>Отмена регистрации личного домена

tooderegister пользовательского домена для конечной точки хранения больших двоичных объектов, используйте одну из следующих процедур hello.

### <a name="azure-portal"></a>Портал Azure

Выполните следующие hello в hello Azure портала tooremove приветствия пользовательского домена.

1. Перейдите tooyour учетной записи хранилища в hello [портал Azure](https://portal.azure.com).
1. В разделе **службы BLOB-ОБЪЕКТОВ** колонке hello меню, выберите **пользовательский домен** tooopen hello *пользовательский домен* колонку.
1. Очистить hello содержимое hello текстовое поле, содержащее пользовательское имя домена.
1. Выберите hello **Сохранить** кнопки.

Hello пользовательский домен успешно удален, появится портала уведомление о том, что ваша учетная запись хранения успешно обновлен.

### <a name="azure-cli-20"></a>Azure CLI 2.0

Используйте hello [обновление учетной записи хранилища az](https://docs.microsoft.com/cli/azure/storage/account#update) CLI команду и укажите пустую строку (`""`) для hello `--custom-domain` tooremove значение аргумента регистрации пользовательского домена.

* Формат команды:

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* Пример команды:

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

Используйте hello [набор AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) командлета PowerShell и укажите пустую строку (`""`) для hello `-CustomDomainName` tooremove значение аргумента регистрации пользовательского домена.

* Формат команды:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* Пример команды:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>Дальнейшие действия
* [Сопоставить конечную точку Azure доставки содержимого сети (CDN) tooan пользовательского домена](../../cdn/cdn-map-content-to-custom-domain.md)
* [Использование больших двоичных объектов tooaccess Azure CDN hello с пользовательскими доменами по протоколу HTTPS](storage-https-custom-domain-cdn.md)
