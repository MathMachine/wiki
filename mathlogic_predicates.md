## Логика предикатов

Логика предикатов за счет введения дополнительных составляющих записываемых формул позволяет
конкретизировать формализацию
предложений естественного языка, выделив внутреннюю структуру утверждений. Язык логики предикатов также называют
языком первого порядка, в языке первого порядка кванторы относятся к объектам, в отличие от логики второго порядка,
в которой под знаком квантора могут стоять другие функции.

Предикат выделяет определенное отношение между объектами, например, "верно, что число простое", "два умножить на три равно шесть",
"одно число меньше второго". Таким образом, то, что в логике высказываний записывается одной пропозициональной переменной,
может быть выражено на языке 1 порядка в виде предиката, зависящего от нескольких термов, тем самым на языке 1 порядка
можно выразить больше информации об интересующих объектах.

Термом в логике предикатов называют комбинацию функций, переменных и констант. Здесь переменные уже не пропозициональные,
а индивидные, то есть принимают значения из некоторого универсума. Формула в логике предикатов составляется из атомарных формул,
логических операций и кванторов. Терм имеет определенное значение, его можно вычислить, а формула имеет логическое значение,
"да" или "нет". Если на место пропозициональных переменных в формуле логики высказываний подставить предикаты, зависящие от термов,
то получим логическое выражение, истинность которого определяется зависимостью истинности формулы от переменных и значениями термов.


### Понятия сигнатуры, алгебраической системы, подсистемы, порожденной множеством

*Алгебраическая система* -- это непустое множество (носитель) вместе с заданными на нем
константами, предикатами и функциями. 
*Сигнатура* -- это набор символов, обозначающих константы, предикаты и функции на заданном множестве.
Таким образом, алгебраическая система -- это множество, заданное вместе с сигнатурой, проинтерпретированной конкретными объектами.

Пусть имеем алгебраическую систему $\mathcal M$ с множеством $M$ и сигнатурой $\sigma$, и пусть $A \subset M$.
Скажем, что $A$ -- замкнутое множество алгебраической системы $\mathcal M$, если:

- все константы сигнатуры принадлежат $A$;

- для всех функций сигнатуры, если значения переменных принадлежат $A$, то значения функций также принадлежат $A$.

Для замкнутого множества $A$ можно определить подсистему $\mathcal N = \langle A, \sigma \rangle$: все символы на множестве $A$
надо интерпретировать так же, как они интерпретировались в системе $\mathcal M$.

Алгебраическая система, включающая сигнатуру, представляет собой интерпретацию заданного набора символов
операций над объектами. С примерами алгебраических систем можно ознакомиться [здесь](https://youtu.be/7EvuCyW0i3g).
Поскольку сигнатура -- это просто набор символов, то одна и та же сигнатура может соответствовать разным
по смыслу алгебраическим системам.

### Понятия терма данной сигнатуры, значение терма на кортеже в алгебраической системе

Терм -- это алгебраическое или арифметическое выражение, у него есть какое-то значение, его можно вычислить.
Дадим индуктивное определение *терма*:

* если $x$ -- индивидная переменная, то $x$ -- терм;

* если $c$ -- константный символ, то $c$ -- терм;

* если $t_1, \dots, t_k$ -- термы, $f$ -- функциональный символ арности $k$, то $f(t_1, \dots, t_k)$ -- терм.

Значение терма при значениях переменных $x_1 = a_1, x_2 = a_2, \dots, x_k = a_k$ определяется по индукции:

* если терм -- это переменная, то значение терма берется из кортежа значений переменных $(a_1,\dots,a_k)$;

* если терм -- функциональный символ от набора термов, то берутся значения этих термов, и значение терма
есть значение соответствующей данному символу функции от этих значений.


### Теорема о подсистеме, порожденной множеством

*Теорема.* Если $\mathcal M = \langle M, \sigma \rangle$ -- алгебраическая система, $A \subset M$, $A \neq \varnothing$,
то существует единственная подсистема $\mathcal M(A) = \langle M(A), \sigma \rangle$ алгебраической системы $\mathcal M$
такая, что $A \subset M(A)$ и $\mathcal M(A) \subset \mathcal N$ для любой подсистемы $\mathcal N = \langle A, \sigma \rangle$
алгебраической системы $\mathcal M$, для которой $A \subset M$.

*Доказательство.* В качестве $M(A)$ рассмотрим пересечение носителей всех подсистем, содержащих $A$.


### Формулы ЛП

*Атомарной формулой* называют комбинацию предикатного символа и термов, от которых он зависит:
если $t_1, \dots, t_k$ -- термы, $P$ -- предикатный символ, то $P(t_1, \dots, t_k)$ -- атомарная формула.

*Формулой ЛП* называют комбинацию атомарных формул, логических операций и кванторов:

1) атомарная формула сигнатуры $\sigma$ есть формула сигнатуры $\sigma$;

2) если $\varphi$, $\psi$ -- формулы сигнатуры $\sigma$, то $\neg\varphi$, $(\varphi\,\&\, \psi)$,
$(\varphi\vee \psi)$, $\varphi \to \psi$, $\forall x\,\varphi$, $\exists x \, \varphi$ -- формулы сигнатуры $\sigma$;

