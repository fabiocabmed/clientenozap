<div align="center">
  <h1>ClienteNoZap</h1>
  <p><strong>Plataforma de Captação Direta de Clientes via WhatsApp &amp; Vitrine Comercial Regional</strong></p>
  <p>Um produto do <strong>Grupo Vitally</strong> • Desenvolvido por <strong>Vitally Studio</strong></p>

  <p>
    <a href="https://clientenozap-eta.vercel.app" target="_blank">
      <img src="https://img.shields.io/badge/Produ%C3%A7%C3%A3o-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Deploy Vercel" />
    </a>
    <img src="https://img.shields.io/badge/Database-Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" alt="Supabase" />
    <img src="https://img.shields.io/badge/Stack-HTML5%20%7C%20Tailwind%20%7C%20JS-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="Stack" />
    <img src="https://img.shields.io/badge/Status-Ativo-16A34A?style=for-the-badge" alt="Status Ativo" />
  </p>
</div>

---

## Sobre o Projeto

O **ClienteNoZap** é uma plataforma web projetada para conectar autônomos, prestadores de serviço, MEIs e negócios locais diretamente aos consumidores da sua região — **sem intermediários, sem comissões por serviço e com conversão imediata no WhatsApp**.

Com foco inicial na **Região Metropolitana de Belém — PA** (*Belém, Ananindeua, Icoaraci, Mosqueiro, Marituba, Benevides e Castanhal*), o sistema combina uma vitrine regional inteligente com **páginas comerciais exclusivas de alta conversão** (`/:slug`) para cada anunciante.

---

## Principais Funcionalidades

### Para Visitantes e Consumidores
- **Busca Inteligente por Serviço e Localidade:** Filtro rápido para encontrar profissionais e lojas ativas na cidade ou bairro desejado.
- **Páginas Exclusivas por Negócio (`/:slug`):** Cada anunciante possui um link curto e compartilhável (ex.: `/barbearia-dos-manos`, `/jc-autopecas`, `/fabiane-personalizados`) com identidade visual própria, catálogo de serviços, horários e provas sociais.
- **Contato Direto em 1 Clique:** Preenchimento guiado de orçamento/agendamento que abre imediatamente a conversa no WhatsApp do profissional com a mensagem já estruturada.

### Para Anunciantes e Gestão (Painel Administrativo)
- **Sincronização em Nuvem (Supabase):** Persistência centralizada de profissionais, leads, configurações e páginas HTML customizadas com fallback automático local.
- **Roteamento Dinâmico & Quebra de Cache:** Configuração de rewrites na Vercel (`vercel.json`) que resolve slugs amigáveis diretamente para o perfil do cliente, ideal para campanhas de tráfego pago e compartilhamento no WhatsApp.
- **Ponte Rastreada de Leads:** Registro silencioso de solicitações de orçamento (`postMessage`) no painel administrativo antes do redirecionamento externo ao WhatsApp.
- **Gestão Financeira e Controle de Voucher:** Acompanhamento de ciclos de assinatura, dias restantes, simulador de receita e flag de **Cliente Voucher / Cortesia** (para parcerias estratégicas sem distorcer a Receita em Ciclo).
- **Estúdio de Criação (IA & HTML Customizado):** Geração assistida de landing pages por estilo/paleta ou upload direto de código HTML exclusivo por anunciante.
- **Auto-Cadastro Público (`?cadastro=empresa`):** Link dedicado para captação e onboarding rápido de novos negócios interessados.

---

## Arquitetura e Tecnologias

O projeto adota uma arquitetura **leve, zero-build e de carregamento instantâneo**, eliminando dependências pesadas de empacotamento:

| Camada | Tecnologia | Função |
| :--- | :--- | :--- |
| **Front-end** | HTML5, CSS3, Tailwind CSS (CDN), Lucide Icons | Interface responsiva, vitrine e painel administrativo |
| **Lógica & Estado** | JavaScript ES Modules (Vanilla JS) | Roteamento por slug, máscaras, ponte de leads e renderização |
| **Banco de Dados** | Supabase (REST / JS Client) | Armazenamento em nuvem e sincronização multi-dispositivo |
| **Hospedagem & Edge** | Vercel (`vercel.json`) | Deploy contínuo, rewrites de URL amigável e controle de cache |

---

## Estrutura do Repositório

```text
clientenozap/
├── index.html          # Aplicação principal (Vitrine, Roteador de Slugs, Modais e Painel Admin)
├── vercel.json         # Regras de rewrite (/:slug -> /index.html) e headers de Cache-Control
├── *.jpeg / *.png      # Ativos visuais estáticos das páginas exclusivas dos anunciantes
└── README.md           # Documentação oficial do projeto
```

> **Nota de Deploy:** A Vercel publica diretamente os arquivos estáticos da raiz (`index.html` e `vercel.json`). Arquivos auxiliares de ambientes de prototipação (`package.json`, `server.js`, `metadata.json`) não devem ser incluídos na branch `main` para evitar conflitos de build.

---

## Configuração e Deploy

### 1. Variáveis e Conexão Supabase
As credenciais públicas do projeto (`supabaseUrl` e `supabaseAnonKey`) operam como padrão na inicialização da aplicação (`obterCredenciaisSupabase()`), permitindo que qualquer visitante mobile abra links diretos sem configuração prévia, enquanto o painel administrativo permite atualização dinâmica.

### 2. Rewrites na Vercel (`vercel.json`)
Para garantir que URLs amigáveis como `https://clientenozap-eta.vercel.app/nome-do-cliente` funcionem sem erro `404` e sem retenção de cache antigo nos navegadores móveis:

```json
{
  "headers": [
    {
      "source": "/index.html",
      "headers": [
        { "key": "Cache-Control", "value": "no-cache, no-store, must-revalidate" }
      ]
    }
  ],
  "rewrites": [
    {
      "source": "/:slug([^.]+)",
      "destination": "/index.html"
    }
  ]
}
```

### 3. Fluxo de Atualização
1. Realize as alterações no `index.html` ou adicione ativos estáticos na raiz do repositório.
2. Faça o commit na branch `main` do GitHub (`fabiocabmed/clientenozap`).
3. A **Vercel** executa o deploy automático em poucos segundos.

---

<div align="center">
  <p><strong>ClienteNoZap</strong> — Você foca no seu serviço. A gente coloca clientes da sua região chamando no seu WhatsApp.</p>
  <p><sub>© 2026 Grupo Vitally • Vitally Studio. Todos os direitos reservados.</sub></p>
</div>