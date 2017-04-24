---
title: "Рекомендации по использованию коллекций | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 297b8f1d-b11f-4dc6-960a-8e990817304e
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Рекомендации по использованию коллекций
Можно рассматривать как коллекцию любого типа, разработанные специально для использования нескольких объектов с общими характеристиками. Почти всегда подходит для таких типов для реализации <xref:System.Collections.IEnumerable> или <xref:System.Collections.Generic.IEnumerable%601>, поэтому в этом разделе мы использовать только типы, реализующие один или оба этих интерфейсов для коллекции.  
  
 **X не** использование слабо типизированных коллекций в открытых интерфейсах API.  
  
 Тип возвращаемого значения и параметров, представляющих элементы коллекции должен быть точный тип, не одному из его базовых типов \(это относится только к открытых членов коллекции\).  
  
 **X не** используйте <xref:System.Collections.ArrayList> или <xref:System.Collections.Generic.List%601> в открытых интерфейсах API.  
  
 Эти типы — это структуры данных, предназначенные для использования в внутренней реализации, не в открытых интерфейсах API.`List<T>` оптимизирован для производительности и мощности за счет cleanness API\-интерфейсов и гибкость. Например, если возвращается `List<T>`, никогда нельзя возможность получать уведомления, когда клиентский код изменяет коллекцию. Кроме того `List<T>` предоставляет множество элементов, таких как <xref:System.Collections.Generic.List%601.BinarySearch%2A>, который не полезны или применимо во многих ситуациях. Следующих двух разделах описаны типы \(абстракций\) разработан специально для использования в открытых интерфейсах API.  
  
 **X не** используйте `Hashtable` или `Dictionary<TKey,TValue>` в открытых интерфейсах API.  
  
 Эти типы являются предназначены для использования в реализации внутренних структур данных. Общедоступные API следует использовать <xref:System.Collections.IDictionary>, `IDictionary <TKey, TValue>`, или пользовательский тип, реализующий одного или обоих интерфейсов.  
  
 **X не** использовать <xref:System.Collections.Generic.IEnumerator%601>, <xref:System.Collections.IEnumerator>, или любого другого типа, реализующего любой из этих интерфейсов, за исключением того, как возвращаемый тип `GetEnumerator` метод.  
  
 Типы, отличные от возврат перечислители из методов `GetEnumerator` не может использоваться с `foreach` инструкции.  
  
 **X не** реализовать оба `IEnumerator<T>` и `IEnumerable<T>` на тот же тип. Это же правило применяется для неуниверсальных интерфейсов `IEnumerator` и `IEnumerable`.  
  
## Коллекция параметров  
 **✓ сделать** использовать возможные специализированные наименее тип в качестве типа параметра. Большинство членов занимает коллекций, как использовать параметры `IEnumerable<T>` интерфейса.  
  
 **ИЗБЕЖАТЬ X** с помощью <xref:System.Collections.Generic.ICollection%601> или <xref:System.Collections.ICollection> в качестве параметра только доступ к `Count` свойство.  
  
 Вместо этого рекомендуется использовать `IEnumerable<T>` или `IEnumerable` и динамически проверки, реализует ли объект `ICollection<T>` или `ICollection`.  
  
