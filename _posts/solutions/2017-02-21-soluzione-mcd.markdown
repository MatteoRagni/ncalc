---
layout: post
title:  "Soluzione Minimo Comune Divisore"
categories: post
permalink: /solutions/mcd
visible: 0
---

## Soluzione Minimo Comune Divisore

Si forniscono le soluzioni per entrambe le strategie:

```ruby
# VERSIONE RICORSIVE
def mcd_r(a, b)
  # Controlliamo gli input
  raise ArgumentError, "a deve essere un Fixnum" unless a.is_a? Fixnum
  raise ArgumentError, "b deve essere un Fixnum" unless b.is_a? Fixnum
  # Ordiniamo a, b in x, y dove sicuramente x >= y
  x, y = (a >= b ? [a, b] : [b, a])

  # Usiamo l'algoritmo ricorsivo
  if x % y == 0
    return y
  else
    return mcd_r(x - y, y)
  end
end

# VERSIONE ITERATIVA
def mcd_i(a, b)
  # Controlliamo gli input
  raise ArgumentError, "a deve essere un Fixnum" unless a.is_a? Fixnum
  raise ArgumentError, "b deve essere un Fixnum" unless b.is_a? Fixnum
  # Ordiniamo a, b in x, y dove sicuramente x >= y
  x, y = (a >= b ? [a, b] : [b, a])

  # Usiamo l'algoritmo iterativo
  while x % y != 0
    x = x - y
    x, y = (x >= y ? [x, y] : [y, x])
  end
  return y
end
```
