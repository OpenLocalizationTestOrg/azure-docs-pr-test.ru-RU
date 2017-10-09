---
title: "aaaAuthor настраиваемые модули R в машинном обучении Azure | Документы Microsoft"
description: "Краткое руководство по созданию пользовательских R-модулей в Машинном обучении Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>Создание пользовательских R-модулей в Машинном обучении Azure
В этом разделе описывается способ tooauthor и развернуть пользовательские модули R в машинном обучении Azure. Он описывает сущность пользовательских R-модулей и файлы, используемые toodefine их. Он показывает, каким образом tooconstruct hello файлы, определяющие модуль и как tooregister hello модуль для развертывания в рабочей области машинного обучения. Hello элементы и атрибуты, используемые в определении hello пользовательского модуля hello затем описаны более подробно. Как также описана toouse вспомогательные функции и файлы и несколько выходов. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>Что такое пользовательский R-модуль?
Объект **пользовательский модуль** пользовательского модуля, который может быть переданы tooyour рабочей области и выполняется как часть эксперимента машинного обучения Azure. **Пользовательский R-модуль** представляет собой настраиваемый модуль, который выполняет определяемую пользователем R-функцию. **R** — это язык программирования, предназначенный для статистических вычислений и работы с графикой. Его широко используют специалисты по статистике, а также обработке и анализу данных для реализации алгоритмов. В настоящее время R — единственный языковой hello поддерживается в пользовательские модули, но поддержка для дополнительных языков запланирована для будущих версий.

Пользовательские модули имеют **состояние первого** в машинном обучении Azure в смысле hello, их можно использовать так же, как и любой другой модуль. Их можно выполнять с другими модулями, включенными в опубликованный эксперимент или визуализации. Контролировать алгоритм hello реализована модулем hello, hello используется toobe портов ввода-вывода, hello параметры моделирования и другие различные характеристики среды выполнения. Эксперимент, который содержит пользовательские модули могут быть опубликованы в коллекции Cortana аналитики hello упрощает совместное использование.

## <a name="files-in-a-custom-r-module"></a>Файлы в пользовательском R-модуле
Пользовательский R-модуль создается на основе ZIP-файла, содержащего как минимум два файла:

* Объект **исходный файл** , реализующий функции hello R, предоставляемыми hello модуля
* **XML-файл определения** , описывающий hello интерфейс пользовательского модуля

Также можно включить дополнительные вспомогательные файлы в ZIP-файл hello, предоставляет функции, которые доступны из пользовательского модуля hello. Эта возможность описана в hello **аргументы** частью hello справочном разделе **элементов в XML-файл определения hello** следующий пример hello краткое руководство.

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>Пример быстрого запуска: определение, создание пакета и регистрация пользовательского R-модуля
В этом примере показано, как tooconstruct hello файлы, необходимые пользовательский модуль R, упаковать их в ZIP-файл, а затем зарегистрировать модуль hello в рабочей области машинного обучения. Hello примере ZIP-пакета и образец файлы можно загрузить из [CustomAddRows.zip, загрузите файл](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).

## <a name="hello-source-file"></a>исходный файл Hello
Рассмотрим пример hello **Добавление строк настраиваемых** модуль, который изменяет стандартную реализацию hello hello **Добавление строк** модуль использовать tooconcatenate строк (наблюдений) из двух наборов данных (кадры данных). Стандартная Hello **Добавление строк** модуль добавляет строки hello hello второго входного набора данных toohello конца hello первого входного набора данных с помощью hello `rbind` алгоритма. настроить Hello `CustomAddRows` функция аналогично принимает два набора данных, а также принимает параметр логическое swap как дополнительный вход. Если параметр замены hello установлен слишком**FALSE**, он возвращает hello того же набора данных как hello стандартную реализацию. Но если параметр замены hello **TRUE**, функции hello добавляет строки из первого входного набора данных toohello конец hello второго набора данных, вместо этого. Hello CustomAddRows.R файл, который содержит реализацию hello hello R `CustomAddRows` из функций hello **Добавление строк настраиваемых** модуль имеет следующий код R hello.

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a>XML-файл определения Hello
tooexpose это `CustomAddRows` функции в качестве XML-файла определения модуля машинного обучения Azure, необходимо создать toospecify как hello **Добавление строк настраиваемых** модуля следует выглядят и работают так. 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


