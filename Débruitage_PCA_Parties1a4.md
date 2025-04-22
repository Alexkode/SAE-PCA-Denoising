
# Débruitage d’images par Analyse en Composantes Principales (ACP)

## Partie 1 : Une image est dégradée par du bruit gaussien

### 1. Qu’est-ce qu’une image numérique ?
Une image en niveaux de gris est représentée par une **matrice de réels** \( X_0 \in \mathbb{R}^{\ell \times c} \), où :
- \( \ell \) est le nombre de lignes (hauteur),
- \( c \) est le nombre de colonnes (largeur),
- Chaque valeur \( X_0(i, j) \in [0, 255] \) est l’intensité d’un pixel.

### 2. Ajout du bruit
On ajoute un **bruit gaussien additif centré** :
\[
X_b(i, j) = X_0(i, j) + n(i, j)
\]
avec :
- \( n(i, j) \sim \mathcal{N}(0, \sigma^2) \)

Le bruit est **i.i.d.** : indépendant et identiquement distribué.

### 3. Pourquoi du bruit gaussien ?
Modèle réaliste du bruit des capteurs. Facile à simuler :
```java
Random rand = new Random();
double bruit = rand.nextGaussian() * sigma;
Xb[i][j] = X0[i][j] + bruit;
```

---

## Partie 2 : On extrait des petits morceaux (patchs)

### 1. Pourquoi ?
- Facilite l’analyse locale (contours, textures),
- Travaille sur des vecteurs de petite dimension,
- Permet d’identifier des motifs répétitifs.

### 2. Définition
Un **patch** est une sous-matrice carrée de taille \( s \times s \), extraite de l’image \( X_b \).

### 3. Vectorisation
Chaque patch est transformé en un vecteur colonne :
\[
v_k = \text{Vect}(P_k) \in \mathbb{R}^{s^2}
\]

### 4. Ensemble des patchs
\[
V = [v_1\ |\ v_2\ |\ \cdots\ |\ v_M] \in \mathbb{R}^{s^2 \times M}
\]

---

## Partie 3 : On applique l’ACP pour détecter l’information importante et enlever le bruit

### 1. Moyenne des vecteurs
\[
m_V = \frac{1}{M} \sum_{k=1}^{M} v_k
\]

### 2. Centrage
\[
v_k^c = v_k - m_V
\]

### 3. Matrice de covariance
\[
\Gamma = \frac{1}{M} V_c V_c^T
\]

### 4. Diagonalisation
\[
\Gamma u_i = \lambda_i u_i
\]

### 5. Projection dans la base propre
\[
\alpha_i^{(k)} = u_i^T (v_k - m_V)
\]

---

## Partie 4 : On reconstruit l’image nettoyée

### 1. Reconstruction d’un patch
\[
\hat{v}_k = m_V + \sum_{i=1}^{s^2} \tilde{\alpha}_i^{(k)} u_i
\]

### 2. Inverse de la vectorisation
\( \hat{v}_k \rightarrow \hat{P}_k \in \mathbb{R}^{s \times s} \)

### 3. Recollage des patchs

#### Cas 1 : Patchs non superposés  
Placer directement chaque patch à sa position.

#### Cas 2 : Patchs superposés (avec moyenne)
\[
\hat{X}(i,j) = \frac{\hat{X}_{sum}(i,j)}{W(i,j)}
\]

### 4. Évaluation finale
- **MSE** :
\[
\text{MSE} = \frac{1}{\ell \cdot c} \sum_{i=1}^{\ell} \sum_{j=1}^{c} \left( X_0(i,j) - \hat{X}(i,j) \right)^2
\]

- **PSNR** :
\[
\text{PSNR} = 10 \cdot \log_{10} \left( \frac{255^2}{\text{MSE}} \right)
\]
