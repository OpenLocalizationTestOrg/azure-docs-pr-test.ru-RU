---
title: "aaaHow toocreate и развертывание облачной службы | Документы Microsoft"
description: "Узнайте, как toocreate и развертывание облачной службы, с помощью метода быстрого создания hello в Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Как tooCreate и развертывание облачной службы
> [!div class="op_single_selector"]
> * [Портал Azure](cloud-services-how-to-create-deploy-portal.md)
> * [классическом портале Azure](cloud-services-how-to-create-deploy.md)
> 
> 

Hello классический портал Azure предоставляет два способа для вас toocreate и развертывание облачной службы: **быстрое создание** и **настраиваемое создание**.

В этом разделе объясняется, как toouse hello toocreate метод быстрое создание новой облачной службы, а затем используйте **отправить** tooupload и развернуть пакет облачной службы в Azure. При использовании этого метода hello классический портал Azure делает доступных ссылок, удобный для выполнения всех требований, при переходе. Если вы готовы toodeploy вашей облачной службы при его создании, это можно сделать из hello используя **настраиваемое создание**.

> [!NOTE]
> Если планируется toopublish облачной службы из Visual Studio Team Services (VSTS), используйте **быстрое создание**и затем настроить публикацию VSTS из **быстрый запуск** или панели мониторинга hello.
> 
> 

## <a name="concepts"></a>Основные понятия
В порядке toodeploy приложения как облачной службы в Azure требуются три компонента:

* **Определение службы.**  
  облако Hello для файла определения службы (.csdef) определяет модель службы hello, включая hello число ролей.
* **Конфигурация службы.**  
  файл конфигурации облачной службы Hello (.cscfg) предоставляет параметры конфигурации для hello облачной службы и отдельных ролей, включая hello число экземпляров роли.
* **Пакет службы.**  
  Hello пакета службы (cspkg-файл) содержит код приложения hello и конфигурации и файл определения службы hello.

