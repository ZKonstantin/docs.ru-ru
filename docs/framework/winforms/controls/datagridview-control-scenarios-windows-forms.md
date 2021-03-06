---
title: "Сценарии использования элементов управления DataGridView (Windows Forms) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "данные [Windows Forms], отображения в табличном формате"
  - "таблицы данных, сведения о таблицах данных"
  - "DataGridView - элемент управления [Windows Forms], сценарии"
ms.assetid: 09a5fd05-3447-47ec-a4ec-6082a2b7f0dd
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Сценарии использования элементов управления DataGridView (Windows Forms)
Элемент управления <xref:System.Windows.Forms.DataGridView> позволяет отображать в табличной форме данные из различных источников данных.  В простых случаях можно заполнять <xref:System.Windows.Forms.DataGridView> вручную и управлять данными напрямую через элемент управления.  Однако обычно данные хранятся во внешнем источнике данных, а привязка элемента управления к ним осуществляется через компонент <xref:System.Windows.Forms.BindingSource>.  
  
 В данном разделе описываются наиболее распространенные сценарии, включающие элемент управления <xref:System.Windows.Forms.DataGridView>.  
  
## Сценарий 1. Отображение небольших объемов данных  
 Для отображения в элементе управления <xref:System.Windows.Forms.DataGridView> данные необязательно хранить во внешнем источнике данных.  При работе с небольшими объемами данных можно самостоятельно заполнить элемент управления и управлять данными через элемент управления.  Такой режим называется *несвязанным режимом*.  Дополнительные сведения содержатся в разделе [Практическое руководство. Создание не связанного с данными элемента управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md).  
  
### Ключевые моменты сценария  
  
-   В несвязанном режиме элемент управления заполняется вручную.  
  
-   Несвязанный режим хорошо подходит для работы с небольшими объемами данных, доступных только для чтения.  
  
-   Несвязанный режим также подходит для работы с таблицами с малой степенью заполнения.  
  
## Сценарий 2. Просмотр и обновление данных, которые хранятся во внешнем источнике данных  
 Элемент управления <xref:System.Windows.Forms.DataGridView> можно использовать как пользовательский интерфейс, с помощью которого пользователи осуществляют доступ к данным, хранящимся в источнике данных, таком как таблица базы данных или коллекция бизнес\-объектов.  Дополнительные сведения содержатся в разделе [Практическое руководство. Привязка данных к элементу управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md).  
  
### Ключевые моменты сценария  
  
-   В связанном режиме можно подключаться к источнику данных, автоматически формировать столбцы на основе свойств источника данных или столбцов базы данных, а также автоматически заполнять элемент управления.  
  
-   Cвязанный режим подходит для взаимодействия с большими объемами данных.  Данные можно форматировать для отображения, а синтаксический анализ пользовательских данных может быть выполнен в формате, ожидаемом источником данных.  Ошибки форматирования при вводе данных и ошибки, связанные с ограничением базы данных, могут быть обнаружены, это позволяет предупреждать пользователя и исправлять ошибочные ячейки.  
  
-   Дополнительные функциональные возможности, такие как сортировка, закрепление и изменение порядка столбцов, дают пользователям возможность просматривать данные наиболее удобным способом.  
  
-   Поддержка буфера обмена позволяет копировать данные из собственных приложений в другие приложения.  
  
## Сценарий 3. Дополнительные возможности работы с данными  
 В случае особых требований, выходящих за пределы возможностей стандартной модели привязки данных, можно реализовать *виртуальный режим* для управления взаимодействием между элементом управления и данными.  Реализация виртуального режима означает реализацию одного или нескольких обработчиков событий, позволяющих элементу управления запрашивать сведения о ячейках, когда они требуются.  
  
 Например, чтобы обеспечить оптимальную эффективность при работе с большими объемами данных, можно реализовать виртуальный режим.  Виртуальный режим также удобен для сохранения значений в несвязанных столбцах, которые отображаются вместе со столбцами, извлеченными из другого источника данных.  
  
 Дополнительные сведения о виртуальном режиме содержатся в разделе [Пример. Реализация виртуального режима для элемента управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md).  
  
### Ключевые моменты сценария  
  
-   Виртуальный режим подходит для отображения очень больших объемов данных при необходимости точной настройки производительности.  
  
## Сценарий 4. Автоматическое изменение размера столбцов и строк  
 Можно автоматически изменять размер столбцов и строк при отображении данных, которые регулярно обновляются, для обеспечения видимости всего содержимого.  Элемент управления <xref:System.Windows.Forms.DataGridView> предоставляет несколько параметров, позволяющих включать и выключать возможность изменения размера вручную, изменять размер программными средствами в указанное время или автоматически изменять размер при изменении содержимого.  Дополнительные сведения см. в разделе [Изменение размеров управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md).  
  
### Ключевые моменты сценария  
  
-   Функция изменения размера вручную предоставляет пользователям возможность изменять высоту и ширину ячеек.  
  
-   Автоматическое изменение размера позволяет поддерживать размеры ячеек таким образом, чтобы содержимое ячеек не обрезалось.  
  
-   Программное изменение размера позволяет изменять размеры ячеек в указанное время, чтобы избежать потери производительности при непрерывном автоматическом изменении.  
  
## Сценарий 5. Простая настройка  
 Элемент управления <xref:System.Windows.Forms.DataGridView> предоставляет функциональные возможности, которые позволяют изменять его основной внешний вид и поведение.  Дополнительные сведения см. в разделе [Стили ячеек элемента управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  
  
### Ключевые моменты сценария  
  
-   Объекты <xref:System.Windows.Forms.DataGridViewCellStyle> позволяют предоставлять информацию о цвете, шрифтах, форматировании и размещении на нескольких уровнях и для отдельных элементов в элементе управления.  
  
-   Стили ячеек могут размещаться и совместно использоваться несколькими элементами, позволяя повторно использовать код.  
  
## Сценарий 6. Расширенная настройка  
 Элемент управления <xref:System.Windows.Forms.DataGridView> предоставляет функциональные возможности, которые позволяют настраивать его внешний вид и поведение.  
  
### Ключевые моменты сценария  
  
-   Можно предоставить собственный код окраски ячеек.  Дополнительные сведения содержатся в разделе [Практическое руководство. Настройка внешнего вида ячеек элемента управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md).  
  
-   Можно предоставить собственную окраску строк.  Это полезно, например, для создания строк, содержимое которых объединяет несколько столбцов.  Дополнительные сведения содержатся в разделе [Практическое руководство. Настройка внешнего вида строк элемента управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/customize-the-appearance-of-rows-in-the-datagrid.md).  
  
-   Можно реализовать собственные классы ячеек и столбцов для настройки внешнего вида ячеек.  Дополнительные сведения содержатся в разделе [Практическое руководство. Дополнительные возможности управления внешним видом и поведением ячеек и столбцов элемента управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md).  
  
-   Можно реализовать собственные классы ячеек и столбцов для размещения элементов управления, отличных от предоставляемых встроенными типами столбцов.  Дополнительные сведения содержатся в разделе [Практическое руководство. Размещение элементов управления в ячейках элемента управления DataGridView в Windows Forms](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md).  
  
## См. также  
 <xref:System.Windows.Forms.DataGridView>   
 [Общие сведения об элементе управления DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)