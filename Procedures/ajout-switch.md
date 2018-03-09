# Ajouter un switch entre un routeur et les périphériques réseaux

Si le switch a déjà été utilisé, il faut le réinitialiser.

## Réinitialiser un switch

1. Brancher le switch au portable via communication série (le port console bleu)
2. Sur le portable, lancer PuTTy sur le port console (COM1)
3. Passer le switch en mode dégradé
   * Débrancher
   * Maintenir le bouton
   * Rebrancher
   * Maintenir le bouton jusqu'à voir un message dans PuTTy
4. Monter la mémoire flash `flash_init`
5. Se déplacer dans le répertoire flash `dir flash:`
6. Effacer les fichiers de configuration `delete flash:fichiers`
7. Reset le switch `reset`