3) других формул нет.


### Истинность формул ЛП в алгебраической системе

Всякая формула ЛП определяет некоторый предикат (возможно, нуль-местный, то есть высказывание).
Истинность этого высказывания с учетом логических операций определяется, как и раньше, дополнительно учитывается
семантика кванторов. Заметим, что все предикаты можно отнести к одному из трех типов:

1) тождественно истинные: предикат истинен при любых наборах аргументов;

2) тождественно ложные: предикат ложен вне зависимости от значений аргументов;

3) выполнимые: предикат истинен хотя бы при одном наборе аргументов.

По определению, квантор общности $\forall x\, P(x)$ принимает истинное значение только в том случае,
когда предикат $P(x)$ тождественно истинен, а квантор существования $\exists x\,P(x)$ ложен только в том
случае, когда предикат $P(x)$ тождественно ложен.


### Эквивалентные формулы ЛП

Две формулы ЛП сигнатуры $\sigma$ называются *эквивалентными*, если вторая формула является логическим
следствием первой (истинна при любых значениях переменных, при которых первая формула истинна)
и также первая формула является логическим следствием второй. Здесь подразумевается, что это верно
для любой алгебраической системы данной сигнатуры.

Рассмотрим несколько таких эквивалентностей.
Первым типом эквивалентности служит тавтология логики высказываний: при подстановке на место
одинаковых пропозиональных переменных одинаковых атомарных формул получаются эквивалентные
формулы ЛП.

Следующие эквивалентности получаются при перестановке кванторов:

$\forall x \forall y\, \varphi \equiv \forall y \forall x \, \varphi$

$\exists x \exists y \,\varphi \equiv \exists y \, \exists x \, \varphi$.

Заметим, что разноименные кванторы можно менять местами только в одном порядке:

$\exists x \forall y \,\varphi \to \forall y \exists x \, \varphi$.

Аналог закона де Моргана:

$\neg\exists x \,\varphi \equiv \forall x \,\neg \varphi$
(отрицание существования -- это всеобщность отрицания)

$\neg \forall x \,\varphi \equiv \exists x\, \neg\varphi$
(отрицание всеобщности -- это существование отрицания).

Отметим, что квантор общности можно понимать как бесконечную конъюнкцию,
а квантор существования -- как бесконечную дизъюнкцию.
В следующих эквивалентностях меняется порядок конечной и бесконечной конъюнкции и дизъюнкции:

$\forall x \, (\varphi \,\&\,\psi) \equiv \forall x\,\varphi \,\&\, \forall x \,\varphi$

$\exists x (\varphi \vee \psi) \equiv \exists x\,\varphi \vee \exists x \, \psi)$

Если смешивать конъюнкцию и дизъюнкцию, то логическое следствие будет только в одну сторону:

$\exists x \, (\varphi \,\&\,\psi) \to \exists x\,\varphi \,\&\, \exists x\,\psi$,

$\forall x\,\varphi \vee \forall x\,\psi \to \forall x \, (\varphi \vee \psi)$.

Следующая эквивалентность относится к импликации:

$\exists x\,(\varphi \to \psi) \equiv (\forall x\,\varphi \to \exists x\,\psi)$.

Эту эквивалентность можно проинтерпретировать так: в баре хотя бы один посетитель закусывает ($\psi)$, когда пьет ($\varphi$).
Тогда если все пьют, то он закусывает. И обратно: если все пьют, то импликация слева опять выполняется для этого $x$, потому что
$\psi(x) = 1$.

И наконец, логические следствия, которые верны только в одну сторону:

$(\exists x\,\varphi \to \forall x \,\psi) \to \forall x\,(\varphi \to \psi)$,

$\forall x\,(\varphi\to\psi) \to (\forall x\,\varphi \to \forall x \, \psi)$,

$\forall x \,(\varphi \to \psi) \to (\exists x \,\varphi \to \exists x \, \psi)$.

Важно отметить, что если переменная $x$ не является параметром формулы $\psi$, то следующая эквивалентность
верна в обе стороны:

$\exists x\,(\varphi \,\&\,\psi) \equiv \exists x\,\varphi\,\&\,\psi$.


### ПНФ для формул ЛП

Формула приведена к *предваренной нормальной форме*, если выполняются следующие условия:

1) все кванторы вынесены в начало формулы;

2) в формуле присутствуют только основные логические операции;

3) отрицание относится только к предикатам.

**Теорема.** Для любой формулы логики предикатов существует эквивалентная ей формула в ПНФ.


### Литература

Григорьев, Степанкина -- Системы искусственного интеллекта (1998)

Лавров -- Математическая логика (2006)

Дехтярь, Дудаков, Карлов -- Лекции по дискретной математике (2021)

Степанова, Плешкова, Гусев -- Математическая логика и теория алгоритмов (2010)

Игошин -- Математическая логика (2016)

Пруцков, Волкова -- Математическая логика и теория алгоритмов (2018)

[Курс лекций МФТИ по математической логике и теории алгоритмов](https://mipt.ru/online/diskretnaya-matematika/matematicheskaya-logika-i-teoriya-algoritmov.php), [[текст](http://ru.discrete-mathematics.org/fall2017/1/logic_pmi/lecture-9-first-order.pdf)]