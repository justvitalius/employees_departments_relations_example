# Пример по реализации связи между двумя моделями посредством Angular
## Задача
Есть два списка ```Employees``` и ```Departments```, приложение получает их через API. Оба списка связаны через ```id``` друг с другом.
Нужно на клиенте отобразить оба списка с расширенной информацией по связанному объекту. 
Так, например: при отрисовке сотрудника нужно нарисовать не только аватарку и имя, но и вывести полное имя департамента. И наоборот.


## Решение
- Оба списка существуют в своих модулях. Это чистое усложнение примера;
- Оба списка получая json оборачивают его в js-класс. Это опять же для усложнения и имитации настоящего приложения;
- Всю логику с загрузкой, хранением списка и конструкторами выносим в отдельные провайдеры (provider) в соответствующих модулях;
- В (главном) модуле ```App``` подгружаем commonjs-модуль, который декорирует конструкторы ```Employees``` и ```Departments```. 
Чтобы избежать циклической зависимости фабрик, приходится использовать запись ```$injector.get('departmentsFactory')``` вместо указания ```departmentsFactory``` в зависимостях самой ```EmployeeConstructor``` (см.пример)
- После инициализации приложения, декоратор апгрейдит каждую фабрику и они получают расширенный набор методов

## Как запустить
Нужно склонировать приложение к себе, выполнить ```npm install```, далее ```npm run builder``` соберет js-код, а ```npm run server``` запустить локальный сервер. 
После чего по адресу ```http://localhost:8080``` будет доступен пример приложения.

## Особенности
- Для примера, что это все не фикция, загрузка департаментов отложена на 4сек после загрузки приложения. Поэтому не растраивайтесь, если после октрытия приложения в браузере, вы увидете только список топ-менеджмента трех IT-гигинтов

