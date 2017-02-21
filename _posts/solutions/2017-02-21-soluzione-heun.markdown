---
layout: post
title:  "Soluzione Heun"
categories: post
permalink: /solutions/heun
visible: 0
---

## Soluzione Heun

```ruby
def heun( x0, x1, y0, npts, &blocco )
  # Il controllo dei dati in ingresso ci è richiesto
  # dall'esercizio stesso quindi scriviamolo immediatamente
  [x0, x1, y0].each do |z|
    raise ArgumentError, "I primi tre argomenti devono essere Numeric" unless z.is_a? Numeric
  end
  raise ArgumentError, "npts deve essere un Fixnum" unless npts.is_a? Fixnum
  raise ArgumentError, "Richiesto un blocco" unless block_given?
  raise ArgumentError, "Intervallo deve essere x0 < x1" unless x0 < x1

  # Calcoliamo il valore dello step
  h = (x1 - x0) / npts.to_f
  # E l'oggetto che restituiremo
  res = { x: [x0], y: [y0] }

  # Questo ciclo for implementa esattamente quanto descritto
  # nel testo dell'esercizio. Yield chiama quanto contenuto
  # nel blocco esterno
  for i in 0...npts
    fk = yield(res[:x][-1], res[:y][-1])
    ut = res[:y][-1] + h * fk
    # Aggiornimao i nuovi valori
    res[:x] << res[:x][-1] + h
    res[:y] << res[:y][-1] + (h/2) * (fk + yield(res[:x][-1], ut))
  end
  return res
end
```

Esempio d'uso:

```ruby
dati = heun(0, 2, 1, 10) { |x, y| -y - 3*x }
puts dati

dati = heun(1, 20, 20, 20) { |x,y| -y*2 - 1/x }
puts dati
```
