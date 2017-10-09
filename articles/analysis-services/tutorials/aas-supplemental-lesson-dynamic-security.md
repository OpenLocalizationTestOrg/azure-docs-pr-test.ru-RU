---
Заголовок: aaa» Azure Analysis Services tutorial дополнительного занятия: динамическая безопасность | Документы Microsoft» Описание: описание, как фильтры toouse динамической безопасности с помощью строки в учебнике hello Azure Analysis Services.
службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Дополнительное занятие. Динамическая безопасность

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

В этом дополнительном занятии вы создадите дополнительную роль, реализующую динамическую безопасность. Динамическая безопасность обеспечивает безопасность на уровне строк на основе hello пользователя имя или имя входа кода hello пользователя, вошедшего в систему. 
  
tooimplement динамической безопасности, добавьте модели tooyour таблицы, содержащей имена пользователей hello тех пользователей, которые могут подключаться toohello модели и просматривать объекты и модели данных. Hello модели, созданные с помощью этого учебника находится в контексте hello Adventure Works; Тем не менее, toocomplete это занятие, необходимо добавить таблицу, содержащую пользователей из собственного домена. Не обязательно hello пароли для hello имена пользователей, которые были добавлены. toocreate таблицу EmployeeSecurity с небольшой выборкой пользователей из собственного домена используется функция hello вставки данных из электронной таблицы Excel. В реальном сценарии hello таблицу, содержащую имена пользователей обычно можно привести таблицу из фактической базы данных в качестве источника данных; Например, реальную таблицу DimEmployee.  
  
