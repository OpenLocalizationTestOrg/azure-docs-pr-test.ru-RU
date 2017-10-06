---
title: "aaaSerialize данные в Hadoop - библиотеки Microsoft Avro - Azure | Документы Microsoft"
description: "Узнайте, как tooserialize и десериализовать данные в Hadoop в HDInsight с помощью toomemory toopersist hello библиотеку Microsoft Avro Library, базы данных или файла."
keywords: avro,hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>Сериализация данных в Hadoop с hello библиотеки Microsoft Avro

>[!NOTE]
>Hello Avro SDK больше не поддерживается корпорацией Майкрософт. Библиотека Hello является открытой поддерживается сообществом разработчиков. Hello источников для библиотеки hello расположены в [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

В этом разделе показано, как toouse hello [библиотеки Microsoft Avro](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize объектов и других данных структуры в потоки toopersist их toomemory, базы данных или файла. Здесь также показано, как toodeserialize их toorecover hello исходных объектов.

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
Hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">библиотеки Microsoft Avro</a> Здравствуйте, реализует систему сериализации данных Apache Avro для hello Microsoft.NET среды. Apache Avro обеспечивает компактный формат обмена двоичными данными для сериализации. Она использует <a href="http://www.json.org" target="_blank">JSON</a> toodefine от языка схемы, underwrites взаимодействие между языками. Данные, сериализованные в одном языке, могут быть прочитаны в другом. В настоящее время поддерживаются C, C++, C#, Java, PHP, Python и Ruby. Подробные сведения о формате hello можно найти в hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro спецификации</a>. 

>[!NOTE]
>Hello библиотеки Microsoft Avro поддерживает hello удаленной процедуры вызовы (RPC) часть данной спецификации.
>

представление Hello сериализации объекта в системе Avro hello состоит из двух частей: схемы и фактическое значение. схемы Avro Hello описывается модель данных зависит от языка программирования hello hello сериализации данных с JSON. Она представлена параллельно с двоичным представлением данных. Наличие отдельно от hello двоичное представление схемы hello разрешает toobe каждого объекта, записанных с затратами не-значение, делая сериализации быстрое и hello представление небольшой.

## <a name="hello-hadoop-scenario"></a>сценарий Hadoop Hello
формат сериализации Apache Avro Hello широко используется в других средах Apache Hadoop и Azure HDInsight. Avro предоставляет toorepresent удобный способ сложные структуры данных в задание Hadoop MapReduce. Hello формат файлов Avro (файл контейнера объекта Avro) был спроектированный toosupport hello распределенных MapReduce программной модели. ключевой особенностью Hello, включающий распределение hello является «разбить таблицу» в смысле hello, один поиска любой точки в файле и приступить к чтению из определенного блока hello файлы.

## <a name="serialization-in-avro-library"></a>Сериализация в библиотеке Avro
Hello библиотеки .NET для Avro поддерживает два способа сериализации объектов:

* **отражение** -hello схему JSON для типов hello автоматически строится на основе данных hello атрибуты контракта hello .NET типы toobe сериализации.
* **Универсальный записи** -схема JSON явно указан в записи, представленный hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) класса при типы .NET не существует схема hello toodescribe для toobe данных hello сериализовать.

Если схема данных hello известен tooboth hello записи и чтения потока hello, hello данных могут отправляться без его схемы. В случаях, когда используется файл Avro объекта контейнера, hello схема сохраняется в файле hello. Можно указать другие параметры, такие как hello кодек, использующийся для сжатия данных. Эти сценарии являются более подробно описано и показано в следующих примерах кода hello:

## <a name="install-avro-library"></a>Установка библиотеки Avro
требуются следующие Hello сертификаты, прежде чем устанавливать hello библиотеки:

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 или более поздней версии)

Обратите внимание, что hello зависимостей Newtonsoft.Json.dll автоматически загружается с установкой hello hello библиотеки Microsoft Avro. процедура Hello представлен в следующем разделе hello:

Hello библиотеку Microsoft Avro Library распространяется в виде пакета NuGet, который можно установить из Visual Studio через hello следующие процедуры:

1. Выберите hello **проекта** -> вкладка **управление пакетами NuGet...**
2. Поиск «Microsoft.Hadoop.Avro» в hello **поиск в Интернете** поле.
3. Нажмите кнопку hello **установить** рядом слишком**библиотеку Avro Microsoft Azure HDInsight**.

Обратите внимание, что hello Newtonsoft.Json.dll (> = 6.0.4) также зависимостей автоматически загружается с hello библиотеки Microsoft Avro.

