MISSION : INTÉGRATION PROFESSIONNELLE — ICT + 73 CANDLE PATTERNS
NINJA PROTRADER + L_LUCIEN PROTRADER + AUTO TRADE + STRATEGY TESTER

======================================================================
0. FICHIERS DE RÉFÉRENCE
======================================================================

PROJET CIBLE À MODIFIER :



SOURCE OFFICIELLE DES 73 PATTERNS CANDLE :

super_candles.zip

FICHIER DE DIAGNOSTIC :

po_v6_.zip

IMPORTANT :

- Le projet cible est la base principale.
- super_candles.zip est la SEULE source de vérité pour les candlestick patterns.
- pine_v6_engine_v26_73_candle_patterns.zip est UNIQUEMENT une version à AUDITER pour comprendre les erreurs.
- Ne considère jamais v26 comme référence fonctionnelle.
- Ne copie pas aveuglément le code de v26.
- Ne remplace pas l’architecture du projet cible par celle de v26.
- Ne repars pas de zéro.

======================================================================
1. OBJECTIF FINAL
======================================================================

Intégrer les 73 candlestick patterns de super_candles.zip dans les DEUX
stratégies existantes :

1. Ninja ProTrader
2. L_Lucien ProTrader

ET permettre leur utilisation dans :

- Auto Trade
- Strategy Tester
- Rule Builder CALL/PUT
- Lightweight Charts
- « Tags & labels sur le graphique »

Tout en conservant intégralement :

- BOS Up
- BOS Down
- CHoCH Up
- CHoCH Down
- CISD Up
- CISD Down
- Candles Validation
- CISD Guard
- remaining Time Before Candle Closure
- logique Ninja
- logique L_Lucien
- Replay Engine
- money management
- payout
- règlement WIN/LOSS/TIE
- fonctionnalités existantes

AUCUNE RÉGRESSION ACCEPTÉE.

======================================================================
2. RÈGLE ABSOLUE : SOURCE DE VÉRITÉ DES CANDLES
======================================================================

Les 73 patterns doivent être pris DIRECTEMENT depuis :

super_candles.zip

Le nombre final DOIT être :

73

Pas 72.
Pas 74.
Pas 80.

Créer un contrôle automatique :

sourcePatternIds
vs
integratedPatternIds

Le test doit exiger :

count(sourcePatternIds) === 73
count(integratedPatternIds) === 73
Set(sourcePatternIds) === Set(integratedPatternIds)

Toute différence = FAIL.

======================================================================
3. NE JAMAIS INVENTER DE PATTERN
======================================================================

INTERDIT :

- nouveaux patterns
- alias
- synonymes
- variantes artificielles
- patterns composites
- patterns renommés
- patterns fusionnés

Exemple INTERDIT :

Doji + Spinning Top

devenant :

DOJI · SPINNING TOP

Ils restent DEUX patterns distincts.

Exemple INTERDIT :

Hammer + Bullish Engulfing

devenant :

ENGULFING · HAMMER

Ils restent DEUX patterns distincts.

======================================================================
4. NOM EXACT DES 73 PATTERNS
======================================================================

Les labels doivent utiliser exactement les noms de super_candles.zip.

INTERDIT de faire :

Bullish Engulfing → ENGULFING

Bullish Marubozu → MARUBOZU

Long-Legged Doji → DOJI

Bearish Harami Cross → HARAMI

Upgap Side-by-Side White Lines
→ SIDE-BY-SIDE

INTERDIT.

Conserver le nom complet.

Exemple :

Bullish Engulfing

reste :

Bullish Engulfing

======================================================================
5. UN PATTERN = UN ÉVÉNEMENT = UN LABEL
======================================================================

C’est une règle CRITIQUE.

Si une même bougie détecte :

Doji
Spinning Top
Long-Legged Doji

alors le moteur contient :

3 événements indépendants.

Et l’overlay affiche :

3 labels indépendants.

JAMAIS :

Doji · Spinning Top · Long-Legged Doji

JAMAIS un badge multi-pattern.

JAMAIS de concaténation.

Ne jamais utiliser une logique du type :

join(' · ')

ou toute autre fusion de textes.

