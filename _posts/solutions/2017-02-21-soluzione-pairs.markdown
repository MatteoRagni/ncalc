---
layout: post
title:  "Soluzione Pairs"
categories: post
permalink: /solutions/pairs
visible: 0
---

## Soluzione Pairs

```ruby
# Scelgo una strategia che non è decisamente la più
# efficiente ma la più facile da implementare.
def pairs(a)
  # Controlliamo l'input per essere un Array
  raise ArgumentError, "Deve essere un Array" unless a.is_a? Array

  # Un Array che contiene tutti gli elementi ripetuti
  repet = []
  # Un Array temporaneo per la raccolata degli elementi
  tmp = [a[0]]
  # Andiamo a raccogliere tutte le serie uguali in repet
  for i in 1...a.size
    if a[i] == tmp[-1]
      tmp << a[i]
    else
      # L'array viene salvato solo se non ha dimensione 1
      repet << tmp.dup unless tmp.size == 1
      # e tmp viene inizializzato di nuovo
      tmp = [a[i]]
    end
  end

  # Ora costruiamo il vettore dei risultati
  ret = {}
  for i in 0...repet.size
    # nuovo elemento dela chiave come Array vuoto se non
    # esiste già
    ret[repet[i].size] = [] unless ret[repet[i].size]
    # Appendiamo un nuovo elemento all'Array di quella
    # chiave, come ultimo elemento per mantenere l'ordine
    ret[repet[i].size] << repet[i][0]
  end

  # Ritorniamo il risultato
  return ret
end
```
