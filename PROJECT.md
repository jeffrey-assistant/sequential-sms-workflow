# Sequential SMS n8n Workflow

**Project:** Sequential SMS Dispatch via Line-Break Parsing
**Started:** 2026-02-02
**Status:** ✅ COMPLETE
**GitHub Issue:** [#1](https://github.com/jeffrey-assistant/sequential-sms-workflow/issues/1)
**GitHub Repo:** https://github.com/jeffrey-assistant/sequential-sms-workflow
**Local Commit:** b8102f0

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

- [x] Créer la structure du projet
- [x] Créer le workflow JSON n8n
- [x] Créer documentation SETUP.md
- [x] Créer test example (test-example.json)
- [x] Créer RALPH_DONE.md
- [x] Commit et push vers GitHub