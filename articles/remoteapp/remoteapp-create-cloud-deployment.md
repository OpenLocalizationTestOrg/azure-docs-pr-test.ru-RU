---
title: "aaaHow toocreate коллекцию Azure RemoteApp облака | Документы Microsoft"
description: "Узнайте, как развертывание Azure RemoteApp, которая сохраняет данные в toocreate hello облако Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>Как toocreate облака коллекцию Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Существует два типа [коллекций Azure RemoteApp](remoteapp-collections.md): 

* Облачные: располагаются полностью в Azure. Toosave можно выбрать все данные в облаке hello (поэтому коллекции только для облака) или tooconnect вашей коллекции tooa виртуальной сети и сохранения данных существует.   
* Гибридное: включает виртуальную сеть для локального доступа — это потребует hello использование Azure AD и в локальной среде Active Directory.

Этот учебник поможет выполнить процесс создания облачной коллекции hello. Этот процесс состоит из четырех этапов. 

1. Создание коллекции Azure RemoteApp
2. При необходимости настройка синхронизации каталогов. Если вы используете Azure AD + Active Directory имеются toosynchronize пользователей, контактов и паролей из вашего клиента Azure AD tooyour локальной Active Directory.
3. Публикация приложений
4. Настройка доступа пользователей.

**Перед началом работы**

Необходимы следующие hello toodo перед созданием коллекции hello.

