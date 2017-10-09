
По умолчанию API-интерфейсы в серверной части мобильных приложений могут вызываться анонимно. Далее необходимо toorestrict tooonly проверку подлинности клиентов.  

* **Завершить node.js обратно (через hello портал Azure)** :  

    В разделе "Параметры" мобильных приложений щелкните **Простые таблицы** и выберите таблицу. Щелкните **Изменить разрешения**, выберите для всех разрешений параметр **Authenticated access only** (Доступ только с проверкой подлинности) и нажмите кнопку **Сохранить**.
* **Серверная часть .NET (C#):**  

    В проекте сервера hello, перейдите слишком**контроллеров** > **TodoItemController.cs**. Добавить hello `[Authorize]` атрибута toohello **TodoItemController** класса, как показано ниже. toorestrict доступ только toospecific методы, можно также применить этот метод просто toothose атрибута вместо класса hello. Повторная публикация проекта сервера hello.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Серверная служба Node.js (через код Node.js)** :  

    toorequire проверки подлинности для доступа к таблице, добавьте следующие строки toohello Node.js серверного скрипта hello:

        table.access = 'authenticated';

    Дополнительные сведения см. в разделе [как: требуется проверка подлинности для доступа к tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). toolearn проекта кода toodownload hello начало работы с веб-узла, в статье [как: загрузки hello Node.js серверной быстрый запуск проекта кода с помощью Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
