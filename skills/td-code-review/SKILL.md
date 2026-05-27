---
name: td-code-review
description: Führe im Rahmen des TD-Workflows eine Code-Review der zur Review stehenden TD-Issues durch.
---
Ich will eine Code-Review nach TD – Task Management for AI Agents (**critical**: you must know the content of `td-task-management`). Es warten Issues auf eine Review.

See [td-implementation-standards.md](../td-shared/td-implementation-standards.md) for the implementation standards in TD-workflows.

Wenn du es für sinnvoll hältst, setze Subagenten ein:
- _Codebase Explorer_ für Code/Doku. Liest gezielt betroffene Dateien, Nachbarschaftscode und Doku/
  Plan, meldet nur belegte Risiken
- _Test Reviewer_ für Coverage. Prüft Acceptance Criteria gegen Tests, Randfälle, Regressionen und ob der richtige Check gelaufen ist.
- _Integration Reviewer_: nur bei größeren Tickets; schaut auf Persistenz/API/UI/Runner-
  Verkettung und mögliche Seiteneffekte
- **Du** integrierst und entscheidest.

## Bei Problemen

Bewerte ob die Probleme die du findest, nur theoretischer Natur sind. Wenn du keine Beweise für diese Probleme hast, dann ignoriere die theoretischen Probleme.

Wenn du Probleme findest, steht es dir frei, das Issue zu "rejecten". Wenn du die Umsetzungen als ausreichend bewertest, kannst du ein Approval geben.

## Mögliche Follow-Up-Issues

Wenn dir im Rahmen der Implementierung mögliche Improvements außerhalb des Scopes des Issues auffallen (Performanceverbesserung, mögliches Refactoring, Verbesserung der Architektur), dann mache für jedes mögliche Improvement am Issue je ein `td log`. Die Log-Message beginnt mit "Possible new issue:" und dahinter folgt deine Entscheidungsvorlage damit im Projekt später evaluiert werden kann, ob daraus ein neues Issue angelegt wird.

Am Ende der Code-Review wende den Skill `td-create-follow-up-issue <issue-id>` an.
