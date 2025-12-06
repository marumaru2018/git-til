Error: エラー内容: "Unexpected token '<', \"<!DOCTYPE \"... is not valid JSON"
at createConsoleError (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/next-devtools/shared/console-error.js:23:71)
at handleConsoleError (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/next-devtools/userspace/app/errors/use-error-handler.js:45:54)
at console.error (webpack-internal:///(app-pages-browser)/./node_modules/next/dist/next-devtools/userspace/app/errors/intercept-console-error.js:50:57)
at SearchResult.useMutation[mutation] [as onError] (webpack-internal:///(app-pages-browser)/./src/app/\_components/SearchResult.tsx:94:25)
at Mutation.execute (webpack-internal:///(app-pages-browser)/./node_modules/@tanstack/query-core/build/modern/mutation.js:136:37)

## 原因

応答が JSON 形式でない
