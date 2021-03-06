---
title: "Обзор локализуемости | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "международные приложения, локализуемость"
  - "разработка приложений [платформа .NET Framework], локализация"
  - "локализуемость [платформа .NET Framework]"
  - "международные приложения [платформа .NET Framework], локализуемость"
  - "глобализация [платформа .NET Framework], локализуемость"
  - "язык и региональные параметры, локализуемость"
  - "локализация [платформа .NET Framework], локализуемость"
  - "глобальные приложения, локализуемость"
  - "локализация ресурсов"
ms.assetid: 3aee2fbb-de47-4e37-8fe4-ddebb9719247
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Обзор локализуемости
Проверка локализуемости \- промежуточный шаг в разработке международных приложений.  Он проверяет, что распространяющееся в глобальном масштабе приложение готово для локализации и определяет код или элементы интерфейса пользователя, которые требуют специальной обработки.  Этот шаг также помогает удостовериться, что процесс локализации не внесет никаких функциональных дефектов в приложение.  Когда все проблемы, вызванные анализом локализуемости, рассмотрены, приложение готово для локализации.  Если проверка локализуемости проведена тщательно, нет необходимости изменять исходный код в процессе локализации.  
  
 Анализ локализуемости состоит из трёх следующих проверок:  
  
-   [Реализованы ли рекомендации по глобализации?](#global)  
  
-   [Правильно ли обрабатываются функции, чувствительные к языковым и региональным параметрам?](#culture)  
  
-   [Проводилось ли тестирование приложения с использованием данных на других языках?](#test)  
  
<a name="global"></a>   
## Реализация рекомендаций по глобализации  
 Если при проектировании и разработке приложения помнить о локализации, и если были выполнены рекомендации, описанные в статье [Глобализация](../../../docs/standard/globalization-localization/globalization.md), проверка локализуемости будет гарантировать качественную локализацию.  С другой стороны, во время этого шага необходимо просмотреть и реализовать рекомендации по [глобализации](../../../docs/standard/globalization-localization/globalization.md)и исправить ошибки в исходном коде, которые препятствуют локализации.  
  
<a name="culture"></a>   
## Обработка функций, чувствительных к языковым и региональным параметрам  
 Платформа .NET Framework не обеспечивает программную поддержку в нескольких областях, которые значительно различаются в зависимости от языка и региональных параметров.  В большинстве случаев необходимо написать пользовательский код для обработки функциональных областей следующим образом:  
  
-   Адреса.  
  
-   Телефонные номера.  
  
-   Размер бумаги.  
  
-   Единицы измерения, используемые для длины, веса, площади, объема и температур.  Хотя платформа .NET Framework не обеспечивает встроенную поддержку для преобразования между единицами измерения, можно использовать свойство <xref:System.Globalization.RegionInfo.IsMetric%2A?displayProperty=fullName>, чтобы определить использует ли определенная страна или регион метрическую систему, как показано в следующем примере.  
  
     [!code-csharp[Conceptual.Localizability#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.localizability/cs/ismetric1.cs#1)]
     [!code-vb[Conceptual.Localizability#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.localizability/vb/ismetric1.vb#1)]  
  
<a name="test"></a>   
## Тестирование приложения  
 Перед локализацией приложения необходимо протестировать его с использованием данных на других языках на международных версиях операционной системы.  Хотя большая часть интерфейса пользователя не будет локализирована на этом этапе, можно будет обнаружить следующие проблемы:  
  
-   Сериализованные данные, которые не будут правильно десериализованы в разных версиях операционной системы.  
  
-   Числовые данные, которые не отражают соглашения текущего языка и региональных параметров.  Например, числа могут быть отображены с неверными разделителями групп, десятичными разделителями, или символами валют.  
  
-   Сведения о дате и времени, которые не отражают правил текущего языка и региональных параметров.  Например, числа, которые представляют месяц и день могут следовать в неверном порядке, могут быть неправильными разделители компонентов даты или данные часового пояса.  
  
-   Ресурсы, которые не удается найти, поскольку не был указан язык по умолчанию для приложения.  
  
-   Строки, которые отображаются в нестандартном порядке для конкретного языка.  
  
-   Сравнения строк или сравнения на равенство, возвращающие непредвиденные результаты.  
  
 Если при разработке приложения были выполнены рекомендации по глобализации; верно обработаны функции, чувствительные к языковым и региональным параметрам; определены и решены проблемы локализации, которые возникли во время тестирования, можно перейти к следующему шагу: [Локализация](../../../docs/standard/globalization-localization/localization.md).  
  
## См. также  
 [Глобализация и локализация](../../../docs/standard/globalization-localization/index.md)   
 [Локализация](../../../docs/standard/globalization-localization/localization.md)   
 [Глобализация](../../../docs/standard/globalization-localization/globalization.md)   
 [Ресурсы в приложениях для настольных систем](../../../docs/framework/resources/index.md)