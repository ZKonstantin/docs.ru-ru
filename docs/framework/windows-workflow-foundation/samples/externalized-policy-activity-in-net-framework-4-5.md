---
title: "Реализованное действие политики в .NET Framework 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92fd6f92-23a1-4adf-b96a-2754ea93ad3e
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Реализованное действие политики в .NET Framework 4.5
Этот образец демонстрирует, как с помощью действия ExternalizedPolicy4 можно выполнять существующие объекты [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] [!INCLUDE[wf2](../../../../includes/wf2-md.md)] \(WF 3.5\) <xref:System.Workflow.Activities.Rules.RuleSet> непосредственно в [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] [!INCLUDE[wf2](../../../../includes/wf2-md.md)] \(WF 4.5\), используя для этого обработчик правил, входящий в комплект поставки WF 3.5.Используя это действие, можно создавать и выполнять любой существующий набор правил <xref:System.Workflow.Activities.Rules.RuleSet> WF 3.5.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] обработчике правил WF 3.5, являющемся частью Windows Workflow Foundation, см. в разделе [Введение в обработчик правил в Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=166079).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] правилах миграции на [!INCLUDE[wf1](../../../../includes/wf1-md.md)] в [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] см. в инструкции по миграции [Руководство по миграции](../../../../docs/framework/windows-workflow-foundation//migration-guidance.md).  
  
## Проекты в этом образце  
  
||||  
|-|-|-|  
|Имя проекта|Описание|Основные файлы|  
|ExternalizedPolicy4|Содержит действие PolicyExternalizedPolicy4 и его конструктор WF 4.5.|**ExternalizedPolicy4.cs**: определение действия.<br /><br /> **ExternalizedPolicy4Designer.xaml**: пользовательский конструктор действия ExternalizedPolicy4.Он использует редактор правил \(<xref:System.Workflow.Activities.Rules.Design.RuleSetDialog>\), определенный в конструкторе правил WF 3.5.|  
|ImperativeCodeClientSample|Образец клиентского приложения, осуществляющего конфигурирование и запуск рабочего процесса с использованием приложения PolicyExternalizedPolicy4, использующего императивный код C\# \(конструктор не используется\).|**ApplyDiscount.rules**: Файл с определениями правил [!INCLUDE[wf1](../../../../includes/wf1-md.md)].<br /><br /> **Order.cs**: Тип, представляющий заказ клиента.Правила применяются к объектам этого типа.<br /><br /> **Program.cs**: Настраивает и запускает рабочий процесс с действием Policy4 для применения правил, определенных в ApplyDiscount.rules, к экземплярам объектов Order.<br /><br /> App.config: файл конфигурации, содержащий путь к файлу правил.|  
|DesignerClientSample|Образец клиентского приложения, осуществляющего конфигурирование и запуск рабочего процесса с использованием приложения ExternalPolicy4 в конструкторе [!INCLUDE[wf1](../../../../includes/wf1-md.md)].|**Sequence1.xaml**: Последовательный рабочий процесс, использующий действие Policy4 для проверки правил.<br /><br /> **Program.cs**: Выполняет экземпляр рабочего процесса, определенного в Sequence1.xaml.|  
  
## Действие ExternalizedPolicy4  
 Действие ExternalizedPolicy4 представляет собой действие <xref:System.Activities.NativeActivity>, позволяющее выполнять объекты WF 3.5 <xref:System.Workflow.Activities.Rules.RuleSet> в рамках рабочих процессов WF 4.5.Следующий пример кода представляет собой упрощенное определение публичной объектной модели действия.  
  
```  
public class ExternalizedPolicy4Activity<TResult>: CodeActivity  
{  
    public string RulesFilePath   
  
    public string RuleSetName           
  
    [RequiredArgument]  
    public InArgument<T> TargetObject   
  
    [RequiredArgument]  
    public OutArgument<T> ResultObject   
  
    public OutArgument<ValidationErrorCollection> ValidationErrors   
}  
```  
  
|||  
|-|-|  
|Свойство|Описание|  
|RuleSetFilePath|Путь к файлу <xref:System.Workflow.Activities.Rules.RuleSet> в .NET Framework 3.5, который определяется при выполнении действия.|  
|RuleSetName|Имя <xref:System.Workflow.Activities.Rules.RuleSet>, которое будет использоваться в файлах правил с расширением RULES.|  
|TargetObject|Объект, для которого рассчитываются объекты <xref:System.Workflow.Activities.Rules.Rule> в <xref:System.Workflow.Activities.Rules.RuleSet>.|  
|ResultObject|Результирующий объект, полученный после применения правил \(например, правил, примененных к входному аргументу\), с сохранением результата в результирующем аргументе.|  
|ValidationError|Список ошибок проверки, возвращаемый обработчиком правил WF 3.5 при проверке класса <xref:System.Workflow.Activities.Rules.RuleSet> для целевого объекта до его выполнения.|  
  
## Конструктор действия ExternalizedPolicy4  
 Конструктор действия ExternalizedPolicy4 позволяет конфигурировать активность таким образом, чтобы использовать существующий набор правил без необходимости написания кода.Достаточно просто задать путь к файлу с расширением RULES и указать желаемое имя <xref:System.Workflow.Activities.Rules.RuleSet>.Конструктор также позволяет вносить изменения в <xref:System.Workflow.Activities.Rules.RuleSet>.После построения решения действие будет занесено в область элементов в раздел Microsoft.Samples.Activities.Rules.Конструктор позволяет выбирать файл с расширением RULES и <xref:System.Workflow.Activities.Rules.RuleSet>.При нажатии кнопки **Изменить набор правил** на экран будет выведено диалоговое окно WF 3.5 <xref:System.Workflow.Activities.Rules.Design.RuleSetDialog>.Это диалоговое окно представляет собой повторно размещенный редактор правил WF 3.5, используемый для просмотра и изменения правил, выполняемых действием ExternalizedPolicy4.  
  
## Policy4 и ExternalPolicy4  
 Действие [Действие политики в .NET Framework 4.5](../../../../docs/framework/windows-workflow-foundation/samples/policy-activity-in-net-framework-4-5.md) позволяет создавать и выполнять набор правил .NET Framework 3.5 в рамках рабочего процесса WF 4.5.Набор правил <xref:System.Workflow.Activities.Rules.RuleSet> сериализуется в рамках определения действия Policy4 в языке XAML.Образец действия ExternalizedPolicy4 показывает, как использовать существующий внешний набор правил <xref:System.Workflow.Activities.Rules.RuleSet> \(содержащийся в файле с расширением RULES\).  
  
## Использование этого образца  
 Для запуска этого образца специальные настройки не требуются.Откройте решение в среде [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] и нажмите клавишу F5 для запуска приложения.  
  
 Этот образец содержит два клиентских приложения: ImperativeCodeClientSample и DesignerClientSample.Клиентское приложение ImperativeCodeClientSample показывает, как конфигурировать и запускать действие ExternalizedPolicy4 с использованием императивного кода C\#.Клиентское приложение DesignerClientSample показывает, как конфигурировать и запускать действие ExternalizedPolicy4 с использованием конструктора.  
  
#### Запуск клиентского приложения ImperativeCodeClientSample  
  
1.  Откройте файл решения Policy4sample.sln в среде [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  В окне **Обозреватель решений** щелкните правой кнопкой мыши проект **ImperativeCodeClientSample** и выберите команду **Назначить запускаемым проектом**.  
  
3.  Чтобы запустить проект, нажмите клавиши CTRL\+F5.  
  
#### Нажмите клавишу F5, чтобы запустить приложение DesignerClientSample.  
  
1.  Откройте файл решения Policy4sample.sln в среде [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  В окне **Обозреватель решений** щелкните правой кнопкой мыши проект **DesignerClientSample** и выберите команду **Назначить запускаемым проектом**.  
  
3.  Чтобы скомпилировать проект, нажмите сочетание клавиш CTRL\+SHIFT\+B.  
  
4.  Чтобы запустить проект, нажмите клавиши CTRL\+F5.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Rules-ExternalizedPolicy4`