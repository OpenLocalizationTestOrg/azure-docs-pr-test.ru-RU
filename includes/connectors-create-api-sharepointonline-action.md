Теперь, когда вы добавили триггер, его время toodo интересные с данными hello, создаваемое hello триггера. Выполните эти шаги tooadd hello **SharePoint Online — создать файл** действие. Это действие создает файл в SharePoint Online каждый время hello новый элемент триггеров. 

Это действие hello tooconfigure, вы должны будете hello tooprovide следующую информацию. Можно предоставить эти сведения, можно заметить, что это данные легко toouse, создаваемые триггером hello как входные данные для некоторых свойств hello для hello новый файл:

| Свойство "Создание файла" | Описание |
| --- | --- |
| URL-адрес сайта |Это hello URL-адрес сайта SharePoint Online hello, где требуется toocreate hello новый файл. Выберите сайт hello из представления списка hello. |
| Путь к папке |Это является hello перейдите в папку (hello URL-адрес сайта, на предыдущем шаге hello), которую будет помещен новый файл hello. Найдите и выберите папку hello. |
| Имя файла |Это имя создаваемого файла hello hello. |
| содержимое файла; |Hello содержимое, которое будет записан файл toohello. |

1. Выберите **+ новый шаг** tooadd действие hello.  
   ![Действие SharePoint Online, изображение 1](./media/connectors-create-api-sharepointonline/action-1.png)  
2. Выберите hello **добавить действие** ссылку. Открывает окна поиска hello поиска для любого действия вы хотели бы tootake. В нашем случае это действия SharePoint.    
   ![Действие SharePoint Online, изображение 2](./media/connectors-create-api-sharepointonline/action-2.png)    
3. Введите *sharepoint* toosearch для tooSharePoint связанные действия.
4. Выберите **SharePoint Online — создать файл** как hello tootake действие.   **Примечание**: вы будет запрашиваемые tooauthorize вашей tooaccess логику приложения, учетной записи SharePoint, если вы еще не создали tooSharePoint подключения в сети.    
   ![Действие SharePoint Online, изображение 3](./media/connectors-create-api-sharepointonline/action-3.png)    
5. Hello **создать файл** управления откроется.   
   ![Действие SharePoint Online, изображение 4](./media/connectors-create-api-sharepointonline/action-4.png)     
6. Выберите **URL-адрес сайта** и обзор toofind hello сайта, куда toocreate hello файла.     
   ![Действие SharePoint Online, изображение 5](./media/connectors-create-api-sharepointonline/action-5.png)  
7. Выберите **путь к папке** и обзор toofind hello папки, которую будет помещен новый файл hello.  
   ![Действие SharePoint Online, изображение 6](./media/connectors-create-api-sharepointonline/action-6.png)  
8. Выберите hello **имя файла** управления и введите имя hello hello файла требуется toocreate. Здесь вы можете ввести имя файла hello непосредственно, или можно использовать любые свойства hello из hello триггер, созданный ранее. Это делается путем выбора из списка hello свойства **выходные данные при создании нового элемента**. Этот список является отображение только после выбора hello **имя файла** элемента управления. В этом walkthough я выбрал ID (идентификатор hello hello нового элемента списка), как имя hello hello файла, создаваемого hello **SharePoint Online — создать файл** действие.    
   ![Действие SharePoint Online, изображение 7](./media/connectors-create-api-sharepointonline/action-7.png)  
9. Выберите hello **содержимое файла** управления и введите hello содержимое, которое будет записан файл toohello, который будет создан. Содержимое файла hello Обратите внимание, можно использовать любые свойства hello из hello триггера, созданный ранее. Просто выберите свойства hello представлен список hello. Кроме того, можно ввести hello **содержимое файла** текст непосредственно в элемент управления hello. В этом примере я выбрал несколько свойств и добавил пробелы и дефис между ними.        
   ![Действие SharePoint Online, изображение 8](./media/connectors-create-api-sharepointonline/action-8.png)  
10. Сохранение рабочего процесса tooyour изменения hello  
11. Итак, теперь у вас есть приложение полностью функционален логики, которое запускается при добавлении нового элемента списка SharePoint Online tooa. приложение Hello создаст файл с помощью некоторых свойств hello из hello нового элемента списка.  Теперь можно проверить его, создав новый элемент в списке SharePoint hello. 

