# OK Groot - Custom Wake Word Model

![Status](https://img.shields.io/badge/status-experimental-orange)
![Language](https://img.shields.io/badge/language-french-blue)
![ESPHome](https://img.shields.io/badge/ESPHome-2024.7.0+-green)

## 📋 Description

**OK Groot** est un wake word personnalisé entraîné avec [microWakeWord](https://github.com/kahrendt/microWakeWord) pour être utilisé avec ESPHome et Home Assistant.

⚠️ **Version expérimentale** - Ce modèle est en phase de test et peut nécessiter des ajustements.

## 🎯 Caractéristiques

- **Wake word**: "OK Groot"
- **Langue**: Français
- **Taille du modèle**: 59.45 KB
- **Architecture**: MixedNet streaming
- **Échantillons d'entraînement**: 100 enregistrements vocaux

## 📊 Métriques d'entraînement

- **Accuracy**: ~99%
- **Recall**: ~98%
- **Precision**: ~89%
- **Training steps**: 10,000

## 🚀 Installation

### Configuration ESPHome

Ajoutez ceci à votre fichier YAML ESPHome :

```yaml
micro_wake_word:
  models:
    - https://raw.githubusercontent.com/Raphdeumax/wake-word-models/main/ok_groot.json
  on_wake_word:
    then:
      - voice_assistant.start:
```

### Flasher sur ESP32

```bash
esphome run votre-esp-assistant.yaml
```

## ⚙️ Paramètres

Les paramètres actuels sont optimisés pour éviter les faux positifs :

| Paramètre | Valeur | Description |
|-----------|--------|-------------|
| `probability_cutoff` | 0.85 | Seuil de détection (0.0-1.0) |
| `sliding_window_size` | 5 | Taille de la fenêtre de lissage |
| `tensor_arena_size` | 37000 | Mémoire allouée sur ESP32 |

### Ajustements

Si le modèle ne se déclenche **pas assez** :
- Réduire `probability_cutoff` à `0.75` ou `0.65`

Si le modèle se déclenche **trop souvent** (faux positifs) :
- Augmenter `probability_cutoff` à `0.90` ou `0.95`

## 🛠️ Configuration matérielle requise

- ESP32-S3 (recommandé) ou ESP32
- Microphone I2S
- ESPHome 2024.7.0 ou supérieur

## 📝 Notes de version

### Version 1.0 (Expérimentale)

- Première version de test
- 100 échantillons d'entraînement en français
- Paramètres optimisés pour la détection stricte
- Nécessite des tests en conditions réelles

## 🔗 Liens utiles

- [Repository GitHub](https://github.com/Raphdeumax/wake-word-models)
- [microWakeWord](https://github.com/kahrendt/microWakeWord)
- [ESPHome Voice Assistant](https://esphome.io/components/voice_assistant.html)

## 📄 Licence

Ce modèle est fourni "tel quel" à des fins de test et d'expérimentation personnelle.

## 🙏 Remerciements

- Kevin Ahrendt pour [microWakeWord](https://github.com/kahrendt/microWakeWord)
- La communauté ESPHome et Home Assistant

---

**Auteur**: Raphdeumax  
**Date**: Décembre 2025  
**Statut**: Expérimental ⚠️