tooimplement динамической безопасности, используйте две функции DAX: [функция USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) и [функция LOOKUPVALUE (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Такие функции, применяемые в формуле фильтра строк, определяются в новой роли. С помощью функции LOOKUPVALUE hello, формула hello указывает значение из таблицы EmployeeSecurity hello. Формула Hello затем передает, значение toohello USERNAME, функция, которая указывает имя пользователя hello hello пользователя, зарегистрированного в системе относится toothis роли. Hello пользователь может просматривать только данные, заданные hello фильтры строк. В этом случае укажите, что сотрудники отдела продаж могут просматривать только те данные Интернет-продаж для hello территорий продаж, в которых они являются членами.  
  
Таким образом определяются задачи, которые являются уникальными toothis сценария табличной модели Adventure Works, но они не обязательно tooa реальном сценарии. Каждое задание включает дополнительные сведения, описывающие цель hello задачу hello.  
  
Предполагаемое время toocomplete на этом занятии: **30 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Это дополнительное занятие входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello в этом дополнительном занятии, необходимо завершить все предыдущие занятия.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Добавить toohello таблицы DimSalesTerritory hello проекта табличной модели AW Internet Sales  
tooimplement динамической безопасности для этого сценария Adventure Works, необходимо добавить две модели tooyour дополнительных таблиц. Hello первой таблицы, добавляемого называется DimSalesTerritory (т Территория продаж) из hello одной базы данных AdventureWorksDW. Затем применять таблицы SalesTerritory toohello фильтр строк, которая определяет hello данных можно просмотреть hello, вошедшего в систему пользователя.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>таблицы DimSalesTerritory tooadd hello  
  
1.  В обозревателе табличных моделей выберите **Источники данных**, щелкните правой кнопкой мыши подключение и выберите элемент **Импортировать новые таблицы**.  

    Если появится диалоговое окно учетные данные олицетворения hello, введите учетные данные олицетворения hello, который использовался в занятии 2: Добавление данных.
  
2.  Выберите в навигаторе hello **DimSalesTerritory** , а затем выберите пункт **ОК**.    
  
3.  В редакторе запросов щелкните hello **DimSalesTerritory** запроса, а затем удалите **SalesTerritoryAlternateKey** столбца.  
  
7.  Щелкните **Импорт**.  
  
    область toohello модели добавляется новая таблица Hello. Затем объекты и данные из исходной таблицы DimSalesTerritory hello импортируются в табличной модели AW Internet Sales.  
  
9. После успешного импорта таблицы hello, нажмите кнопку **закрыть**.  

## <a name="add-a-table-with-user-name-data"></a>Добавление таблицы с именами пользователей  
Hello таблица DimEmployee в образце базы данных AdventureWorksDW hello содержит пользователей из домена AdventureWorks hello. Эти имена пользователей не существуют в вашей среде. Необходимо создать в модели таблицу, содержащую небольшую выборку данных фактических пользователей из вашей организации (по крайней мере трех). Затем добавьте этих пользователей как членов toohello новой роли. Нет необходимости hello пароли для имен пользователей образец hello, но вам нужен имена реальных пользователей Windows из собственного домена.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd EmployeeSecurity таблицы  
  
1.  Откройте Microsoft Excel и создайте лист.  
  
2.  Hello в следующей таблице, включая строку заголовка hello, скопируйте и вставьте его в лист hello.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Замените hello имя, фамилию и домен\имя_пользователя hello имена и идентификаторы входа трех пользователей в вашей организации. Поместите hello одного пользователя на первые две строки hello 1 EmployeeId, показывающая принадлежит этот пользователь toomore чем одной территории продаж. Оставьте hello EmployeeId и SalesTerritoryId поля, как они являются.  
  
4.  Сохраните лист hello как **SampleEmployee**.  
  
5.  На листе hello выделить все ячейки hello с данными о сотрудниках, включая заголовки hello, а затем щелкните правой кнопкой мыши выбранные hello данных и нажмите кнопку **копирования**.  
  
6.  В SSDT выберите hello **изменить** меню, а затем нажмите **вставить**.  
  
    Если вставить неактивен, щелкните любой столбец в любой таблице в окне конструктора моделей hello и повторите попытку.  
  
7.  В hello **Просмотр вставки** диалогового **имя таблицы**, тип **EmployeeSecurity**.  
  
8.  В **toobe данных вставить**, проверьте hello данные включают все данные пользователя hello и заголовки из листа SampleEmployee hello.  
  
9. Установите флажок **Использовать первую строку в качестве заголовков столбцов** и нажмите кнопку **ОК**.  
  
    Создается новую таблицу с именем EmployeeSecurity с данными о сотрудниках копируются из листа SampleEmployee hello.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Создание связей между таблицами FactInternetSales DimGeography и DimSalesTerritory  
Hello FactInternetSales DimGeography и DimSalesTerritory таблицы все имеют общий столбец, SalesTerritoryId. столбец SalesTerritoryId Hello таблицы DimSalesTerritory hello содержит значения с другим идентификатором для каждой территории продаж.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>toocreate связи между hello FactInternetSales DimGeography и таблицы DimSalesTerritory hello  
  
1.  В представлении диаграммы, в hello **DimGeography** таблицы, нажмите и удерживайте на hello **SalesTerritoryId** столбца, а затем перетащите hello курсор toohello **SalesTerritoryId** столбца в hello **DimSalesTerritory** таблицы, а затем отпустите.  
  
2.  В hello **FactInternetSales** таблицы, нажмите и удерживайте на hello **SalesTerritoryId** столбца, а затем перетащите hello курсор toohello **SalesTerritoryId** столбца в hello  **DimSalesTerritory** таблицы, а затем отпустите.  
  
    Обратите внимание hello активного свойства для этого отношения имеет значение False, это означает, что он неактивен. таблицы FactInternetSales Hello уже содержит другую активную связь.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Скрыть hello EmployeeSecurity таблицы от клиентских приложений  
В этой задаче вы скрыть таблицу EmployeeSecurity hello, поддерживая ее появления в списке полей клиентского приложения. Имейте в виду, что скрытие таблицы не повышает ее защищенность. Пользователи по-прежнему могут запрашивать данные из таблицы EmployeeSecurity, если они знают, как это сделать. toosecure Здравствуйте EmployeeSecurity данных таблицы, препятствующие пользователи могли tooquery какие-либо его данные, применить фильтр в одной из следующих задач.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>toohide hello EmployeeSecurity таблицы от клиентских приложений  
  
-   В конструкторе моделей hello в представлении диаграммы, щелкните правой кнопкой мыши hello **сотрудника** заголовок таблицы, а затем нажмите кнопку **скрыть от клиентских средств**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Создание роли пользователя "Торговые специалисты по территориям"  
В этой задаче вы создадите роль пользователя. Эта роль включает фильтр строк, определяющий, какие строки таблицы DimSalesTerritory hello являются видимыми toousers. Hello фильтр будет применен в отношении hello один ко многим другим направление tooall таблиц связанных tooDimSalesTerritory. Можно также применить фильтр, обеспечивающий безопасность всей таблицы EmployeeSecurity hello могли направлять к любой пользователь, который является членом роли hello.  
  
> [!NOTE]  
> Hello сотрудники отдела продаж по территории, создаваемая на этом занятии ограничивает элементы toobrowse (или запрос) только данные о продажах для hello toowhich территории продаж, которые они входят. При добавлении пользователя в качестве члена toohello сотрудники отдела продаж по территории, также существует как в роли для создания в [занятие 11: Создание ролей](../tutorials/aas-lesson-11-create-roles.md), вы получаете сочетание разрешений. Если пользователь входит в несколько ролей, разрешения hello и фильтров строк, определенными для каждой из них. То есть hello пользователем hello большими разрешениями, определяется hello комбинации ролей.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate сотрудники отдела продаж по территории роли пользователя  
  
1.  В SSDT выберите hello **модель** меню, а затем нажмите **ролей**.  
  
2.  В **диспетчере ролей** нажмите кнопку **Создать**.  
  
    Новая роль с hello None разрешение добавлен список toohello.  
  
3.  Щелкните новую роль hello, а затем в hello **имя** столбца, слишком переименовать роль hello**сотрудники отдела продаж по территории**.  
  
4.  В hello **разрешений** столбец, нажмите кнопку раскрывающегося списка hello, а затем выберите hello **чтения** разрешение.  
  
5.  Нажмите кнопку hello **элементы** , а затем щелкните **добавить**.  
  
6.  В hello **Выбор пользователя или группы** диалогового **ввод hello объекта с именем tooselect**, тип hello первый пример имя пользователя, используемое при создании таблицы EmployeeSecurity hello. Нажмите кнопку **проверить имена** tooverify hello пользователя имя является допустимым и нажмите кнопку **ОК**.  
  
    Повторите этот шаг, добавляя hello другие имена из выборки пользователей, используемые при создании таблицы EmployeeSecurity hello.  
  
7.  Нажмите кнопку hello **фильтры строк** вкладки.  
  
8.  Для hello **EmployeeSecurity** таблицы в hello **фильтр DAX** столбец, тип hello следующую формулу:  
  
    ```
      =FALSE()  
    ```
  
    Эта формула указывает, что все столбцы решаются toohello false логическое условие. Не указаны столбцы для таблицы EmployeeSecurity hello могут запрашиваться членом hello сотрудники отдела продаж по территории роли пользователя.  
  
9. Для hello **DimSalesTerritory** таблицы, тип hello следующую формулу:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    В этой формуле hello функция LOOKUPVALUE возвращает все значения для столбца [SalesTerritoryId] DimEmployeeSecurity hello, где hello EmployeeSecurity [LoginId] hello же, как hello текущего входа имя пользователя Windows и EmployeeSecurity [ SalesTerritoryId] hello аналогично hello DimSalesTerritory [SalesTerritoryId].  
  
    Hello набор идентификаторов территории продаж, возвращенные функцией LOOKUPVALUE будет использоваться toorestrict hello строк, отображаемых в hello таблицы DimSalesTerritory. Отображаются только строки, где hello SalesTerritoryID для hello строки в набор идентификаторов, возвращенных функцией LOOKUPVALUE hello hello.  
  
10. В диспетчере ролей нажмите кнопку **ОК**.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Тестирование hello сотрудники отдела продаж по территории роли пользователя  
В этой задаче вы используете hello анализ в Excel в SSDT tootest hello эффективность hello сотрудники отдела продаж по территории роли пользователя. Можно указать один приветствия имен пользователей добавлены toohello EmployeeSecurity таблицы и в качестве члена роли hello. Это имя пользователя затем используется как имя действующего пользователя hello в hello соединения, установленного между Excel и hello модели.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>hello tootest сотрудники отдела продаж по территории роли пользователя  
  
1.  В SSDT выберите hello **модель** меню, а затем нажмите **анализ в Excel**.  
  
2.  В hello **анализ в Excel** диалогового **укажите hello имя или роль toouse tooconnect toohello модели пользователя**выберите **другой пользователь Windows**и нажмите кнопку **Обзор**.  
  
3.  В hello **Выбор пользователя или группы** диалогового **введите имя tooselect hello объекта**, введите имя пользователя, включенные в таблице EmployeeSecurity hello и нажмите кнопку **проверить имена**.  
  
4.  Нажмите кнопку **ОК** tooclose hello **Выбор пользователя или группы** диалоговое окно, а затем щелкните **ОК** tooclose hello **анализ в Excel** диалоговое окно.  
  
    В Excel открывается новая книга. Автоматически создается сводная таблица. Hello список полей сводной таблицы включает большинство полей данных hello, доступные в новой модели.  
  
    Обратите внимание hello EmployeeSecurity таблица не отображается в списке полей сводной таблицы hello. Вы скрыли ее для клиентских средств в предыдущей задаче.  
  
5.  В hello **поля** в списке **∑ Интернет-продаж** (меры) выберите hello **InternetTotalSales** мер. мера Hello вводится в hello **значения** поля.  
  
6.  Выберите hello **SalesTerritoryId** столбец из hello **DimSalesTerritory** таблицы. столбец Hello вводится в hello **метки строк** поля.  
  
    Уведомление Internet цифры продаж появятся только для hello один регион toowhich hello действующего пользователя именем, которое принадлежит. Если выбрать другой столбец, как город из таблицы DimGeography hello поле метки строки, только города hello территории продаж toowhich hello действующего пользователя, принадлежащего отображаются.  
  
    Этот пользователь не может просмотреть или запросить данных Интернет-продаж для других hello один они принадлежат к территорий. Это ограничение обусловлено hello фильтр строк, определенных для таблицы DimSalesTerritory hello в hello сотрудники отдела продаж по территории роли пользователя, защищает данные для всех данных, связанных с tooother территорий продаж.  
  
## <a name="see-also"></a>См. также  
[Функция USERNAME (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[Функция LOOKUPVALUE (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[Функция CUSTOMDATA (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  