# FE-Engineering-Guidelines ver2024

## [코드 스타일 가이드 by 타입스크립트](https://github.ncsoft.com/ziziana0507/MobileServiceTeam-Engineering-Guidelines/blob/main/typescript.md)

## [React 컴포넌트 작성 가이드](https://github.ncsoft.com/ziziana0507/MobileServiceTeam-Engineering-Guidelines/blob/main/react.md)

## [좋은 코드 작성 규칙](https://github.ncsoft.com/ziziana0507/MobileServiceTeam-Engineering-Guidelines/blob/main/code.md)

## EsLint 규칙

```js
{
  rules: {
    'no-case-declarations': 'off',
    'no-use-before-define': 'off',
    'no-unused-expressions': 'off',
    'react-hooks/exhaustive-deps': 'warn',
    'react/display-name': 'off',
  },
}
```

## Prettier 규칙

```js
module.exports = {
  arrowParens: "avoid",
  tabWidth: 2,
  printWidth: 80,
  useTabs: false,
  semi: true,
  quoteProps: "consistent",
  bracketSameLine: true,
  bracketSpacing: true,
  singleQuote: true,
  trailingComma: "all",
  endOfLine: "auto",
};
```
