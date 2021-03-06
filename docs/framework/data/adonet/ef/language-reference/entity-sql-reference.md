---
title: "Справочник по Entity SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 61ce7ee1-ffe2-477d-8a9f-835b0a11d900
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Справочник по Entity SQL
В этом разделе содержатся справочные подразделы по языку [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. В этом подразделе собраны операторы [!INCLUDE[esql](../../../../../../includes/esql-md.md)] по категориям с основными сведениями о каждом операторе.  
  
## Арифметические операторы  
 Арифметические операторы предназначены для выполнения математических операций над двумя выражениями с одним или несколькими числовыми типами данных.  Арифметические операторы [!INCLUDE[esql](../../../../../../includes/esql-md.md)] приведены в следующей таблице.  
  
|Оператор|Применение|  
|--------------|----------------|  
|[\+ \(сложение\)](../../../../../../docs/framework/data/adonet/ef/language-reference/add.md)|Сложение.|  
|[\/ \(деление\)](../../../../../../docs/framework/data/adonet/ef/language-reference/divide-entity-sql.md)|Деление.|  
|[% \(модуль\)](../../../../../../docs/framework/data/adonet/ef/language-reference/modulo-entity-sql.md)|Возвращает остаток от отделения.|  
|[\* \(умножение\)](../../../../../../docs/framework/data/adonet/ef/language-reference/multiply-entity-sql.md)|Умножение.|  
|[\- \(отрицательное\)](../../../../../../docs/framework/data/adonet/ef/language-reference/negative-entity-sql.md)|Отрицание.|  
|[\- \(вычитание\)](../../../../../../docs/framework/data/adonet/ef/language-reference/subtract-entity-sql.md)|Вычитание.|  
  
## Канонические функции  
 Канонические функции поддерживаются всеми поставщиками данных и могут использоваться всеми технологиями запросов.  В следующей таблице приведены канонические функции.  
  
|Функция|Тип|  
|-------------|---------|  
|[Канонические статистические функции языка Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/aggregate-canonical-functions.md)|Обсуждаются статистические канонические функции языка [!INCLUDE[esql](../../../../../../includes/esql-md.md)].|  
|[Математические канонические функции](../../../../../../docs/framework/data/adonet/ef/language-reference/math-canonical-functions.md)|Обсуждаются математические канонические функции языка [!INCLUDE[esql](../../../../../../includes/esql-md.md)].|  
|[Строковые канонические функции](../../../../../../docs/framework/data/adonet/ef/language-reference/string-canonical-functions.md)|Обсуждаются строковые канонические функции языка [!INCLUDE[esql](../../../../../../includes/esql-md.md)].|  
|[Канонические функции даты и времени](../../../../../../docs/framework/data/adonet/ef/language-reference/date-and-time-canonical-functions.md)|Обсуждаются канонические функции даты и времени в языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)].|  
|[Битовые канонические функции](../../../../../../docs/framework/data/adonet/ef/language-reference/bitwise-canonical-functions.md)|Обсуждаются побитовые канонические функции языка [!INCLUDE[esql](../../../../../../includes/esql-md.md)].|  
|[Прочие канонические функции](../../../../../../docs/framework/data/adonet/ef/language-reference/other-canonical-functions.md)|Обсуждаются функции, которые не являются побитовыми, строковыми, математическими, статистическими или функциями даты\-времени.|  
  
## Операторы сравнения  
 Операторы сравнения определены для следующих типов: `Byte`, `Int16`, `Int32`, `Int64`, `Double`, `Single`, `Decimal`, `String`, `DateTime`, `Date`, `Time`, `DateTimeOffset`.  Неявное повышение типов операндов происходит до применения оператора сравнения.  Результатом действия операторов сравнения всегда являются логические значения.  Если один из операндов принимает значение `null`, результат также принимает значение `null`.  
  
 Равенство и неравенство определяются для всех типов объектов, имеющих свойство идентификатора, например для типа `Boolean`.  Объекты, которые не относятся к типам\-примитивам, но обладают свойством идентификатора, считаются равными, если имеют одинаковое значение свойства идентификатора.  Операторы сравнения [!INCLUDE[esql](../../../../../../includes/esql-md.md)] приведены в следующей таблице.  
  
