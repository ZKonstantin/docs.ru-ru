---
title: "&lt;sendMessageChannelCache&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 241e428e-5030-4b13-8a0a-69f05288d3d9
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;sendMessageChannelCache&gt;
Поведение службы, которое позволяет изменить уровни доступа к кэшу, параметры кэша фабрики канала и параметры кэша канала для рабочих процессов, которые отправляют сообщения в конечные точки служб с использованием действий отправки сообщений.  
  
## Синтаксис  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
       <sendMessageChannelCache allowUnsafeCaching="Boolean" >          
           <channelSettings idleTimeout="TimeSpan" leaseTimeout="TimeSpan" maxItemsInCache="Integer" />  
           <factorySettings idleTimeout="TimeSpan" leaseTimeout="TimeSpan" maxItemsInCache="Integer" />  
       </sendMessageChannelCache>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### Атрибуты  
  
|Атрибут|Описание|  
|-------------|--------------|  
|allowUnsafeCaching|Логическое значение, указывающее, следует ли включить кэширование.  Если служба рабочего процесса имеет пользовательские привязки или поведения, то кэширование может оказаться небезопасным \(и будет отключено по умолчанию\).  Однако если кэширование необходимо включить, то установите это свойство в значение **true**.|  
  
### Дочерние элементы  
  
|Элемент|Описание|  
|-------------|--------------|  
|[\<channelSettings\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/channelsettings.md)|Указывает параметры кэша канала.|  
|[\<factorySettings\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/factorysettings.md)|Указывает параметры кэша фабрики канала.|  
  
### Родительские элементы  
  
|Элемент|Описание|  
|-------------|--------------|  
|[\<behavior\> для \<serviceBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md)|Указывает элемент поведения.|  
  
## Заметки  
 Это поведение службы предназначено для рабочих процессов, отправляющих сообщения в конечные точки служб.  Эти рабочие процессы обычно являются клиентскими, но также могут быть службами рабочих процессов, размещенными в <xref:System.ServiceModel.WorkflowServiceHost>.  
  
 По умолчанию в рабочем процессе, размещенном в <xref:System.ServiceModel.WorkflowServiceHost>, кэш, используемый действиями обмена сообщениями <xref:System.ServiceModel.Activities.Send>, совместно используется всеми экземплярами рабочих процессов в <xref:System.ServiceModel.WorkflowServiceHost> \(кэширование уровня узла\).  Для клиентского рабочего процесса, не размещенного в <xref:System.ServiceModel.WorkflowServiceHost>, кэш доступен только для экземпляра рабочего процесса \(кэширование уровня экземпляра\).  По умолчанию кэширование отключено для всех действий отправки в рабочем процессе, в конфигурации которого определены конечные точки.  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] том, как изменять уровни совместного использования кэша по умолчанию, а также настройки кэша для фабрики каналов и кэша каналов, см. в разделе [Изменение уровней совместного использования кэша для действий «Send»](../../../../../docs/framework/wcf/feature-details/changing-the-cache-sharing-levels-for-send-activities.md).  
  
## Пример  
 В размещенной службе рабочего процесса в файле конфигурации приложения можно указать параметры кэша фабрики и канала.  Для этого необходимо создать поведение службы, содержащее параметры для кэша фабрики и канала, и добавить это поведение в службу.  В следующем примере показано содержимое файла конфигурации, в котором находится поведение службы **MyChannelCacheBehavior**  с пользовательскими параметрами кэша фабрики и канала.  Это поведение службы добавляется к службе посредством атрибута **behaviorConfiguarion** .  
  
```  
  
<configuration>    
  <system.serviceModel>  
    <!-- List of other config sections here -->   
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="MyChannelCacheBehavior">  
          <sendMessageChannelCache allowUnsafeCaching ="false" >  
            <!-- Control only the host level settings -->   
            <factorySettings maxItemsInCache = "8" idleTimeout = "00:05:00" leaseTimeout="10:00:00" />  
            <channelSettings maxItemsInCache = "32" idleTimeout = "00:05:00" leaseTimeout="00:06:00" />  
          </sendMessageChannelCache>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="MyService" behaviorConfiguration="MyChannelCacheBehavior" />  
    </services>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## См. также  
 <xref:System.ServiceModel.Activities.SendMessageChannelCache>   
 <xref:System.ServiceModel.Activities.Configuration.SendMessageChannelCacheElement>   
 <xref:System.ServiceModel.Activities.Send>   
 [Изменение уровней совместного использования кэша для действий «Send»](../../../../../docs/framework/wcf/feature-details/changing-the-cache-sharing-levels-for-send-activities.md)