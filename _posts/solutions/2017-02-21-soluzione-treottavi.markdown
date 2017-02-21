---
layout: post
title:  "Soluzione Tre Ottavi"
categories: post
permalink: /solutions/treottavi
visible: 0
---

## Soluzione Tre Ottavi

```ruby
def tre_ottavi(a, b, n)
  # Effettuiamo un controllo dell'ingresso, come al solito
  [a, b].each do |z|
    raise ArgumentError, "Deve essere un Numeric" unless z.is_a? Numeric
  end
  raise ArgumentError, "Deve essere un Fixnum" unless n.is_a? Fixnum
  raise ArgumentError, "a deve essere minore di b" unless a < b

  # Calcoliamo lo step di integrazione:
  h = (b.to_f - a.to_f)/(3 * n.to_f)
  x = a
  y = 0
  # Cerchiamo di scrivere un algoritmo il più
  # possibile efficiente con un solo calcolo della
  # funzione (ogni ciclo la chiama una volta invece
  # di chiamarla 4 volte)
  f = [yield(x), yield(x + h), yield(x + 2*h), yield(x + 3*h)]

  while (x + 3*h) < b
    y += h/8 * (f[0] + 3 * f[1] + 3 * f[2] + f[3])

    # Ricostruiamo il nostro vettore di f in modo tale
    # che riutilizziamo i vecchi valori di calcolo della
    # funzione facendo scorrere il vettore
    f = f[1..3] + [yield(x + 3*h)]
    # Incrementiamo di un passo lo step di integrazione
    x += h
  end
  return y
end
```

Esempio di utilizzo:
```ruby
puts tre_ottavi( 4, 12, 50 ) { |x| Math::sin(x)*Math::exp(-x) }
```
