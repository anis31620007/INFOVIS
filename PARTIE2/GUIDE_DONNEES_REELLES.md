# 🏆 Guide des Données Réelles World Cup

## 📊 Données Utilisées

Les exercices 3 et 4 utilisent maintenant les **vraies données** du réseau de football international provenant du site http://vlado.fmf.uni-lj.si/pub/networks/data/sport/football.htm

## 🌍 Contenu du Dataset

### Pays (35 nations)

| Code | Pays | Région |
|------|------|---------|
| ARG | Argentina | Amérique du Sud |
| AUT | Austria | Europe de l'Ouest |
| BEL | Belgium | Europe de l'Ouest |
| BGR | Bulgaria | Europe de l'Est |
| BRA | Brazil | Amérique du Sud |
| CHE | Switzerland | Europe de l'Ouest |
| CHL | Chile | Amérique du Sud |
| CMR | Cameroon | Afrique |
| COL | Colombia | Amérique du Sud |
| DEU | Germany | Europe de l'Ouest |
| DNK | Denmark | Europe du Nord |
| ESP | Spain | Europe de l'Ouest |
| FRA | France | Europe de l'Ouest |
| GBR | England | Europe du Nord |
| GRE | Greece | Europe de l'Est |
| HRV | Croatia | Europe de l'Est |
| IRN | Iran | Asie |
| ITA | Italy | Europe de l'Ouest |
| JAM | Jamaica | Afrique |
| JPN | Japan | Asie |
| KOR | South Korea | Asie |
| MAR | Morocco | Afrique |
| MEX | Mexico | Amérique du Sud |
| NGA | Nigeria | Afrique |
| NLD | Netherlands | Europe de l'Ouest |
| NOR | Norway | Europe du Nord |
| PRT | Portugal | Europe de l'Ouest |
| PRY | Paraguay | Amérique du Sud |
| ROM | Romania | Europe de l'Est |
| SCO | Scotland | Europe du Nord |
| TUN | Tunisia | Afrique |
| TUR | Turkey | Europe de l'Est |
| USA | USA | Amérique du Sud |
| YUG | Yugoslavia | Europe de l'Est |
| ZAF | South Africa | Afrique |

### Régions/Groupes

1. **Groupe 1** (Rouge) - Amérique du Sud : ARG, BRA, CHL, COL, MEX, PRY, USA
2. **Groupe 2** (Bleu) - Europe de l'Ouest : AUT, BEL, CHE, DEU, ESP, FRA, ITA, NLD, PRT
3. **Groupe 3** (Orange) - Europe de l'Est : BGR, GRE, HRV, ROM, TUR, YUG
4. **Groupe 4** (Vert) - Afrique : CMR, JAM, MAR, NGA, TUN, ZAF
5. **Groupe 5** (Violet) - Europe du Nord : DNK, GBR, NOR, SCO
6. **Groupe 6** (Cyan) - Asie : IRN, JPN, KOR

## 📈 Statistiques du Réseau

- **Total de pays** : 35
- **Total de connexions** : 118 liens
- **Total de matchs** : 277 matchs historiques
- **Pays le plus connecté** : À découvrir dans le graphe !
- **Connexion la plus forte** : Paraguay-Brazil (10 matchs), Norway-England (12 matchs)

## 🔍 Analyse du Format Original (Pajek)

### Format Source
```
*Vertices     35
  1 "ARG"    0.3784 0.7257 0.5
  ...
*Arcs
  1 12   4    # ARG -> ESP (4 matchs)
  ...
```

### Conversion en JSON
Le format Pajek a été converti en JSON D3.js avec :
- **Vertices** → **nodes** avec id, name, fullName, group
- **Arcs** → **links** avec source, target, value
- **Indices** : Pajek commence à 1, JSON commence à 0 (converti automatiquement)

## 🎯 Points d'Intérêt dans le Graphe

### Rivalités Historiques
- **Argentina vs Italy** : 9 matchs (lien le plus fort)
- **Paraguay vs Brazil** : 10 matchs
- **Norway vs England** : 12 matchs (record!)
- **Yugoslavia vs Spain** : 9 matchs

### Pays Centraux (Hub)
Les pays avec le plus de connexions :
1. **Germany (DEU)** : Centre de l'Europe
2. **Spain (ESP)** : Hub méditerranéen
3. **England (GBR)** : Hub nord-européen
4. **Italy (ITA)** : Pont sud-européen

