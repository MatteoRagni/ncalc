---
layout: post
title:  "Soluzione Triangolo"
categories: post
permalink: /solutions/triangolo
visible: 0
---

## Soluzione Triangolo

```ruby
def classifica(a,b,c)
  # Controlliamo se i dati sono validi
  [a, b, c].each do |z|
    return -1 unless z.is_a? Numeric
    return -1 if z <= 0
  end  

  # controllo se equilatero
  return 2 if (a == b && b == c)

  # controllo se rettangolo
  return 3 if (a**2 == b**2 + c**2 or
                b**2 == a**2 + c**2 or
                c**2 == a**2 + b**2)

  # controllo se isoscele
  return 1 if (a == b or b == c or a == c)

  # ok è scaleno
  return 0
end
```
