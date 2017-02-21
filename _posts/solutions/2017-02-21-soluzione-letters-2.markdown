---
layout: post
title:  "Soluzione Lettere (b)"
categories: post
permalink: /solutions/letters/b
visible: 0
---

## Soluzione Lettere (b)

```ruby
def letters(msg)
  # Controlliamo l'input
  raise ArgumentError, "msg deve essere una stringa" unless msg.is_a? String

  # Costruiamo alcuni elementi su cui lavorare come l'hash
  # da ritornare e il messaggio in ingresso con tutte le
  # lettere lower case
  r, m = {}, msg.downcase
  # per ogni lettera dell'alfabeto, range da "a" a "z"
  ("a".."z").each do |c|
    # per ogni lettera del messaggio
    m.each_char do |l|
      # se sono uguali
      if l == c
        # aggiungi la chiave all'hash se non esiste
        r[c] = 0 unless r.keys.include? c
        # inrementa il suo contatore
        r[c] += 1
      end
    end
  end

  # Ritorna l'hashsu cui stiamo lavorando
  return r
end
```
