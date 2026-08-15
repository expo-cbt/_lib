# Software Maintenance

## Agile Workflows 🗣️

- How to pm, professional Certifications
  mgt meeting, Sprint planning, Time estimates, Board mgt ,workflow expectations
  1.Briefly tell us about your childhood, education and career, and ultimately how you entered into the space of Product Management?
  2.What is Product Management, and how does it differ from Project Management?
  3.Why is Product Management important?
  4.What are the traits of a world-class PM?
  5.What are the basic KPIs measured by a PM?
  6.Give us a brief walkthrough of “A typical day in Life of a PM”, from your POV?
  7.What are the key characteristics of a so-called “Agile environment”?
  8.What are Agile best practices for managing cross-functional teams?
  9.What are common misconceptions about Product Management?
  10.Describe a time you were assigned to manage a time-sensitive product launch with limited resources, and the strategies you implemented to achieve a favorable outcome?

#### Trivia Questions

TQ1. What do you do for fun?
TQ2. If given the opportunity and resources to choose a non-tech career path, what would it be, and why?
TQ3. In what way, shape or form has Artificial Intelligence (AI) influenced your lifestyle, job or business?
TQ4. Who drags fe or be

## Branch

- **feature/** — new feature — `feature/wallet-balance-toggle`
- **fix/** — bug fix — `fix/negative-amount-formatting`
- **chore/** — maintenance/tooling — `chore/update-expo-sdk`
- **refactor/** — code restructuring — `refactor/extract-transactions-hook`
- **hotfix/** — urgent production fix — `hotfix/crash-on-login`
- **release/** — release preparation — `release/v1.2.0`
- **docs/** — documentation — `docs/update-readme`

Convention: `type/short-kebab-case-description`, often prefixed with ticket ID if using issue tracking — e.g. `feature/PROJ-123-wallet-balance-toggle`.

## PR

- **feat** — new feature — `feat: add wallet balance visibility toggle`
- **fix** — bug fix — `fix: correct negative amount formatting`
- **chore** — maintenance/tooling, no functional change — `chore: update expo sdk to 52`
- **refactor** — code change that neither fixes a bug nor adds a feature — `refactor: extract useRecentTransactions hook`
- **docs** — documentation only — `docs: update readme setup instructions`
- **style** — formatting/whitespace, no logic change — `style: fix indentation in TransactionListItem`
- **test** — adding or fixing tests — `test: add unit tests for Transaction model`
- **perf** — performance improvement — `perf: memoize transformed transaction list`
- **build** — build system or external dependencies — `build: add babel plugin for reanimated`
- **ci** — CI/CD config changes — `ci: add github actions workflow for lint`
- **revert** — reverts a previous commit — `revert: revert "feat: add dark mode"`

## Changelog

**Keep a Changelog** convention — standard format for `CHANGELOG.md`:

```markdown
# Changelog

## [1.2.0] - 2026-08-14

### Added

- Wallet balance visibility toggle

### Changed

- Updated Expo SDK to 52

### Fixed

- Negative amount formatting on transaction list

### Removed

- Deprecated moment.js dependency

### Deprecated

- Old wallet card component (use WalletCard v2)

### Security

- Patched dependency vulnerability in xyz package
```

Categories: **Added**, **Changed**, **Fixed**, **Removed**, **Deprecated**, **Security** — grouped under a version + date heading, newest on top, unreleased changes go under an `## [Unreleased]` heading until versioned.
