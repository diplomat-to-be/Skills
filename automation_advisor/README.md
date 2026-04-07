# Automation Advisor

Скил для Claude Code. 10 вопросов → скоринг по 4 осям → вердикт (автоматизировать / подумать / оставить вручную) + расчет окупаемости из ваших реальных цифр.

## Установка

```bash
claude install-skill https://github.com/diplomat-to-be/automation-advisor/tree/main/skill
```

Или вручную:

```bash
mkdir -p ~/.claude/skills/automation-advisor/references
# скопируйте skill/SKILL.md → ~/.claude/skills/automation-advisor/SKILL.md
# скопируйте skill/references/scoring.md → ~/.claude/skills/automation-advisor/references/scoring.md
```

## Использование

В Claude Code:

```
/automation-advisor
```

Или просто опишите задачу:

> Каждый день трачу 20 минут на сверку балансов в таблице с данными на блокчейне. Стоит ли это автоматизировать?

## Что внутри

- **SKILL.md** — логика: 10 вопросов, фазы интервью, формулы, формат отчета
- **references/scoring.md** — таблицы баллов, модификаторы, формула окупаемости, дерево выбора подхода

## Автор

[AI ПАТЧ](https://t.me/AI_patching) — канал об автоматизации бизнеса с помощью AI
