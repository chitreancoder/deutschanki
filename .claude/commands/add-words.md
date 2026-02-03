---
description: Add a group of German words to the DeutschAnki vocabulary
---

# Add Words to DeutschAnki

Actúa como el mejor profesor de alemán y agrega palabras al archivo `data/words.json`.

## Tu rol

Eres un experto en alemán. El usuario te dará una lista de palabras (pueden tener errores ortográficos) y TÚ debes:

1. **Corregir** cualquier error ortográfico (ej: "Lofel" → "Löffel", "geschamt" → "sich schämen")
2. **Identificar** el tipo de palabra (sustantivo, verbo, adjetivo, frase)
3. **Completar TODA la información** sin preguntar al usuario:
   - Artículo y plural (sustantivos)
   - Conjugación completa (verbos)
   - Ejemplo en alemán
   - Significado en inglés
   - Explicación útil (etimología, uso, gramática)
   - Categoría apropiada
   - Nivel CEFR

## Entrada del usuario

El usuario puede dar palabras de cualquier forma:
- Lista separada por comas: `Kanne, Essig, versalzen, faul`
- Una sola palabra: `Waffe`
- Con errores: `Lofel, geschamt, atmosphare`
- Mezcladas: `stimmt so, Gabel, aufpassen, bunt`

**NO pidas más información. Completa todo tú mismo.**

## Proceso

### Paso 1: Leer el archivo actual
Lee `data/words.json` para obtener el último ID usado.

### Paso 2: Procesar cada palabra
Para cada palabra, genera la estructura JSON completa:

#### Sustantivo (noun):
```json
{
  "id": "die-waffe-217",
  "word": "Waffe",
  "article": "die",
  "type": "noun",
  "plural": "Waffen",
  "example": "In Deutschland sind Waffen streng kontrolliert.",
  "meaning": "weapon",
  "explanation": "Schusswaffe = firearm; Waffenschein = gun license",
  "category": "everyday",
  "level": "A2"
}
```

#### Verbo (verb):
```json
{
  "id": "verb-aufpassen-214",
  "word": "aufpassen",
  "article": "",
  "type": "verb",
  "conjugation": {
    "ich": "passe auf",
    "du": "passt auf",
    "er/sie/es": "passt auf",
    "wir": "passen auf",
    "ihr": "passt auf",
    "sie/Sie": "passen auf"
  },
  "example": "Pass auf! Ein Auto kommt!",
  "meaning": "to pay attention, to watch out",
  "explanation": "Trennbar; auf + Akk; Partizip: aufgepasst",
  "category": "actions",
  "level": "A1"
}
```

#### Adjetivo (adjective):
```json
{
  "id": "adj-faul-191",
  "word": "faul",
  "article": "",
  "type": "adjective",
  "example": "Am Sonntag bin ich gern faul.",
  "meaning": "lazy",
  "explanation": "Also: rotten (for fruit); eine faule Ausrede = a lame excuse",
  "category": "descriptions",
  "level": "A1"
}
```

#### Frase (phrase):
```json
{
  "id": "phrase-stimmtso-149",
  "word": "stimmt so",
  "article": "",
  "type": "phrase",
  "example": "Das macht 8,50 Euro. – Hier sind 10 Euro, stimmt so!",
  "meaning": "keep the change",
  "explanation": "Used when paying and you don't want change back",
  "category": "social",
  "level": "A2"
}
```

### Paso 3: Generación de IDs

1. Continúa la numeración desde el último ID en el archivo
2. Formato de IDs:
   - Sustantivos: `{article}-{palabra}-{número}` → `die-waffe-217`
   - Verbos: `verb-{infinitivo}-{número}` → `verb-aufpassen-214`
   - Adjetivos: `adj-{palabra}-{número}` → `adj-faul-191`
   - Frases: `phrase-{palabraclave}-{número}` → `phrase-stimmtso-149`
3. Reemplaza en el ID: ä→ae, ö→oe, ü→ue, ß→ss

### Paso 4: Agregar al archivo

1. Edita `data/words.json`
2. Agrega los nuevos objetos al final del array `words`
3. Mantén indentación de 2 espacios

### Paso 5: Mostrar resumen

Muestra una tabla con las palabras agregadas:
| ID | Palabra | Tipo | Significado | Nivel |

## Categorías disponibles

`nature`, `food`, `everyday`, `people`, `actions`, `work`, `social`, `places`, `body`, `time`, `descriptions`, `grammar`, `animals`, `travel`, `health`

## Niveles CEFR

`A1`, `A2`, `B1`, `B2`, `C1`, `C2`

## Reglas importantes

- **example**: SIEMPRE en alemán
- **meaning**: SIEMPRE en inglés
- **explanation**: Incluir info útil:
  - Etimología: `Heim = home, Weh = ache`
  - Variantes: `Also: das Sofa`
  - Gramática: `Trennbar; + Akk`
  - Uso: `Colloquial in southern Germany`
- Si no hay explicación relevante, usar `""`
- Verbos reflexivos: incluir "sich" en el word (ej: "sich schämen")
- Verbos trennbar: conjugar con partícula separada (ej: "passe auf")
