REGISTRO DE DECISÕES DE LAYOUT (EVIDÊNCIA DE RACIOCÍNIO)

exercício 8.1    

1.  Grids dos Cards e da Agenda (index.html):
    - Decisão: Intrínseca (repeat(auto-fit, minmax(260px, 1fr))).
    - Por quê? Estrutura repetitiva e uniforme. A função auto-fit calcula a
      quantidade de colunas automaticamente de acordo com o espaço disponível,
      sem necessidade de media queries extras.
    - Largura de falha do protótipo: Abaixo de 280px os títulos quebravam em
      mutas linhas. Com 260px no minmax, acomoda-se perfeitamente sem rolagem.

2.  Reorganização do Cabeçalho e Exibição do Menu Lateral (index.html):
    - Decisão: Deliberada (@media (min-width: 768px)).
    - Por quê? Em dispositivos móveis, a barra lateral (aside) empurra o conteúdo
      principal para baixo. O menu lateral só deve surgir quando houver largura.
    - Largura de falha observada: Ao encolher a janela abaixo de 768px no layout
      de duas colunas (180px 1fr), o conteúdo principal ficava espremido e ilegível.

3.  Página de Detalhes (local.html):
    - Decisão: Intrínseca com contêiner limitado (max-width: 520px; margin: 0 auto;).
    - Por quê? Segue o padrão de cartão centralizado focado na leitura linear.
    - Largura de falha observada: A tabela de informações estourava a tela em visores
      muito estreitos (<320px). O uso de .tabela-wrapper { overflow-x: auto; } evitou
      a rolagem da página inteira.

4.  Inclusão de Imagens Temáticas nos Cards:
    - Decisão: Adaptação visual via CSS de suporte (.card-ilustracao img).
    - Por quê? Para garantir que as imagens inseridas via URL/imagem real preencham
      o topo do card sem distorcer o aspecto nem ultrapassar o limite das caixas,
      utilizou-se object-fit: cover e posicionamento absoluto para as legendas.

5.  Elementos deixados de fora temporariamente:
    - Tipografia com fontes externas (@font-face).
    - Por quê? O foco principal é a estrutura de layout e responsividade. O uso de
      system-ui resolve a apresentação visual perfeitamente sem causar lentidão.

---

Registro de Decisões — Exercício 8.3

1. Cálculo da Tipografia Fluida (`clamp`)

Título da Vitrine (`.hero h2`)

Regra CSS: `font-size: clamp(1.75rem, 5vw + 1rem, 3rem);`
Cálculo em ~360px (Mobile):**
`5% de 360px` = 18px
`18px + 16px (1rem)` = 34px
Resultado:\* Mantém excelente legibilidade sem estourar o container.
Cálculo em 1280px (Desktop):
`5% de 1280px` = 64px
`64px + 16px (1rem)` = 80px - Resultado: Atinge o limite máximo da trava em **48px (3rem), garantindo equilíbrio visual.

Título da Página do Local (`.titulo-pagina-local`)
Regra CSS:** `font-size: clamp(1.5rem, 4vw + 0.8rem, 2.5rem);`
Cálculo em ~360px:** `14.4px + 12.8px` = **27.2px**
Cálculo em ~1280px:** `51.2px + 12.8px` = 64px &rarr; Trava no máximo de **40px (2.5rem).

- 2. Auditoria de Acessibilidade (Lighthouse)

- Página: Home (`index.html`)
  Nota Acessibilidade:** 98
  Achado do Relatório:** Links de contato no rodapé não possuíam indicador claro para estado de foco ao navegar via teclado.
  Ação Corretiva:Implementada a regra `:focus-visible` global no CSS com contorno contrastante de 3px.

- Página: Local (`local.html`)
  Nota Acessibilidade: 92
  Achado do Relatório:Contraste reduzido no texto secundário da legenda da tabela (`.legenda-data`).
  Ação Corretiva:Ajustada a cor da legenda para um tom com maior taxa de contraste (`#595959`).

---

- 3.  Matriz de Resolução (Divisão Por Página)

| Página | O que a folha de estilos única (`style.css`) resolveu sozinho | O que era por página e precisou de correção própria |

| Home (`index.html`)| - Regra universal de mídias (`max-width: 100%`).<br>- Dimensionamento fluido do título com `clamp()`.<br>- Garantia da área de toque de 44px nos links de navegação. | - Ajuste da ordem dos títulos hierárquicos (`<h1>` no topo, `<h2>` na vitrine e `<h3>` nas categorias).<br>- Adição de atributos `aria-label` na navegação por categorias. |

| Página do Local (`local.html`)| - Foco visível com `:focus-visible` nos elementos interativos.<br>- Responsividade e enquadramento da imagem de destaque via `object-fit: cover`. | - Criação do wrapper com rolagem horizontal na tabela (`.tabela-wrapper`) para evitar estouro da página em telas <320px.<br>- Descrições `alt` detalhadas nas imagens dos banners.

-------------------------------------------
