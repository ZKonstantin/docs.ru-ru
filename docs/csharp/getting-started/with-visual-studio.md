---
title: "Создание приложения Hello World на C# с помощью .NET Core в Visual Studio 2017 | Microsoft Docs"
description: "Узнайте, как создать простое консольное приложение .NET Core с помощью Visual Studio 2017."
keywords: ".NET Core, консольное приложение .NET Core, Visual Studio 2017"
author: BillWagner
ms.author: wiwagn
ms.date: 05/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 97aa50bf-bdf8-416d-a56c-ac77504c14ea
ms.translationtype: Human Translation
ms.sourcegitcommit: 4437ce5d344cf06d30e31911def6287999fc6ffc
ms.openlocfilehash: 08c8e18a95c25477eb81bd6df10cf593b284bf64
ms.contentlocale: ru-ru
ms.lasthandoff: 05/23/2017

---

<a id="building-a-c-hello-world-application-with-net-core-in-visual-studio-2017" class="xliff"></a>
# Создание приложения "Hello World" на C# с помощью .NET Core в Visual Studio 2017

В этой статье содержится пошаговое описание процессов построения, отладки и публикации простого консольного приложения .NET Core с помощью Visual Studio 2017. Visual Studio 2017 предоставляет полнофункциональную среду для разработки приложений .NET Core. Если само приложение не имеет зависимостей от конкретной платформы, его можно выполнять на любой официально поддерживаемой платформе .NET Core и в любой системе, в которой установлена .NET Core.

<a id="prerequisites" class="xliff"></a>
## Предварительные требования

[Visual Studio 2017](https://www.visualstudio.com/downloads/) с установленной рабочей нагрузкой "Кроссплатформенная разработка .NET Core". 

Дополнительные сведения см. в разделе [Необходимые компоненты для .NET Core в Windows](../../core/windows-prerequisites.md).

<a id="a-simple-hello-world-application" class="xliff"></a>
## Простое приложение Hello World

Для начала создадим простое консольное приложение Hello World. Выполните следующие действия.

1. Запустите Visual Studio 2017. Выберите **Файл** > **Создать** > **Проект** в меню. В диалоговом окне **Добавление нового проекта** выберите узел **.NET Core**, а затем — шаблон проекта **Консольное приложение (.NET Core)**. В текстовом поле **Имя** введите "HelloWorld". Нажмите кнопку **OK**.

   ![Диалоговое окно создания проекта, в котором выбран шаблон проекта консольного приложения](./media/with-visual-studio/newproject.png)
   
1. Visual Studio загружает среду разработки. Шаблон консольного приложения C# для .NET Core автоматически определяет класс `Program` с одним методом `Main`, который принимает в качестве аргумента массив <xref:System.String>. `Main` — точка входа в приложение. Это метод, который автоматически вызывается средой выполнения при запуске приложения. Все аргументы, предоставленные в командной строке при запуске приложения, доступны через массив *args*.

   ![Visual Studio и новый проект Hello World](./media/with-visual-studio/devenv.png)

   Этот шаблон создает простое приложение Hello World. Он вызывает метод <xref:System.Console.WriteLine(System.String)?displayProperty=fullName> для отображения литеральной строки "Hello World!" в окне консоли. Запустите программу в режиме отладки, нажав на панели инструментов кнопку **HelloWorld** с зеленой стрелкой. Окно консоли появится на короткое время и затем сразу же закроется. Это происходит потому, что метод `Main` и приложение в целом завершаются сразу же, как только будет выполнена единственная инструкция в методе `Main`.

1. Чтобы приостановить приложение перед тем, как закроется окно консоли, добавьте следующий код сразу после вызова метода <xref:System.Console.WriteLine(System.String)?displayProperty=fullName>:

   ```csharp
   Console.Write("Press any key to continue...");
   Console.ReadKey(true);
   ```
   Этот код предлагает пользователю нажать любую клавишу и приостанавливает работу программы до нажатия клавиши.

1. В строке меню выберите **Сборка** > **Собрать решение**. При этом программа компилируется в промежуточный язык IL, который затем преобразуется в двоичный код JIT-компилятором.

1. Запустите программу, нажав кнопку **HelloWorld** с зеленой стрелкой на панели инструментов.

   ![Окно консоли с приложением Hello World и надписью "Чтобы продолжить, нажмите любую клавишу"](./media/with-visual-studio/helloworld1.png)

1. Для закрытия консольного окна нажмите любую клавишу.

<a id="enhancing-the-hello-world-application" class="xliff"></a>
## Расширение приложения Hello World

Давайте расширим приложение. Теперь у пользователя будет запрашиваться имя, которое затем будет отображаться с датой и временем. Выполните следующие действия, чтобы изменить и протестировать программу.

1. Введите следующий код C# в окно редактирования кода между первой открывающей скобкой за строкой `public static void Main(string[] args)` и первой закрывающей скобкой:

   [!code-csharp[GettingStarted#1](../../../samples/snippets/csharp/getting_started/with_visual_studio/helloworld.cs#1)]

   ![Файл C# Visual Studio с обновленным методом Main](./media/with-visual-studio/codewindow.png)

   Теперь код выдает строку "What is your name?" (Как вас зовут?) в окно консоли и ожидает, чтобы пользователь ввел строку текста и нажал клавишу ВВОД. Приложение сохраняет полученную строку в переменной с именем `name`. Оно также получает значение свойства <xref:System.DateTime.Now?displayProperty=fullName>, которое содержит текущее локальное время, и присваивает его переменной с именем `date`. Наконец, с помощью [строки составного формата](../../standard/base-types/composite-format.md) эти значения выводятся в окно консоли.

1. Скомпилируйте программу, выбрав действие **Сборка** > **Собрать решение**.

1. Запустите программу в режиме отладки, выбрав на панели инструментов кнопку с зеленой стрелкой, нажав клавишу F5 или выбрав пункт меню **Отладка** > **Начать отладку**. В ответ на приглашение в командной строке введите имя и нажмите клавишу ВВОД.

   ![Окно консоли с измененными выходными данными программы](./media/with-visual-studio/helloworld2.png)

1. Для закрытия консольного окна нажмите любую клавишу.

Вы создали и запустили приложение. Чтобы приложение достигло профессионального уровня, нужно выполнить еще несколько шагов для подготовки приложения к выпуску:

- Сведения об отладке приложения см. в разделе [Отладка приложения Hello World на C# в Visual Studio 2017](debugging-with-visual-studio.md).

- Сведения о разработке и публикации распространяемой версии приложения см. в разделе [Публикация приложения Hello World с помощью Visual Studio 2017](publishing-with-visual-studio.md).

<a id="related-topics" class="xliff"></a>
## См. также

Вместо консольного приложения .NET Core и Visual Studio 2017 позволяют создать библиотеку классов. Пошаговое описание этого процесса вы найдете в статье [Building a class library with C# and .NET Core in Visual Studio 2017](library-with-visual-studio.md) (Создание библиотеки классов с помощью C# и .NET Core в Visual Studio 2017).

Для разработки консольных приложений .NET Core для Mac, Linux и Windows также можно использовать редактор кода [Visual Studio Code](https://code.visualstudio.com/). Пошаговые инструкции см. в статье [Getting Started with Visual Studio Code](with-visual-studio-code.md) (Приступая к работе с Visual Studio Code).

