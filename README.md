# proxy

Библиотека для создания оберток (прокси) над классами.

Прокси-объект повторяет публичный интерфейс класса (экспортные методы и поля),
делегируя вызов вложенному реальному объекту.

Возможности:

* создание прокси-объекта с идентичным интерфейсом;
* синхронизация значений полей прокси-объекта и реального объекта;
* добавление методов, импортов, полей, шагов инициализации в runtime;
* добавление перехватчиков ("перед", "после") вызова метода;
* поддержка вложенных прокси.

docs - todo;

## Пример использования

```bsl
#Использовать proxy

КакойТоКласс = Новый КакойТоКласс();
КакойТоКласс.Поле = 123;

ИмяМетода = "ДобавленнаяФункция";
ТекстМетода = "Возврат Поле + 1;";

Прокси = Новый КонструкторПрокси(КакойТоКласс)
    .ДобавитьИмпортПоИмени("fs")
    .ДобавитьПубличноеПоле("НовоеПоле", "ЗначениеПоУмолчанию")
    .ДобавитьМетод(ИмяМетода, ТекстМетода)
    .ДобавитьПередВызовомМетода("ДобавленнаяФункция", "Сообщить(""Привет, мир!"");")
    .Построить();

Ожидаем.Что(Прокси.Поле).Равно(123);
Ожидаем.Что(Прокси.РоднаяФункцияВозвращающаяИстина()).ЭтоИстина();
Ожидаем.Что(Прокси.ДобавленнаяФункция()).Равно(124);
```

## Документация по методам

### КонструкторПрокси

#### ПриСозданииОбъекта

```bsl
// Конструктор
//
// Параметры:
//   Объект - Произвольный - Инстанс объекта, над которым нужно создать прокси-объект.
//
Процедура ПриСозданииОбъекта(Объект) 
```

#### ДобавитьПриватноеПоле

```bsl
// Добавляет в прокси-объект новое приватное поле.
//
// Параметры:
//   ИмяПоля - Строка - Имя добавляемого поля
//   ЗначениеПоля - Произвольный - Значение, которым необходимо проинициализировать добавляемое поле.
//                                 Если не задано, поле не инициализируется и содержит Неопределено.
//
//  Возвращаемое значение:
//   КонструкторПрокси - Ссылка на текущий инстанс КонструкторПрокси
//
Функция ДобавитьПриватноеПоле(ИмяПоля, ЗначениеПоля = Неопределено) 
```

#### ДобавитьПубличноеПоле

```bsl
// Добавляет в прокси-объект новое публичное (экспортное) поле.
//
// Параметры:
//   ИмяПоля - Строка - Имя добавляемого поля
//   ЗначениеПоля - Произвольный - Значение, которым необходимо проинициализировать добавляемое поле.
//                                 Если не задано, поле не инициализируется и содержит Неопределено.
//
//  Возвращаемое значение:
//   КонструкторПрокси - Ссылка на текущий инстанс КонструкторПрокси
//
Функция ДобавитьПубличноеПоле(ИмяПоля, ЗначениеПоля = Неопределено) 
```

#### ДобавитьМетод

```bsl
// Добавляет в прокси-объект новый публичный (экспортный) метод.
//
// Параметры:
//   ИмяМетода - Строка - Имя добавляемого метода.
//   ТекстМетода - Строка - Текст добавляемого метода. Допустимо использование многострочной строки.
//
//  Возвращаемое значение:
//   КонструкторПрокси - Ссылка на текущий инстанс КонструкторПрокси
//
Функция ДобавитьМетод(ИмяМетода, ТекстМетода) 
```

#### ДобавитьПередВызовомМетода

