Mettre en place un Linter et un Prettier [VSCODE]	

## Installation


Premierement il faut installer les extensions VSCode suivantes : 

Eslint | Rechercher ```dbaeumer.vscode-eslint```

Prettier | Rechercher ```esbenp.prettier-vscode```

Il faut ensuite installer les paquets suivants :

avec yarn :

```yarn add babel-eslint prettier-eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-react --dev```

ou npm : 

``` npm i babel-eslint prettier-eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-react --save-dev ```

Pour voir ce que font les packages en details:

[eslint](https://github.com/eslint/eslint)

[babel-eslint](https://github.com/babel/babel-eslint)

[prettier-eslint](https://github.com/prettier/prettier-eslint)

[eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)

[eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)

[eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react)

## Mise en place des fichier de configuration


Pour mettre en place les règles de linter et de prettier, il faudra mettre en place quelques fichiers de configuration.

Dans un premier temps, la mise en place d'eslint.

Elle se fait via le fichier ```.eslintrc.json``` que l'on place a la racine du projet.

.eslintrc.json : 

```json
{
  "parser": "babel-eslint",
  "plugins": ["prettier"],
  "extends": ["eslint:recommended", "plugin:react/recommended", "prettier"],
  "env": { "browser": true, "node": true, "jest": true },
  "rules": {
    "prettier/prettier": "warn",
       "no-unused-vars": 1,
        "react/react-in-jsx-scope": 0,
        "react/display-name":1,
        "react/jsx-key":1,
        "react/jsx-no-comment-textnodes":1,
        "react/jsx-no-duplicate-props":1,
        "react/jsx-no-target-blank":1,
        "react/jsx-no-undef":1,
        "react/jsx-uses-react":1,
        "react/jsx-uses-vars":1,
        "react/no-children-prop":1,
        "react/no-danger-with-children":1,
        "react/no-deprecated":1,
        "react/no-direct-mutation-state":1,
        "react/no-find-dom-node":1,
        "react/no-is-mounted":1,
        "react/no-render-return-value":1,
        "react/no-string-refs":1,
        "react/no-unescaped-entities":1,
        "react/no-unknown-property":1,
        "react/prop-types":1,
        "react/require-render-return":1
  }
}
```

La ligne ```"prettier/prettier": "error"``` indique que les règles de linter seront celles de prettier qui se trouveront dans le fichier ```.prettierrc```, toujours à la racine du projet.

.prettierrc :

```json
{
  "arrowParens": "avoid",
  "bracketSpacing": true,
  "endOfLine": "auto",
  "htmlWhitespaceSensitivity": "css",
  "insertPragma": false,
  "jsxBracketSameLine": false,
  "jsxSingleQuote": true,
  "printWidth": 80,
  "proseWrap": "preserve",
  "quoteProps": "as-needed",
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "none",
  "useTabs": false,
  "parser": "babel"
}
```

Nous avons donc un projet linté,
Cependant on aimerait que les corrections se fassent à la sauvegarde.
Pour cela, nous allons créer un fichier de configuration pour VSCode.

Créez à la racine du projet un dossier ```.vscode```

Dans ce dossier, créez un fichier nommé ```settings.json```

settings.json:
```json
{
    // does not render single space between words
    "editor.renderWhitespace": "boundary",
    // vertical rule after 80 charachter
    "editor.rulers": [80],
    // turns off validations that VSCode
    "javascript.validate.enable": false,
    // tab = 2 spaces
    "editor.tabSize": 2,
    // allow prettier to fix eslint 
    // "eslint.autoFixOnSave": true,
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    }
  }
```

Le fichier settings.json définit les règles vsCode pour le projet, très pratique lorsque l'on travaille à plusieurs.

```json   
"editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    }
```
Cette ligne permet l'application des règles du prettier/linter à chaque sauvegarde.
