## Лабораторные работы

*1*. Вычисление и минимизация логических формул.

Построить таблицу истинности логической формулы.
Написать программу, которая для заданного логического выражения найдет СДНФ.
По желанию: минимизировать ее методом Квайна или методом неопределенных коэффициентов.

Дополнительно: найти многочлен Жегалкина для заданной булевой функции.

[Заготовка](https://disk.yandex.ru/d/840XHFZ5LWs4qQ)

1*. Нахождение отрицания логической формулы.

Применить однопроходный алгоритм, который заменяет каждую операцию конъюнкции и дизъюнкции на двойственную
и навешивает/убирает отрицание у переменных, см. раздел "Задачи".

1**. Нахождение СКНФ с помощью взятия отрицания СДНФ.

Используя программу построения СДНФ и программу нахождения отрицания выражения, найдите СКНФ заданного выражения.
Для этого найдите СДНФ отрицания заданного выражения и затем найдите ее отрицание.
Чтобы найти отрицание СДНФ, вы можете вызвать функцию преобразования строки с СДНФ в дерево выражения.
     
*2*. Вывод логических формул.

На вход программе подается логическая формула. Построить вывод этой формулы из аксиом (если она общезначима).

См. обзор: [[Игошин](https://znanium.com/read?id=243891), параграф 13].

Дополнительно: построить логический вывод формул, содержащих предикаты и кванторы.

Чтобы написать программу, которая автоматически решает примеры из задачника на исчисление высказываний,
можно применить следующий алгоритм.

- Чтобы получить отрицание, надо добавить к посылкам выражение без отрицания и получить противоречие.

- Чтобы получить конъюнкцию, надо вывести оба множителя.

- Чтобы получить дизъюнкцию, надо добавить к посылкам отрицание одного слагаемого и попытаться вывести
другое слагаемое.

- Чтобы получить импликацию, надо добавить левую часть к посылкам и попытаться вывести заключение.

- Также важно применить следующие индуктивные процедуры к множеству гипотез и выведенных формул:

  * modus ponens: если среди гипотез есть $A \to B$ и $A$, добавляем $B$;

  * modus tollens: если среди гипотез есть $A \to B$ и $\neg B$, добавляем $\neg A$;

  * сокращение слагаемого: если есть $\neg A$ и $A \vee B$ или $B \vee A$, добавляем $B$;

  * разделение конъюнкции;

  * введение дизъюнкции.

[Заготовка](https://disk.yandex.ru/d/0Ey8eiTqGg3BDw)

*3*. Разбор словесных выражений с предикатами.

Преобразовать словесные высказывания из [логического теста 1](http://p98414p4.beget.tech/test) к виду выражения исчисления высказываний
или исчисления предикатов (в случае наличия в формуле кванторов).

Дополнительно: для логической формулы и множества формул определить, какие формулы из множества следуют из первой формулы.

*4*. Машина Тьюринга.

Дан [эмулятор машины Тьюринга](https://github.com/saisubham/turing-machine-simulator).
Реализовать программу для машины Тьюринга, вычисляющую заданную функцию.

*5*. Логический анализ компьютерных программ.

Применить аппарат математической логики для умеренно доказательных вычислений.
Попрактиковаться в точном указании спецификаций функций, комментировании инвариантов циклов и прочих
логических условий, освоить исчисление Хоара для логического обоснования правильности программы.
Источник: Шень -- Программирование: теоремы и задачи.

*6*. Разработать программу, которая будет делать логические выводы на основе заданных ограничений.
Предметная область -- расписание в университете. Дана БД, содержащая следующие таблицы:
План (id, Группа, Предмет, Тип, Частота), Предметы, Группы, Типы занятий, Частоты занятий.
Построить таблицу Расписание (День недели, Номер пары, Пара (из плана)) на основе логических
ограничений, которые тоже вводятся в БД или интерфейс программы. Если ответов возможно несколько или даже много,
то разбить все возможные расписания на группы и попытаться как-то их упорядочить, чтобы можно было на основе вывода программы
получить представление обо всём этом множестве и выбрать из него оптимальный, исходя из введенных или не введенных
критериев пользователя.

[Заготовка](https://disk.yandex.ru/d/66wbNm5AuuvXPA)

*7*. Решить вычислительную задачу высокой сложности, применив программирование с соглашениями.
Сперва "спроектировать" свой алгоритм: 1) разбить задачу на подзадачи, 2) записать соглашение для каждой подзадачи,
3) записать проект решения каждой подзадачи в отдельности, перечислив в комментариях последовательность логических
условий, которые будут выполняться в этом месте программы, а затем реализовать соответствующие операторы,
приводящие к истинности этих условий.

*8*. (дополнительно) Разработать программу, которая будет анализировать предметную область и выводить логические выводы,
на основании которых утверждается такой ответ. Например, БД содержит общие правила (знания) о грибах,
и задана информация о грибе, который был обнаружен. Программа может задавать уточняющие вопросы, требуется сделать
выводы, какой это гриб, по его признакам, и вывести ответ вместе с цепочкой логических выводов.

*9*. (дополнительно) Процесс приготовления пищи как аналог вычислительного процесса. Определить типы данных, которые
будут хранить информацию о состоянии отдельных частей кухонных принадлежностей (сковорода = ..., кастрюля = ...,
миска = ..., плита = ..., духовка = ..., микроволновка = ...,
разделочная доска = ..., продукты = ...). Смоделировать вычислительный процесс с обязательным
указанием логических комментариев, характеризующих состояние кухни на каждом промежуточном этапе.
Для ввода данных в программу можно ограничиться самим объектно-ориентированным языком, то есть обойтись без
специального интерфейса пользователя.

*10*. Разработать программу "Импликация", которая будет выявлять закономерности в данных количественной
и категориальной природы. Например, программа может установить по большой выборке данных, что справедлива
импликация $P(x) \to Q(x)$, где $P(x)$, $Q(x)$ -- введенные пользователем предикаты, определенные на 
данных $x = (x_1, \dots, x_n)$. Либо более слабое условие $P(x) \,\&\, Q(x) \to R(x)$ или $P(x) \to Q(x)\vee R(x)$,
либо более сильное условие $P(x) \vee Q(x) \to R(x)$, $P(x) \to Q(x) \,\&\, R(x)$.
Для обратной импликации $Q(x)\to P(x)$ тоже посчитать, в каком числе случаев (в %) она выполняется.
Программа может сама конструировать логические формулы по заданному шаблону и проверять справедливость этого
логического условия для всего массива данных.