Hello библиотеку Microsoft Avro Library исходный код доступен на [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

## <a name="compile-schemas-using-avro-library"></a>Компиляция схем с использованием библиотеки Avro
Hello библиотеку Microsoft Avro Library содержит создания кода, служебная программа, которая позволяет создавать типы C# автоматически на основании hello ранее определенные схемы JSON. Программа формирования кода Hello не поставляется как двоичный исполняемый файл, но можно легко создавать через hello после процедуры:

1. Загрузки hello ZIP-файла с последней версией hello HDInsight SDK исходного кода из <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK для Hadoop</a>. (Щелкните hello **загрузки** значок, не hello **загружает** вкладке.)
2. Извлеките hello каталог tooa HDInsight SDK на компьютере hello с .NET Framework 4 установлена и подключена toohello Интернет для загрузки пакетов NuGet необходимые зависимости. Ниже мы предполагаем, что hello исходный код находится извлеченный tooC:\SDK.
3. Перейдите в папку toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools и запустите build.bat. (hello файл вызовы MSBuild из 32-разрядных распределение hello hello .NET Framework. Если требуется 64-разрядная версия toouse hello редактировать build.bat, следуя hello комментарии в файле hello.) Убедитесь, что hello построение выполнено успешно. (В некоторых системах MSBuild может создавать предупреждения. Эти предупреждения не влияют на приветствия программы при условии, что отсутствуют ошибки построения.)
4. Служебная программа Hello компиляции находится в C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.

tooget знакомы с hello синтаксис командной строки, выполните следующую команду из папки hello, где находится служебная программа для создания кода hello hello:`Microsoft.Hadoop.Avro.Tools help /c:codegen`

Программа hello tootest, можно создать классов C# из hello образца JSON схемы файла с исходным кодом hello. Выполните следующую команду hello:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

Это должно tooproduce два файла C# в текущем каталоге hello: SensorData.cs и Location.cs.

toounderstand hello логику, которая использует программа создания кода hello при преобразовании типов tooC # hello JSON схемы, см. файл hello GenerationVerification.feature, расположенный в C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.

Пространства имен, извлекаются из схемы JSON hello, с помощью логики hello, описанных в файле hello, упомянутые в предыдущем абзаце hello. Пространства имен, извлеченных из схемы hello имеют приоритет над все, что входит в состав параметр /n hello в hello служебной программы командной строки. Если вы хотите hello toooverride пространства имен, содержащиеся в схеме hello, используйте параметр /nf hello. Например, toochange все пространства имен из hello SampleJSONSchema.avsc toomy.own.nspace, выполнить hello следующую команду:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>Об образцах hello
Шесть примеры, приведенные в этом разделе иллюстрируют различные сценарии, поддерживаемые hello библиотеки Microsoft Avro. Hello библиотеку Microsoft Avro Library — спроектированный toowork с любой поток. В этих примерах для простоты и последовательности управление данными осуществляется с использованием потоков в памяти, а не файловых потоков или баз данных. Hello подходов, использованных в рабочей среде зависит от требований конкретного сценария hello, источник данных и тома, ограничения производительности и других факторов.

Здравствуйте первый двух примерах показано, как tooserialize и десериализации данных в памяти буферы потока с помощью отражение и универсальные записей. Hello схемы в этих двух случаях предполагается toobe совместно hello средств чтения и записи по каналу.

Hello третья и четвертая примеры как tooserialize и десериализации данных с помощью объекта контейнера hello Avro файлов. Если данные хранятся в файле Avro контейнер, его схемы всегда хранится вместе с ним, поскольку hello схемы должны быть общими для десериализации.

Hello содержащий образец hello первые четыре примеры можно загрузить из hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">образцы кода Azure</a> сайта.

Hello пятый примере показан способ toouse кодек сжатия для Avro объекта контейнера файлов. Образец, содержащий код hello для в этом примере можно загрузить из hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">образцы кода Azure</a> сайта.

Hello шестой образце показано, как toouse Avro сериализации tooupload данных tooAzure хранилище больших двоичных объектов, а затем проанализировать его с помощью Hive кластера HDInsight (Hadoop). Ее можно загрузить из hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">образцы кода Azure</a> сайта.

Ниже приведены ссылки toohello шесть образцы, описанные в разделе hello.

* <a href="#Scenario1">**Сериализация с отражением** </a> -hello схему JSON для сериализации toobe типов автоматически строится на основе данных hello атрибутов контракта.
* <a href="#Scenario2">**Сериализации с помощью универсального записи** </a> -hello схемы JSON при задан явно в записи тип .NET, не доступны для отражения.
* <a href="#Scenario3">**Сериализации с помощью объекта контейнера файлов с отражением** </a> -схемы JSON hello автоматически создаваемый и общих вместе с данными сериализации hello через файл Avro объекта контейнера.
* <a href="#Scenario4">**Сериализации с помощью объекта контейнера файлов с записью универсального** </a> -схемы JSON hello явно задан перед выполнением сериализации hello и общих вместе с данными hello через файл Avro объекта контейнера.
* <a href="#Scenario5">**Сериализации с помощью объекта контейнера файлов с использованием кодека сжатия** </a> -hello примере показано, как toocreate Avro объектного файла контейнера с пользовательской реализации кодек сжатия данных Deflate hello .NET.
* <a href="#Scenario6">**Использование данных Avro tooupload hello службы Microsoft Azure HDInsight** </a> -пример hello иллюстрирует способ сериализации Avro взаимодействия с hello службы HDInsight. Активные Azure подписки и доступа tooan кластера Azure HDInsight требуется toorun в этом примере.

## <a name="Scenario1"></a>Пример 1. Сериализация с помощью отражения
Hello схему JSON для типов hello автоматически создается с hello библиотеку Microsoft Avro Library через отражение из данных hello атрибуты контракта hello C# объекты toobe сериализации. Hello библиотеку Microsoft Avro Library создает [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello поля toobe сериализации.

В этом примере объекты ( **SensorData** класса с членом **расположение** struct) являются tooa сериализованный поток памяти и в свою очередь десериализации данного потока. Hello результат равен то сравниваемых toohello исходный экземпляр tooconfirm, hello **SensorData** восстановить объект имеет одинаковые toohello исходного.

Схема Hello в этом примере предполагается, что toobe совместно hello средствами чтения и записи, поэтому формат контейнера объекта Avro hello не является обязательным. Пример того, как tooserialize и десериализации данных в буферы памяти с помощью отражения с форматом контейнера hello объекта при hello схемы должны быть общими данными hello, в разделе <a href="#Scenario3">сериализации с помощью объекта контейнера файлов с отражением</a>.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a>Пример 2. Сериализация с помощью универсальной записи
Схема JSON можно явно указать универсальный записи при отражения не может использоваться, поскольку hello данных не могут быть представлены через классы .NET с контрактом данных. Этот метод занимает больше времени, чем использование отражения. В таких случаях hello схему для данных hello также могут быть динамическим, то есть не известна во время компиляции. Данные представлены в виде значения с разделителями запятыми (CSV) файлы, схема остается неизвестным до его преобразования формата Avro toohello во время выполнения является примером такого рода динамический сценарий.

В этом примере показано, как toocreate и использовать [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly указания схемы JSON, как toopopulate его с данными hello, а затем как tooserialize и десериализацию. Hello результат затем сравнивается tooconfirm toohello исходный экземпляр, hello восстановить запись имеет идентичные toohello исходного.

Схема Hello в этом примере предполагается, что toobe совместно hello средствами чтения и записи, поэтому формат контейнера объекта Avro hello не является обязательным. Пример того, как tooserialize и десериализации данных в буферы памяти с помощью универсального записи с форматом контейнера hello объекта при hello схемы должен быть включен с hello сериализации данных, в разделе hello <a href="#Scenario4">сериализации с помощью объекта контейнера файлы с записью универсального</a> примере.

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>Пример 3. Сериализация с помощью файлов контейнеров объектов и сериализация с помощью отражения
Данный пример является похожее toohello в hello <a href="#Scenario1"> в первом примере</a>, где hello схемы неявно определяется с помощью отражения. Hello различие состоит в том, hello схемы не предполагается toobe известные toohello чтения, которое десериализует его. Hello **SensorData** сериализации toobe объекты и их неявно указанной схемы хранятся в файл контейнера Avro объекта, представленного hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) класс.

Hello данных сериализуется в этом примере с [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) и десериализации с [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). результат Hello то сравниваемых toohello начальных экземпляров tooensure удостоверений.

Hello данные в hello объекта сжатии контейнера по умолчанию hello [ **Deflate** ] [ deflate-100] кодек сжатия с .NET Framework 4. В разделе hello <a href="#Scenario5"> пятого примера</a> в этой статье toolearn как toouse более новую и более высокой версии hello [ **Deflate** ] [ deflate-110] сжатия кодек, доступных в .NET Framework 4.5.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>Пример 4. Сериализация с помощью файлов контейнеров объектов и сериализация с помощью универсальной записи
Данный пример является похожее toohello в hello <a href="#Scenario2"> во втором примере</a>, где явно указана схема hello с JSON. Hello различие состоит в том, hello схемы не предполагается toobe известные toohello чтения, которое десериализует его.

Hello проверочных данных собираются в список [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) объектов через явно определенной схемой JSON, а затем сохраняются в файл контейнера объекта, представленного hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) класса. Этот файл контейнер создает записи, — это данные, используемые tooserialize hello, несжатых данных, поток памяти tooa, затем сохраняется файл tooa. Hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) параметр, используемый для создания средства чтения hello указывает, что эти данные не сжимается.

