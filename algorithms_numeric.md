## Целочисленные алгоритмы

*Наибольшим общим делителем* целых чисел $a$ и $b$ (хотя бы одно из которых не равно 0) называется наибольшее натуральное число $d$ такое, что $a$ кратно $d$ и $b$ кратно $d$ (т.е. остаток от деления равен 0).

**Теорема** (о линейном представлении НОД)
	Пусть $a,b \in \mathbb Z$, $b \neq 0$, $d = \text{\rm НОД}(a,b)$.
	Тогда $\exists\, u, v \in \mathbb Z \colon d = au + bv$.	
*Доказательство.*
	Построим последовательности $\{q_i\}$, $\{r_i\}$, $i = 1, 2, \dots$ по формулам:
$$
	r_0 = a, \quad r_1 = b,
$$
$$
	\label{r2}
	r_{i-1} = r_iq_{i+1} + r_{i+1}, \quad i = 1, 2, \dots
$$
	То есть делим $r_{i-1}$ на $r_i$, пока $r_i \neq 0$. Неполное частное от деления равно $q_{i+1}$, остаток от деления равен $r_{i+1}$.
	
	Алгоритм построения последовательности $\{r_i\}$ ({\it алгоритм Евклида}):
		
${\rm gcd}(a, b) = \{$
	
	\qquad $r_0 \leftarrow a; \;\; r_1 \leftarrow b; \;\; i \leftarrow 1$
	
	\qquad ${\bf while}\;\; r_i \neq 0 \;\; \{$
	
	\qquad\qquad $r_{i+1} \leftarrow r_{i-1} \bmod r_i$
	
	\qquad\qquad $i \leftarrow i + 1$
	
	\qquad $\}$	
	
	\qquad ${\bf return}\;\, r_{i-1}$
	
$\}$


Далее мы докажем, что функция $\rm gcd$ возвращает $\text{\rm НОД}(a,b)$. Алгоритм можно записать в другом виде:


${\rm gcd}(a, b) \;\langle\; a, b \in \mathbb Z, \; b \neq 0 \;\rangle = \{$

\qquad $p \leftarrow a; \;\; q \leftarrow b; \;\; i \leftarrow 1$

\qquad // $p = r_0$, $q = r_1$

\qquad ${\bf while}\;\; q \neq 0 \;\; \{$

\qquad\qquad // $p = r_{i-1}$, $q = r_i$

\qquad\qquad $r \leftarrow p \bmod q$

\qquad\qquad // $r = r_{i+1}$

\qquad\qquad $p \leftarrow q; \;\; q \leftarrow r$

\qquad\qquad // $p = r_i$, $q = r_{i+1}$

\qquad\qquad $i \leftarrow i + 1$

\qquad $\}$	

\qquad ${\bf return}\;\, p$

$\}$


Справедливы равенства [Фаддеев, с. 10]:
$$
\begin{gathered*}
a = bq_1 + r_1,\\
b = r_1q_2 + r_2,\\
r_1 = r_2q_3 + r_3,\\
\dots\\
r_{k-2} = r_{k-1}q_k + r_k,\\
r_{k-1} = r_kq_{k+1}.
\end{gathered*}
$$
При этом, по определению остатка от деления,
$$
\begin{gathered*}
0 < r_1 \leq |b| - 1,\\
0 < r_2 \leq r_1 - 1,\\
0 < r_3 \leq r_2 - 1,\\
\dots\\
0 < r_k \leq r_{k-1} - 1.
\end{gathered*}
$$
Поэтому $|b| > r_1 > r_2 > r_3 > \dots > r_k > r_{k+1} = 0$. Следовательно, алгоритм Евклида конечен.

Из цепочки равенств вытекает, что $r_{k-1}$ кратно $r_k$, затем --
что $r_{k-2}$ кратно $r_k$ как сумма двух чисел, кратных $r_k$, и т.д., получим, что $a$ и $b$ кратны $r_k$, то есть $r_k$ -- общий делитель $a$ и $b$.

Покажем, что $r_k$ -- это наибольший общий делитель $a$ и $b$.
Пусть $d'$ -- какой-нибудь общий делитель чисел $a$ и $b$.
Из первого равенства вытекает, что $r_1$ делится на $d'$ как разность двух чисел, делящихся на $d'$, из второго -- что $r_2$ делится на $d'$ по той же причине, и т.д., $r_k$ делится на $d'$. Следовательно, $r_k \geq d'$. Так что $r_k = d \equiv \text{\rm НОД}(a,b)$.

Далее построим линейное представление НОД: $d = au + bv$.
Для этого последовательно найдем линейные представления остатков $r_i$, $i = 0, 1, \ldots, k$.

Очевидно, $a = r_0 = 1 \cdot a + 0 \cdot b$,
$b = r_1 = 0 \cdot a + 1 \cdot b$, так что $r_i = au_i + bv_i$, $i = 0, 1$, где $u_0 = 1, v_0 = 0$, $u_1 = 0, v_1 = 1$.

Предположим, что нам известны линейные представления остатков $r_{i-1}$ и $r_i$:
$$
r_{i-1} = au_{i-1} + bv_{i-1},\quad r_i = au_i + bv_i.
$$
Тогда из формулы (\ref{r2}) получим, что
$$
r_{i+1} = au_{i+1} + bv_{i+1}, \quad\;\text{где}\;\;\; u_{i+1} = u_{i-1} - q_{i+1}u_i, \;\; v_{i+1} = v_{i-1} - q_{i+1}v_i.
$$
Следовательно, $d = r_k = au_k + bv_k$, поэтому можно положить
$u := u_k$, $v := v_k$.


Сформулируем *расширенный алгоритм Евклида* [Окулов, с. 74]:

${\rm gcd\_ext}(a, b) \rightarrow [d, u, v] = \{$

\qquad $r_0 \leftarrow a; \;\; r_1 \leftarrow b; \;\; i \leftarrow 1$

\qquad $u_0 \leftarrow 1; \;\; v_0 \leftarrow 0; \;\; u_1 \leftarrow 0; \;\; v_1 \leftarrow 1$

\qquad ${\bf while}\;\; r_i \neq 0 \;\; \{$

\qquad\qquad $r_{i+1} \leftarrow r_{i-1} \bmod r_i$

\qquad\qquad $q_{i+1} \leftarrow [r_{i-1} / r_i]$

\qquad\qquad $u_{i+1} \leftarrow u_{i-1} - q_{i+1}u_i; \;\;
v_{i+1} \leftarrow v_{i-1} - q_{i+1}v_i$

\qquad\qquad $i \leftarrow i + 1$

\qquad $\}$	

\qquad $d \leftarrow r_{i-1};\;\; u \leftarrow u_{i-1}; \;\; v \leftarrow v_{i-1}$

$\}$

### Литература

[Фаддеев] Фаддеев -- Лекции по алгебре

[Окулов] Окулов, Лялин, Пестов, Разова -- Алгоритмы компьютерной арифметики (2015)