---
title: "кластер aaaCreate Apache Spark в Azure HDInsight | Документы Microsoft"
description: "Примеры использования HDInsight Spark на как кластер toocreate Apache Spark в HDInsight."
keywords: "краткое руководство Spark,интерактивный запрос Spark,интерактивный запрос,Hdinsight Spark,Azure Spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>Создание кластера Apache Spark в Azure HDInsight

В этой статье вы узнаете, как кластер toocreate Apache Spark в Azure HDInsight. Сведения о Spark в HDInsight см. в [этой статье](hdinsight-apache-spark-overview.md).

   ![Краткое руководство схема, описывающая шаги toocreate кластера с Apache Spark на Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark начало работы с помощью Apache Spark в HDInsight. Описанные действия: создание кластера; выполнение интерактивного запроса Spark")

## <a name="prerequisites"></a>Предварительные требования

* **Подписка Azure**. Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure. Ознакомьтесь со страницей [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/free).

## <a name="create-hdinsight-spark-cluster"></a>Создание кластера HDInsight Spark

Следуя инструкциям из этого раздела, вы создадите кластер HDInsight Spark, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/). Другие способы создания кластера см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Щелкните hello следующий шаблон hello tooopen изображения в hello портал Azure.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Введите hello следующие значения:

    ![Создание кластера HDInsight Spark с использованием шаблона Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Создание кластера Spark в HDInsight с использованием шаблона Azure Resource Manager")

    * **Подписка.** Выберите свою подписку Azure для этого кластера.
    * **Группа ресурсов.** Создайте группу ресурсов или выберите существующую. Группы ресурсов — используется toomanage ресурсы Azure для проектов.
    * **Расположение**: выберите расположение для группы ресурсов hello. шаблон Hello использует это расположение для создания кластера hello также и для хранения данных кластера по умолчанию hello.
    * **Имя_кластера**: Введите имя кластера HDInsight hello, которое следует toocreate.
    * **Версия Spark**: выберите **2.0** hello версии, которые должны tooinstall на кластере hello.
    * **Имя входа и пароль кластера**: hello имя входа по умолчанию — admin.
    * **Имя пользователя SSH и пароль**.

   Запишите эти значения.  Они необходимы далее в учебнике hello.

3. Выберите **я принимаю условия, указанных выше, toohello**выберите **toodashboard ПИН-код**и нажмите кнопку **покупки**. Появится новый элемент под названием "Идет отправка развертывания для развертывания шаблона". Он принимает кластера hello toocreate около 20 минут.

Если возникли проблемы с создания кластеров HDInsight, возможно, у вас toodo hello нужные разрешения таким образом. Дополнительные сведения см. в разделе [Требования к контролю доступа](hdinsight-administer-use-portal-linux.md#create-clusters).

> [!NOTE]
> В этой статье создается кластер Spark, использующий [BLOB-объектов хранилища Azure как hello кластера хранилища](hdinsight-hadoop-use-blob-storage.md). Можно также создать кластер Spark, которая использует [хранилища Озера данных Azure](hdinsight-hadoop-use-data-lake-store.md) хранения по умолчанию hello. Инструкции см. в инструкциях по [созданию кластера HDInsight с Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>Выполнение запросов Hive с помощью Spark SQL

При использовании записной книжке Jupyter, настроенных для кластера HDInsight Spark, вы получаете стиль `sqlContext` , которые можно использовать запросы Hive toorun с помощью Spark SQL. В этом разделе вы узнаете, как toostart записной книжке Jupyter, а затем запустите базового запроса Hive.

1. Откройте hello [портал Azure](https://portal.azure.com/).

2. Если вы выбрали мониторинга toohello toopin hello кластера, щелкните плитку кластера hello из hello мониторинга toolaunch hello кластера колонки.

    Если не закрепить мониторинга toohello кластера hello hello левой панели, нажмите кнопку **кластеров HDInsight**и нажмите кнопку hello кластера, вы создали.

3. В разделе **Быстрые ссылки** щелкните **Панели мониторинга кластера**, а затем — **Записная книжка Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.

   ![Откройте Jupyter записной книжки toorun интерактивного Spark SQL-запроса](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "откройте Jupyter записной книжки toorun интерактивного Spark SQL-запроса")

   > [!NOTE]
   > Также может обращаться к записной книжки Jupyter hello для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Создайте записную книжку. Щелкните **Создать**, а затем выберите **PySpark**.

   ![Создать интерактивный запрос Spark SQL Jupyter записной книжки toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "создания Jupyter записной книжки toorun интерактивного Spark SQL-запроса")

   Создается и открывается с именем hello Untitled(Untitled.pynb) новый блокнот.

4. Щелкните имя записной книжки hello вверху hello и введите понятное имя, если требуется.

    ![Введите имя для hello Jupter записной книжки toorun интерактивных Spark запросов из](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "укажите имя для hello Jupter записной книжки toorun интерактивных Spark запросов из")

5.  Ниже hello вставить код в пустой ячейке и нажмите клавишу **SHIFT + ВВОД** toorun кода hello. В следующем примере кода hello `%%sql` (вызываемой hello sql magic) сообщает предустановку hello toouse записной книжки Jupyter `sqlContext` toorun запроса Hive hello. Hello запрос извлекает hello первые 10 строк из таблицы Hive (**hivesampletable**), доступное по умолчанию для всех кластеров HDInsight.

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![Запрос Hive в HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")

    Дополнительные сведения о hello `%%sql` magic и hello предустановленный набор контекстов см. в разделе [Jupyter ядер, доступных для кластера HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

    > [!NOTE]
    > Показывает каждый раз при выполнении запроса в Jupyter, заголовок окна обозревателя вашей веб **(Busy)** состояния вместе с hello записной книжки заголовка. Появится следующий toohello сплошной кружок **PySpark** текст в верхнем правом углу hello. По завершении задания hello изменяется tooa полый круг.
    >
    >
    
6. экран приветствия следует обновить результат запроса tooshow hello.

    ![Выходные данные запроса Hive в HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")

7. Завершение работы ресурсов кластера hello toorelease записной книжки hello, после завершения работы приложения hello. toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.

8. Если в дальнейшем планируется toocomplete hello дальнейшие действия, убедитесь, что удаление кластера HDInsight hello, созданный в этой статье. 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>Дальнейшие действия 

В этой статье вы узнали, как кластер HDInsight Spark toocreate и выполнения основных Spark SQL запроса. Переместить toohello toolearn далее в статье как кластер HDInsight Spark toouse toorun интерактивной обработки запросов на образце данных.

> [!div class="nextstepaction"]
>[Выполнение интерактивных запросов в кластере HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md)



