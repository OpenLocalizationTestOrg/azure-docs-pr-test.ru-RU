---
title: "aaaConfigure SSL для облачной службы | Документы Microsoft"
description: "Узнайте, как toospecify конечной точки HTTPS для веб-роли и как tooupload SSL сертификат toosecure приложения. В этих примерах используются hello портал Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a>Настройка SSL для приложения в Azure
> [!div class="op_single_selector"]
> * [Портал Azure](cloud-services-configure-ssl-certificate-portal.md)
> * [классическом портале Azure](cloud-services-configure-ssl-certificate.md)
>

Безопасное шифрование Socket Layer (SSL) — наиболее часто используемые hello способ защиты данных, передаваемых через hello Интернета. Продолжение вводимых рассматриваются как toospecify конечной точки HTTPS для веб-роли и как tooupload SSL сертификат toosecure приложения.

> [!NOTE]
> Hello процедуры в этой задаче применяются tooAzure облачные службы; Службы приложений. в разделе [это](../app-service-web/web-sites-configure-ssl-certificate.md).
>

В этой задаче используется рабочее развертывание. В конце hello в этом разделе предоставляются сведения об использовании промежуточного развертывания.

Если вы еще не создали облачную службу, сначала прочтите [эту статью](cloud-services-how-to-create-deploy-portal.md) .

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Шаг 1. Получение SSL-сертификата
tooconfigure SSL для приложения, необходимо сначала tooget SSL-сертификат, подписанный по сертификации (ЦС), доверенным сторонним, выдающий сертификаты для этой цели. Если вы не сделали этого, необходимо один tooobtain компания продает SSL-сертификаты.

Hello сертификат должен удовлетворять hello следующие требования к SSL-сертификаты в Azure.

* Hello сертификат должен содержать закрытый ключ.
* необходимо создать сертификат Hello для обмена ключами, tooa экспортируемый файл обмена личной информацией (PFX-файл).
* Hello имя субъекта сертификата должно соответствовать hello домен, используемый tooaccess hello облачной службы. Не удается получить SSL-сертификат из сертификата центром сертификации (ЦС) для домена cloudapp.net hello. Для этого нужно получить имя пользовательского домена toouse при обращении к службе. Когда вы запрашиваете сертификат из центра сертификации, имя субъекта сертификата hello должно соответствовать hello доменное имя, используемое tooaccess приложения. Например, если вы используете домен **contoso.com**, необходимо запросить сертификат из центра сертификации для ***.contoso.com** или **www.contoso.com**.
* Hello сертификата необходимо использовать не менее 2048-битное шифрование.

В целях тестирования вы можете [создать](cloud-services-certs-create.md) и использовать самозаверяющий сертификат. Самозаверяющий сертификат не прошел проверку подлинности через ЦС и hello cloudapp.net домен можно использовать как URL-адрес веб-сайта hello. Например, hello следующей задаче используется самозаверяющий сертификат, в которой hello — общее имя (CN) в сертификате hello **sslexample.cloudapp.net**.

После этого необходимо включить сведения о сертификате hello в определение службы и файлы конфигурации службы.

<a name="modify"> </a>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>Шаг 2: Измените файлы определения и конфигурации службы hello
Приложение должно быть настроенный toouse hello сертификата и необходимо добавить конечную точку HTTPS. В результате hello определение службы и файлы конфигурации службы необходимо обновить toobe.

1. В среде разработки, откройте hello файл определения службы (CSDEF), добавьте **сертификаты** раздела в hello **WebRole** статьи и включите следующую информацию hello сертификат (и промежуточные сертификаты):

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   Hello **сертификаты** раздел определяет имя hello нашей сертификата, его расположение и имя hello hello хранилища, где он расположен.

   Разрешения (`permisionLevel` атрибут) может быть tooone набор из hello следующие значения:

   | Значение разрешения | Описание |
   | --- | --- |
   | limitedOrElevated |**(По умолчанию)**  Всем процессам роли можно получить доступ к закрытым ключом hello. |
   | elevated |Только процессов с повышенными правами можно получить доступ к закрытым ключом hello. |

