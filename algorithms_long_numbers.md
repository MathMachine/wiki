## Длинные числа

Во [введении](algorithms_introduction.md) мы ввели абстрактный тип
данных "целое число" и структуру данных "32-битное целое число со знаком"
с множеством представимых объектов $$-2^{31}..2^{31}-1$$.
Аналогично можно определить структуру данных "беззнаковое 32-битное целое
число" с множеством представимых объектов $$0 .. 2^{32}-1$$.
Эти структуры данных соответствуют встроенным типам данных в языках
программирования и реализованы в CPU на аппаратном уровне.

Данный раздел посвящен описанию АТД "целое число в $$m$$-ичной системе счисления"
и структуры данных "длинное число по модулю $$m$$".


### 1. АТД "целое число в $m$-ичной системе счисления"

АТД "целое число в $m$-ичной с.с." эквивалентен АТД "целое число" и
конкретизирует способ представления числа в виде последовательности
цифр (элементов алфавита $0 .. m-1$). Таким образом, АТД "целое число
в $m$-ичной с.с." по способу хранения информации эквивалентен АТД
"последовательность типа $0 .. m-1$", но содержит дополнительные операции:
$+, -, \cdot, /$.


### 2. Представление натурального числа в системе счисления по основанию $m$

Для построения СД "длинное число по модулю $$m$$" нужно определить представление
АТД "целое число в $m$-ичной с.с.", то есть взаимно однозначное соответствие
между числами $$\mathbb N$$ и строками $$A^*$$,
где $$A = 0 .. m-1 \equiv \{0, 1, \dots, m-1\}$$, $$A^*$$ -- множество всех
строк, составленных из символов алфавита $$A$$.

Докажем теорему о существовании и единственности такого представления.

**Теорема.** $$\sqsupset m \in \mathbb N, \; m > 1$$.

$$\forall a \in \mathbb N \, \, \exists ! \; \overline{a} \in A^*, \; A = 0 .. m-1$$,

$$\overline{a} = (a_0, a_1, \dots, a_k)$$:

$$a = a_k m^k + a_{k-1} m^{k-1} + \dots + a_1 m + a_0$$,

$$0 \leq a_i < m, \; a_k \neq 0$$.

Строка $$\overline{a}$$ называется представлением числа $$a$$ в с.с.
по основанию $$m$$.

*Доказательство существования.*

Построим алгоритм:

&nbsp;&nbsp;&nbsp; $$i \leftarrow 0$$<br/>
&nbsp;&nbsp;&nbsp; $${\bf do}$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$a_i \leftarrow a \;{\rm mod}\; m$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$a \leftarrow [a/m]$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$i \leftarrow i + 1$$<br/>
&nbsp;&nbsp;&nbsp; $$\} {\bf while}\; a > 0 \;
$$<br/>
&nbsp;&nbsp;&nbsp; // $$k = i-1$$

Здесь $$a \;{\rm mod}\; m$$ -- остаток от деления $$a$$ на $$m$$,
$$[a/m]$$ -- неполное частное от деления $$a$$ на $$m$$
($$[x]$$ -- целая часть числа $$x$$).

Напомним теорему о делении с остатком.

**Теорема.** [Фаддеев, с. 8]

$$\sqsupset a, b \in \mathbb Z, \; b \neq 0$$.

$$\exists ! \; q, r \in \mathbb Z : a = bq + r, \; 0 \leq r < \vert b \vert$$.

$$q$$ -- неполное частное, $$r$$ -- остаток.
<br/>

