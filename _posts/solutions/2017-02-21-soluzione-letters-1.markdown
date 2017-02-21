---
layout: post
title:  "Soluzione Lettere (a)"
categories: post
permalink: /solutions/letters/a
visible: 0
---

## Soluzione Lettere (a)

```ruby
def letters(msg)
  # Controlliamo che l'input sia una stringa
  raise ArgumentError, "Input deve essere String" unless msg.is_a? String

  # r rappresenta la stringa in uscita. Trasformiamo il messaggio
  # in tutte lettere lowercase ("WoW".downcase -> "wow")
  r = ""
  m = msg.downcase
  # Per ogni lettera andiamo a controllare se la nostra stringa la
  # la contiene, se si la aggiungiamo alla risposta
  ("a".."z").each do |l|
     r << l if m.include? l
  end
  return r
end
```
