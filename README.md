# Pequeno Hermeneuta - Guia de Contexto e Diretrizes para IA (Landing Page)

Este documento serve como a **memória técnica e conceitual** da landing page do **Pequeno Hermeneuta**. Ele foi estruturado especificamente para ser fornecido a Inteligências Artificiais (como copilotos de código e agentes autônomos) para que possam manter, evoluir ou refatorar a página mantendo a consistência visual, técnica e de tom de voz.

---

## 1. Visão Geral e Contexto de Negócio

*   **O que é o Pequeno Hermeneuta:** Um selo editorial infantil e juvenil dedicado a traduzir grandes temas da Filosofia Contemporânea e da Espiritualidade Prática em linguagem lúdica, poética e acolhedora.
*   **Finalidade da Landing Page:** Capturar leads qualificados (nome e e-mail) de pais interessados em educação socioemocional e consciente, oferecendo como recompensa uma amostra digital (PDF) do livro de estreia do selo: **"Saudade de Ti"**.
*   **Público-Alvo (Early Adopters):** Pais, mães, avós e educadores que já possuem rituais de leitura com crianças de 3 a 10 anos e sentem falta de materiais para iniciar conversas profundas sobre temas existenciais (morte, tempo, ausência) de forma laica e socrática.
*   **Tom de Voz:** Poético, reflexivo, socrático e aconchegante. Evitar termos comerciais agressivos, "gatilhos mentais" de escassez ou urgência exagerada e chamadas puramente focadas em vendas. O foco é a conexão afetiva familiar.

---

## 2. Estrutura do Projeto e Arquivos

O projeto é estático, leve e feito com tecnologias web puras (Vanilla stack) para garantir carregamento instantâneo.

```text
pequeno-hermeneuta-landing/
├── index.html           # Estrutura de conteúdo, SEO e script de formulário
├── style.css            # Folha de estilos, animações e Design System (tokens)
├── assets/              # Mídias locais do projeto
│   ├── avatar.jpg       # Foto/Logo circular no cabeçalho (42x42px)
│   └── cover.jpg        # Imagem de capa do livro (usada no mockup 3D, proporção 3:4)
└── README.md            # Este arquivo de contexto
```

---

## 3. Design System & Identidade Visual (Tokens)