```bsl
// Добавляет в прокси-объект перехватчик, срабатывающий перед вызовом указанного метода.
//
// Параметры:
//   ИмяМетода - Строка - Имя перехватываемого метода.
//   ТекстПерехватчика - Текст - Текст добавляемого перехватчика. Допустимо использование многострочной строки.
//
//  Возвращаемое значение:
//   КонструкторПрокси - Ссылка на текущий инстанс КонструкторПрокси
//
Функция ДобавитьПередВызовомМетода(ИмяМетода, ТекстПерехватчика) 
```

#### ДобавитьПослеВызоваМетода

```bsl
// Добавляет в прокси-объект перехватчик, срабатывающий после вызова указанного метода.
//
// Параметры:
//   ИмяМетода - Строка - Имя перехватываемого метода.
//   ТекстПерехватчика - Текст - Текст добавляемого перехватчика. Допустимо использование многострочной строки.
//
//  Возвращаемое значение:
//   КонструкторПрокси - Ссылка на текущий инстанс КонструкторПрокси
//
Функция ДобавитьПослеВызоваМетода(ИмяМетода, ТекстПерехватчика) 
```

#### ДобавитьИмпортПоИмени

```bsl
// Добавляет в прокси-объект импорт библиотеки (#Использовать) по имени библиотеки.
//
// Параметры:
//   ИмяБиблиотеки - Строка - Имя библиотеки.
//
//  Возвращаемое значение:
//   КонструкторПрокси - Ссылка на текущий инстанс КонструкторПрокси
//
Функция ДобавитьИмпортПоИмени(ИмяБиблиотеки) 
```

#### ДобавитьИмпортПоПути

```bsl
// Добавляет в прокси-объект импорт библиотеки (#Использовать) по пути к библиотеке.
//
// Параметры:
//   ПутьКБиблиотеке - Строка - Путь к библиотеке. Можно использовать как абсолютный, так и относительный путь.
//
//  Возвращаемое значение:
//   КонструкторПрокси - Ссылка на текущий инстанс КонструкторПрокси
//
Функция ДобавитьИмпортПоПути(ПутьКБиблиотеке) 
```

#### ДобавитьШагИнициализации

```bsl
// Добавляет в прокси-объект шаг инициализации в тело модуля.
//
// Параметры:
//   ТекстШага - Строка - Выполняемый код.
//
//  Возвращаемое значение:
//   КонструкторПрокси - Ссылка на текущий инстанс КонструкторПрокси
//
Функция ДобавитьШагИнициализации(ТекстШага) 
```

#### ТекстСценария

```bsl
// Получить сконструированный текст сценария будущего прокси-объекта
//
//  Возвращаемое значение:
//   Строка - Текст сценария прокси-объекта
//
Функция ТекстСценария() 
```

#### Построить

```bsl
// Сконструировать готовый прокси-объект по настройкам конструктора прокси.
//
// Параметры:
//   ТекстСценария - Строка - Текст сценария прокси-объекта. Если не задан, формируется автоматически.
//
//  Возвращаемое значение:
//   Произвольный - Прокси над объектом, переданным в конструктор прокси
//
Функция Построить(ТекстСценария = Неопределено) 
```

### Модуль ОбработкаПроксиОбъекта

#### ИсходныйТип

```bsl
// Получает тип объекта, вокруг которого построен прокси-объект (рекурсивно).
//
// Параметры:
//   Прокси - Произвольный - Объект, у которого нужно найти исходный тип объекта
//
//  Возвращаемое значение:
//   Тип - Исходный тип объекта
//
Функция ИсходныйТип(Прокси) 
```

#### СинхронизироватьПоля

```bsl
// Синхронизировать значения экспортных полей двух объектов.
//
// Параметры:
//   ИсходныйОбъект - Произвольный - Источник значений свойств
//   Потребитель - Произвольный - Получатель значений свойств
//
Процедура СинхронизироватьПоля(ИсходныйОбъект, Потребитель) 
```

### Модуль Константы_Прокси

```bsl
// Имя поля, в котором хранится ссылка на исходный объект.
Перем Поле_ИнстансОбъекта Экспорт;
```
