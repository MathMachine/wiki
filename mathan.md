## Математический анализ

- [Примеры](mathan_examples.md)

### Источники

1. [Лекции Ю.А. Клевчихина](https://yadi.sk/d/uM4I2FCJ3Ky46Y)

### Линейные ОДУ

$$
f'(s) + \mu(s)f(s) = Q(s)
$$

Домножим уравнение на интегрирующий множитель $$\exp\left(\int_0^s \mu(x) dx\right)$$.

$$
f'(s)\exp\left(\int_0^s \mu(x) dx\right) + \mu(s)f(s)\exp\left(\int_0^s \mu(x) dx\right) = Q(s)\exp\left(\int_0^s \mu(x) dx\right)
$$

$$
\left( f(s)e^{\int_0^s \mu(x) dx} \right)' = Q(s)e^{\int_0^s \mu(x) dx}
$$

Проинтегрируем полученное выражение от 0 до $$t$$.

$$
f(t)e^{\int_0^t \mu(x) dx} = f(0) + \int_0^t Q(s)e^{\int_0^s \mu(x) dx}\, ds
$$

$$
f(t) = f(0)e^{-\int_0^t \mu(x) dx} + e^{-\int_0^t \mu(x) dx}\int_0^t Q(s)e^{\int_0^s \mu(x) dx}\, ds =
$$

$$
= f(0)e^{-\int_0^t \mu(x) dx} + \int_0^t Q(s)e^{- \int_s^t \mu(x) dx}\, ds.
$$
