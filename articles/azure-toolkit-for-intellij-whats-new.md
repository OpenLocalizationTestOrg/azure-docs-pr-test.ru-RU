---
title: "Новые возможности набора средств Azure для IntelliJ | Документация Майкрософт"
description: "Сведения о новых функциях набора средств Azure для IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 23714856f0f778be04cf321e0726b53ade430f57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a>Новые возможности набора средств Azure для IntelliJ
## <a name="azure-toolkit-for-intellij-releases"></a>Выпуски набора средств Azure для IntelliJ
Эта статья содержит сведения о различных выпусках и последних обновлениях набора средств Azure для IntelliJ.

> [!NOTE]
> Также имеется набор средств Azure для интегрированной среды разработки Eclipse. Дополнительные сведения см. в разделе [Набор средств Azure для Eclipse].
> 
> 

### <a name="april-14-2017"></a>14 апреля 2017 г.
Набор средств Azure для IntelliJ, выпущенный в апреле 2017 года, включает следующие улучшения:

* **Улучшенная процедура входа Azure**: набор средств Azure для IntelliJ теперь поддерживает два метода входа в учетную запись Azure: *интерактивный* и *автоматический*. Дополнительные сведения см. в статье [Инструкции по входу для набора средств Azure для IntelliJ].
* **Публикация с помощью контейнеров Docker**: теперь с помощью набора средств Azure для IntelliJ веб-приложения можно публиковать в виде контейнеров Docker. Дополнительные сведения см. в статье [Публикация веб-приложения в виде контейнера Docker с помощью набора средств Azure для IntelliJ].
* **Управление учетными записями хранения**: набор средств Azure для IntelliJ теперь поддерживает управление учетными записями хранения из представления Azure Explorer. Дополнительные сведения см. в статье [Управление учетными записями хранения с помощью Azure Explorer для IntelliJ].
* **Управление виртуальными машинами**: набор средств Azure для IntelliJ теперь поддерживает управление виртуальными машинами из окна средства Azure Explorer. Дополнительные сведения см. в статье [Управление виртуальными машинами хранения с помощью Azure Explorer для IntelliJ].
* **Прекращение поддержки удаленной отладки**. Удаленная отладка для веб-приложений Java в службе приложений Azure была удалена из набора средств Azure для IntelliJ. Это потребовалось для устранения некоторых проблем, возникающих при работе с набором.

### <a name="august-26-2016"></a>26 августа 2016 г.
Набор средств Azure для IntelliJ, выпущенный в августе 2016 года, включает в себя следующие улучшения.

* **Пользовательские дистрибутивы JDK**. Набор средств Azure для IntelliJ теперь поддерживает указание и развертывание произвольной версии JDK в контейнере веб-приложений Azure.
  * В дополнение к версиям JDK, предоставляемым Azure, можно выбрать из обширного набора версий Zulu OpenJDK, которые доступны в Azure благодаря Azul Systems.
  * Можно также указать собственный дистрибутив JDK, если передать его как ZIP-файл в свою учетную запись хранения.
* **Усовершенствования в представлении Azure Explorer**.
  * Поддержка управления виртуальными машинами с помощью новой модели Resource Manager: можно выводить список, создавать и удалять виртуальные машины на основе Resource Manager, не выходя из интегрированной среды разработки.
  * Поддержка управления большими двоичными объектами учетной записи хранения с помощью Azure Resource Manager, который дополняет существующие функциональные возможности управления "классическими" учетными записями хранения.
* **Microsoft JDBC Driver 6.0 для SQL Server**. Это обновление включает в себя последнюю версию драйвера JDBC для Microsoft SQL Server (версии 6.0), включенную в виде библиотеки, которую можно легко добавить в свои проекты Java, заменив предыдущую версию.

### <a name="june-29-2016"></a>29 июня 2016 г.
Набор средств Azure для IntelliJ, выпущенный в июне 2016 г., включает в себя следующие улучшения.

* **Требование Java 8**. Набор средств Azure для IntelliJ теперь требует установки Java 8, однако это требование относится только к набору средств: приложения могут и дальше использовать все версии Java, поддерживаемые Azure.
* **Поддержка последних выпусков пакета SDK для Java (JDK)**. Набором средств Azure для IntelliJ теперь поддерживаются последние версии пакета SDK для Java (JDK).
* **Поддержка пакета SDK Azure версии 2.9.1**. Последняя версия пакета SDK Azure теперь является минимальным необходимым условием для установки набора средств Azure для IntelliJ.
* **Интегрированные примеры**. Набор средств Azure для IntelliJ теперь содержит несколько примеров приложений, помогающих разработчикам приступить к работе.
* **Интеграция средств HDInsight**. Средства HDInsight Azure теперь входят в набор средств Azure для IntelliJ. Дополнительные сведения см. в статье [Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания приложений Spark для кластера Spark в HDInsight на платформе Linux].
* **Удаленная отладка веб-приложений Java**. Набор средств Azure для IntelliJ теперь поддерживает удаленную отладку веб-приложений Java в службе приложений Azure.

### <a name="april-12-2016"></a>12 апреля 2016 г.
Набор средств Azure для IntelliJ, выпущенный в апреле 2016 года, включает следующие улучшения:

* **Поддержка пакета SDK Azure версии 2.9.0**. Последняя версия пакета SDK Azure теперь является минимальным необходимым условием для установки набора средств Azure для IntelliJ.
* **Различные улучшения удобства использования, скорости реагирования и производительности, связанные с поддержкой веб-приложений Azure**. Некоторая оптимизация взаимодействия набора средств с Azure привела к улучшению быстродействия пользовательского интерфейса.
* **Возможность удалить существующий контейнер веб-приложения в Azure из IntelliJ**. Набор средств Azure для IntelliJ теперь позволяет удалить существующий веб-контейнер Azure, не выходя из IntelliJ.

## <a name="see-also"></a>См. также
Дополнительные сведения о наборах средств Azure для Java IDE см. по следующим ссылкам:

* [Набор средств Azure для Eclipse]
  * [Новые возможности набора средств Azure для Eclipse]
  * [Установка набора средств Azure для Eclipse]
  * [Создание веб-приложения Hello World для Azure в Eclipse]
  * [Инструкции по входу для набора средств Azure для Eclipse]
* [Набор средств Azure для IntelliJ]
  * *Новые возможности набора средств Azure для IntelliJ (в этой статье)*
  * [Установка набора средств Azure для IntelliJ]
  * [Инструкции по входу для набора средств Azure для IntelliJ]
  * [Создание веб-приложения Hello World для Azure в IntelliJ]

Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Hello World для Azure в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Установка набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции по входу для набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Публикация веб-приложения в виде контейнера Docker с помощью набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Управление учетными записями хранения с помощью Azure Explorer для IntelliJ]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[Управление виртуальными машинами хранения с помощью Azure Explorer для IntelliJ]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Центре разработчиков Java для Azure]: http://go.microsoft.com/fwlink/?LinkID=699547

[Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания приложений Spark для кластера Spark в HDInsight на платформе Linux]: ./hdinsight/hdinsight-apache-spark-intellij-tool-plugin.md
