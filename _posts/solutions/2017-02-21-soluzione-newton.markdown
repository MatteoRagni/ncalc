---
layout: post
title:  "Soluzione Newton"
categories: post
permalink: /solutions/newton
visible: 0
---

## Soluzione Newton

```ruby
def newton(x0, maxiter, tol)
  # Controlliamo gli input
  [x0, tol].each do |z|
    raise ArgumentError, "deve essere Numeric" unless z.is_a? Numeric
  end
  raise ArgumentError, "tol deve essere > 0" unless tol > 0
  raise ArgumentError, "maxiter deve essere Fixnum" unless maxiter.is_a? Fixnum

  x = x0.to_f
  i = 0

  while i < maxiter
    i += 1
    f, df = yield(x)

    # Se siamo sotto tolleranza ritorna x
    return x if f.abs < tol
    # altrimenti ricalcoliamo x
    x = x - f / df
  end
  # Se siamo arrivati qui non siamo a convergenza
  # quindi ritorniamo nil
  return nil
end
```

Esempio di utlizzo:

```ruby
puts newton(1, 100, 1e-8) { |x| [ x**2 - 2.0, 2.0*x ] }
```
