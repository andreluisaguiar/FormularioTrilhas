# 📝 Formulário de Inscrição com Validação

> Desafio 2 do **Programa Trilhas**: página de cadastro feita com HTML, CSS e JavaScript, seguindo o design do Figma e validando os dados antes do envio.

![Status](<https://img.shields.io/badge/status-em%20desenvolvimento-yellow>)
![HTML](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)

---

## 📑 Sumário

- [Sobre o projeto](#-sobre-o-projeto)
- [Integrantes](#-integrantes)
- [Tecnologias](#-tecnologias)
- [Como executar](#-como-executar)
- [Estrutura de pastas](#-estrutura-de-pastas)
- [Requisitos](#-requisitos)
- [Regras de validação](#-regras-de-validação)
- [Divisão de tarefas](#-divisão-de-tarefas)
- [Fluxo de trabalho no Git](#-fluxo-de-trabalho-no-git)
- [Critérios de avaliação](#-critérios-de-avaliação)

---

## 📌 Sobre o projeto

Este projeto é uma página com um **formulário de cadastro**. Antes de enviar, o formulário confere se os dados foram preenchidos do jeito certo e, quando algo está errado, **mostra uma mensagem de erro logo abaixo do campo** dizendo o que precisa ser corrigido.

Esse tipo de formulário aparece em quase todo site e aplicativo (cadastros, compras online, inscrições), por isso aprender a fazê-lo é um passo importante para quem está começando no Front-end.

**O que praticamos:**

- HTML para a estrutura da página
- CSS para reproduzir o layout do Figma
- JavaScript para validar os campos
- Git e GitHub para trabalhar em dupla

🎨 **Design de referência:** [Figma do desafio](COLE_AQUI_O_LINK_DO_FIGMA)

---

## 👥 Integrantes

| Nome                             | GitHub                                            |
| -------------------------------- | ------------------------------------------------- |
| André Luis Aguiar do Nascimento | [@andreluisaguiar](https://github.com/andreluisaguiar)    |
| Maria Clara                     | [@MariClaraFront-end](https://github.com/MariClaraFront-end) |

---

## 🛠 Tecnologias

- **HTML5**: estrutura semântica do formulário
- **CSS3**: estilização (cores, fontes, espaçamentos, layout)
- **JavaScript (puro)**: validação dos campos, sem bibliotecas
- **Git e GitHub**: versionamento e colaboração

---

## ▶️ Como executar

1. Clone o repositório:

   ```bash
   git clone https://github.com/andreluisaguiar/FormularioTrilhas.git
   cd FormularioTrilhas
   ```
2. Abra o arquivo `index.html` no navegador.

   > Dica: no VS Code, a extensão **Live Server** recarrega a página sozinha a cada alteração.
   >

---

## 📁 Estrutura de pastas

```
FormularioTrilhas/
├── index.html          # Estrutura da página e do formulário
├── css/
│   └── style.css       # Estilos da página
├── js/
│   └── script.js       # Validações do formulário
├── assets/
│   └── imgs/           # Imagens e ícones exportados do Figma
└── README.md
```

---

## ✅ Requisitos

### Layout (HTML + CSS)

- [ ] Montar a estrutura com HTML: título, textos, campos do formulário e botões
- [ ] Incluir **todos** os campos que aparecem no Figma
- [ ] Reproduzir a aparência do design com CSS: cores, fontes, tamanhos, espaçamentos e posição dos elementos
- [ ] Botões **"Cancelar"** e **"Realizar inscrição"** (podem ser só visuais, sem ação)

### Validação (JavaScript)

- [ ] Validar **Telefone**
- [ ] Validar **E-mail**
- [ ] Validar **CPF** (com dígitos verificadores)
- [ ] Validar **Data de nascimento**
- [ ] Mostrar mensagem de erro **logo abaixo** do campo inválido
- [ ] Tirar a mensagem de erro quando o campo for corrigido

> Os outros campos do Figma precisam aparecer na página, mas a validação só é obrigatória para os quatro acima.

### GitHub

- [ ] Fazer commits a cada etapa concluída (nada de um único commit gigante no final)
- [ ] Os **dois integrantes** precisam ter commits no repositório

---

## 🔍 Regras de validação

| Campo                        | Regra                                                                                                                 | Mensagem de erro sugerida                 |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| **Telefone**           | DDD + número, com **10 ou 11 dígitos** no total. Não pode ter letras.                                        | `Insira um número de telefone válido` |
| **E-mail**             | Precisa ter formato de e-mail, com `@` e domínio. Ex.: `nome@email.com`                                          | `Insira um e-mail válido`              |
| **CPF**                | Precisa ter **11 dígitos** e ser um CPF **válido** (os dígitos verificadores também são conferidos). | `Insira um CPF válido`                 |
| **Data de nascimento** | Precisa ser uma data que **existe** (ex.: 31/02 não existe) e **não pode estar no futuro**.             | `Insira uma data de nascimento válida` |

### Exemplo visual do erro

```
Telefone
┌──────────────────────────────────┐
│ 9888                             │  ← borda do campo em vermelho
└──────────────────────────────────┘
Insira um número de telefone válido   ← texto vermelho, logo abaixo
```

### Detalhes de implementação

<details>
<summary><strong>📞 Telefone</strong></summary>

1. Remover a máscara/formatação (parênteses, espaços, hífen) para ficar só com os números.
2. Se o valor original tiver **letras**, é inválido.
3. Conferir se sobraram **10 ou 11 dígitos**.

```js
const apenasNumeros = valor.replace(/\D/g, '');
const temLetras = /[a-zA-Z]/.test(valor);
const valido = !temLetras && (apenasNumeros.length === 10 || apenasNumeros.length === 11);
```

</details>

<details>
<summary><strong>📧 E-mail</strong></summary>

Conferir o formato `texto@dominio.extensao` com uma expressão regular simples:

```js
const valido = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(valor);
```

</details>

<details>
<summary><strong>🪪 CPF</strong></summary>

1. Tirar pontos e hífen, deixando só os números.
2. Conferir se há **11 dígitos**.
3. Recusar sequências repetidas (`000.000.000-00`, `111.111.111-11`...). Elas passam no cálculo, mas não são CPFs válidos.
4. **1º dígito verificador:** multiplicar os 9 primeiros dígitos por 10, 9, 8... até 2, somar tudo e calcular `(soma * 10) % 11`. Se der 10, o dígito é 0. O resultado tem que ser igual ao 10º dígito.
5. **2º dígito verificador:** multiplicar os 10 primeiros dígitos por 11, 10, 9... até 2 e repetir a conta. O resultado tem que ser igual ao 11º dígito.

> CPF válido para testar: `529.982.247-25`

</details>

<details>
<summary><strong>🎂 Data de nascimento</strong></summary>

1. Separar dia, mês e ano.
2. Criar a data com `new Date(ano, mes - 1, dia)` e conferir se o dia, o mês e o ano continuam os mesmos. Uma data como 31/02 "vira" 03/03, e assim dá para saber que ela não existe.
3. Comparar com a data de hoje: a data **não pode ser no futuro**.

```js
const data = new Date(ano, mes - 1, dia);
const existe = data.getFullYear() === ano && data.getMonth() === mes - 1 && data.getDate() === dia;
const noFuturo = data > new Date();
const valido = existe && !noFuturo;
```

</details>

### Quando validar

- **Ao clicar em "Realizar inscrição"**: valida todos os campos e mostra todos os erros de uma vez.
- **Ao sair do campo (`blur`)**: valida só aquele campo, para a pessoa ver o erro na hora.
- **Ao corrigir o campo (`input`)**: tira a mensagem de erro assim que o valor ficar válido.

---

## 🗂 Divisão de tarefas

> Cada tarefa deve virar **uma branch** e **pelo menos um commit**. Atualizem a coluna **Status** conforme forem avançando.

### Resumo por pessoa

| Integrante | Tarefas | Foco |
| ---------- | ------- | ---- |
| **Maria** | 2.1, 2.2, 2.3, 2.4, 2.5 | Toda a estrutura da página em **HTML** |
| **André** | 1.1, 1.2, 1.3, 3.1 a 3.5, 4.1 a 4.6, 5.1 a 5.3 | Configuração, todo o **CSS**, todo o **JavaScript** e a finalização |

> Para os commits da Maria aparecerem bem no histórico, cada tarefa de HTML (2.1 a 2.5) deve ter **pelo menos um commit próprio**, em vez de um único commit com o HTML inteiro.

### Etapa 1: Configuração

| #   | Tarefa                                                                                        | Responsável | Status |
| --- | --------------------------------------------------------------------------------------------- | ------------ | ------ |
| 1.1 | Criar repositório, adicionar a parceira como colaboradora e subir este README                | André        | ⬜     |
| 1.2 | Criar a estrutura de pastas e os arquivos base (`index.html`, `style.css`, `script.js`) | André        | ⬜     |
| 1.3 | Exportar do Figma as imagens/ícones e anotar cores e fontes                                  | André        | 🟨     |

### Etapa 2: Estrutura (HTML)

| #   | Tarefa                                                                 | Responsável | Status |
| --- | ---------------------------------------------------------------------- | ------------ | ------ |
| 2.1 | Cabeçalho e título/textos da página                                 | Maria        | ⬜     |
| 2.2 | Campos de dados pessoais (nome, CPF, data de nascimento, etc.)         | Maria        | ⬜     |
| 2.3 | Campos de contato (telefone, e-mail, etc.) e os demais campos do Figma | Maria        | ⬜     |
| 2.4 | Botões "Cancelar" e "Realizar inscrição"                            | Maria        | ⬜     |
| 2.5 | Espaço para a mensagem de erro abaixo de cada campo validado          | Maria        | ⬜     |

### Etapa 3: Estilo (CSS)

| #   | Tarefa                                                            | Responsável | Status |
| --- | ----------------------------------------------------------------- | ------------ | ------ |
| 3.1 | Variáveis de cores e fontes (`:root`), reset e estilos globais | André        | ⬜     |
| 3.2 | Layout geral da página (container, espaçamentos, alinhamentos)  | André        | ⬜     |
| 3.3 | Estilo dos campos (inputs, labels, selects, foco)                 | André        | ⬜     |
| 3.4 | Estilo dos botões                                                | André        | ⬜     |
| 3.5 | Estilo de erro (borda vermelha e mensagem)                        | André        | ⬜     |

### Etapa 4: Validação (JavaScript)

| #   | Tarefa                                                              | Responsável | Status |
| --- | ------------------------------------------------------------------- | ------------ | ------ |
| 4.1 | Funções para mostrar e limpar a mensagem de erro                  | André        | ⬜     |
| 4.2 | Validação do **Telefone**                                   | André        | ⬜     |
| 4.3 | Validação do **E-mail**                                     | André        | ⬜     |
| 4.4 | Validação do **CPF**                                        | André        | ⬜     |
| 4.5 | Validação da **Data de nascimento**                         | André        | ⬜     |
| 4.6 | Ligar as validações aos eventos (`submit`, `blur`, `input`) | André        | ⬜     |

### Etapa 5: Finalização

| #   | Tarefa                                                                  | Responsável | Status |
| --- | ----------------------------------------------------------------------- | ------------ | ------ |
| 5.1 | Comparar a página com o Figma e ajustar os detalhes                    | André        | ⬜     |
| 5.2 | Testar todos os casos (ver [checklist de testes](#-checklist-de-testes)) | André        | ⬜     |
| 5.3 | Revisar o README e marcar o status como concluído                      | André        | ⬜     |

**Legenda:** ⬜ A fazer · 🟨 Em andamento · ✅ Concluído

### Combinado entre o HTML e o CSS/JS

Como o HTML é de uma pessoa e o CSS/JS de outra, os dois precisam usar **os mesmos nomes**. A Maria usa estes `id`s e classes no HTML, e o André usa os mesmos no CSS e no JavaScript:

| Elemento | No HTML | Exemplo |
| -------- | ------- | ------- |
| Formulário | `id="formulario"` | `<form id="formulario" novalidate>` |
| Telefone | `id="telefone"` | `<input type="tel" id="telefone" name="telefone">` |
| E-mail | `id="email"` | `<input type="email" id="email" name="email">` |
| CPF | `id="cpf"` | `<input type="text" id="cpf" name="cpf">` |
| Data de nascimento | `id="data-nascimento"` | `<input type="date" id="data-nascimento" name="data-nascimento">` |
| Grupo de cada campo | `class="campo"` | uma `<div class="campo">` envolvendo label, input e erro |
| Mensagem de erro | `class="mensagem-erro"` + `id="erro-<campo>"` | `<span class="mensagem-erro" id="erro-telefone"></span>` |

Exemplo completo de um campo validado:

```html
<div class="campo">
  <label for="telefone">Telefone</label>
  <input type="tel" id="telefone" name="telefone" placeholder="(00) 00000-0000">
  <span class="mensagem-erro" id="erro-telefone"></span>
</div>
```

> Se algum nome precisar mudar, combinem antes e atualizem esta tabela.

### Ordem e dependências

1. **André** termina a configuração (1.1, 1.2 e 1.3) e sobe para a `main`.
2. **Maria** monta o HTML seguindo o [combinado acima](#combinado-entre-o-html-e-o-cssjs). Ela pode começar logo depois do passo 1.
3. Enquanto isso, **André** já adianta o que não depende do HTML pronto: variáveis e reset (3.1) e as funções de validação (4.2 a 4.5), que só recebem um valor e respondem se é válido.
4. Quando o HTML estiver na `main`, **André** faz o restante do CSS (3.2 a 3.5) e liga as validações à página (4.1 e 4.6).
5. Por último vêm os ajustes com o Figma e os testes (5.1 a 5.3).

### 🧪 Checklist de testes

| Campo    | Entrada             | Esperado                      |
| -------- | ------------------- | ----------------------------- |
| Telefone | `9888`            | ❌ Erro                       |
| Telefone | `(11) 9abc-1234`  | ❌ Erro                       |
| Telefone | `(11) 3456-7890`  | ✅ Válido (10 dígitos)      |
| Telefone | `(11) 98765-4321` | ✅ Válido (11 dígitos)      |
| E-mail   | `nome.email.com`  | ❌ Erro                       |
| E-mail   | `nome@email`      | ❌ Erro                       |
| E-mail   | `nome@email.com`  | ✅ Válido                    |
| CPF      | `123.456.789-00`  | ❌ Erro (dígitos errados)    |
| CPF      | `111.111.111-11`  | ❌ Erro (sequência repetida) |
| CPF      | `529.982.247-25`  | ✅ Válido                    |
| Data     | `31/02/2000`      | ❌ Erro (data não existe)    |
| Data     | data de amanhã     | ❌ Erro (futuro)              |
| Data     | `15/08/1999`      | ✅ Válido                    |

---

## 🔀 Fluxo de trabalho no Git

### Branches

- `main`: só recebe código pronto e revisado
- Uma branch por tarefa, criada a partir da `main`:

```bash
git checkout main
git pull
git checkout -b feat/validacao-cpf
```

Exemplos de nomes: `feat/html-estrutura`, `style/campos`, `feat/validacao-telefone`, `fix/erro-data`.

### Commits

Façam commits pequenos e frequentes, com mensagens claras no padrão:

```
tipo: descrição curta do que foi feito
```

| Tipo         | Uso                                         | Exemplo                                          |
| ------------ | ------------------------------------------- | ------------------------------------------------ |
| `feat`     | Nova funcionalidade                         | `feat: adiciona validação de CPF`            |
| `style`    | Mudança visual/CSS                         | `style: estiliza botões conforme o Figma`     |
| `fix`      | Correção de bug                           | `fix: corrige data aceitando 31/02`            |
| `docs`     | Documentação                              | `docs: atualiza divisão de tarefas no README` |
| `refactor` | Melhoria de código sem mudar comportamento | `refactor: separa funções de validação`    |
| `chore`    | Configuração/arquivos do projeto          | `chore: cria estrutura de pastas`              |

### Pull Requests

1. Terminou a tarefa? Suba a branch: `git push -u origin nome-da-branch`
2. Abra um **Pull Request** para a `main` no GitHub.
3. O **parceiro revisa** e aprova.
4. Faça o merge e apague a branch.
5. Antes de começar a próxima tarefa, atualize a `main` local com `git pull`.

> ⚠️ Para evitar conflitos, combinem quem mexe em cada parte do `index.html` e do `style.css` ao mesmo tempo.

---

## 🏆 Critérios de avaliação

- [ ] A página segue o layout do Figma
- [ ] Os quatro campos têm validação funcionando
- [ ] As mensagens de erro são claras e aparecem perto do campo
- [ ] O repositório tem commits organizados ao longo do desafio
- [ ] Os dois integrantes da dupla têm commits

---

<p align="center">Feito em dupla para o <strong>Programa Trilhas</strong> 💜</p>