Это критическое toonote, hello значение hello **идентификатор** атрибуты hello **ввода** и **Arg** элементов в XML-файле hello должны совпадать имена параметров функции hello hello R Код файла CustomAddRows.R hello точно: (*dataset1*, *dataset2*, и *swap* в примере hello). Аналогичным образом hello значение hello **entryPoint** атрибут hello **язык** элемент должен полностью соответствовать hello имя функции hello в скрипте hello R: (*CustomAddRows* в примере hello). 

Здравствуйте, напротив, **идентификатор** атрибут для hello **вывода** элемента не соответствует tooany переменных в сценарии hello R. Если требуется несколько выходных данных, просто вернуть список из функции hello R с результатами разместить *в hello порядке* как **выходов** элементы, объявленные в XML-файле hello.

### <a name="package-and-register-hello-module"></a>Пакет и зарегистрировать модуль hello
Сохранить эти файлы как *CustomAddRows.R* и *CustomAddRows.xml* и затем zip вместе hello два файла в *CustomAddRows.zip* файла.

их в рабочей области машинного обучения, рабочей области перейдите tooyour в студии машинного обучения hello щелкните hello tooregister **+ создать** нижней hello и выберите команду **МОДУЛЯ -> из ZIP-ПАКЕТА** tooupload новый Hello **Добавление строк настраиваемых** модуля.