======================================================================
6. LES 73 PATTERNS DOIVENT RESTER INDÉPENDANTS
======================================================================

Si :

Doji = true
Spinning Top = true

Alors :

Doji = événement 1
Spinning Top = événement 2

Ils peuvent être vrais simultanément.

Ils ne doivent jamais être considérés comme un seul pattern.

Même logique pour tous les patterns du pack source.

======================================================================
7. NE PAS LIMITER LA DÉTECTION
======================================================================

INTERDIT :

limiter les candles à :

- 1 pattern
- 2 patterns
- 3 patterns

La détection doit toujours évaluer les 73 patterns.

L’UI peut masquer des patterns.

Mais :

DISPLAY FILTER ≠ DETECTION FILTER

Si Hammer est masqué :

Hammer continue d’exister dans le moteur.

======================================================================
8. DISPLAY FILTERS
======================================================================

Le switch existant :

Tags & labels sur le graphique

reste le MASTER SWITCH.

OFF :

aucun label.

ON :

l’utilisateur peut sélectionner ce qu’il veut afficher.

Créer des groupes repliables.

STRUCTURE
---------

BOS Up
BOS Down
CHoCH Up
CHoCH Down
CISD Up
CISD Down

ICT
---

BISI
SIBI
BISI Rebalanced
SIBI Rebalanced
VI Up
VI Down
GI Up
GI Down
CE

BLOCKS
------

OB Up
OB Down
OB Up+
OB Down+
OB Up Retest
OB Down Retest

Breaker Up
Breaker Down
Breaker Up Retest
Breaker Down Retest

MB Up
MB Down
MB Up Retest
MB Down Retest

SWINGS
------

HH
HL
LH
LL
Swing High
Swing Low

LIQUIDITY
---------

BSL
SSL
Old High
Old Low
Liquidity Pool
Buystops Purged
Sellstops Purged

PO3
---

Po3 Buy
Po3 Sell
Judas Swing Up
Judas Swing Down
Midnight Open

SMT
---

SMT Bullish
SMT Bearish

AMD
---

Accumulation
Manipulation
Distribution

CANDLE PATTERNS
---------------

Bullish Patterns MASTER
Bearish Patterns MASTER
Neutral Patterns MASTER

PLUS :

un checkbox individuel pour CHACUN des 73 patterns.

======================================================================
9. FILTRES CANDLE INDIVIDUELS
======================================================================

Exemple :

☑ Doji
☑ Bullish Marubozu
☐ Bearish Marubozu
☑ Spinning Top
☐ Hammer
☑ Bullish Engulfing
etc.

Si :

Hammer = OFF

alors :

Hammer invisible.

Mais :

Hammer reste disponible dans :

- Rule Builder
- Auto Trade
- Strategy Tester
- Event Engine

======================================================================
10. LES LABELS DOIVENT RESTER ATTACHÉS AUX BOUGIES
======================================================================

C’est également CRITIQUE.

Chaque label doit être lié à :

- candleTime
- barIndex
- priceAnchor

NE PAS utiliser une coordonnée pixel fixe persistante.

INTERDIT :

x = 500
y = 300

Une fois le graphique déplacé :

le label doit suivre la bougie.

======================================================================
11. ZOOM / DEZOOM / PAN
======================================================================

Tester explicitement :

- zoom in
- zoom out
- pan left
- pan right
- changement du visible range

Le label doit rester attaché EXACTEMENT à la même bougie.

Aucun label ne doit :

- rester fixe à l’écran ;
- glisser ;
- se détacher ;
- changer de bougie ;
- changer arbitrairement de côté.

Le positionnement doit être recalculé depuis :

time → coordinate X

price → coordinate Y

à chaque update du viewport.

======================================================================
12. COLLISION MANAGER
======================================================================

Créer un vrai gestionnaire de placement.

IMPORTANT :

Ce gestionnaire NE REGROUPE JAMAIS les événements.

Il fait uniquement :

- collision detection
- placement
- reflow
- spacing
- anchoring
- reuse

Chaque événement reste indépendant.

======================================================================
13. COLLISION = BOUNDING BOX RÉELLE
======================================================================

Pour chaque label :

calculer :

left
right
top
bottom

en fonction de :

