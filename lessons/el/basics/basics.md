%{
  version: "1.3.0",
  title: "Βασικά",
  excerpt: """
  Κάνοντας την αρχή, βασικοί τύποι δεδομένων και βασικές λειτουργίες.
  """
}
---

## Κάνοντας την αρχή

### Εγκατάσταση της Elixir

Οδηγίες εγκατάστασης για όλα τα λειτουργικά συστήματα μπορούν να βρεθούν στο elixir-lang.org, στον οδηγό [Installing Elixir](http://elixir-lang.org/install.html).

Αφού εγκαταστήσετε την Elixir, μπορείτε έυκολα να βρείτε την εγκαταστημένη έκδοση.

    % elixir -v
    Erlang/OTP {{ site.erlang.OTP }} [erts-{{ site.erlang.erts }}] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

    Elixir {{ site.elixir.version }}

### Δοκιμάζοντας τον Διαδραστικό Τρόπο

Η Elixir περιέχει το IEx, ένα διαδραστικό κέλυφος, το οποίο μας επιτρέπει να επιβεβαιώνουμε εκφράσεις της Elixir καθώς τις γράφουμε.

Για να ξεκινήσουμε, ας γράψουμε `iex`:

    Erlang/OTP {{ site.erlang.OTP }} [erts-{{ site.erlang.erts }}] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

    Interactive Elixir ({{ site.elixir.version }}) - press Ctrl+C to exit (type h() ENTER for help)
    iex>

Σημείωση: Στο PowerShell των Windows, θα πρέπει να γράψετε `iex.bat`.

Ας προχωρήσουμε τις δοκιμές μας γράφοντας μερικές απλές εκφράσεις:

```elixir
iex> 2+3
5
iex> 2+3 == 5
true
iex> String.length("The quick brown fox jumps over the lazy dog")
43
```

Μην ανησυχείτε αν δεν καταλαβαίνετε όλες τις εκφράσεις ακόμα, ελπίζουμε όμως να πιάνετε το νόημα.

## Βασικοί Τύποι Δεδομένων

### Ακέραιοι

```elixir
iex> 255
255
```

Υπάρχει προεγκατεστημένη υποστήριξη για δυαδικούς, οκταδικούς και δεκαεξαδικούς αριθμούς:

```elixir
iex> 0b0110
6
iex> 0o644
420
iex> 0x1F
31
```

### Κινητής Υποδιαστολής

Στην Elixir, οι αριθμοί κινητής υποδιαστολής απαιτούν ένα δεκαδικό ψηφίο μετά από τουλάχιστον ένα ψηφίο.  Έχουν 64 μπιτ διπλής ακρίβειας και υποστηρίζουν το `e` για τους εκθετικούς αριθμούς:

```elixir
iex> 3.14
 3.14
iex> .14
** (SyntaxError) iex:2: syntax error before: '.'
iex> 1.0e-10
1.0e-10
```

### Δυαδικές Τιμές

Η Elixir υποστηρίζει τις τιμές `true` και `false` σαν δυαδικές.  Οποιαδήποτε τιμή εκτός των `false` και `nil` στέκεται σαν αληθής (truthy)

```elixir
iex> true
true
iex> false
false
```

### Άτομα

Ένα άτομο είναι μια σταθερά της οποίας το όνομα είναι και η τιμή της.
Αν είστε εξοικειωμένοι με την Ruby, τα άτομα είναι συνώνυμα με τα Σύμβολα:

```elixir
iex> :foo
:foo
iex> :foo == :bar
false
```

Οι δυαδικές τιμές `true` και `false` είναι επίσης τα άτομα `:true` και `:false` αντίστοιχα.

```elixir
iex> is_atom(true)
true
iex> is_boolean(:true)
true
iex> :true === true
true
```

Τα ονόματα των ενοτήτων (modules) στην Elixir είναι επίσης άτομα.  Το `MyApp.MyModule` είναι ένα έγκυρο άτομο, ακόμα και αν δεν έχει οριστεί τέτοια ενότητα ακόμα.

```elixir
iex> is_atom(MyApp.MyModule)
true
```

Τα άτομα επίσης χρησιμοποιούνται για να αναφερθούμε σε κάποια ενότητα από τις βιβλιοθήκες της Erlang, συμπεριλαμβανομένων των ενσωματωμένων.

```elixir
iex> :crypto.strong_rand_bytes 3
<<23, 104, 108>>
```

### Αλφαριθμητικά

Τα αλφαριθμητικά στην Elixir είναι κωδικοποιημένα σε UTF-8 και βρίσκονται μέσα σε διπλά εισαγωγικά.

```elixir
iex> "Hello"
"Hello"
iex> "dziękuję"
"dziękuję"
```

Τα αλφαριθμητικά υποστηρίζουν αλλαγές γραμμών και ακολουθίες διαφυγής:

```elixir
iex> "foo
...> bar"
"foo\nbar"
iex> "foo\nbar"
"foo\nbar"
```

Η Elixir επίσης υποστηρίζει πιο πολύπλοκους τύπους δεδομένων.
Θα μάθουμε περισσότερα για αυτούς όταν μάθουμε για τις [Συλλογές](/el/lessons/basics/collections) και τις [Συναρτήσεις](/el/lessons/basics/functions).

## Βασικές Λειτουργίες

### Αριθμητικές

Η Elixir υποστηρίζει τους βασικούς τελεστές `+`, `-`, `*`, και `/`, όπως θα περιμένατε.
Είναι σημαντικό να παρατηρήσουμε ότι ο τελεστής `/` πάντα επιστρέφει αριθμό κινητής υποδιαστολής:

```elixir
iex> 2 + 2
4
iex> 2 - 1
1
iex> 2 * 5
10
iex> 10 / 5
2.0
```

Αν χρειάζεστε ακέραια διαίρεση ή το υπόλοιπο της διαίρεσης, η Elixir περιέχει δύο χρήσιμες συναρτήσεις για να το πετύχει:

```elixir
iex> div(10, 3)
3
iex> rem(10, 3)
1
```

### Δυαδικές

Η Elixir παρέχει τους δυαδικούς τελεστές `||`, `&&` και `!`.
Αυτοί υποστηρίζουν όλους τους τύπους:

```elixir
iex> -20 || true
-20
iex> false || 42
42

iex> 42 && true
true
iex> 42 && nil
nil

iex> !42
false
iex> !false
true
```

Υπάρχουν τρεις πρόσθετοι τελεστές το πρώτο όρισμα των οποίων _πρέπει_ να είναι δυαδικός (`true` και `false`):

```elixir
iex> true and 42
42
iex> false or true
true
iex> not false
true
iex> 42 and true
** (ArgumentError) argument error: 42
iex> not 42
** (ArgumentError) argument error
```

Σημείωση: Οι συναρτήσεις `and` και `or` της Elixir στην πραγματικότητα αντιστοιχούν στις `andalso` και `orelse` της Erlang.

### Σύγκριση

Η Elixir έρχεται με όλους τους τελεστές σύγκρισης που έχουμε συνηθίσει: `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<` και `>`.

```elixir
iex> 1 > 2
false
iex> 1 != 2
true
iex> 2 == 2
true
iex> 2 <= 3
true
```

Για αυστηρή σύγκριση ακέραιων και κινητής υποδιαστολής χρησιμοποιήστε τον τελεστή `===`:

```elixir
iex> 2 == 2.0
true
iex> 2 === 2.0
false
```

Ένα σημαντικό χαρακτηριστικό της Elixir είναι ότι οποιοιδήποτε δύο τύποι μπορούν να συγκριθούν, το οποίο είναι πολύ χρήσιμο στις ταξινομήσεις.  Δεν χρειάζεται να αποστηθίσουμε την σειρά ταξινόμησης, αλλά είναι σημαντικό να την γνωρίζουμε:

```elixir
αριθμός < άτομο < αναφορά < συνάρτηση < θύρα < pid < τούπλα < χάρτης < λίστα < bitstring
```

Αυτό μπορεί να οδηγήσει σε μερικές ενδιαφέρουσες, αλλά ισχύουσες, συγκρίσεις τις οποίες μπορεί να μην βρείτε σε άλλες γλώσσες:

```elixir
iex> :hello > 999
true
iex> {:hello, :world} > [1, 2, 3]
false
```

### Ενσωμάτωση Αλφαριθμητικών

Αν έχετε χρησιμοποιήσει την Ruby, η ενσωμάτωση αλφαριθμητικών στην Elixir θα σας φανεί γνώριμη:

```elixir
iex> name = "Sean"
iex> "Γειά σου #{name}"
"Γειά σου Sean"
```

### Σύνδεση Αλφαριθμητικών

Η σύνδεση αλφαριθμητικών χρησιμοποεί τον τελεστή `<>`:

```elixir
iex> name = "Sean"
iex> "Γεια σου " <> name
"Γεια σου Sean"
```
