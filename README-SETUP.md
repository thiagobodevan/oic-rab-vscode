# Setup & Configuration Guide - Oracle Integration Cloud Rapid Adapter Builder

## Visão Geral
Esta é uma extensão VS Code para o **Oracle Integration Cloud Rapid Adapter Builder (RAB)**,
que facilita o desenvolvimento, validação e implantação de adaptadores RAB para OIC (Oracle Integration Cloud).

## Pré-requisitos
- VS Code >= 1.73.0
- Node.js
- npm
- Conta Oracle Integration Cloud (OIC) para registro de adaptadores

## 📦 Instalação de Dependências

### Primeira instalação
```bash
cd oic-rab-vscode
npm install
```

### Windows Note
O script de build original usa comandos Unix (`rm -rf`). Para Windows, foi modificado em `package.json`:
```json
"esbuild-base": "node -e \"const fs=require('fs');fs.rmSync('out',{recursive:true,force:true});\" && esbuild ..."
```

## 🔧 Compilação

### Build padrão
```bash
npm run build
```

### Watch mode (desenvolvimento)
```bash
npm run watch
```

### Pack para distribuição
```bash
npm run package
```

## 🧪 Testes

### Lint
```bash
npm run lint
```

### Type checking
```bash
npx tsc --noEmit
```

### Testes unitários
```bash
npm run test
```

## 📁 Estrutura do Projeto
```
oic-rab-vscode/
├── src/                    # Código fonte TypeScript
│   ├── api.ts              # Integrações API OIC
│   ├── commands/           # Comandos VS Code
│   ├── webview/            # Componentes webview
│   ├── utils.ts            # Funções utilitárias
│   └── ...
├── out/                    # Código compilado (gerado)
├── schemas/                # Schemas JSON para validação
├── snippets/               # Snippets de código VS Code
├── webview/                # Arquivos HTML/CSS/JS para webviews
├── scaffold/               # Templates de scaffold
├── rollup.config.js        # (não usado - usa esbuild)
├── tsconfig.json           # Configuração TypeScript
├── package.json            # Manifesto e dependências
└── .vscode/                # Configurações do VS Code
```

## ⚙️ Configurações Importantes

### tsconfig.json
- Target: ES2020
- Module: CommonJS
- Module Resolution: Node
- Strict mode: enabled
- Source maps: enabled

### ESLint
- Usa `@typescript-eslint` plugin
- Configuração em `.eslintrc.json`

## 🛠️ Comandos Disponíveis

| Comando | Descrição |
|---------|-----------|
| `npm run build` | Compila com esbuild |
| `npm run watch` | Compila em modo watch |
| `npm run lint` | Executa ESLint |
| `npx tsc --noEmit` | Type checking |
| `npm test` | Executa lint + type check |
| `npm run package` | Cria pacote .vsix |

## 🐛 Problemas Conhecidos & Soluções

### 1. Erro de compilação no Windows: `'rm' não é reconhecido`
**Solução:** O script `esbuild-base` foi atualizado para usar `node -e` em vez de `rm -rf`.

### 2. Warnings de ESLint (77 warnings)
**Notas:**
- 0 erros críticos
- Warnings são principalmente de estilo (naming conventions, semicolons)
- Não afetam o funcionamento

### 3. Vulenrabilidades npm audit
- 32 vulnerabilidades (4 baixas, 8 moderadas, 18 altas, 2 críticas)
- Executar `npm audit fix --force` para resolver (pode ter breaking changes)

## 🔗 Links Úteis
- [Oracle Integration Cloud Documentation](https://docs.oracle.com/en/cloud/paas/integration-cloud/index.html)
- [VS Code Extension API](https://code.visualstudio.com/api)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [esbuild Documentation](https://esbuild.github.io/getting-started/)