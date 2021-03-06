<img src="media/AUEB_logo.jpg" width="425" /> <img src="media/BA_Lab.png" width="425" />
# Προγραμματισμός ΙΙ
## Κληρονομικότητα, Αφηρημένες κλάσεις, Διεπαφές

* [Στέφανος Γεωργίου](https://www.balab.aueb.gr/stefanos-georgiou.html)
* [Κωνσταντίνος Κραββαρίτης](https://www.balab.aueb.gr/konstantinos-kravvaritis.html)


## Κληρονομικότητα

* Κληρονομικότητα στον αντικειμενοστραφή προγραμματισμό είναι η δυνατότητα να
παραχθούν ειδικότερες κλάσεις από γενικότερες.
* Οι ειδικότερες κλάσεις ονομάζονται και υποκλάσεις των γενικότερων και
αντίστροφα οι γενικότερες κλάσεις ονομάζονται υπερκλάσεις των ειδικότερων.
* Ένα αντικείμενο μιας υποκλάσης είναι και αντικείμενο της (κάθε) υπερκλάσης.
* Στη java κάθε κλάση μπορεί να κληρομήσει άμεσα μόνο μία υπερκλάση
χρησιμοποιώντας τη δεσμευμένη λέξη extends.

```java
class SubClass extends SuperClass {...}
```
* Όλες οι κλάσεις στη java κληρονομούν την κλάση Object ακόμα και όταν αυτό δε
γίνεται ρητά μέσω της εντολής extends.

## Παράδειγμα

```java
class Triangle {

    public String whoIAm() { return "I am a triangle"; }
}

class EquilateralTriangle extends Triangle {

    public String whoIReallyAm() { return "I am equilateral"; }
}
```

```java
public class Test {
    EquilateralTriangle equilateral = new EquilateralTriangle();
    System.out.println(equilateral.whoIAm())
    System.out.println(equilateral.whoIReallyAm());
}
```


## Override

* Μια κλάση μπορεί να αλλάξει τη συμπεριφορά μιας μεθόδου που αλλιώς θα
κληρονομούσε απο υπερκλάση της, ορίζοντάς την με το ίδιο όνομα, τα ίδια ορίσματα,
τον ίδιο τύπο και το σώμα που επιθυμεί ο χρήστης. (Αρκεί να μην έχει χαρακτηριστεί
ως final).
* Όταν μια μέθοδος γίνεται Override ο χρήστης μπορεί να προσθέσει πάνω από τον
ορισμό της μεθόδου το annotation '@Override'. Αυτό γίνεται για να:
    * κανει ξεκάθαρο στους χρήστες ότι η μέθοδος γίνεται override.
    * ο μεταγλωτιστής θα αναγνωρίσει κάποιο σφάλμα οπώς για παράδειγμα να μην
    υπάρχει αυτή η μέθοδος στην υπερκλάση.


## Παράδειγμα

```java
class Triangle {

    public String whoIAm() { return "I am a triangle"; }
}

class EquilateralTriangle extends Triangle {

    @Overrride
    public String whοΙAm() { return "I am an equilateral triangle"; }
}
```


## super

* Σε μια κλάση η δεσμευμένη λέξη **super** είναι αντίστοιχη της δεσμευμένης λέξης
**this** με τη διαφορά ότι το αντικείμενο αναφέρεται στον εαυτό του ως αντικείμενο
της άμεσης υπερκλάσης.
* Το **super** χρησιμοποιείται για να κληθεί κάποια μέθοδος της υπερκλάσης που έχει
γίνει **override** από την υποκλάση, ή κάποιο πεδίο που δεν είναι private.
* Το **super(ορίσμα)** χρησιμοποιείται για να καλέσει τον κατασκευαστή της άμεσης
υπερκλάσης.
* Σε κάθε κατασκευαστή πρέπει να καλείται ο κατασκευαστής της άμεσης υπερκλάσης
στην πρώτη γραμμή του σώματός του. Αν δεν γραφτεί κάτι ρητά τοτε και πάλι καλείται
ο κατασκευαστής της υπερκλάσης στη πρώτη γραμμή χωρίς κάποιο όρισμα.


## Παράδειγμα

```java
class Triangle {

    public String whoIAm() { return "I am a triangle"; }
}

class EquilateralTriangle extends Triangle {

    @Override
    public String whοΙAm() {
        return super.whoIAm() + " and an equilateral one too";
    }
}
```


## Παράδειγμα(2)

```java
class Triangle {

    private int base;
    private int height;

    public Triangle(int base, int height) {
        // super();   <-- Εννοείται
        this.base = base;
        this.height = height;
    }
}

class EquilateralTriangle extends Triangle {

    public EquilateralTriangle(int base, int height) {
        super(base, height);  // Εδω η κλήση της super είναι απαραίτητη
    }
}
```


## Αφηρημένες κλάσεις

* Όταν μια συλλογή από κλάσεις έχουν κάποια κοινά πεδία ή/και κάποια κοινή
συμπεριφορά τότε αυτά τα κοινά στοιχεία μπορούν να περιληφθούν σε μια υπερκλάση.
Αν αυτή η υπερκλάση είναι υπερβολικά γενική ή τα αντικείμενά της από το
προγραμμά δεν είναι χρήσιμα, τότε είναι καλή πράκτική να την κάνουμε αφηρημένη.
* Μια αφηρημένη κλάση έχει τη δεσμευμένη λέξη **abstract** στον ορισμό της.
* Παρ' όλο που δεν μπορεί να αρχικοποιηθεί, διαθέτει κατασκευαστή.
* Στις αφηρημένες κλάσεις μπορούν να ορισθούν αφηρημένες μέθοδοι.
* Οι αφηρημένες κλάσεις έχουν όμοιες συμβάσεις για τη γραφή του ονόματός τους με
τις συνήθεις κλάσεις.


## Αφηρημένες μέθοδοι

* Σε αφηρημένες κλάσεις δίνεται η δυνατότητα να οριστούν αφηρημένες μέθοδοι.
* Μια αφηρημένη μέθοδος είναι μια μέθοδος που τη δεσμευμένη λέξη 'abstract' στον
όρισμό της.
* Είναι χρήσιμες στο να επιβάλει μια αφηρημένη κλάση μια γενική συμπεριφορά στις
υποκλάσεις της.
* Αν σε μια αφηρημένη κλάση ορισθεί μια αφηρημένη μέθοδος, τότε κάθε υποκλάση της
είναι υποχρεωμένη να την υλοποιήσει.


## Παράδειγμα

```java
abstract class Shape {

    private int numberOfVertices;

    public Shape(int numberOfVertices) {
        this.numberOfVertices = numberOfVertices;
    }

    public int getNumberOfVertices() {
        return this.numberOfVertices;
    }

    public abstract double area();
}
```


## Παράδειγμα(συνέχεια)

```java
class triangle extends Shape {

    private int base;
    private int height;

    public Triangle(int base, int height) {
        super(3)
        this.base = base;
        this.height = height;
    }

    @Override
    public double area() {
        return (base * height) / 2.0;
    }
}
```


## Παράδειγμα(συνέχεια)

```java
class square extends Shape {

    private int edge;

    public Square(int edge) {
        super(4);
        this.edge = edge;
    }

    @Override
    public double area() {
        return edge * edge;
    }
}
```


## Διεπαφές

* Ομοιότητες με αφηρημένες κλάσεις
    * Καθορίζουν μέρος της συμπεριφοράς των κλάσεων που τις υλοποιούν.
    * Μπορούν να ορισθούν αφηρημένες μεθόδοι χωρίς όμως την ανάγκη της
    δεσμευμένης λέξης 'abstract'. Αντίθετα μέθοδοι με σώμα μπορούν να ορισθούν
    (από το jdk1.8 και μετά) με τη δεσμευμένη λέξη 'default' στον ορισμό.
    * Κάθε αντικείμενο που υλοποιεί μια διεπαφή αποκτά και τον τύπο που ορίζει
    το όνομά της.


## Διεπαφές(2)

* Διαφορές με αφηρημένες κλάσεις:
    * Οι διεπαφές υλοποιούνται με τη δεσμευμένη λέξη 'implements'.
    * Μια κλάση μπορεί να υλοποιήσει παραπάνω από μια διεπαφή.
    * Μια διεπαφή μπορεί να έχει μονο final static πεδιά (σταθερές). Συνεπώς μια
    διεπαφή δεν επηρεάζει τη κατάσταση του αντικειμένου που την υλοποιεί αλλά
    μόνο τη συμπεριφορά.
    * Δεν έχουν κατασκευαστές.
    * Στα ονόματα των διεπαφών η σύμβαση είναι να χρησιμοποιείται συνήθως επίθετο
    αντί για ουσιαστικό σε μορφή CamelCase.


## Παράδειγμα

```java
abstract class Shape {

    private int numberOfVertices;

    public Shape(int numberOfVertices) {
        this.numberOfVertices = numberOfVertices;
    }

    public int getNumberOfVertices() {
        return numberOfVertices;
    }
}
```


## Παράδειγμα(συνέχεια)

```java
interface CalculableArea() {

    double area();
}
```


## Παράδειγμα(συνέχεια)

```java
public class Triangle extends Shape implements CalculableArea {

    private int base;
    private int height;

    public Triangle(int base, int height) {
        super(3);
        this.base = base;
        this.height = height;
    }

    @Override
    public double area() {
        return (base * height) / 2.0;
    }
}
```  