## Свойства коллекции и возвращаемые значения  
 **X не** предоставляют коллекции можно задать свойства.  
  
 Пользователи могут заменить содержимое коллекции, сначала очисткой коллекции и затем добавив новое содержимое. Если распространенным сценарием является замена всей коллекции, следует рассмотреть возможность создания `AddRange` метод в коллекции.  
  
 **✓ сделать** использовать `Collection<T>` или подкласс `Collection<T>` для свойства или возвращаемого значения представления коллекции для чтения и записи.  
  
 Если `Collection<T>` не соответствует требованиям некоторые \(например, коллекции не должен реализовывать <xref:System.Collections.IList>\), используется реализация пользовательской коллекции `IEnumerable<T>`, `ICollection<T>`, или <xref:System.Collections.Generic.IList%601>.  
  
 **✓ сделать** использовать <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>, подкласс `ReadOnlyCollection<T>`, или, в редких случаях `IEnumerable<T>` для свойства или возвращаемого значения представления коллекции только для чтения.  
  
 Как правило, предпочтение `ReadOnlyCollection<T>`. Если он не соответствует требованиям некоторые \(например, коллекции не должен реализовывать `IList`\), используется реализация пользовательской коллекции `IEnumerable<T>`, `ICollection<T>`, или `IList<T>`. Если реализуется пользовательская коллекция только для чтения, реализовать `ICollection<T>.ReadOnly` возвращает значение false.  
  
 В случаях, когда вы уверены, единственный случай, когда\-нибудь потребуется поддерживать только вперед итерации, можно просто использовать `IEnumerable<T>`.  
  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** вместо использования коллекций подклассов универсальных коллекций базовый.  
  
 Это позволяет для более понятные имена и добавления вспомогательные методы, которые не присутствуют на базовых типов коллекций. Это особенно относится к API высокого уровня.  
  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** возврат подкласс `Collection<T>` или `ReadOnlyCollection<T>` из очень часто используемые методы и свойства.  
  
 Это сделает его можно добавить вспомогательные методы или изменить реализации коллекции в будущем.  
  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** с помощью коллекцию с ключом, если элементы, хранящиеся в коллекции имеют уникальные ключи \(имена, идентификаторы и т. д.\). С ключом коллекции — это коллекции, которые могут быть проиндексированы, целое число и ключ и обычно реализуется путем наследования от класса `KeyedCollection<TKey,TItem>`.  
  
 Коллекции с ключом обычно занимают больше ресурсов памяти и не должен использоваться, если нагрузка на память превосходит преимущества ключи.  
  
 **X не** возвращать значения null из свойства коллекции или методами, возвращающими коллекции. Возвращает пустую коллекцию, или пустой массив.  
  
 Общее правило состоит в null и пустые коллекции \(элемент 0\) или массивы следует обрабатывается так же.  
  
### Моментальные снимки и динамической коллекций  
 Коллекции, представляющие состояние в определенный момент времени называются моментальный снимок коллекции. Например коллекция, содержащая строки, возвращаемые из запроса к базе данных будет моментального снимка. Коллекции, которые всегда представляют текущее состояние, называются динамической коллекций. Например, коллекция `ComboBox` элементы — это динамическая коллекция.  
  
 **X не** возвращают коллекции моментального снимка из свойств. Свойства должны возвращать динамической коллекций.  
  
 Получатели значений свойств должны быть облегченной операции. Возвращение моментального снимка необходимо создать копию во внутреннюю коллекцию в операцией O\(n\).  
  
 **✓ сделать** использовать моментальный снимок коллекции или активной `IEnumerable<T>` \(или его подтипов\) для представления коллекций, которые являются временными \(т. е., можно изменить без явного изменения коллекции\).  
  
 Как правило все коллекции, представляющий общий ресурс \(например, файлы в каталоге\) являются переменными. Такие коллекции — это очень сложно или невозможно реализовать как динамической коллекции, если реализация не просто однопроходные перечислителя.  
  
## Выбор между массивы и коллекции  
 **✓ сделать** предпочтут коллекций и массивов.  
  
 Коллекции обеспечивают больший контроль над содержимым, могут меняться с течением времени и более удобным. Кроме того использование массивов для сценариев только для чтения, не рекомендуется из\-за чрезмерного стоимость клонирование массива. Удобство использования исследования показали, что некоторые разработчики удобнее работать с помощью интерфейсов API на основе коллекций.  
  
 Тем не менее если вы разрабатываете интерфейсам API низкого уровня, возможно, лучше использовать массивы для сценариев чтения и записи. Массивы имеют меньший объем памяти, помогает уменьшить рабочее множество, и доступ к элементам массива выполняется быстрее, поскольку он оптимизирован средой выполнения.  
  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** использование массивов в API низкого уровня к минимуму потребление памяти и повышения производительности.  
  
 **✓ сделать** использовать байтовые массивы вместо коллекций байтов.  
  
 **X не** использование массивов для свойств, если свойство пришлось бы возвращать новый массив \(например, копия внутреннего массива\) при каждом вызове получателя свойства.  
  
