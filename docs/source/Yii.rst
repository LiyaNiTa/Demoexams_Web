Yii
===============

.. _Что такое Yii?:

Что такое Yii?
---------------

 .. note::
   Yii

Yii – это высокопроизводительный компонентный PHP фреймворк, предназначенный для
быстрой разработки современных веб-приложений.

 .. note::
   Особенности Yii

Как и многие другие PHP фреймворки, для организации кода Yii использует архитектурный
паттерн MVC (Model-View-Controller).
Yii придерживается философии простого и элегантного кода, не пытаясь усложнять
дизайн только ради следования каким-либо шаблонам проектирования.
Yii является full-stack фреймворком и включает в себя проверенные и хорошо
зарекомендовавшие себя возможности, такие как ActiveRecord для реляционных и NoSQL
баз данных, поддержку REST API, многоуровневое кэширование и другие.
Yii отлично расширяем. Вы можете настроить или заменить практически любую часть
основного кода. Используя архитектуру расширений, легко делиться кодом или
использовать код сообщества.
Одна из главных целей Yii – производительность.

 .. note::
   Что такое MVC?
 
Model View Controller (Модель-Представление-Контроллер) — схема разделения данных
приложения, и управляющей логики на три отдельных компонента:

- *модель*
- *представление*
- *контроллер* 

Эти компоненты представлены таким образом, что модификация каждого из них может осуществляться независимо

 .. note::
   Model

Логика манипулирования данными
Взаимодействия с БД (SELECT, INSERT, UPDATE, DELETE)
Предоставляет данные и реагирует на команды контроллера, изменяя свое состояние. В контексте обычного пониманя - это *база данных*.

 .. note::
   View

Представление - это шаблоны. Отвечает за отображение данных модели пользователю, реагируя на изменения модели
Обычно содержит HTML & CSS
Общается с контроллером
Используются шаблонизаторы

 .. note::
   Controller

Получает данные
Обрабатывает запросы
Получает данные из модели
Передает данные в представление

 .. note::
   Кроме MVC, Yii приложения также имеют следующие сущности:

- входные скрипты;
- приложения;
- компоненты приложения;
- модули;
- фильтры;
- виджеты.

.. image:: /_static/photo1714315124.jpeg
   :alt: mvc
   :width: 700

.. Установка и настройка:

Установка и настройка
-----------------------

Скачиваем архив с официального сайта https://www.yiiframework.com/download и распаковываем в папку /opt/lampp/htdocs Папке передаем права для редактирования

.. code-block:: console

   $ chmod -R 777 htdocs/

.. image:: /_static/yii.png
   :alt: yii
   :width: 700

Далее открываем папку через Visual Studio Code

.. image:: /_static/vsCode.png
   :alt: vsCode
   :width: 700

В браузере переходим по ссылке http://localhost/web/ на что выдает следующую ошибку (не забудьте запустить XAMPP)

.. image:: /_static/ошибка.png
   :alt: ошибка
   :width: 700

Это значит, что не указан cookieValidationKey в файле /opt/lampp/htdocs/config/web.php Также может возникать ошибка: The directory is not writable by the Web process: /opt/lampp/htdocs/web/assets
В этом случае просто снимаем защиту с папки командой

.. code-block:: console

   $ chmod 777 lampp/htdocs/web/assets

.. image:: /_static/уи_установлен.png
   :alt: уи_установлен
   :width: 700

Далее проверяем подключение к бд, указав правильное имя базы

.. image:: /_static/db.png
   :alt: db
   :width: 700

Настройка адресации: уберем необходимость вводить в путь сайта слово web. Для этого скопируем файл /opt/lampp/htdocs/web/.htaccess в папку /opt/lampp/htdocs и пропишем регулярное выражение

.. code-block:: HTML

   RewriteEngine on
   RewriteRule ^(.+)?$ /web/$1

.. image:: /_static/Настройка_адресации.png
   :alt: Настройка_адресации
   :width: 700