Hello данных считывается из файла hello и десериализации в коллекции объектов. Эта коллекция является первоначальный список сравниваемых toohello tooconfirm записи Avro, что они совпадают.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>Пример 5. Сериализация с использованием файлов контейнеров объектов с помощью настраиваемого кодека сжатия
Hello пятый примере показан способ toouse кодек сжатия для Avro объекта контейнера файлов. Образец, содержащий код hello для в этом примере можно загрузить из hello [образцы кода Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) сайта.

Hello [спецификации Avro](http://avro.apache.org/docs/current/spec.html#Required+Codecs) разрешает использование кодек сжатия необязательно (кроме слишком**Null** и **Deflate** значения по умолчанию). В этом примере не реализует новый кодек, например Snappy (упоминается как поддерживаемые необязательные кодек в hello [Avro спецификации](http://avro.apache.org/docs/current/spec.html#snappy)). Здесь показано, как toouse hello реализация .NET Framework 4.5 hello [ **Deflate** ] [ deflate-110] кодека, который обеспечивает более эффективный алгоритм сжатия основании hello [zlib](http://zlib.net/) библиотеки сжатия, чем версия .NET Framework 4 hello по умолчанию.

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>Пример 6: Использование данных Avro tooupload для hello службы Microsoft Azure HDInsight
Hello шестой пример иллюстрирует некоторые программирования toointeracting связанные методы со службой Azure HDInsight hello. Образец, содержащий код hello для в этом примере можно загрузить из hello [образцы кода Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) сайта.

Образец Hello hello следующие задания:

* Подключается tooan существующий кластер службы HDInsight.
* Сериализует несколько CSV-файлы и отправляет хранилища больших двоичных объектов tooAzure результат hello. (hello CSV-файлы, распространяемые вместе с образец hello и представляют извлечения из AMEX Stock исторических данных, распределенных по [Infochimps](http://www.infochimps.com/) период hello 1970-2010. Образец Hello считывает данные CSV-файла, преобразует hello tooinstances записей из hello **Stock** класса, а затем выполняет сериализацию с помощью отражения. Определение типа биржевой создается на основе схемы JSON через hello программа создания кода библиотеки Microsoft Avro.
* Создает новую таблицу внешнего **акции** в кусте и связывает его toohello данные отправлены в предыдущем шаге hello.
* Выполняет запрос с использованием Hive через hello **акции** таблицы.

Кроме того образец hello выполняет процедуру очистки, до и после выполнения основных операций. Во время hello очистки все hello, связанные с удаляются данные больших двоичных объектов Azure и папки hello Hive таблица удаляется. Можно также вызвать процедуру очистки hello из командной строки образца hello.

Образец Hello имеет hello следующие предварительные требования:

* Активная подписка Microsoft Azure и ее идентификатор.
* Сертификат управления для подписки hello с hello соответствующего закрытого ключа. Hello сертификат должен быть установлен в hello текущего пользователя закрытого хранения на образце hello toorun компьютер, используемый hello.
* Активный кластер HDInsight.
* Учетная запись хранилища Azure связан toohello кластер HDInsight из предыдущего необходимым условием hello, вместе с hello соответствующего доступа первичного или вторичного ключа.

Перед запуском образца hello все сведения hello hello необходимых компонентов следует введенное toohello образец файла конфигурации. Существует два способа toodo его:

* Измените файл app.config hello в корневом каталоге образца hello и затем Постройте образец hello
* Сначала постройте образец hello, а затем измените AvroHDISample.exe.config в каталог сборки hello

В обоих случаях необходимо сделать все изменения в hello  **<appSettings>**  разделе "Параметры". Выполните hello комментарии в файле hello.
Hello пример запущен из командной строки hello, выполнив следующую команду (где hello ZIP-файл с примером hello признан tooC:\AvroHDISample toobe извлечь; Если в противном случае используйте hello соответствующий путь к файлу) hello:

    AvroHDISample run C:\AvroHDISample\Data

tooclean hello кластера, запустите hello следующую команду:

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
