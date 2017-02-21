---
layout: post
title:  "Soluzione Simpson"
categories: post
permalink: /solutions/simpson
visible: 0
---

## Soluzione Simpson

```ruby
def simpson(a, b, n)
  # Effettuiamo un controllo dell'ingresso, come al solito
  [a, b].each do |z|
    raise ArgumentError, "Deve essere un Numeric" unless z.is_a? Numeric
  end
  raise ArgumentError, "Deve essere un Fixnum" unless n.is_a? Fixnum
  raise ArgumentError, "a deve essere minore di b" unless a < b

  # Calcoliamo lo step di integrazione:
  h = (b.to_f - a.to_f)/(n.to_f)
  x = [a, a + h, a + (2 * h)]
  # Cerchiamo di scrivere un algoritmo il più
  # possibile efficiente con un solo calcolo della
  # funzione (ogni ciclo la chiama due volte invece
  # di chiamarla 3 volte)
  f = x.map { |e| yield e }
  y = 0.0

  while (x[0] + h) < b
    # Usiamo la regola di cavalieri simspon per valutare l'integrale
    y += (f[0] + 4 * f[1] + f[2])

    # Ricostruiamo il nostro vettore di f in modo tale
    # che riutilizziamo i vecchi valori di calcolo della
    # funzione facendo scorrere il vettore
    x = x[1..3] + [x[2] + h]
    f = f[1..3] + [yield(x[2])]
    # Incrementiamo di un passo lo step di integrazione
  end
  return y * (h/6)
end
```

Esempio di utilizzo:

```ruby
puts simpson(4, 12, 200) { |x| Math::sin(x) * Math::exp(-x) }
puts simpson(4, 12, 200) { |x| Math::sin(x) * (1 + x ** 2) }
```
