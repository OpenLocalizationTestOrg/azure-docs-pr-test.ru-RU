---
title: "aaaHow toocreate гибридной коллекции для Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как toocreate развертывания RemoteApp, подключается tooyour внутренней сети."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>Как toocreate гибридной коллекции для Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Существует два типа коллекций Azure RemoteApp:

* Облачные: располагаются полностью в Azure. Toosave можно выбрать все данные в облаке hello (поэтому коллекции только для облака) или tooconnect вашей коллекции tooa виртуальной сети и сохранения данных существует.   
* Гибридное: включает виртуальную сеть для локального доступа — это потребует hello использование Azure AD и в локальной среде Active Directory.

Не знаете, что выбрать? Прочитайте статью [Какой тип коллекции требуется для Azure RemoteApp](remoteapp-collections.md).

Этот учебник поможет выполнить процесс создания гибридной коллекции hello. Существует восемь шагов.

1. Решить, что [изображения](remoteapp-imageoptions.md) toouse для коллекции. Можно создать пользовательский образ или использовать одно из изображений Microsoft hello, включенными в вашу подписку.
2. Настройка виртуальной сети. Извлечение hello [планирование виртуальной сети](remoteapp-planvnet.md) и [изменения размера](remoteapp-vnetsizing.md) сведения.
3. Создание коллекции.
4. Соединение с локальным доменом tooyour вашей коллекции.
5. Добавьте набор tooyour образа шаблона.
6. Настройка синхронизации каталога. Azure RemoteApp требуется интегрировать Azure Active Directory, либо 1) Настройка синхронизации Azure Active Directory с hello параметр Синхронизация паролей или (2) Настройка синхронизации Azure Active Directory без параметра hello синхронизации паролей, но используется домен федеративные tooAD федерации Active Directory. Извлечение hello [сведения о конфигурации для службы Active Directory с RemoteApp](remoteapp-ad.md).
7. Публикация приложений RemoteApp.
8. Настройка доступа пользователей.

**Перед началом работы**

Необходимы следующие hello toodo перед созданием коллекции hello.