- largeur réelle du texte
- hauteur réelle
- taille choisie

Utiliser :

measureText()

pour mesurer le texte.

Ne pas utiliser une largeur constante arbitraire.

Deux rectangles ne doivent jamais se chevaucher.

======================================================================
14. LANES
======================================================================

Créer des voies :

ABOVE:

lane 0
lane 1
lane 2
lane 3
lane 4
...

BELOW:

lane 0
lane 1
lane 2
lane 3
lane 4
...

Exemple :

Bougie 100 :

BOS Down
→ Above lane 0

Shooting Star
→ Above lane 1

Doji
→ Above lane 2

Bougie 101 :

CISD Down
→ Above lane 0

Hanging Man
→ Above lane 1

Jamais deux rectangles superposés.

======================================================================
15. PRIORITÉ VISUELLE
======================================================================

Ordre de placement :

1. BOS / CHoCH / CISD
2. ICT setup
3. Candle Pattern
4. Swing
5. Liquidity
6. Context

IMPORTANT :

la priorité ne signifie PAS fusion.

Elle signifie uniquement :

qui prend la meilleure voie visuelle.

======================================================================
16. NE PAS MODIFIER LE POSITIONNEMENT HISTORIQUE BOS/CHoCH/CISD
======================================================================

Le projet cible possède déjà une logique graphique pour :

BOS
CHoCH
CISD

NE PAS la remplacer par un nouveau renderer générique si cela modifie :

- leur position ;
- leur distance ;
- leur ordre ;
- leur couleur ;
- leur taille ;
- leur ancrage.

L’ajout des candles doit s’intégrer AUTOUR du système existant.

Si nécessaire :

conserver renderer historique BOS/CHoCH/CISD

ET créer un renderer compatible pour les nouveaux événements.

======================================================================
17. BOS / CHOCH / CISD RESTENT SÉPARÉS
======================================================================

Si une bougie possède :

BOS Down
CHoCH Down
CISD Down

afficher :

BOS Down
CHoCH Down
CISD Down

Trois labels séparés.

Jamais :

BOS Down · CHoCH Down · CISD Down

======================================================================
18. ICÔNES
======================================================================

NE PAS utiliser de petits marqueurs sans texte.

INTERDIT :

- micro triangles
- micro points
- petites icônes ambiguës

Le texte doit être lisible.

======================================================================
19. LABEL SIZE
======================================================================

Le sélecteur doit proposer EXACTEMENT :

Very Tiny
Tiny
Small
Normal
Large
Huge

Valeurs possibles :

Very Tiny = 6 px
Tiny = 8 px
Small = 10 px
Normal = 12 px
Large = 18 px
Huge = 24 px

Les valeurs exactes peuvent être adaptées si le renderer du projet l’exige.

Mais :

Very Tiny DOIT exister.
Tiny DOIT exister.

======================================================================
20. LABELS LONGS
======================================================================

Les noms longs ne doivent pas être tronqués.

Exemple :

Upgap Side-by-Side White Lines

Si nécessaire :

Upgap Side-by-Side
White Lines

dans UN SEUL label.

Mais toujours :

UN SEUL pattern.

Ne jamais fusionner avec un second pattern.

======================================================================
21. NINJA PROTRADER
======================================================================

Conserver EXACTEMENT :

- détection sur bougie en formation ;
- signal intrabar ;
- prix réel ;
- logique existante ;
- anti-retrigger ;
- Candles Validation historique ;
- CISD Guard ;
- remaining Time Before Candle Closure.

Les Candle Patterns doivent être compatibles avec cette temporalité.

======================================================================
22. L_LUCIEN PROTRADER
======================================================================

Conserver EXACTEMENT :

- confirmation à clôture ;
- signal sur bougie clôturée ;
- Candles Validation ;
- CISD Guard ;
- expiration existante.

Les Candle Patterns doivent être confirmés selon cette logique.

======================================================================
23. UN SEUL MOTEUR DE DÉTECTION
======================================================================

Architecture :

EVENT ENGINE
    ↓
SIGNAL REGISTRY
    ↓
RULE ENGINE
    ↓
NINJA / LUCIEN
    ↓
AUTO TRADE / STRATEGY TESTER

