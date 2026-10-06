# InfraSpec v3.0 - Engenharia de Infraestrutura, CFTV, Energia & Redes

> **Documento de Arquitetura, Identidade Visual e Especificação Técnica**  
> **Homologação:** Outubro de 2026  
> **Ambiente:** Execução 100% Client-Side (HTML5 + TailwindCSS + Vanilla JS ES6+)  
> **Custo Operacional:** R$ 0,00 • Sem necessidade de Node.js, banco externo ou compiladores.

---

## 1. Identidade Visual & Design System

A identidade visual do **InfraSpec v3.0** foi concebida diretamente a partir da linguagem gráfica do logotipo oficial (`img/is-logo.jpg`):

- **Conceito Visual:** Engenharia de precisão, redes corporativas e circuitos integrados (*PCB trace*).
- **Atmosfera:** Sóbria, corporativa, tecnológica e de alto contraste, proporcionando foco e produtividade para engenheiros, analistas de infraestrutura e técnicos de telecomunicações.

### 1.1 Paleta Cromática

| Token | Valor Hex | Aplicação no Sistema |
| :--- | :--- | :--- |
| **Dark Canvas (Background)** | `#070d14` | Fundo principal da aplicação em modo escuro de alta legibilidade |
| **Surface Dark (Cards)** | `#0d1723` | Cartões de parâmetros, formulários e painéis de cálculo |
| **Surface Dark Accent** | `#132233` | Sub-seções, acordeões abertos e cabeçalhos de tabela |
| **Border Dark** | `#1e324a` | Delimitadores sutis de contorno e separadores de grid |
| **Cyber Cyan (Primária)** | `#00d2ff` | Realce principal, traçados do logo, botões de ação e valores destacados |
| **Sky Blue (Secundária)** | `#38bdf8` | Indicadores de foco, badges de versão e estados ativos |
| **Steel Teal (Neutro Técnico)**| `#5c89a6` | Subtítulos técnicos, labels secundárias e dados analíticos |
| **Amber Warning** | `#f59e0b` | Alertas de dissipação térmica e capacidade energética |
| **Emerald Success** | `#10b981` | Integrações ativas, exportação WhatsApp e status nominal |
| **Print Paper (Impressão)** | `#ffffff` | Fundo puro com texto `#0f172a` para emissão do Laudo Técnico ABNT |

### 1.2 Tipografia & Ergonomia
- Fonte Principal: `Inter` (Google Fonts), com pesos 400 (corpo), 500 (médio), 600 (semi-bold) e 700 (bold).
- Layout responsivo adaptado para Desktop, Notebooks de campo e Smartphones/Tablets.

---

## 2. Visão Geral da Arquitetura Multi-Módulos

O InfraSpec v3.0 opera como uma estação de trabalho completa (*Single Page Application* autônoma), estruturada em 5 visões integradas:

```
┌────────────────────────────────────────────────────────────────────────┐
│                        InfraSpec v3.0 - Topbar                         │
│  [Logo IS]  InfraSpec v3.0   [Técnico Ativo: Roberto - (11) 98765...] │
├────────────────────────────────────────────────────────────────────────┤
│  Módulos:                                                              │
│  [1. Cabeamento] [2. Rack & CFTV] [3. Energia] [4. Wi-Fi] [5. Laudo]  │
└────────────────────────────────────────────────────────────────────────┘
       │                 │                │               │
       ▼                 ▼                ▼               ▼
  Cabeamento           CFTV            Nobreak          Wi-Fi
  Horizontal         IP / HD          Senoidal / DPS   6/6E/7
       │                 │                │               │
       └───────────┬─────┴────────────────┴───────────────┘
                   │
                   ▼ (Checkboxes de Interconexão entre Módulos)
       ┌──────────────────────────────────────────────────┐
       │   5. Laudo Consolidado & Memorial Técnico ABNT   │
       │   - Lista de Compras Unificada                   │
       │   - Exportação CSV / WhatsApp / Impressão A4 PDF │
       └──────────────────────────────────────────────────┘
```

---

