---
layout: post
title:  "Soluzione Somma e Prodotto"
categories: post
permalink: /solutions/sumprod
visible: 0
---

## Soluzione Somma e Prodotto

```ruby
def sum_prod(vec)
  # Controlliamo l'input
  raise ArgumentError, "vec deve essere un Array" unless vec.is_a? Array
  vec.each do |z|
    raise ArgumentError, "vec deve contenere Numeric" unless z.is_a? Numeric
  end

  # Due indici: i per scorrere il vettore, z per la chiave hash
  i, z = 0, 0
  # Valore da ritornare
  r = {}

  while i < vec.size
    z += 1 # Incrementiamo l'indice
    r[z] = [
      vec[i] + (vec[i + 1] || 0) + (vec[i + 2] || 0), # Somma
      vec[i] * (vec[i + 1] || 1) * (vec[i + 2] || 1)  # Prodotto
    ]
    i += 3 # incrementiamo il gruppo in vec considerato
  end

  # (vec[i] || 0) ritorna vec[i] se vec[i] != nil. Se è nil ritorna 0.

  return r
end
```
