---
layout: post
title:  "Soluzione Differenze Divise"
categories: post
permalink: /solutions/diffdiv
visible: 0
---

## Soluzione Differenze Divise

```ruby
# Mettendo questa variabile a true, la funzione stampa a schermo i
# singoli passaggi
$mostra_passaggi = false

def diffdiv(x, y)
  # Come al solito, la prima cosa da fare è controllare che i
  # nostri input siano del tipo atteso. Mettiamoli in un Array
  # per fare prima.
  # In questo caso non è stato richiesto a livello di testo
  # del problema, ma è buona norma farlo comunque.
  [x, y].each do |z|
    raise ArgumentError, "Richiesti 2 Array in ingresso" unless z.is_a? Array
    raise ArgumentError, "Richiesti Array non vuoti" unless z.size != 0
    z.each do |i|
      raise ArgumentError, "Gli Array devono contenere numeri" unless i.is_a? Numeric
    end
  end

  # Per prima cosa, ci occupiamo del caso in
  # cui la dimensione dei due vettori non sia uguale
  return nil if x.size != y.size

  # Inizializziamo un nuovo vettore vuoto della
  # stessa dimensione di y (copiandolo). Non dobbiamo tenerci
  # tutte le differenze divise, visto che ci richiede
  # solamente la soluzione di ordine n = y.size
  # Per essere sicuri di ottenere divisioni tra float, usiamo
  # la funzione map (cfr: suggerimento nella descrizione)
  a = y.map(&:to_f)
  # Ci facciamo anche un secondo vettore di supporto, per
  # poter salvare i valori temporanei del nostro calcolo
  b = a.dup

  # Lavoriamo come se fossimo in una tabella mobile, nella
  # quale consideriamo solo la prima colonna di x, la colonna
  # di valori correnti a e la colonna di prossimi valori b.
  # A ogni ciclo perdiamo un elemento della colonna
  # Al ciclo i-esimo per esempio, j itera tra i e (n-1)

  # ciclo  0   1   2   ... i
  # x      ... ... ... ... a   b
  # --------------------------------------------------------
  # x0       
  # x1     ...         
  # x2     ... ...      
  # x3     ... ... ...
  # x4     ... ... ... ...
  # x5     ... ... ... ... a5
  # x[j]   ... ... ... ... a6  b6 = (a5 - a6)/(x[j-i] - x[j])
  for i in 1...a.size
    for j in i...a.size
      b[j] = (a[j-1] - a[j])/(x[j-i] - x[j])
      if $mostra_passaggi
        print "#(a[#{j-1}] - a[#{j}])/(x[#{j-i}] - x[#{j}]) : "
        puts "#{b[j]} = (#{a[j-1]} - #{a[j]})/(#{x[j-i]} - #{x[j]})"
      end
    end
    puts if $mostra_passaggi
    a = b.dup # Attenzione a questo dup. Se non ci fosse,
              # modificando b, si modificherebbe anche a
              # quindi è meglio farne una copia duplicata
  end

  # Ci interessa solo l'ultimo valore quindi ritorniamo
  # solo quello
  return a[-1]
end
```
