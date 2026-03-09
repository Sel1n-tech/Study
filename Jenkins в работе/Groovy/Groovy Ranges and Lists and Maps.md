## List

**Список** - структура данных, представляет собой упорядоченный набор данных(значения могут повторяться и быть разных типов данных). Groovy lang содержит встроенную поддержку списков. Groovy использует список значений, разделенных запятыми, заключенных в квадратные скобки, для обозначения списков. В Groovy список содержит последовательность ссылок на объекты. Ссылки на объекты в списке занимают позицию в последовательности и различаются целочисленным индексом. Литерал списка представляет собой серию объектов, разделенных запятыми и заключенных в квадратные скобки. Списки Groovy — это обычный JDK java.util.List, поскольку Groovy не определяет свои собственные классы коллекций. 

Определяем список цифр, разделенных запятыми и заключенных в квадратные скобки, и присваиваем этот список переменной, это будет однородный список, потому что содержит все элементы одного типа данных:

```java
def numbers = [0, 1, 2, 3, 4]
println numbers[0]  // обращение к элементу по индексу
  
def empty = []  // Создание пустого списка
```

Размер списка можно запросить с помощью метода size(), и он вернет нам 5, это означает что в нем хранится пять элементов.

А вот пример разнородного списка, в котором будут содержаться целые числа, строка и логическое значение

```java
def numbers = [0, 1, "Hello", 3, true]  
```

