---
title: "приложение Java интенсивно aaaCompute на виртуальной Машине | Документы Microsoft"
description: "Узнайте, как можно отслеживать toocreate виртуальной машине Azure, работает под управлением приложения Java большим объемом вычислений, другое приложение Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>Как toorun интенсивных вычислительных задач на языке Java на виртуальной машине
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

С помощью Azure можно использовать задачи вычислений toohandle виртуальной машины. Например виртуальной машины можно управлять задачами и доставки результатов tooclient компьютеров или мобильных приложений. После считывания в этой статье, будет иметь представление о том, как можно отслеживать toocreate виртуальной машины, которая запускает приложение Java большим объемом вычислений, другое приложение Java.

В учебнике предполагается, что вы знаете, как можно импортировать приложение Java tooyour библиотеки toocreate Java консольные приложения и создавать архивом Java (JAR). Знания о платформе Microsoft Azure не требуются.

Вы узнаете:

* Как toocreate виртуальной машины с Java Development Kit (JDK) уже установлена.
* Каким образом tooremotely вход tooyour виртуальной машины.
* Как toocreate службы шины пространства имен.
* Как toocreate приложения Java, выполняющей задачу, большим объемом вычислений.
* Как toocreate приложение Java, которое отслеживает hello ход выполнения задачи hello вычислений.
* Как toorun hello приложений Java.
* Как toostop hello приложений Java.

Этого учебника будет использоваться hello коммивояжера hello ресурсоемких задач. Hello ниже приведен пример выполняемой hello Java приложения hello вычислений задачи.

![Средство поиска решения для задачи коммивояжера][solver_output]

Hello ниже приведен пример hello задача вычислений мониторинга hello приложений Java.