## Реализация пользовательских коллекций  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** наследование от `Collection<T>`, `ReadOnlyCollection<T>`, или `KeyedCollection<TKey,TItem>` при разработке новых коллекций.  
  
 **✓ сделать** реализации `IEnumerable<T>` при разработке новых коллекций. Рассмотрите возможность реализации `ICollection<T>` или даже `IList<T>` где имеет смысл.  
  
 При реализации таких пользовательскую коллекцию, соответствуют шаблону API, созданные `Collection<T>` и `ReadOnlyCollection<T>` настолько, насколько возможно. Иными словами явно реализовать те же члены, имена параметров, как эти две коллекции имя каждого из них и т. д.  
  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** реализация интерфейсов неуниверсальных коллекций \(`IList` и `ICollection`\), если коллекция часто передается API\-интерфейсы используя эти интерфейсы в качестве входных данных.  
  
 **ИЗБЕЖАТЬ X** реализация интерфейсов коллекций для типов с помощью сложных интерфейсов API, не относящихся к концепции коллекции.  
  
 **X не** наследовать от неуниверсальных коллекций базовый, такие как `CollectionBase`. Используйте `Collection<T>`, `ReadOnlyCollection<T>`, и `KeyedCollection<TKey,TItem>` вместо.  
  
### Имена пользовательских коллекций  
 Коллекции \(типы, реализующие `IEnumerable`\) создаются в основном по двум причинам: \(1\) для создания новой структуры данных с помощью операций, зависящих от структуры и часто различные характеристики производительности чем существующие структуры данных \(например,  <xref:System.Collections.Generic.List%601>, <xref:System.Collections.Generic.LinkedList%601>, <xref:System.Collections.Generic.Stack%601>\) и \(2\) для создания специализированных коллекции для хранения конкретного набора элементов \(например,  <xref:System.Collections.Specialized.StringCollection>\). Структуры данных, наиболее часто используются в внутренней реализации приложений и библиотек. Специализированные коллекции — это главным образом будет предоставляться в API \(как свойства и типы параметров\).  
  
 **✓ сделать** использовать суффикс «Словарь» в именах реализации абстракций `IDictionary` или `IDictionary<TKey,TValue>`.  
  
 **✓ сделать** используйте суффикс «Коллекции» в именах типы, реализующие `IEnumerable` \(или один из его потомков\) и представляет список элементов.  
  
 **✓ сделать** использовать имя структуры данных для пользовательских структур данных.  
  
 **ИЗБЕЖАТЬ X** использование любой конкретной реализации, такие как «LinkedList» или «Хэш\-таблица», подразумевая, в именах абстракций коллекции.  
  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** префикса имен коллекций с именем типа элемента. Например, коллекция хранения элементов типа `Address` \(реализация `IEnumerable<Address>`\) должен иметь имя `AddressCollection`. Если тип является интерфейсом, буква «I» префикс элемента типа может быть опущено. Таким образом, коллекция <xref:System.IDisposable> элементов может быть вызван `DisposableCollection`.  
  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** использование префикса «ReadOnly» в именах коллекций только для чтения, если соответствующую коллекцию для записи могут быть добавлены или уже существует в структуре.  
  
 Например, должен быть вызван только для чтения коллекцию строк, `ReadOnlyStringCollection`.  
  
 *Частей © 2005, 2009 корпорации Microsoft. Все права защищены.*  
  
 *Воспроизведены разрешении Пирсон образования, Inc. из [Framework рекомендации по проектированию: условные обозначения, стили и шаблоны для повторного использования библиотеки .NET, второе издание](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina и Брэд Абрамс опубликованы 22 октября 2008 г., издательство Addison\-Wesley Professional как часть цикла разработки Microsoft Windows.*  
  
## См. также  
 [Рекомендации по проектированию Framework](../../../docs/standard/design-guidelines/index.md)   
 [Правила использования](../../../docs/standard/design-guidelines/usage-guidelines.md)