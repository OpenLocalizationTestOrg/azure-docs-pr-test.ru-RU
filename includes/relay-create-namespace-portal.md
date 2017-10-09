1. Войдите на toohello [портал Azure][Azure portal].
2. В области навигации слева hello hello портала щелкните **New**, нажмите кнопку **интеграцию**и нажмите кнопку **ретрансляции**.
3. В hello **создать пространство имен** диалоговое окно, введите имя пространства имен. система Hello немедленно проверяет toosee, доступно ли имя hello.
4. В hello **подписки** выберите подписку Azure в какие toocreate hello пространств имен.
5. В hello  **[группы ресурсов](../articles/azure-resource-manager/resource-group-portal.md)**  выберите существующую группу ресурсов в какой hello пространство имен будет live или создайте новую.      
6. В **расположение**, выберите hello страну или регион, в котором должна размещаться пространства имен.
   
    ![Создание пространства имен][create-namespace]
7. Щелкните **Создать**. система Hello теперь создает пространство имен и включает его. Через несколько минут hello система выделяет ресурсы для вашей учетной записи.

### <a name="obtain-hello-management-credentials"></a>Получить учетные данные управления hello
1. В списке hello пространств имен выберите hello созданное имя пространства имен.
2. В колонке приветствия имен щелкните **политики общего доступа**.
3. В hello **политики общего доступа** колонка, щелкните **RootManageSharedAccessKey**.
   
    ![Сведения о подключении][connection-info]
4. В hello **политики: RootManageSharedAccessKey** колонке нажмите кнопку "Копировать" hello Далее слишком**строка — первичный ключ подключения**, toocopy подключения hello строка буфера обмена tooyour для последующего использования. Вставьте на время эти значения в Блокноте или любом другом месте.
   
    ![Строка подключения][connection-string]

5. Повторите hello предыдущего шага, скопировав и вставив значение hello **первичного ключа** tooa временное расположение для дальнейшего использования.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
