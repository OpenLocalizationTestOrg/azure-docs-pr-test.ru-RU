---
title: "aaaConfigure SSL для облачной службы (классические) | Документы Microsoft"
description: "Узнайте, как toospecify конечной точки HTTPS для веб-роли и как tooupload SSL сертификат toosecure приложения."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
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
> 

Безопасное шифрование Socket Layer (SSL) — наиболее часто используемые hello способ защиты данных, передаваемых через hello Интернета. Продолжение вводимых рассматриваются как toospecify конечной точки HTTPS для веб-роли и как tooupload SSL сертификат toosecure приложения.

> [!NOTE]
> Hello процедуры в этой задаче применяются tooAzure облачные службы; Службы приложений. в разделе [это](../app-service-web/web-sites-configure-ssl-certificate.md) статьи.
> 
> 

В этой задаче используется рабочее развертывание. В конце hello в этом разделе предоставляются сведения об использовании промежуточного развертывания.

Если вы еще не создали облачную службу, сначала прочтите [эту](cloud-services-how-to-create-deploy.md) статью.

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

3. В файле определения службы добавьте **привязки** элемент в пределах hello **сайтов** раздела. В этом разделе добавляет toomap привязки HTTPS сайта tooyour конечной точки:
   
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
   
   Файл определения всех hello необходимые изменения toohello службы будет завершена, но по-прежнему требуются сведения сертификата hello tooadd для файла конфигурации службы hello.
4. В файле конфигурации службы (CSCFG), ServiceConfiguration.Cloud.cscfg, добавьте **сертификаты** раздела в hello **роли** раздел, заменив значение отпечатка образец hello, показано ниже с помощью который сертификата:
   
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

(hello предшествующий в этом примере используется **sha1** для hello алгоритм отпечатка. Укажите соответствующее значение hello алгоритм отпечатка вашего сертификата).

Теперь, когда hello определения и обновления файлов конфигурации службы были обновлены, пакет развертывания для передачи tooAzure. Если используется **cspack**, не используйте флаг **/generateConfigurationFile**, так как он приведет к перезаписи сведений о сертификате, которые вы добавили.

## <a name="step-3-upload-a-certificate"></a>Шаг 3. Отправка сертификата
Пакет развертывания был toouse обновленный сертификат hello и добавлена конечная точка HTTPS. Теперь можно отправить hello пакета и сертификата tooAzure hello классический портал Azure.

1. Войдите в toohello [классический портал Azure][Azure classic portal]. 
2. Нажмите кнопку **облачные службы** на панели навигации слева hello.
3. Щелкните hello требуемого облачную службу.
4. Нажмите кнопку hello **сертификаты** вкладки.
   
    ![Откройте вкладку сертификатов hello](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. Нажмите кнопку hello **отправить** кнопки.
   
    ![Отправить](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. Укажите hello **файл**, **пароль**, нажмите кнопку **завершить** (hello флажок).

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Шаг 4: Экземпляр роли toohello подключения по протоколу HTTPS
Теперь, когда развертывание работает в Azure, можно подключить tooit, с помощью протокола HTTPS.

1. В hello классический портал Azure, выберите развертывание, а затем щелкните ссылку hello в **URL-адрес сайта**.
   
   ![Определение URL-адреса сайта][2]
2. В веб-браузере изменить ссылку toouse hello **https** вместо **http**, а затем на странице приветствия.
   
   > [!NOTE]
   > Если вы используете самозаверяющий сертификат, при просмотре конечной точки HTTPS tooan, связанной с самозаверяющим сертификатом hello может появиться сообщение об ошибке сертификата в браузере hello. Использовать сертификат, подписанный доверенным центром сертификации избавиться от этой проблемы; в hello временем, ошибку можно игнорировать hello. (Другой вариант — tooadd hello самозаверяющий сертификат toohello доверенный сертификат центра хранилище сертификатов пользователя).
   > 
   > 
   
   ![Пример веб-сайта SSL][3]

Если требуется toouse SSL для промежуточного развертывания вместо развертывания в рабочей среде, необходимо сначала toodetermine hello URL-адреса для hello промежуточное развертывание. Развертывание облачной службы toohello промежуточной среде без включения сертификат или никаких сведений о сертификате. После развертывания, можно определить hello GUID URL-адрес, который указан в hello классический портал Azure **URL-адрес сайта** поля. Создайте сертификат с hello общие имя (CN) равно toohello на основе GUID URL-адрес (например, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**). Используйте hello Azure классического портала tooadd hello сертификат tooyour промежуточное облачной службы. Добавьте hello сертификат сведения tooyour CSDEF и CSCFG-файлы, упакуйте приложение и обновить новый пакет hello toouse промежуточное развертывание.

## <a name="next-steps"></a>Дальнейшие действия
* [Общая настройка облачной службы](cloud-services-how-to-configure.md).
* Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy.md).
* Настройте [пользовательское доменное имя](cloud-services-custom-domain-name.md).
* [Управляйте облачной службой](cloud-services-how-to-manage.md).

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
