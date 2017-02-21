---
layout: post
title:  "Soluzione Star"
categories: post
permalink: /solutions/star
visible: 0
---

## Soluzione Star

```ruby
def star(x0, x1, tol, imax)
  # Controlliamo l'input
  [x0, x1, tol].each do |z|
    raise ArgumentError, "Deve essere Numeric" unless z.is_a? Numeric
  end
  raise ArgumentError, "Deve essere integer" unless imax.is_a? Integer
  #raise ArgumentError, "Intevallo negativo" if x0 > x1
  raise ArgumentError, "Blocco richiesto" unless block_given?

  r = { solution: nil, iter: 0, converged: false }

  # Inizializziamo con il metdo delle secanti il problema,
  # ci portiamo dietro l'Array in modo tale da ridurre il meno
  # possibile il numero di valutazioni del blocco
  f = [yield(x0.to_f), yield(x1.to_f), nil]
  x = [x0.to_f, x1.to_f,
       x1.to_f - f[1] * (x1.to_f - x0.to_f)/(f[1] - f[0])]
  f[2] = yield(x[2])

  # Impostiamo un ciclo while che ha due condizioni di uscita:
  #  - iterazioni massime
  #  - convergenza per tolleranza
  while r[:iter] < imax
    r[:iter] += 1

    # Esecuzione dell'algoritmo star
    d10 = (f[1] - f[0])/(x[1] - x[0])
    d21 = (f[2] - f[1])/(x[2] - x[1])
    d20 = (f[2] - f[0])/(x[2] - x[0])

    x_t = x[2] - f[2]/(d21 + d20 - d10)

    # Riaggiorniamo la posizione nell'Array
    # Da notare che nell'algoritmo iterativo
    # valutiamo la funzione 1 VOLTA, senza
    # valutarla 3 volte con una implementazione
    # poco ragionata
    x = [x[1], x[2], x_t]
    f = [f[1], f[2], yield(x_t)]

    # Se siamo sotto la tolleranza, ritorniamo
    # la convergenza e il valore della soluzione
    # che è x[2]
    if f[2] < tol
      r[:converged] = true
      r[:solution] = x[2]
      break
    end
  end

  return r
end
```

Esempio d'uso:

```
z = star(9, 10, 1e-12, 20) { |x| (3 * x / 2)**4 - 1 }

puts z
```
