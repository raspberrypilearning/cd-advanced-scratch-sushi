## Χάνοντας το παιχνίδι

Καταρχάς! Χρειάζεσαι έναν τρόπο για να τερματίσεις το παιχνίδι όταν ο παίκτης χάσει όλες τις ζωές. Αυτή τη στιγμή αυτό δεν συμβαίνει.

Μπορεί να έχεις παρατηρήσει ότι το μπλοκ `χάνει`{:class="block3myblocks"} από τις **Εντολές μου** στο σενάριο του αντικειμένου **Παίκτης** είναι άδειο. Θα το συμπληρώσεις και θα δημιουργήσεις όλα τα κομμάτια που χρειάζεται για εμφανίζεται μια ωραία οθόνη «Τέλος Παιχνιδιού».

--- task ---

Αρχικά, βρες το μπλοκ `χάνει`{:class="block3myblocks"} και συμπλήρωσε τον ακόλουθο κώδικα:

```blocks3
    define χάνει
+    stop [other scripts in sprite v] :: control stack
+    broadcast [Τέλος Παιχνιδιού v]
+    go to x:(0) y:(0)
+    say [Τέλος Παιχνιδιού!] for (2) secs
+    stop [all v]
```

--- /task ---

--- collapse ---
---
title: Τι κάνουν αυτές οι εντολές;
---

Όποτε εκτελείται το μπλοκ `χάνει`{:class="block3myblocks"}, αυτό που κάνει είναι:

1. Σταματάει τη φυσική και άλλα σενάρια παιχνιδιού που ενεργούν στο αντικείμενο **Παίκτης**
2. Λέει σε όλα τα άλλα αντικείμενα ότι το παιχνίδι τελείωσε **μεταδίδοντας** ένα μήνυμα `τέλος παιχνιδιού`{:class="block3events"}, στο οποίο μπορούν να αντιδράσουν και να αλλάξουν αυτό που κάνουν
3. Μετακινεί το **Παίκτη** στο κέντρο της σκηνής και να του λέει ότι το παιχνίδι τελείωσε
4. Σταματάει όλα τα σενάρια στο παιχνίδι

--- /collapse ---

Τώρα πρέπει να βεβαιωθείς ότι όλα τα αντικείμενα ξέρουν τι να κάνουν όταν τελειώσει το παιχνίδι και πώς να επαναφέρουν τον εαυτό τους όταν ο παίκτης ξεκινά ένα νέο παιχνίδι. **Μην ξεχνάς ότι τυχόν νέα αντικείμενα που προσθέτεις ενδέχεται να χρειάζονται επιπλέον κώδικα για αυτό!**

### Απόκρυψη των πλατφορμών και των ορίων

--- task ---

Ξεκίνησε με τα ευκολότερα αντικείμενα. Τα αντικείμενα **Πλατφόρμες** και **Όρια** χρειάζονται κώδικα για να εμφανίζονται όταν ξεκινά το παιχνίδι και να εξαφανίζονται όταν λαμβάνουν το μήνυμα `Τέλος Παιχνιδιού`{:class="block3events"}, οπότε πρόσθεσε αυτά τα μπλοκ σε καθένα από αυτά:

```blocks3
+    when I receive [Τέλος Παιχνιδιού  v]
+    hide
```

```blocks3
+    when green flag clicked
+    show
```

--- /task ---

### Σταματώντας τα αστέρια

Τώρα, αν κοιτάξεις τον κώδικα για το αντικείμενο **Βραβείο**, θα δεις ότι λειτουργεί με δημιουργία **κλώνων** του εαυτού του. Δηλαδή δημιουργεί αντίγραφα που εκτελούν τις εντολές του μπλοκ `όταν ξεκινήσω ως κλώνος`{:class="block3events"}.

Θα μιλήσουμε περισσότερο για το τι κάνει τους κλώνους ξεχωριστούς όταν φτάσουμε στο βήμα για τη δημιουργία νέων και διαφορετικών βραβείων. Προς το παρόν, αυτό που πρέπει να γνωρίζεις είναι ότι οι κλώνοι μπορούν να κάνουν **σχεδόν** όλα όσα μπορεί να κάνει ένα κανονικό αντικείμενο, συμπεριλαμβανομένης και της `λήψης μηνυμάτων`{:class="block3events"}.

Δες πώς δουλεύει το αντικείμενο **Βραβείο**. Δες αν μπορείς να καταλάβεις μέρος του κώδικά του:

```blocks3
    when green flag clicked
    hide
    set [αξία-βραβείου v] to [1]
    set [ταχύτητα-βραβείου v] to [1]
    set [συχνότητα-βραβείου v] to [1]
    set [δημιουργία-βραβείων v] to [true]
    set [τύπος-βραβείου v] to [1]
    repeat until <not <(δημιουργία-βραβείων) = [true]>>
        wait (συχνότητα-βραβείου) secs
        go to x: (pick random (-240) to (240)) y: (179)
        create clone of [myself v]
    end
```

1. Πρώτα κάνει το αρχικό αντικείμενο **Βραβείο** αόρατο, εξαφανίζοντάς το
2. Στη συνέχεια, ρυθμίζει τις μεταβλητές ελέγχου - θα επανέλθουμε σε αυτές αργότερα
3. Η μεταβλητή `δημιουργία-βραβείων`{:class="block3variables"} αποτελεί ένα διακόπτης on / off για κλωνοποίηση: ο βρόχος δημιουργεί κλώνους εάν η `δημιουργία-βραβείων`{:class="block3variables"} είναι `αληθής (true)`, και δεν κάνει τίποτα αν είναι ψευδής (false)

--- task ---

Τώρα δημιούργησε ένα μπλοκ για το αντικείμενο **Βραβείο**, έτσι ώστε να ανταποκρίνεται στη μήνυμα `Τέλος Παιχνιδιού`:

```blocks3
+    when I receive [Τέλος Παιχνιδιού v]
+    hide
+    set [δημιουργία-βραβείων v] to [false]
```

--- /task ---

Αυτός ο κώδικάς είναι παρόμοιος με τον κώδικα που ελέγχει τα αντικείμενα **Πλατφόρμες** και **Όρια**. Η μόνη διαφορά είναι ότι ρυθμίζεις και τη μεταβλητή `δημιουργία-βραβείων`{:class="block3variables"} σε `ψευδές (false)`, έτσι ώστε να μην δημιουργούνται νέοι κλώνοι όταν τελειώσει το παιχνίδι.

Έχε στο νου ότι μπορείς να χρησιμοποιήσεις τη μεταβλητή `δημιουργία-βραβείων`{:class="block3variables"} για τη μετάδοση μηνυμάτων από ένα μέρος του κώδικα σε ένα άλλο!