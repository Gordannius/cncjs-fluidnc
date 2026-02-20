---
id: cncjs-i18n-updates
trigger: when adding or modifying UI text
confidence: 0.88
domain: internationalization
source: local-repo-analysis
priority: high
analyzed_commits: 200
---

# Update i18n Files When Adding UI Text

## Action

When adding or modifying user-facing text in the UI, update the internationalization files in `src/app/i18n/`.

**Pattern:**

1. Add the English translation to `src/app/i18n/en/resource.json`
2. Consider updating other language files (15+ languages supported)
3. Use scope `(l10n)` or `(i18n)` in commit message

**Supported languages:**

- `en` (English) - primary/required
- `zh-cn` (Simplified Chinese)
- `zh-tw` (Traditional Chinese)
- `ja` (Japanese)
- `es` (Spanish)
- `fr` (French)
- `de` (German)
- `it` (Italian)
- `pt-br` (Brazilian Portuguese)
- `ru` (Russian)
- `tr` (Turkish)
- `nl` (Dutch)
- `hu` (Hungarian)
- `cs` (Czech)
- `uk` (Ukrainian)

## Evidence

i18n files are frequently updated together:

- `src/app/i18n/nl/resource.json` - 12 commits
- `src/app/i18n/zh-tw/resource.json` - 11 commits
- `src/app/i18n/zh-cn/resource.json` - 11 commits
- `src/app/i18n/ja/resource.json` - 11 commits
- `src/app/i18n/es/resource.json` - 11 commits
- `src/app/i18n/tr/resource.json` - 10 commits
- ...and more

Recent i18n commits:

```
feat(l10n): update Spanish translation (#900)
feat(l10n): upgrade `i18next-scanner` and refresh translations (#884)
```

## Workflow

1. **Add text to component:**

```jsx
import { Trans } from 'react-i18next';

<Trans i18nKey="widget.axes.jogSpeed">Jog Speed</Trans>
```

2. **Add to `src/app/i18n/en/resource.json`:**

```json
{
  "widget": {
    "axes": {
      "jogSpeed": "Jog Speed"
    }
  }
}
```

3. **Run i18n linter:**

```bash
yarn i18nlint
```

4. **Consider updating other languages** (or leave placeholder for translators)

## Note

- The project has a dedicated i18n linter: `yarn i18nlint`
- Run `yarn lint` before committing to catch JSON syntax errors
- Batch i18n updates are common (update multiple languages in one commit)