Дополнительные сведения об этих и как toocreate пакета [здесь](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Подготовка приложения
Перед развертыванием облачной службы необходимо создать пакет hello облачной службы (cspkg-файл) с кодом приложения и файл конфигурации облачной службы (.cscfg). Hello Azure SDK предоставляет средства для подготовки этих требуемые файлы развертывания. Можно установить пакет SDK для hello из hello [загрузки Azure](https://azure.microsoft.com/downloads/) страницы на языке hello, в котором вы предпочитаете toodevelop код вашего приложения.

Перед экспортом пакета службы необходимо отдельно настроить три компонента облачной службы:

* Если требуется, чтобы toodeploy облачной службы, которая использует протокол Secure Sockets Layer (SSL) для шифрования данных, [настройки приложения](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) для SSL.
* Если нужно экземпляров toorole подключения удаленного рабочего стола tooconfigure, [настроить роли hello](cloud-services-role-enable-remote-desktop.md) для удаленного рабочего стола.
* Если вы хотите tooconfigure подробного мониторинга для облачной службы, включение диагностики Azure для hello облачной службы. *Минимальный мониторинг* (по умолчанию hello уровень мониторинга) использует счетчики производительности, собранных из операционных систем узлов hello для экземпляров роли (виртуальных машин). «Подробный мониторинг * собирает дополнительные метрики на основе данных производительности в рамках hello экземпляры роли tooenable более тщательного анализа проблем, возникающих во время обработки приложения. в разделе диагностики Azure tooenable, toofind о том, как [включение диагностики в Azure](cloud-services-dotnet-diagnostics.md).

необходимо toocreate облачную службу с развертываниями веб-ролей или рабочих ролей [создать пакет службы hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Перед началом работы
* Если вы не установили hello Azure SDK, нажмите кнопку **установить пакет Azure SDK** tooopen hello [страницу загрузок Azure](https://azure.microsoft.com/downloads/)и загрузите hello пакета SDK для hello язык, в котором toodevelop кода. (Чтобы иметь возможность toodo это более поздней версии.)
* Если все экземпляры ролей, требуется сертификат, создайте сертификаты hello. В облачных службах используется PFX-файл с закрытым ключом. Вы можете [отправить hello сертификаты tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) как создать и развернуть облачную службу hello.
* Если планируется toodeploy hello облачной службы tooan территориальную группу, создайте территориальную группу hello. Можно использовать территориальную группу toodeploy облачных служб и других служб Azure toohello местоположения в области. Можно создать hello территориальную группу в hello **сетей** область hello классический портал Azure, на hello **Территориальные группы** страницы.

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>Практическое руководство. Создание облачной службы с помощью функции "Быстрое создание"
1. В hello [классический портал Azure](http://manage.windowsazure.com/), нажмите кнопку **New**>**вычислений**>**облачной службы** > **Быстрое создание**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. В **URL-адрес**, введите имя дочернего домена toouse в hello общедоступный URL-адрес для доступа к облачной службы в производственной среде. формат URL-адреса Hello для рабочих развертываний: http://*myURL*. cloudapp.net.
3. В **регион или территориальная группа**, выберите hello географическом регионе или территориальной группе toodeploy hello облачной службы. Выберите территориальную группу, если требуется toodeploy вашей облачной службы toohello же расположении, что другие службы Azure в области.
4. Выберите **Создать облачную службу**.
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    Можно отслеживать состояние hello hello процесса в области сообщений hello hello нижней части окна hello.
   
    Hello **облачные службы** откроется область с новой облачной службе hello отображается. При изменении состояния hello tooCreated создания облачной службы успешно завершена.
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>Практическое руководство. Отправка сертификата для облачной службы
1. В hello [классический портал Azure](http://manage.windowsazure.com/), нажмите кнопку **облачные службы**, щелкните имя hello hello облачной службы и нажмите кнопку **сертификаты**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. Щелкните **Отправить сертификат** или **Отправить**.
3. В **файл**, используйте **Обзор** tooselect hello сертификат (PFX-файл).
4. В **пароль**, введите hello закрытый ключ для сертификата hello.
5. Нажмите кнопку **OK** (флажок).
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    Можно отслеживать ход выполнения hello передачи hello в области сообщений hello, показано ниже. По завершении передачи hello hello сертификат добавляется toohello таблицы. В области сообщений hello нажмите кнопку ОК tooclose приветственное сообщение.
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>Практическое руководство. Развертывание облачной службы
1. В hello [классический портал Azure](http://manage.windowsazure.com/), нажмите кнопку **облачные службы**, щелкните имя hello hello облачной службы и нажмите кнопку **мониторинга**.
2. Щелкните **Загрузите новое рабочее развертывание** или **Отправить**.
3. В **метка развертывания**, введите имя для нового развертывания hello - например, MyCloudServicev4.
4. В **пакета**, используйте **Обзор** tooselect hello службы пакета файл (cspkg) toouse.
5. В **конфигурации**, используйте **Обзор** tooselect hello службы настройки toouse файл (cscfg).
6. Если только с одним экземпляром hello облачной службы будет включать все роли, выберите hello **развернуть, даже если одна или несколько ролей содержат отдельный экземпляр** tooproceed развертывания hello tooenable флажок.
   
    Azure можно только гарантирует 99,95% доступа toohello облачной службы во время обслуживания и обновления, если у каждой роли есть по крайней мере два экземпляра. При необходимости можно добавить дополнительные экземпляры роли на hello **шкалы** после того, как развернуть облачную службу hello. Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).
7. Нажмите кнопку **ОК** развертывания облачной службы (в виде галочки) toobegin hello.
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    Можно отслеживать состояние hello hello развертывания в области сообщений hello. Нажмите кнопку ОК toohide приветственное сообщение.
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>Проверка успешного завершения развертывания
1. Нажмите на кнопку **Панель мониторинга**.
   
    Hello состояния должен показать, что служба hello **под управлением**.
2. В разделе **быстрый обзор**, нажмите кнопку tooopen URL-адрес сайта hello облачной службы в веб-браузере.
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>Дальнейшие действия
* [Общая настройка облачной службы](cloud-services-how-to-configure.md).
* Настройка [пользовательского имени домена](cloud-services-custom-domain-name.md).
* [Управление облачной службой](cloud-services-how-to-manage.md).
* Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate.md).

