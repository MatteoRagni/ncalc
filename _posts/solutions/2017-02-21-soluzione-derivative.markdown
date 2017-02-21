---
layout: post
title:  "Soluzione Derivative"
categories: post
permalink: /solutions/derivative
visible: 0
---

## Soluzione Derivative

```ruby
def derivative(x, h)
  # Valutazione delle
  [x, h].each do |z|
    raise ArgumentError, "deve essere Numeric" unless z.is_a? Numeric
  end
  raise ArgumentError, "h < 0" unless h > 0
  raise ArgumentError, "Manca blocco f(x)" unless block_given?

  # Riduciamo il numero di valutazioni con una pre-analisi
  z = [x.to_f - h,   x.to_f,      x.to_f + h]
  f = z.map { |e| yield(e) }

  # Ritorniamo il valore
  return {
    central:  (f[2] - f[0]) / (2 * h),
    forward:  (f[2] - f[1]) / h,
    backward: (f[1] - f[0]) / h,
    order2:   (f[2] - 2 * f[1] + f[0]) / (h ** 2.0)
  }
end
```

Esempio d'uso:

```ruby
r1 = derivative(5,0.01) { |x| x**2 - 1 }
r2 = derivative(1,0.002) { |x| Math::exp(x) * x }
```
