---
title: "Коллекции схем Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89a75de8-dee8-45e2-a97f-254d7e62e7e1
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Коллекции схем Oracle
Поставщик данных Microsoft .NET Framework для Oracle поддерживает следующие специальные коллекции схем в дополнение к общим коллекциям схем.  
  
-   Столбцы  
  
-   Indexes  
  
-   IndexColumns  
  
-   Процедуры  
  
-   Последовательности  
  
-   Synonyms  
  
-   Таблицы  
  
-   Users  
  
-   Представления  
  
-   Функции  
  
-   Пакеты  
  
-   PackageBodies  
  
-   Аргументы  
  
-   UniqueKeys  
  
-   PrimaryKeys  
  
-   ForeignKeys  
  
-   ForeignKeyColumns  
  
-   ProcedureParameters  
  
## Столбцы  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец таблицы, представления или кластера.|  
|TABLE\_NAME|Строковое|Имя таблицы, представления или кластера.|  
|COLUMN\_NAME|Строковое|Имя столбца.|  
|Идентификатор|Десятичное число|Порядковый номер столбца, присвоенный при создании.|  
|DATATYPE|Строковое|Тип данных столбца.|  
|LENGTH|Десятичное число|Длина столбца в байтах.|  
|PRECISION|Десятичное число|Точность десятичного представления для типа данных NUMBER; точность двоичного представления для типа данных FLOAT, значение NULL для всех других типов данных.|  
|SCALE|Десятичное число|Количество знаков в числе справа от запятой.|  
|NULLABLE|Строковое|Указывает, допускает ли столбец значения NULL.  Значение равно N, если на столбце задано ограничение NOT NULL или если столбец входит в состав ограничения PRIMARY KEY.|  
  
