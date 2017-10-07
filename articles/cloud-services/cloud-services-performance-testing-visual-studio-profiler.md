---
title: "Облачные службы локально в эмуляторе вычислений hello aaaProfiling | Документы Microsoft"
services: cloud-services
description: "Анализа проблем с производительностью в облачные службы с помощью профилировщика Visual Studio hello"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Тестирование производительности облачной службы локально hello в hello hello Azure эмуляторе вычислений с помощью профилировщика Visual Studio
Широкий набор средств и приемов доступны для тестирования производительности hello облачных служб.
При публикации облачной службы tooAzure, что Visual Studio сбора данных профилирования, а затем анализировать эти данные локально, как описано в [профилирование приложения Azure][1].
Можно также использовать tootrack диагностики производительности широкий набор счетчиков, как описано в [использование счетчиков производительности в Azure][2].
Можно также tooprofile перед его развертыванием toohello облачные приложения локально в эмуляторе вычислений hello.

В этой статье описан метод выборки циклов ЦП hello профилирования, это можно сделать локально в эмуляторе hello. Выборка из ЦП — это метод профилирования, который не сильно влияет на работу среды. С интервалом выборки указанный профилировщик hello делает моментальный снимок стека вызовов hello. Hello данные собираются за период времени и отображаемых в отчете. Этот метод профилирования обычно tooindicate, где в приложении с большим объемом вычислений большую часть работы hello ЦП, проводится.  Это дает hello toofocus возможных сделок на hello «Горячий путь», где приложение тратит hello большая часть времени.

## <a name="1-configure-visual-studio-for-profiling"></a>1. Настройка Visual Studio для профилирования
Во-первых, есть несколько параметров настройки Visual Studio, которые могут быть полезны при выполнении профилирования. Суть toomake Здравствуйте отчетов профилирования, вам потребуется символов (PDB-файлов) для вашего приложения, а также символы для системных библиотек. Будет необходимо убедиться, что ссылаться на серверы доступных символов hello toomake. toodo это на hello **средства** меню в Visual Studio выберите **параметры**, выберите **Отладка**, затем **символы**. Убедитесь, что в **Местоположение файла символов (PDB)**указаны серверы символов корпорации Майкрософт.  Также можно указать адрес http://referencesource.microsoft.com/symbols, который может содержать дополнительные файлы символов.

![Параметры "Символ"][4]

При желании можно упростить hello сообщает создает этот профилировщик hello, задав только мой код. Только мой код стеки вызовов функции упрощены, полностью внутренней toolibraries, которая вызывает и hello .NET Framework, скрыты от hello отчеты. На hello **средства** меню, выберите **параметры**. Разверните hello **средства повышения производительности** узел и выберите **Общие**. Установите флажок hello для **включить только мой код для отчетов профилировщика**.

![Параметры "Только мой код"][17]

Эти инструкции можно использовать как для нового, так и для существующего проекта.  При создании нового hello tootry проекта методик, описанных ниже, выберите C# **облачной службы Azure** проекта, а затем выберите **веб-роли** и **рабочей роли**.

![Роли проекта облачной службы Azure][5]

Например целей, добавить некоторые tooyour проекта кода, который занимает много времени и демонстрируются некоторые проблемы производительности очевидно. Например добавьте следующий проект рабочей роли код tooa hello:

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

Этот код можно вызовите из hello RunAsync метод класса, производного от RoleEntryPoint hello рабочей роли. (Не учитывать hello предупреждение о методе hello синхронное выполнение).

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Построение и запуск облачной службы локально без отладки (Ctrl + F5), задайте слишком конфигурации решения hello**выпуска**. Это гарантирует, что все файлы и папки создаются для выполнения приложения hello локально и гарантирует, что запущены все Привет эмуляторы. Запустите пользовательский Интерфейс эмулятора вычислений hello из tooverify hello задач, на котором выполняется рабочей роли.

## <a name="2-attach-tooa-process"></a>2: присоединение процесса tooa
Вместо профилирования приложения hello, запустите его из hello интерфейса IDE Visual Studio 2010, необходимо присоединить hello профилировщик tooa выполнения процесса. 

tooattach hello профилировщик tooa процесса на hello **анализ** меню, выберите **профилировщик** и **подключение/отключение**.

![Параметр "Присоединить профиль"][6]

Для рабочей роли найдите процесс WaWorkerHost.exe hello.

![Процесс WaWorkerHost][7]

Если вашей папки проекта находится на сетевом диске, профилировщик hello запросит tooprovide toosave hello другое расположение, отчеты профилирования.

 Можно также присоединить tooa веб-роли путем присоединения tooWaIISHost.exe.
Если существует несколько рабочих процессов для роли в приложении, необходимо toouse hello processID toodistinguish их. Вы можете запрашивать hello processID программным путем при доступе к объекту процесса hello. Например если добавить этот код toohello выполнения метод класса, производного от RoleEntryPoint hello в роли, можно взглянуть на журнала в пользовательский Интерфейс эмулятора вычислений tooknow hello какие tooconnect процесса для.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

