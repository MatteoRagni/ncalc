---
layout: post
title:  "Soluzione Otto Regine"
categories: post
permalink: /solutions/regine
visible: 0
---

## Soluzione Otto Regine

```ruby
# Il modo giusto di risolvere questo problema è la costruzione di una
# classe che contenga il problema, farlo in una funzione solo sarebbe
# troppo caotico e difficile da gestire. Usiamo un algoritmo
# di backtracking classico. Il backtracking affrontato in modo ricorsivo
# permette di costruire un problema che sia dinamico sia rispetto
# la deimensione della scacchiera che rispetto al numero di regine da
# mettere sulla scacchiera
class NQueens
  # Ci sono due elementi nella nostra classe, che rendiamo
  # disponibili in lettura. La soluzione (sol) e la dimensione della
  # scacchiera per il nostro problema
  attr_reader :sol, :size

  # Inizializziamo la nostra soluzione sotto forma di scacchiera di
  # dimensione quadrata. Questa è una delle due interfacce che richiede
  # il check dei dati in ingresso (intero positivo)
  def initialize(size = 8, queens = 8)
    raise ArgumentError, "size deve essere Fixnum" unless size.is_a? Integer
    raise ArgumentError, "size deve essere positivo" unless size > 0
    raise ArgumentError, "queens deve essere Fixnum" unless queens.is_a? Integer
    raise ArgumentError, "queens deve essere positivo" unless queens > 0
    # La soluzione è una matrice n x n inizializzata a 0
    @size   = size
    @queens = queens
    @sol    = Array.new(@size) { Array.new(@size) { 0 } }
  end

  # Il resto delle funzioni non hanno alcun input che viene data dall'utente
  # (o almeno non dovrebbero) quindi per le altre siccome sappiamo cosa passiamo
  # non inseriamo nessun controllo sull'input

  # Questa è una funzione interfaccia esterna che permette di ottenere
  # all'esterno la soluzione. (attiva anche il calcolo della soluzione)
  def solve
    # se riesce a piazzare tutte le regine (partendo da zero)
    if self.place(0)
      # allora ritorna la matrice con la soluzione
      return @sol
    else
      # Altrimenti con un errore ci avvisa che non esiste soluzione
      raise RuntimeError, "Non esiste soluzione"
    end
  end

  # La funzione che prova a piazzare una nuova regina, che è
  # chiamata ricorsivamente. Se la regina riesce a piazzarla,
  # chiama ricorsivamente il piazzamento di queen + 1
  def place(queen)
    # Strategia di uscita della funzione ricorsiva
    return true if queen == @queens          # USCITA RICORSIONE

    # Piazzando la soluzione, la posizione della regina
    # nella matrice viene messa ad 1. Se la soluzione non funziona
    # allora si annulla la modifica imponendo la posizione della
    # matrice a 0. Questa strategia è chiamata BACKTRACKING
    for row in 0...@size
      if self.place?(row, queen)
        @sol[row][queen] = 1
        return true if self.place(queen + 1) # RICORSIONE
        @sol[row][queen] = 0                  # BACKTRACKING
      end
    end
    return false
  end

  # Questa funzione controlla se è effettivamente possibile piazzare
  # la regina in una data posizione row, col, controllando che nel raggio
  # di azione, la regina piazzata in quella posizione row, col non sia
  # in grado di mangiare un'altra delle regine già piazzate. Esempio 4 x 4
  # REGINE PIAZZATE     Regina in 2, 3
  # | 0 R 0 0 |         | 0 x 0 x |
  # | 0 0 0 R |         | 0 0 x x |
  # | 0 0 0 ? |         | x x x x |
  # | 0 0 0 0 |         | 0 0 x x |
  # In questo esempio non posso piazzare la nuova regina in 2, 3 perchè
  # entrambe le prime due regine verrebbero mangiate
  def place?(row, col)
    # Siccome inseriamo le regine una riga alla volta,
    # ci basta controllare solo rispetto alla colonna
    for i in 0...@size
      return false if @sol[row][i] == 1
    end

    # Usiamo y = x + q1 e y = x - q2 per
    # valutare gli elementi diagonali
    q1 = row - col
    q2 = row + col
    for i in 0...@size
      if (0...@size).include?(i + q1)
        return false if @sol[i + q1][i] == 1
      end
      if (0...@size).include?(i - q2)
        return false if @sol[i - q2][i] == 1
      end
    end

    # Se una qualsiasi delle caselle controllate prima
    # contiene una regina, allora ritorniamo false, altrimenti
    # ritorniamo true
    return true
  end
end


# A questo punto risolviamo il vero e proprio problema
# rispondendo con una funzione che usa la notra classe
def otto_regine
   regine = 30 # <- cambia qui per cambiare la dimensione
              #    del problema (es. 12?)

  # In una riga, risolviamo il problema
  r = NQueens.new(regine, regine).solve

  # Stampiamo a schermo la soluzione tanto per vederla
  puts r.map { |e|
    e.map { |z|
      z == 1 ? "Q" : "."
    }.join(" ")
  }.join("\n")

  # Creiamo l'Array che conterrà la soluzione così come richiesto
  # nel testo dell'esercizio
  s = Array.new(regine) { 0 }
  for i in 0...regine
    for j in 0...regine
      s[i] = j if r[i][j] == 1
    end
  end

  return s
end

```
