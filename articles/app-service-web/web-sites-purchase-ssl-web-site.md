---
title: "aaaAdd SSL-сертификатов tooyour приложение службы приложений Azure | Документы Microsoft"
description: "Узнайте, как tooadd SSL-сертификат tooyour приложением служб приложений."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Приобретение и настройка сертификата SSL для службы приложений Azure

В этом руководстве вы защитите свое веб-приложение, приобретя SSL-сертификат для **[службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714)**, безопасно сохранив его в [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) и сопоставив с личным доменом.

## <a name="step-1---log-in-tooazure"></a>Шаг 1. вход tooAzure

Войдите в toohello портал Azure по адресу http://portal.azure.com

## <a name="step-2---place-an-ssl-certificate-order"></a>Шаг 2. Размещение заказа на SSL-сертификат

Можно разместить заказ SSL-сертификат, создав новую [сертификат службы приложения](https://portal.azure.com/#create/Microsoft.SSL) в hello **портал Azure**.

![Создание сертификата](./media/app-service-web-purchase-ssl-web-site/createssl.png)

Введите понятное **имя** для протокола SSL сертификатов и введите hello **имя домена**

> [!NOTE]
> Это одна из наиболее важных частей hello hello процесса покупки. Убедитесь, что tooenter Исправьте имя узла (пользовательский домен), которые должны tooprotect с помощью этого сертификата. **Нет** Добавление hello имени узла с веб-публикации. 
>

Выберите **подписку**, **группу ресурсов** и **SKU сертификата**.

> [!WARNING]
> Сертификаты службы приложений может использоваться только в другие службы приложения hello одной подписке.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>Шаг 3 — хранить hello сертификат в хранилище ключей Azure

> [!NOTE]
> [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) — это служба Azure, которая помогает защитить криптографические ключи и секреты, используемые облачными приложениями и службами.
>

После завершения hello покупки SSL-сертификат необходимо tooopen [сертификатов службы приложений](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) колонки ресурсов.

![Вставьте изображение готово toostore в кв](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

Вы заметите, что состояние сертификата — **«Ожидающие выдачи»** имеется несколько дополнительных действий необходимо toocomplete перед началом использования этого сертификата.

Нажмите кнопку **конфигурация сертификата** в колонке свойства сертификата и нажмите кнопку **шаг 1: хранилище** toostore этот сертификат в хранилище ключей Azure.

Из **состояния хранилища ключей** колонке нажмите кнопку **репозитория хранилища ключей** toochoose существующего хранилища ключей toostore этот сертификат **или создать новое хранилище ключей** toocreate новый ключ в хранилище внутри же подписке и группе ресурсов.

> [!NOTE]
> Расходы на хранение этого сертификата в Azure Key Vault будут минимальными.
> Дополнительные сведения см. в разделе с **[ценами на Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.
>

После выбора toostore hello репозитория хранилища ключ этого сертификата в, hello **хранилища** параметр должен показывать ход.

![Вставить изображение с успешным сохранением в Key Vault](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>Шаг 4. Проверка hello владельца домена

> [!NOTE]
> Сертификаты службы приложений поддерживают три типа проверки домена: проверка через домен, по почте и вручную. Эти механизмы описаны более подробно hello [расширенный раздел](#advanced).

Из hello же **настройку сертификата** колонки, который использовался в шаге 3, нажмите кнопку **шаг 2: проверка**.

**Проверка домена** это наиболее удобный процесс hello **, только если** у вас есть  **[приобретенному личного домена службы приложений Azure.](custom-dns-web-site-buydomains-web-app.md)**
Щелкните **проверьте** кнопку toocomplete этот шаг.

![Вставить изображение с проверкой через домен](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

После нажатия кнопки **проверьте**, использовать hello **обновление** кнопки до hello **проверьте** параметр должен показывать ход.

![Вставить изображение с успешной проверкой в Key Vault](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>Шаг 5 – назначить tooApp сертификата службы приложений

> [!NOTE]
> Перед выполнением действия hello в этом разделе, нужно, чтобы связанные пользовательское доменное имя вместе с приложением. Дополнительные сведения см. в разделе **[Сопоставление имени личного домена с приложением Azure](app-service-web-tutorial-custom-domain.md)**.
>

В hello  **[портал Azure](https://portal.azure.com/)**, нажмите кнопку hello **службы приложений** параметр hello левой части страницы приветствия.

Щелкните имя hello toowhich вашего приложения требуется tooassign этот сертификат.

В hello **параметры**, нажмите кнопку **SSL-сертификаты**.

Нажмите кнопку **импорта сертификата службы приложения** и hello выберите сертификат, который вы приобрели.

![вставить изображение для импорта сертификата](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

В hello **привязки ssl** статьи щелкните на **добавления привязок**и используется имя hello раскрывающихся списках tooselect hello домена toosecure с протоколом SSL, а hello toouse сертификат. Можно также выбрать, будет ли toouse  **[Указание имени сервера (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  или SSL на основе IP.

![вставить изображение для привязок SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

Нажмите кнопку **Добавление привязки** toosave hello изменения и включить SSL.

> [!NOTE]
> Если вы выбрали **SSL на основе IP** и личный домен настраивается с помощью записи, необходимо выполнить следующие дополнительные шаги hello. Эти механизмы описаны более подробно hello [расширенный раздел](#Advanced).

На этом этапе вы должен быть доступ toovisit приложения с использованием `HTTPS://` вместо `HTTP://` tooverify, hello сертификат был настроен правильно.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>Шаг 6. Задачи управления

### <a name="azure-cli"></a>Инфраструктура CLI Azure

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>Расширенная

### <a name="verifying-domain-ownership"></a>Проверка принадлежности домена

Сертификаты службы приложений поддерживают еще два типа проверки домена: проверка по почте и вручную.

#### <a name="mail-verification"></a>Проверка по почте

Уже было отправлено письмо с подтверждением toohello адреса электронной почты, связанной с этим доменом пользовательских.
этап проверки электронной почты toocomplete hello, открыть сообщение hello и щелкните ссылку проверки hello.

![Вставить изображение с проверкой по почте](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

При необходимости проверочное сообщение hello tooresend щелкните hello **отправить повторно** кнопки.

#### <a name="manual-verification"></a>Проверка вручную

> [!IMPORTANT]
> Проверка веб-страницы HTML (работает только с номером SKU сертификата уровня "Стандартный").
>

1. Создайте HTML-файл **starfield.html**.

1. Содержимое этого файла должно быть hello точное имя hello токена проверки домена. (Вы можете скопировать hello маркер из hello колонке состояния проверки домена)

1. Отправить файл в корне hello hello веб-сервере с доменом`/.well-known/pki-validation/starfield.html`

1. Нажмите кнопку **обновление** tooupdate состояние сертификата hello после завершения проверки. Он может занять несколько минут для проверки toocomplete.

> [!TIP]
> Убедитесь в терминалов с использованием `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello ответ должен содержать hello `<verification-token>`.

#### <a name="dns-txt-record-verification"></a>Проверка записей типа TXT DNS

1. В диспетчере DNS, создайте запись TXT на hello `@` дочерний домен с toohello равно значение токена проверки домена.
1. Нажмите кнопку **«Обновить»** tooupdate hello состояние сертификата после завершения проверки.

> [!TIP]
> Требуется toocreate TXT-запись на `@.<domain>` со значением `<verification-token>`.

### <a name="assign-certificate-tooapp-service-app"></a>Назначьте tooApp сертификата службы приложений

Если вы выбрали **SSL на основе IP** и личный домен настраивается с помощью записи, необходимо выполнить следующие дополнительные шаги hello:

После настройки SSL-привязку на основе IP, выделенный IP-адрес назначается tooyour приложения. Этот IP-адрес можно найти на hello **пользовательский домен** в разделе параметров приложения, сразу над hello **имена узлов** раздела. Он указывается как **Внешний IP-адрес**

![вставить изображение для SSL на основе IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

Обратите внимание, что этот IP-адрес отличается от hello виртуальный IP-адрес используется ранее tooconfigure hello A-запись для домена. Если для пользователя настроен toouse SNI SSL на основе или не настроена toouse SSL, не будет приведено адреса для данной записи.

С помощью инструментов hello регистратора доменных имен, измените запись для вашего личного домена имя toopoint toohello IP-адрес из предыдущего шага hello hello.

## <a name="rekey-and-sync-hello-certificate"></a>Повторное создание ключа и синхронизировать hello сертификата

Если в дальнейшем tooRekey свой сертификат, выберите **повторное создание ключа и синхронизировать** меню **свойства сертификата** колонку.

Нажмите кнопку **повторное создание ключа** кнопку tooinitiate hello процесса. Этот процесс может занять toocomplete 1 – 10 минут.

![вставить изображение для повторного создания ключа SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

Смена ключей сертификата откатывается hello сертификата на новый сертификат, выданный центром сертификации hello.

## <a name="next-steps"></a>Дальнейшие действия

* [Добавление сети доставки содержимого](app-service-web-tutorial-content-delivery-network.md)