Журнал tooview hello, hello начала пользовательский Интерфейс эмулятора вычислений.

![Запустить пользовательский Интерфейс эмулятора вычислений hello][8]

Откройте окно hello рабочей роли журнала консоли в hello пользовательский Интерфейс эмулятора вычислений, щелкнув на панели заголовка окна консоли hello. Вы увидите идентификатор процесса hello в журнале hello.

![Просмотр идентификатора процесса][9]

Который присоединен, выполните действия hello в сценарий hello tooreproduce приложения пользовательского интерфейса (при необходимости).

При необходимости toostop профилирования выберите hello **остановить профилирование** ссылку.

![Параметр "Остановить профилирование"][10]

## <a name="3-view-performance-reports"></a>3. Просмотр отчетов о производительности
отображается отчет о производительности Hello для вашего приложения.

На этом этапе hello профилировщик прекращает выполнение, сохраняет данные в VSP-файл и отображает отчет, показывающий анализ этих данных.

![Отчет профилировщика][11]

Если вы видите String.wstrcpy в hello критический путь, щелкнув только мой код toochange hello представление tooshow только код пользователя.  Если вы видите String.Concat, попробуйте нажав кнопку "Показать все код hello".

Вы увидите метод СЦЕПИТЬ hello и String.Concat занимают большую часть времени выполнения hello.

![Анализ отчета][12]

При добавлении кода объединения строку hello в этой статье вы увидите предупреждение в hello список задач для этого. Может также появиться предупреждение, что имеется слишком много мусора, которая наступает toohello число строк, которые создаются и удален.

![Предупреждения о производительности][14]

## <a name="4-make-changes-and-compare-performance"></a>4. Внесение изменений и сравнение производительности
Вы также можете сравнить производительность hello до и после изменения кода.  Остановить процесс hello и изменить hello кода tooreplace hello сцепление строк с использованием hello объекта StringBuilder:

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

Выполните запуск другой производительности, а затем сравнить производительность hello. В hello Обозреватель производительности, если hello запусков находятся в hello же сеансе, просто выберите оба отчета, откройте контекстное меню hello и выберите **Сравнить отчеты о производительности**. Toocompare с выполнения во время другого сеанса производительности, откройте hello **анализ** меню и выберите **Сравнить отчеты о производительности**. Укажите оба файла в диалоговом окне приветствия, отображается.

![Параметр "Сравнить отчеты о производительности"][15]

отчеты Hello подчеркивают различия между двумя выполнениями hello.

![Сравнительный отчет][16]

Поздравляем! Начала работы с профилировщиком hello.

## <a name="troubleshooting"></a>Устранение неполадок
* Убедитесь, что выполняется профилирование сборки для выпуска, и запустите без отладки.
* Если hello присоединение и отсоединение профилировщика меню hello не включена, запустите мастер производительности hello.
* Используйте пользовательский Интерфейс эмулятора вычислений hello tooview состояние hello приложения. 
* Если возникают проблемы при запуске приложения в эмуляторе hello или присоединение hello профилировщика, завершение работы эмулятора вычислений hello и перезапустите ее. Если это не устранит проблему hello, попробуйте перезагрузить. Это может происходить, если использовать эмулятор вычислений toosuspend hello и удалить выполняемых развертываниях.
* При использовании любого из hello профилирование команды из командной строки, особенно Здравствуйте глобальные параметры, убедитесь, что вызван VSPerfClrEnv/globaloff и что VsPerfMon.exe была завершена.
* Если при выборке данных, вы увидите сообщение hello» PRF0025: данные не собраны,» убедитесь, что процесс присоединенный toohas ЦП действие hello. Приложения, которые не производят вычислений, могут не предоставлять данных для выборки.  Можно также, hello процесс завершился до любой выборки, выполненной. Проверьте toosee, которые не прерывают hello метод Run для роли, которая выполняется профилирование.

## <a name="next-steps"></a>Дальнейшие действия
Инструментирование Azure двоичные файлы в эмуляторе hello в профилировщик Visual Studio hello не поддерживается, но если вы хотите tootest выделения памяти, можно выбрать этот параметр при профилировании. Вы также можете профилирования с параллелизмом, которая помогает определить, ли потоков тратит время конкурирующие за блокировки или профилирование уровневого взаимодействия, что помогает отслеживать проблемы с производительностью при взаимодействии между уровнями приложения, наиболее часто между уровнем данных hello и рабочей роли.  Могут просматривать hello запросы к базе данных, приложение создает и использовать hello профилирования данных tooimprove использование hello базы данных. Сведения о профилировании взаимодействия уровней см. в разделе hello записи блога [Пошаговое руководство: использование hello профилировщик уровня взаимодействия в Visual Studio Team System 2010][3].

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
