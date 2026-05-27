# Critical: Communication in TD

Nutze `td log <issue-id>` (bei TD-Worksessions: `td ws log`) während der Arbeit mit den entsprechenden Flags für relevante Fortschritte, Entscheidungen und Auffälligkeiten (decision, blocker, hypothesis, tried, result). Logge nicht nur “started” oder “done”, sondern konkret:
- welche Dateien/Module du geändert hast
- welche Tests/Checks du ausgeführt hast und mit welchem Ergebnis
- welche Akzeptanzkriterien erfüllt sind
- welche bewussten Einschränkungen, offenen Punkte oder Abweichungen vom Plan bestehen

## Kommunikation vor der Review

Wenn ein Akzeptanzkriterium nicht erfüllt ist oder du unsicher bist, reiche das Issue nicht zur Review ein, sondern dokumentiere den Restpunkt.

Der `td handoff` vor Review muss reviewer-tauglich sein:
- `--done`: konkret, was umgesetzt wurde
- `--remaining`: nichts / oder konkrete Restpunkte
- `--decision`: wichtige Architektur- oder Tooling-Entscheidungen
- `--uncertain`: Unsicherheiten, Risiken, nicht geprüfte Annahmen
- Verwende niemals generische Handoffs wie “Auto-generated for review submission”.
- Hast du mögliche Improvements außerhalb des Scopes des Issues gefunden (z.B. Performanceverbesserung, mögliches Refactoring, Verbesserung der Architektur)
    - Für jedes mögliche Improvement je ein `td log  <issue-id>`.
    - Die Log-Message beginnt mit "Possible new issue:"
    - Dahinter folgt deine Entscheidungsvorlage zur späteren Evaluierung, ob ein neues Issue angelegt wird.
