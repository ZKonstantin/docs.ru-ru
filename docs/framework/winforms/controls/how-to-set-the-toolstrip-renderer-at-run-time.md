---
title: "Практическое руководство. Назначение средства визуализации компоненту ToolStrip во время выполнения | Microsoft Docs"
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
  - "MenuStrip - элемент управления [Windows Forms]"
  - "панели инструментов [Windows Forms]"
  - "ToolStrip - элемент управления [Windows Forms]"
  - "ToolStripManager - класс [Windows Forms]"
  - "ToolStripProfessionalRenderer - класс [Windows Forms]"
ms.assetid: 525e2347-0804-49aa-b9a3-9b2cabbf1c35
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Практическое руководство. Назначение средства визуализации компоненту ToolStrip во время выполнения
С помощью пользовательского класса `ProfessionalColorTable` можно настраивать внешний вид элемента управления <xref:System.Windows.Forms.ToolStrip>.  
  
## Пример  
 В примере кода ниже показано создание пользовательского класса `ProfessionalColorTable`.  Этот класс определяет градиент для элементов управления <xref:System.Windows.Forms.MenuStrip> и <xref:System.Windows.Forms.ToolStrip>.  
  
 Чтобы использовать этот пример, выполните компиляцию и запуск приложения, после чего нажмите **Change Colors** \(Изменить цвета\) для применения градиентов, определенных в классе `ProfessionalColorTable`.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#1)]  
[!code-csharp[System.Windows.Forms.ToolStrip.Misc#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#20)]
[!code-vb[System.Windows.Forms.ToolStrip.Misc#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#20)]  
  
## Определение пользовательского класса ProfessionalColorTable  
 Пользовательские градиенты определяются в классе `CustomProfessionalColors`.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#30)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#30)]  
  
## Назначение пользовательского средства отрисовки  
 Создайте новое средство отрисовки `ToolStripProfessionalRenderer` с классом `CustomProfessionalColors` и присвойте его свойству <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=fullName>.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#22)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#22)]  
  
## Компиляция кода  
 Для этого примера требуются:  
  
-   ссылки на сборки System.Design, System.Drawing и System.Windows.Forms.  
  
 Информацию о выполнении сборки этого примера из командной строки для [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] или [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] можно найти в разделе [Построение из командной строки](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) или [Построение из командной строки с помощью csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  Чтобы выполнить сборку этого примера в [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], можно также вставить код в новый проект.  См. также [Практическое руководство. Компиляция и выполнение скомпилированного примера кода формы Windows Forms с помощью Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## См. также  
 <xref:System.Windows.Forms.ToolStripManager>   
 <xref:System.Windows.Forms.ProfessionalColorTable>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripProfessionalRenderer>   
 [Элемент управления ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)