|Оператор|Описание|  
|--------------|--------------|  
|[\= \(равно\)](../../../../../../docs/framework/data/adonet/ef/language-reference/equals-entity-sql.md)|Проверяет равенство двух выражений.|  
|[\> \(больше\)](../../../../../../docs/framework/data/adonet/ef/language-reference/greater-than-entity-sql.md)|Сравнивает два выражения и определяет, имеет ли левое выражение значение больше значения правого выражения.|  
|[\>\= \(больше или равно\)](../../../../../../docs/framework/data/adonet/ef/language-reference/greater-than-or-equal-to-entity-sql.md)|Сравнивает два выражения и определяет, имеет ли левое выражение значение, большее или равное значению правого выражения.|  
|[IS &#91;NOT&#93; NULL](../../../../../../docs/framework/data/adonet/ef/language-reference/isnull-entity-sql.md)|Определяет, имеет ли выражение запроса значение null.|  
|[\< \(меньше\)](../../../../../../docs/framework/data/adonet/ef/language-reference/less-than-entity-sql.md)|Сравнивает два выражения, чтобы определить, является ли значение левого выражения меньшим, чем значение правого выражения.|  
|[\<\= \(меньше или равно\)](../../../../../../docs/framework/data/adonet/ef/language-reference/less-than-or-equal-to-entity-sql.md)|Сравнивает два выражения и определяет, имеет ли левое выражение значение, меньшее или равное значению правого выражения.|  
|[&#91;NOT&#93; BETWEEN](../../../../../../docs/framework/data/adonet/ef/language-reference/between-entity-sql.md)|Определяет, находится ли значение выражения в указанном диапазоне.|  
|[\!\= \(не равно\)](../../../../../../docs/framework/data/adonet/ef/language-reference/not-equal-to-entity-sql.md)|Сравнивает два выражения, чтобы определить, является ли значение левого выражения не равным значению правого выражения.|  
|[&#91;NOT&#93; LIKE](../../../../../../docs/framework/data/adonet/ef/language-reference/like-entity-sql.md)|Определяет, совпадает ли указанная символьная строка с заданным шаблоном.|  
  
## Логические операторы, операторы с выражением CASE  
 Логические операторы проверяют истинность некоторого условия.  Выражение CASE для определения результата вычисляет набор логических выражений.  Логические операторы и операторы с выражением CASE приведены в следующей таблице.  
  
|Оператор|Описание|  
|--------------|--------------|  
|[&& \(Логическое И\)](../../../../../../docs/framework/data/adonet/ef/language-reference/and-entity-sql.md)|Логическое И.|  
|[\!  \(логическое НЕ\)](../../../../../../docs/framework/data/adonet/ef/language-reference/not-entity-sql.md)|Логическое НЕ.|  
|[&#124;&#124; \(Логическое ИЛИ\)](../../../../../../docs/framework/data/adonet/ef/language-reference/or-entity-sql.md)|Логическое ИЛИ.|  
|[CASE](../../../../../../docs/framework/data/adonet/ef/language-reference/case-entity-sql.md)|Вычисляет набор логических выражений для определения результата.|  
|[THEN](../../../../../../docs/framework/data/adonet/ef/language-reference/then-entity-sql.md)|Результат предложения [WHEN](http://msdn.microsoft.com/ru-ru/6233fe9f-00b0-460e-8372-64e138a5f998), если оно имеет значение true.|  
  
## Операторы запроса  
 С помощью операторов запросов определяются выражения запроса, возвращающие данные сущности.  Операторы запросов приведены в следующей таблице.  
  
|Оператор|Применение|  
|--------------|----------------|  
|[FROM](../../../../../../docs/framework/data/adonet/ef/language-reference/from-entity-sql.md)|Указывает коллекцию, используемую в инструкциях [SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md).|  
|[GROUP BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md)|Определяет группы, в которые должны быть помещены объекты, возвращаемые выражением запроса \([SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)\).|  
|[GroupPartition](../../../../../../docs/framework/data/adonet/ef/language-reference/grouppartition-entity-sql.md)|Возвращает коллекцию значений аргумента, проекция которых получена из раздела группы, с которой связано статистическое выражение.|  
|[HAVING](../../../../../../docs/framework/data/adonet/ef/language-reference/having-entity-sql.md)|Задает условие поиска для группы или статистического выражения.|  
|[LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md)|Используется с предложением [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) для выполненного физического разбиения на страницы.|  
|[ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)|Указывает порядок сортировки для объектов, возвращаемых инструкцией [SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md).|  
|[SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)|Указывает элементы в проекции, возвращаемые запросом.|  
|[SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md)|Используется с предложением [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) для выполненного физического разбиения на страницы.|  
|[TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)|Указывает на то, что будет возвращен только первый набор строк из результата запроса.|  
|[WHERE](../../../../../../docs/framework/data/adonet/ef/language-reference/where-entity-sql.md)|Выполняет условную фильтрацию данных, возвращаемых запросом.|  
  
## Ссылочные операторы  
 Ссылка — это логический указатель \(внешний ключ\) на отдельную сущность в определенном наборе сущностей.  Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] поддерживает следующие операторы для конструирования, деконструирования и перехода по ссылкам.  
  
|Оператор|Применение|  
|--------------|----------------|  
|[CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md)|Создает ссылки на сущность в наборе сущностей.|  
|[DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md)|Разыменовывает значение ссылки и выдает результат разыменования.|  
|[KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md)|Извлекает ключ ссылки или выражение сущности.|  
|[NAVIGATE](../../../../../../docs/framework/data/adonet/ef/language-reference/navigate-entity-sql.md)|Позволяет переходить по связям от одного типа сущности к другому.|  
|[REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)|Возвращает ссылку на экземпляр сущности.|  
  
## Операторы набора  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] предоставляет целый ряд мощных операторов работы с наборами.  Сюда относятся операторы работы с множествами, аналогичные таким операторам Transact\-SQL, как UNION, INTERSECT, EXCEPT и EXISTS.  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] также поддерживает операторы для исключения повторяющихся значений \(SET\), проверки членства \(IN\) и соединения \(JOIN\).  Операторы [!INCLUDE[esql](../../../../../../includes/esql-md.md)] работы с множествами приведены в следующей таблице.  
  
|Оператор|Применение|  
|--------------|----------------|  
|[ANYELEMENT](../../../../../../docs/framework/data/adonet/ef/language-reference/anyelement-entity-sql.md)|Извлекает элемент из многозначной коллекции.|  
|[EXCEPT](../../../../../../docs/framework/data/adonet/ef/language-reference/except-entity-sql.md)|Возвращает коллекцию различных значений из выражения запроса, расположенного левее операнда EXCEPT, за исключением тех, которые были возвращены выражением запроса, расположенного правее операнда EXCEPT.|  
|[&#91;NOT&#93; EXISTS](../../../../../../docs/framework/data/adonet/ef/language-reference/exists-entity-sql.md)|Определяет, является ли коллекция пустой.|  
|[FLATTEN](../../../../../../docs/framework/data/adonet/ef/language-reference/flatten-entity-sql.md)|Преобразовывает коллекцию коллекций в плоскую коллекцию.|  
|[&#91;NOT&#93; IN](../../../../../../docs/framework/data/adonet/ef/language-reference/in-entity-sql.md)|Определяет, совпадает ли значение с каким\-либо значением в коллекции.|  
|[INTERSECT](../../../../../../docs/framework/data/adonet/ef/language-reference/intersect-entity-sql.md)|Возвращает коллекцию различных значений, возвращаемых выражениями запроса, указанных как слева, так и справа от операнда INTERSECT.|  
|[OVERLAPS](../../../../../../docs/framework/data/adonet/ef/language-reference/overlaps-entity-sql.md)|Определяет, содержат ли две коллекции общие элементы.|  
|[SET](../../../../../../docs/framework/data/adonet/ef/language-reference/set-entity-sql.md)|Используется для преобразования коллекции объектов во множество путем получения новой коллекции, в которой удалены все повторяющиеся элементы.|  
|[UNION](../../../../../../docs/framework/data/adonet/ef/language-reference/union-entity-sql.md)|Сводит результаты двух или более запросов в одну коллекцию.|  
  
## Операторы работы с типами  
 В [!INCLUDE[esql](../../../../../../includes/esql-md.md)] предусмотрены операции, позволяющие конструировать тип выражения \(его значения\), выполнять к нему запросы и управлять им.  В следующей таблице перечислены операторы, предназначенные для работы с типами.  
  
|Оператор|Применение|  
|--------------|----------------|  
|[CAST](../../../../../../docs/framework/data/adonet/ef/language-reference/cast-entity-sql.md)|Преобразует выражение одного типа данных в другой.|  
|[COLLECTION](../../../../../../docs/framework/data/adonet/ef/language-reference/collection-entity-sql.md)|Используется в операции [FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md) для объявления коллекции типов сущности или сложных типов.|  
|[IS &#91;NOT&#93; OF](../../../../../../docs/framework/data/adonet/ef/language-reference/isof-entity-sql.md)|Определяет, относится ли тип выражения к указанному типу или одному из его подтипов.|  
|[OFTYPE](../../../../../../docs/framework/data/adonet/ef/language-reference/oftype-entity-sql.md)|Возвращает коллекцию объектов из выражения запроса, которое относится к заданному типу.|  
|[Конструктор именованных типов](../../../../../../docs/framework/data/adonet/ef/language-reference/named-type-constructor-entity-sql.md)|Используется для создания экземпляров типов сущности или сложных типов.|  
|[MULTISET](../../../../../../docs/framework/data/adonet/ef/language-reference/multiset-entity-sql.md)|Создает экземпляр мультинабора из списка значений.|  
|[ROW](../../../../../../docs/framework/data/adonet/ef/language-reference/row-entity-sql.md)|Создает анонимные структурно типизированные записи из одного или нескольких значений.|  
|[TREAT](../../../../../../docs/framework/data/adonet/ef/language-reference/treat-entity-sql.md)|Обрабатывает объект некоторого базового типа, как объект указанного производного типа.|  
  
## Другие операторы  
 Другие операторы [!INCLUDE[esql](../../../../../../includes/esql-md.md)] приведены в следующей таблице.  
  
|Оператор|Применение|  
|--------------|----------------|  
|[\+ \(объединения строк\)](../../../../../../docs/framework/data/adonet/ef/language-reference/string-concatenation-entity-sql.md)|Используется для объединения строк в [!INCLUDE[esql](../../../../../../includes/esql-md.md)].|  
|[.  \(Доступ к членам\)](../../../../../../docs/framework/data/adonet/ef/language-reference/member-access-entity-sql.md)|Используется для доступа к значению свойства или полю экземпляра структурного типа концептуальной модели.|  
|[\-\- \(комментарий\)](../../../../../../docs/framework/data/adonet/ef/language-reference/comment-entity-sql.md)|Включить комментарии [!INCLUDE[esql](../../../../../../includes/esql-md.md)].|  
|[FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md)|Определяет встроенную функцию, которая может выполняться в запросе Entity SQL.|  
  
## См. также  
 [Язык Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)