# avec des Notes

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
> Améliorer le programme pour que l'utilisateur puisse saisir autant de note qu'il veut
