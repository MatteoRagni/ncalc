---
layout: post
title:  "Soluzione Ordered (a)"
categories: post
permalink: /solutions/ordered/a
visible: 0
---

## Soluzione Ordered (a)

```ruby
def ordered(a)
  # Per prima cosa controlliamo che in ingresso abbiamo un Array di tutti
  # numeri (il secondo controllo si potrebbe effettuare dentro il loop
  # dell'algoritmo per maggiore efficienza, lo mettiamo fuori per
  # maggiore chiarezza)
  raise ArgumentError, "Ci vuole un Array in ingresso" unless a.is_a? Array
  a.each do |z|
    raise ArgumentError,
      "Tutti gli elementi dell'Array devono essere Numeric" unless z.is_a? Numeric
  end

  # Adesso ci occupiamo del vero e proprio algoritmo, costruendo
  # prima un Array vuoto r che porterà fuori la soluzione e un Array
  # temporaneo b con il primo elemento di a (a[0])
  r, b = [], [a[0]]

  # Si esegue un ciclo (ne basta uno) da 1 a (a.size - 1)
  for i in 1...(a.size)
    # controlliamo se l'elemento che stiamo analizzando è
    # strettamente decrescente rispetto all'ultimo elemento
    # del vettore b. Se lo è lo aggiungiamo alla fine di b.
    if b[-1] > a[i]
      b << a[i]

    # Altrimenti, inseriamo b dentro l'insieme dei risultati r
    # e inizializziamo il nuovo b con il valore corrente di
    # a, ovvero a[i].
    else
      r << b
      b = [a[i]]
    end
  end
  # Ritorniamo r, ma prima dobbiamo aggiungere l'ultimo stato di
  # b, che non può mai incontrare la situazione di aggiunta
  return r << b

  # Questa è una delle tante possibili soluzioni per questo problema,
  # si potrebbero usare cicli nidificati.
end
```