Ne pas créer un Candle Engine Ninja
et un Candle Engine Lucien.

======================================================================
24. ICT EVENTS
======================================================================

Conserver/intégrer :

BISI
SIBI
BISI Rebalanced
SIBI Rebalanced
VI Up
VI Down
GI Up
GI Down
CE

OB Up
OB Down
OB Up+
OB Down+
OB Up Retest
OB Down Retest

Breaker Up
Breaker Down
Breaker Up Retest
Breaker Down Retest

MB Up
MB Down
MB Up Retest
MB Down Retest

Po3 Buy
Po3 Sell
Judas Swing Up
Judas Swing Down
Midnight Open

HH
HL
LH
LL

BSL
SSL
Old High
Old Low
Liquidity Pool
Buystops Purged
Sellstops Purged

SMT Bullish
SMT Bearish

AMD Accumulation
AMD Manipulation
AMD Distribution

DRT
DRH
DRL
DRT 75
DRT 50
DRT 25
Premium
Discount

IMPORTANT :

Les éléments de type LEVEL / CONTEXT ne sont pas automatiquement des triggers CALL/PUT.

======================================================================
25. ICT SIGNAL REGISTRY
======================================================================

Chaque événement doit avoir :

id
label
category
direction
nature
available
displayDefault
tradable

Exemple :

BISI :

id:
bisi

label:
BISI

category:
IMBALANCE

direction:
up

nature:
SIGNAL

======================================================================
26. INTERDICTION DU FAUX REGISTRY
======================================================================

Ne pas faire ceci :

déclarer :

BISI
OB Up
Breaker Up

dans un registry

avec :

available = false

sans implémentation.

SI UN SIGNAL EST DÉCLARÉ DISPONIBLE :

IL DOIT ÊTRE RÉELLEMENT DÉTECTÉ.

Sinon :

ne pas le présenter comme intégré.

======================================================================
27. RULE BUILDER
======================================================================

Le Rule Builder doit accepter :

ICT
+
Candle
+
Swing
+
Liquidity
+
Po3
+
SMT

Exemple CALL :

BOS Up
+
BISI
+
Bullish Engulfing
+
OB Up

AND réel.

Exemple PUT :

BOS Down
+
SIBI
+
Bearish Engulfing
+
Breaker Down Retest

AND réel.

======================================================================
28. NOMBRE DE CONDITIONS
======================================================================

Ne pas limiter arbitrairement à deux conditions.

L’utilisateur doit pouvoir :

Ajouter une condition
Ajouter une condition
Ajouter une condition
...

jusqu’à une limite raisonnable définie par l’architecture.

Chaque condition est AND.

======================================================================
29. CONFLIT CALL / PUT
======================================================================

Si une règle CALL et une règle PUT de même spécificité deviennent vraies :

HOLD.

Ne jamais choisir arbitrairement.

======================================================================
30. EXPIRATION EN BOUGIES
======================================================================

Le Rule Builder DOIT proposer :

Expiration Mode :

Candles

Expiration :

1
2
3
5
10

Le modèle doit stocker :

expirationMode

expirationCandles

======================================================================
31. STRATEGY TESTER
======================================================================

Le Strategy Tester DOIT proposer :

L_Lucien ProTrader

Ninja ProTrader

Les deux doivent être réellement fonctionnels.

Pas seulement un selector visuel.

======================================================================
32. STRATEGY TESTER + NINJA
======================================================================

Ninja doit respecter son comportement :

signal en formation.

Si le dataset replay possède des ticks/subbars :

utiliser les données disponibles.

Ne pas simuler Ninja uniquement à la clôture.

======================================================================
33. STRATEGY TESTER + LUCIEN
======================================================================

Lucien :

signal à clôture.

Ne jamais faire apparaître un trade Lucien avant clôture.

======================================================================
34. STRATEGY TESTER RULE BUILDER
======================================================================

Le Strategy Tester doit permettre de choisir :

Strategy

CALL Rules

PUT Rules

Expiration

Candles Validation

La logique doit être la même que Auto Trade.

NE PAS maintenir deux systèmes de règles différents.

======================================================================
35. EXPIRATION
======================================================================

Lorsque :

expirationMode = candles

