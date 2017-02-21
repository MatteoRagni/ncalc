---
layout: post
title:  "Soluzione Bolletta"
categories: post
permalink: /solutions/bolletta
visible: 0
---

## Soluzione Bolletta

```ruby
def bolletta(filename)
  # Controlliamo l'input: sia che sia una stringa, sia che il file esista
  raise ArgumentError, "filename deve essere String" unless filename.is_a? String
  raise RuntimeError, "filename non esiste" unless File.exist? filename

  # Costruiamo l'elemento in uscita
  ret = {}
  # Apriamo il file ed eseguiamo per ogni linea
  File.open(filename, "r").each_line do |l|
    # Leggiamo una singola linea e la suddividiamo su base ","
    # e convertiamo ogni elemento in numero intero (map, che applica to_i)
    tel, tr, tm = l.chomp.split(",").map(&:to_i)

    # Se non esiste la chiave numero di telefono
    # crea la chiave ocn valore 0
    ret[tel] = 0 unless ret.keys.include? tel
    # Clacola la tariffa
    ret[tel] += tr * tm
  end
  # Ritorna il risultato
  return ret
end

```