## 3. Especificação dos Módulos

### 3.1 Módulo 1: Cabeamento Estruturado & Redes (Engine v2.3 Consolidada)
- **Cabeamento Horizontal:** Medição por metragem absoluta de planta ou distância média por ponto RJ45 com margem de subidas/curvas (0 a 50%).
- **Cálculo de Bobinas (305m):** Lances simultâneos de puxamento (mínimo 2 a 4 bobinas) para evitar repuxo mecânico e otimizar tempo de passagem.
- **Conectividade:** Keystones RJ45 Cat6/Cat5e (UTP/FTP), espelhos 4x2 com módulos cegos automáticos, conectores EZ-Crimp passantes com 25% de margem mecânica.
- **Patch Cords Flexíveis:** Modos automáticos (0,5m rack + 2,5m postos) ou sob medida de 0,5m a 3,0m, divididos entre injetados e montagem manual em campo.
- **Validação Térmica de Mini-Racks:** Alerta automático e inclusão preventiva de Kit de Ventilação Forçada com 2 Coolers bivolt para racks $\le 16\text{U}$ com alta densidade PoE.

### 3.2 Módulo 2: Montagem de Rack para Câmeras CFTV
- **Topologia de Câmeras:**
  - Câmeras IP PoE (802.3af/at): Conexão direta em Switch PoE através de cabo UTP, dispensando fiação elétrica dedicada.
  - Câmeras Analógicas HD (MHD / HD-CVI / TVI): Utiliza baluns passivos de vídeo sobre UTP e barramento de alimentação 12V DC.
  - Perfis de Câmeras: Bullet Externa (IP67 com IR longo alcance) e Dome Interna (antivandalismo IK10).
- **Armazenamento (Storage) & NVR/DVR:**
  - Cálculo de capacidade em Terabytes baseado no padrão de compressão H.265:
    $$\text{Storage (TB)} = \left\lceil \frac{\text{Câmeras} \times \text{Bitrate (Mbps)} \times 86.400 \times \text{Dias de Retenção}}{8 \times 10^6 \times 0.90} \right\rceil$$
  - Seleção automática de HDs especializados de vigilância 24/7 (Western Digital Purple / Seagate SkyHawk) de 4TB a 8TB.
- **Acessórios de Instalação e Campo:**
  - Caixas de sobrepor herméticas V Box IP66 por câmera para alojamento estanque de conectores.
  - Baluns com proteção integrada contra surtos (no modo analógico) ou conectores RJ45 blindados (no modo IP).
  - Fonte colmeia chaveada estabilizada de 12V dimensionada com 1.2A por câmera + 25% de folga.
- **Rack CFTV:** Mini-rack 19" de parede com fechadura à chave (6U a 16U) com bandeja para NVR, ou opção de integração direta no rack principal do projeto.

### 3.3 Módulo 3: Identificação & Estimativa Energética (Nobreak, DPS Clamper & Aterramento)
- **Integração de Cargas Automatizada:**
  - Opção de marcar `[x] Importar cargas do Cabeamento Principal` e `[x] Importar cargas do Módulo CFTV`.
  - Soma as cargas ativas (switches com PoE Budget, roteadores, NVR, câmeras, servidores e iluminação de rack).
- **Fórmulas Energéticas:**
  - Potência Ativa Total: $P_{\text{total}} = \sum P_{\text{cargas}} \times 1.25$ (Watts com margem de segurança de 25%).
  - Potência Aparente Mínima: $S_{\text{VA}} = \frac{P_{\text{total}}}{\text{FP}}$, onde $\text{FP} \approx 0.70$ (Fator de Potência típico de fontes de TI).
  - Enquadramento comercial de Nobreak: 1200VA, 1500VA, 2000VA, 2200VA, 3000VA (3kVA) ou 5kVA.
  - Topologia: **Senoidal Puro** (indispensável para equipamentos com PFC ativo e comutação rápida sem ruído).
- **Autonomia & Banco de Baterias:**
  - Seleção de autonomia (15 min, 30 min, 1h, 2h).
  - Indicação de módulo de baterias estacionárias externas seladas com conector de engate rápido tipo Anderson.
