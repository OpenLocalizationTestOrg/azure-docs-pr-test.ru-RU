---
title: "aaaHow toocreate и развертывание облачной службы | Документы Microsoft"
description: "Узнайте, как toocreate и развернуть облачную службу с помощью портала Azure hello."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Как toocreate и развертывание облачной службы
> [!div class="op_single_selector"]
> * [Портал Azure](cloud-services-how-to-create-deploy-portal.md)
> * [классическом портале Azure](cloud-services-how-to-create-deploy.md)
>
>

Hello Azure предоставляет два способа для вас toocreate и развертывание облачной службы: *быстрое создание* и *настраиваемое создание*.

В этой статье объясняется, как toouse hello toocreate метод быстрое создание новой облачной службы, а затем используйте **отправить** tooupload и развернуть пакет облачной службы в Azure. При использовании этого метода hello портал Azure делает доступных ссылок, удобный для выполнения всех требований, при переходе. Если вы готовы toodeploy вашей облачной службы при его создании, это можно сделать из hello одновременно с помощью настраиваемое создание.

> [!NOTE]
> Если планируется toopublish облачной службы из Visual Studio Team Services (VSTS), использовать функцию быстрого запуска и затем настроить публикацию VSTS с панели мониторинга быстрый запуск Azure или hello hello. Дополнительные сведения см. в разделе [tooAzure непрерывной поставки с помощью Visual Studio Team Services][TFSTutorialForCloudService], или получить справки для hello **быстрый запуск** страницы.
>
>

## <a name="concepts"></a>Основные понятия
Три компонента находятся необходимые toodeploy приложения как облачной службы в Azure:

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

* Если требуется, чтобы toodeploy облачной службы, которая использует протокол Secure Sockets Layer (SSL) для шифрования данных, [настройки приложения](cloud-services-configure-ssl-certificate-portal.md#modify) для SSL.
* Если нужно экземпляров toorole подключения удаленного рабочего стола tooconfigure, [настроить роли hello](cloud-services-role-enable-remote-desktop-new-portal.md) для удаленного рабочего стола.
* Если вы хотите tooconfigure подробного мониторинга для облачной службы, включение диагностики Azure для hello облачной службы. *Минимальный мониторинг* (по умолчанию hello уровень мониторинга) использует счетчики производительности, собранных из операционных систем узлов hello для экземпляров роли (виртуальных машин). *Подробный мониторинг* собирает дополнительные метрики на основе данных производительности в рамках hello экземпляры роли tooenable более тщательного анализа проблем, возникающих во время обработки приложения. в разделе диагностики Azure tooenable, toofind о том, как [включение диагностики в Azure](cloud-services-dotnet-diagnostics.md).

необходимо toocreate облачную службу с развертываниями веб-ролей или рабочих ролей [создать пакет службы hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Перед началом работы
* Если вы не установили hello Azure SDK, нажмите кнопку **установить пакет Azure SDK** tooopen hello [страницу загрузок Azure](https://azure.microsoft.com/downloads/)и загрузите hello пакета SDK для hello язык, в котором toodevelop кода. (Чтобы иметь возможность toodo это более поздней версии.)
* Если все экземпляры ролей, требуется сертификат, создайте сертификаты hello. В облачных службах используется PFX-файл с закрытым ключом. Можно передать tooAzure сертификаты hello, как создать и развернуть облачную службу hello.

## <a name="create-and-deploy"></a>Создание и развертывание
1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Нажмите кнопку **Создать > вычислений**, а затем прокрутите экран вниз tooand щелкните **облачной службы**.

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. В новых hello **облачной службы** колонки, введите значение для hello **DNS-имя**.
4. Создайте новую **группу ресурсов** или выберите существующую.
5. Выберите **расположение**.
6. Щелкните **Пакет**. После этого откроется hello **загрузки пакета** колонку. Заполните необходимые hello. Если какая-либо из ролей содержит отдельный экземпляр, убедитесь, что установлен флажок **Развернуть, даже если одна или несколько ролей содержат отдельный экземпляр** .
7. Убедитесь, что установлен флажок **Запустить развертывание** .
8. Нажмите кнопку **ОК** которого будет закрыт hello **загрузки пакета** колонку.
9. Если у вас tooadd все сертификаты, щелкните **создать**.

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Загрузить сертификат
Если пакет развертывания был [настроить сертификаты toouse](cloud-services-configure-ssl-certificate-portal.md#modify), теперь можно отправить сертификат hello.

1. Выберите **сертификаты**и на hello **Добавление сертификатов** колонке выберите PFX-файл сертификата SSL hello, а затем введите hello **пароль** для сертификата hello
2. Нажмите кнопку **сертификат присоединения**и нажмите кнопку **ОК** на hello **добавить сертификаты** колонку.
3. Нажмите кнопку **создать** на hello **облачной службы** колонку. При развертывании hello достиг hello **готовности** состояние, можно продолжить toohello дальнейшие действия.

    ![Публикация облачной службы](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Проверка успешного завершения развертывания
1. Щелкните экземпляр службы hello облака.

    Hello состояния должен показать, что служба hello **под управлением**.
2. В разделе **Essentials**, нажмите кнопку hello **URL-адрес сайта** tooopen вашей облачной службы в веб-браузере.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Дальнейшие действия
* [Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).
* Настройка [пользовательского имени домена](cloud-services-custom-domain-name-portal.md).
* [Управление облачной службой](cloud-services-how-to-manage-portal.md).
* Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).
