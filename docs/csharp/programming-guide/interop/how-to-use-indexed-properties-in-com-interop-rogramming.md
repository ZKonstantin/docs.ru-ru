---
title: "Практическое руководство. Использование индексированных свойств в программировании COM-взаимодействия (руководство по программированию на C#) | Документы Майкрософт"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- indexed properties [C#]
- Office programming [C#], indexed properties
- properties [C#], indexed
ms.assetid: 756bfc1e-7c28-4d4d-b114-ac9288c73882
caps.latest.revision: 20
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: ae550ba7d3f2767cf7cc64a14bc177d15f426c36
ms.contentlocale: ru-ru
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-use-indexed-properties-in-com-interop-programming-c-programming-guide"></a>Практическое руководство. Использование индексированных свойств в программировании COM-взаимодействия (Руководство по программированию на C#)
*Индексированные свойства* делают использование свойств COM с параметрами при программировании на C# более удобным. Индексированные свойства используются совместно с другими компонентами, представленными в Visual C#, например [именованными и необязательными аргументами](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md), новым типом ([dynamic](../../../csharp/language-reference/keywords/dynamic.md)) и [внедренными сведениями о типах](../../../csharp/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md) для расширения возможностей программирования для Microsoft Office.  
  
 В более ранних версиях C# методы доступны как свойства только при условии, что у метода `get` нет параметров, а у метода `set` есть только один параметр значения. Однако не все свойства COM удовлетворяют этим ограничениям. Например, свойство [Range](http://go.microsoft.com/fwlink/?LinkId=166053) Excel имеет метод доступа `get`, которому требуется параметр для имени диапазона. Раньше из-за отсутствия возможности прямого обращения к свойству `Range` приходилось использовать вместо этого метод `get_Range`, как показано в следующем примере.  
  
 [!code-cs[csProgGuideIndexedProperties#1](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_1.cs)]  
  
 Индексированные свойства позволяют вместо этого использовать следующий код:  
  
 [!code-cs[csProgGuideIndexedProperties#2](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_2.cs)]  
  
> [!NOTE]
>  В предыдущем примере также используются [необязательные аргументы](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md), которые позволяют опустить `Type.Missing`.  
  
 Аналогичным образом, чтобы задать значение свойства `Value` объекта [Range](https://msdn.microsoft.com/library/microsoft.office.interop.excel.range.aspx) в Visual C# 2008 и более ранних версиях, требуется два аргумента. Один предоставляет аргумент для необязательного параметра, указывающего тип значения диапазона. Другой предоставляет значение для свойства `Value`. Эти методы показаны в следующих примерах. В примерах ячейке A1 задается значение `Name`.
  
 [!code-cs[csProgGuideIndexedProperties#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_3.cs)]  
  
 Индексированные свойства позволяют вместо этого использовать следующий код.  
  
 [!code-cs[csProgGuideIndexedProperties#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_4.cs)]  
  
 Разработчики не могут создавать собственные индексированные свойства. Эта возможность поддерживает только использование имеющихся индексированных свойств.  
  
## <a name="example"></a>Пример  
 Ниже приведен полный пример кода. Дополнительные сведения о создании проекта, обращающегося к Office API, см. в разделе [Практическое руководство. Доступ к объектам взаимодействия Office с помощью функций языка Visual C#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md).  
  
 [!code-cs[csProgGuideIndexedProperties#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_5.cs)]  
  
## <a name="see-also"></a>См. также  
 [Именованные и необязательные аргументы](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [Динамический](../../../csharp/language-reference/keywords/dynamic.md)   
 [Использование типа dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Практическое руководство. Использование именованных и необязательных аргументов в программировании приложений Office](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)   
 [Практическое руководство. Доступ к объектам взаимодействия Office с помощью функций языка Visual C#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)   
 [Walkthrough: Office Programming](../../../csharp/programming-guide/interop/walkthrough-office-programming.md) (Пошаговое руководство. Программирование приложений Office)
