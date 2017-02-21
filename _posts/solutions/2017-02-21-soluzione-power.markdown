---
layout: post
title:  "Soluzione Power"
categories: post
permalink: /solutions/power
visible: 0
---

## Soluzione

```ruby
# Proviamo a costruire la funzione in forma ricorsiva
# Se n = 0
#   allora ritorniamo [ [] ], che è il set di base
#   (questa è la strategia di uscita dalla ricorsione)
# Se invece n > 0 allora,
#   calcola l'insieme power(n - 1) (ricorsione)
#   prendi quella parte calcolata, e crea un nuovo
#   insieme identico al quale aggiungo solo il numero corrente n
#   unisco il vettore precedente al nuovo con n
def power(n)
  # Eseguo un controllo dell'input
  raise ArgumentError, "n deve essere un Fixnum" unless n.is_a? Fixnum

  # Implemento la strategia di uscita
  return [[]] if n == 0

  # Calcolo il risultato per tutte le condizioni
  # precedenti
  a = power(n - 1)
  # Uso la soluzione precedente per costruirne la
  # parziale nuova aggiungendo [n]
  # Array#map permette di costruire un nuovo array b
  # usando gli elementi e di a, modificati secondo
  # quanto specificato in un blocco
  b = a.map do |e|
    e + [n]
  end

  # Quello che ritorno come soluzione completa
  # è l'insieme delle precedenti con le successive
  return a + b
end
```
