---
title: "aaaGet работает с приложениями Azure Mobile для приложений Xamarin.Android"
description: "Выполните этот учебник tooget работы с использованием мобильных приложений Azure для разработки Xamarin Android"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Создание приложения Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как tooadd облачную серверную службу tooa Xamarin.Android приложения. Дополнительные сведения см. в статье [Что такое мобильные приложения?](app-service-mobile-value-prop.md).

Снимок экрана из приложения hello завершения используется следующим образом:

![][0]

Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными мобильным приложениям для приложений Xamarin.Android.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие предварительные требования:

* Активная учетная запись Azure. При отсутствии учетной записи, зарегистрироваться для пробной версии Azure и приступить к too10 бесплатные приложения для мобильных устройств. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio с Xamarin. Инструкции см. в статье об [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).

## <a name="create-an-azure-mobile-app-backend"></a>Создание серверной части мобильного приложения Azure
Выполните эти шаги toocreate серверной мобильного приложения.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Итак, вы подготовили серверную часть мобильного Azure, которая может использоваться мобильными клиентскими приложениями. Затем загрузить проект сервера для простого «todo list» серверная часть и опубликовать его tooAzure.

## <a name="configure-hello-server-project"></a>Настройка проекта сервера hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Загрузите и запустите приложение Xamarin.Android hello
1. В разделе **загрузки и запуска проекта Xamarin.Android**, нажмите кнопку hello **загрузки** кнопки.

      Сохраните hello проекта сжатый файл tooyour локального компьютера и запишите где его сохранить.
2. Нажмите клавишу hello **F5** ключа toobuild hello проект и запустить приложение hello.
3. В приложение hello введите значимыми текстовыми, таких как *завершения hello учебника* и нажмите кнопку hello **добавить** кнопки.

    ![][10]

    Данные из запроса hello вставляется в таблицу TodoItem hello. Элементы, хранящиеся в таблице hello возвращаются сервером мобильного приложения hello, и данные в списке hello.

   > [!NOTE]
   > Можно просмотреть hello код, который обращается к tooquery серверной части вашего мобильного приложения и вставки данных, относящийся к hello файл ToDoActivity.cs C#.
   >
   >

## <a name="next-steps"></a>Дальнейшие действия
* [Добавить приложение tooyour автономной синхронизации](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Добавить приложение tooyour проверки подлинности](app-service-mobile-xamarin-android-get-started-users.md)
* [Добавить приложение Xamarin.Android tooyour уведомлений push](app-service-mobile-xamarin-android-get-started-push.md)
* [Управление toouse hello клиента для мобильных приложений Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