* [Зарегистрируйтесь](https://azure.microsoft.com/services/remoteapp/) в Azure RemoteApp. 
* Сбор сведений о пользователях hello, которым требуется доступ toogrant. Это могут быть либо данные учетной записи Майкрософт, либо данные рабочей учетной записи Active Directory пользователя.
* Эта процедура предполагает, что являются либо постоянной toouse одного из образов шаблона hello, предоставляемых в рамках вашей подписки или наличие уже отправлен требуется toouse образ шаблона hello. Если вам требуется tooupload изображение другого шаблона, можно сделать, со страницы приветствия образы шаблонов. Просто щелкните **отправить образ шаблона** и следуйте указаниям мастера hello в hello. 
* Требуется toouse hello Office 365 профессиональный плюс изображение? Ознакомьтесь с [этой информацией](remoteapp-officesubscription.md).
* Требуется tooprovide пользовательские приложения или бизнес-программ? Создайте [образ](remoteapp-imageoptions.md) и используйте его в своей облачной коллекции.
* Понять, нужна ли tooconnect tooa виртуальной сети. При выборе tooconnect tooa виртуальной сети, убедитесь, что он соответствует hello [изменения размера рекомендации](remoteapp-vnetsizing.md) и что он [могут подключаться tooRemoteApp](remoteapp-vnet.md). Извлечение hello [виртуальной сети планирования статьи ](remoteapp-planvnet.md)для получения дополнительной информации.
* Если вы используете виртуальную сеть, решите, будет ли toojoin его tooyour локального домена Active Directory.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>Шаг 1. Создание облачной коллекции – с виртуальной сетью или без нее.
Используйте hello следующие шаги слишком**создания коллекции только для облака**:

1. На портале управления hello переход на страницу toohello RemoteApp.
2. Щелкните **Создать > Быстрое создание**.
3. Введите имя коллекции и выберите регион.
4. Выбор нужных toouse - стандартные или базовые плана hello.
5. Выберите toouse hello шаблона для этой коллекции. 
   
    **Совет:** подписку на RemoteApp поставляется с [образы шаблонов](remoteapp-images.md) , которые содержат Office 365 или Office 2013 (для пробного использования) программы, некоторые публикации (например Word) и другие готовы toopublish. Вы также можете создать [образ](remoteapp-imageoptions.md) и использовать его в своей облачной коллекции.
6. Щелкните **Создать коллекцию RemoteApp**.
   
    **Важно:** может занять tooprovision минут too30 вашей коллекции.

После создания коллекции Azure RemoteApp, дважды щелкните имя hello hello коллекции. Появится hello **быстрый запуск** страница — это где завершения настройки коллекции hello.

Используйте hello следующие шаги toocreate **облако + виртуальной сети коллекции**:

1. На портале управления hello переход на страницу toohello Azure RemoteApp.
2. Щелкните **Создать** > **Создать с помощью VNet**.
3. Введите имя своей коллекции.
4. Выбор нужных toouse - стандартные или базовые плана hello.
5. Выберите hello виртуальной сети, которые уже созданы. Не знаете, как toodo? На данном этапе hello действия находятся в hello [гибридных](remoteapp-create-hybrid-deployment.md) раздела.
6. Решите, будет ли toojoin домена tooyour коллекции. Если Да, вам потребуется toointegrate Connect toouse AD Azure AD и средой Active Directory. Это описано ниже в **Шаге 2**.
7. Щелкните **Создать коллекцию RemoteApp**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>Шаг 2. Настройка синхронизации каталогов Active Directory (при необходимости)
Если вы хотите toouse Active Directory, Azure RemoteApp требует синхронизации службы каталогов между Azure Active Directory и вашей локальной Active Directory toosynchronize пользователей, контактов и клиента Azure Active Directory tooyour пароли. Сведения о планировании см. в статье [Требования Azure AD + Active Directory для Azure RemoteApp](remoteapp-ad.md). Можно также перейти непосредственно слишком[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) сведения.

## <a name="step-3-publish-apps"></a>Шаг 3. Публикация приложений
Приложение Azure RemoteApp является приложение hello или предоставить пользователям tooyour программы. Он находится в образе шаблона hello, загруженный для hello коллекции. Когда пользователь открывает приложение, приложение hello отображается toorun в своей локальной среде, но он действительно выполняется на виртуальной машине в Azure. 

Для доступа приложения, необходимо, чтобы toopublish их — публикации приложений позволяет пользователям доступа к приложениям hello через hello клиента удаленного рабочего стола.

Можно опубликовать несколько приложений tooyour коллекции Azure RemoteApp. На странице приветствия публикации нажмите **публикации** tooadd программы. Можно либо опубликовать hello **запустить** меню hello образа шаблона или указав путь hello на hello образ шаблона для приложения hello. Если выбрать tooadd hello **запустить** меню, выберите toopublish приложения hello. Если приложение toohello tooprovide hello пути, укажите имя для приложения hello и toowhere путь hello, установленному на образ шаблона hello.

## <a name="step-4-configure-user-access"></a>Шаг 4. Настройка доступа пользователей
После создания коллекции необходимо tooadd hello пользователям требуется доступ toouse toobe удаленных ресурсов. При использовании Active Directory предоставляют доступ tooneed tooexist в клиент Active Directory hello связанных с подпиской hello пользователей hello используется toocreate этой коллекции.

1. На странице быстрого запуска приветствия щелкните **настроить доступ пользователя**. 
2. Введите hello рабочей учетной записи (из Active Directory) или учетной записи Майкрософт, которую требуется toogrant для.
   
   **Примечания.** 
   
   Убедитесь, что используется hello  *user@domain.com*  формат.
   
   Если вы используете Office 365 профессиональный плюс в коллекции, необходимо использовать hello удостоверения Active Directory для пользователей. Это поможет проверять лицензирование. 
3. После проверки пользователей hello щелкните **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
Итак, облачная коллекция Azure RemoteApp успешно создана и развернута. Hello следующим шагом является toohave пользователей загрузить и установить клиент удаленного рабочего стола hello. Hello URL-адрес для hello клиента можно найти на странице быстрого запуска Azure RemoteApp hello. Затем у пользователей, входящих в клиент hello и получать доступ к приложениям hello публикации.

### <a name="help-us-help-you"></a>Помогите нам помочь вам
Знали ли вы, что в toorating сложения в этой статье и создания примечаний вниз ниже, можно внести самой статье toohello изменения? Чего-то не хватает? Что-то неправильно? Что-то изложено непонятно? Прокрутка вверх и нажмите кнопку **изменить на GitHub** изменения toomake - те поступит toous для просмотра и, когда мы выйдите из системы на них, вы увидите, изменения и усовершенствования здесь.

