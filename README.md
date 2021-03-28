# 002 - Static Analysis Testing Javascript

## 01 - Configurando e executando o ESLINT
O Eslint é um lint (verificador) de arquivos onde podemos analisar nosso código ao longo do desenvolvimento e aplicar padrões de código em nossa aplicação, isso faz com que todo o nosso software tenha a mesma base de código, as mesmas regras em relação a code base assim como também uma constância na aplicação o que faz com que todos os desenvolvedores do projeto estejam alinhados.

01 - Para iniciar devemos instalar o ESLint:
```bash
npm install --save-dev eslint
```

02 - Criar o arquivo de configuração do eslint: ```.eslintrc```
```json
{
  "parserOptions": {
    "ecmaVersion": 2019,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "rules": {
    "valid-typeof": "warn",
    "no-unsafe-negation": "error",
    "no-unused-vars": "error",
    "no-unexpected-multiline": "error",
    "no-undef": "error",
    "strict": ["error", "never"]
  },
  "env": {
    "browser": true
  }
}
```

**parseOptions**: São algumas informações acerca da versão do JavaScript que estamos utilizando.
**rules**: São algumas regras onde definimos como nosso código deve ser escrito, restrições e etc.
**env**: Se refere ao ambiente pois as regras podem variar de ambiente para ambiente seja no browser ou no servidor.

## 02 - Instalar a extensão do eslint no VSCODE:
Com a extensão do eslint podemos ver os erros, concertar alguns através da própria extensão.

Link Extensão: [Eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Também podemos executar o comando abaixo, para que o eslint de forma automatica corrija alguns erros.

```bash
npx eslint . --fix
```


## 03 - Usando as pré-configurações recomendas pelo ESLINT
Ao adicionar uma configuração dentro do nosso ```.eslintrc```, temos a definição de algumas regras básicas de acordo com o eslint. Ou seja é um pacote pré-definido de algumas regras onde podemos adicionar a seguinte propriedade no JSON de configuração:
```json
{
  "extends": ["eslint:recommended"]
}
```

Nosso json do arquivo ```.eslintrc```, fica da seguinte forma:
```json
{
  "parserOptions": {
    "ecmaVersion": 2019,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "extends": ["eslint:recommended"],
  "rules": {
    "strict": ["error", "never"]
  },
  "env": {
    "browser": true
  }
}
```

## 04 - Executando Eslint a partir de npm scripts
Com os npm's scripts podemos executar diversos comandos, incluindo pacotes como o do eslint, para isso dentro do arquivo ```package.json``` criaremos o seguinte comando:
```json
{
  "scripts": {
    "lint": "eslint --ignore-path .gitignore",
    "build": "babel src --out-dir dist"
  }
}
```

O comando **lint**, executará o eslint também ignorará todas as pastas e arquivos que estiverem dentro do arquivo ```.gitignore```. Para executar basta digitar o comando abaixo:
```bash
npm run lint
```

Opcionalmente também podemos criar o arquivo ```.eslintignore```, que nos possibilita adicionar pacotes e arquivos para não serem incluidos na analise do eslint.
```
node_modules
dist
```

## 05 - Formatando código com Prettier
O prettier é um formatador de código, responsavel por deixar nosso código mais bonito e legivel.

01 - Primeiramente devemos instalar o prettier:
```bash
npm install --save-dev prettier
```

02 - Podemos rodar o comando abaixo em um arquivo, nesse caso se o código estiver mal formatado ele irá formatar o código e mostrará no console:
```bash
npx prettier src/example.js
```
Ex: Código mal formatado
```js
const name = "Freddy";
typeof name === "string";

if (   !("serviceWorker" in navigator)) {
  // you have an old browser :-(
}

const greeting = "hello";
console.log(`${greeting} world!`);
[(1, 2, 3)].forEach((x) => console.log(x));
```
Ex: Código mostrado no console após rodar o comando
```js
const name = "Freddy";
typeof name === "string";

if (!("serviceWorker" in navigator)) {
  // you have an old browser :-(
}

const greeting = "hello";
console.log(`${greeting} world!`);
[(1, 2, 3)].forEach((x) => console.log(x));
```
03 - Em seguida para que o prettier possa agir podemos rodar o comando abaixo, assim ele irá formatar e sobrescrever o código
```bash
npx prettier src/example.js --write
```

04 - Para agilizar a formatação dos arquivos, podemos criar um script que formatará todos os arquivos que terminem com ```.js``` e ```.json```.
```json
{
  "scripts": {
    "lint": "eslint --ignore-path .gitignore",
    "build": "babel src --out-dir dist",
    "format": "prettier --ignore-path .gitignore --write \"**/*.+(js|json)\""
  },
}
``` 

O comando acima formata todos os arquivos ```.js``` e ```.json```, também passamos a flag de para ignorarmos todas as pastas e arquivos que estão dentro do arquivo ```.gitignore```.


## 06 - Configurando Prettier
Assim como o EsLint, também podemos configurar o prettier criando um arquivo de configuração chamado ```.prettierrc```.

Para facilitar a criação do arquivo podemos utilizar o playground da propria ferramenta para aplicar as opções: [Playground Prettier](https://prettier.io/playground/)

Ao fim podemos copiar as configurações e colar dentro de um arquivo chamado ```.prettierrc```.
```json
{
  "arrowParens": "avoid",
  "bracketSpacing": false,
  "embeddedLanguageFormatting": "auto",
  "htmlWhitespaceSensitivity": "css",
  "insertPragma": false,
  "jsxBracketSameLine": false,
  "jsxSingleQuote": false,
  "printWidth": 80,
  "proseWrap": "always",
  "quoteProps": "as-needed",
  "requirePragma": false,
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "all",
  "useTabs": true,
  "vueIndentScriptAndStyle": false
}
```

Essas configurações serão usadas quando rodarmos algum comando que tenha o prettier no contexto, como o comando abaixo:
```bash
npm run format
```

## 07 - Usando a extensão do prettier no VSCODE
Assim como a extensão do eslint podemos usar também a do prettier.

Você pode baixa-la no seguinte link: [Prettier VSCODE](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Ao instalarmos, teremos que definir como padrão um formatador de código, abrimos o arquivo ```config.json```, do vscode e adicionamos a seguinte propriedade abaixo no arquivo
```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```
Também podemos utilizar o prettier para que formate o código ao salvar, adicionando a seguinte linha:
```json
{
  "editor.formatOnSave": true
}
```

## 08 - Desabilitando estilos desnecessarios do eslint com eslint config prettier
Ao usar o eslint e o prettier, podemos em algum momento ter conflitos nas regras, um exemplo disso seria apontar no prettier que não queremos ";" no final de nossas linhas e dentro do eslint apontarmos que ao final de toda linha queremos o ";", sendo assim seria necessário desabilitar dentro do eslint essa regra, porém podemos usar o pacote ```eslint-config-prettier```, para que esses modulos possam se conversar entre si.

01 - Inicialmente devemos instalar o ```eslint-config-prettier```:
```bash
npm install --save-dev eslint-config-prettier
```

02 - Em seguida dentro da propriedade ```extends```, devemos adicionar essa extensão ```eslint-config-prettier```.
```json
{
  "extends": ["eslint:recommended", "eslint-config-prettier"],
}
```

Após isso teremos o resultado onde esses dois pacotes irão se conversar e evitar conflitos.