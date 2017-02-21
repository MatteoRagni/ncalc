---
layout: post
title:  "Soluzione "
categories: post
permalink: /solutions/oddeven
visible: 0
---

## Soluzione

```ruby
def odd_even(vec)
  # Controlliamo l'input, deve essere un Array
  raise ArgumentError, "vec deve essere un Array" unless vec.is_a? Array

  # Ecco l'elemento che restituiremo in output
  res = []

  # Iteriamo con uno step due su tutti gli elementi dispari
  # (1...vec.size).step(2) => i = 1, 3, 5, ...
  (1...vec.size).step(2) { |i| res << vec[i] }
  (0...vec.size).step(2) { |i| res << vec[i] }
  return res
end
```
