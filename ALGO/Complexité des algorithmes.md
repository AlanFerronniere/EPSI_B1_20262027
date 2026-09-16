# La complexité des algorithmes

## Définition

La complexité des algorithmes désigne l'étude de la quantité de ressources nécessaires pour exécuter un algorithme. Les ressources les plus couramment analysées sont le temps (complexité temporelle) et l'espace mémoire (complexité spatiale).

## n, n², log(n) et autres

La complexité d'un algorithme est souvent exprimée en fonction de la taille de l'entrée, notée \( n \). Voici quelques notations courantes :
- **O(1)** : Complexité constante. Le temps d'exécution ne dépend pas de la taille de l'entrée.
- **O(log n)** : Complexité logarithmique. Le temps d'exécution augmente logarithmiquement avec la taille de l'entrée.
- **O(n)** : Complexité linéaire. Le temps d'exécution augmente proportionnellement à la taille de l'entrée.
- **O(n log n)** : Complexité quasi-linéaire. Couramment observée dans les algorithmes de tri efficaces.
- **O(n²)** : Complexité quadratique. Le temps d'exécution augmente proportionnellement au carré de la taille de l'entrée.
- **O(2^n)** : Complexité exponentielle. Le temps d'exécution double à chaque augmentation de la taille de l'entrée.
- **O(n!)** : Complexité factorielle. Le temps d'exécution augmente de manière extrêmement rapide avec la taille de l'entrée.
- **O(√n)** : Complexité racine carrée. Le temps d'exécution augmente proportionnellement à la racine carrée de la taille de l'entrée.

O est la notation "Big O", qui décrit une borne supérieure sur le temps d'exécution ou l'espace mémoire en fonction de la taille de l'entrée. C'est à dire le pire cas possible.
## Evaluation de la complexité

Pour évaluer la complexité d'un algorithme, on analyse le nombre d'opérations élémentaires effectuées en fonction de la taille de l'entrée. On se concentre généralement sur le pire cas (worst-case) pour garantir une performance acceptable dans toutes les situations.

## Exemple : recherche sur un tableau

Voici un exemple simple d'algorithme de recherche linéaire dans un tableau, en pseudocode, avec son analyse de complexité :

```
fonction rechercheLinéaire(tableau, valeur) :
		pour i de 0 à Taille(tableau) - 1 faire :
				si tableau[i] == valeur alors :
						retourner i
				fin si
		fin pour
		retourner -1
fin fonction
```

### Analyse de complexité
- **Complexité temporelle** : Dans le pire des cas, l'algorithme parcourt tout le tableau, ce qui donne une complexité de O(n).
- **Complexité spatiale** : L'algorithme utilise un espace constant pour les variables, donc la complexité spatiale est O(1).

## Exemple : tri par inversion
Voici un exemple d'algorithme de tri par inversion (tri à bulles) en pseudocode, avec son analyse de complexité :

```
fonction triParInversion(tableau) :
	n = Taille(tableau)
	pour i de 0 à n - 1 faire :
			pour j de 0 à n - i - 2 faire :
					si tableau[j] > tableau[j + 1] alors :
							échanger(tableau[j], tableau[j + 1])
					fin si
			fin pour
	fin pour
	retourner tableau
fin fonction

```

### Analyse de complexité
- **Complexité temporelle** : Dans le pire des cas, l'algorithme effectue environ \( n^2 \) comparaisons et échanges, ce qui donne une complexité de O(n²).
- **Complexité spatiale** : L'algorithme utilise un espace constant pour les variables, donc la complexité spatiale est O(1).
