---
layout: post
title:  "Soluzione Collatz"
categories: post
permalink: /solutions/collatz
visible: 0
---

## Soluzione Collatz

```ruby
def collatz(x0, x1, y0, npts)
  # Il controllo dei dati in ingresso ci è richiesto
  # dall'esercizio stesso quindi scriviamolo immediatamente
  [x0, x1, y0].each do |z|
    raise ArgumentError, "I primi tre argomenti devono essere Numeric" unless z.is_a? Numeric
  end
  raise ArgumentError, "npts deve essere un Fixnum" unless npts.is_a? Fixnum
  raise ArgumentError, "Richiesto un blocco" unless block_given?
  raise ArgumentError, "Intervallo deve essere x0 < x1" unless x0 < x1

  # Step size
  h = (x1.to_f - x0.to_f) / npts.to_f
  # Risultato da ritornare
  r = { x: [x0] , y: [y0] }

  for k in 0...npts
    yh = r[:y][-1] + (h / 2.0) * yield(r[:x][-1], r[:y][-1])

    r[:y] << r[:y][-1] + h * yield(r[:x][-1] + h / 2.0, yh)    
    r[:x] << r[:x][-1] + h
  end

  return r
end
```

Esempio d'uso:

```ruby
r = collatz(0, 2, 1, 10) { |x, y| -y - 3*x }
```