![Передача ZIP-файла](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

Hello **Добавление строк настраиваемых** модуль является теперь готовы toobe обращаются эксперименты машинного обучения.

## <a name="elements-in-hello-xml-definition-file"></a>Элементы в XML-файл определения hello
### <a name="module-elements"></a>Элементы «Модуль»
Hello **модуль** элемент является toodefine используется пользовательский модуль в XML-файле hello. С помощью нескольких элементов **модуль** в одном XML-файле можно определить несколько модулей. Каждый модуль в рабочей области должен иметь уникальное имя. Зарегистрировать пользовательский модуль hello одинаковые имена, как существующий пользовательский модуль, и он заменяет существующий модуль hello hello новый. Пользовательские модули, тем не менее, может быть зарегистрирована hello точно такое же имя в качестве существующего модуля машинного обучения Azure. Если таким образом, они отображаются в hello **настраиваемый** категории hello модуля палитры.

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


В рамках hello **модуль** элемента, можно указать два дополнительных необязательных элементов:

* **владельца** элемент, который внедряется в модуль hello  
* **описание** элемент, который содержит текст, отображающийся в экспресс-Справка для модуля "hello" и при наведении на модуль hello в hello интерфейса обучения.

Правила ограничения символов в элементах hello модуля:

* Здравствуйте, значение hello **имя** атрибута в hello **модуль** элемента не должна превышать 64 символов. 
* Здравствуйте, содержимое hello **описание** элемента не должна превышать 128 символов.
* Здравствуйте, содержимое hello **владельца** элемента не должна превышать 32 символов.

Результаты модуля могут быть детерминированными или nondeterministic.* * по умолчанию, все модули, считаются toobe детерминированной. Т. е если неизменяемый набор входных параметров и данных, модуль hello должен возвращать hello же результаты, eacRAND или functionh время запуска. Это поведение, студии машинного обучения Azure перезапустит только модули, которые помечены как детерминированную, если параметр или hello входные данные были изменены. Возврат результатов hello кэширования также предоставляет гораздо более быстрого выполнения экспериментов.

Нет функций, которые являются недетерминированными, таких как RAND или функцию, возвращающую hello текущей даты или времени. Если модуль использует недетерминированную функцию, можно указать модуля hello не является детерминированным, параметр hello необязательно **isDeterministic** атрибут слишком**FALSE**. Это гарантирует, что этот модуль hello запускается повторно при каждом запуске эксперимента hello, даже если hello входных данных модуля и параметры не были изменены. 

### <a name="language-definition"></a>Определение языка
Hello **языка** элемент в XML-файл определения — язык пользовательского модуля используется toospecify hello. В настоящее время R — hello поддерживается только язык. Здравствуйте, значение hello **sourceFile** атрибута должно быть именем hello hello R-файла, который содержит toocall функции hello при запуске модуля hello. Этот файл должен быть частью hello ZIP-пакета. Здравствуйте, значение hello **entryPoint** атрибут hello имя вызываемой функции hello и должно соответствовать является допустимой функцией, определенные в исходном файле hello.

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>порты;
Hello портов ввода-вывода для настраиваемого модуля указываются в дочерних элементов hello **порты** раздел XML-файла определения hello. Hello порядок этих элементов разметки hello опытным (UX) пользователями. первый дочерний элемент Hello **ввода** или **выходные данные** перечисленные в hello **порты** элемент hello XML-файла становится входного порта hello слева в hello UI машины обучения.
Каждый входной и выходной порт может иметь дополнительный **описание** дочерний элемент, который указывает текст hello, отображаемый при наведении курсора мыши hello порт hello в hello интерфейса обучения.

**Правила портов**:

* Максимальное число **портов входа и выхода** — по 8 для каждого.

### <a name="input-elements"></a>Входные элементы
Входные порты позволяют функция tooyour R toopass данных и рабочей области. Hello **типы данных** , которые поддерживаются для входных портов, как показано ниже: 

**DataTable:** этот тип передается функции tooyour R как data.frame. На самом деле, все типы (например, CSV-файлы или файлы ARFF), поддерживаемых машинного обучения, которые совместимы с **DataTable** , преобразованный tooa data.frame автоматически. 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

Hello **идентификатор** атрибутов, связанных с каждым **DataTable** входного порта должны иметь уникальное значение, и это значение должно соответствовать соответствующего именованного параметра в функции R.
Необязательный **DataTable** порты, которые не передаются в качестве входных данных в эксперимент имеют значение hello **NULL** функция переданный toohello R и порты необязательный zip учитываются, если входные данные hello не подключен. Hello **isOptional** атрибут является необязательным для обоих hello **DataTable** и **Zip** типы, а также является *false* по умолчанию.

**Zip** — пользовательские модули могут принимать в качестве входных данных ZIP-файл. Входные данные, распакованного в рабочий каталог hello R этой функции

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

Для пользовательских R-модулей идентификатор hello для порта Zip не иметь toomatch параметров функции hello R. Это происходит потому hello ZIP-файл является автоматически извлеченные toohello R рабочий каталог.

**Правила входных данных:**

* Здравствуйте, значение hello **идентификатор** атрибут hello **ввода** элемент должен быть допустимым именем переменной R.
* Здравствуйте, значение hello **идентификатор** атрибут hello **ввода** элемент должен быть не длиннее 64 символов.
* Здравствуйте, значение hello **имя** атрибут hello **ввода** элемент должен быть не длиннее 64 символов.
* Здравствуйте, содержимое hello **описание** элемент должен быть не длиннее 128 символов
* Здравствуйте, значение hello **тип** атрибут hello **ввода** элемент должен быть *ZIP-* или *DataTable*.
* Hello значение hello **isOptional** атрибут hello **входных данных** элемент не является обязательным (и *false* по умолчанию, если не указан); но если он указан, он должен быть *true* или *false*.

### <a name="output-elements"></a>Выходные элементы
**Стандартного вывода порты:** порты выходные данные, сопоставленные toohello возвращаемые значения функции R, который можно использовать в последующих модулях. *DataTable* — тип порта hello только стандартные выходные данные, в настоящее время поддерживается. (Ожидается поддержка *Learners* и *Transforms*.) Выходной объект *DataTable* определяется следующим образом:

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

Для выходных данных в пользовательских R-модулей hello значение hello **идентификатор** атрибут не имеет toocorrespond с ничего в скрипте hello R, но он должен быть уникальным. Для одного модуля выхода, должен быть hello возвращаемое значение функции hello R *data.frame*. В заказ toooutput более одного объекта поддерживаемый тип данных, порты hello соответствующие выходные данные должны toobe, указанный в XML-файл определения hello и hello объекты должны toobe возвращаются в виде списка. Hello выходных объектов назначаются toooutput порты из левой tooright, отражая hello порядок, в котором hello объекты размещаются в возвращаемый список hello.

Например, если вы хотите toomodify hello **Добавление строк настраиваемых** toooutput модуль hello исходного двух наборов данных, *dataset1* и *dataset2*, кроме присоединяется новый toohello набор данных, *набора данных*, (по порядку, от левой tooright как: *набора данных*, *dataset1*, *dataset2*), а затем определите hello выходных портов в файле CustomAddRows.xml hello следующим образом:

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


И возвращают список объектов hello в виде списка в правильном порядке hello в «CustomAddRows.R»:

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**Выходные данные визуализации:** можно также указать порт вывода типа *визуализации*, отображающего hello hello R графического устройства и консоли вывода. Этот порт не является частью выходные данные функции hello R и не влияет на порядок hello hello другие выходные типы портов. Добавьте визуализации порт toohello пользовательские модули, tooadd **выходные данные** элемент со значением *визуализации* для его **тип** атрибута:

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**Правила выходных данных:**

* Здравствуйте, значение hello **идентификатор** атрибут hello **вывода** элемент должен быть допустимым именем переменной R.
* Здравствуйте, значение hello **идентификатор** атрибут hello **выходные данные** элемент должен быть не более 32 символов.
* Здравствуйте, значение hello **имя** атрибут hello **вывода** элемент должен быть не длиннее 64 символов.
* Здравствуйте, значение hello **тип** атрибут hello **вывода** элемент должен быть *визуализации*.

### <a name="arguments"></a>Аргументы
Дополнительные данные могут передаваться функции toohello R через параметры модуля, которые определены в hello **аргументы** элемента. Эти параметры отображаются панели свойств справа hello hello интерфейса обучения при выборе модуля hello. Аргументы могут быть любого типа hello поддерживается, или можно создать пользовательские перечисления, при необходимости. Аналогичные toohello **порты** элементов, **аргументы** элементов может иметь дополнительный **описание** элемент, который задает hello текст, отображаемый при наведении указателя мыши hello через имя параметра hello.
Аргумент tooany как атрибуты tooa можно добавить дополнительные свойства для модуля, например defaultValue minValue и maxValue **свойства** элемента. Допустимые свойства для hello **свойства** элемента зависят от типа аргумента hello и описываются с типами аргументов hello поддерживается в следующем разделе hello. Аргументы, имеющие hello **isOptional** значение свойства слишком**«true»** tooenter пользователя hello значение не требуется. Если значение аргумента toohello не предоставлено, hello аргумент не передается toohello функцию точки входа. Аргументы функции точки входа hello, которые являются toobe необязательно должны явным образом обрабатываются функции hello, например назначить значение NULL по умолчанию в определении функции точки входа hello. Необязательный аргумент только будет обеспечивать hello ограничения других аргументов, т. е., min или max, если значение указано пользователем hello.
Как и для входных и выходных данных, очень важно, у каждого из параметров hello уникальный идентификатор значения, связанные с ними. Наши руководства по быстрому запуску был пример hello связанный идентификатор и параметра *swap*.

### <a name="arg-element"></a>Элемент Arg
Параметр модуля определяется с помощью hello **Arg** дочерний элемент элемента hello **аргументы** раздел XML-файла определения hello. Как и в случае с дочерними элементами hello в hello **порты** статьи, hello порядок параметров в hello **аргументы** раздел определяет макет hello в hello UI. Hello параметры отображаются сверху вниз в hello пользовательского интерфейса в hello же порядок, в котором они определены в XML-файле hello. Здесь перечислены Hello, поддерживаемым службами машинного обучения для параметров. 

**int** — параметр целочисленного типа (32-разрядная версия).

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *Необязательные свойства*: **min**, **max**, **default** и **isOptional**.

**double** — параметр типа double.

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *Необязательные свойства*: **min**, **max**, **default** и **isOptional**.

**bool** — логический параметр, который представлен в UX в виде флажка.

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *Необязательные свойства*: **по умолчанию** — значение false (если не задано).

**string**— стандартная строка

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *Необязательные свойства*: **default** и **isOptional**.

**ColumnPicker** — параметр выбора столбца. Этот тип готовится к просмотру в hello UX как выбор столбца. Hello **свойство** элемента — идентификатор hello используется здесь toospecify порт hello, из которой выбираются столбцы, где hello целевого типа порта должно быть *DataTable*. результат Hello выделенный фрагмент столбца hello передается функции toohello R как список строк, содержащих имена hello выбранных столбцов. 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *Требуемые свойства*: **portId** -совпадений hello идентификатор элемента входных данных с типом *DataTable*.
* *Необязательные свойства*:
  
  * **allowedTypes** -типы столбцов hello фильтры, из которого можно выбрать. Допустимые значения: 
    
    * Числовой
    * Логический
    * категориальные;
    * string
    * Метка
    * Функция
    * Оценка
    * Все
  * **по умолчанию** -варианты выбора по умолчанию для выбора столбцов hello включают: 
    
    * None
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * Все

**DropDown**— указанный пользователем пронумерованный (раскрывающийся) список. Hello раскрывающийся список элементов, заданных в hello **свойства** элемента с помощью **элемента** элемент. Hello **идентификатор** для каждого **элемент** должно быть уникальным и является допустимой переменной R. Здравствуйте, значение hello **имя** из **элемент** служит в качестве текста hello, вы видите и hello значению, переданному функции toohello R.

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *Необязательные свойства*:
  * **по умолчанию** - hello значение для свойства по умолчанию hello должен соответствовать со значением идентификатора из какого-либо hello **элемент** элементов.

### <a name="auxiliary-files"></a>Вспомогательные файлы
Любой файл, который помещается в ZIP-файл настраиваемого модуля является постоянной toobe доступны для использования во время выполнения. Вся структура каталогов сохраняется. Это означает, что работает считывания файла hello же локально и в выполнении машинного обучения Azure. 

> [!NOTE]
> Обратите внимание, что все файлы, извлеченные too'src "directory, чтобы все пути должны иметь ' src /" префикс.
> 
> 

Например предположим, требуется tooremove все строки, содержащие NAs из набора данных hello, а также удалить все повторяющиеся строки, перед выводом ее в CustomAddRows и уже написаны функцию R, который делает это в файле RemoveDupNARows.R:

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
Может получать вспомогательного файла hello RemoveDupNARows.R hello CustomAddRows функции:

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

Затем передать ZIP-файл, содержащий CustomAddRows.R, CustomAddRows.xml и RemoveDupNARows.R, в качестве пользовательского R-модуля.

## <a name="execution-environment"></a>Среда выполнения
Hello среды выполнения для скрипта hello R использует hello же версии R как hello **выполнение скрипта R** модуля и может использовать hello же пакетов по умолчанию. Можно также добавить дополнительные R пакеты tooyour пользовательского модуля, включая их в ZIP-пакет hello пользовательский модуль. Просто загрузите их в R-скрипт так же, как в среду R. 

**Ограничения для среды выполнения hello** включают:

* Временный файловая система: файлы, записанные при выполнении пользовательского модуля hello не сохраняются между несколькими запусками hello одного модуля.
* Нет доступа к сети

