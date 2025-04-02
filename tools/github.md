# GitHub

GitHub hosting for Git repositories with collaboration features.

## Pull Requests
1. Create branch
2. Make changes
3. Push to GitHub
4. Open Pull Request
5. Review and merge

## Actions
```yaml
name: CI
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm test
```
