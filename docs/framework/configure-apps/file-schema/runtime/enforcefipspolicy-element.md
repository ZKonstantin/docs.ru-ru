---
title: "Элемент &lt;enforceFIPSPolicy&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<enforceFIPSPolicy> - элемент"
  - "enforceFIPSPolicy - элемент"
  - "Федеральные стандарты обработки информации (FIPS)"
  - "FIPS"
ms.assetid: c35509c4-35cf-43c0-bb47-75e4208aa24e
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Элемент &lt;enforceFIPSPolicy&gt;
Указывает, следует ли включить обязательное исполнение требования конфигурации компьютера, чтобы криптографические алгоритмы соответствовали FIPS.  
  
## Синтаксис  
  
```  
<enforceFIPSPolicy enabled="true|false" />  
```  
  
## Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### Атрибуты  
  
|Атрибут|Описание|  
|-------------|--------------|  
|enabled|Обязательный атрибут.<br /><br /> Указывает, следует ли включить обязательное исполнение требования конфигурации компьютера, чтобы криптографические алгоритмы соответствовали FIPS.|  
  
## Атрибут enabled  
  
|Значение|Описание|  
|--------------|--------------|  
|`true`|Если в соответствии с настройками компьютера необходимо, чтобы криптографические алгоритмы соответствовали стандарту FIPS, это требование реализуется принудительно.  Если класс реализует алгоритм, который не соответствует стандарту FIPS, конструкторы или методы `Create` этого класса создают исключения при выполнении на этом компьютере.  Это значение по умолчанию.|  
|`false`|Алгоритмы шифрования, которые используются приложением, не обязательно должны соответствовать FIPS, вне зависимости от конфигурации компьютера.|  
  
### Дочерние элементы  
 Нет.  
  
### Родительские элементы  
  
|Элемент|Описание|  
|-------------|--------------|  
|`configuration`|Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями платформы .NET Framework.|  
|`runtime`|Элемент, содержащий сведения о привязке сборок и сборке мусора.|  
  
## Заметки  
 Начиная с версии .NET Framework 2.0, создание классов, которые реализуют алгоритмы шифрования контролируется конфигурацией компьютера.  Если в соответствии с настройками компьютера необходимо, чтобы алгоритмы соответствовали стандарту FIPS, и класс реализует алгоритм, который не соответствует стандарту FIPS, любая попытка создать экземпляр этого класса вызывает исключение.  Конструкторы вызывают исключение <xref:System.InvalidOperationException>, а методы `Create` вызывают исключение <xref:System.Reflection.TargetInvocationException> с внутренним исключением <xref:System.InvalidOperationException>.  
  
 Если приложение выполняется на компьютерах, конфигурации которых требуют соблюдения FIPS, и приложение использует алгоритм, не соответствующий стандарту FIPS, можно использовать в файле конфигурации этот элемент, чтобы предотвратить принудительное соблюдение FIPS для среды CLR.  Этот элемент был представлен в [!INCLUDE[net_v20SP1_long](../../../../../includes/net-v20sp1-long-md.md)].  
  
## Пример  
 В следующем примере показано, как не позволить среде CLR принудительно применять соответствие FIPS.  
  
```  
<configuration>  
    <runtime>  
        <enforceFIPSPolicy enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## См. также  
 [Схема параметров среды выполнения](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Схема файла конфигурации](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Cryptography Model](../../../../../docs/standard/security/cryptography-model.md)