---
layout: post
title:  "Soluzione Triangolare"
categories: post
permalink: /solutions/triangolare
visible: 0
---

## Soluzione Triangolare

```ruby
def triangolare(n)
  raise ArgumentError, "input deve essere Fixnum" unless n.is_a? Fixnum

  # Purtroppo a causa del numero 3, che è triagolare, non esiste
  # nessuna condizione che ci facilita la ricerca minore di n
  # Infatti quando n = 3, 3 * (3 - 1) = 2 * 3 -> k = 3
  k = 0

  while k < n
    k += 1
    return true if n == k * (k -1) / 2.0
  end

  return false
end

for i in 3..50
  puts i if triangolare i
end
```
