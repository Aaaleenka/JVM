
## Описание каждой строки с точки зрения происходящего в JVM

При запуске программы сначала происходит подгрузка классов посредством **ClassLoader**: подгружаются
- System classes(String, Object, Integer, System)
- JvmComprehension

Далее происходит Связавыние Linking, а именно:

- Verify проверка валидности и синтаксической консистентности
- Prepare подготовка примитивов в статических классах (в примере не проверяется)
- Resolve разрешение символьных ссылок (в примере пропускаеися). 

**И наши классы попадют в Metaspace**

- На пункте 1 Cоздается новый фрейм в Stack Memory, туда записывается примитив int i = 1.
- На пункте 2 в Heap создается создается новый объект класса Object, который записывается в кучу Heap, а ссылка o - в Stack Memory.
- На пункте 3 аналогично второму пункту
- На пукнте 4 происходит создание фрейма в Stack Memory для функции printAll и далее начинается его заполнение.
- На пункте 5 аналогично пункту 2 и 3
- На пункте 6 создается новый фрейм в SM под вызов println и передаются значения + будет добавлен новый фрейм toString для объекта o
- На пункте 7 в Stack формируется фрейм println, в котором создается ссылка на объект String, значение которого "finished". Сам же объект типа String со значением создается для хранения в хипе.

### Наглядная картинка ###

<picture>
 <source media="(prefers-color-scheme: dark)" srcset="https://github.com/Aaaleenka/JVM/blob/master/example.png">
 <source media="(prefers-color-scheme: light)" srcset="https://github.com/Aaaleenka/JVM/blob/master/example.png">
 <img alt="YOUR-ALT-TEXT" src="https://github.com/Aaaleenka/JVM/blob/master/example.png">
</picture>

Сборщик мусора, наверное, может удалять переменную i в выполненном коде, т.к. на нее никто не ссылается. 