alors :

expiryIndex =
entryIndex + expiryCandles

Exemple :

entry = 100
expiryCandles = 3

expiry = 103

Aucune conversion silencieuse.

======================================================================
36. REMAINING TIME
======================================================================

Conserver :

Remaining Time Before Candle Closure

Ne pas le supprimer.

Ne pas le remplacer par expiration fixe.

======================================================================
37. CANDLES VALIDATION
======================================================================

Conserver :

Candles Validation

RGR
GR
RG
etc.

La bougie en formation ne doit pas être rétroactivement considérée comme clôturée.

======================================================================
38. CISD GUARD
======================================================================

Conserver le CISD Guard existant.

Ne pas créer un deuxième système.

Ne pas appliquer le CISD Guard automatiquement aux Candle Patterns.

======================================================================
39. STRATEGY TESTER STATS
======================================================================

Afficher clairement :

Start balance
Balance
Available
Net P&L
Win rate
Profit factor
Max DD
Trades

Les chiffres doivent être nettement visibles.

Utiliser une grille responsive.

Pas de micro-texte.

======================================================================
40. TRADE DETAILS
======================================================================

Chaque trade doit afficher :

Strategy
CALL / PUT
Rule
Conditions
Entry
Exit
Expiration
Result
P&L

======================================================================
41. SUPPRESSION DES PANNEAUX MARQUÉS X
======================================================================

Dans la capture de référence utilisateur, les blocs suivants sont barrés :

« Vérification CISD — étapes optionnelles »

et

« Confirmation bougie précédente »

Ces blocs doivent être supprimés de l’interface utilisateur.

IMPORTANT :

Si leurs données sont utilisées en interne :

conserver uniquement la logique backend nécessaire.

Mais NE PLUS AFFICHER ces panneaux dans l’UI.

======================================================================
42. DISPLAY SETTINGS
======================================================================

Les filtres doivent être persistants.

Ne pas perdre les préférences après reload.

Stocker :

showLabels
+
displayFilters
+
labelSize

et les préférences par stratégie si nécessaire.

======================================================================
43. DISPLAY ≠ TRADING
======================================================================

Exemple :

Hammer OFF

Le graphique ne montre pas Hammer.

MAIS :

CALL rule :

BOS Up
+
Hammer

doit continuer à fonctionner.

C’est obligatoire.

======================================================================
44. PERFORMANCE LIGHTWEIGHT CHARTS
======================================================================

NE PAS :

- recréer tous les labels à chaque tick ;
- recréer tous les événements à chaque tick ;
- recalculer tout l’historique à chaque render ;
- créer un nouveau label pour chaque tick Ninja.

Utiliser :

- stable event IDs
- cache
- diff
- object reuse
- incremental render
- viewport filtering

La détection reste complète.

Le rendu doit être limité au viewport.

======================================================================
45. LIVE LABEL
======================================================================

Pour Ninja :

les événements en formation peuvent avoir :

LIVE

Exemple :

LIVE · Bullish Engulfing

Mais :

LIVE n’autorise pas la fusion de plusieurs patterns.

Si trois patterns sont actifs :

3 labels LIVE séparés.

======================================================================
46. COULEURS
======================================================================

Palette professionnelle.

Bullish :

vert professionnel

Bearish :

rouge professionnel

Neutral :

gris/slate

ICT :

bleu / teal / violet selon catégorie

Pas d’orange agressif partout.

======================================================================
47. SMA / EMA / RSI / MACD
======================================================================

INTERDIT d’ajouter :

EMA
SMA
RSI
MACD
Oscillateur

à quelque niveau que ce soit :

- UI
- Event Engine
- Strategy Engine
- Rule Engine

SAUF si une formule existe DÉJÀ dans la source officielle du pattern et qu’elle est strictement nécessaire à son implémentation originale.

IMPORTANT :

Ne jamais ajouter volontairement une SMA ou EMA pour déterminer une tendance si ce n’est pas défini dans la source.

======================================================================
48. KILLZONES
======================================================================

Les Killzones ont été volontairement supprimées.

NE PAS les réintroduire.

======================================================================
49. UN SEUL MAIN
======================================================================

