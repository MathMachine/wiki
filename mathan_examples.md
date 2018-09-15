## Математический анализ: примеры

### Объём n-мерного шара и площадь сферы

Источники:
1. [Демидов Обобщенные функции в математической физике](https://yadi.sk/d/AfVY7fW3HJQy6g), с. 8
2. [How to derive the volume of an n-dimensional hypersphere](https://youtu.be/eEJtMFdkzzU)
3. [Hypersphere: MathWorld](http://mathworld.wolfram.com/Hypersphere.html)

$$B_n$$ - единичный шар в $$\mathbb R^n$$, $$\sigma_n$$ - площадь поверхности единичной ($$n-1$$)-мерной сферы в $$\mathbb R^n$$

$$
|B_n| = \int_0^1 r^{n-1}\sigma_n dr = \dfrac{\sigma_n}{n}
$$

[Дискуссия на форуме](https://groups.google.com/forum/#!topic/mathdvfu/bdHIOA2K1YE) по поводу этой формулы

Найдём $$\sigma_n$$.

$$
\int_{\mathbb R^n} e^{-|x|^2}dx = \int_{\mathbb R^n} e^{-(|x_1|^2 + |x_2|^2 + \ldots + |x_n|^2)}dx =
$$
$$
= \left(\int_{-\infty}^{+\infty}e^{-|x_1|^2}dx_1\right)\left(\int_{-\infty}^{+\infty}e^{-|x_2|^2}dx_2\right)\ldots\left(\int_{-\infty}^{+\infty}e^{-|x_n|^2}dx_n\right)
= \left(\int_{-\infty}^{+\infty} e^{-t^2} dt\right)^n.
$$

![Картинка от Физтех.Радио](/images/fun/cat1.jpg)

Делаем замену:

$$
\int_{\mathbb R^n} e^{-|x|^2}dx = \int_0^\infty e^{-r^2}r^{n-1}\sigma_n dr
$$

(Здесь $$r^{n-1}\sigma_n$$ - площадь сферы радиуса $$r$$.)

$$\Gamma(\lambda) = \int_0^\infty t^{\lambda - 1}e^{-t}dt$$, где $${\rm Re}\, \lambda > 0$$ - гамма-функция Эйлера.

$$\int_0^\infty e^{-r^2}r^{n-1}dr = \int_0^\infty e^{-r^2}r^{n-2}rdr =
\frac{1}{2}\int_0^\infty e^{-r^2}e^{2(\frac{n}{2}-1)}d(r^2) = \frac{1}{2}\int_0^\infty e^{-t}t^{\frac{n}{2} - 1}dt = \frac{1}{2}\Gamma(n/2)$$

Итак,

$$
\tag{1}
\left(\int_{-\infty}^{+\infty} e^{-t^2}dt\right)^n = \frac{1}{2}\Gamma\left(\frac{n}{2}\right)\sigma_n
$$

При $$n = 2$$: $$\left(\int_{-\infty}^{+\infty} e^{-t^2}dt\right)^2 = \pi\Gamma(1) =
\pi\int_0^\infty e^{-t}dt = \pi$$.

Поэтому

$$
\int_{-\infty}^{+\infty} e^{-t^2}dt = \sqrt{\pi}
$$

Из формулы (1):

$$
\pi^{n/2} = \frac{1}{2}\Gamma\left(\frac{n}{2}\right)\sigma_n \Rightarrow \sigma_n = \frac{2\pi^{n/2}}{\Gamma(\frac{n}{2})}
$$

При $$n = 3$$:

$$
\sigma_3 = 4\pi = \frac{2\pi^{3/2}}{\Gamma(\frac{3}{2})} \Rightarrow 2\Gamma\left(\frac{3}{2}\right) = \sqrt{\pi} \Rightarrow \Gamma\left(\frac{3}{2}\right) = \frac{\sqrt{\pi}}{2}.
$$

$$
\Gamma(\lambda + 1) = \lambda\Gamma(\lambda) \Rightarrow\Gamma(n+1) = n!
$$

$$
\sigma_5 = \sigma_{2\cdot 2 + 1} = \dfrac{2\pi^{2 + 1/2}}{\Gamma(5/2)} =
\dfrac{2\pi^{2 + 1/2}}{3/2 \cdot \Gamma(3/2)}
= \dfrac{2\pi^{2}}{3/2 \cdot 1/2}.
$$

Итак,

$$
\sigma_{2n} = \frac{2\pi^n}{(n-1)!}, \quad \sigma_{2n+1} = \frac{2\pi^n}{(n-1/2)\cdot(n-3/2)\cdot\ldots\cdot 3/2 \cdot 1/2}.
$$

Отметим, что
$$
\Gamma\left(\frac{1}{2}\right) = \int_0^\infty t^{-1/2}e^{-t}dt = 2\int_0^\infty e^{-t}d(\sqrt{t}) = 2\int_0^\infty e^{-x^2}dx = \int_{-\infty}^{+\infty} e^{-x^2}dx = \sqrt{\pi},
$$

$$
\Gamma\left(\frac{3}{2}\right) = \frac{\sqrt{\pi}}{2}.
$$
