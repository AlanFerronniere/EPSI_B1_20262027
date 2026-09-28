# avec des Notes

> **Équivalent PHP :** Voir [[Exercice 1 en PHP]]

## Etape 1
> Demander à l'utilisateur de saisir 10 notes qu'on stocke dans un tableau

```
Variable notes : tableau[10] Entier
Pour i de 0 à 9 Faire
	Ecrire "Note N°" + (i+1)
	Lire note[i]
Fin Pour
```

Dans un language qui permet des tableaux dynamiques (dont on ne donne pas la taille en définissant la variable), ça donne :
```
Variable notes : tableau[] Entier
Pour i de 0 à 9 Faire
	Ecrire "Note" + (i+1)
	Lire note[] //pas besoin de mettre l'indice
Fin Pour
```

## Etape 2
> Calculer la moyenne de ce qu'il y a dans le tableau

```
Variable notes : tableau[] Entier
Pour i de 0 à 9 Faire
	Ecrire "Note" + (i+1)
	Lire note[] //pas besoin de mettre l'indice
Fin Pour

Variable somme : Reel <- 0
Variable moyenne : Reel

Pour i de 0 à 9 Faire
	somme <- somme + notes[i]
Fin Pour

moyenne <- somme / 10

Ecrire "La moyenne est : " + moyenne 
```

## Etape 3
> Améliorer le programme pour que l'utilisateur puisse saisir autant de note qu'il veut (jusqu'à ce qu'il fasse une entrée vide)

```
Variable notes : tableau[] Reel
Variable saisie : Chaine

Ecrire "Entrez une note (laisser vide pour terminer) :"
Lire saisie

Tant Que saisie != "" Faire
	notes[] <- saisie
	Ecrire "Entrez une note (laisser vide pour terminer) :"
	Lire saisie
Fin Tant Que

Variable somme : Reel <- 0
Variable moyenne : Reel

Si Taille(notes) > 0 Alors
	Pour i de 0 à Taille(notes) - 1 Faire
		somme <- somme + notes[i]
	Fin Pour

	moyenne <- somme / Taille(notes)

	Ecrire "La moyenne est : " + moyenne
Sinon
	Ecrire "Aucune note n'a été saisie."
Fin Si
```

> **Variante pour le parcours du tableau :**  
> On peut aussi utiliser la boucle `Pour Chaque` pour simplifier le calcul de la somme :
> ```
> Pour Chaque note dans notes Faire
> 	somme <- somme + note
> Fin Pour
> ```

### Variante en une seule boucle (sans tableau et avec filtrage)
Si le but est uniquement de calculer la moyenne sans conserver l'historique de chaque note, on peut se passer complètement de tableau en utilisant un simple compteur. On peut également filtrer la saisie pour s'assurer que la note est comprise entre 0 et 20 :

```
Variable saisie : Chaine
Variable note : Reel
Variable somme : Reel <- 0
Variable nbNotes : Entier <- 0
Variable moyenne : Reel

Ecrire "Entrez une note entre 0 et 20 (laisser vide pour terminer) :"
Lire saisie

Tant Que saisie != "" Faire
	note <- ConvertirEnReel(saisie)
	Si note >= 0 et note <= 20 Alors
		somme <- somme + note  // Cumul direct
		nbNotes <- nbNotes + 1 // Comptage des notes valides
	Sinon
		Ecrire "Erreur : la note doit être comprise entre 0 et 20."
	Fin Si

	Ecrire "Entrez une note entre 0 et 20 (laisser vide pour terminer) :"
	Lire saisie
Fin Tant Que

Si nbNotes > 0 Alors
	moyenne <- somme / nbNotes
	Ecrire "La moyenne est : " + moyenne
Sinon
	Ecrire "Aucune note valide n'a été saisie."
Fin Si
```

