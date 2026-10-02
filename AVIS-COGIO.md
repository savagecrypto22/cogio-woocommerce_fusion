# Avis de modification

Ce dépôt est une version modifiée de WooCommerce Fusion, publiée par Cogio le 2026-10-01.

- Projet d'origine : https://github.com/Starktail/woocommerce_fusion
- Révision d'origine : `ab71a15d322232fff58d93fa0aa469812bfa9a30` (branche `version-16`)
- Licence : GNU General Public License v3.0, celle que déclare le projet d'origine (`README.md`, `hooks.py`).
  Le projet d'origine ne porte pas de fichier de licence : le texte de la GPL-3.0 est ajouté ici (`LICENSE`), sans
  rien changer aux droits.
- Branche modifiée : `cogio`.

## Ce qui change

1. Validation et annulation d'une facture de vente, d'une entrée de stock, d'un rapprochement de stock et d'un bon
   de livraison : le crochet `update_stock_levels_for_woocommerce_item` cherchait les serveurs WooCommerce actifs
   par `frappe.get_list`, une lecture soumise aux droits de la personne. Une personne qui ne lit pas le type
   « WooCommerce Server » (seul le gestionnaire du système le lit) ne pouvait donc valider aucun de ces documents,
   même sans aucune boutique branchée (« Insufficient Permission for WooCommerce Server »). Le crochet lit
   maintenant sa propre configuration sans les droits de la personne (`frappe.db.exists`) et s'arrête tout de suite
   quand aucun serveur actif ne synchronise les stocks. Rien de la configuration n'est montré à la personne.

Aucune autre règle n'est modifiée : avec un serveur actif, la mise à jour des stocks part comme avant.

## Fichiers modifiés ou ajoutés

- `woocommerce_fusion/tasks/stock_update.py`
- `LICENSE`
- `AVIS-COGIO.md`