* [Зарегистрируйтесь](https://azure.microsoft.com/services/remoteapp/) в Azure RemoteApp.
* Создание учетной записи пользователя в Active Directory toouse как hello Azure RemoteApp учетной записи службы. Ограничения hello разрешения для этой учетной записи, таким образом, чтобы его можно только домену машины toohello.
* Соберите сведения о локальной сети, а именно получить информацию об IP-адресе и VPN-устройстве.
* Установка hello [Azure PowerShell](/powershell/azure/overview) модуля.
* Сбор сведений о пользователях hello, которым требуется доступ toogrant. Будет необходимо hello имя участника-пользователя Azure Active Directory (например, name@contoso.com) для каждого пользователя. Убедитесь в том, что hello, соответствует имени участника-пользователя между Azure AD и Active Directory.
* Выберите образ шаблона. Azure образ шаблона RemoteApp содержит hello приложений и программ, что требуется toopublish для пользователей. Дополнительные сведения см. в статье [Создание образа Azure RemoteApp](remoteapp-imageoptions.md).
* Требуется toouse hello Office 365 профессиональный плюс изображение? Ознакомьтесь с [этой информацией](remoteapp-officesubscription.md).
* [Настроить Active Directory для RemoteApp](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>Шаг 1. Настройка виртуальной сети
Вы можете развернуть гибридную коллекцию, которая использует существующую виртуальную сеть Azure, или создать новую виртуальную сеть. Виртуальная сеть позволяет пользователям получать доступ к данным в локальной сети через удаленные ресурсы RemoteApp. С помощью виртуальной сети Azure предоставляет вашей коллекции прямого сетевого доступа tooother служб Azure и развернуть виртуальные машины toothat виртуальной сети.

Обязательно изучите hello [планирование виртуальной сети](remoteapp-planvnet.md) и [размер виртуальной сети](remoteapp-vnetsizing.md) сведения перед созданием виртуальной сети.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Создание виртуальной сети Azure и присоедините его tooyour службы каталогов Active Directory
Сначала создайте [виртуальную сеть](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Это делается на hello **сети** hello портал Azure на вкладке. Необходимо tooconnect toohello вашей виртуальной сети развертывания Active Directory, синхронизированные tooyour клиента Azure Active Directory.

В разделе [создать виртуальную сеть с помощью портала Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) для получения дополнительной информации.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Убедитесь, что виртуальная сеть готова к использованию Azure RemoteApp
Перед созданием коллекции убедитесь, что ваша новая виртуальная сеть готова к работе. Это можно проверить, выполнив hello ниже:

1. Создание виртуальной машины Azure в подсети hello hello виртуальной сети, созданный для RemoteApp.
2. Используйте удаленный рабочий стол tooconnect toohello виртуальной машины. (Щелкните **Подключить**.)
3. Присоединиться к ней toohello же службы каталогов Active Directory, чтобы получить toouse RemoteApp.

Сработало? Ваша виртуальная сеть и подсеть готовы к использованию с Azure RemoteApp!

Можно найти дополнительные сведения о создании виртуальных машин Azure и подключение удаленного рабочего стола toothem [здесь](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Шаг 2. Создание коллекции Azure RemoteApp
1. В hello [портал Azure](http://manage.windowsazure.com), откройте страницу toohello Azure RemoteApp.
2. Щелкните **Создать > Создать с помощью VNet**.
3. Введите имя своей коллекции.
4. Выбор нужных toouse - стандартные или базовые плана hello.
5. Выберите hello раскрывающегося списка, а затем подсеть виртуальной сети.
6. Выберите toojoin его tooyour домена.
7. Щелкните **Создать коллекцию RemoteApp**.

После создания коллекции Azure RemoteApp, дважды щелкните имя hello hello коллекции. Появится hello **быстрый запуск** страница — это где завершения настройки коллекции hello.

Что-то пошло не так? Извлечение hello [гибридной коллекции, сведения об устранении неполадок](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-toohello-local-domain"></a>Шаг 3: Привязка к локальному домену toohello коллекции
1. На hello **быстрый запуск** щелкните **соединение с локальным доменом**.
2. Добавьте hello Azure RemoteApp домен учетной записи службы tooyour локальной Active Directory. Необходимо будет hello имя домена, подразделение, имя пользователя учетной записи службы и пароль.
   
    Это hello сведения, собранные, если вы следовали инструкциям hello [настроить Active Directory для Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>Шаг 4: Изображение Azure RemoteApp tooan ссылки
Azure образ шаблона RemoteApp содержит программы hello требуется tooshare с пользователями. Можно создать новый [образ шаблона](remoteapp-imageoptions.md) или ссылку tooan существующий образ (одно уже импортированы или переданные tooAzure RemoteApp). Кроме того, можно связать tooone из hello Azure RemoteApp [образы шаблонов](remoteapp-images.md) , содержащие Office 365 или Office 2013 (для пробного использования) программы.

Если вы отправляете hello новый образ, необходимо tooenter hello имя и выберите расположение hello для hello изображения. На следующей странице приветствия мастера hello вам увидеть набор командлетов PowerShell - копии и выполнить эти командлеты из с повышенными привилегиями Windows PowerShell prompt tooupload hello указанного образа.

При связывании tooan существующий образ шаблона, просто укажите имя образа hello, расположение и связанной подписки Azure.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Шаг 5. Настройка синхронизации каталога Active
Azure RemoteApp требуется интегрировать Azure Active Directory, либо 1) Настройка синхронизации Azure Active Directory с hello параметр Синхронизация паролей или (2) Настройка синхронизации Azure Active Directory без параметра hello синхронизации паролей, но используется домен федеративные tooAD федерации Active Directory.

Воспользуйтесь [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/). В этой статье описано, как настроить интеграцию каталогов за четыре шага.

Сведения о планировании и подробные действия см. в статье [Интеграция локальных удостоверений с Azure Active Directory](http://msdn.microsoft.com//library/azure/hh967642.aspx).

## <a name="step-6-publish-apps"></a>Шаг 6. Публикация приложений
Приложение Azure RemoteApp является приложение hello или предоставить пользователям tooyour программы. Он находится в образе шаблона hello, загруженный для hello коллекции. Когда пользователь обращается к приложению, он отображается toorun в своей локальной среде, но фактически выполняется в Azure.

Для доступа приложения, необходимо, чтобы toopublish их – это позволяет пользователям приложения hello доступ через клиент удаленного рабочего стола hello.

Можно опубликовать несколько приложений tooyour коллекции. На странице приветствия публикации нажмите **публикации** tooadd приложения. Можно либо опубликовать hello **запустить** меню hello образа шаблона или указав путь hello на hello образ шаблона для приложения hello. Если выбрать tooadd hello **запустить** меню, выберите tooadd программа hello. Если приложение toohello tooprovide hello пути, укажите имя для приложения hello и toowhere путь hello, установленному на образ шаблона hello.

## <a name="step-7-configure-user-access"></a>Шаг 7. Настройка доступа пользователей
После создания коллекции необходимо tooadd hello пользователям требуется доступ toouse toobe удаленных ресурсов. Пользователи Hello предоставляют доступ tooneed tooexist в клиент Active Directory hello связанных с подпиской hello используется toocreate коллекции Azure RemoteApp.

1. На странице быстрого запуска приветствия щелкните **настроить доступ пользователя**.
2. Введите hello рабочей учетной записи (из Active Directory) или учетной записи Майкрософт, которую требуется toogrant для.
   
   **Примечания.**
   
   Убедитесь, что используется hello  *user@domain.com*  формат.
   
   Если вы используете Office 365 профессиональный плюс в коллекции, необходимо использовать hello удостоверения Active Directory для пользователей. Это поможет проверять лицензирование.
3. После проверки пользователей hello щелкните **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
Вы успешно создали и развернули гибридную коллекцию Azure RemoteApp. Hello следующим шагом является toohave пользователей загрузить и установить клиент удаленного рабочего стола hello. Hello URL-адрес для hello клиента можно найти на странице быстрого запуска Azure RemoteApp hello. Затем у пользователей, входящих в клиент hello и получать доступ к приложениям hello публикации.

### <a name="help-us-help-you"></a>Помогите нам помочь вам
Знали ли вы, что в toorating сложения в этой статье и создания примечаний вниз ниже, можно внести самой статье toohello изменения? Чего-то не хватает? Что-то неправильно? Что-то изложено непонятно? Прокрутка вверх и нажмите кнопку **изменить на GitHub** изменения toomake - те поступит toous для просмотра и, когда мы выйдите из системы на них, вы увидите, изменения и усовершенствования здесь.

