---
title: "aaaSign в инструкции для средств Azure для Eclipse hello | Документы Microsoft"
description: "Узнайте, как toosign в Microsoft Azure с помощью hello средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Azure входа в инструкции для hello средств Azure для Eclipse

Hello средств Azure для Eclipse предоставляет два метода для входа в учетную запись Azure:

  * **Интерактивно** — при использовании этого метода потребуется вводить учетные данные Azure при каждом входе в учетную запись Azure.
  * **Автоматическое** — при использовании этого метода будет создан файл учетных данных, который содержит данные участника службы, после чего можно использовать файл tooautomatically hello учетные данные входа в учетную запись Azure.

Hello в следующих разделах hello будет описано, как toouse каждого метода.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Интерактивный вход в учетную запись Azure

Hello ниже будет показано, как toosign в Azure, вручную введя свои учетные данные Azure.

1. Откройте проект с помощью Eclipse.

1. Выберите **Сервис**, **Azure** и затем **Войти**.

   ![Меню Eclipse для входа в систему Azure][I01]

1. Здравствуйте, когда **входа в Azure** диалоговое окно, выберите **Interactive**и нажмите кнопку **входа**.

   ![Диалоговое окно входа][I02]

1. Здравствуйте, когда **журнала в Azure** диалоговое окно, введите свои учетные данные Azure и нажмите кнопку **входа**.

   ![Диалоговое окно входа в Azure][I03]

1. Здравствуйте, когда **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Выход из учетной записи Azure после интерактивного входа

После настройки hello действия в предыдущем разделе hello, будет выполнен автоматический выход из учетной записи Azure каждый раз, перезапустите Eclipse. Тем не менее toosign из учетной записи Azure без перезапуска Eclipse, используйте следующие шаги hello.

1. В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.

   ![Меню Eclipse для выхода из системы Azure][L01]

1. Здравствуйте, когда **выйти Azure** диалоговое окно, нажмите кнопку **Да**.

   ![Диалоговое окно выхода][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Автоматически войти в учетную запись Azure и создании учетных данных файла toouse в hello будущих

Hello ниже поможет вам выполнить создание файл учетных данных, который содержит данные участника службы. После выполнения этих действий, Eclipse будет автоматически использовать hello учетные данные файла tooautomatically входа вы в Azure каждый раз при откройте свой проект.

1. Откройте проект с помощью Eclipse.

1. Выберите **Сервис**, **Azure** и затем **Войти**.

   ![Меню Eclipse для входа в систему Azure][A01]

1. Здравствуйте, когда **входа в Azure** диалоговое окно, выберите **автоматизирован**и нажмите кнопку **New**.

   ![Диалоговое окно входа][A02]

1. Здравствуйте, когда **журнала в Azure** диалоговое окно, введите свои учетные данные Azure и нажмите кнопку **входа**.

   ![Диалоговое окно входа в Azure][A03]

1. Здравствуйте, когда **создать файлы для проверки подлинности** диалоговое окно, выберите hello подписки требуется toouse, выберите каталог назначения и нажмите кнопку **запустить**.

   ![Диалоговое окно входа в Azure][A04]

1. Hello **Creatation состояния субъекта-службы** отображается диалоговое окно, а после успешного создания файлов, нажмите кнопку **ОК**.

   ![Диалоговое окно состояния создания субъекта-службы][A05]

1. Здравствуйте, когда **входа в Azure** диалоговое окно, нажмите кнопку **входа**.

   ![Диалоговое окно входа в Azure][A06]

1. Здравствуйте, когда **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Выход из учетной записи Azure после автоматического входа

После настройки hello действия в предыдущем разделе hello hello набора средств Azure будет автоматически выполняться вход в учетную запись Azure каждый раз, перезапустите Eclipse. Тем не менее toosign со стороны вашей учетной записью Azure, а также запретить вход автоматически, hello используйте следующие шаги hello набора средств Azure.

1. В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.

   ![Меню Eclipse для выхода из системы Azure][L01]

1. Здравствуйте, когда **выйти Azure** диалоговое окно, нажмите кнопку **Да**.

   ![Диалоговое окно выхода][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Автоматический вход в учетную запись Azure с помощью созданного файла учетных данных

Если при использовании Eclipse, следует выйти из Azure, необходимо будет tooreconfigure hello набора средств Azure для Eclipse toouse файл учетных данных, в которой создана перед регистрацией автоматически в ваша Azure учетная запись. Hello следующее поможет настройка набора средств Azure toouse hello существующий файл учетных данных.

1. Откройте проект с помощью Eclipse.

1. Выберите **Сервис**, **Azure** и затем **Войти**.

   ![Меню Eclipse для входа в систему Azure][A01]

1. Здравствуйте, когда **входа в Azure** диалоговое окно, выберите **автоматизирован**и нажмите кнопку **Обзор**.

   ![Диалоговое окно входа][A02]

1. Здравствуйте, когда **выбрать файл с проверкой подлинности** диалоговое окно, выберите файл учетных данных, которая была создана ранее и нажмите кнопку **выберите**.

   ![Диалоговое окно входа][A08]

1. Здравствуйте, когда **входа в Azure** диалоговое окно, нажмите кнопку **входа**.

   ![Диалоговое окно входа в Azure][A06]

1. Здравствуйте, когда **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][A07]

## <a name="see-also"></a>См. также
Дополнительные сведения о hello наборы инструментов Azure для Java интегрированными средами разработки. в разделе hello ссылкам:

* [Набор средств Azure для Eclipse]
  * [Новые возможности средств Azure для Eclipse hello]
  * [Установка средств Azure для Eclipse hello]
  * *Вход в инструкции для hello средств Azure для Eclipse (Эта статья)*
  * [Создание веб-приложения Hello World для Azure в Eclipse]
* [Набор средств Azure для IntelliJ]
  * [Новые возможности средств Azure для IntelliJ hello]
  * [Установка hello Azure Toolkit для IntelliJ]
  * [Вход в инструкции для hello средств Azure для IntelliJ]
  * [Создание веб-приложения Hello World для Azure в IntelliJ]

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Hello World для Azure в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Вход в инструкции для hello средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
