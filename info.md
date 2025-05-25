name: Frontend CI

on:
  pull_request:
    branches: [main, dev]

jobs:
  lint-build-test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run Lint
        run: npm run lint

      - name: Run Type Check
        run: npm run type-check

      - name: Run Unit Tests
        run: npm test

      - name: Build project
        run: npm run build
