# Функциональный анализ: примеры

## Метрические пространства

#### Пример 1

_Пространство $C[0,+\infty)$ не банахово._

Норма в этом пространстве:
$$\|y\|_{C[0,+\infty)} = \sup\limits_{t\in[0,+\infty)} y(t)$$.

Приведём пример фундаментальной, но не сходящейся последовательности.

Определим кусочно-линейную функцию с вершинами в точках $0, 1, 2, \ldots$ по следующей формуле:

$$
y_n(0) = 0,\quad y_n(k) = \max\left\{ 1 - \frac{n}{k}, 0\right\}, \; k = 1, 2, \ldots
$$


Нетрудно видеть, что для любого $n$: $y_n(1) = y_n(2) = \ldots = y_n(n) = 0$. Отсюда
$$\|y_n - y_m\|_{C[0,+\infty)} < 1/k$$, если $$n, m > k$$.
Следовательно, последовательность $y_n$ фундаментальна.

Допустим, что $y_n \to y$, т.е. $\|y_n - y\|_{C[0,+\infty)} \to 0$.
Тогда $|y_n(k) - y(k)| \to 0\;\; \forall k = 1, 2, \ldots$.

В то же время $\forall\, k = 1, 2, \ldots:\, y_n(k) \to 0,\; n \to \infty$, поэтому $y = 0$.
Но $\|y_n\| = 1 \; \forall n$, потому что $y_n(k) \to 1,\; k \to +\infty$.
Отсюда $\|y\| = 1$ -- противоречие. Следовательно, последовательность $y_n$
фундаментальна и не сходится, а значит, пространство $C[0,+\infty)$ не является полным.


## Пространства Соболева

#### Пример 2
_Справедливо вложение $$H^1(a,b) \subset C[a,b]$$, вложение строгое._

Докажем, что $$\exists u \in C[a,b] \colon u \notin H^1(a,b)$$.

$$u(x) = \sqrt{x} \in C[0,1]$$, $$u'(x) = \dfrac{1}{2\sqrt{x}}$$,

