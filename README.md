Περιγραφή της λύσης του καθε σταδίου. Μετά από κάθε στάδιο χρησιμοποίησα το command: "exit" ώστε στην συνέχεια μέσω του command:
"ssh banditx@bandit.labs.overthewire.org -p220" και της εισαγωγής του εκάστοτε κωδικού να εισέλθω στο επόμενο στάδιο.
(όπου x αναφέρεται στο αντίστοιχο στάδιο π.χ. bandit0, bandit1....) 

bandit0: Δίνεται από το overthewire.
 
bandit1: Για να διαβάσουμε το αρχείο readme χρησιμοποιούμε το commmand: "cat readme". Μέσα στο αρχείο "readme" βρίσκεται ο κωδικός.
 
bandit2: Επειδή το αρχείο "-" ξεκινά με χαρακτήρα "-" για να το διαβάσουμε πρέπει να χρησιμοποιήσουμε το command: "cat < -". Αν χρησιμοποιηθεί το command "cat -" τότε αντί να διαβάσουμε το αρχείο ενεργοποιείται standard input. Μέσα στο αρχείο "-" βρίσκεται ο κωδικός. 

bandit3: Για να διαβαστεί το αρχείο "spaces in this filename" πρέπει να χρησιμοποιηθεί το command: "cat 'spaces in this filename'" διότι το command: "cat spaces in this filename" οδηγεί το σύστημα στο να αναζητήσει 4 διαφορετικά και μη υπαρκτά αρχεία ("spaces", "in", "this", "filename"). Μέσα στο αρχείο "spaces in this filename" βρίσκεται ο κωδικός.
