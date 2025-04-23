# Débruitage d'Images par ACP

Ce projet vise à implémenter une méthode de débruitage d'images basée sur l'Analyse en Composantes Principales (ACP) en utilisant une approche par patchs.

## Description

Le projet implémente une méthode de débruitage qui :
1. Découpe l'image en petits patchs
2. Applique l'ACP pour réduire le bruit
3. Reconstruit l'image à partir des patchs débruités

## Structure du Projet

```
SAE-PCA-Denoising/
├── README.md                # Ce fichier
├── docs/                    # Documentation
│   └── Livrable1.pdf       # Document de conception
├── images/                  # Base d'images
│   ├── train/              # Images d'entraînement
│   │   ├── original/       # Images originales
│   │   └── noisy/         # Images bruitées
│   └── test/               # Images de test
│       ├── original/       # Images originales
│       └── noisy/         # Images bruitées
├── src/                    # Code source
├── tests/                  # Tests unitaires
└── meta.json              # Métadonnées des images
```

## Installation

1. Cloner le dépôt :
```bash
git clone [URL_DU_REPO]
```

2. Installer les dépendances :
```bash
pip install -r requirements.txt
```

## Utilisation

```python
from denoising import ImageDenoiser

# Charger et débruiter une image
denoiser = ImageDenoiser()
denoised_image = denoiser.denoise("path/to/image.jpg")
```

## Contribution

1. Fork le projet
2. Créer une branche (`git checkout -b feature/AmazingFeature`)
3. Commit les changements (`git commit -m 'Add some AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

## Équipe

- [Membre 1] - Chef de projet
- [Membre 2] - Responsable technique
- [Membre 3] - Data Scientist
- [Membre 4] - Documentation

## Licence

Ce projet est sous licence MIT - voir le fichier [LICENSE.md](LICENSE.md) pour plus de détails.