Le projet final doit conserver UNE SEULE entrée principale adaptée à son architecture.

NE PAS créer :

Main.pine
Main_Candle.pine
Main_ICT.pine

comme trois versions concurrentes.

Intégrer les fonctionnalités dans le Main approprié du projet cible.

======================================================================
50. TEST EXACT DES 73 PATTERNS
======================================================================

Créer un test automatique.

source = super_candles.zip

target = integrated engine

Vérifier :

73 / 73

Pour chaque pattern :

patternId identique
label identique
direction cohérente
détecteur présent

======================================================================
51. TEST MULTI-PATTERN
======================================================================

Scénario :

Doji
+
Spinning Top

Résultat :

2 événements.

Pas 1.

Scénario :

Hammer
+
Bullish Engulfing
+
Piercing

Résultat :

3 événements.

Pas 1.

======================================================================
52. TEST IDENTITÉ
======================================================================

Vérifier :

Bullish Engulfing

affichage exact :

Bullish Engulfing

et NON :

ENGULFING

Même test pour les 73.

======================================================================
53. TEST ICT
======================================================================

Vérifier que les nouveaux ICT ne sont pas seulement présents dans un registry.

Pour chaque :

BISI
SIBI
OB
Breaker
MB
Po3
SMT
etc.

vérifier :

registry
+
detector
+
event
+
Rule Engine
+
display filter

======================================================================
54. TEST ZOOM
======================================================================

Automatiser :

viewport 1
viewport 2
viewport 3

et :

zoom
pan

Vérifier que le même événement reste sur la même bougie.

======================================================================
55. TEST COLLISION
======================================================================

Créer au moins 10 événements sur 4 bougies.

Vérifier :

aucun rectangle ne chevauche un autre.

Chaque texte reste lisible.

======================================================================
56. TEST DÉDUPLICATION
======================================================================

Même :

BOS Down

sur même :

referenceSwing
+
candleTime

Résultat :

1 événement.

Même :

Hammer

sur même bougie :

1 événement.

Un nouveau Hammer sur une nouvelle bougie :

nouvel événement.

======================================================================
57. TEST DISPLAY FILTER
======================================================================

Tags OFF :

aucun tag.

Tags ON :

tags sélectionnés.

Hammer OFF :

Hammer invisible.

Bullish Engulfing ON :

visible.

Mais :

les deux événements restent présents dans le moteur.

======================================================================
58. TEST RULE ENGINE
======================================================================

CALL :

BOS Up
+
Bullish Engulfing

BOS Up seul :

HOLD.

Bullish Engulfing seul :

HOLD.

Les deux :

CALL.

PUT :

BOS Down
+
Bearish Engulfing

même logique.

======================================================================
59. TEST EXPIRATION
======================================================================

Tester :

1 candle
2 candles
3 candles
5 candles
10 candles

CALL et PUT.

Vérifier :

expiryIndex =
entryIndex + expiryCandles

======================================================================
60. TEST NINJA
======================================================================

Vérifier :

Ninja

signal en formation.

Candles Validation :

bougies clôturées.

======================================================================
61. TEST LUCIEN
======================================================================

Vérifier :

Lucien

signal à clôture.

======================================================================
62. TEST STRATEGY TESTER
======================================================================

Tester :

L_Lucien
+
Ninja

avec :

1 candle
3 candles
5 candles

Les résultats doivent utiliser la même logique de Rule Engine.

======================================================================
63. TEST REGRESSION
======================================================================

Tous les tests déjà présents dans le projet doivent continuer de passer.

Notamment :

BOS
CHoCH
CISD
Candles Validation
CISD Guard
Ninja
Lucien
Replay
Expiry
Payout
WIN
LOSS
TIE
Money Management

======================================================================
64. AUDIT AVANT LIVRAISON
======================================================================

Avant de livrer :

rechercher explicitement dans le code les anti-patterns suivants :

join(' · ')
shortCandleLabel
future(...)
available:false
group events same candle
badge multi-pattern
hardcoded pixel coordinates
fixed x/y labels
tiny marker
concat candle names
SMA ajouté
EMA ajouté

Toute occurrence problématique doit être corrigée.

======================================================================
65. LIVRABLE FINAL
======================================================================

