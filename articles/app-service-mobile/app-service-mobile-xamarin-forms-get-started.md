---
title: "aaaGet работы с приложениями для мобильных устройств с помощью Xamarin.Forms"
description: "Выполните этот учебник toostart использование мобильных приложений для разработки Xamarin.Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Создание приложения Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как tooadd облачных служб tooa Xamarin.Forms мобильного приложения с помощью hello компонент службы приложения Azure в качестве серверной части hello мобильные приложения. Вы создадите новую серверную часть при помощи функции "Мобильные приложения" и простое приложение Xamarin.Forms для списка дел, в котором в Azure хранятся данные приложения.

Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными мобильным приложениям для приложений Xamarin.Forms.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие:

* Активная учетная запись Azure. При отсутствии учетной записи, можно зарегистрироваться в пробной версии Azure и получите бесплатные too10 мобильных приложений, которые вы можете продолжать использовать даже после окончания срока действия пробной версии никакие. Дополнительные сведения см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).

* Visual Studio с Xamarin. Сведения см. в разделе hello [задать Настройка и установка Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) страницы.

* Компьютер Mac с установленным ПО XCode версии 7.0 или выше и Xamarin Studio Community. Сведения см. в статьях о [настройке и установке](https://msdn.microsoft.com/library/mt613162.aspx) и [программе установки, установке и проверке для пользователей Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-a-new-mobile-apps-back-end"></a>Создание серверной части при помощи функции "Мобильные приложения"

toocreate завершить Mobile новых приложений, hello следующие:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Теперь при помощи функции "Мобильные приложения" мы настроили серверную часть, которую могут использовать ваши клиентские мобильные приложения. Затем загрузите серверный проект для серверную часть списка простые задачи и затем опубликовать его tooAzure.

## <a name="configure-hello-server-project"></a>Настройка проекта сервера hello

tooconfigure hello server project toouse hello серверной части, Node.js или .NET, hello следующие:

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>Загрузите и запустите решение Xamarin.Forms hello

Вы можете загрузить решение hello одним из двух способов. Загрузите его tooa Mac и откройте его в Xamarin Studio, или загрузить компьютер Windows tooa и открыть его в Visual Studio с помощью сетевых Mac для создания приложения iOS hello. Дополнительные ведения см. в статье о [настройке и установке](https://msdn.microsoft.com/library/mt613162.aspx).

На компьютере Mac или Windows hello следующие:

1. Go toohello [портал Azure].

2. На hello **параметры** колонку для мобильного приложения в разделе **Mobile**выберите **приступить к работе** > **Xamarin.Forms**. На **шаге 3** выберите **Создание нового приложения** и нажмите **Загрузить**.

   Это действие загружает проект, содержащий клиентское приложение, которое является подключенных tooyour мобильного приложения. Сохраните hello проекта сжатый файл tooyour локального компьютера и запишите где его сохранить.

3. Извлеките hello проекта, который вы загрузили и затем откройте в Visual Studio (Windows) или Xamarin Studio (Mac).

   ![Извлеченный проект в Xamarin Studio][9]

   ![Извлеченный проект в Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a>(Необязательно) Запустите проект iOS hello
В этом разделе вы запустите проект iOS hello Xamarin для устройств iOS. Пропустите этот раздел, если вы не работаете с устройствами iOS.

#### <a name="in-xamarin-studio"></a>В Xamarin Studio
1. Щелкните правой кнопкой мыши проект iOS hello, а затем выберите **Назначить запускаемым проектом**.

2. На hello **запуска** последовательно выберите пункты **начать отладку** toobuild hello проект и запустить приложение hello в эмуляторе iPhone hello.

#### <a name="in-visual-studio"></a>В Visual Studio
1. Щелкните правой кнопкой мыши проект iOS hello, а затем выберите **Назначить запускаемым проектом**.

2. На hello **построения** последовательно выберите пункты **Configuration Manager**.

3. В hello **Configuration Manager** диалоговое окно, выберите hello **построения** и **развернуть** проект iOS toohello Далее флажки.

4. toobuild hello проект и запустить приложение hello в эмуляторе iPhone hello, выберите hello **F5** ключа.

   > [!NOTE]
   > Если возникают проблемы при построении проекта hello, запустите hello NuGet пакета диспетчера и обновления toohello последнюю версию пакеты поддержки Xamarin hello. Примеры использования проектов может быть медленным tooupdate toohello последние версии.    
   >
   >

5. В приложение hello введите значимыми текстовыми, таких как *узнать Xamarin*, и затем выберите Здравствуйте, "плюс" (**+**).

    ![][10]

    Это действие отправляет toohello запрос post, новые мобильные приложения серверной части, который размещается в Azure. Данные из запроса hello вставляется в таблицу TodoItem hello. Данные отображаются в списке hello элементов, хранящихся в таблице hello возвращаются по hello заканчивается обратно мобильные приложения и hello.

    > [!NOTE]
    > Вы найдете hello код, который обращается к вашей серверной части мобильных приложений в hello TodoItemManager.cs C# файл hello проекта переносимой библиотеки классов для вашего решения.
    >
    >

## <a name="optional-run-hello-android-project"></a>(Необязательно) Запустите проект Android hello
В этом разделе выполняется hello Xamarin droid проекта для Android. Пропустите этот раздел, если вы не работаете с устройствами Android.

#### <a name="in-xamarin-studio"></a>В Xamarin Studio

1. Щелкните правой кнопкой мыши проект Android hello, а затем выберите **Назначить запускаемым проектом**.

2. toobuild hello проект и запустить приложение hello в эмуляторе Android, на hello **запуска** последовательно выберите пункты **начать отладку**.

#### <a name="in-visual-studio"></a>В Visual Studio

1. Щелкните правой кнопкой мыши проект Android (Droid) hello, а затем выберите **Назначить запускаемым проектом**.

2. На hello **построения** последовательно выберите пункты **Configuration Manager**.

3. В hello **Configuration Manager** диалоговое окно, выберите hello **построения** и **развернуть** флажки Далее toohello проекта для Android.

4. toobuild hello проект и запустить приложение hello в эмуляторе Android, выберите hello **F5** ключа.

   > [!NOTE]
   > Если возникают проблемы при построении проекта hello, запустите hello NuGet пакета диспетчера и обновления toohello последнюю версию пакеты поддержки Xamarin hello. Примеры использования проектов может быть медленным tooupdate toohello последние версии.    
   >
   >

5. В приложение hello введите значимыми текстовыми, таких как *узнать Xamarin*, и затем выберите Здравствуйте, "плюс" (**+**).

    ![][11]
    
    Это действие отправляет toohello запрос post, новые мобильные приложения серверной части, который размещается в Azure. Данные из запроса hello вставляется в таблицу TodoItem hello. Данные отображаются в списке hello элементов, хранящихся в таблице hello возвращаются по hello заканчивается обратно мобильные приложения и hello.
    
    > [!NOTE]
    > Вы найдете hello код, который обращается к вашей серверной части мобильных приложений в hello TodoItemManager.cs C# файл hello проекта переносимой библиотеки классов для вашего решения.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(Необязательно) Запустите проект Windows hello

В этом разделе выполняется hello Xamarin WinApp проекта для устройств Windows. Пропустите этот раздел, если вы не работаете с устройствами Windows.

#### <a name="in-visual-studio"></a>В Visual Studio

1. Щелкните правой кнопкой мыши проекты Windows hello, а затем выберите **Назначить запускаемым проектом**.

2. На hello **построения** последовательно выберите пункты **Configuration Manager**.

3. В hello **Configuration Manager** диалоговое окно, выберите hello **построения** и **развернуть** флажки Далее toohello проект Windows, выбранное.

4. toobuild hello проект и запустить приложение hello в эмуляторе Windows, выберите hello **F5** ключа.

   > [!NOTE]
   > Если возникают проблемы при построении проекта hello, запустите hello NuGet пакета диспетчера и обновления toohello последнюю версию пакеты поддержки Xamarin hello. Примеры использования проектов может быть медленным tooupdate toohello последние версии.    
   >
   >

5. В приложение hello введите значимыми текстовыми, таких как *узнать Xamarin*, и затем выберите Здравствуйте, "плюс" (**+**).

    Это действие отправляет toohello запрос post, новые мобильные приложения серверной части, который размещается в Azure. Данные из запроса hello вставляется в таблицу TodoItem hello. Данные отображаются в списке hello элементов, хранящихся в таблице hello возвращаются по hello заканчивается обратно мобильные приложения и hello.
    
    ![][12]
    
    > [!NOTE]
    > Вы найдете hello код, который обращается к вашей серверной части мобильных приложений в hello TodoItemManager.cs C# файл hello проекта переносимой библиотеки классов для вашего решения.
    >
    >

## <a name="next-steps"></a>Дальнейшие действия

* [Добавить приложение tooyour проверки подлинности](app-service-mobile-xamarin-forms-get-started-users.md)  
  Узнайте, как пользователи tooauthenticate приложения с поставщиком удостоверений.

* [Добавить приложение tooyour уведомлений push](app-service-mobile-xamarin-forms-get-started-push.md)  
  Узнайте, как push-уведомления tooadd поддерживают приложения tooyour и настройте ваши мобильные приложения серверной части toouse концентраторов уведомлений Azure toosend hello push-уведомления.

* [Включение автономной синхронизации для приложения](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Узнайте, как tooadd поддержке приложения с помощью мобильных приложений серверной части. Автономная синхронизация позволяет просматривать, добавлять или изменять данные мобильного приложения даже при отсутствии подключения к сети.

* [Использование hello управляемого клиента для мобильных приложений](app-service-mobile-dotnet-how-to-use-client-library.md)  
  Узнайте, как toowork с hello управление пакет SDK для клиента приложения Xamarin.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[портал Azure]: https://portal.azure.com/
