RO en attente de la fin de migration


































# bc-relative
bc permet de calculer ; on peut aussi stocker dans des variables, mettre en commentaire ou afficher 

# Calcul lisible
```sh
user@host:~$ echo "\
   /* foo devis initial 256€ \
     + 20€ pour la renovation des phares (de memoire) */ \
foo_mo_devis_initial = 256 ; \
foo_mo_renovation_phare = 20 ; \
\
foo_mo_obligatoire = \
   foo_mo_devis_initial + foo_mo_renovation_phare ; \
titi_non_obligatoire = \
   /* freins AVD/G */ 27.98 + \
   /* barre de triangle ARD/G */ 42.02 + 42.02 ; \
\
total = \
   ( /* ass JFM */ remb_ass_bar = 35 * 3 ) + \
   ( /* CG obligatoire */ cg = 121.76 ) + \
   ( /* CT initial en mai */ ct1 =  84 ) + \
   ( /* CV a venir */ cv = 25 ) + \
( piece_obligatoire = \
   /* essuie_glace_avg */ 8.99 + \
   /* cde_toto */ 189.73 + \
   /* cde_titi (SANS NON obligatoire) */ \
      185.63 - titi_non_obligatoire \
) + \
( piece_non_obligatoire = \
   titi_non_obligatoire + \
   /* batterie_occas */ 20 + \
   /* frein AVD/G fardier (seul vehicule) */ 27.91 \
) + \
( mo_obligatoire = \
   /* loulou asso + tutu */ 10 + \
   foo_mo_obligatoire \
) + \
( mo_non_obligatoire = \
   /* MO foo NON obligatoire ) */ \
      300 - foo_mo_obligatoire ) + \
( transport_remb = \
   /* A peage St L > paris riri*/ 2.40 + \
   /* TER St L > nice (annule, \
      fifi serait venu me chercher en gare) */ 1.70 + \
   /* A peage St L > nice pour retard avec fifi */ 2.70 \
) + \
( transport_non_remb = \
   /* AR St robert <> paris */ (4.68 + 5.19) + \
   /* AR St L <> tokyo (R avec voiture K, \
      a lui remb) */ ( 3.02 + 3.02 ) + \
   /* R tokyo > St L (A avec fifi) */ 3.02 \
) + \
/* tuilage assurance fardier 17/03/21 AM */ ( tuilage = 23 * 2 ) + \
( erreur = \
   /* retour_cde2_par_erreur */ 8.10 + \
   /* CT2 */ 68 + \
   /* tuilage ass excedent mai JnJt paye en A */ 23 * 2 + \
   /* frein AVD/G fardier (seul vehicule) */ 27.91 ) \
; \
\
print \"\n\" ; \
print \"Remb assurance bar : \" , \
    remb_ass_bar , \" €\n\" ; \
print \"CG : \" , \
   cg , \" €\n\" ; \
print \"CT1 en mai : \" , \
   ct1 , \" €\n\" ; \
print \"CV a venir : \" , \
   cv , \" €\n\" ; \
print \"Pièces obligatoires : \" , \
   piece_obligatoire , \" €\n\" ; \
print \"Pièces NON obligatoires : \" , \
   piece_non_obligatoire , \" €\n\" ; \
print \" => total Pièces : \" , \
   piece_obligatoire + piece_non_obligatoire , \" €\n\" ; \
print \"MO obligatoires : \" , \
   mo_obligatoire , \" €\n\" ; \
print \"MO NON obligatoires : \" , \
   mo_non_obligatoire , \" €\n\" ; \
print \" => total MO : \" , \
   mo_obligatoire + mo_non_obligatoire , \" €\n\" ; \
print \"Transports : \" , \
   transport_remb + transport_non_remb , \" €\n\" ; \
print \"Tuilage ass fardier pour CV initiale : \" , \
   tuilage , \" €\n\" ; \
print \"Erreurs (retour cde 2, CT2, tuilage en +, \
frein fardier) : \" , \
      erreur , \" €\n\" ; \
print \"\n\" ; \
print \"=> Total : \" , \
   total, \" €\n\" ; \
print \"\n\" ; \
print \"=> comptabilisable pour collectivite : \" , \
   cg + ct1 + cv + piece_obligatoire + piece_non_obligatoire + \
   mo_obligatoire + mo_non_obligatoire + transport_remb + \
      tuilage + erreur , \
   \" €\n\" ; \
print \"\n\" ; \
print \"=> Comparativement aux 1500 € demandes \
initialement par garagiste\n\" , \
   \"   CT/CV + pieces/MO obligatoire + tuilage + transport : \" , \
   ct1 + cv + piece_obligatoire + mo_obligatoire + tuilage + \
   transport_remb + transport_non_remb , \
   \" €\n\" ; \
print \"Nota : sont exclus remb ass bar (geste de ma part), \
erreurs, CG, \n pieces NON obligatoires\" ; \
print \"\n\" ; \
" | bc
```
```
Remb assurance Bar : 105 €
CG : 121.76 €
CT1 en mai : 84 €
CV a venir : 25 €
Pièces obligatoires : 272.33 €
Pièces NON obligatoires : 159.93 €
 => total Pièces : 432.26 €
MO obligatoires : 286 €
MO NON obligatoires : 24 €
 => total MO : 310 €
Transports : 25.73 €
Tuilage ass fardier pour CV initiale : 46 €
Erreurs (retour cde 2, CT2, tuilage en +, frein fardier) : 150.01 €

=> Total : 1299.76 €

=> comptabilisable pour collectivite : 1175.83 €

=> Comparativement aux 1500 € demandes initialement par garagiste
   CT/CV + pieces/MO obligatoire + tuilage + transport : 739.06 €
Nota : sont exclus remb ass barr (geste de ma part), erreurs, CG, 
  pieces NON obligatoires
```
# Calcul avec décimales
Par défaut calcule avec des entiers ; si on veut gérer les nombres décimaux il faut ajouter le paramètre -l (L minuscule)
```sh
user@host:~$ bc -l
```
