---
title: "aaaInstall собственными приложениями Hadoop в Azure HDInsight | Документы Microsoft"
description: "Узнайте, как приложения tooinstall HDInsight на HDInsight приложений."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Установка пользовательских приложений Hadoop в Azure HDInsight

В этой статье вы узнаете, как tooinstall приложении Hadoop в HDInsight Azure, который не был опубликован toohello портал Azure. приложение Hello установкой в этой статье [оттенка](http://gethue.com/).

Пользователи могут устанавливать приложения HDInsight в кластере HDInsight под управлением Linux.  Разработчиками этих приложений могут быть корпорация Майкрософт, независимые поставщики программного обеспечения или вы сами.  

Другие статьи по этой теме:

* [Установка приложений HDInsight](hdinsight-apps-install-applications.md): Узнайте, как кластеры tooinstall tooyour HDInsight приложения.
* [Публикация приложений HDInsight](hdinsight-apps-publish-applications.md): Узнайте, как toopublish вашего пользовательского tooAzure приложения Marketplace HDInsight.
* [MSDN: Установить приложение HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Узнайте, как toodefine HDInsight приложений.

## <a name="prerequisites"></a>Предварительные требования
Если требуется tooinstall HDInsight приложений в существующем кластере HDInsight необходимо иметь кластер HDInsight. разделе toocreate, [создавать кластеры](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Вы также можете установить приложения HDInsight во время создания кластера HDInsight.

## <a name="install-hdinsight-applications"></a>Установка приложений HDInsight
HDInsight приложения можно установить при создании кластера или tooan существующего кластера HDInsight. Инструкции по определению шаблонов Azure Resource Manager см. в статье [Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (Установка приложения HDInsight) на сайте MSDN.

Hello файлы, необходимые для развертывания этого приложения (цветовой тон):

* [azuredeploy.JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): hello шаблона диспетчера ресурсов для установки приложения HDInsight. Инструкции по разработке собственного шаблона Resource Manager см. в статье [Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (Установка приложения HDInsight) на сайте MSDN.
* [цветовой тон install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): hello действие скрипта, вызываемые hello шаблона диспетчера ресурсов для настройки hello граничного узла.
* [цветовой тон binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): hello оттенка двоичный файл вызывается из hui install_v0.sh.
* [цветовой тон двоичные файлы-14 04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): hello оттенка двоичный файл вызывается из hui install_v0.sh.
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz) — пример веб-приложения (Tomcat), вызываемый из hui-install_v0.sh.

**существующий кластер HDInsight tooinstall оттенка tooan**

1. Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портала Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Эта кнопка открывает шаблон диспетчера ресурсов, на основе hello портал Azure.  Hello шаблона диспетчера ресурсов находится в каталоге [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn как toowrite этого шаблона диспетчера ресурсов, в разделе [MSDN: установить приложение HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Из hello **параметры** колонке введите hello следующие данные:

   * **Имя_кластера**: Введите имя hello hello кластера, на котором требуется tooinstall приложения hello. Это должен быть существующий кластер.
3. Нажмите кнопку **ОК** toosave hello параметров.
4. Из hello **развертывания пользовательского** колонке введите **группы ресурсов**.  Группа ресурсов Hello является контейнером, который группирует hello кластера, учетной записи хранилища зависимых hello и другие ресурсы. Она необходима toouse hello же группе ресурсов кластера hello.
5. Щелкните **Условия использования**, а затем — кнопку **Создать**.
6. Проверьте hello **toodashboard ПИН-код** флажок установлен и нажмите кнопку **создать**. Можно просмотреть состояние установки hello с панели мониторинга портала закрепленных toohello hello плитки и уведомления на портале hello (щелкните значок колокольчика hello в верхней части hello hello портала).  Он принимает приложения hello tooinstall около 10 минут.

**tooinstall оттенка при создании кластера**

1. Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портала Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Эта кнопка открывает шаблон диспетчера ресурсов, на основе hello портал Azure.  Hello шаблона диспетчера ресурсов находится в каталоге [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn как toowrite этого шаблона диспетчера ресурсов, в разделе [MSDN: установить приложение HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Выполните hello инструкция toocreate кластер и установите цветовой тон. Дополнительные сведения о создании кластеров HDInsight см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

В дополнение к этому toohello портал Azure можно также использовать [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) и [Azure CLI](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall шаблоны диспетчера ресурсов.

## <a name="validate-hello-installation"></a>Проверка установки hello
Можно проверить состояние приложения hello на установку приложения hello Azure портала toovalidate hello. Кроме того если таковой имеется можно также проверить все поступивших конечных точек HTTP копирование надлежащим образом и веб-страницы приветствия:

**цветовой тон портала tooopen hello**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Нажмите кнопку **кластеров HDInsight** в левом меню hello.  Если меню не отображается, нажмите кнопку **Обзор**, а затем щелкните **Кластеры HDInsight**.
3. Щелкните кластер hello, где вы установили приложение hello.
4. Из hello **параметры** колонка, щелкните **приложений** под hello **Общие** категории. Вы увидите **оттенка** в hello **установленные приложения** колонку.
5. Нажмите кнопку **оттенка** из toolist hello hello списка свойств.  
6. Щелкните hello веб-странице ссылку toovalidate hello веб-сайт; Откройте hello HTTP конечной точки в браузере toovalidate hello оттенка веб-интерфейса, SSH Привет открыть конечную точку, с помощью SSH. См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="troubleshoot-hello-installation"></a>Устранение неполадок при установке hello
Можно проверить состояние установки приложения hello из портала уведомления hello (щелкните значок колокольчика hello в верхней части hello hello портала).

При сбое установки приложения, можно просматривать сообщения об ошибках hello и отладочную информацию из 3 мест:

* Приложения HDInsight: общие сведения об ошибке.

    Откройте hello кластера с портала hello и приложений из колонки hello параметры:

    ![приложения hdinsight приложение ошибка установки](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* Действие HDInsight сценария: Если сообщение об ошибке приложения HDInsight hello указывает на сбой действия сценария, Дополнительные сведения о сбое сценария hello, отображаются в области действия сценария hello.

    Щелкните действие скрипта из колонки параметры hello. Сообщения об ошибках hello показывает журнал действий скриптов

    ![приложения hdinsight ошибка действия сценария](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari Web пользовательского интерфейса: Если сценарий установки hello hello причину сбоя hello, используйте веб-интерфейса Ambari toocheck переполненные журналы о сценариях установки hello.

    Дополнительные сведения см. в разделе [Устранение неполадок](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

## <a name="remove-hdinsight-applications"></a>Удаление приложений HDInsight
Существует несколько способов toodelete HDInsight приложения.

### <a name="use-portal"></a>С помощью портала
**tooremove приложение с помощью портала hello**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Нажмите кнопку **кластеров HDInsight** в левом меню hello.  Если меню не отображается, нажмите кнопку **Обзор**, а затем щелкните **Кластеры HDInsight**.
3. Щелкните кластер hello, где вы установили приложение hello.
4. Из hello **параметры** колонка, щелкните **приложений** под hello **Общие** категории. Вы увидите список установленных приложений. В этом учебнике **оттенка** в hello **установленные приложения** колонку.
5. Щелкните правой кнопкой мыши приложение hello tooremove и нажмите кнопку **удалить**.
6. Нажмите кнопку **Да** tooconfirm.

Из портала hello можно также удалить кластер hello или удаления группы ресурсов hello, который содержит приложение hello.

### <a name="use-azure-powershell"></a>Использование Azure PowerShell
С помощью Azure PowerShell, можно удалить кластер hello или удаления группы ресурсов hello. Сведения об удалении кластеров с помощью Azure PowerShell см. [здесь](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Использование интерфейса командной строки Azure
С помощью Azure CLI, можно удалить кластер hello или удаления группы ресурсов hello. Сведения об удалении кластеров с помощью интерфейса командной строки Azure см. [здесь](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Дальнейшие действия
* [MSDN: Установить приложение HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Узнайте, как toodevelop шаблоны диспетчера ресурсов для развертывания приложений HDInsight.
* [Установка приложений HDInsight](hdinsight-apps-install-applications.md): Узнайте, как кластеры tooinstall tooyour HDInsight приложения.
* [Публикация приложений HDInsight](hdinsight-apps-publish-applications.md): Узнайте, как toopublish вашего пользовательского tooAzure приложения Marketplace HDInsight.
* [Настроить кластеры HDInsight под управлением Linux, с помощью сценария действия](hdinsight-hadoop-customize-cluster-linux.md): Узнайте, как toouse действие сценария tooinstall дополнительные приложения.
* [Создавать кластеры под управлением Linux Hadoop в HDInsight с помощью шаблонов диспетчера ресурсов](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Узнайте, как кластеры toocreate шаблонов диспетчера ресурсов toocall HDInsight.
* [Используйте пустой краевым узлам в HDInsight](hdinsight-apps-use-edge-node.md): Узнайте, как toouse пустой ребро узла для доступа к кластеру HDInsight, тестирование приложений HDInsight и размещение приложений HDInsight.
