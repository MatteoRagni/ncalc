---
layout: post
title:  "Soluzione Minimo Comune Multiplo"
categories: post
permalink: /solutions/mcm
visible: 0
---

## Soluzione Minimo Comune Multiplo

```ruby
# costruiamo una funzione di massimo comun divisore giusto per semplificarci
# la vita in seguito nella funzionedi minimo comune multiplo
def mcd_r(a, b)
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

# Costruiamo anche la versione iterativa come esercizio
def mcd_i(a, b)
  raise ArgumentError, "a deve essere un Fixnum" unless a.is_a? Fixnum
  raise ArgumentError, "b deve essere un Fixnum" unless b.is_a? Fixnum

  x, y = (a >= b ? [a, b] : [b, a])

  while x % y != 0
    x = x - y
    x, y = (x >= y ? [x, y] : [y, x])
  end
  return y
end

# Ed ecco la soluzione:
def mcm(a,b)
  raise ArgumentError, "a deve essere un Fixnum" unless a.is_a? Fixnum
  raise ArgumentError, "b deve essere un Fixnum" unless b.is_a? Fixnum

  return a * b / mcd_r(a, b)
end
```