Fournir :

1. ZIP complet.

2. Liste des fichiers modifiés.

3. Liste des fichiers ajoutés.

4. Registry final des 73 Candle Patterns.

5. Tableau :
Source Pattern → Integrated Pattern.

6. Résultat des tests.

7. Résultat du build.

8. Résultat lint.

9. Résultat tests unitaires.

10. Résultat tests intégration.

11. Résultat tests E2E.

12. Éventuels problèmes restants.

======================================================================
66. RÈGLE DE VÉRACITÉ
======================================================================

NE JAMAIS écrire :

« compile OK »

si le compilateur n’a pas réellement été exécuté.

NE JAMAIS écrire :

« tests OK »

si les tests n’ont pas réellement été exécutés.

NE JAMAIS déclarer :

« les 73 patterns sont intégrés »

sans avoir comparé les 73 IDs source avec les 73 IDs intégrés.

======================================================================
67. RÉSULTAT VISUEL ATTENDU
======================================================================

Le graphique doit respecter cette philosophie :

PRIX
↓
STRUCTURE
↓
SETUP
↓
CANDLE PATTERN

mais chaque élément reste INDÉPENDANT.

Exemple :

BOS Down

Bearish Engulfing

Shooting Star

Doji

HH

chaque élément possède :

- son propre label ;
- son propre ancrage ;
- sa propre position ;
- son propre texte ;
- sa propre visibilité.

Aucune fusion.

Aucune concaténation.

Aucun flottement au zoom.

Aucun déplacement arbitraire.

======================================================================
68. CE QU’IL NE FAUT SURTOUT PLUS FAIRE
======================================================================

NE PAS reproduire les erreurs vues dans pine_v6_engine_v26_73_candle_patterns.zip :

- fusion de plusieurs patterns ;
- labels du type « DOJI · SPINNING TOP » ;
- labels raccourcis ;
- modification du nom source ;
- labels qui se déplacent au zoom ;
- tags qui changent de disposition ;
- renderer commun qui détruit le placement historique BOS/CHoCH/CISD ;
- absence de Very Tiny / Tiny ;
- patterns inventés ;
- registry de signaux ICT non implémentés ;
- panneaux UI que l’utilisateur a demandé de retirer ;
- ajout caché d’indicateurs classiques.

======================================================================
69. ARCHITECTURE CIBLE
======================================================================

             SHARED EVENT ENGINE
                      |
          +-----------+-----------+
          |                       |
       ICT EVENTS            73 CANDLES
          |                       |
          +-----------+-----------+
                      |
                SIGNAL REGISTRY
                      |
                  RULE ENGINE
                      |
          +-----------+-----------+
          |                       |
        NINJA                  L_LUCIEN
     FORMING CANDLE          CLOSED CANDLE
          |                       |
          +-----------+-----------+
                      |
             AUTO TRADE / TESTER
                      |
                DISPLAY ENGINE
                      |
             LIGHTWEIGHT CHARTS

DISPLAY ENGINE :

NE CHANGE PAS LES ÉVÉNEMENTS.

NE CHANGE PAS LEUR NOM.

NE LES FUSIONNE PAS.

NE LES SUPPRIME PAS.

Il ne fait que :

FILTER
ANCHOR
COLLISION
LAYOUT
RENDER

======================================================================
70. CRITÈRE FINAL ABSOLU
======================================================================

Le projet final doit simultanément satisfaire :

[OK] 73 Candle Patterns exacts de super_candles.zip
[OK] aucun pattern inventé
[OK] aucun pattern fusionné
[OK] aucun nom raccourci
[OK] 1 pattern = 1 événement
[OK] 1 pattern = 1 label
[OK] labels ancrés aux bougies
[OK] zoom/pan stable
[OK] collision-free
[OK] Very Tiny
[OK] Tiny
[OK] Small
[OK] Normal
[OK] Large
[OK] Huge

[OK] BOS/CHoCH/CISD conservés
[OK] disposition historique conservée
[OK] ICT signals réellement détectés
[OK] ICT signals utilisables dans Rule Builder

[OK] Ninja ProTrader conservé
[OK] L_Lucien ProTrader conservé
[OK] Auto Trade partagé
[OK] Strategy Tester partagé