## Indexes  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец индекса.|  
|INDEX\_NAME|Строковое|Имя индекса.|  
|INDEX\_TYPE|Строковое|Тип индекса \(NORMAL, BITMAP, FUNCTION\-BASED NORMAL, FUNCTION\-BASED BITMAP или DOMAIN\).|  
|TABLE\_OWNER|Строковое|Владелец индексированного объекта.|  
|TABLE\_NAME|Строковое|Имя индексированного объекта.|  
|TABLE\_TYPE|Строковое|Тип индексированного объекта \(например, TABLE, CLUSTER\).|  
|UNIQUENESS|Строковое|Указывает, имеет ли индекс тип UNIQUE или NONUNIQUE.|  
|COMPRESSION|Строковое|Указывает, имеет ли индекс тип ENABLED или DISABLED.|  
|PREFIX\_LENGTH|Десятичное число|Количество столбцов в префиксе ключа сжатия.|  
|TABLESPACE\_NAME|Строковое|Имя табличного пространства, содержащего индекс.|  
|INI\_TRANS|Десятичное число|Начальное количество транзакций.|  
|MAX\_TRANS|Десятичное число|Максимальное количество транзакций.|  
|INITIAL\_EXTENT|Десятичное число|Размер начального экстента.|  
|NEXT\_EXTENT|Десятичное число|Размер вторичных экстентов.|  
|MIN\_EXTENTS|Десятичное число|Минимальное количество экстентов, допускаемых в сегменте.|  
|MAX\_EXTENTS|Десятичное число|Максимальное количество экстентов, допускаемое в сегменте.|  
|PCT\_INCREASE|Десятичное число|Увеличение размера экстента в процентах.|  
|PCT\_THRESHOLD|Десятичное число|Предельное значение допустимого пространства блока в расчете на элемент указателя, в процентах.|  
|INCLUDE\_COLUMN|Десятичное число|Идентификатор последнего столбца, который может быть включен в индекс первичного ключа таблицы, организованной по индексам \(без переполнения\).  Этот столбец сопоставляется со столбцом COLUMN\_ID представлений словаря данных \*\_TAB\_COLUMNS.|  
|FREELISTS|Десятичное число|Количество списков свободных блоков процесса, распределенных для этого сегмента.|  
|FREELIST\_GROUPS|Десятичное число|Количество групп списка свободных блоков, распределенных для этого сегмента.|  
|PCT\_FREE|Десятичное число|Минимальный объем свободного пространства в блоке в процентах.|  
|LOGGING|Строковое|Данные журналов.|  
|BLEVEL|Десятичное число|Уровень B\*\-дерева: глубина индекса от корневого до конечных блоков.  Глубина 0 указывает, что корневой блок и листовой блок совпадают.|  
|LEAF\_BLOCKS|Десятичное число|Количество листовых блоков в индексе|  
|DISTINCT\_KEYS|Десятичное число|Количество различных индексированных значений.  Применительно к индексам, которые предписывают ограничения UNIQUE и PRIMARY KEY, это значение совпадает с количеством строк в таблице \(USER\_TABLES.NUM\_ROWS\).|  
|AVG\_LEAF\_BLOCKS\_PER\_KEY|Десятичное число|Среднее количество конечных блоков, в которых каждое различимое значение в индексе появляется с округлением до ближайшего целого числа.  Применительно к индексам, которые предписывают ограничения UNIQUE и PRIMARY KEY, это значение всегда равно 1.|  
|AVG\_DATA\_BLOCKS\_PER\_KEY|Десятичное число|Среднее количество блоков данных в таблице, на которые указывает различимое значение в индексе, округленное до ближайшего целого числа.  Это статистический показатель представляет собой среднее количество блоков данных, содержащих строки, которые содержат данное значение для индексированных столбцов.|  
|CLUSTERING\_FACTOR|Десятичное число|Указывает количественное значение порядка строк в таблице на основе значений индекса.|  
|STATUS|Строковое|Указывает, имеет ли несекционированный индекс значение VALID или UNUSABLE.|  
|NUM\_ROWS|Десятичное число|Количество строк в индексе.|  
|SAMPLE\_SIZE|Десятичное число|Размер образца, используемого для анализа индекса.|  
|LAST\_ANALYZED|DateTime|Дата, в которую проводился последний по времени анализ этого индекса.|  
|DEGREE|Строковое|Количество потоков, применяемых для просмотра индекса, в расчете на экземпляр.|  
|INSTANCES|Строковое|Количество экземпляров, в рамках которых должны быть просмотрены индексы.|  
|PARTITIONED|Строковое|Указывает, является ли этот индекс секционированным \(YES &#124; NO\).|  
|TEMPORARY|Строковое|Указывает, задан ли этот индекс на временной таблице.|  
|GENERATED|Строковое|Указывает, имеет ли индекс имя, сформированное системой \(Y&#124;N\).|  
|SECONDARY|Строковое|Указывает, является ли индекс вторичным объектом, созданным методом ODCIIndexCreate картриджа данных Oracle9i \(Y&#124;N\).|  
|BUFFER\_POOL|Строковое|Имя предусмотренного по умолчанию буферного пула, который используется для индексных блоков.|  
|USER\_STATS|Строковое|Указывает, введены ли статистические данные непосредственно пользователем.|  
|DURATION|Строковое|Указывает время существования временной таблицы: 1\)SYS$SESSION: строки сохраняются на все время существования сеанса; 2\) SYS$TRANSACTION: строки удаляются после выполнения инструкции COMMIT; 3\) значение NULL для постоянной таблицы.|  
|PCT\_DIRECT\_ACCESS|Десятичное число|Применительно к вторичному индексу на таблице, организованной по индексам, процентная доля строк с предположением VALID.|  
|ITYP\_OWNER|Строковое|Применительно к индексу домена, владелец типа индекса.|  
|ITYP\_NAME|Строковое|Применительно к индексу домена, имя типа индекса.|  
|PARAMETERS|Строковое|Применительно к индексу домена, строка параметра.|  
|GLOBAL\_STATS|Строковое|Применительно к секционированным индексам указывает, был ли выполнен сбор статистических данных путем анализа всего индекса в целом \(YES\) или была проведена оценка на основании статистических данных, относящихся к базовым секциям и подсекциям индекса \(NO\).|  
|DOMIDX\_STATUS|Строковое|Отражает состояние индекса домена.  NULL: указанный индекс не является индексом домена.  VALID: индекс является допустимым индексом домена.  IDXTYP\_INVLD: тип индекса этого индекса домена недопустим.|  
|DOMIDX\_OPSTATUS|Строковое|Отражает состояние операции, которая была выполнена на индексе домена. NULL: указанный индекс не является индексом домена.  VALID: операция выполнена без ошибок.  FAILED: операция завершилась неуспешно с ошибкой.|  
|FUNCIDX\_STATUS|Строковое|Указывает состояние индекса, основанного на функции. NULL: это не основанный на функции индекс; ENABLED: основанный на функции индекс разрешен; DISABLED: основанный на функции индекс запрещен.|  
|JOIN\_INDEX|Строковое|Указывает, является ли этот индекс индексом соединения или нет.|  
  