$$\displaystyle\int_0^1 (u'(x))^2\,dx = \dfrac{1}{4}\displaystyle\int_0^1 \dfrac{dx}{x} = \infty \Rightarrow u' \notin L^2(0, 1) \Rightarrow u \notin H^1(0,1)$$.

#### Пример 3

*Для функции $$x(t) \in L^2(0,\pi)$$ следующие условия равносильны:*

$$
x(t) \in H^1_0(0, \pi) \Leftrightarrow \sum_{k=1}^\infty k^2 b_k < \infty,
$$

$$
b_k = \frac{2}{\pi}\int_0^\pi x(t) \sin kt \,dt.
$$

*При этом* $$\|x(t)\|^2_{H^1} = \dfrac{\pi}{2}\sum_{k=1}^\infty (k^2+1)b_k^2$$.

(?) Где здесь учитывается, что функция равна 0 на границе?

##### Нахождение базиса в $$L^2$$ и $$H^1_0$$

Рассмотрим краевую задачу:
$$-u''(x) = f(x), \;\; x \in (0,\pi),$$
$$u(0) = u(\pi) = 0.$$

Слабая формулировка:
$$u \in H^1_0(0,\pi) \colon \int_0^\pi u' v' \,dx = \int_0^\pi fv \,dx \;\; \forall v \in H^1_0(0,\pi)$$.

Скалярное произведение в $$L^2(0,\pi)$$: $$(u,v) = \int_0^\pi uv\,dx$$.

Скалярное произведение в $$H^1_0(0,\pi)$$: $$((u,v)) = \int_0^\pi u'v'\,dx$$.

Запишем задачу в виде: $$((u,v)) = (f,v) \; \forall v \in H^1_0(0,\pi)$$.

$$f \colon H^1_0(0,\pi) \to \mathbb R: (f,v) = \int_0^\pi fv \,dx$$ - линейный непрерывный функционал, так как по неравенству Фридрихса-Пуанкаре

$$
|(f,v)| \leq \|f\|_{L^2}\|v\|_{L^2} \leq C\|f\|_{L^2}\|v\|_{H^1_0}.
$$

По теореме Рисса существует единственный элемент $$F \in H^1_0(0,\pi)$$:
$$((F,v)) = (f,v) \; \forall v \in H^1_0(0,\pi)$$.

Аналогично определим оператор $$A \colon L^2(0,\pi) \to H^1_0(0,\pi)$$:
$$((Au,v)) = (u,v)\; \forall v \in H^1_0(0,\pi)$$.

$$A \colon H^1_0(0,\pi) \to H^1_0(0,\pi)$$ - самосопряженный и компактный [Михайлов, с. 177].

Самосопряженность:

$$
((Au,v)) = (u,v) = (v,u) = ((Av,u)) = ((u,Av)).
$$

Докажем компактность. Оператор $$A \colon L^2(0,\pi) \to H^1_0(0,\pi)$$ непрерывен:

$$
\|Au\|_{H^1_0} = \sup_{\|v\|_{H^1_0} = 1} ((Au,v)) = \sup_{\|v\|_{H^1_0} = 1} (u,v) \leq C\|u\|_{L^2}.
$$

Пусть последовательность $$\{x_n\} \subset H^1_0(0,\pi)$$ ограничена, тогда в силу компактности вложения $$H^1(0,\pi) \subset L^2(0,\pi)$$ найдется подпоследовательность $$\{x_{n'}\} \colon x_{n'} \to x$$ в $$L^2(0,\pi)$$. Следовательно, в силу непрерывности оператора $$A$$ получаем, что $$Ax_{n'} \to Ax$$ в $$H^1_0(0,\pi)$$. Таким образом, оператор $$A$$ переводит ограниченное множество в относительно компактное, поэтому $$A$$ компактен.

Следовательно, по теореме Гильберта-Шмидта собственные векторы оператора $$A$$ образуют ортогональный базис в $$H^1_0(0,\pi)$$.

Найдём собственные векторы и собственные значения, для этого рассмотрим задачу Штурма-Лиувилля:

$$
-u''(x) = \lambda u(x), \; x \in (0,\pi),
$$

$$
u(0) = u(\pi) = 0.
$$

Слабая формулировка: $$u \in H^1_0(0,\pi): ((u, v)) = \lambda (u,v) = \lambda ((Au,v)) \;\; \forall v \in H^1_0(0,\pi)$$, что эквивалентно равенству $$u = \lambda Au$$.

Найдем собственные векторы и собственные значения: $$u_j = \lambda_j Au_j$$.

Задача Штурма-Лиувилля имеет решение [Алексеев, §4.1]: $$\lambda_j = j^2, \widetilde u_j(x) = \sin(jx)$$.

$$
\|\widetilde u_j\|^2_{L^2} = \int_0^\pi \sin^2(jx)\,dx = \int_0^\pi \frac{1 - \cos(2jx)}{2}\,dx = \frac{\pi}{2} - \frac{1}{4j}\sin(2jx)|_0^\pi = \frac{\pi}{2} \Rightarrow \|\widetilde u_j\| = \sqrt{\frac{\pi}{2}}.
$$

$$
u_j = \frac{\widetilde u_j}{\|\widetilde u_j\|_{L^2}} = \sqrt{\frac{2}{\pi}}\sin(jx),\; \|u_j\|_{L^2} = 1.
$$

$$
((u_j, v)) = \lambda_j(u_j, v)
$$

$$
v = u_j \Rightarrow \|u_j\|^2_{H^1_0} = \lambda_j\|u_j\|^2_{L^2} = \lambda_j
\Rightarrow
\|u_j\|_{H^1_0} = \sqrt{\lambda_j} = j
$$

$$
v_j(x) = \frac{u_j(x)}{\|u_j\|_{H^1_0}} = \frac{1}{j}\sqrt{\frac{2}{\pi}}\sin(jx)
$$

$\{v_j\}$ - ортонормированный базис в $H^1_0(0,\pi)$.

##### Разложение в ряд Фурье

$$
\forall f \in H^1(0,\pi) \colon f = \sum_{j=1}^\infty ((f,v_j))v_j
$$

$$
\|f\|^2_{H^1_0} = \sum_{j=1}^\infty |((f,v_j))|^2
$$

$$
((f,v_j)) = \lambda_j (f,v_j) = j^2 \int_0^\pi f(x)\frac{1}{j}\sqrt{\frac{2}{\pi}}\sin(jx)\,dx = j\sqrt{\frac{2}{\pi}}\int_0^\pi f(x)\sin(jx)\,dx = \sqrt{\frac{\pi}{2}}jf_j,
$$
где $$f_j = \frac{2}{\pi}\int_0^\pi f(x) \sin(jx)\,dx$$.

$$
\|f\|^2_{H^1_0} = \frac{\pi}{2}\sum_{j = 1}^\infty j^2 f_j^2.
$$

$$
f \in H^1_0(0,\pi) \Leftrightarrow \|f\|_{H^1_0}^2 < \infty \Leftrightarrow \sum_{j=1}^\infty j^2 f_j^2 < \infty.
$$

$$H^1_0(0,\pi)$$ плотно в $$L^2(0,\pi) \Rightarrow u_j$$ -- базис в $$L^2(0,\pi) \Rightarrow f = \sum_{j=1}^\infty (f,u_j)u_j$$,
$$\|f\|^2_{L^2} =
\sum_{j=1}^\infty|(f,u_j)|^2$$.

$$
(f,u_j) = \sqrt{\frac{2}{\pi}}\int_0^\pi f(x)\sin(jx)\,dx = \sqrt{\frac{\pi}{2}}f_j
$$

$$
\|f\|^2_{L^2} = \frac{\pi}{2}\sum_{j=1}^\infty f_j^2
$$

$$
\|f\|^2_{H^1} = \|f\|^2_{L^2} + \|f\|^2_{H^1_0} = \frac{\pi}{2}\sum_{j=1}^\infty (j^2+1)f_j^2.
$$
