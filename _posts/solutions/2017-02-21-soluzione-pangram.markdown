---
layout: post
title:  "Soluzione Pangram"
categories: post
permalink: /solutions/pangram
visible: 0
---

## Soluzione Pangram

```ruby
# Compio una scelta di progetto. Il mio algoritmo controlla per pangrammi
# di natura inglese (con tutte le 26 lettere dell'alfabeto), potrebbe
# non essere la soluzione corretta dell'esame, ma è facile farlo tornare
def pangram(msg)
  # Come sempre dobbiamo controllare l'ingresso
  raise ArgumentError, "Deve essere una stringa" unless msg.is_a? String

  # Costruiamo l'hash di lettere
  letters = {}; ("a".."z").each { |l| letters[l] = nil }

  for i in 0...msg.size
    letters.delete msg[i].downcase # delete non ritorna errore se la chiave non esiste
  end

  # Ritorna true se abbiamo usato tutte le lettere (nessuna chiave rimasta)
  return letters == {}
end
```