Обозначим через $a'$ величину $$a$$ после выполнения одной итерации цикла,
через $$a''$$ -- после двух, $$a'''$$ -- после трех и т.д.,
$$a^{(k)}$$ -- величина $$a$$ после выполнения $$k$$ итераций цикла.

$$a_0 = a\;{\rm mod}\; m, \; a' = [a/m] \; \Rightarrow \; a = a'm + a_0$$,

$$a_1 = a'\;{\rm mod}\; m, \; a'' = [a'/m] \; \Rightarrow \; a' = a''m + a_1$$,

$$a_2 = a''\;{\rm mod}\; m, \; a''' = [a''/m] \; \Rightarrow \; a'' = a'''m + a_2$$,

.$$\dots$$.

$$a_{k-1} = a^{(k-1)} \;{\rm mod}\; m, \; a^{(k)} = [a^{(k-1)}/m] \; \Rightarrow \; a^{(k-1)} = a^{(k)}m + a_{k-1}$$.

Пусть $$k$$ -- наименьший индекс, при котором $$0 < a^{(k-1)} < m$$.
Тогда $$a_k = a^{(k-1)} \;{\rm mod}\; m, \; a^{(k+1)} = [a^{(k)}/m] = 0 \; \Rightarrow \; a^{(k)} = a_k$$.

Заметим, что $$0 < a_k < m, \;\; 0 \leq a_i < m, \; i = 0, \dots, k-1$$.

Вопрос: существует ли такой индекс $$k$$?

Если нет, то $$\exists\, j : a^{(j)} = 0, \; a^{(j-1)} \geq m$$.
Но тогда $$a^{(j)} = [a^{(j-1)}/m] \geq 1$$ -- противоречие.

Вопрос: алгоритм конечен?

$$a > a' > a'' > \dots > a^{(k-1)} > a^{(k)} > a^{(k+1)} = 0$$,
поэтому конечен.

Вопрос: алгоритм находит искомое представление натурального числа в с.с. по
основанию $$m$$?

Имеем

$$a = a'm + a_0$$,

$$a' = a''m + a_1$$,

$$a'' = a'''m + a_2$$,

...

$$a^{(k-1)} = a^{(k)}m + a_{k-1}$$,

$$a^{(k)} = a_k$$.

