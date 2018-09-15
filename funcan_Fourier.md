## Ряды Фурье

Источники:

1. Колмогоров, Фомин \(гл. III, пар. 4, п. 4\)
2. Треногин \(гл. I, пар. 6, п. 6.5\)
3. Zeidler Nonlinear functional analysis and its applications. II/A: Linear monotone operators \(с. 116\)

Пусть $$V$$ - гильбертово пространство, $$\{u_n\}$$ - счетная ортонормированная система в $$V$$: $$(u_i,u_j)=\delta_{ij}$$.

Ряд Фурье имеет вид


$$
u = \sum\limits_{n=1}^\infty (u_n, u)u_n\tag{1}
$$


_Определение._ Ортонормированная система $$\{u_n\}$$ называется _полной _в $$V$$, если \(1\) выполняется для всех $$u\in V$$.

Найдём наилучшее приближение элемента из $$u\in V$$ конечными линейными комбинациями $$\sum\limits_{k=1}^n c_k u_k$$.


$$
f(c_1,\ldots,c_n)=\left\| u - \sum_{k=1}^n c_ku_k \right\|^2 \to \min
$$


Это задача наименьших квадратов, которая имеет решение $$c_k = (u_k,u)$$.

Доказательство.


$$
f(c)=\|u\|^2 - 2\sum\limits_{k=1}^n c_k(u,u_k) + \sum\limits_{k=1}^n c_k^2 = \|u\|^2 - \sum\limits_{k=1}^n (u, u_k)^2 + \sum\limits_{k=1}^n ((u, u_k) - c_k)^2
$$


$$\min f(c) = \|u\|^2 - \sum\limits_{k=1}^n (u, u_k)^2$$ при $$c_k = (u_k,u)$$.

Поскольку $$f(c) \geq 0$$, то


$$
\|u\|^2 \geq \sum\limits_{k=1}^n (u, u_k)^2
$$


Данное неравенство называется неравенством Бесселя.

**Предложение \(критерий сходимости\). **Ряд $$\sum_n c_n u_n$$ сходится тогда и только тогда, когда сходится ряд $$\sum_n |c_n|^2$$.

_Доказательство._ Используем критерий Коши, полноту пространства $$V$$ и равенство


$$
\left\|\sum_{n=m}^{m+k} c_nu_n\right\|^2=\sum_{n=m}^{m+k}|c_n|^2.
$$


**Теорема. **\[Zeidler, с. 118\] Следующие условия взаимно эквивалентны:

\(i\) Ортонормированная система $$\{u_n\}$$ полная.

\(ii\) Линейная оболочка $$\{u_n\}$$ плотна в $$V$$.

\(iii\) Для любого $$u \in V$$ выполняется равенство Парсеваля $$\|u\|^2 = \sum_n |(u_n, u)|^2$$.

\(iv\) Пусть $$D$$ плотно в $$V$$. Из $$v \in D$$ и $$(u_n, v) = 0 \forall n$$ вытекает $$v=0$$.



### Дополнительно

[Ряды Фурье и вейвлет-преобразование](https://vk.com/wall-51126445_3444)

[Математика в неожиданных местах](https://youtu.be/JVDRylUg3mw)