### Pays Périphériques
Pays avec peu de connexions :
- Iran (IRN) : Seulement 1 connexion (Germany)
- Greece (GRE) : 2 connexions
- Jamaica (JAM) : 1 connexion (England)

## 💡 Insights Visuels

### Dans l'Exercice 3
- **Taille des nœuds** = Nombre de connexions
- **Épaisseur des liens** = Nombre de matchs joués
- **Couleur** = Région géographique
- **Clusters** = Proximité régionale et historique

### Dans l'Exercice 4 (Fish Eye)
- **Zoom dynamique** : Approchez la souris pour voir les détails
- **Nœuds fixes** (rouges) : Pays que vous avez déplacés
- **Contrôles** : Ajustez le rayon et la distorsion du Fish Eye

## 🛠️ Comment Utiliser Vos Propres Données

### 1. Format JSON Requis
```json
{
  "nodes": [
    {"id": 0, "name": "CODE", "fullName": "Full Name", "group": 1}
  ],
  "links": [
    {"source": 0, "target": 1, "value": 5}
  ]
}
```

### 2. Remplacer les Données
Dans `exercice3.html` ou `exercice4.html`, trouvez la variable `footballData` et remplacez-la par vos données.

### 3. Charger depuis un Fichier
```javascript
// Au lieu de var footballData = {...}
d3.json("football_data.json", function(error, data) {
    if (error) throw error;
    
    footballData = data;
    
    // Reste du code...
    force.nodes(footballData.nodes)
        .links(footballData.links)
        .start();
});
```

## 🔄 Conversion Pajek → JSON

### Script de Conversion (Python)
```python
def pajek_to_json(pajek_file):
    nodes = []
    links = []
    
    with open(pajek_file, 'r') as f:
        lines = f.readlines()
        
    mode = None
    for line in lines:
        if line.startswith('*Vertices'):
            mode = 'vertices'
            continue
        elif line.startswith('*Arcs'):
            mode = 'arcs'
            continue
        elif line.startswith('*Edges'):
            break
            
        if mode == 'vertices' and line.strip():
            parts = line.strip().split()
            node_id = int(parts[0]) - 1  # Pajek starts at 1
            name = parts[1].strip('"')
            nodes.append({
                'id': node_id,
                'name': name,
                'fullName': get_full_name(name),
                'group': assign_group(name)
            })
            
        elif mode == 'arcs' and line.strip():
            parts = line.strip().split()
            source = int(parts[0]) - 1
            target = int(parts[1]) - 1
            value = int(parts[2])
            links.append({
                'source': source,
                'target': target,
                'value': value
            })
    
    return {'nodes': nodes, 'links': links}
```

## 📚 Références

- **Source originale** : http://vlado.fmf.uni-lj.si/pub/networks/data/sport/football.htm
- **Format Pajek** : http://vlado.fmf.uni-lj.si/pub/networks/pajek/
- **D3.js Force Layout** : https://github.com/d3/d3-force
- **Observable HQ** : https://observablehq.com/@d3/force-directed-graph

## ✅ Validation des Données

### Vérifications Effectuées
- ✅ 35 nœuds chargés
- ✅ 118 liens créés
- ✅ Pas de liens auto-référents
- ✅ Tous les indices source/target valides
- ✅ Groupes assignés (1-6)
- ✅ Valeurs de matchs > 0

### Tests de Cohérence
```javascript
// Dans la console du navigateur
console.log("Nœuds:", footballData.nodes.length);
console.log("Liens:", footballData.links.length);
console.log("Total matchs:", 
    footballData.links.reduce((sum, l) => sum + l.value, 0));
```

## 🎓 Exercices Pédagogiques

### Questions d'Analyse
1. Quel pays a le plus de connexions ?
2. Quelle est la rivalité la plus forte (plus de matchs) ?
3. Quels pays forment des clusters géographiques ?
4. Y a-t-il des pays isolés ?

### Modifications Possibles
1. **Filtrer par région** : N'afficher qu'une région à la fois
2. **Seuil de matchs** : Ne montrer que les liens > X matchs
3. **Timeline** : Ajouter une dimension temporelle
4. **Statistiques dynamiques** : Calculer centralité, betweenness, etc.

---

**Créé pour le TP2 - InfoVis 2023**  
**Données : World Cup Football Network**  
**Format : Pajek → JSON D3.js**