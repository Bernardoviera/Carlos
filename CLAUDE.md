# Projeto: Video Editor IA — Carlos Zavele

## O que é
Aplicação web com Next.js 14 + TypeScript que gera vídeos automaticamente com animações profissionais sobre o conteúdo falado. O usuário faz upload de um vídeo, a IA transcreve (OpenAI Whisper), sugere momentos-chave e gera animações sincronizadas com Remotion + FFmpeg.

## Stack Técnica
- **Frontend/Backend:** Next.js 14 App Router + TypeScript
- **Animações:** Remotion (`@remotion/renderer`, `@remotion/bundler`)
- **Compositing:** FFmpeg com `enable='between(t,START,END)'`
- **IA:** OpenAI Whisper (transcrição) + GPT-4 (sugestão de animações)
- **Deploy:** Railway (precisa plano Hobby $5/mês — trial expirou)

## Identidade Visual PADRÃO (não mudar sem o usuário pedir)
- **Fundo:** preto `#000000`
- **Título:** vermelho `#E53E3E`
- **Subtítulo:** branco `#FFFFFF`
- **Linha divisória:** vermelha `#E53E3E` animando de 0% → 100% de largura
- **Fonte:** Inter weight 700/800 (NÃO usar weight 900 — não existe no Inter)
- **Estilo:** Apple Presentation Style — limpo, espaçado, sem exageros

## Animações Implementadas
| Template | Descrição |
|---|---|
| `LabelOverlay` | Texto sobre o vídeo — fade + blur (12px→0) + translateY com spring() |
| `StatCard` | Card tela cheia azul com número/métrica em destaque |
| `MoneyCard` | Overlay financeiro — R$ valor em destaque |

## Localização dos Arquivos (a recriar se não existir)
```
/
├── app/
│   ├── api/
│   │   ├── render/route.ts       # POST: cria job, retorna jobId
│   │   ├── status/[jobId]/route.ts # GET: progresso do job
│   │   └── analyze/route.ts      # POST: Whisper + GPT-4
│   └── page.tsx                  # UI principal
├── lib/
│   └── render.ts                 # renderMedia() + FFmpeg compositing
├── remotion/
│   ├── Root.tsx
│   └── templates/
│       ├── index.ts              # TemplateName type
│       ├── LabelOverlay.tsx      # ← principal, estilo Apple
│       ├── StatCard.tsx
│       └── MoneyCard.tsx
└── CLAUDE.md                     # este arquivo
```

## Bugs Já Resolvidos (não regredir)
1. **`imageFormat: 'png'`** obrigatório quando `pixelFormat: 'yuva420p'` no renderMedia()
2. **FFmpeg enable=**: usar `between(t,5.000,8.000)` — SEM backslash
3. **Font weight 900**: Inter não tem weight 900, usar 800 no máximo
4. **Jobs na memória**: `const jobs = new Map()` perde estado ao reiniciar o servidor — é limitação conhecida
5. **GPT-4 inventando texto**: prompt deve proibir conteúdo não presente na transcrição

## Próximos Passos (em ordem de prioridade)
1. **Typography Motion** — melhorar LabelOverlay com entrada palavra por palavra vindo do eixo Z (zoom out), usando `spring()` por palavra
2. **Testes no Remotion Studio** — rodar `npx remotion studio` para preview visual antes de renderizar
3. **Deploy Railway** — upgrade para Hobby ($5/mês) e configurar variáveis de ambiente

## Prompts de Referência (Google Search — animações Remotion)

### Typography Motion (prioridade)
> "Programe uma animação de texto no Remotion com estilo de motion design moderno. A frase principal deve entrar em cena vindo do eixo Z (zoom out), palavra por palavra. A cor de destaque deve ser VERMELHA (#E53E3E) — não laranja. A velocidade de digitação de 8 caracteres por segundo. Insira controles deslizantes de escala e opacidade para edição no Remotion Studio."

### Gráficos Analytics
> "Crie um gráfico de barras animado no Remotion. O vídeo deve conter três barras verticais subindo da base para cima, simulando crescimento financeiro. A primeira barra deve atingir 30% de altura, a segunda 70% e a terceira 100% (cor vermelha #E53E3E de destaque). Programe o movimento para iniciar no frame 30 e terminar no frame 90 com efeito de elasticidade (easing)."

### Refinamento Iterativo
- Velocidade: ajustar `durationInFrames` por palavra / `spring({ damping })` 
- Cores: sempre usar paleta padrão acima
- Camera Shake: `interpolate(frame, [0,5,10], [0,3,-3])` no translateX

## Preferências do Usuário
- Linguagem da interface: **português brasileiro**
- Quer animações **profissionais, não amadoras** — referência: mateuscastro.ia no Instagram
- Padrão sempre preto/vermelho/branco — só mudar se ele pedir explicitamente
- Não quer cores laranja, marrom ou tons que "parecem errado"