## IndexColumns  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|INDEX\_OWNER|Строковое|Владелец индекса.|  
|INDEX\_NAME|Строковое|Имя индекса.|  
|TABLE\_OWNER|Строковое|Владелец таблицы или кластера.|  
|TABLE\_NAME|Строковое|Имя таблицы или кластера.|  
|COLUMN\_NAME|Строковое|Имя столбца или атрибут столбца типа объекта.|  
|COLUMN\_POSITION|Десятичное число|Позиция столбца или атрибута в индексе.|  
|COLUMN\_LENGTH|Десятичное число|Индексированная длина столбца.|  
|CHAR\_LENGTH|Десятичное число|Максимальная длина столбца в кодовых точках.|  
|DESCEND|Строковое|Указывает, отсортирован ли столбец в порядке убывания.|  
  
## Процедуры  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец объекта.|  
|OBJECT\_NAME|Строковое|Имя объекта.|  
|SUBOBJECT\_NAME|Строковое|Имя вложенного объекта \(например, секции\).|  
|OBJECT\_ID|Десятичное число|Номер объекта в словаре.|  
|DATA\_OBJECT\_ID|Десятичное число|Номер объекта для содержащего объект сегмента в словаре.|  
|LAST\_DDL\_TIME|DateTime|Отметка времени последнего изменения объекта в результате выполнения команды DDL \(включая предоставление и отмену разрешений\).|  
|TIMESTAMP|Строковое|Отметка времени спецификации объекта \(символьные данные\).|  
|STATUS|Строковое|Состояние объекта \(VALID, INVALID или N\/A\).|  
|TEMPORARY|Строковое|Является ли объект временным \(текущему сеансу доступны только данные, которые он сам поместил в объект\).|  
|GENERATED|Строковое|Было ли имя этого объекта сформировано системой?  \(Y &#124; N\).|  
|SECONDARY|Строковое|Является ли этот объект вторичным, созданным методом ODCIIndexCreate картриджа данных Oracle9i \(Y &#124; N\).|  
|CREATED|DateTime|Дата создания объекта.|  
  
## Последовательности  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|SEQUENCE\_OWNER|Строковое|Имя владельца последовательности.|  
|SEQUENCE\_NAME|Строковое|Имя последовательности.|  
|MIN\_VALUE|Десятичное число|Минимальное значение последовательности.|  
|MAX\_VALUE|Десятичное число|Максимальное значение последовательности.|  
|INCREMENT\_BY|Десятичное число|Значение, на которое увеличивается последовательность.|  
|CYCLE\_FLAG|Строковое|Указывает, выполняется ли в последовательности переход в начало цикла после достижения предела.|  
|ORDER\_FLAG|Строковое|Указывает, происходит ли формирование чисел последовательности в определенном порядке.|  
|CACHE\_SIZE|Десятичное число|Количество чисел последовательности в кэше.|  
|LAST\_NUMBER|Десятичное число|Последнее число последовательности, записанное на диск.  Если для последовательности используется кэширование, то число, записанное на диск, представляет собой последнее число, помещенное в кэш последовательности.  Это число, вероятнее всего, превышает последнее используемое число последовательности.|  
  
## Synonyms  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец синонима.|  
|SYNONYM\_NAME|Строковое|Имя синонима.|  
|TABLE\_OWNER|Строковое|Владелец объекта, на который ссылается синоним.|  
|TABLE\_NAME|Строковое|Имя объекта, на который ссылается синонимом.|  
|DB\_LINK|Строковое|Имя канала базы данных, указанного в ссылке, если таковой имеется.|  
  
## Таблицы  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец таблицы.|  
|TABLE\_NAME|Строковое|Имя таблицы.|  
|TYPE|Строковое|Тип таблицы.|  
  
## Users  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|NAME|Строковое|Имя пользователя.|  
|Идентификатор|Десятичное число|Идентификационный номер пользователя.|  
|CREATEDATE|DateTime|Дата создания пользователя.|  
  
## Представления  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец представления.|  
|VIEW\_NAME|Строковое|Имя представления.|  
|TEXT\_LENGTH|Десятичное число|Длина текста представления.|  
|TEXT|Строковое|Текст представления.|  
|TYPE\_TEXT\_LENGTH|Десятичное число|Длина предложения типа типизированного представления.|  
|TYPE\_TEXT|Строковое|Предложение типа типизированного представления.|  
|OID\_TEXT\_LENGTH|Десятичное число|Длина предложения WITH OID типизированного представления.|  
|OID\_TEXT|Строковое|Предложение WITH OID типизированного представления.|  
|VIEW\_TYPE\_OWNER|Строковое|Владелец типа представления, если представление — типизированное представление.|  
|VIEW\_TYPE|Строковое|Тип представления, если представление — типизированное представление.|  
|SUPERVIEW\_NAME|Строковое|Имя суперпредставления.|  
  
## Функции  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец объекта.|  
|OBJECT\_NAME|Строковое|Имя объекта.|  
|SUBOBJECT\_NAME|Строковое|Имя вложенного объекта \(например, секции\).|  
|OBJECT\_ID|Десятичное число|Номер объекта в словаре.|  
|DATA\_OBJECT\_ID|Десятичное число|Номер объекта для содержащего объект сегмента в словаре.|  
|OBJECT\_TYPE|Строковое|Тип объекта.|  
|CREATED|DateTime|Дата создания объекта.|  
|LAST\_DDL\_TIME|DateTime|Отметка времени последнего изменения объекта в результате выполнения команды DDL \(включая предоставление и отмену разрешений\).|  
|TIMESTAMP|Строковое|Отметка времени спецификации объекта \(символьные данные\).|  
|STATUS|Строковое|Состояние объекта \(VALID, INVALID или N\/A\).|  
|TEMPORARY|Строковое|Является ли объект временным \(текущему сеансу доступны только данные, которые он сам поместил в объект\).|  
|GENERATED|Строковое|Было ли имя этого объекта сформировано системой?  \(Y &#124; N\).|  
|SECONDARY|Строковое|Является ли этот объект вторичным, созданным методом ODCIIndexCreate картриджа данных Oracle9i \(Y &#124; N\).|  
  
## Пакеты  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец объекта.|  
|OBJECT\_NAME|Строковое|Имя объекта.|  
|SUBOBJECT\_NAME|Строковое|Имя вложенного объекта \(например, секции\).|  
|OBJECT\_ID|Десятичное число|Номер объекта в словаре.|  
|DATA\_OBJECT\_ID|Десятичное число|Номер объекта для содержащего объект сегмента в словаре.|  
|LAST\_DDL\_TIME|DateTime|Отметка времени последнего изменения объекта в результате выполнения команды DDL \(включая предоставление и отмену разрешений\).|  
|TIMESTAMP|Строковое|Отметка времени спецификации объекта \(символьные данные\).|  
|STATUS|Строковое|Состояние объекта \(VALID, INVALID или N\/A\).|  
|TEMPORARY|Строковое|Является ли объект временным \(текущему сеансу доступны только данные, которые он сам поместил в объект\).|  
|GENERATED|Строковое|Было ли имя этого объекта сформировано системой?  \(Y &#124; N\).|  
|SECONDARY|Строковое|Является ли этот объект вторичным, созданным методом ODCIIndexCreate картриджа данных Oracle9i \(Y &#124; N\).|  
|CREATED|DateTime|Дата создания объекта.|  
  
## PackageBodies  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец объекта.|  
|OBJECT\_NAME|Строковое|Имя объекта.|  
|SUBOBJECT\_NAME|Строковое|Имя вложенного объекта \(например, секции\).|  
|OBJECT\_ID|Десятичное число|Номер объекта в словаре.|  
|DATA\_OBJECT\_ID|Десятичное число|Номер объекта для содержащего объект сегмента в словаре.|  
|LAST\_DDL\_TIME|DateTime|Отметка времени последнего изменения объекта в результате выполнения команды DDL \(включая предоставление и отмену разрешений\).|  
|TIMESTAMP|Строковое|Отметка времени спецификации объекта \(символьные данные\).|  
|STATUS|Строковое|Состояние объекта \(VALID, INVALID или N\/A\).|  
|TEMPORARY|Строковое|Является ли объект временным \(текущему сеансу доступны только данные, которые он сам поместил в объект\).|  
|GENERATED|Строковое|Было ли имя этого объекта сформировано системой?  \(Y &#124; N\).|  
|SECONDARY|Строковое|Является ли этот объект вторичным, созданным методом ODCIIndexCreate картриджа данных Oracle9i \(Y &#124; N\).|  
|CREATED|DateTime|Дата создания объекта.|  
  
## Аргументы  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Имя владельца последовательности.|  
|PACKAGE\_NAME|Строковое|Имя пакета.|  
|OBJECT\_NAME|Строковое|Имя процедуры или функции.|  
|ARGUMENT\_NAME|Строковое|Имя аргумента.|  
|POSITION|Десятичное число|Позиция в списке аргументов или NULL для возвращаемого значения функции.|  
|SEQUENCE|Десятичное число|Последовательность аргументов, включая все уровни вложенности.|  
|DEFAULT\_VALUE|Строковое|Значение аргумента по умолчанию.|  
|DEFAULT\_LENGTH|Десятичное число|Длина значения по умолчанию для аргумента.|  
|IN\_OUT|Строковое|Направление передачи аргумента \(IN, OUT или IN\/OUT\).|  
|DATA\_LENGTH|Десятичное число|Длина столбца в байтах.|  
|DATA\_PRECISION|Десятичное число|Длина в десятичных \(NUMBER\) или двоичных цифрах \(FLOAT\).|  
|DATA\_SCALE|Десятичное число|Количество знаков в числе справа от запятой.|  
|DATA\_TYPE|Строковое|Тип данных аргумента.|  
  
## UniqueKeys  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец определения ограничения.|  
|CONSTRAINT\_NAME|Строковое|Имя определения ограничения.|  
|TABLE\_NAME|Строковое|Имя, связанное с таблицей \(или представлением\), в которой содержится определение ограничения.|  
|SEARCH\_CONDITION|Строковое|Текст условия поиска проверочного ограничения.|  
|R\_OWNER|Строковое|Владелец таблицы, на которую ссылается ссылочное ограничение.|  
|R\_CONSTRAINT\_NAME|Строковое|Имя определения ограничения уникальности для таблицы, на которую имеется ссылка.|  
|DELETE\_RULE|Строковое|Правило удаления ссылочного ограничения \(CASCADE или NO ACTION\).|  
|STATUS|Строковое|Состояние применения ограничения \(ENABLED или DISABLED\).|  
|DEFERRABLE|Строковое|Допускает ли ограничение задержку.|  
|VALIDATED|Строковое|Подчиняются ли все данные ограничению \(VALIDATED или NOT VALIDATED\).|  
|GENERATED|Строковое|Задано ли имя ограничения пользователем или системой.|  
|BAD|Строковое|Значение YES указывает, что это ограничение задает век неоднозначным образом.  Во избежание ошибок из\-за такой неопределенности перепишите ограничение, используя функцию TO\_DATE с четырехзначным значением года.|  
|RELY|Строковое|Применяется ли включенное ограничение принудительно или нет.|  
|LAST\_CHANGE|DateTime|Время последнего включения или отключения ограничения.|  
|INDEX\_OWNER|Строковое|Имя пользователя, владеющего индексом.|  
|INDEX\_NAME|Строковое|Имя индекса.|  
  
## PrimaryKeys  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец определения ограничения.|  
|CONSTRAINT\_NAME|Строковое|Имя определения ограничения.|  
|TABLE\_NAME|Строковое|Имя, связанное с таблицей \(или представлением\), в которой содержится определение ограничения.|  
|SEARCH\_CONDITION|Строковое|Текст условия поиска проверочного ограничения.|  
|R\_OWNER|Строковое|Владелец таблицы, на которую ссылается ссылочное ограничение.|  
|R\_CONSTRAINT\_NAME|Строковое|Имя определения ограничения уникальности для таблицы, на которую имеется ссылка.|  
|DELETE\_RULE|Строковое|Правило удаления ссылочного ограничения \(CASCADE или NO ACTION\).|  
|STATUS|Строковое|Состояние применения ограничения \(ENABLED или DISABLED\).|  
|DEFERRABLE|Строковое|Допускает ли ограничение задержку.|  
|VALIDATED|Строковое|Подчиняются ли все данные ограничению \(VALIDATED или NOT VALIDATED\).|  
|GENERATED|Строковое|Задано ли имя ограничения пользователем или системой.|  
|BAD|Строковое|Значение YES указывает, что это ограничение задает век неоднозначным образом.  Во избежание ошибок из\-за такой неопределенности перепишите ограничение, используя функцию TO\_DATE с четырехзначным значением года.|  
|RELY|Строковое|Применяется ли включенное ограничение принудительно или нет.|  
|LAST\_CHANGE|DateTime|Время последнего включения или отключения ограничения.|  
|INDEX\_OWNER|Строковое|Имя пользователя, владеющего индексом.|  
|INDEX\_NAME|Строковое|Имя индекса.|  
  
## ForeignKeys  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|PRIMARY\_KEY\_CONSTRAINT\_NAME|Строковое|Имя определения ограничения.|  
|PRIMARY\_KEY\_OWNER|Строковое|Владелец определения ограничения.|  
|PRIMARY\_KEY\_TABLE\_NAME|Строковое|Имя, связанное с таблицей \(или представлением\), в которой содержится определение ограничения.|  
|FOREIGN\_KEY\_OWNER|Строковое|Владелец определения ограничения.|  
|FOREIGN\_KEY\_CONSTRIANT\_NAME|Строковое|Имя определения ограничения.|  
|FOREIGN\_KEY\_TABLE\_NAME|Строковое|Имя, связанное с таблицей \(или представлением\), в которой содержится определение ограничения.|  
|SEARCH\_CONDITION|Строковое|Текст условия поиска проверочного ограничения.|  
|R\_OWNER|Строковое|Владелец таблицы, на которую ссылается ссылочное ограничение.|  
|R\_CONSTRAINT\_NAME|Строковое|Имя определения ограничения уникальности для таблицы, на которую имеется ссылка.|  
|DELETE\_RULE|Строковое|Правило удаления ссылочного ограничения \(CASCADE или NO ACTION\).|  
|STATUS|Строковое|Состояние применения ограничения \(ENABLED или DISABLED\).|  
|VALIDATED|Строковое|Подчиняются ли все данные ограничению \(VALIDATED или NOT VALIDATED\).|  
|GENERATED|Строковое|Задано ли имя ограничения пользователем или системой.|  
|RELY|Строковое|Применяется ли включенное ограничение принудительно или нет.|  
|LAST\_CHANGE|DateTime|Время последнего включения или отключения ограничения.|  
|INDEX\_OWNER|Строковое|Имя пользователя, владеющего индексом.|  
|INDEX\_NAME|Строковое|Имя индекса.|  
  
## ForeignKeyColumns  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец определения ограничения.|  
|CONSTRAINT\_NAME|Строковое|Имя определения ограничения.|  
|TABLE\_NAME|Строковое|Имя таблицы с определением ограничения.|  
|COLUMN\_NAME|Строковое|Имя столбца или атрибута столбца типа объекта, заданного в определении ограничения.|  
|POSITION|Десятичное число|Первоначальная позиция столбца или атрибута в определении объекта.|  
  
## ProcedureParameters  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|OWNER|Строковое|Владелец объекта.|  
|OBJECT\_NAME|Строковое|Имя процедуры или функции.|  
|PACKAGE\_NAME|Строковое|Имя процедуры или функции.|  
|OBJECT\_ID|Десятичное число|Номер объекта, относящийся к объекту.|  
|OVERLOAD|Строковое|Уникальный идентификатор перегруженного варианта.|  
|ARGUMENT\_NAME|Строковое|Имя аргумента.|  
|POSITION|Десятичное число|Позиция в списке аргументов или значение NULL для возвращаемого значения функции.|  
|SEQUENCE|Десятичное число|Последовательность аргументов, включая все уровни вложенности.|  
|DATA\_LEVEL|Десятичное число|Глубины вложенности аргумента для составных типов.|  
|DATA\_TYPE|Строковое|Тип данных аргумента.|  
|DEFAULT\_VALUE|Строковое|Значение аргумента по умолчанию.|  
|DEFAULT\_LENGTH|Десятичное число|Длина значения по умолчанию для аргумента.|  
|IN\_OUT|Строковое|Направление передачи аргумента \(IN, OUT или IN\/OUT\).|  
|DATA\_LENGTH|Десятичное число|Длина столбца в байтах.|  
|DATA\_PRECISION|Десятичное число|Длина в десятичных \(NUMBER\) или двоичных цифрах \(FLOAT\).|  
|DATA\_SCALE|Десятичное число|Количество цифр справа от десятичной точки в числе.|  
|RADIX|Десятичное число|Основание системы счисления аргумента для числа.|  
|CHARACTER\_SET\_NAME|Строковое|Имя кодировки для аргумента.|  
|TYPE\_OWNER|Строковое|Владелец типа аргумента.|  
|TYPE\_NAME|Строковое|Имя типа аргумента.  Если тип представляет собой локальный тип пакета \(т.е. объявлен в спецификации пакета\), то в этом столбце отображается имя пакета.|  
|TYPE\_SUBNAME|Строковое|Является значимым только для локальных типов пакета.  Отображает имя типа, объявленного в пакете, который указан в столбце TYPE\_NAME.|  
|TYPE\_LINK|Строковое|Является значимым только для локальных типов пакета, если пакет, указанный в столбце TYPE\_NAME, является удаленно расположенным пакетом.  В этом столбце отображается канал базы данных, используемый для ссылки на удаленно расположенный пакет.|  
|PLS\_TYPE|Строковое|Применительно к числовым аргументам \- имя типа PL\/SQL аргумента.  В противном случае \- значение NULL.|  
|CHAR\_LENGTH|Десятичное число|Предельное значение количества символов для строковых типов данных.|  
|CHAR\_USED|Строковое|Указывает, используется ли для строки предельное значение в байтах \(B\) или предельное значение в символах \(C\).|  
  
## См. также  
 [Центр разработчиков, поставщики ADO.NET Managed Provider и набор данных](http://go.microsoft.com/fwlink/?LinkId=217917)