ESP Antenna Rotor
=================

Σ' αυτό το αποθετήριο υπάρχουν οι οδηγίες κατασκευής (σχέδια και λογισμικό) για τον ESP Rotor. Πρόκειται για μια ελαφριά κατασκευή του συστήματος περιστροφής κατευθυνόμενων κεραιών συνήθως τύπου yagi που χρησιμοποιούν οι ραδιοερασιτέχνες. Για μηχανισμό χρησιμοποίησα τον κινητήρα από μια παλιά σούβλα ψησίματος αρνιού. Ο μηχανισμός αυτός είναι σχετικά απλός, έχει αρκετό χώρο ώστε να κάνουμε παρεμβάσεις, είναι φτηνός και ανθεκτικός και τέλος παρέχει ικανοποιητική ροπή για κεραίες μεσαίου μεγέθους όπως αυτές των VHF.

Ηλεκτρονική κατασκευή
=====================

<p>Για μικροελεγκτή έβαλα το διάσημο και φτηνό ESP8266 που είναι επεξεργαστής 32bit με WiFi. Έτσι χρησιμοποίησα το module ESP12 το οποίο έχει 2 ή 4Mb μνήμη Flash η οποία είναι υπέρ αρκετή για την συγκεκριμένη κατασκευή. Εναλλακτικά μπορεί να χρησιμοποιηθεί το νεότερο ESP32 που είναι πολύ πιο ισχυρό από το ESP8266.</p>

<p>Επειδή το άρθρο έχει και εκπαιδευτικό σκοπό, αποφάσισα να τα κατασκευάσω όλα από το μηδέν. Έτσι αντί να χρησιμοποιήσω μια έτοιμη πλακέτα όπως το Node MCU κατσκεύασα την πλακέτα πάνω σε διάτρητη Perfboard.</p>

<table align="center">
 <tr>
  <td><img src="/hardware/electronics/schematics+images/cpu1.jpg" height="200"></td>
  </tr>
 <tr><td align="center"><sub>Τα υλικά για την κατασκευή της MCU</sub></td></tr>
 </table>

Ακολουθεί το σχέδιο διασύνδεσης του module ESP-12E
<table align="center">
 <tr>
  <td><img src="/hardware/electronics/schematics+images/mcu1.jpg" height="300"></td>
  <td><img src="/hardware/electronics/schematics+images/mcu2.jpg" height="300"></td>
  </tr>
 </table>
 
Επειδή το ESP8266 λειτουργεί στα 3,3V αλλά η υπόλοιπη κατασκευή (βασικά ο κινητήρας) απαιτεί 5V, θα φτιάξουμε ένα τροφοδοτικό από 5V σε 3,3V. Ο καταλληλότερος σταθεροποιητής γι' αυτή την χρήση είναι το LDV33, αλλά επειδή δεν είχα έβαλα το παλιό και κοινό LM317. Από το σπίτι κάτω, στέλνουμε τροφοδοσία 12V πάνω στην κεραία. Ανάλογα με το μήκος και την διατομή του καλωδίου θα έχουμε μια πτώση τάσης 2-4V. Μέσα στο κουτί του ρότορα θα βάλουμε ένα DC to DC converter ο οποίος θα δέχεται 8-10V και θα βγάζει 5V για να τροφοδοτήσει την συσκευή μας.
<table align="center">
 <tr>
  <td><img src="/hardware/electronics/schematics+images/psu1.jpg" height="300"></td>
  <td><img src="/hardware/electronics/schematics+images/psu2.jpg" height="300"></td>
  </tr>
 </table>
 