[OK] CALL personnalisable
[OK] PUT personnalisable
[OK] AND réel
[OK] HOLD en conflit

[OK] expiration en bougies
[OK] expiration secondes compatible
[OK] remaining time conservé

[OK] 8 statistiques visibles
[OK] Start balance
[OK] Balance
[OK] Available
[OK] Net P&L
[OK] Win rate
[OK] Profit factor
[OK] Max DD
[OK] Trades

[OK] Tags & labels master switch
[OK] filtres individuels
[OK] détection indépendante de l’affichage

[OK] panneaux marqués X retirés
[OK] aucune Killzone
[OK] aucune EMA
[OK] aucune SMA ajoutée
[OK] aucun RSI
[OK] aucun MACD
[OK] aucun oscillateur

======================================================================
71. ORDRE D’EXÉCUTION OBLIGATOIRE
======================================================================

ÉTAPE 1 :
AUDITER LE PROJET CIBLE.

ÉTAPE 2 :
AUDITER super_candles.zip.

ÉTAPE 3 :
AUDITER v26 ET IDENTIFIER CHAQUE RÉGRESSION.

ÉTAPE 4 :
CRÉER LE REGISTRY EXACT.

ÉTAPE 5 :
INTÉGRER LES 73 PATTERNS SANS MODIFIER LEUR IDENTITÉ.

ÉTAPE 6 :
INTÉGRER ICT EVENTS RÉELLEMENT DÉTECTÉS.

ÉTAPE 7 :
CONNECTER LE RULE ENGINE.

ÉTAPE 8 :
CONNECTER NINJA.

ÉTAPE 9 :
CONNECTER L_LUCIEN.

ÉTAPE 10 :
CONNECTER STRATEGY TESTER.

ÉTAPE 11 :
AJOUTER EXPIRATION EN BOUGIES.

ÉTAPE 12 :
RÉPARER L’OVERLAY.

ÉTAPE 13 :
RÉTABLIR LE PLACEMENT HISTORIQUE BOS/CHoCH/CISD.

ÉTAPE 14 :
IMPLÉMENTER LE COLLISION MANAGER.

ÉTAPE 15 :
AJOUTER FILTRES INDIVIDUELS.

ÉTAPE 16 :
SUPPRIMER LES PANNEAUX BARRÉS.

ÉTAPE 17 :
TESTER ZOOM/PAN.

ÉTAPE 18 :
TESTER DÉDUPLICATION.

ÉTAPE 19 :
TESTER LES 73 PATTERNS.

ÉTAPE 20 :
BUILD + LINT + TESTS.

ÉTAPE 21 :
SEULEMENT APRÈS CES VALIDATIONS :
LIVRER LE ZIP.

======================================================================
RÈGLE FINALE
======================================================================

NE CHERCHE PAS À FAIRE PLUS.

CHERCHE À FAIRE EXACTEMENT CE QUI EST DEMANDÉ.

LE MOTEUR PEUT DÉTECTER BEAUCOUP DE CHOSES.

LE GRAPHIQUE DOIT RESTER PROPRE.

LA SOURCE CANDLE EST SACRÉE.

LES 73 PATTERNS DOIVENT ÊTRE IDENTIQUES À super_candles.zip.

CHAQUE PATTERN RESTE INDIVIDUEL.

CHAQUE LABEL RESTE INDIVIDUEL.

LES LABELS RESTENT ATTACHÉS AUX BOUGIES.

BOS / CHoCH / CISD NE DOIVENT PAS ÊTRE DÉGRADÉS.

NINJA ≠ LUCIEN.

DISPLAY ≠ TRADING.

DETECTION ≠ DISPLAY.

TESTER ≠ UNE VERSION SIMPLIFIÉE DU MOTEUR.

PAS DE PATCH SUPERFICIEL.

PAS DE FAUX REGISTRY.

PAS DE CONCATÉNATION.

PAS DE LABELS FLOTTANTS.

PAS DE PATTERNS INVENTÉS.

PAS DE RÉGRESSION.

LE LIVRABLE DOIT ÊTRE PROPRE, DÉTERMINISTE, MAINTENABLE ET PROFESSIONNEL.