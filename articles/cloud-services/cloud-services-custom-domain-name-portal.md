---
title: "пользовательское доменное имя в облачных службах aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooexpose вашей Azure toohello данным или приложению Интернета на пользовательский домен, настроив параметры DNS.  В этих примерах используются hello портал Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Настройка пользовательского доменного имени для облачной службы Azure
> [!div class="op_single_selector"]
> * [Портал Azure](cloud-services-custom-domain-name-portal.md)
> * [классическом портале Azure](cloud-services-custom-domain-name.md)
> 
> 

При создании облачной службы Azure назначает его поддомен tooa **cloudapp.net**. Например, если облачная служба имеет имя «contoso», пользователи будут быть может tooaccess приложения на URL-адрес: http://contoso.cloudapp.net. Azure также назначает виртуальный IP-адрес.

Однако приложение можно сделать доступным и на своем собственном домене, например **contoso.com**. В этой статье объясняется, как tooreserve или настроить пользовательское доменное имя для веб-ролей облачной службы.

Вы уже знаете, что такое записи CNAME и A? [Переход за объяснение hello](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Hello процедуры в этой задаче применяются tooAzure облачных служб. Для получения сведений о службах приложений см. [эту статью](../app-service-web/web-sites-custom-domain-name.md). Для получения сведений об учетных записях хранения см. [эту статью](../storage/blobs/storage-custom-domain-name.md).
> 
> 

<p/>

> [!TIP]
> Быстрее--начните использовать новый Azure hello [интерактивной Пошаговое руководство](http://support.microsoft.com/kb/2990804)!  С его помощью вы без труда сможете связать пользовательское доменное имя И защитить обмен данными (SSL) с облачными службами Azure или веб-сайтами Azure.
> 
> 

## <a name="understand-cname-and-a-records"></a>Что такое записи CNAME и A
Запись CNAME (псевдоним записи или) и-записи и обеспечения tooassociate доменное имя с конкретным сервером (или службы в этом случае) тем не менее они работают по-разному. Существуют некоторые специальные рекомендации при использовании Azure облачных службах, которые следует учесть, прежде чем решить, какие toouse записей.

### <a name="cname-or-alias-record"></a>Запись CNAME, или запись псевдонима
Запись CNAME сопоставляет *конкретных* домена, таких как **contoso.com** или **www.contoso.com**, tooa канонического имени домена. В этом случае hello канонического имени домена — hello **.cloudapp [myapp] .net** приложения размещенного доменное имя в Azure. После создания hello CNAME создает псевдоним hello **.cloudapp [myapp] .net**. запись CNAME Hello разрешит toohello IP-адрес вашего **.cloudapp [myapp] .net** службы автоматически, поэтому при изменении IP-адрес hello hello облачной службы, у вас tootake какие-либо действия.

> [!NOTE]
> Некоторые регистраторов возможна только поддомены toomap при использовании записи CNAME, например www.contoso.com и не корневых имен, например contoso.com. Дополнительные сведения о записи CNAME в разделе документации hello вашего регистратора [hello запись CNAME-запись в Википедии](http://en.wikipedia.org/wiki/CNAME_record), или hello [IETF доменных имен - реализацию и спецификация](http://tools.ietf.org/html/rfc1035) документ.
> 
> 

### <a name="a-record"></a>Запись А
*A* запись сопоставляет домен, таких как **contoso.com** или **www.contoso.com**, *или подстановочный домен* например  **\*. contoso.com**, tooan IP-адрес. В случае hello облачной службы Azure hello виртуального IP-адреса службы hello. Поэтому hello основным преимуществом записи CNAME-запись, можно настроить одну строку, в которой используется подстановочный знак, таких как \* **. contoso.com**, который будет обрабатывать запросы для нескольких поддоменов например  **Mail.contoso.com**, **login.contoso.com**, или **www.contso.com**.

> [!NOTE]
> Поскольку записи сопоставлена tooa статический IP-адрес автоматически разрешить изменения toohello IP-адрес облачной службы. Hello IP-адрес, используемый облачной службы выделяется hello первом развертывании tooan пустой слот (производственной или промежуточной.) При удалении развертывания hello для слота hello hello IP-адрес, выпускаемых Azure и любой интервал toohello будущих развертываний могут предоставить новый IP-адрес.
> 
> К счастью hello IP-адрес освобождаемой данного развертывания (рабочий или промежуточный) сохраняется, если переключаться между промежуточной и производственной среде или выполнение обновления на месте существующего развертывания. Дополнительные сведения о выполнении этих действий см. в разделе [как toomanage облачные службы](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Добавление записи CNAME для пользовательского домена
toocreate запись CNAME, необходимо добавить новую запись в таблице hello DNS для личного домена с помощью средств hello регистратора. Каждый регистратор имеет похожие, но немного другой метод указания запись CNAME, но принципы приветствия hello таким же.

1. Используйте один из этих методов toofind hello **. cloudapp.net** имя домена, назначенное tooyour облачной службы.
   
   * Toohello входа [портал Azure]выберите облачную службу, просмотрите hello **Essentials** статьи и найдите hello **URL-адрес сайта** входа.
     
       ![Отображение URL-адрес сайта hello раздел быстрый обзор][csurl]
     
       **OR**
   * Установка и настройка [Azure Powershell](/powershell/azure/overview), а затем hello используйте следующую команду:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Сохраните hello доменного имени, используемого в hello URL-адрес, возвращенный любого метода, как он потребуется при создании записи CNAME.
2. Войдите на веб-сайте регистратора DNS tooyour и переход на страницу toohello управления DNS. Найдите ссылки или области hello узла помечены как **доменное имя**, **DNS**, или **управление сервером имен**.
3. Теперь найдите место, где можно выбрать или ввести CNAME. Имеется запись hello tooselect тип из раскрывающегося списка или перейдите tooan страница «Дополнительные параметры». Следует искать слова hello **CNAME**, **псевдоним**, или **поддомены**.
4. Необходимо также указать домен hello или поддомен псевдоним для hello CNAME, таких как **www** Если требуется псевдоним для toocreate **www.customdomain.com**. Если требуется toocreate псевдоним для hello корневого домена, он имеет отметку hello "**@**" символа в средствах вашего регистратора DNS.
5. Затем необходимо предоставить каноническое имя узла, которым в данном случае является домен **cloudapp.net** вашего приложения.

Например, следующая запись CNAME hello перенаправляет весь трафик от **www.contoso.com** слишком**contoso.cloudapp.net**, hello пользовательское доменное имя развернутого приложения:

| Псевдоним/Имя узла/Поддомен | Канонический домен |
| --- | --- |
| www |contoso.cloudapp.net |

> [!NOTE]
> Посетитель из **www.contoso.com** не увидите hello true узла (contoso.cloudapp.net), поэтому hello процессом перенаправления является невидимым toothe конечного пользователя.
> 
> Hello приведенном выше примере применяется только tootraffic на hello **www** дочерний домен. Поскольку с записями CNAME нельзя использовать подстановочные знаки, необходимо создать один CNAME для каждого домена или поддомена. Следует ли toodirect трафик из дочерних доменов, например *. contoso.com, адрес cloudapp.net tooyour, можно настроить **перенаправления URL-адреса** или **вперед URL-адрес** запись в параметры DNS или создать запись.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Добавление записи A для пользовательского домена
toocreate A-записи, необходимо сначала найти hello виртуальный IP-адрес облачной службы. Добавьте новую запись в таблице hello DNS для личного домена, с помощью инструментов hello регистратора. Каждый регистратор имеет похожие, но немного другой метод указания записи, но принципы приветствия hello таким же.

1. Используйте одну из hello следующие методы tooget hello IP-адрес облачной службы.
   
   * Toohello входа [портал Azure]выберите облачную службу, просмотрите hello **Essentials** статьи и найдите hello **открытый IP-адреса** входа.
     
       ![быстрый обзор раздела, показывающая hello виртуальных IP-адресов][vip]
     
       **OR**
   * Установка и настройка [Azure Powershell](/powershell/azure/overview), а затем hello используйте следующую команду:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Сохраните hello IP-адрес, так как он потребуется при создании записи.
2. Войдите на веб-сайте регистратора DNS tooyour и переход на страницу toohello управления DNS. Найдите ссылки или области hello узла помечены как **доменное имя**, **DNS**, или **управление сервером имен**.
3. Теперь найдите место, где можно выбрать или ввести запись А. Имеется запись hello tooselect тип из раскрывающегося списка или перейдите tooan страница «Дополнительные параметры».
4. Выберите или введите домен hello или поддомен, который будет использовать эту запись A. Например, выберите **www** Если требуется псевдоним для toocreate **www.customdomain.com**. Toocreate входа подстановочный знак для все поддомены, введите "***". Так будут охвачены все поддомены, такие как **mail.customdomain.com**, **login.customdomain.com** и **www.customdomain.com**.
   
    Если требуется toocreate A записи для hello корневого домена, его могут быть указаны как hello "**@**" символа в средствах вашего регистратора DNS.
5. Введите IP-адрес hello облачной службы в hello в предоставленные поля. Это связывает hello записи домена, используемого в записи hello hello IP-адрес развертывания облачной службы.

Например, следующая запись hello перенаправляет весь трафик от **contoso.com** слишком**137.135.70.239**, IP-адрес развернутое приложение hello:

| Имя узла/Поддомен | IP-адрес |
| --- | --- |
| @ |137.135.70.239 |

В этом примере показано создание записи A для hello корневого домена. При желании toocreate toocover входа подстановочные все поддомены, необходимо ввести "***" как поддомен hello.

> [!WARNING]
> IP-адреса в Azure по умолчанию являются динамическими. Возможно, вы захотите toouse [зарезервированные IP-адреса](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure, IP-адрес не изменяется.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* [Как tooManage облачных служб](cloud-services-how-to-manage.md)
* [Как tooMap содержимого CDN tooa пользовательского домена](../cdn/cdn-map-content-to-custom-domain.md)
* [Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).
* Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy-portal.md).
* Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[портал Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