![Клиент задачи коммивояжера][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate виртуальной машины
1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Щелкните **Создать**, **Среда выполнения приложений**, **Виртуальная машина**, а затем — **Из коллекции**.
3. В hello **выберите образ виртуальной машины** выберите **JDK 7 Windows Server 2012**.
   Обратите внимание, что **JDK 6 Windows Server 2012** доступен, если у вас есть устаревшие приложения, которые еще не готовы toorun JDK 7.
4. Щелкните **Далее**.
5. В hello **конфигурации виртуальной машины** диалоговое окно:
   1. Укажите имя для виртуальной машины hello.
   2. Укажите hello toouse размер для виртуальной машины hello.
   3. Введите имя администратора hello в hello **имя пользователя** поля. Запомните этот пароль имя и hello рядом введенной, они будут использоваться при входе удаленно toohello виртуальной машины.
   4. Введите пароль в hello **новый пароль** и повторно введите его в hello **Подтверждение** поля. Это пароль учетной записи администратора hello.
   5. Щелкните **Далее**.
6. В hello Далее **конфигурации виртуальной машины** диалоговое окно:
   1. Для **облачная служба**, использовать значение по умолчанию hello **создать новую облачную службу**.
   2. Здравствуйте, значение для **DNS-имя облачной службы** должно быть уникальным среди cloudapp.net. При необходимости измените это значение, чтобы система Azure показывала его уникальность.
   3. Укажите регион, территориальную группу или виртуальную сеть. Для целей данного учебника укажите регион, например **США, запад**.
   4. В поле **Учетная запись хранения** выберите **Использовать автоматически созданную учетную запись хранения**.
   5. В разделе **Группа доступности** выберите **(Нет)**.
   6. Щелкните **Далее**.
7. В окончательной hello **конфигурации виртуальной машины** диалоговое окно:
   1. Примите записи конечной точки по умолчанию hello.
   2. Нажмите **Завершено**.

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>Журнал tooremotely tooyour виртуальной машине
1. Войдите на toohello [классический портал Azure](https://manage.windowsazure.com).
2. Нажмите **Виртуальные машины**.
3. Щелкните имя hello виртуальную машину, которую требуется toolog в hello.
4. Щелкните **Подключить**.
5. Принятия приглашения toohello необходимые tooconnect toohello виртуальной машины. Когда появится сообщение hello имя и пароль администратора, используйте значения hello, предоставленный при создании виртуальной машины hello.

Обратите внимание, что hello функциональность Azure Service Bus требует toobe сертификат Baltimore CyberTrust Root hello, устанавливаются как часть вашего JRE **cacerts** хранения. Этот сертификат автоматически включается в hello среда выполнения Java (JRE) используется в этом учебнике. Если у вас этот сертификат в вашей JRE **cacerts** хранения см. в разделе [Добавление toohello сертификат, в хранилище сертификатов ЦС Java] [ add_ca_cert] сведения о добавлении она (а также сведения о просмотре hello сертификаты в хранилище cacerts).

## <a name="how-toocreate-a-service-bus-namespace"></a>Как toocreate службы шины пространства имен
с помощью Service Bus toobegin очереди в Azure, необходимо сначала создать пространство имен службы. Это пространство имен службы предоставляет контейнер для адресации ресурсов служебной шины в вашем приложении.

toocreate пространства имен службы:

1. Войдите на toohello [классический портал Azure](https://manage.windowsazure.com).
2. В области навигации слева hello hello классический портал Azure, щелкните **шина обслуживания, управление доступом и кэширование**.
3. В области верхнего левого hello hello классический портал Azure, щелкните hello **Service Bus** узел и нажмите кнопку hello **New** кнопки.  
   ![Снимок экрана узла Service Bus][svc_bus_node]
4. В hello **создания нового пространства имен** диалогового окна введите **пространства имен**, и нажмите кнопку toomake убедиться, что он уникален, **Проверка доступности** кнопки.  
   ![Снимок экрана создания пространства имен][create_namespace]
5. Убедившись в том доступен hello пространства имен, выберите страну или регион, должны размещаться пространство имен и нажмите кнопку hello **создать пространство имен** кнопки.  
   
   пространство имен Hello, созданный появится в hello классический портал Azure и принимает tooactivate некоторое время. Подождите, пока состояние hello **Active** прежде чем переходить к следующему шагу hello.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Получить hello управления учетные данные по умолчанию для пространства имен hello
В операции управления tooperform заказа, например при создании очереди, для hello новое пространство имен необходимо иметь учетные данные управления hello tooobtain для пространства имен.

1. В области навигации слева hello щелкните hello **Service Bus** узел, чтобы отобразить список доступных пространств имен hello.
   ![Снимок экрана доступных пространств имен][avail_namespaces]
2. Выберите пространство имен hello, созданную из отображенного списка hello.
   ![Снимок экрана списка пространств имен][namespace_list]
3. Hello правом **свойства** области перечислены hello свойства для нового пространства имен.
   ![Снимок экрана панели свойств][properties_pane]
4. Hello **ключ по умолчанию** скрыт. Нажмите кнопку hello **представление** кнопку toodisplay учетные данные безопасности hello.
   ![Снимок экрана ключа по умолчанию][default_key]
5. Запишите hello **поставщика по умолчанию** и hello **ключ по умолчанию** как можно будет использовать эту информацию ниже tooperform операции с пространством имен.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>Как toocreate приложения Java, выполняющей задачу, большим объемом вычислений
1. На компьютере разработки (которая не поддерживает toobe hello виртуальную машину, созданную), hello загрузки [пакет Azure SDK для Java](https://azure.microsoft.com/develop/java/).
2. Создайте консольное приложение Java, используя hello пример кода в конце hello в этом разделе. В этом учебнике мы будем использовать **TSPSolver.java** имени файла hello Java. Изменение hello **вашей\_службы\_шины\_имен**, **вашей\_службы\_шины\_владельца**и **вашей\_службы\_шины\_ключ** toouse заполнители service bus **имен**, **поставщика по умолчанию** и  **Ключ по умолчанию** соответственно.
3. После программирования экспорта hello tooa запускаемых Java архива приложения (JAR) и пакета hello необходимые библиотеки в hello созданный JAR-ФАЙЛ. В этом учебнике мы будем использовать **TSPSolver.jar** как имя JAR-ФАЙЛ создан hello.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>Как toocreate приложение Java, которое отслеживает hello ход выполнения задачи hello вычислений
1. На компьютере разработки создайте консольное приложение Java с помощью hello пример кода в конце hello в этом разделе. В этом учебнике мы будем использовать **TSPClient.java** имени файла hello Java. Как показано выше, измените hello **вашей\_службы\_шины\_имен**, **вашей\_службы\_шины\_владельца**, и **вашей\_службы\_шины\_ключ** toouse заполнители service bus **имен**, **поставщика по умолчанию**и **ключ по умолчанию** соответственно.
2. Экспорт tooa приложения hello запускаемых JAR и hello пакета необходимые библиотеки в hello созданный JAR-ФАЙЛ. В этом учебнике мы будем использовать **TSPClient.jar** как имя JAR-ФАЙЛ создан hello.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>Как toorun hello приложений Java
Запустите приложение hello большим объемом вычислений, первый toocreate hello очереди, а затем toosolve hello проходящих Saleseman проблему, в который будет добавлять hello текущего лучший маршрут toohello очередь service bus. При hello вычислений оно работает (или после него), результаты выполнения hello клиента toodisplay hello очередь service bus.

### <a name="toorun-hello-compute-intensive-application"></a>toorun hello ресурсоемких приложений
1. Войдите в систему виртуальной машины tooyour.
2. Создайте папку, где будет выполняться приложение. Например, **c:\TSP**.
3. Копировать **TSPSolver.jar** слишком**c:\TSP**,
4. Создайте файл с именем **c:\TSP\cities.txt** с hello после содержимого.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. В командной строке измените каталоги tooc:\TSP.
6. Убедитесь, что папка bin hello JRE в переменной среды PATH hello.
7. Перед запуском hello TSP solver перестановок, вам потребуется очередь service bus toocreate hello. Выполнения hello следующая команда очередь service bus toocreate hello.
   
        java -jar TSPSolver.jar createqueue
8. Hello очередь создана, можно выполнить hello TSP solver перестановок. Например запустите hello, следующая команда toorun hello и поиск решения для 8 городов.
   
        java -jar TSPSolver.jar 8
   
   Если число не указано, выполняется поиск для 10 городов. Как hello нахождение текущего кратчайший маршруты, они будут добавлены toohello очереди.

> [!NOTE]
> Hello большего hello чисел, которое было задано, будет выполняться дольше hello solver hello. Например, поиск для 14 городов может занять несколько минут, а для 15 городов — несколько часов. Увеличение too16 или дополнительные города может привести к дней среды выполнения (в конечном счете недель, месяцев и лет). Это происходит из-за toohello быстрое увеличение hello число перестановок, поиска решения hello истинность города увеличения количества hello.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>Как toorun hello мониторинга клиентского приложения
1. Войдите в систему компьютера tooyour, где будет выполняться клиентское приложение hello. Это не обязательно toobe hello компьютере под управлением hello **TSPSolver** приложения, хотя он может быть.
2. Создайте папку, где будет выполняться приложение. Например, **c:\TSP**.
3. Копировать **TSPClient.jar** слишком**c:\TSP**,
4. Убедитесь, что папка bin hello JRE в переменной среды PATH hello.
5. В командной строке измените каталоги tooc:\TSP.
6. Выполните следующую команду hello.
   
        java -jar TSPClient.jar
   
    При необходимости укажите номер hello toosleep минут между проверки очереди hello, передавая аргумент командной строки. Hello период по умолчанию спящего режима проверки hello очереди — 3 минуты, который используется, если передается аргумент командной строки, не слишком**TSPClient**. Toouse другое значение для интервала hello спящего режима, например, одну минуту, запустите hello следующую команду.
   
        java -jar TSPClient.jar 1
   
    Hello клиента будет выполняться, пока очередь сообщений «Завершено». Обратите внимание, что при запуске несколько вхождений hello поиска решения без запуска клиента hello может потребовать toorun hello клиента очереди пустой hello toocompletely несколько раз. Кроме того можно удалить очередь hello и создайте его заново. очередь toodelete hello, запустите следующие hello **TSPSolver** (не **TSPClient**) команды.
   
        java -jar TSPSolver.jar deletequeue
   
    Поиск решения Hello будет выполняться, пока закончится ее выполнение проверки всех маршрутов.

## <a name="how-toostop-hello-java-applications"></a>Как toostop hello приложений Java
Для поиска решения hello и клиентских приложений, можно нажать клавишу **Ctrl + C** tooexit, если требуется завершения предыдущего toonormal tooend.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
