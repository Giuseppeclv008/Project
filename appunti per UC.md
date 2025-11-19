appunti per UC:



UC2: ho aggiunto la possibilità di omonimia dei suppliers (immaginando che due contadini di nome Mario Rossi consegnino nello stesso negozio. l'identificazione avviene sul codice partita iva, che è univoco)



UC3: aggiunto campo alfanumerico per l'ordine, e anche uno per avere le informazioni sulla spedizione. aggiunta la possibilità di avere ordini che non hanno shipping information, e anche la possibilità capire dal codice che tipo di shipping company



UC4: la fattura viene identificata da un numero. su quel dato viene eseguita una verifica dal sistema, immaginando casi reali dove il numero della fattura è un univoco tracciabile dalla Agenzia delle Entrate per pagamento di tasse ecc. il sistema controlla il numero e se è già all'interno del sistema, da errore.



UC1-UC7: i prodotti sono identificati dal loro codice a barre. consistenza aumentata tra inventario e catalogo



UC8: notifiche inserite, una per tipo



UC9 - UC10: parte di GUI implementata, per semplicità e per paura di rovinare il make non ho implementato i controlli di formato. l'import gestisce sia un import multifile che la possibilità di importare per uno specifico campo (inventory, catalogue…)



UC11: i filtri sono presenti per ogni pagina quindi non ho toccato nulla



UC12: aggiunta granularità corretta sia per le spese che per i guadagni



UC13: aggiunto identificativo casse. non implemento link esterni per andare alla url del pos provider perché nel prototipo non è gestibile



UC14: aggiunta notifica che il polling di una cassa è sbagliato



UC15: sales/refunds mantenuta come prima



UC16: 

