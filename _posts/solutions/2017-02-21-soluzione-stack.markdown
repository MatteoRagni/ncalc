---
layout: post
title:  "Soluzione Stack"
categories: post
permalink: /solutions/stack
visible: 0
---

## Soluzione

```ruby
# La soluzione di questo esercizio è talmente semplice che non
# ci perdiamo in spiegazioni
class Stack
  def initialize; @r = []; end  
  def push(i); @r << i; end
  def pop; @r.pop; end
  def size; @r.size; end
  def top; @r[-1]; end
end
```
