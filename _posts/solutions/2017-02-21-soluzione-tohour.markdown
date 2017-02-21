---
layout: post
title:  "Soluzione To Hour"
categories: post
permalink: /solutions/tohour
visible: 0
---

## Soluzione To Hour

```ruby
# Esistono due modi per risolvere questo esercizio. Il primo
# utilizzando la libreria standard mediante "datetime" e il secondo
# scrivendo direttamente la funzione che si occupa delle conversioni.

#                 1   2   3   4   5   6   7   8   9  10  11  12
Month_days = [0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

# Dato giorno e mese calcola tutte le ore fino al giorno precedente
# specificato
def date_to_hours(d, m)
  # Non contiamo il giorno corrente, che ne calcoliamo le ore
  days = d - 1
  # Sommatoria di giorni per tutti i mesi precedenti
  for i in 0...m
    days += Month_days[i]
  end
  # Ritorna i giorni moltiplicati per 24
  return days * 24  
end

def to_hour(h,d,m)
  # Per prima cosa controlliamo che siano dati plausibili (ovvero Fixnum)
  [h, d, m].each do |l|
    raise ArgumentError, "Devono essere Fixnum" unless l.is_a? Fixnum  
  end
  # Poi controlliamo il range in cui si trova l'orario (0..23)
  raise ArgumentError, "h in [0..23]" unless (0..23).include? h
  # Controlliamo il range del mese (lo controlliamo prima per
  # usarlo per il numero di giorni in un mese)
  raise ArgumentError, "m in [1..12]" unless (1..12).include? m
  # Controlliamo il numero di giorni in un mese
  raise ArgumentError, "d fuori dal range" unless (1..Month_days[m]).include? d

  # Ritorna tutte le ore
  return date_to_hours(d, m) + h
end
```