2. В файле определения службы добавьте **InputEndpoint** элемент в пределах hello **конечные точки** статьи tooenable HTTPS:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. В файле определения службы добавьте **привязки** элемент в пределах hello **сайтов** раздела. Этот элемент добавляет toomap привязки HTTPS сайта tooyour конечной точки:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   Файл определения всех hello необходимые изменения toohello службы будет завершена; но по-прежнему требуются сведения сертификата hello tooadd для файла конфигурации службы hello.
4. В файле конфигурации службы (CSCFG-файл) ServiceConfiguration.Cloud.cscfg в разделе **Certificates** добавьте значения из своего сертификата. Hello следующий образец кода обеспечивает сведения о hello **сертификаты** разделе, за исключением значение отпечатка hello.

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

(В этом примере используется **sha1** для hello алгоритм отпечатка. Укажите соответствующее значение hello алгоритм отпечатка вашего сертификата).

Теперь, когда hello определения и обновления файлов конфигурации службы были обновлены, пакет развертывания для передачи tooAzure. Если используется **cspack**, не используйте флаг **/generateConfigurationFile**, так как это приведет к перезаписи сведений о сертификате, которые вы только что добавили.

## <a name="step-3-upload-a-certificate"></a>Шаг 3. Отправка сертификата
Подключение toohello портал Azure и...

1. В hello **все ресурсы** hello портала, выберите вариант облачной службы.

    ![Публикация облачной службы](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. Щелкните **Сертификаты**.

    ![Щелкните значок сертификаты hello](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. Нажмите кнопку **отправить** hello верхней части области сертификаты hello.

    ![Пункт меню hello передачи](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. Укажите hello **файл**, **пароль**, нажмите кнопку **отправить** hello нижней части области ввода данных hello.

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Шаг 4: Экземпляр роли toohello подключения по протоколу HTTPS
Теперь, когда развертывание работает в Azure, можно подключить tooit, с помощью протокола HTTPS.

1. Нажмите кнопку hello **URL-адрес сайта** tooopen hello веб-браузера.

   ![Щелкните URL-адрес сайта hello](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. В веб-браузере изменить ссылку toouse hello **https** вместо **http**, а затем на странице приветствия.

   > [!NOTE]
   > Если вы используете самозаверяющий сертификат, при просмотре конечной точки HTTPS tooan, связанной с самозаверяющим сертификатом hello может появиться сообщение об ошибке сертификата в браузере hello. Использовать сертификат, подписанный доверенным центром сертификации избавиться от этой проблемы; в hello временем, ошибку можно игнорировать hello. (Другой вариант — tooadd hello самозаверяющий сертификат toohello доверенный сертификат центра хранилище сертификатов пользователя).
   >
   >

   ![Предварительный просмотр сайта](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > Если требуется toouse SSL для промежуточного развертывания вместо развертывания в рабочей среде, сначала необходимо toodetermine hello URL-адреса для hello промежуточное развертывание. После развертывания облачной службы toohello URL-адрес hello промежуточной среде определяется hello **идентификатор развертывания** GUID в следующем формате:`https://deployment-id.cloudapp.net/`  
   >
   > Создайте сертификат с hello общие имя (CN) равно toohello на основе GUID URL-адрес (например, **328187776e774ceda8fc57609d404462.cloudapp.net**). Используйте hello портала tooadd hello сертификат tooyour промежуточное облачной службы. Добавьте hello сертификат сведения tooyour CSDEF и CSCFG-файлы, упакуйте приложение и обновить новый пакет hello toouse промежуточное развертывание.
   >

## <a name="next-steps"></a>Дальнейшие действия
* [Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).
* Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy-portal.md).
* Настройте [пользовательское доменное имя](cloud-services-custom-domain-name-portal.md).
* [Управляйте облачной службой](cloud-services-how-to-manage-portal.md).
