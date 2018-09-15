Метод простой итерации
======================

Постановка задачи
-----------------

Управляемая система:

$$y_t = y_{xx} + f(t)u(x), \;\; x \in \Omega = (0,1), \; t \in (0,T),$$

$$-y_x + y|_{x=0} = 0,
\; y_x + y|_{x=1} = 0,$$

$$y|_{t=0} = y_0(x).$$

Функционал качества:

$$J(y,u) = \frac{1}{2}\int_0^1(y|_{t=T} - y_d)^2dx + \frac{N}{2} \int_0^1u^2(x)dx \to \inf.$$

Формализация задачи
-------------------

Исходные данные: $$T, N > 0$$, $$f \in L^2(0,T)$$, $$y_0,y_d \in L^2(\Omega)$$.

Пространство состояний: $$Y = \{y \in L^2(0,T;H^1(\Omega)) \colon y_t \in L^2(0,T;(H^1(\Omega))^*\}$$.

Пространство управлений, множество допустимых управлений:
$$U = U_{ad} = L^2(\Omega)$$.

Пространство правых частей:
$$Z = L^2(0,T;(H^1(\Omega))^*)\times L^2(\Omega).$$

Оператор ограничений: $$F \colon Y \times U \to Z$$,
$$F(y,u) = \{y_t + Ay - f(t)u, y|_{t=0}-y_0\}$$.

$$
A:H1(Ω)→(H1(Ω))∗,
(Ay,z) = (y_x,z_x) +
y|_{x=1}\cdot z|_{x=1} +
y|_{x=0}\cdot z|_{x=0}.
$$


## Система оптимальности


Функционал Лагранжа:
$$L(y,u,p,q) = \frac{1}{2}\|y_{t=T} - y_d\|^2 + \frac{N}{2}\|u\|^2 + \int_0^T(y_t + Ay - f(t)u, p)dt + (y|_{t=0} - y_0, q),$$
$$\{p,q\} \in Z^*,\; p \in L^2(0,T;H^1(\Omega)), \; q \in L^2(\Omega).$$

Приведенный фунционал:

$$
\widehat J(u) = J(y(u),u).
$$
$$
\widehat J'(u) = L_u(y(u),u,p(u))
$$,
где $$p = p(u)$$ — решение сопряженного уравнения
$$
\tag{sopr}
L_y(y(u),u,p) = 0.
$$

**Теорема 1.** *Пусть $$(\overline y, \overline u)$$ — решение задачи управления. Тогда
существует множитель Лагранжа $$\overline p \in Z^*$$, такой, что*
$$
\tag{so1}
F(\overline y, \overline u) = 0,
$$
$$\tag{so2}
L_y(\overline y, \overline u, \overline p) = 0,
$$
$$\tag{so3}
L_u(\overline y, \overline u, \overline p) = 0.
$$

Соотношения (so1)–(so3) образуют систему оптимальности.

$$L_y \colon Y \to Z$$, $$L_u \colon U \to Z$$,

$$
(L_y,h) = (y|_{t=T} - y_d, h|_{t=T}) + \int_0^T(h_t + Ah, p)dt + (h|_{t=0},q)\;\;
\forall h \in Y.
$$

Условие $$L_y(y,u,p) = 0$$ равносильно следующему
уравнению:

$$
-p_t + Ap = 0 \mbox{ п.в. на } (0,T),$$
$$
p|_{t=T} = y_d - y|_{t=T}.
$$

Далее,

$$
(L_u, v) = N(u,v) - \int_0^Tf(t)(v,p)dt = \left(Nu - \int_0^Tf(t)p\,dt, v\right)dt \;\; \forall v \in U.
$$

Таким образом, условие $$L_u(y,u,p)=0$$ равносильно

$$
u(x) = \frac{1}{N}\int_0^T f(t)p(x,t)dt.
$$

Кроме того,

$$
\tag{grad}
\widehat J'(u) = Nu - \int_0^T f(t)pdt,
$$

где $$p = p(u)$$ — решение сопряженного уравнения (sopr).

Функционал $$\widehat J' \in U^*$$ будем отождествлять с элементом из $$U$$,
называемым градиентом функционала $$\widehat J$$.

Система оптимальности:
$$y_t = y_{xx} + f(t)u(x), \;\; x \in \Omega = (0,1), \; t \in (0,T),$$
$$-y_x + y|_{x=0} = 0, \; y_x + y|_{x=1} = 0,$$ $$y|_{t=0} = y_0(x),$$
$$-p_t = p_{xx}, \;\; x \in \Omega, \; t \in (0,T),$$
$$-p_x + p|_{x=0} = 0, \; p_x + p|_{x=1} = 0,$$
$$p|_{t=T} = y_d - y|_{t=T},$$
$$u(x) = \frac{1}{N}\int_0^T f(t)p(x,t)dt,\;\; x \in (0,1).$$

Численный алгоритм
------------------

Для решения системы оптимальности предлагается использовать метод
градиентного спуска:
$$\tag{spusk}
u^{k+1} = u^k - \lambda \widehat J'(u^k),
$$
где $$\lambda > 0$$ -- итерационный параметр.

С учетом (grad) метод принимает вид:
$$
u^{k+1} = u^k - \lambda\left(Nu^k - \int_0^T f(t)pdt\right) =
u^k(1-\lambda N) + \lambda \int_0^T f(t)pdt.
$$
Здесь $$p = p(u^k)$$.

При $$\lambda = 1/N$$ метод градиентного спуска переходит в метод простой
итерации.

Докажем, что при достаточно малых $$\lambda$$ метод градиентного спуска
сходится. В [Поляк; Ахмеров] доказано для конечномерного случая, что
если производная целевой функции удовлетворяет условию Липшица, то при
малых $$\lambda$$ производная $$f'(x^k)$$ стремится к 0. Более того, если функция сильно выпукла, то $$x^k \to x^*$$ ($$x^*$$ — точка минимума) со
скоростью геометрической прогрессии.

**Лемма 1.** *Для любой функции $$y \in H^1(\Omega)$$:*
$$
\|y_x\|^2 + y^2|_{x=1} + y^2|_{x=0} \geq \|y\|^2.
$$

*Доказательство.*

$$
\int_0^1 x(y^2)_x\,dx= xy^2|_0^1 - \int_0^1 y^2\,dx = y^2|_{x=1} - \|y\|^2,
$$
$$
\int_0^1 (x-1)(y^2)_x\,dx= (x-1)y^2|_0^1 - \int_0^1 y^2\,dx = y^2|_{x=0} - \|y\|^2,
$$
$$
2\|y\|^2 = -2\int_0^1(2x-1)yy_x\,dx + y^2|_{x=1} + y^2|_{x=0} \leq
2\|y\|\|y_x\| + y^2|_{x=1} + y^2|_{x=0},
$$
$$
2\|y\|^2 \leq \|y\|^2 + \|y_x\|^2 + y^2|_{x=1} + y^2|_{x=0},
$$
$$
\|y\|^2 \leq \|y_x\|^2 + y^2|_{x=1} + y^2|_{x=0}.
$$

**Лемма 2.**
*Существует константа $$M > 0$$ такая, что для любых $$u_1, u_2 \in U$$*:
$$
\|\widehat J'(u_1) - \widehat J'(u_2)\| \leq M\|u_1 - u_2\|.
$$

*Доказательство.*

$$
\widehat J'(u) = Nu - \int_0^Tfp(u)dt.
$$
$$
\|\widehat J'(u_1) - \widehat J'(u_2)\| \leq N\|u_1 - u_2\|_{L^2(\Omega)} +
\left\|\int_0^Tf(p(u_1) - p(u_2))dt\right\|_{L^2(\Omega)}.
$$
$$
\left\|\int_0^Tf(p(u_1) - p(u_2))dt\right\|_{L^2(\Omega)}^2 =
\int_0^1\left(\int_0^Tf(p(u_1) - p(u_2))dt \right)^2dx.
$$
$$
\int_0^T 1\cdot g(t)dt \leq \left( \int_0^T 1 dt\right)^{1/2}\cdot
\left( \int_0^T g^2(t) dt\right)^{1/2},
$$
$$
\left(\int_0^T 1\cdot g(t)dt\right)^2 \leq T\int_0^T g^2(t) dt.
$$
$$
\left\|\int_0^Tf(p(u_1) - p(u_2))dt\right\|_{L^2(\Omega)}^2 \leq
T\int_0^1\int_0^Tf^2(p(u_1) - p(u_2))^2dt \leq
$$
$$
\leq T\|f\|^2_{L^\infty(0,T)}\int_0^T
\|p(u_1) - p(u_2)\|^2dt.
$$

Таким образом,
$$
\tag{ok1}
\|\widehat J'(u_1) - \widehat J'(u_2)\| \leq N\|u_1 - u_2\|_{L^2(\Omega)} +
\sqrt{T}\|f\|_{L^\infty(0,T)}\left(\int_0^T
\|p(u_1) - p(u_2)\|^2dt\right)^{1/2}.
$$

Осталось получить оценку непрерывности оператора $$p(u)$$.

Обозначим $$y_1 = y(u_1)$$, $$y_2 = y(u_2)$$, $$p_1 = p(u_1)$$,
$$p_2 = p(u_2)$$, $$u = u_1 - u_2$$, $$y = y_1 - y_2$$, $$p = p_1 - p_2$$. Тогда
$$\tag{a1}
y_t + Ay = f(t)u \;\mbox { п.в. на } (0,T),
$$
$$\tag{a2}
y|_{t=0} = 0,
$$
$$\tag{a3}
-p_t + Ap = 0 \;\mbox { п.в. на } (0,T),
$$
$$\tag{a4}
p|_{t=T} = -y|_{t=T}.
$$

Из (a1) получаем
$$
(y_t,v) + (y_x,v_x) + y|_{x=1}\cdot v|_{x=1} + y|_{x=0}\cdot v|_{x=0} =
(f(t)u,v)\;\; \forall v \in H^1(\Omega) \; \mbox{ п.в. на } (0,T).
$$

Положим $$v = y$$.
$$
\frac{1}{2}\frac{d\|y\|^2}{dt} + \|y_x\|^2 + y^2|_{x=1} + y^2|_{x=0} =
(f(t)u, y),
$$
$$
(f(t)u, y) \leq \|f\|_{L^\infty(0,T)}\|y\|\|u\| =
\sqrt{2}\|y\|\cdot\frac{\|f\|_{L^\infty(0,T)}}{\sqrt{2}}\|u\| \leq
\|y\|^2 + \frac{1}{4}\|f\|_{L^\infty(0,T)}^2\|u\|^2.
$$

Используя лемму 1, получаем
$$
\frac{1}{2}\frac{d\|y\|^2}{dt} \leq \frac{1}{4}\|f\|_{L^\infty(0,T)}^2\|u\|^2.
$$

Отсюда $$
\|y(T)\|^2 \leq \frac{T\|f\|_{L^\infty(0,T)}^2}{2}\|u\|^2,
$$
$$
\|y(T)\| \leq \sqrt{\frac{T}{2}}\|f\|_{L^\infty(0,T)}\|u\|.
$$

Из (a3) получаем
$$
-(p_t,v) + (y_x,v_x) + y|_{x=1}\cdot v|_{x=1} + y|_{x=0}\cdot v|_{x=0} = 0
\;\; \forall v \in H^1(\Omega) \; \mbox{ п.в. на } (0,T).
$$

Положим $$v = p$$.
$$
-\frac{1}{2}\frac{d\|p\|^2}{dt} + \|p_x\|^2 + p^2|_{x=1} + p^2|_{x=0} = 0.$$
По лемме 1
$$
-\frac{1}{2}\frac{d\|p\|^2}{dt} + \|p\|^2 \leq 0.
$$

Проинтегрировав это неравенство по $$(t,T)$$, получим
$$
-\frac{1}{2}\|y(T)\|^2 + \frac{1}{2}\|p(t)\|^2 + \int_t^T\|p(t)\|^2dt \leq 0.
$$
Отсюда
$$
\int_0^T\|p(t)\|^2dt \leq \frac{1}{2}\|y(T)\|^2,
$$
$$
\left(\int_0^T\|p(t)\|^2dt\right)^{1/2} \leq \frac{1}{\sqrt{2}}\|y(T)\|.
$$

Таким образом,
$$
\left(\int_0^T
\|p(u_1) - p(u_2)\|^2dt\right)^{1/2} \leq
\frac{\sqrt{T}}{2}\|f\|_{L^\infty(0,T)}\|u_1 - u_2\|.
$$

Тогда из (ok1) получим
$$
\|\widehat J'(u_1) - \widehat J'(u_2)\| \leq N\|u_1 - u_2\| +
\frac{T}{2}\|f\|_{L^\infty(0,T)}^2\|u_1 - u_2\|.
$$

Итак,
$$
\|\widehat J'(u_1) - \widehat J'(u_2)\| \leq M\|u_1 - u_2\|,
$$
где
$$
M = N + \frac{T}{2}\|f\|_{L^\infty(0,T)}^2.
$$

**Теорема 2.**
*Пусть $$\lambda$$ удовлетворяет условию $$0 < \lambda < 2/M$$. Тогда в
методе градиентного спуска (spusk) градиент стремится к 0:*
$$
\widehat J'(u^k) \to 0 \mbox{ сильно в } L^2(\Omega),
$$
*а функция $$\widehat J(u)$$ монотонно убывает:*
$$
\widehat J(u^{k+1}) \leq \widehat J(u^k).
$$

<span>*Доказательство.* </span>

Функционал $$\widehat J(u)$$ непрерывно дифференцируем как суперпозиция
непрерывно дифференцируемых операторов $$J(y,u)$$ и $$y(u)$$. Поэтому
отображение $$z \mapsto (\widehat J'(z), h)$$ непрерывно на отрезке
$$z \in [u, u+h]$$. Следовательно, по теореме о среднем значении [Иоффе, Тихомиров,
с. 38]
$$
\widehat J(u+h) - \widehat J(u) = \int_0^1 (\widehat J'(u+th), h)dt.
$$
$$
\tag{p1}
\widehat J(u+h) - \widehat J(u) =
(\widehat J'(u), h) +
\int_0^1 (\widehat J'(u+th) - \widehat J'(u), h)dt \;\; \forall u, h \in U.
$$

Полагая в (p1) $$u = u^k$$, $$h = -\lambda \widehat J'(u^k)$$, получим
$$
\widehat J(u^{k+1}) - \widehat J(u^k) =
-\lambda\|\widehat J'(u^k)\|^2
-\lambda\int_0^1 (\widehat J'(u^k-t\lambda \widehat J'(u^k)) - \widehat J'(u^k),
\widehat J'(u^k))dt.
$$

По лемме 2
$$
\|\widehat J'(u^k-t\lambda \widehat J'(u^k)) - \widehat J'(u^k)\| \leq
Mt\lambda\|\widehat J'(u^k) \|.
$$

Отсюда
$$
\left|\int_0^1 (\widehat J'(u^k-t\lambda \widehat J'(u^k)) - \widehat J'(u^k),
\widehat J'(u^k))dt\right| \leq M\lambda\|\widehat J'(u^k) \|^2\int_0^1t\,dt =
\frac{1}{2}M\lambda\|\widehat J'(u^k) \|^2.
$$

Следовательно,
$$
\widehat J(u^{k+1}) - \widehat J(u^k) \leq
-\lambda\|\widehat J'(u^k)\|^2 + \frac{1}{2}M\lambda^2\|\widehat J'(u^k) \|^2 =
-\lambda\left( 1 - \frac{1}{2}M\lambda \right)\|\widehat J'(u^k) \|^2.
$$

Суммируя неравенства
$$
\widehat J(u^{k+1}) - \widehat J(u^k) \leq -\alpha\|\widehat J'(u^k) \|^2,\quad
\alpha = \lambda\left( 1 - \frac{1}{2}M\lambda \right) > 0
$$
по $$k$$ от 0 до $$n$$, получаем
$$
\widehat J(u^{n+1}) - \widehat J(u^0) \leq -\alpha \sum_{k=0}^n\|\widehat J'(u^k) \|^2,
$$
$$
\sum_{k=0}^n\|\widehat J'(u^k) \|^2 \leq \frac{1}{\alpha}
(\widehat J(u^{0}) - \widehat J(u^{n+1})) \leq
\frac{1}{\alpha}
\widehat J(u^{0})$$ при всех $$n$$.
Следовательно,
$$
\sum_{k=0}^\infty\|\widehat J'(u^k) \|^2 < \infty.
$$
Отсюда $$\|\widehat J'(u^k) \| \to 0.$$

**Следствие 1.** *Если $$N > M/2$$, то в методе простой итерации градиент стремится к 0, а
функционал монотонно убывает.*

Условие $$N > M/2$$ можно переписать в виде
$$
N > \frac{T}{2}\|f\|_{L^\infty(0,T)}^2.
$$

**Определение 1.** *Функционал $$J \colon V \to \mathbb R$$ называется сильно выпуклым с
константой $$C > 0$$, если для любых $$u, v \in V$$, $$\theta \in [0,1]$$*:
$$
J(u + \theta(v-u)) \leq J(u) + \theta(J(v) - J(u)) - \frac{1}{2}C\theta(1-\theta)\|v-u\|^2.
$$

**Лемма 3.** [Поляк, с. 20] *Для дифференцируемой функции $$f(x)$$ на $$\mathbb R^n$$
сильная выпуклость эквивалентна неравенству*
$$
f(x+y) \geq f(x) + (\nabla f(x), y) + C\|y\|^2/2.
$$

** Лемма 4.** *Пусть функционал $$J \colon V \to \mathbb R$$ дифференцируем по Гато на
$$V$$. Тогда $$J$$ сильно выпуклый тогда и только тогда, когда для любых
$$u,v \in V$$:*
$$
J(v) - J(u) \geq J'(u,v-u) + \frac{C}{2}\|v-u\|^2.
$$

*Доказательство.*

Пусть $$u, v \in V$$. Введем функцию
$$\varphi(t) = J(u + t(v-u)),\; t \in [0,1]$$. Заметим, что
$$\varphi'(t) = J'(u + t(v-u), v-u)$$.

Если $$J$$ сильно выпуклый с константой $$C$$, то для любого
$$\theta \in [0,1]$$:
$$
\varphi(\theta) \leq \varphi(0) + \theta\varphi(1) -
\frac{1}{2}C\theta(1-\theta)\|u-v\|^2,
$$
то есть функция $$\varphi(t)$$
сильно выпукла с константой $$C\|u-v\|^2$$. Тогда по лемме 3
$$
\varphi(1) \geq \varphi(0) + \varphi'(0) + \frac{C}{2}\|u-v\|^2.
$$
Следовательно,
$$
J(v) \geq J(u) + J'(u,v-u) + \frac{C}{2}\|u-v\|^2.
$$

Доказательство в обратную сторону проводится аналогично.

**Лемма 5.** *Пусть функционал $$J \colon V \to \mathbb R$$ дважды дифференцируем по
Гато и для любых $$u, \varphi \in V$$:*
$$
J''(u,\varphi,\varphi) \geq C\|\varphi\|^2.
$$
*Тогда $$J$$ сильно выпуклый с константой $$C$$.*

*Доказательство.*

Пусть $$u, v \in V$$. Существует
$$\theta \in (0,1)$$, такое, что
$$J(v) = J(u) + J'(u,v-u) + \frac{1}{2}J''(u + \theta(v-u), v-u, v-u) \geq
J(u) + J'(u,v-u) + \frac{C}{2}\|v-u\|^2.$$
По лемме 4 $$J$$ сильно выпуклый.

Заметим, что функционал
$$
J(y,u) = J_1(y|_{t=T}) + J_2(u),
$$
$$
J_1(y|_{t=T}) = \frac{1}{2}\int_0^1(y|_{t=T} - y_d)^2dx, \quad J_2(u) = \frac{N}{2}
\int_0^1u^2(x)dx
$$
сильно выпуклый по $$y$$ и $$u$$, так как
$$
J''_1(y,\varphi,\psi) = (\varphi,\psi),\quad
J''_2(u,\varphi,\psi) = N(\varphi,\psi),
$$
$$
J''_1(y,\varphi,\varphi) = \|\varphi\|^2,\quad
J''_2(u,\varphi,\varphi) = N\|\varphi\|^2.
$$

Отсюда следует, что функционал
$$\widehat J(u) = J(y(u),u) = J_1(y(u)) + J_2(u)$$ сильно выпуклый в силу
аффинности оператора $$y(u)$$. Действительно,
$$
J_1(y((1-\theta)u + \theta v)) =
J_1((1-\theta)y(u) + \theta y(v)) \leq
$$
$$
\leq
(1-\theta)J_1(y(u)) +
\theta J_1(y(v)) - \frac{1}{2}\theta(1-\theta)\|y(u)|_{t=T} - y(v)|_{t=T}\|^2 \leq
$$
$$
\leq
(1-\theta)J_1(y(u)) +
\theta J_1(y(v)).
$$

Для функционала $$J_2$$:
$$
J_2((1-\theta)u + \theta v) \leq
(1-\theta)J_2(u) + \theta J_2(v) - \frac{N}{2}\theta(1-\theta)\|u - v\|^2.
$$
Складывая два последних неравенства, получаем, что
$$
\widehat J((1-\theta)u + \theta v) \leq (1-\theta)\widehat J(u) +
\theta\widehat J(v) - \frac{N}{2}\theta(1-\theta)\|u - v\|^2,
$$ то есть
функционал
$$\widehat J(u)$$ сильно выпуклый с константой $$N$$.

**Лемма 6.** *Пусть $$u^*$$ — точка минимума функционала $$\widehat J(u)$$. Тогда*
$$
\widehat J(u) \geq \widehat J(u^*) + \frac{N}{2}\|u - u^*\|^2.
$$

*Доказательство.*

По лемме 4
$$
\widehat J(u) - \widehat J(u^*) \geq \widehat J'(u^*,u-u^*) +
\frac{C}{2}\|u-u^*\|^2.
$$
Так как $$\widehat J'(u^*) = 0$$, то
$$
\widehat J(u) \geq \widehat J(u^*) + \frac{N}{2}\|u - u^*\|^2.
$$

**Лемма 7.** *Пусть $$u^*$$ — точка минимума функционала $$\widehat J(u)$$. Тогда*
$$
\|\widehat J'(u)\|^2 \geq 2N(\widehat J(u) - \widehat J(u^*)).
$$

*Доказательство.*

Положим в лемме 4 $$v = u^*$$. Тогда
$$
\widehat J(u^*) - \widehat J(u) \geq (\widehat J'(u), u^*-u) + \frac{N}{2}\|u^*-u\|^2,
$$
$$
\widehat J(u) - \widehat J(u^*) + \frac{N}{2}\|u^*-u\|^2 \leq
(\widehat J'(u), u-u^*) \leq \|\widehat J'(u)\|\|u-u^*\| =
$$
$$
= \sqrt{N}\|u-u^*\|\cdot\frac{1}{\sqrt{N}}\|\widehat J'(u)\| \leq
\frac{N}{2}\|u-u^*\|^2 + \frac{1}{2N}\|\widehat J'(u)\|^2.
$$
Следовательно,
$$
\|\widehat J'(u)\|^2 \geq 2N(\widehat J(u) - \widehat J(u^*)).
$$

**Теорема 3.** *При $$0 < \lambda < 2/M$$ метод градиентного спуска (spusk) сходится к
единственной точке глобального минимума $$u^*$$ со скоростью
геометрической прогрессии:*
$$
\|u^k - u^*\| \leq cq^k,\quad 0 < q < 1.
$$

*Доказательство.*
Из рассуждений теоремы 2 следует, что
$$
\widehat J(u^{k+1}) - \widehat J(u^k) \leq
-\lambda\left( 1 - \frac{1}{2}M\lambda \right)\|\widehat J'(u^k) \|^2.
$$

Используем лемму 7:
$$\widehat J(u^{k+1}) - \widehat J(u^k) \leq
-N\lambda(2 - M\lambda)(\widehat J(u^k) - \widehat J(u^*)).
$$
Отсюда
$$
\widehat J(u^{k+1}) - \widehat J(u^*) \leq
(1 -N\lambda(2 - M\lambda))(\widehat J(u^k) - \widehat J(u^*)) =
q(\widehat J(u^k) - \widehat J(u^*)),
$$
$$
q = 1 -2N\lambda + MN\lambda^2,\quad 0 < q < 1,
$$
$$
\widehat J(u^{k}) - \widehat J(u^*) \leq q^k(\widehat J(u^0) - \widehat J(u^*)).
$$
Следовательно, $$\widehat J(u^{k}) \to \widehat J(u^*)$$.

Из леммы 6 следует, что
$$
\|u^k - u^*\|^2 \leq \frac{2}{N}(\widehat J(u^k) - \widehat J(u^*)) \leq
\frac{2}{N}q^k(\widehat J(u^0) - \widehat J(u^*)).
$$
Следовательно, $$u^k \to u^*$$ сильно в $$U$$.

## Литература

Поляк Б.Т. Введение в оптимизацию. М.: Наука, 1983.

Ахмеров Р.Р. Методы оптимизации гладких функций.
URL: http://www.sbras.ru/rus/textbooks/akhmerov/mo_unicode/index.html

Иоффе А.Д., Тихомиров В.М. Теория экстремальных задач. М: Наука, 1974.