As regras visuais do projeto estão centralizadas como CSS Custom Properties (variáveis) em [style.css](file:///Users/calicojack/Library/CloudStorage/GoogleDrive-romeuivolela@gmail.com/My%20Drive/Work/Romeu%20Ivolela%20Consultoria/Development/pequeno-hermeneuta-landing/style.css). Toda e qualquer modificação deve respeitar estes valores:

### Paleta de Cores (Cores Terrosas e Orgânicas)
*   `--color-bg`: `#FDFBF7` (Fundo off-white quente)
*   `--color-text-main`: `#2B2B2B` (Chumbo escuro para legibilidade sem contraste excessivo)
*   `--color-text-muted`: `#555555` (Cinza médio para descrições e subtítulos)
*   `--color-sage`: `#8FA89B` (Verde sálvia, cor de destaque secundária)
*   `--color-sage-light`: `#F0F4F2` (Fundo suave de seções alternativas)
*   `--color-sage-dark`: `#6C8578` (Verde sálvia escuro para textos em fundos claros)
*   `--color-terracota`: `#D07C60` (Terracota, cor principal de CTA e destaque primário)
*   `--color-terracota-light`: `#F9EFEB` (Fundo para badges e caixas)
*   `--color-terracota-dark`: `#B05F45` (Terracota escuro para hover states)
*   `--color-gold`: `#D6A45C` (Dourado sutil para estrelas e detalhes)

### Tipografia
*   **Títulos e Botões (`h1`, `h2`, `h3`, `.btn`, `.badge`):** `'Outfit', sans-serif` (Moderna, geométrica e amigável).
*   **Corpo de Texto e Parágrafos (`body`, `p`):** `'Lora', serif` (Elegante, clássica e de altíssima legibilidade para prosa literária).

### Bordas e Efeitos
*   `--border-radius-sm`: `8px`
*   `--border-radius-md`: `16px`
*   `--border-radius-lg`: `24px`
*   `--transition-smooth`: `all 0.3s cubic-bezier(0.4, 0, 0.2, 1)` (Usar em todas as transições de hover e foco)
*   `--box-shadow-soft`: `0 10px 30px rgba(43, 43, 43, 0.05)`
*   `--box-shadow-medium`: `0 20px 40px rgba(43, 43, 43, 0.1)`

---

## 4. Animações e Efeitos Especiais (Preservar e Respeitar)

1.  **Luzes de Fundo (Ambient Glow):**
    Existem duas div's `.ambient-glow` (`glow-1` e `glow-2`) que criam círculos borrados e flutuantes de cores sálvia e terracota no fundo da página. Eles utilizam as animações `@keyframes float-glow-1` e `@keyframes float-glow-2`. Não remova ou aumente o brilho delas para não comprometer a performance ou o contraste dos textos.
2.  **Mockup de Livro 3D:**
    O livro na seção Hero (`.book-3d`) utiliza transformações 3D no eixo Y e X para criar perspectiva física. Ao passar o mouse, ele gira suavemente (`hover`). O spine lateral simula o verso do livro físico.
3.  **Imagem Inclinada:**
    A ilustração da história na seção Book Showcase (`.showcase-img`) possui uma rotação estática de `-1.5deg` que zera no `hover` acompanhada de um leve scale. Isso dá um ar orgânico de "livro deitado na mesa".

---

## 5. Funcionamento do Formulário e Backend

### Comportamento Atual (Front-end Puro)
O formulário de captura (`#lead-form`) previne o comportamento padrão de recarregamento e:
1. Oculta o formulário original.
2. Atualiza dinamicamente o nome do usuário na tela de sucesso.
3. Mostra o estado `#form-success`, contendo um link para baixar a amostra em PDF (atualmente apontando para `assets/cover.jpg` de forma temporária).

```javascript
document.getElementById('lead-form').addEventListener('submit', function(e) {
  e.preventDefault();
  const name = document.getElementById('parent-name').value;
  const email = document.getElementById('parent-email').value;
  if(name && email) {
    document.getElementById('lead-form').classList.add('hidden');
    document.querySelector('.form-title').classList.add('hidden');
    document.querySelector('.form-desc').classList.add('hidden');
    document.getElementById('user-name').innerText = name.split(' ')[0];
    document.getElementById('form-success').classList.remove('hidden');
    console.log(`Lead Captured - Name: ${name}, Email: ${email}`);
  }
});
```

### Instruções para Integração de API Futura
Se for solicitado a integrar o formulário com um serviço de e-mail marketing (ex: Mailchimp, Substack API, MailerLite ou um webhook do Google Sheets):
1.  **Mantenha a validação HTML5** (`required`, `type="email"`).
2.  Faça uma requisição assíncrona (`fetch`) com `method: 'POST'` e payload JSON.
3.  Exiba uma mensagem de carregamento sutil no botão enquanto a API responde.
4.  Apenas exiba o estado de sucesso (`#form-success`) caso a requisição retorne `status 200/201`.
5.  Em caso de erro de rede, mantenha o formulário visível e exiba uma mensagem de erro abaixo dele para que o usuário possa tentar novamente.

---

## 6. Diretrizes de Desenvolvimento para a IA

Quando for instruído a realizar alterações neste repositório, você **deve seguir rigorosamente** as seguintes regras:

*   **Não altere a stack básica:** Não instale frameworks pesados (React, Vue, Next.js) a menos que explicitamente ordenado pelo proprietário do projeto. A página deve continuar carregando com apenas um arquivo HTML e um arquivo CSS.
*   **Responsividade em Primeiro Lugar:** A página utiliza CSS Grid e Flexbox com um breakpoint principal em `992px` para dispositivos móveis. Certifique-se de testar qualquer nova seção em telas menores (320px a 768px). A ordem mobile inverte a visualização do Hero para colocar a imagem acima do formulário para melhor conversão móvel.
*   **Proporção dos Mockups:** A imagem de capa do livro (`cover.jpg`) e o contêiner 3D estão desenhados estritamente na proporção 3:4. Se for atualizar a imagem da capa do livro, certifique-se de que a nova imagem também possua essa proporção para não distorcer o mockup.
*   **Acessibilidade (a11y):** Garanta que todos os campos de formulário (`input`) tenham `<label>` correspondentes, que os links tenham descrições claras e que o contraste de texto atenda aos padrões WCAG AA usando os tons das variáveis de texto escuro sobre o fundo off-white.

---

## 7. Como publicar alterações (Protocolo de Deploy no Vercel)

Esta landing page está publicada na Vercel no projeto vinculado à conta do autor.

*   **Diretório de Deploy:** O deploy é feito na pasta raiz do projeto.
*   **Script Automatizado (Localizado no repositório pai `po-harness-ai`):**
    Se você estiver no workspace de automação principal, poderá rodar o deploy executando:
    ```bash
    python scripts/deploy_to_vercel.py
    ```
    *Nota: Este comando deve ser executado no terminal com Bypass de Sandbox ativado (`BypassSandbox: true`), pois necessita de conexão externa à API da Vercel.*
*   **URLs de Produção Ativas:**
    *   URL Principal: [https://landingpage-mu-sandy.vercel.app](https://landingpage-mu-sandy.vercel.app)
    *   URL Alternativa: [https://landingpage-ho983un0t-o-hermeneuta.vercel.app](https://landingpage-ho983un0t-o-hermeneuta.vercel.app)
*   **Registro de Deploys:** Toda nova publicação com alterações significativas no layout ou no copy deve ser registrada no histórico do arquivo [experiments.md](file:///Users/calicojack/Library/CloudStorage/GoogleDrive-romeuivolela@gmail.com/My%20Drive/Work/Romeu%20Ivolela%20Consultoria/po-harness-ai/products/pequeno-hermeneuta/validation/experiments.md) do produto.
