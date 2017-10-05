---
title: "Установка набора средств Azure для Eclipse | Документация Майкрософт"
description: "Узнайте, как установить набор средств Azure для Eclipse."
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
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Установка набора средств Azure для Eclipse
В набор средств Azure для Eclipse входят шаблоны и функциональные возможности для простого создания, разработки, тестирования и развертывания приложений Azure с помощью среды разработки Eclipse. Набор средств Azure для Eclipse является проектом с открытым кодом. Исходный код доступен по лицензии MIT по адресу: <https://github.com/microsoft/azure-tools-for-java>.

Ниже приведен процесс установки набора средств Azure для Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Установка набора средств Azure для Eclipse
1. Запустите Eclipse.
2. Щелкните меню **Help** (Справка) и выберите пункт **Install New Software** (Установить новое программное обеспечение), как показано на следующем рисунке.
   
    ![Установка набора средств Azure для Eclipse][01]
3. В диалоговом окне **Available Software** (Доступное программное обеспечение) в текстовом поле **Work with** (Работа с) введите `http://dl.microsoft.com/eclipse` и нажмите клавишу **ВВОД**.
4. В области **Name** (Имя) установите флажок **Azure Toolkit for Eclipse** (Набор средств Azure для Eclipse) и снимите флажок **Contact all update sites during install to find required software** (Проверить все сайты обновления во время установки для поиска требуемого ПО). Экран должен выглядеть следующим образом:
   
    ![Установка набора средств Azure для Eclipse][02]
5. Если вы развернете узел **Azure Toolkit for Eclipse**(Набор средств Azure для Eclipse), то увидите следующие элементы:
   
   * **Application Insights Plugin for Java**(Подключаемый модуль Application Insights для Java) — этот компонент позволяет использовать службы регистрации и анализа телеметрии Azure для приложений и экземпляров серверов.
   * **Фильтр служб контроля доcтупа Azure**— этот компонент обеспечивает поддержку проверки подлинности пользователей приложения с помощью Azure ACS, используя сценарии единого входа и перемещая логику удостоверений из приложения.
   * **Общий подключаемый модуль Azure**— этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.
   * **Обозреватель Azure для Eclipse**— этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.
   * **Подключаемый модуль Azure для Eclipse с Java**— этот компонент обеспечивает поддержку проектов, помогающих собирать, тестировать и развертывать приложения Java для облака Microsoft Azure в Eclipse и с помощью командной строки.
   * **Подключаемый модуль веб- приложений Azure с Java**— этот компонент обеспечивает поддержку развертывания веб-приложений Java в контейнерах веб-приложений Microsoft Azure.
   * **Драйвер Microsoft JDBC 4.2 для SQL Server**— этот компонент предоставляет API JDBC для SQL Server и Базу данных SQL Microsoft Azure для платформы Java Enterprise Edition 8.
   * **Package for Apache Qpid Client Libraries for JMS**(Пакет для клиентских библиотек Apache Qpid для JMS) — этот компонент предоставляет клиентские компоненты JMS из проекта Apache Qpid, чтобы ваше приложение могло использовать обмен сообщениями на основе протокола AMQP в Azure.
   * **Пакет для библиотек Microsoft Azure для Java** — этот компонент предоставляет API для доступа к службам Microsoft Azure, таким как хранилище, служебная шина, среда выполнения службы и т. д.
6. Щелкните **Далее**. (Если при установке набора средств возникают необычные задержки, убедитесь, что снят флажок **Contact all update sites during install to find required software** [Проверить все сайты обновления во время установки для поиска требуемого ПО].)
7. В диалоговом окне **Install Details** (Сведения об установке) нажмите кнопку **Далее**.
   
    ![Просмотр сведений об установке][03]
8. В диалоговом окне **Review Licenses** (Просмотр лицензий) ознакомьтесь с условиями лицензионного соглашения. Если вы принимаете условия лицензионных соглашений, установите переключатель **I accept the terms of the license agreements** (Я принимаю условия лицензионных соглашений), а затем нажмите кнопку **Готово**. (В следующих действиях предполагается, что вы принимаете условия лицензионных соглашений. Если вы не принимаете эти условия, завершите процесс установки.)
   
    ![Review Licenses][04]
   
    Eclipse скачает и установит необходимые пакеты.
   
    ![Ход установки][05]
9. Если отображается запрос на перезапуск Eclipse для завершения установки, нажмите кнопку **Yes**(Да).
   
    ![Запрос перезапуска][06]

## <a name="see-also"></a>См. также
Дополнительные сведения о наборах средств Azure для Java IDE см. по следующим ссылкам:

* [Набор средств Azure для Eclipse]
  * [Новые возможности набора средств Azure для Eclipse]
  * *Установка набора средств Azure для Eclipse (в этой статье)*
  * [Инструкции по входу для набора средств Azure для Eclipse]
  * [Создание веб-приложения Hello World для Azure в Eclipse]
* [Набор средств Azure для IntelliJ]
  * [Новые возможности набора средств Azure для IntelliJ]
  * [Установка набора средств Azure для IntelliJ]
  * [Инструкции по входу для набора средств Azure для IntelliJ]
  * [Создание веб-приложения Hello World для Azure в IntelliJ]

Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Hello World для Azure в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Установка набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции по входу для набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
