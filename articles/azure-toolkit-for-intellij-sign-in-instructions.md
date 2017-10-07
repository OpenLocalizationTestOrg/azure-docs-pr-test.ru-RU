---
title: "aaaSign в инструкции для hello Azure Toolkit для IntelliJ | Документы Microsoft"
description: "Узнайте, как toosign в tooMicrosoft Azure с помощью hello Azure Toolkit для IntelliJ."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Вход инструкции для hello Azure Toolkit для IntelliJ

набор средств Azure для IntelliJ Hello предоставляет два метода для входа в учетную запись Azure tooyour:

  * **Интерактивный**: Введите учетные данные Azure при каждом входе в tooyour учетная запись Azure.
  * **Автоматическое**: Создание файла учетных данных, можно использовать tooautomatically входа в tooyour учетная запись Azure.

Hello ниже описано, как toouse каждого метода.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Интерактивного входа в учетную запись Azure tooyour

toosign в tooAzure, вручную введя свои учетные данные Azure hello следующие:

1. Откройте проект с помощью IntelliJ IDEA.

2. Нажмите кнопку **средства**, слишком точки**Azure**, а затем нажмите кнопку **входа в Azure**.

   ![Hello команда IntelliJ входа в Azure][I01]

3. В hello **входа в Azure** выберите **Interactive**, а затем нажмите кнопку **входа в**.

   ![Hello входа в Azure окно с выбранной Interactive][I02]

4. В hello **журнала в Azure** диалоговое окно, введите свои учетные данные Azure и нажмите кнопку **входа**.

   ![Hello Azure входа диалоговое окно][I03]

5. В hello **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.

   ![диалоговое окно Выбор подписки Hello][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Выход из учетной записи Azure после интерактивного входа

После настройки учетной записи с помощью hello в предыдущих шагах, будет автоматически выполнен из учетной записи Azure каждый раз при перезапуске IntelliJ ИДЕЯ. Тем не менее если вам нужны toosign учетной записью Azure *без* перезапуска ИДЕЯ IntelliJ hello следующие.

1. В ПОНЯТИЕ IntelliJ, hello **средства** меню точки слишком**Azure**и нажмите кнопку **выйти Azure**.

   ![Hello IntelliJ Azure входа с выходом-команда][L01]

2. В hello **выйти Azure** окне подтверждения нажмите кнопку **Да**.

   ![Hello Azure выйти окно подтверждения][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Автоматический вход tooyour учетная запись Azure

В этом разделе показано, как создать файл учетных данных, содержащий данные субъекта-службы. После завершения этого процесса Eclipse использует hello учетные данные файла tooautomatically выхода в tooAzure каждый раз при откройте свой проект.

1. Откройте проект с помощью IntelliJ IDEA.

2. На hello **средства** меню выберите пункт слишком**Azure**и нажмите кнопку **входа в Azure**.

   ![Hello команда IntelliJ входа в Azure][A01]

3. В hello **входа в Azure** выберите **автоматизирован**, а затем нажмите кнопку **New**.

   ![Вход в Azure окна Hello с выбран автоматический][A02]

4. В hello **диалоговое окно входа Azure** окно, введите свои учетные данные Azure и нажмите кнопку **входа**.

   ![Hello Azure входа диалоговое окно][A03]

5. В hello **создать файлы для проверки подлинности** окно, выберите hello подписки требуется toouse, выберите каталог назначения и нажмите кнопку **запустить**.

   ![Создание файлов для проверки подлинности окна Hello][A04]

6. В hello **состояние создания участника службы** диалоговое окно, после успешного создания файлов, нажмите кнопку **ОК**.

   ![диалоговое окно состояния создания участника службы Hello][A05]

7. В hello **входа в Azure** окно, нажмите кнопку **входа**.

   ![Диалоговое окно входа в Azure][A06]

8. В hello **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.

   ![диалоговое окно Выбор подписки Hello][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Выход из учетной записи Azure после автоматического входа

После настройки учетной записи с помощью предыдущих шагах hello hello набора средств Azure автоматически вход в tooyour при каждом перезапуске IntelliJ ИДЕЯ учетная запись Azure. Тем не менее, toosign со стороны вашей учетной записью Azure и предотвратить hello набора средств Azure из автоматического входа, hello следующие:

1. В ПОНЯТИЕ IntelliJ, hello **средства** меню точки слишком**Azure**и нажмите кнопку **выйти Azure**.

   ![Hello IntelliJ Azure входа с выходом-команда][L01]

2. В hello **выйти Azure** окне подтверждения нажмите кнопку **Да**.

   ![Hello Azure выйти окно подтверждения][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Автоматический вход в систему tooyour учетная запись Azure с помощью существующего файла учетных данных

Если при использовании IntelliJ ИДЕЯ, следует выйти из учетной записи Azure, необходимо использовать знак tooautomatically файл существующие учетные данные обратно в toohello учетной записи. hello tooconfigure набора средств Azure для Eclipse toouse существующий файл учетных данных, hello следующие:

1. Откройте проект с помощью IntelliJ IDEA.

2. На hello **средства** меню выберите пункт слишком**Azure**и нажмите кнопку **входа в Azure**.

   ![Hello команда IntelliJ входа в Azure][A01]

3. В hello **входа в Azure** выберите **автоматизирован**, а затем нажмите кнопку **Обзор**.

   ![Вход в Azure окна Hello с выбран автоматический][A02]

4. В hello **выберите файл проверки подлинности** диалоговое окно, выберите файл ранее созданные учетные данные и нажмите кнопку **выберите**.

   ![Выберите файл проверки подлинности Hello-диалоговое окно][A08]

5. В hello **входа в Azure** окно, нажмите кнопку **входа**.

   ![Вход в Azure окна Hello с выбран автоматический][A06]

6. В hello **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.

   ![диалоговое окно Выбор подписки Hello][A07]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello наборы инструментов Azure для Java интегрированными средами разработки. в разделе hello ссылкам:

* [Набор средств Azure для Eclipse]
  * [Новые возможности средств Azure для Eclipse hello]
  * [Установка средств Azure для Eclipse hello]
  * [Инструкции вход для hello средств Azure для Eclipse]
  * [Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]
* [Набор средств Azure для IntelliJ]
  * [Новые возможности средств Azure для IntelliJ hello]
  * [Установка hello Azure Toolkit для IntelliJ]
  * *Вход инструкции для hello Azure Toolkit для IntelliJ* (Эта статья)
  * [Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции вход для hello средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