Отсюда
$$
a = \left( \underbrace{  \left( \underbrace{  \left( \underbrace{ \dots ( \overbrace{ a_k m + a_{k-1} }^{a^{(k-1)}} ) m  \dots  }_{a'''}  \right) m  + a_2 }_{a''}  \right) m + a_1  }_{a'} \right) m + a_0 =
$$

$$
= a_0 + a_1 m + a_2 m^2 + a_3 m^3 + \dots + a_{k-1} m^{k-1} + a_k m^k,
$$
причем $$0 \leq a_i < m, \; a_k \neq 0$$.

Следовательно,
$$\overline{a} = (a_0, a_1, \dots, a_k) \in A^{k+1} \subset A^* $$ --
представление числа $$a$$ в с.с. по основанию $$m$$.
Существование доказано.

*Доказательство единственности.*
На самостоятельный анализ [Андреева, с. 20].


Итак, мы построили взаимно однозначное соответствие между всеми числами
$\mathbb N$ и строками $A^* $, $A = 0 .. m-1$, с ненулевым последним
элементом. Поэтому с числами мы можем работать, как со строками, и со строками,
как с числами.

Алгоритм, приведенный в доказательстве теоремы, позволяет перевести любое число
$a \in \mathbb N$ в $m$-ичную систему счисления при помощи операций
деления нацело и взятия остатка от деления.


### 3. Преобразование АТД "целое число в $p$-ичной с.с." в АТД "целое число в $q$-ичной с.с."

Пусть $a \in \mathbb N$,

$$\widetilde a$$ -- представление числа $a$ в с.с. по основанию $p$,

$$\overline{a}$$ -- представление числа $a$ в с.с. по основанию $q$:

$$\widetilde a = (\widetilde a_0, \widetilde a_1, \dots, \widetilde a_k)$$,

$$\overline a = (\overline a_0, \overline a_1, \dots, \overline a_l)$$.

Дано: $\widetilde a$. Найти: $\overline a$.

По определению:
$$
a = \widetilde a_0 + \widetilde a_1 p + \widetilde a_2 p^2 + \dots + \widetilde a_k p^k.
$$

Тогда если все слагаемые имеют тип "целое число в $q$-ичной с.с.", то по этой
формуле мы найдем объект $a$, который будет иметь такой же тип -- это и будет
представление числа $a$ в $q$-ичной с.с.

Предположим, что в АТД "целое число в $m$-ичной с.с." реализованы следующие
операции:

- преобразование числа из АТД "32-битное целое число" в АТД "целое число в
$m$-ичной с.с." (инициализация длинного числа);

- сложение чисел АТД "целое число в $m$-ичной с.с." (сложение длинных чисел);

- умножение числа АТД "целое число в $m$-ичной с.с. на число АТД
"32-битное целое число" (умножение длинного числа на короткое).

Тогда алгоритм перевода можно записать так:

&nbsp;&nbsp;&nbsp; $${\tt alg}(p, q : {\tt Int};\; a : {\tt LongInt}\langle p \rangle) \to
x : {\tt LongInt}\langle q \rangle = \{$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$k = {\tt length}(a)$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $${\tt LongInt}\langle q \rangle : x
\leftarrow {\tt init}\langle q \rangle(a[0])$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $${\tt LongInt}\langle q \rangle : y \leftarrow 1$$<br/>
<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $${\bf for}\; i \leftarrow 1 .. k \; \{$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // $$y = p^{i-1}, \; x = \widetilde a_0 + \widetilde a_1 p + \dots + \widetilde a_{i-1} p^{i-1}$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$y \leftarrow y \cdot p$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$x \leftarrow x + a[i] \cdot y$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // $$y = p^i, \; x = \widetilde a_0 + \widetilde a_1 p + \dots + \widetilde a_i p^i$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$\}$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // $$y = p^k, \; x = \widetilde a_0 + \widetilde a_1 p + \dots + \widetilde a_k p^k$$<br/>
&nbsp;&nbsp;&nbsp; $$\}$$


### 4. Структура данных "длинное число по модулю $m$"

Абстрактное *длинное число по модулю $m$* -- это представление числа $a \in \mathbb N$ в системе счисления по основанию $m$:
$\overline{a} = (a_0, a_1, a_2, \dots, a_k)$, где
$$
a = a_0 + a_1 m + a_2 m^2 + a_3 m^3 + \dots + a_k m^k,
$$
где $0 \leq a_i < m$, при этом $a_k > 0$.
Для числа $a = 0$ делаем исключение: оно представляется в виде $\overline{a} = (a_0)$, где $a_0 = 0$, $k = 0$.

Для построения структуры данных "длинное число по модулю $m$" нам нужно определить, как последовательность цифр $a_0, a_1, \dots, a_k$ будет храниться в памяти и как будут производиться операции над этими данными.

В качестве реализации АТД "целое число в $m$-ичной системе счисления" используем
массив целых чисел от 0 до $m-1$, содержащий представление хранимого длинного числа
в системе счисления по основанию $m$. Цифры расположены от младших разрядов к старшим:
в 0-м элементе массива содержится последняя цифра числа, в последнем элементе первая.

В силу того, что существует взаимно однозначное
соответствие между такими последовательностями цифр и натуральными числами,
над длинными числами можно выполнять арифметические операции, которые в результате
дают представления суммы, разности, произведения и частного в $m$-ичной системе счисления. Ниже мы разберем алгоритмы получения этих представлений.

Описание структуры данных на ЯП C++:

```cpp
class LongInt {
  const int radix_default = 10000;
  int radix;  // основание системы счисления
public:
  int num_digits;  // количество цифр в длинном числе
  vector<int> digits;

  // инвариант:
  //   num_digits > 0,  digits.size() == num_digits,
  //   digits[num_digits - 1] > 0

  // конструктор: инициализация длинного числа значением value
  LongInt (int value = 0, int radix = radix_default);

  // арифметические операции
  LongInt operator+ (const LongInt& b);  // длинное сложение
  LongInt operator- (const LongInt& b);  // длинное вычитание
  LongInt operator* (int b);  // умножение длинного числа на короткое
  LongInt operator* (const LongInt& b);  // умножение длинного на длинное

  // сравнение длинных чисел
  bool operator== (const LongInt& b);
  bool operator!= (const LongInt& b);
  bool operator< (const LongInt& b);
  bool operator<= (const LongInt& b);
  bool operator> (const LongInt& b);
  bool operator>= (const LongInt& b);

  int get_radix (); // основание системы счисления
};

// длинное деление и взятие остатка от деления
LongInt div_mod (const LongInt& a, const LongInt& b, LongInt& a_mod_b);
```

Для корректного представления чисел в СД "длинное число по модулю $m$" требуется, чтобы операции модификации СД сохраняли инвариант: количество цифр должно быть положительным, и старшая цифра должна быть отлична от 0.


### 5. Алгоритмы операций над длинными числами

Предположим, что нам задано два представления целых неотрицательных чисел $a, b$ в системе счисления по основанию $m$:
$\overline{a} = (a_0, a_1, a_2, \dots, a_k)$, где
$$
a = a_0 + a_1 m + a_2 m^2 + a_3 m^3 + \dots + a_k m^k,
$$
где $0 \leq a_i < m$, при этом $a_k > 0$, за исключением случая $a = 0$, и аналогично
$\overline{b} = (b_0, b_1, b_2, \dots, b_l)$, где
$$
b = b_0 + b_1 m + b_2 m^2 + b_3 m^3 + \dots + b_l m^l,
$$

где $0 \leq b_i < m$, при этом $b_l > 0$, за исключением случая $b = 0$.

Требуется вычислить представление числа $c = f(a, b)$ в той же системе счисления.
Отметим, что в силу единственности такого представления, если мы найдем
последовательность цифр $(c_0, c_1, c_2, \dots, c_s)$, для которой $0 \leq c_i < m$, такую, что
$c = \displaystyle\sum_{i=0}^s c_i m^i$, то это и будет искомое представление числа $c$
в $m$-ичной системе счисления.

#### Длинное сложение

Сложим два представления $a = \displaystyle\sum_{i=0}^k a_i m^i$ и
$b = \displaystyle\sum_{i=0}^l b_i m^i$ и преобразуем сумму
$c = a + b = \displaystyle\sum_{i=0}^p (a_i + b_i) m^i$, где $p = \max\{k, l\}$, к виду
$c = \displaystyle\sum_{i=0}^s c_i m^i$, где $0 \leq c_i < m$.

По теореме о делении с остатком $a_0 + b_0 = qm + r$, где $q$ -- неполное частное, $r$ -- остаток, $q, r \in \mathbb Z$, $0 \leq r < m$.
Обозначим $d_1 := q$, $c_0 := r$. Другое обозначение:
$d_1 = [(a_0 + b_0)/m]$, $c_0 = (a_0 + b_0) \bmod m$.

Таким образом,
$$
c = c_0 + (a_1 + b_1 + d_1)m + \sum_{i=2}^p (a_i + b_i)m^i =.
$$

$$
= c_0 + m\left[ (a_1 + b_1 + d_1) + \sum_{i=1}^p (a_{i+1} + b_{i+1})m^i \right],
$$
и задача свелась к нахождению цифр числа $(a_1 + b_1 + d_1) + \displaystyle\sum_{i=1}^p (a_{i+1} + b_{i+1})m^i$.

Теперь у нас вырисовывается математическая индукция, которая в программе может
быть реализована рекурсивно либо итерационно. Такие конструкции часто встречаются
при алгоритмизации.

Разделив $(a_1 + b_1 + d_1)$ на $m$, получим
$$
c = c_0 + c_1m + (a_2 + b_2 + d_2)m^2 + \sum_{i=3}^p (a_i + b_i)m^i,
$$
где $a_1 + b_1 + d_1 = c_1 + d_2m$, то есть $c_1 = (a_1 + b_1 + d_1) \bmod m$, $d_2 = [(a_1 + b_1 + d_1)/m]$.
Далее, аналогично,
$$
c = c_0 + c_1m + c_2m^2 + (a_3 + b_3 + d_3)m^3 + \sum_{i=4}^p (a_i + b_i)m^i,
$$
где $a_2 + b_2 + d_2 = c_2 + d_3m$,
и вообще
$$
c = \sum_{i=0}^j c_im^i + (a_{j+1} + b_{j+1} + d_{j+1})m^{j+1} + \sum_{i=j+2}^p (a_i + b_i)m^i, \quad j = 0..p-2,
$$
где $a_j + b_j + d_j = c_j + d_{j+1}m$, то есть $c_j = (a_j + b_j + d_j) \bmod m$, $d_{j+1} = [(a_j + b_j + d_j)/m]$.

Здесь мы считаем
$$
a_i = 0 \text{ при } i > k,\quad b_i = 0 \text{ при } i > l.
$$

Итак, резюмируя всё вышесказанное,
$$
c = a + b = \sum_{i=0}^p (a_i + b_i) m^i =
$$
$$
= c_0 + (a_1 + b_1 + d_1)m + \sum_{i=2}^p (a_i + b_i) m^i =
$$
$$
= c_0 + c_1m + (a_2 + b_2 + d_2)m^2 + \sum_{i=3}^p (a_i + b_i) m^i =
$$
$$
= c_0 + c_1m + c_2m^2 + (a_3 + b_3 + d_3)m^3 + \sum_{i=3}^p (a_i + b_i) m^i = \ldots =
$$
$$
= \sum_{i=0}^{p-1} c_im^i + (a_p + b_p + d_p)m^p = \sum_{i=0}^{p} c_im^i + d_{p+1}m^{p+1}.
$$

Поскольку $a < m^{p+1}$ и $b < m^{p+1}$, то $a + b < 2m^{p+1}$, поэтому $d_{p+1} < 2$.
Этим объясняется то, что старшая цифра суммы в случае возникновения переноса в $(p+1)$-й разряд
не превосходит 1.

Переобозначим $c_{p+1} = d_{p+1}$ и $s = p+1$ в случае $d_{p+1} > 0$, иначе $s = p$.
Итак, мы вывели представление суммы $c = a+b = \displaystyle\sum_{i=0}^s c_im^i$
в системе счисления по основанию $m$, поскольку $0 \leq c_i < m$.

Алгоритм длинного сложения:

&nbsp;&nbsp;&nbsp; $${\tt sum}(a, b : {\tt LongInt\langle m \rangle}) \to
c : {\tt LongInt}\langle m \rangle = \{$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$k = {\tt length}(a);\; l = {\tt length}(b)$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$d \leftarrow 0;\; i \leftarrow 0$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $${\bf while}\;\; i \leq k\; \vee\; i \leq l\; \vee\; d > 0\;\{$$ <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // $$d = d_i$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$c_i \leftarrow (a_i + b_i + d) \bmod m$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$d \leftarrow [(a_i + b_i + d) / m]$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // $$d = d_{i+1}$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$i \leftarrow i + 1$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$\}$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$$s \leftarrow i - 1$$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// $$c = c_0 + c_1 m + c_2 m^2 + \ldots + c_s m^s$$<br/>
&nbsp;&nbsp;&nbsp; $$\}$$

#### Длинное вычитание

Допустим, что $a \geq b$, то есть $k \geq l$ и $a_k \geq b_k$.

Вычтем из представления $a = \displaystyle\sum_{i=0}^k a_i m^i$ представление
$b = \displaystyle\sum_{i=0}^l b_i m^i$:

$$
a - b = \sum_{i=0}^k (a_i - b_i)m^i,
$$
и если $a_i < b_i$, заменим соответствующее слагаемое на $(m + a_i - b_i) - m$.

Обозначим $d_0 = 0$, 

$c_i = a_i - b_i - d_i$, $d_{i+1} = 0$, если $a_i - b_i - d_i \geq 0$

и $c_i = m - (a_i - b_i - d_i)$, $d_{i+1} = 1$, если $a_i - b_i - d_i < 0$.

$$
a - b = a_0 - b_0 + \sum_{i=1}^k (a_i - b_i)m^i =
  c_0 + (a_1 - b_1 - d_1)m + \sum_{i=2}^k (a_i - b_i)m^i =
$$
$$
= c_0 + c_1m + (a_2 - b_2 - d_2)m^2 + \sum_{i=3}^k (a_i - b_i)m^i = \ldots =
$$
$$
= \sum_{i=0}^{k-1} c_im^i + (a_k - b_k - d_k)m^k = \sum_{i=0}^k c_im^i.
$$

Алгоритм длинного вычитания:

&nbsp;&nbsp;&nbsp; ${\tt sub}(a, b : {\tt LongInt\langle m \rangle}) \to c : {\tt LongInt}\langle m \rangle = \{$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $k = {\tt length}(a);\; l = {\tt length}(b)$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$d \leftarrow 0;\; i \leftarrow 0$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;${\bf for}\;\; i \leftarrow 0\, .\,. \,k \;\; \{$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// $d = d_i$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;${\bf if}\;\; a[i] - b[i] - d \geq 0 \;\;\{$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$c[i] \leftarrow a[i] - b[i] - d$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$d \leftarrow 0$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$\}$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;${\bf else}\;\; \{$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$c[i] \leftarrow m + (a[i] - b[i] - d)$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$d \leftarrow 1$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$\}$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// $d = d_{i+1}$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$\}$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// $c = c[0] + c[1] m + c[2] m^2 + \ldots + c[k] m^k$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$s \leftarrow k$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;${\bf while}\;\; s > 0 \; \& \; c[s] = 0 \;\;\{$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\qquad $s \leftarrow s - 1$<br/>
&nbsp;&nbsp;&nbsp;$\}$<br/>

Цикл while удаляет нули в старших разрядах найденного числа.

При реализации нужно не забыть, что в элементах массива ${\tt b[i]}$ при ${\tt i > l}$ могут быть произвольные числа. (При записи алгоритма мы считали, что $b_i = 0$ при $i > l$.)

#### Умножение длинных чисел

Пусть $\overline a = (a_0, a_1, \ldots, a_k)$, 
$\overline b = (b_0, b_1, \ldots, b_l)$ -- представления целых неотрицательных чисел $a$ и $b$ в системе счисления по основанию $m$.
Предположим, что $k \geq l$. Требуется найти представление числа $c = ab$ в той же системе счисления.

По определению,
$$
b = b_0 + b_1 m + b_2 m^2 + \dots + b_l m^l.
$$

Тогда
$$
c = ab = ab_0 + ab_1 m + ab_2 m^2 + \dots + ab_l m^l.
$$

Предположим, что для СД "длинное число по модулю $m$" определены операции:

* $c = {\rm add}(a,b)$ -- сложение длинных чисел $a,b$
* $c = {\rm mult\_short}(a,b)$ -- умножение длинного числа $a$ на короткое число $b$
* $c = {\rm mult\_power}(a,j)$ -- умножение длинного числа $a$ на $m^j$ (сдвиг массива цифр)

Алгоритм:

&nbsp;&nbsp;&nbsp;${\rm mult}(a,b) \rightarrow c = \{$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$c \leftarrow 0$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;${\bf for}\;\; i \leftarrow 0\, .\,. \,l \;\; \{$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // $c = ab_0 + ab_1m + \dots + ab_{i-1}m^{i-1}$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$x \leftarrow {\rm mult\_short}(a, b[i])$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// $x = ab_i$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$x \leftarrow {\rm mult\_power}(x, i)$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// $x = ab_im^i$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$c \leftarrow {\rm add}(c, x)$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// $c = ab_0 + ab_1m + \dots + ab_{i-1}m^{i-1} + ab_{i}m^{i}$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$\}$<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// $c = ab_0 + ab_1m + \dots + ab_{l}m^{l} = ab$<br/>
&nbsp;&nbsp;&nbsp;$\}$<br/>

На выполнение алгоритма будет затрачено $O(kl)$ времени.


### Литература

[Андреева] [Андреева, Босова, Фалина -- Математические основы информатики (2005)](https://yadi.sk/i/R89HOZ6aXeAIMQ)

[Кнут2] [Кнут -- Искусство программирования. Т. 2. Получисленные алгоритмы](https://yadi.sk/d/Jz2Fn_XXNLMbPQ) -- С. 294-303

[Романовский] [Романовский -- Дискретный анализ (2008)](https://yadi.sk/d/b6TTmh4UhffYHQ) -- С. 115-116

[Левитин] [Левитин -- Алгоритмы: введение в разработку и анализ (2006)](https://yadi.sk/i/1IkcA145-decvg) -- С. 189-192

[Фаддеев] [Фаддеев -- Лекции по алгебре (2007)](https://yadi.sk/i/KNQK1G-RqgFEDA)

[Курбатова] [Курбатова, Филиппов -- Курс лекций по алгебре (2015)](https://yadi.sk/i/SoU9B34AfqIR6g)
