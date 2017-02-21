---
layout: post
title:  "Soluzione Halley"
categories: post
permalink: /solutions/halley
visible: 0
---

## Soluzione

```ruby
def halley(x0, tol, imax)
  # Per prima cosa controlliamo gli argomenti in ingresso. Ad esempio:
  #  * x0 deve essere un Numeric (in seguito lo forziamo Float)
  #  * la tolleranza non può non essere un Float
  #  * imax è un numero Intero
  #  * alla funzione deve essere fornito un blocco
  raise ArgumentError, "x0 deve essere un numero" unless x0.is_a? Numeric
  raise ArgumentError, "tol deve essere un Float" unless tol.is_a? Float
  raise ArgumentError, "imax deve essere un Fixnum" unless imax.is_a? Fixnum
  raise ArgumentError, "la funzione richiede un blocco" unless block_given?

  # Costruiamo l'hash della soluzione contenente le chiavi richieste.
  # Inizializziamo la soluzione al valore iniziale x0, le iterate a 0
  # e costringiamo la convergenza a false
  h = {
    solution:  x0.to_f,
    iter:      0,
    converged: false
  }

  # fintant che non siamo arrivati al numero massimo di iterazioni
  while h[:iter] < imax
    # incrementiamo le iterazioni
    h[:iter] += 1

    # Richiediamo al blocco i valori richiesti, che sono passati per
    # mezzo di una hash
    blk = yield h[:solution]

    # Valuiamo il valore della funzione nel punto calcolato. Se la
    # funzione ha valore inferiore a tol, allora non continuiamo
    # e usciamo dopo aver impostato :converged a true
    h[:converged] = (blk[:f].abs <= tol)
    break if h[:converged]

    # Calcoliamo il nuovo punto dove valutare la funzione secondo
    # la equazione fornita nel testo dell'esercizio
    h[:solution] = h[:solution] -
       (blk[:f] * blk[:df])/(blk[:df]**2 - 0.5*blk[:f]*blk[:ddf])
  end

  # Ritorniamo la hash
  return h
end
```
Esempio d'uso
```ruby
puts halley_soluzione(10, 1e-4, 20) { |x|
  {f: (3 * x / 2) ** 4 - 1,  df: 81 * (x ** 3) / 4, ddf: 243 * (x**2) / 4}
}
```
