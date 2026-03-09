## if - else

Условные инструкции называют также командами ветвления , поскольку с их помощью выбирается ветвь кода, подлежащая вы­полнению.

![](https://lh6.googleusercontent.com/iGOz8ZYcXCXtx2lvoN6UFLKVyqZALCbMpS9Hyt9WM0YP8--m4CTyHKOA-OzlbzQAH9LSOgUeNp14u0JM9_zmVOnZNyO_0anEVtIsWvAiABD467Ff54DJaCvs8LSxp25-5Hndw4-A5IIj5hC_G3SU2g)

**Условие** это некоторое условное выражение.

После ключевого слова **if** или **else** стоит одиночная инструкция.

Предложение else неявля­ется обязательным. После ключевых слов **if** и **else** могут также стоять блоки инструкций .

Ниже приведена общая форма условной инструкции if, в которой используются блоки кода.

![](https://lh3.googleusercontent.com/f5lkvL2BU2p4XnyVA1vg4F18oloq48OHl45ssmdHa4nn8rC-C8wNwuxsO46Cn5k7n5CMy1geExyrFTjOMeKgjKGz069gFkWOBCIajo5V_YrJgzXLzofZK7WEH5wUGI8ZAJhBKdgHZ508drECvIk3qA)

Если условное выражение оказывается истинным , то выполняется ветвь **if** .

В противном случае выпол няется ветвь **else** , если таковая существует.

Выпол­нение сразу двух ветвей невозможно.

Условное выражение, управляющее инструкцией if , должно давать результат типа **boolean** 

![](https://lh5.googleusercontent.com/KK3oPsi_e3cfrU7Lturw3RdBH2JtB5ENUed-r_6TGEIWafovbJJQhYOExXRxGXlVjComoU9UZH_GyLhZ7gX-7zrHJxFEDulfebykAzAv5nw_b8lwHqqoQ2sHT9ud9dtQuvjOTgNav6HXdmkT9o7p6w)

![](https://lh6.googleusercontent.com/iGOz8ZYcXCXtx2lvoN6UFLKVyqZALCbMpS9Hyt9WM0YP8--m4CTyHKOA-OzlbzQAH9LSOgUeNp14u0JM9_zmVOnZNyO_0anEVtIsWvAiABD467Ff54DJaCvs8LSxp25-5Hndw4-A5IIj5hC_G3SU2g)

## **Вложенные условные инструкции if** 

Вложенные инструкции if представляют собой условные инструкции , являющиеся телом ветви if или else.

Пользуясь ими , следует помнить, что в Java ветвь **else** всегда связана с ближайшей к ней ветви if, находящейся в том же блоке кода и не связанной с другим предложением **else.**

```java
int x = 15
int y = 30

if(x == 15){
    
    if(y > 10){
        println("y>10")
    } else {
        println("y == 5")
    }
    
} else {
    println("x != 15 ")
}
```

![](https://ucarecdn.stepik.net/16cd6217-e7a9-4557-aa62-08ca1b0cf73a/)

![](https://lh4.googleusercontent.com/6xH4xZU3hUX9qoVtVHTJy4I-1HjqBC0aEBBTb7ICjakYT79hsq6ARiUVuN1jg7o-shVOgNx1tXk04xmTwuc9S4JXVgRV3KGl_xapfd73rMV0AHNuUbKUV2BXH60VvuQoTat7LaTgfMvjVFppQQeVEQ)

##  **If - else if - else**

![](https://lh6.googleusercontent.com/n5xxmPfIrNpervLXB1ajHb1HWm3snqQZAFsxxrtEkc5tv5CHK7eUmu1QzeC2O8_DyWG4VBu2n13_qc1ON1uk0b_dPY89BQWjnTNC_of5FTo1ggMzdyCQI50Po_4B96bf9LJOsrfWMKcfVBjlp6TunA)

![636](https://lh3.googleusercontent.com/orJyb8JWR4MG_xVduNGZt_Wcc3MgwklhYlMLtCui6V64QbBIm5CulKXaaP89fK1-2vKGEeweemkl-4JeDIGgxkwuhjOAju2F8QFbaRhaZQ_OdPYyeTq5oi-I_IAdy5x8ldck-d3Fq25260XXtleB1w)

```go
def i = 17

if (i > 21) {
  println(i + " > 21 ")
} else if (i <= 21 && i >= 11){
  println(i + " диапазон между 11 & 25")
} else{
  println(i + " < 10.")
}
```

 Output:

17 диапазон между 11 & 25


## **switch**

Оператор switch в Groovy обратно совместим с кодом Java; так что вы можете пропустить случаи, когда один и тот же код используется для нескольких совпадений.

Одно отличие состоит в том, что оператор Groovy switch может обрабатывать любые значения переключателя, и могут выполняться различные виды сопоставления.

Switch поддерживает следующие виды сравнений:

- Значения регистра класса совпадают, если значение переключателя является экземпляром класса
- Значения регистра регулярного выражения совпадают, если представление значения переключателя toString () совпадает с регулярным выражением
- Значения вариантов коллекции совпадают, если значение переключателя содержится в коллекции. Это также включает диапазоны (поскольку они являются списками)
- Значения случая закрытия совпадают, если вызов закрытия возвращает результат, который является истинным в соответствии с истиной Groovy.
- Если ничего из вышеперечисленного не используется, то значение case совпадает, если значение case равно значению переключателя.

![](https://lh5.googleusercontent.com/u_urFMbn-AhVqmce7EFeGHAVLhwHrU_bu38f6QoNGHEjuzMY70_YMWQTc3X8TulCLLnFB8K4gxpguNPHOnfI5qGsfKRHE1puNlZ8mZ-d87bTQNjS0YthOg5_evOuFV39b550JC3Ns_1AXZ-hnWkRsg)

![](https://lh3.googleusercontent.com/_1m_4pqIhOz6UszQFLVqT5UpuKzvwuxLLAsiFFm3EJyxs3CyHxnLCh0vbDc6Pp373u2MpxB813heoSghE1fxTIVisIm4r2xrdDTn2Wq4eX6lXLek-H-yRP0G6G7v513fx27ns-LoSWLyNSjX75e4HA)

Оператор `break` в Groovy используется для **прерывания** выполнения ближайшего цикла или оператора выбора (например, `switch-case`). Это означает, что как только оператор `break` выполняется, программа немедленно выходит из текущего цикла или блока `switch`.

В Groovy, как и в других языках программирования, использование оператора `break` в конструкции `switch-case` не является обязательным. Если он отсутствует, выполнение программы будет продолжено со следующего случая (`case`) или блока `default`, если ни один из случаев не подошёл.

  
Взгляните на код примера:

```java
def x = 17
def result = ""

switch ( x ){
    case "bar":
        result += "bar"
    case [4, 5, 17, 'inList']:
        result = "list"
        break
    case 10..20:
        result = "range"
        break
    case Integer:
        result = "integer"
        break
    case Number:
        result = "number"
        break
    default:
        result = "default"
}

println result
```

В данном коде используется конструкция **switch-case**, которая позволяет выполнять различные блоки кода в зависимости от значения переменной `x`.

В начале объявляются две переменные: `x` и `result`. Переменная `x` получает значение 17.

Затем начинается блок `switch`, который проверяет значение переменной `x` и выполняет соответствующий блок кода.

Конструкция `switch (x)` означает, что код внутри блока будет выполняться в зависимости от значения переменной `x`. Далее следуют **блоки case**, которые определяют, какое значение должна иметь переменная x, чтобы выполнялся соответствующий блок кода:

- case "bar": если x равно строке "bar", то к переменной result добавляется строка "bar".
- case [4, 5, 17, 'inList']: если `x` находится в списке **[4, 5, 17, 'inList']**, то переменной `result` присваивается значение _"list"_.
- case 10..20: если x находится между 10 и 20 включительно, то переменной result присваивается значение "range".
- case Integer: если тип переменной x — Integer, то переменной result присваивается значение "integer".
- case Number: если тип переменной x — Number, то переменной result присваивается значение "number".

Если ни один из блоков case не подходит, выполняется блок default, в котором переменной result присваивается значение "default".

После выполнения конструкции switch значение переменной `result` выводится на экран с помощью `println`.

> В языке Groovy тип данных Number является супертипом для всех числовых типов, включая целые и вещественные числа. Integer — это один из подтипов типа Number, который представляет собой 32-битное целое число со знаком.
> 
> Integer используется для представления целых чисел, а Number может представлять как целые, так и дробные числа.
> 
> Чтобы определить тип переменной в Groovy, можно воспользоваться методом `getClass()`. Этот метод возвращает класс объекта, на который ссылается переменная.
> 
> def x = 17 // целое число  
> println(x.getClass()) // class java.lang.Integer  
> myVariable = 17.4 // дробное число  
> println(x.getClass()) // class java.math.BigDecimal  
>  
> 
> Попробуйте изменить в примере значение `x` на 17.4 и выполнится условие `case Number`

![270](https://ucarecdn.stepik.net/b2615b99-787e-4a49-b65b-e535ac5b7c23/)


## **Тернарный оператор**

Тернарный оператор в Groovy — это условный оператор, который возвращает одно из двух значений в зависимости от условия. (_сокращенное выражение, которое эквивалентно ветке **if / else**, присваивающей какое-либо значение переменной)_

Он имеет следующий синтаксис:

```undefined
условие ? значение1 : значение2
```

Проверяется **условие**,  если оно истинно(true),  возвращается - `значение1`, иначе (false) - `значение2`

Это позволяет выполнять простые проверки условий и сразу же присваивать значения переменным или выполнять другие действия.

Вместо:

```java
def string = 'Hello'

if (string != null && string.length() > 0) {
    println('Found')
} else {
    println('Not found')
}
```

можно написать:

```java
def string = 'Hello'
result = ( string != null && string.length() >0 ) ? 'Found' : 'Not found'
print(result)
```

Тернарный оператор также совместим с истиной Groovy , поэтому вы можете сделать его еще проще:

result = string ? 'Found' : 'Not found'

> Здесь проверяет значение переменной **string**. Если переменная имеет значение, отличное от null и пустой строки "", то результат присваивается значение «Found». Иначе — «Not found».

![](https://ucarecdn.stepik.net/a4771be3-aa78-4c84-a5cd-393528ab00b7/)