Добавим строку 'baseUrl' => '', и раскомментируем urlManager для правильной работы переходов по страницам

.. image:: /_static/adress.png
   :alt: adress
   :width: 700

Следующим этапом переходим в конфигурационные файлы и проводим настройу в них. 
ВАЖНО! Конфигурационные файлы находятся по адресу: /opt/lampp/htdocs/config

Вносим следующие изенения в файл web.php  *'language' => 'ru-RU',* - добавляем в первый блок кода после $config = [ *'id' => 'basic',* - это позволит нам перевести валидацию на русский язык.

Работа с gii
---------------

Затем необходимо разкомментировать последнюю строчку блока кода содержащего информацию о *gii*    **'allowedIPs' => ['*'],**. чтобы перейти на страницу кола gii, нужно в браузер ввести следующую ссылку: https://localhost/web/index.php?r=gii 

.. image:: /_static/gii.png
   :alt: gii
   :width: 700

Необходимо в http://localhost/phpmyadmin/index.php?lang=ru создать базу данных с таблицами

 .. note::
   Авторизация: таблица пользователей

Зададим первином ключу автоинкримент и будем требовать логин и пароль. Для безопасности зашифруем пароль через md5

.. image:: /_static/bdShop.png
   :alt: bdShop
   :width: 700

.. image:: /_static/users.png
   :alt: users
   :width: 700

.. image:: /_static/usersTable.png
   :alt: usersTable
   :width: 700

.. image:: /_static/usersData.png
   :alt: usersData
   :width: 700

Далее переименуем существующий файл пользователей models/User.php и по ссылке http://localhost/gii/model создадим файл по нашей таблице. таблицу можно выбрать из списка

.. image:: /_static/usersModel.png
   :alt: usersModel
   :width: 700

В случае ошибки открываем доступ к папке 

.. image:: /_static/error.png
   :alt: error
   :width: 700

Редактируем код, проверяем, чтобы везде в проекте был не Username, а login

.. code-block:: PHP

  <?php
 
 namespace app\models;
 
 use Yii;
 use yii\web\IdentityInterface;
 
 /**
  * This is the model class for table "users".
  *
  * @property int $id
  * @property string $login
  * @property string $password
  */
 class User extends \yii\db\ActiveRecord implements IdentityInterface
 {
     /**
      * {@inheritdoc}
      */
     public static function tableName()
     {
         return 'users';
     }
 
     /**
      * {@inheritdoc}
      */
     public function rules()
     {
         return [
             [['login', 'password'], 'required'],
             [['login', 'password'], 'string', 'max' => 255],
         ];
     }
 
     /**
      * {@inheritdoc}
      */
     public function attributeLabels()
     {
         return [
             'id' => 'ID',
             'login' => 'Login',
             'password' => 'Password',
         ];
     }
     public static function findIdentity($id)
     {
         return static::findOne($id);
     }
 
     public static function findIdentityByAccessToken($token, $type = null)
     {
         return null;
     }
 
     public function getId()
     {
         return $this->id;
     }
 
     public function getAuthKey()
     {
         return null;
     }
 
     public function validateAuthKey($authKey)
     {
         return false;
     }
 
     public function validatePassword($password)
     {
         return $this->password === md5($password);
     }
 
     public static function findBylogin($login)
     {
         return User::findOne(['login' => $login]);
     }
 }

Для вывода данных из таблицы необхлжимо помимо модели создать контроллер. 

.. image:: /_static/orders.png
   :alt: orders
   :width: 700

.. image:: /_static/ordersData.png
   :alt: ordersData
   :width: 700

.. image:: /_static/ordersModel.png
   :alt: ordersModel
   :width: 700

.. image:: /_static/ordersController.png
   :alt: ordersController
   :width: 700

.. image:: /_static/ordersView.png
   :alt: ordersView
   :width: 700

.. autosummary::
   :toctree: generated

   lumache
