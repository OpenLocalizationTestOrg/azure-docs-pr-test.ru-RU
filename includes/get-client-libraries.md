### <a name="install-via-composer"></a>Установка через компоновщик
1. [Установите Git][install-git]. Обратите внимание, что в Windows, необходимо также добавить переменную среды PATH исполняемый tooyour Git hello. 
2. Создайте файл с именем **composer.json** в hello корень проекта и добавьте следующий код tooit hello:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Скачайте **[composer.phar][composer-phar]** в корневой каталог проекта.
4. Откройте командную строку и выполните следующую команду в корневом каталоге проекта hello
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