- **Proteção Contra Surtos (DPS Clamper):**
  - DPS Classe II para painel elétrico do rack (CLAMPER Front / VCL 20kA/45kA) e réguas iClamper Energia 8 tomadas.
  - Protetores de surto específicos de dados CLAMPER Ethernet RJ45 PoE para câmeras externas e links de operadora.
- **Aterramento Normativo (NBR 5410):**
  - Barra de equipotencialização em cobre para rack 19" com kit de fixação e condutor verde/amarelo 6mm².

### 3.4 Módulo 4: Ampliação da Rede para Pontos Wi-Fi Corporativo
- **Classificação de Ambientes:**
  - Escritório Corporativo (1 AP a cada 80–120 $m^2$ ou a cada 25–35 usuários simultâneos).
  - Alta Densidade / Auditório (1 AP para cada 50–100 conexões com divisão de canais e rádio tri-band).
  - Galpão Logístico / Indústria (antenas de alto ganho com proteção contra interferência de estruturas metálicas).
  - Área Externa / Outdoor (Grau de proteção IP67, resistência a raios UV e surtos atmosféricos).
- **Padrões de Tecnologia:**
  - Wi-Fi 6 (802.11ax), Wi-Fi 6E (banda limpa de 6 GHz) e Wi-Fi 7 (802.11be com canais de 320 MHz).
- **Infraestrutura PoE & Gestão:**
  - Dimensionamento de Switches PoE+ (802.3at de 30W por porta) ou Injetores individuais Gigabit.
  - Opção de Controladora em Nuvem (*Cloud*) ou Appliance físico em rack 1U.
  - Integração opcional para alimentar automaticamente o cabeamento horizontal e portas do rack principal.

---

## 4. Banco de Dados Local & Sistema de Identificação de Usuário

O sistema utiliza a API nativa de `localStorage` do navegador com estrutura relacional desacoplada:

### 4.1 Esquema de Dados

```json
{
  "infraspec_users": [
    {
      "id": "usr_1728210000000",
      "nome": "Eng. Roberto Santos",
      "telefone": "(11) 98765-4321",
      "registro": "CFT 123456-BR",
      "empresa": "Tech Solutions TI",
      "dataCadastro": "2026-10-06T11:00:00.000Z"
    }
  ],
  "infraspec_active_user_id": "usr_1728210000000",
  "infraspec_projects": [
    {
      "id": "proj_1728210000001",
      "userId": "usr_1728210000000",
      "nomeProjeto": "Hospital Samaritano - Ala Sul",
      "cliente": "Hospital Samaritano",
      "dataAtualizacao": "2026-10-06T11:20:00.000Z",
      "modulosAtivos": ["cabeamento", "cftv", "energia", "wifi"],
      "dados": {
        "cabeamento": { ... },
        "cftv": { ... },
        "energia": { ... },
        "wifi": { ... }
      }
    }
  ]
}
```

### 4.2 Recursos do Módulo de Usuário
- **Cadastro Ágil:** Nome Completo e Contato Telefônico (com suporte a máscara do WhatsApp).
- **Assinatura Automática:** Preenchimento instantâneo do Responsável Técnico e Contato em todos os laudos técnicos.
- **Histórico & Gestão de Projetos:** Criação, clonagem, exportação em lote (*backup JSON*) e restauração sem servidor.

---

## 5. Emissão do Laudo Técnico Consolidado (ABNT)

- Impressão nativa via `@media print` formatada especificamente para papel A4 portrait com margens técnicas de 10mm.
- Inclui cabeçalho técnico com logotipo oficial `img/is-logo.jpg`.
- Tabelas quantitativas segmentadas por módulo técnico ativo.
- Declaração de responsabilidade técnica em conformidade com as normas **ABNT NBR 14565**, **ANSI/TIA-568**, **ABNT NBR 5410** e boas práticas de telecomunicações.
- Blocos formais de assinatura do responsável técnico e do contratante.
