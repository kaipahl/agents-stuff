# Definition of Done

- Jede Änderung an Templates, Partials oder Daten gilt erst als abgeschlossen, wenn das Durchbauen und die Tests ohne Fehler durchlaufen.
- Zu den Tests gehören auch, wenn für die Änderungen relevant, ESLint und/oder tsc (z.B. `npx tsc --noEmit prüfen`)
- Nie “fertig” melden ohne erfolgreichen Build.
- Jede Änderung am Styling oder class im Markup gilt erst als abgeschlossen, wenn die visuellen Regressionstests ohne Regressionen durchgelaufen sind. Nie “fertig” melden ohne erfolgreichen Regressionstest.
