🛠 Présentation technique du projet SIMPLE-RNN-IMDB
1. Objectif
Implémenter un modèle de sentiment analysis sur le dataset IMDB (50 000 critiques de films labellisées positive / negative) en utilisant un Simple Recurrent Neural Network.

2. Dataset
Source : keras.datasets.imdb

Pré-traitement :

Limitation du vocabulaire aux n mots les plus fréquents (ex. : 10 000)

Padding/Truncation des séquences à longueur fixe (maxlen)

Représentation des mots par indices entiers (Word Index de Keras)

3. Architecture du modèle
python
Copier
Modifier
model = Sequential()
model.add(Embedding(input_dim=vocab_size,
                    output_dim=embedding_dim,
                    input_length=maxlen))
model.add(SimpleRNN(units=hidden_units,
                    activation='tanh'))
model.add(Dense(1, activation='sigmoid'))
Layer 1 : Embedding — vecteur dense pour chaque mot

Layer 2 : SimpleRNN — traite la séquence mot par mot, garde un état caché

Layer 3 : Dense (sigmoid) — sortie binaire (probabilité d’avis positif)

4. Entraînement
Loss : binary_crossentropy

Optimizer : adam

Metrics : accuracy

Batch size : typiquement 32 ou 64

Epochs : 5–10 (selon convergence et overfitting)

Split : train/test 50 % chacun (IMDB déjà pré-partagé par Keras)

5. Points techniques importants
Le SimpleRNN est utilisé pour la clarté pédagogique, mais souffre du vanishing gradient sur longues séquences → pas optimal pour textes longs (LSTM/GRU plus performants).

Embedding trainable : ajusté pendant l’entraînement pour améliorer la représentation sémantique.

Binary output avec sigmoid → seuil de 0.5 pour la classification.

6. Extensions possibles
Remplacer SimpleRNN par LSTM/GRU

Utiliser des embeddings pré-entraînés (GloVe, fastText)

Ajouter un dropout récurrent pour limiter l’overfitting

Fine-tuning sur d’autres datasets pour meilleure généralisation

💡 Pitch technique résumé :

Pipeline Keras → IMDB dataset tokenisé & padé → Embedding → SimpleRNN → Dense Sigmoid.
Objectif : démontrer le fonctionnement d’un RNN de base pour du NLP binaire.
---------------------------------------------------------------------------------------------------------------------------------------------------

Explication accessible du projet « SIMPLE-RNN-IMDB »
1. Le sujet du projet
Ce projet utilise une forme d’intelligence artificielle (un Simple RNN) pour analyser des critiques de films IMDB et déterminer si elles sont positives ou négatives, un peu comme un quiz automatique : « Est-ce que ce film est jugé bon ou mauvais ? ».

2. Comment ça fonctionne, simplement ?
Le texte d’un avis est transformé en une liste de nombres (chaque mot reçoit un numéro unique). Cela permet à l’ordinateur de "traduire" le texte.
Keras

Ensuite, ce "texte traduit" passe dans un petit réseau neuronal qui lit les mots un par un, en mémorisant ce qui a été lu juste avant, un peu comme si on lisait une phrase et qu’on se souvient du début pour comprendre la suite.


Après avoir lu tout l’avis, le réseau décide s’il est positif (aimé) ou négatif (pas aimé). Le résultat s’affiche souvent sous forme de pourcentage de confiance.

3. À quoi ça ressemble pour un utilisateur non-technique ?
Tu ouvres une petite application web.

Tu colles un texte comme : "Ce film était incroyable, j’ai adoré l’histoire et les acteurs."

Tu cliques sur un bouton, et l’IA te répond : "Avis POSITIF (95 % de confiance)".

Et ça marche aussi avec un avis négatif, genre : "Ennuyeux, fade, je ne le recommande pas."

4. Les grandes étapes concrètes (version "humaine")
Préparation des avis
Les avis de films sont organisés, triés et transformés en données lisibles par machine.


Formation du modèle
Le réseau apprend à repérer des schémas : quel type de phrases correspond à un avis positif ou négatif.


L’œil qui lit (l’interface utilisateur)
Une interface simple (souvent développée avec Streamlit) permet à chacun d’écrire un avis et de voir instantanément s’il est positif ou négatif.


En résumé pour une personne non-technique
Tu as un assistant virtuel qui lit des critiques de films et te dit instantanément si c’est un avis positif ou négatif. Il apprend en lisant des milliers d’avis existants, puis exploite ce qu’il a appris pour analyser de nouveaux avis en temps réel.
