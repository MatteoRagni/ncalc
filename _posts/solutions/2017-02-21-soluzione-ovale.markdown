---
layout: post
title:  "Soluzione Ovale"
categories: post
permalink: /solutions/ovale
visible: 0
---

## Soluzione Ovale

```ruby
def ovale(n, m)
  # Controlliamo che l'input sia un numero intero maggiore di 0
  [n, m].each do |z|
    raise ArgumentError, "Deve essere un Fixnum" unless z.is_a? Fixnum
    raise ArgumentError, "Deve essere positivo" unless z > 0
  end

  # Costruiamo le singole stringhe in un array
  ret = []
  ret << "  " + "* " * n + " "
  for i in 0...m
    ret << "* " + "  " * n + "*"
  end
  ret << ret[0]
  # uniamo l'array con un carattere di nuova linea in fondo "\n"
  return ret.join("\n")
end
```
