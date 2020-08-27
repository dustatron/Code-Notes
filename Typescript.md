## Tut

[Link](https://medium.com/javascript-in-plain-english/how-to-build-a-budget-app-with-react-typescript-web-storage-api-pt-1-433d72b72248)

```shell
npx create-react-app budget-app-ts --typescript
```



install two extra packages

```shell
npm install react-router-dom @types/react-router-dom

npm install shortid @types/shortid
```

## tsconfig

make sure you have  tsconfig.json file at the base of your project

```javascript
{
    "include": [
        "./src/*"
    ],
    "compilerOptions": {
        "lib": [
            "dom",
            "es2015"
        ],
        "jsx": "react",
        "target": "es5",
        "allowJs": true,
        "skipLibCheck": true,
        "esModuleInterop": true,
        "allowSyntheticDefaultImports": true,
        "strict": true,
        "forceConsistentCasingInFileNames": true,
        "module": "esnext",
        "moduleResolution": "node",
        "resolveJsonModule": true,
        "isolatedModules": true,
        "noEmit": true
    }
}
```



Project layout

```
budget-app-ts/
├─node_modules
├─public
│ ├─favicon.ico
│ ├─index.html
│ ├─manifest.json
│ └─robots.txt
├─src
│ ├─components
│ │ ├─item-item-add.tsx
│ │ ├─item-item.tsx
│ │ ├─item-list.tsx
│ │ ├─item-total.tsx
│ │ ├─icon-bin.tsx
│ │ └─icon-settings.tsx
│ ├─data
│ │ └─currency-codes.ts
│ ├─pages
│ │ └─home.tsx
│ │ └─settings.tsx
│ ├─styles
│ │ └─styles.css
│ ├─app-router.tsx
│ ├─index.tsx
│ ├─interfaces.ts
│ └─react-app-env.d.ts
├─ package.json
└─ tsconfig.json
```

