# paradigma. — E-mail Marketing + Quiz Interativo

> Newsletter de desenvolvimento com quiz embutido para descoberta de paradigma de programação ideal.

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Zero dependências](https://img.shields.io/badge/dependências-zero-4ecb8d?style=flat)
![License: MIT](https://img.shields.io/badge/License-MIT-8B7FE8?style=flat)

---

## Sobre o projeto

**paradigma.** é um template de e-mail marketing responsivo que incorpora um quiz interativo diretamente na página — sem redirecionamentos, sem frameworks, sem dependências externas.

O usuário lê a newsletter sobre paradigmas de programação e, ao clicar em "Fazer o quiz agora →", o quiz aparece inline na mesma página. Ao responder 5 perguntas, recebe um resultado personalizado com seu paradigma dominante, linguagens recomendadas e barras de compatibilidade animadas.

Este projeto foi desenvolvido como um desafio de **compatibilidade de e-mail** e **UX progressiva**, resolvendo os principais problemas de renderização cross-client com técnicas de produção.

---

## Demo

Abra o arquivo `email-marketing-quiz.html` diretamente no navegador — nenhum servidor necessário.

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/paradigma-email-quiz.git

# Abra no navegador
open email-marketing-quiz.html
# ou: double-click no arquivo
```

---

## Funcionalidades

### E-mail
- Layout completo com header, hero, barra de estatísticas, 4 cards de features (grade 2×2), citação destacada, tabela comparativa e footer
- CTA principal que abre o quiz inline via scroll suave
- Links de descadastro e preferências no footer (conformidade LGPD/CAN-SPAM)
- Preview text oculto para clientes de e-mail

### Quiz
- 5 perguntas com 4 opções cada, cobrindo estilo de raciocínio, satisfação no código, tipo de projeto, relação com bugs e filosofia de programação
- Motor de pontuação: cada resposta acumula pontos para um dos 4 paradigmas (declarativo, OOP, funcional, imperativo)
- Barra de progresso animada por etapa
- Navegação para frente e para trás entre perguntas
- Resultado personalizado com título, descrição, traits de personalidade, barras de compatibilidade animadas e linguagens recomendadas com badges coloridos
- Botão "Refazer o quiz" com reset completo de estado

---

## Compatibilidade de e-mail

Este template implementa técnicas específicas para os principais clientes de e-mail:

| Cliente | Técnica aplicada |
|---|---|
| **Outlook 2016–2021** | Namespaces VML (`xmlns:v`, `xmlns:o`), `PixelsPerInch`, comentários condicionais `<!--[if mso]>` |
| **Outlook (todos)** | `mso-table-lspace: 0pt` e `mso-table-rspace: 0pt` para zerar espaçamento fantasma em tabelas |
| **Apple Mail / iOS** | `x-apple-data-detectors` para impedir que textos sejam convertidos em links automáticos |
| **iOS Safari** | `-webkit-text-size-adjust: 100%` para evitar zoom automático de texto |
| **Windows Phone** | `-ms-text-size-adjust: 100%` |
| **Gmail** | Estilos inline em todos os elementos críticos; sem `<link>` externo |
| **Todos os clientes** | `role="presentation"` em todas as tabelas de layout |

### Responsividade

A grade de 2 colunas colapsa para 1 coluna abaixo de 600px usando `display: block` via media query nas classes `.stack-column` e `.stack-column-center`. Padding, tamanho de fonte e margens são ajustados progressivamente no breakpoint mobile.

---

## Estrutura do arquivo

O projeto é entregue em um único arquivo HTML autocontido:

```
email-marketing-quiz.html
│
├── <head>
│   ├── Meta tags de compatibilidade
│   ├── Estilos do e-mail (reset, responsividade)
│   └── Estilos do quiz (cards, animações, resultado)
│
├── #email-section          ← Newsletter completa em tabelas
│   ├── Header
│   ├── Hero + CTA
│   ├── Stats bar (3 colunas)
│   ├── Feature cards (2×2 → 1×4 mobile)
│   ├── Blockquote
│   ├── Tabela comparativa
│   ├── CTA quiz
│   └── Footer
│
├── #quiz-section           ← Quiz interativo (oculto até o CTA)
│   ├── Barra de progresso
│   ├── Q1–Q5 (cards com transição fadeUp)
│   └── #quiz-result (resultado com barras animadas)
│
└── <script>
    ├── selectOpt()         ← Registra resposta e habilita botão
    ├── goNext() / goBack() ← Navegação entre perguntas
    ├── computeResult()     ← Calcula paradigma dominante por tally
    ├── showResult()        ← Renderiza resultado e anima barras
    ├── startQuiz()         ← Exibe #quiz-section com scroll suave
    └── restartQuiz()       ← Reset completo de estado
```

---

## Os 4 paradigmas

| Paradigma | Linguagens | Pontos fortes |
|---|---|---|
| 🎯 **Declarativo** | SQL, HTML/CSS, GraphQL, Python, TypeScript | Legibilidade, intenção clara, produtividade |
| 🧩 **Orientado a objetos** | Python, Kotlin, Java, C#, Swift | Modelagem, reutilização, escalabilidade |
| 🔄 **Funcional** | Elixir, Haskell, F#, Clojure, Scala | Pureza, composição, testabilidade |
| ⚙️ **Imperativo** | C, Go, Rust, C++, Bash | Controle, performance, proximidade do hardware |

---

## Personalização

### Trocar as cores do tema

As cores principais estão definidas inline nos elementos. As variáveis de cor do projeto:

```
#8B7FE8   → Roxo primário (accent, CTAs, paradigma declarativo)
#4ecb8d   → Verde (paradigma OOP, stat positiva)
#e8b84b   → Âmbar (paradigma funcional)
#7a7a8a   → Cinza (paradigma imperativo)
#0f0f12   → Background principal
#16161f   → Background de cards
#2a2a38   → Bordas e separadores
```

### Adicionar ou remover perguntas

Cada pergunta é um `<div class="q-card" id="qN">`. Para adicionar uma pergunta:

1. Copie um bloco `q-card` existente e incremente o `id`
2. Defina os `data-val` das opções com um dos 4 paradigmas
3. Atualize a constante `totalQ` no script para o novo total
4. Ajuste os atributos `onclick` de `goNext()` e `goBack()` nos botões de navegação

### Adaptar para envio real

Para usar em plataformas de e-mail (Mailchimp, SendGrid, etc.):

- Extraia apenas o conteúdo de `#email-section` — o quiz é uma funcionalidade de landing page
- Substitua o `onclick="startQuiz()"` por um link externo para a versão hospedada do quiz
- Inline todos os estilos restantes com uma ferramenta como o [Juice](https://github.com/Automattic/juice) antes do envio

---

## Tecnologias

- **HTML5** com compatibilidade retroativa para Outlook via VML
- **CSS3** com media queries, animações `@keyframes` e transições
- **JavaScript vanilla** — zero bibliotecas, zero frameworks, zero dependências

---

## Licença

MIT — use, modifique e distribua livremente.

---

<p align="center">Feito com <strong>paradigma.</strong> · 2026</p>
