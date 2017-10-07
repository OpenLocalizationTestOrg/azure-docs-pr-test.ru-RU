---
title: "hello aaaInstalling средств Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как tooinstall hello средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6c195fab2b47fb5c42541a8cf52be4ec88d27b5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="installing-hello-azure-toolkit-for-eclipse"></a>Установка средств Azure для Eclipse hello
Hello средств Azure для Eclipse предоставляет шаблоны и функциональные возможности, которые позволяют вам tooeasily создавать, разрабатывать, тестировать и развертывать приложения Azure с помощью среды разработки Eclipse hello. Hello средств Azure для Eclipse является проекта с открытым кодом. Hello исходный код доступен по лицензии MIT hello из <https://github.com/microsoft/azure-tools-for-java>.

Привет, следующие шаги показывают, как tooinstall hello средств Azure для Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a>hello tooinstall средств Azure для Eclipse
1. Запустите Eclipse.
2. Нажмите кнопку hello **справки** меню, а затем нажмите **Установка нового программного обеспечения**, как показано в следующих рисунке hello.
   
    ![Установка средств Azure для Eclipse hello][01]
3. В hello **доступного программного обеспечения** диалоговое окно, в пределах hello **работать с** введите `http://dl.microsoft.com/eclipse` следуют hello **ввод** ключа.
4. В hello **имя** области проверьте **средств Azure для Eclipse**и снимите флажки **контакт все сайты обновлений во время установки программного обеспечения требуется toofind**. Экран должен выглядеть примерно toohello следующее:
   
    ![Установка средств Azure для Eclipse hello][02]
5. При разворачивании hello **средств Azure для Eclipse**, вы увидите hello следующих элементов:
   
   * **Подключаемый модуль Application Insights для Java**: этот компонент позволяет toouse Azure телеметрии ведения журнала и анализ службы для приложений и экземпляров серверов.
   * **Фильтр служб Azure Access-Control**: этот компонент обеспечивает поддержку проверки подлинности пользователей приложения в Azure ACS, Включение сценариев единого входа и вынесению логику приложения hello.
   * **Общий подключаемый модуль Azure**: этот компонент предоставляет общие функциональные возможности hello необходимости другими компонентами набора средств.
   * **Azure Explorer для Eclipse**: этот компонент предоставляет общие функциональные возможности hello необходимости другими компонентами набора средств.
   * **Подключаемый модуль Azure для Eclipse с Java**: этот компонент обеспечивает поддержку для разработки проектов, помогающие создания, тестирования и развертывания приложений Java для hello облако Microsoft Azure в Eclipse и с помощью командной строки.
   * **Подключаемый модуль приложения Azure Web с Java**: этот компонент обеспечивает поддержку для развертывания контейнеров Java web приложений tooMicrosoft веб-приложения Azure.
   * **Драйвер Microsoft JDBC 4.2 для SQL Server**— этот компонент предоставляет API JDBC для SQL Server и Базу данных SQL Microsoft Azure для платформы Java Enterprise Edition 8.
   * **Пакет для клиентских библиотек Apache Qpid для JMS**: этот компонент обеспечивает hello JMS клиентский компонент из tooenable проекта Apache Qpid hello приложения toouse AMQP обмена сообщениями в Microsoft Azure.
   * **Пакет для библиотек Microsoft Azure для Java** — этот компонент предоставляет API для доступа к службам Microsoft Azure, таким как хранилище, служебная шина, среда выполнения службы и т. д.
6. Щелкните **Далее**. (Если при установке hello набора средств возникают необычные задержки, убедитесь, что **контакт все сайты обновлений во время установки программного обеспечения требуется toofind** снят.)
7. В hello **сведения об установке** диалоговое окно, нажмите кнопку **Далее**.
   
    ![Просмотр сведений об установке][03]
8. В hello **Просмотр лицензий** диалогового окна, ознакомьтесь с условиями hello hello лицензионных соглашений. Если вы принимаете условия лицензионных соглашений hello hello, нажмите кнопку **я принимаю условия лицензионного соглашения hello hello** и нажмите кнопку **Готово**. (hello оставшихся шагах предполагается, что вы принимаете условия лицензионных соглашений hello hello. Если вы не принимаете условия лицензионных соглашений hello hello, выйти из процесса установки hello.)
   
    ![Review Licenses][04]
   
    Eclipse будет загрузить и установить необходимые пакеты hello.
   
    ![Ход установки][05]
9. Если запрос toorestart Eclipse toocomplete установки, нажмите кнопку **Да**.
   
    ![Запрос перезапуска][06]

## <a name="see-also"></a>См. также
Дополнительные сведения о hello наборы инструментов Azure для Java интегрированными средами разработки. в разделе hello ссылкам:

* [Набор средств Azure для Eclipse]
  * [Новые возможности средств Azure для Eclipse hello]
  * *Установка hello средств Azure для Eclipse (Эта статья)*
  * [Вход в инструкции для hello средств Azure для Eclipse]
  * [Создание веб-приложения Hello World для Azure в Eclipse]
* [Набор средств Azure для IntelliJ]
  * [Новые возможности средств Azure для IntelliJ hello]
  * [Установка hello Azure Toolkit для IntelliJ]
  * [Вход в инструкции для hello средств Azure для IntelliJ]
  * [Создание веб-приложения Hello World для Azure в IntelliJ]

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Hello World для Azure в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Вход в инструкции для hello средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Вход в инструкции для hello средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
