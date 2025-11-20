# Décision de promotion — TP MLflow (CV YOLO Tiny)

## Objectifs et contraintes
- Objectif principal : maximiser mAP et recall pour la détection de personnes.  
- Contraintes : latence faible pour traitement rapide, coût énergétique limité, stabilité inter-seed.

## Candidat promu
- Run name / ID : yolov8n_e5_sz416_lr0.01_s42 (Run 2)  
- Paramètres clés : epochs=5, imgsz=416, lr0=0.01, seed=42  
- Métriques : mAP@50=0.3059, mAP50-95=0.2699, Precision=0.0080, Recall=0.7742

## Comparaison (résumé)
- Alternative A (Run 1 : baseline) :  
  - POUR : rapide, faible coût, simplicité  
  - CONTRE : mAP et recall plus faibles, risque de mauvaise détection
- Alternative B (Run 2 : candidat) :  
  - POUR : meilleure recall et mAP, meilleure performance globale  
  - CONTRE : temps d’entraînement légèrement plus long, coût un peu plus élevé  
- Observations : Run 2 est plus performant et stable sur les métriques clés malgré un léger compromis sur la latence.
- | Critère              | Run 1 (baseline)            | Run 2 (candidat)            |
|----------------------|----------------------------|----------------------------|
| mAP@50               | 0.275                       | 0.306                     |
| mAP50-95             | 0.231                       | 0.270                     |
| Recall               | 0.710                       | 0.774                     |
| Precision            | 0.00836                     | 0.00800                   |
| Temps / Latence      | rapide                      | un peu plus lent          |
| Complexité / coût    | faible                      | moyen                     |

## Risques et mitigations
- Risque 1 : augmentation du temps d’inférence → Mitigation : tester sur batch réel, optimiser batch size si nécessaire  
- Risque 2 : coût computationnel plus élevé → Mitigation : valider sur subset de production, puis promotion graduelle

## Décision
- Promouvoir : Oui, Run 2 est choisi pour Staging, puis Production après validation.  
- Étapes suivantes :  
  1. Enregistrer le modèle dans le Model Registry (Stage : Staging)  
  2. Tester sur un dataset de production limité (Canary test)  
  3. Si performance stable, promotion vers Production
