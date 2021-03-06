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