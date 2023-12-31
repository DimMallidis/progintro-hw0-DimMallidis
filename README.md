Περιγραφή της λύσης του καθε σταδίου. Μετά από κάθε στάδιο χρησιμοποίησα το command: "exit" ώστε στην συνέχεια μέσω του command:
"ssh banditx@bandit.labs.overthewire.org -p220" και της εισαγωγής του εκάστοτε κωδικού να εισέλθω στο επόμενο στάδιο.
(όπου x αναφέρεται στο αντίστοιχο στάδιο π.χ. bandit0, bandit1....) 

bandit0: Δίνεται από το overthewire.
 
bandit1: Για να διαβάσουμε το αρχείο readme χρησιμοποιούμε το commmand: "cat readme". Μέσα στο αρχείο "readme" βρίσκεται ο κωδικός.
 
bandit2: Επειδή το αρχείο "-" ξεκινά με χαρακτήρα "-" για να το διαβάσουμε πρέπει να χρησιμοποιήσουμε το command: "cat < -". Αν χρησιμοποιηθεί το command "cat -" τότε αντί να διαβάσουμε το αρχείο ενεργοποιείται standard input. Μέσα στο αρχείο "-" βρίσκεται ο κωδικός. 

bandit3: Για να διαβαστεί το αρχείο "spaces in this filename" πρέπει να χρησιμοποιηθεί το command: "cat 'spaces in this filename'" διότι το command: "cat spaces in this filename" οδηγεί το σύστημα στο να αναζητήσει 4 διαφορετικά και μη υπαρκτά αρχεία ("spaces", "in", "this", "filename"). Μέσα στο αρχείο "spaces in this filename" βρίσκεται ο κωδικός.

bandit4: Αρχικά χρησιμοποιούμε το command: "cd inhere" ώστε να εισέλθουμε στο directory: inhere. Στην συνέχεια, χρησιμοποιούμε το command: "ls -a" ώστε να δούμε όλα τα περιεχόμενα του directory, ακόμα και τα hidden files. Έτσι βλέπουμε πως το μοναδικό αρχείο είναι το ".hidden" το οποίο είναι hidden καθώς το ονομά του ξεκινά με (.). Άρα χρησιμοποιούμε το command "cat .hidden". Μέσα στο αρχείο ".hidden" βρίσκεται ο κωδικός.

bandit5: Αρχικά χρησιμοποιούμε το command: "cd inhere" ώστε να εισέλθουμε στο directory: inhere. Στην συνέχεια, χρησιμοποιούμε το command: "ls -a" ώστε να δούμε όλα τα αρχεία μέσα στο directory. Χρησιμοποιούμε το command "file ./-file0*" ώστε να δούμε τι τύπου αρχείου είναι το καθένα. Παρατηρούμε πως το μόνο human-readable είναι το αρχείο "-file07" άρα γράφουμε "cat < -file07". Μέσα στο αρχείο "-file07" βρίσκεται ο κωδικός.

bandit6: Αρχικά χρησιμοποιούμε το command: "find ./inhere/ -type f -size 1033c" ώστε να αναζητήσουμε το αρχείο το οποίο έχει μέγεθος 1033 bytes στο directory: "inhere". Άρα χρησιμοποιούμε το command "cat ./inhere/maybehere07/.file2" καθώς το αρχείο έχει το κατάλληλο μέγεθος. Μέσα στο αρχείο "./maybehere07/.file2" βρίσκεται ο κωδικός.

bandit7: Θα χρησιμοποιήσουμε το command: "find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null" ώστε να αναζητήσουμε αρχεία από όλο το server τα οποία ανήκουν στον χρήστη bandit7 και στο group bandit6 και έχουν μέγεθος 33 bytes. Επειδή σε πολλά από αυτά τα αρχεία δεν έχουμε πρόσβαση παρουσιάζονται διάφορα errors αν δεν έχουμε χρησιμοποιήσει το command "2>/dev/null".  Άρα χρησιμοποιούμε το command "cat /var/lib/dpkg/info/bandit7.password" καθώς αυτό είναι το μοναδικό αρχείο στο οποίο έχουμε πρόσβαση. Μέσα στο αρχείο "/var/lib/dpkg/info/bandit7.password" βρίσκεται ο κωδικός.

bandit8: Αφού δοκιμάσουμε το command "cat data.txt" τότε παρατηρούμε πως αποτελείται από έναν μεγάλο αριθμό γραμμών. Άρα θα χρησιμοποιήσουμε το command "grep "millionth" data.txt" ώστε να εντοπίσουμε τη γραμμή στην οποία βρίσκεται ο κωδικός.


bandit9: Για να βρούμε τον κωδικό αυτού του σταδίου πρέπει να δημιουργήσουμε ένα pipeline. Το command: "uniq -u" είναι ικανό να παρουσιάσει μόνο το line στο αρχείο το οποίο δεν επαναλαμβάνεται όμως για να αναγνωρίσει τα επαναλαμβανόμενα lines πρέπει αυτά να είναι το ένα κάτω από το άλλο (adjacent). Δηλαδή αν το αρχείο είχε την εξής μορφή: [

i like music

i hate music

i like music
]

τότε αν χρησιμοποιούσαμε το command: "uniq -u" δεν θα επέστρεφε το επιθυμητό: "i hate music" αλλά θα επέστρεφε το αρχικό αρχείο χωρίς να έχει αφαιρέσει κάποιο line. Άρα απαιτείται να κάνουμε sort τα lines του αρχείου. Άρα τελικά χρησιμοποιούμε το command: "sort data.txt| uniq -u" το οποίο επιστρέφει τον κωδικό.


bandit10: Θα χρησιμοποιήσουμε το command: " strings data.txt| grep ==" καθώς με αυτόν τον τρόπο θα παρουσιαστούν από το αρχείο data.txt μόνο τα strings τα οποία είναι human readable και περιέχουν δύο ή περισσότερα "=". Με αυτόν τον τρόπο, από τα 4 strings που τυπώνονται εύκολα αναγνωρίζουμε ποιός είναι ο κωδικός.

bandit11: Θα χρησιμοποιήσουμε το command "base64 -d data.txt" για να αποκωδικοποιήσουμε το αρχείο το οποίο περιέχει τον κωδικό.