Στη συνέχεια κατασκευάζουμε το κύκλωμα του reset καθώς και αυτό για τον προγραμματισμό του μικροελεγκτή. Για τον προγραμματισμό και την εκσφαλμάτωση (Debuging) βάζουμε έναν μετατροπέα από USB σε σειριακή με το FT232. Από τον υπολογιστή μας με το Arduino IDE ή με το VS Code και το Platform IO στέλνουμε το firmware στον μικροελεγκτή και εποπτεύουμε από το τερματικό την λειτουργία εμφανίζοντας μηνύματα και τιμές μεταβλητών. Στο pin 10 έβαλα ένα βραχυκυκλωτήρα και μέσα στο πρόγραμμα έγραψα λίγο κώδικα, έτσι ώστε αν ενωθεί για πάνω από 5 δευτερόλεπτα να φορτώσει τις αρχικές ρυθμίσεις. Αυτό είναι χρήσιμο αν για παράδειγμα έχουμε βάλει κάποιο WiFi SSID ή κάποια διεύθυνση IP που έχει παύσει να ισχύει είτε γιατί αλλάξαμε router είτε γιατί βάλαμε τον ρότορα σε άλλο δίκτυο και δεν υπάρχει επικοινωνία. Μετά την επαναφορά το WiFi λειτουργεί σαν Access Point με SSID SV6GMP-ROTOR χωρίς κρυπτογράφηση. Αφού συνδεθούμε με το κινητό μας, πάμε στην διεύθυνση 192.168.4.1 και ανοίγει η σελίδα των ρυθμίσεων. Από εκεί μπορούμε να βάλουμε νέες ρυθμίσεις.
<table align="center">
 <tr>
  <td><img src="/hardware/electronics/schematics+images/reset_prog1.jpg" height="300"></td>
  <td><img src="/hardware/electronics/schematics+images/reset_prog2.jpg" height="300"></td>
  </tr>
 </table>
<p>Τα σύρματα στην πίσω πλευρά της πλακέτας είναι μονωμένο σύρμα πηνίου. Για να κολλήσουμε την άκρη πρέπει να ξύσουμε το βερνίκι με κάποιο αιχμηρό αντικείμενο.</p>

<b>Δοκιμή επικοινωνίας και προγραμματισμού</b>
<p>Στο σημείο αυτό μπορούμε να δοκιμάσουμε αν λειτουργεί ο μικροελεγκτής. Δίνουμε 5V και βάζουμε τον μετατροπέα από USB σε RS232 στην υποδοχή της πλακέτας και από την άλλη πλευρά συνδέουμε με μια θύρα USB του υπολογιστή. Κατεβάζουμε ένα μικρό πρόγραμμα π.χ. το blink και ελέγχουμε αν λειτουργεί.</p>
<table align="center">
 <tr>
  <td><img src="/hardware/electronics/schematics+images/test_prog1.jpg" height="300"></td>
  </tr>
 <tr><td align="center"><sub>Τοποθέτηση του μετατροπέα από USB σε σειριακή RS232.</sub></td></tr>
 </table>
 
<b>Η τελική κατασκευή</b>
<p> . </p>
<table align="center">
 <tr>
  <td><img src="/hardware/electronics/schematics+images/schematic.jpg" height="400"></td>
  </tr>
 <tr><td align="center"><sub>Το σχέδιο της τελικής κατασκευής.</sub></td></tr>
 </table>
 
 <table align="center">
 <tr>
  <td><img src="/hardware/electronics/schematics+images/complit1.jpg" height="200"></td>
  <td><img src="/hardware/electronics/schematics+images/complit2.jpg" height="200"></td>
  <td><img src="/hardware/electronics/schematics+images/complit3.jpg" height="200"></td>
  </tr>
 </table>
 
<b>Η μέτρηση της γωνίας</b>
<p> . </p>
<table align="center">
 <tr>
  <td><img src="/hardware/mechanics/interrupter3D.png" height="400"></td>
  </tr>
 <tr><td align="center"><sub>Το γρανάζι 7 δοντιών με τον πλαστικό άξονα και τον δίσκο 16 σχισμών.</sub></td></tr>
 </table>
<table align="center">
 <tr>
  <td><img src="/hardware/electronics/schematics+images/interrupter1.jpg" height="300"></td>
  <td><img src="/hardware/electronics/schematics+images/interrupter2.jpg" height="300"></td>
  </tr>
 </table>