![](https://ucarecdn.stepik.net/59b77038-9b47-445c-8170-925399409ca3/)

Чтобы обрабатывать данные в списке, мы должны иметь доступ к отдельным элементам. Списки Groovy индексируются с помощью оператора индексации **[ ]** . Индексы списка начинаются с нуля, что означает первый элемент.

![](https://lh3.googleusercontent.com/C4frXO77_Pa50qbJoMKh63ROS0kxHPPaLjAwcstyuYXei5Vfmaz5g1WmOBR56bZVRRWV6gBv0Ov2_ZYeSp9wtza0jhUS0fSWSUhmSsYzXZ0Oc9vNEg0OQMeIqynvV3afHa1vmle538BhImtfbjzbsQ)

  
Рассмотрим следующий объект List, идентифицированный как числа, и некоторый пример доступа к List.Если целочисленный индекс отрицательный, то он относится к элементам, считая с конца.

![](https://lh4.googleusercontent.com/Qd8uCMYyMqWz3KuDxsg779-Xq2SZdHdMO4oFSfYmsv_ui-jC5ClchJa9qyE_GPu0nTY_Hiu6Lrd4Few_PzYNp55egj9s7V12RpOEbeFcJnvlYp7XZdtLF4kcHYHdw2ghetQdnOfV9JTB5B6Upuk77Q)

![](https://lh3.googleusercontent.com/aw1DvV9QAoJSF1GrudhuWLS7QmqJqJWIdMBNsuOrj-oxvLxZ6bPromneN-QD7xJzsNKzCHsMiSUrmJMU7Rp4dn6_uW7vogZi3yjJzzrL0jhFkWfz1MAXkWMeOOE79058gll3H95KvPpP4GwlDg718Q)

Таким образом, оператор [] - это метод getAt, определенный в классе List. Следовательно, помимо ссылки на элемент списка как на числа [3], мы должны понимать, что на самом деле мы вызываем метод getAt для номеров объектов списка с параметром метода 3, как в numbers.getAt(3) 

**Object get(int index) Возвращает элемент в указанной позиции из списка.**

![](https://lh5.googleusercontent.com/jg1faC_rGZkSCprI13AJBG8HVIW_hJD0_EJon-C-9LzW7CMGmM8VjWn2SOQgOwvWKTItON-kfPhsiLwhra3IuTTg2WUJRJP2p2XdJ5JQ73z6IqVxSxMSAN9lc-y1qj2shRq5ekiK9zDxJbm3y1rrqw)

Кроме того, мы можем индексировать список, используя диапазоны 

Включенный диапазон формы start..end доставляет новый объект List, содержащий ссылки на объекты из исходного списка, начиная с начала позиции индекса и заканчивая концом позиции индекса.

Исключительный диапазон формы start .. < end включает все элементы, кроме последнего конечного элемента. 

**Пример обращения к элементам используя диапазоны [..]**

![](https://lh3.googleusercontent.com/55FROeCmJXXyUjYqD7p_rI-d_Irtt798ziApV0jJsZgn-QTPojS5_8TnuY91z0VjUAEVVcd-1zMmM-4ReAv8o4y0_dAR1RfqGBo8dVZ13oXZz0Tw3IYzULYceLgvzWCYL47935ydSD0JrR5TGmP_MA)

Оператор индексации списка также может использоваться для установки новых значений в список. 

Используемый слева от присваивания, элемент в данной позиции заменяется значением справа от присваивания.

Индекс может быть только одним целочисленным выражением. 

Если значение замены в правой части присвоения само является списком, то оно используется в качестве замены.

![](https://lh4.googleusercontent.com/OzvYJBjLKA74WyZQv33c-YO_ci6QInNn3UmOCD2n5H31Cb_lts2-SG0BAUMe8mXaCB03UjZuCEZ66XLl_iRwR4jCDrBtEh16URAr_PI0pLoO4KZks149OXmSinmAvhvqh5z4gNoHEDutooabrIBlsg)

**Это назначение обеспечивается методом putAt** 

**Новый элемент может быть добавлен в правый конец списка с помощью <<**

**оператор (метод leftShift), как в:**

![](https://lh3.googleusercontent.com/5D1X3zigTSBcoDzPjfTfdZsnNbk0x0Om-8Goq851HNgMEGJYpMZkVdmpZAUnHvs9fuAcnPSriarH8QDI72LGDv15W59EUgX840YfPUpEMqIfcAx6jzd6SKwFYFhr_q8DVhRUcZ6sSOcpJ6Fp8-tTQw)

**Точно так же оператор + (метод плюс) используется для объединения списков:**

![](https://lh5.googleusercontent.com/r_Ett_ccV4kGng0Pl3ZIKydhbEYdoNKL46DFMdke469Z8HZa-ISDX5Caf-L0s54TX28hYWwu3qmA6AJDjZmhJv_-jH3hWPulzKcQOAbpK2l_LPdN-P5bVc1YJy87Xr9EPGIikrQqkACDVDLIKuDsOQ)

**Оператор - (метод минус) используется для удаления элементов из списка:**

![](https://lh6.googleusercontent.com/mAhPLUkAdvNLyBofhFBYhqB3wWoFG8Uxyq0a2jc31DzLjip0eaRAlsdzrpkJc9odfVLjBUJ1g9GA2s0OC1UYrRP5xhnDmMyi5b7n3OVeyf-Euuf0JZ0o8YmTDLMQ-rWuryFjE52HFHhUvYSKhiDLuQ)

## Итерация по списку

  
Перебор элементов списка обычно выполняется с помощью методов each и eachWithIndex, которые выполняют код для каждого элемента списка:

```csharp
[100, 2000, 30000, 400000].each {
    println "Item: $it" // it - неявный параметр, соответствующий текущему элементу
}
```

![](https://ucarecdn.stepik.net/88d34896-4688-4c58-883d-17756f9942d5/)

```kotlin
['Valera', 'Vovan', 'Petro', 'Dmitro'].eachWithIndex { 
    it, i -> println "$i: $it"  // it — текущий элемент,  i — индекс
}
```

![](https://ucarecdn.stepik.net/622db59f-2f65-42a2-8b0b-fc79d97c0559/)

## Методы для списков

Метод `flatten()` используется для выравнивания структуры данных. Он преобразует коллекцию (например, список) в плоскую структуру, объединяя все элементы на одном уровне.

Предположим, у нас есть список списков чисел:

```lua
def numbers = [[1, 2, 3], [4, 5], [6, 7, 8, 9]]
```

Чтобы сгладить этот список с помощью функции `flatten`, мы просто вызываем метод `flatten` для списка:

```java
def flattenedNumbers = numbers.flatten()
```

Теперь переменная `flattenedNumbers` будет содержать все числа из исходного списка в виде единого списка без подсписков:

```csharp
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```lua
def numbers = [[1, 2, 3], [4, 5], [6, 7, 8, 9]]
def flattenedNumbers = numbers.flatten()
println("numbers: " + numbers)
println("flattenedNumbers: " + flattenedNumbers)
```

![](https://ucarecdn.stepik.net/124c332e-dec3-4bf2-80da-edf161ca7182/)

![434](https://ucarecdn.stepik.net/858da998-45ba-4964-be3b-76e46fa1be8d/)

![434](https://ucarecdn.stepik.net/6201f682-f1f9-472d-84e1-c9bdfe2b39d9/)

 **[https://groovy-lang.org/gdk.html](https://groovy-lang.org/gdk.html)**

**![388](https://lh3.googleusercontent.com/qvwrtuYi4wG0sEt7YMvGRdWlsV_4iwxzkZqxyJ_rDY6hF1tpYmSUqz8bCf5aSszsUyxUF0r08OF8hbJrR1O6iMKNBn7qXfauPuKv80FSboqMfFM4OkP1xBsAXUWD9uHskzh5SGe3rhyZDLCDMnOZcQ)**

## Map

Карта (также известная как ассоциативный массив, словарь, таблица и хэш) — это неупорядоченная коллекция ссылок на объекты. Доступ к элементам в коллекции **Map** осуществляется по значению ключа. Ключи, используемые в Map, могут быть любого класса. Когда мы вставляем в коллекцию **Map**, требуются два значения: ключ и значение. Индексация карты с тем же ключом может затем получить это значение. 

В Таблице  показан пример

![](https://ucarecdn.stepik.net/bdde1d1f-3127-4361-a20c-1fc86c3bc75a/)

Литералы карты, содержащие разделенный запятыми список пар ключ:значение, заключенный в квадратные скобки.

![](https://lh4.googleusercontent.com/LAhb0iHXQPkqkGBdqqu6GzlwGk2rJx3w4Z9IF0pNKbe-6cK49K0Og91dDgTptBSsWELaIDIJ8qffOKb-pVI6D0zX7QPhxT0mFNNzty-o978yq0SQNJLo6FK7KJ4oiyDqzFbdmW2U9d4YnFZ_XX_8LA)

Обратите внимание, что если ключ в литерале Map является именем переменной, то он интерпретируется как строковое значение. В примере:

![](https://ucarecdn.stepik.net/2411302c-9d4b-4072-b8c7-a7213e6e748f/)

![](https://lh3.googleusercontent.com/Dab5gB2fTT7IvM1vTQNfPrPxScHyIdq5sFcDW2o-k1xB7GOOhKVGBw16eIglC-QFLLjgYmxLgxG4bKyMRNROHu6cwheK3Z_ajBo4feE0uaUymWrnkEhfwqvAgruAwxII9DaJIPTvBJn1Nq2xrcvtrw)

Попробуйте выполнить пример:

```java
def m = ['first' : 100, 'second' : 500, 'last' : 999]
m.put('age', 33) // добавит ключ : значение
println m.containsKey('age') // вернет true or false в зависимости есть ли ключ
println m.values().asList() // вернет список значений[100, 500, 999, 33]
println m.keySet() // вернет список ключей [first, second, last, age]
println m.size()  // вернет размер карты 4
println m.get('second') // вернет значения ключа second, т.е 500 
```

Обратите внимание, как метод values возвращает коллекцию значений, содержащихся в Map . Часто бывает полезно иметь их в виде списка.

Класс Map поддерживает ряд методов, упрощающих обработку карты.

# Итерация Map

  
Как обычно в пакете разработки Groovy, итерация на картах использует методы each и eachWithIndex. Стоит отметить, что карты, созданные с использованием литеральной нотации карты, упорядочены, то есть если вы повторяете записи карты, гарантируется, что записи будут возвращены в том же порядке, в котором они были добавлены в **MAP**.

```yaml
def map = [ Apple: 42,
            Raspberry: 54,
            Onion: 13,
            Pear: 70 ]

```

```go
map.each { entry -> println "key: $entry.key | value: $entry.value" } // entry - это запись карты
```

![](https://ucarecdn.stepik.net/e86ce541-fd3a-4e5a-a4e9-d25a2550cba9/)

```kotlin
map.eachWithIndex { 
    entry, i -> //  entry - это запись карты, i индекс на карте
    println "$i - Name: $entry.key Price: $entry.value" 
}
```

![](https://ucarecdn.stepik.net/ff820db9-0048-4836-a268-32165c6e591e/)

```java

map.eachWithIndex { key, value, i -> // Ключ, значение и индекс 
    println "$i - Name: $key Price: $value"
}
```

![](https://ucarecdn.stepik.net/df080f17-2ad2-471e-9cb0-5828f33383a1/)

Информацию о методах Map  **[https://groovy-lang.org/gdk.html](https://groovy-lang.org/gdk.html)** 

![](https://lh3.googleusercontent.com/qvwrtuYi4wG0sEt7YMvGRdWlsV_4iwxzkZqxyJ_rDY6hF1tpYmSUqz8bCf5aSszsUyxUF0r08OF8hbJrR1O6iMKNBn7qXfauPuKv80FSboqMfFM4OkP1xBsAXUWD9uHskzh5SGe3rhyZDLCDMnOZcQ)

![](https://ucarecdn.stepik.net/28128a26-d75e-4cc9-a214-34f208ae4a70/)

# Ranges

**Диапазон** — это сокращение для указания последовательности значений.

Диапазон обозначается первым и последним значениями в последовательности, и диапазон может быть включающим или исключающим. 

Включающий диапазон включает все значения от первого до последнего, а исключительный диапазон включает все значения, кроме последнего. 

Вот несколько примеров литералов Range:

- **1..9** – диапазон по возрастанию
- **1 .. <10** – диапазон
- **'a' .. 'h'** – диапазоны также могут состоять из символов
- **9..1** – диапазоны также могут быть в порядке убывания
- **'z’ .. 'a'** – Диапазоны также могут состоять из символов и быть в порядке убывания.

```java
numbers = "0123456789".
println numbers[1..7] // 1234567
println numbers[-1..1] // 987654321
println numbers[1..-1] // 123456789
println numbers[1..<7] // 123456
```

Диапазон может быть обозначен строками или целыми числами. 

Как показано, Range может быть задан как в порядке возрастания, так и в порядке убывания.

Первое и последнее значения для Range также могут быть любыми числовыми целыми выражениями, например:

![](https://ucarecdn.stepik.net/6f015f0f-978d-4639-9fff-9884f09852ec/)

Определен ряд методов для работы с диапазонами.

- **contains()** - Проверяет, содержит ли диапазон определенное значение
- **get()** Возвращает элемент в указанной позиции в этом диапазоне.
- **getFrom()** Получить меньшее значение этого диапазона.
- **getTo()** Получить верхнее значение этого диапазона.
- **isReverse() -**  Это перевернутый диапазон, повторяющийся в обратном направлении? Для лучшего понимания смотри пример ниже:

```go
println((5..1).collect()) // result: [5, 4, 3, 2, 1]
def range = (5..1).reverse()
println(range) // result: [1, 2, 3, 4, 5]
println( (5..1).isReverse() ) // result: true
```

- **size()** Возвращает количество элементов в этом диапазоне.
- **subList()** Возвращает представление части этого диапазона между указанным fromIndex, включительно, и toIndex, исключая

Ниже показаны некоторые примеры этих методов Range и их эффектов: 

**![](https://lh4.googleusercontent.com/tzyFh10qP3HhBQ86JEnKhU2EshftMYf2jKZ-yZZHqe-mFf-m6-g3HE4ISrDnbZWJlkFXPcGR4AiFdXeJ0MZ0Sa183CBx8cfwg4fx4eSuiYWCj5-q-FPZ11BjPWU_CXE2vxbCZDgb0w_XxqxtKYj19Q)**