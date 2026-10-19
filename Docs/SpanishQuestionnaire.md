# Spanish HNAI prototype

Conciencia auditiva is the first home option. It loads the exact 22 supplied statements, with layout whitespace normalized, from Assets/_HearingNotion/Resources/Questionnaires/HNAI.es.json. Domains contain 9, 5 and 8 items.

Confirmed response scale:
1. Completamente en desacuerdo
2. Parcialmente en desacuerdo
3. Neutral
4. Parcialmente de acuerdo
5. Completamente de acuerdo

Choose one response per item. The selected option has a visible [X] and contrasting background. Siguiente requires an answer; Anterior permits revision. Finalizar appears at item 22 and requires all 22 responses. Completion shows an acknowledgement with an option to review responses. Home navigation preserves answers for the current visit; Reset visitor session clears all responses and completion state.

Responses are stored in a separate local prototype draft list with item ID, choice ID and UTC answer timestamp. Numeric values are defined by the questionnaire choices. They are not added to consented research assessment records, persisted, exported or scored. Full research administration and interpretation remain dependent on an approved protocol; protocolConfirmed stays false.

Verification: source compilation and JSON structure checks passed. In Unity Play Mode, verify answer selection, revision, disabled Next for unanswered items, final completion, navigation away/back, and reset. Inspect portrait and landscape wrapping. Play Mode verification has not been performed by the agent.
