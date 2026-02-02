# Sequential SMS n8n Workflow

**Project:** Sequential SMS Dispatch via Line-Break Parsing
**Started:** 2026-02-02
**Status:** 🚧 In Progress
**GitHub Issue:** #1

---

## Description

Crée un workflow n8n qui:
- Prend des réponses AI avec des line breaks intentionnels
- Parse chaque ligne séparément
- Envoie chaque ligne comme SMS distinct via Twilio
- Avec delay configurable entre chaque SMS

## Spécification

```
AI Output → Split by Line Breaks → Remove Empty Lines → Loop (1 msg) → Delay → Send SMS
```

## Input Example

```text
Bonjour! 👋
Merci pour votre message.

Nous allons traiter votre demande.
Un conseiller vous contactera sous 24h.

Bonne journée! 😊
```

## Expected Output

```
SMS 1: Bonjour! 👋
SMS 2: Merci pour votre message.
SMS 3: Nous allons traiter votre demande.
SMS 4: Un conseiller vous contactera sous 24h.
SMS 5: Bonne journée! 😊
```

## Tasks

- [ ] Créer la structure du projet
- [ ] Créer le workflow JSON n8n
- [ ] Créer documentation SETUP.md
- [ ] Créer test example (test-example.json)
- [ ] Créer RALPH_DONE.md
- [ ] Commit et push vers GitHub