---
title: "сертификаты службы и управления ими aaaCloud | Документы Microsoft"
description: "Узнайте, как toocreate и использование сертификатов с Microsoft Azure"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Общие сведения о сертификатах для облачных служб Azure
Использовать сертификаты для облачных служб в Azure ([сертификаты службы](#what-are-service-certificates)) и для проверки подлинности с помощью API-Интерфейс управления hello ([сертификаты управления](#what-are-management-certificates) при с помощью классического портала Azure hello и не Hello не классический портал Azure). В этом разделе приводится общий обзор обоих типов сертификатов, как слишком[создания](#create) и [развертывание](#deploy) их tooAzure.

Сертификаты, используемые в Azure, являются сертификатами x.509 v3; они могут быть заверены другим доверенным сертификатом или быть самозаверяющими. Поскольку самозаверяющий сертификат подписывает его автор, он не считается надежным по умолчанию. Большинство браузеров может игнорировать эту проблему. Самозаверяющие сертификаты должны использоваться только при разработке и тестировании облачных служб. 

Сертификаты, используемые в Azure, могут содержать закрытый или открытый ключ. Сертификаты имеют отпечаток, предоставляющий tooidentify означает их однозначной. Этот отпечаток используется в hello Azure [файла конфигурации](cloud-services-configure-ssl-certificate.md) tooidentify которого сертификатов облачной службы следует использовать. 

## <a name="what-are-service-certificates"></a>Что такое сертификаты службы
Сертификаты службы — это вложенное toocloud службы и включите tooand безопасного обмена данными из службы hello. Например если вы развернули веб-роли, нужно toosupply сертификат, который может проверить подлинность предоставляется конечная точка HTTPS. Сертификаты службы, определенные в определении службы, являются toohello автоматически развернутой виртуальной машины, на котором выполняется экземпляр роли. 

Вы можете отправить классический tooAzure сертификаты службы портала либо с помощью hello Azure классического портала или с помощью hello классической модели развертывания. Эти сертификаты связаны с конкретной облачной службой. Они назначаются tooa развертывания в файле определения службы hello.

Сертификатами службы можно управлять отдельно от служб. Это могут делать разные пользователи. Например разработчик может передать пакет служб, который ссылается сертификат tooa ИТ-менеджер ранее загрузил tooAzure. ИТ-менеджер может управлять и обновить сертификат (изменение конфигурации hello hello службы) без необходимости tooupload новый пакет служб. Обновление без новый пакет служб возможна, потому что hello логическое имя, имя хранилища и расположение сертификата hello в файле определения службы hello и пока hello отпечаток сертификата указан в файле конфигурации службы hello. сертификат tooupdate hello, это только необходимые tooupload новый сертификат и отпечаток hello изменить значение в файле конфигурации службы hello.

>[!Note]
>Hello [облачных служб часто задаваемые вопросы о](cloud-services-faq.md) статья содержит некоторые полезные сведения о сертификатах.

## <a name="what-are-management-certificates"></a>Что такое сертификаты управления
Сертификаты управления позволяют tooauthenticate с hello классической модели развертывания. Многие программы и средства (например, Visual Studio или hello Azure SDK) использовать эти сертификаты tooautomate конфигурации и развертывания различных служб Azure. Они не toocloud действительно связанных служб. 

> [!WARNING]
> Будьте осторожны! Разрешить эти типы сертификатов всех, кто выполняет проверку подлинности с ними toomanage hello подписки, связанные с ними. 
> 
> 

### <a name="limitations"></a>Ограничения
Существует ограничение в 100 сертификатов управления на одну подписку. Существует ограничение в 100 сертификатов управления для всех подписок в рамках конкретного идентификатора пользователя администратора службы. Если hello идентификатор пользователя для учетной записи администратора hello уже используется tooadd 100 сертификатов управления и есть потребность в большем количестве сертификатов, можно добавить соадминистратора сертификаты дополнительных tooadd hello. 

Перед добавлением более 100 сертификатов убедитесь, что существующий сертификат можно использовать повторно. Использование соадминистраторов добавляет потенциально ненужную сложность tooyour сертификатов управления процесса.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>Создание самозаверяющего сертификата
Можно использовать любое средство доступных toocreate самозаверяющий сертификат при условии, что они соответствуют toothese параметры:

* Используется сертификат X.509.
* Содержит закрытый ключ.
* Создано для обмена ключами (PFX-файл).
* Имя субъекта должно соответствовать hello домен, используемый tooaccess hello облачной службы.

    > Не удается получить сертификат SSL для hello cloudapp.net (или других связанных с Azure) домена; Имя субъекта сертификата Hello должен соответствовать hello доменное имя, используемое tooaccess приложения. Например, **contoso.net**, а не **contoso.cloudapp.net**.

* Минимум 2048-разрядное шифрование.
* **Службы сертификатов только**: клиентский сертификат должен размещаться в hello *личных* хранилище сертификатов.

Существует две возможности toocreate сертификат в Windows, с hello `makecert.exe` программы или службы IIS.

### <a name="makecertexe"></a>Makecert.exe
Эта программа устарела и в данном документе не описывается. Дополнительные сведения см. в [этой статье в библиотеке MSDN](https://msdn.microsoft.com/library/windows/desktop/aa386968).

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> Сертификат hello toouse IP-адрес, а не в домен, воспользуйтесь hello IP-адрес в параметре - DnsName hello.


Если требуется toouse [сертификат с портала управления hello](../azure-api-management-certs.md), экспортировать его tooa **.cer** файла:

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)
Существует много страниц на hello Интернета, охватывающие как toodo это со службами IIS. [этой странице](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) . 

### <a name="java"></a>Java
Можно также использовать Java[создать сертификат](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).

### <a name="linux"></a>Linux
[Это](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) статье описывается, как toocreate сертификаты с SSH.

## <a name="next-steps"></a>Дальнейшие действия
[Отправьте ваш toohello сертификата службы классический портал Azure](cloud-services-configure-ssl-certificate.md) (или hello [портал Azure](cloud-services-configure-ssl-certificate-portal.md)).

Отправка [сертификата API управления](../azure-api-management-certs.md) toohello классический портал Azure. портал Azure Hello не использует сертификаты управления для проверки подлинности.

