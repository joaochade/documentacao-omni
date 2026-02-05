flowchart LR
  subgraph Legend[" "]
    L1["Ação do Cliente B2B"]
    L2["Integração Conexa → Omni"]
    L3["Ação do Usuário Final"]
    L4["Fim do Fluxo"]
  end

  A["Cliente B2B envia/atualiza base de colaboradores na Conexa"] --> B["Conexa identifica colaboradores com benefício Omni ativo"]
  B --> C{"Usuário já existe na Omni?"}
  C -- Não --> D["Criar usuário na Omni<br>POST /v2/users"]
  C -- Sim --> E["Consultar usuário na Omni por CPF<br>GET /v2/users/cpf/cpf"]
  D --> F["Criar/atualizar carteira do usuário<br>POST /v2/wallets"]
  E --> F
  F --> G["Usuário acessa app Conexa e clica em<br>Benefício de Medicamentos"]
  G --> H["Conexa gera link temporário autenticado na Omni<br>POST /v2/temporary-links"]
  H --> I["Conexa abre WebView Omni com link temporário"]
  I --> J{"Usuário realizou teleconsulta<br>e recebeu receita?"}
  J -- Sim --> K["Conexa envia receita para Omni <br>POST /v2/prescriptions/process-urls"]
  J -- Não --> L["Fim: usuário pode navegar no ambiente Omni"]
  K --> M["Fim: receita disponível no ambiente Omni"]

  style L1 fill:#f5f5f5,stroke:#999,stroke-width:2px
  style L2 fill:#e3f2fd,stroke:#42a5f5,stroke-width:2px
  style L3 fill:#e8f5e9,stroke:#66bb6a,stroke-width:2px
  style L4 fill:#fafafa,stroke:#bdbdbd,stroke-width:1px
  style A fill:#f5f5f5,stroke:#999,stroke-width:2px
  style B fill:#e3f2fd,stroke:#42a5f5,stroke-width:2px
  style D fill:#e3f2fd,stroke:#42a5f5,stroke-width:2px
  style E fill:#e3f2fd,stroke:#42a5f5,stroke-width:2px
  style F fill:#e3f2fd,stroke:#42a5f5,stroke-width:2px
  style G fill:#e8f5e9,stroke:#66bb6a,stroke-width:2px
  style H fill:#e3f2fd,stroke:#42a5f5,stroke-width:2px
  style I fill:#e3f2fd,stroke:#42a5f5,stroke-width:2px
  style K fill:#e3f2fd,stroke:#42a5f5,stroke-width:2px
  style L fill:#fafafa,stroke:#bdbdbd,stroke-width:1px
  style M fill:#fafafa,stroke:#bdbdbd,stroke-width:1px
  style Legend fill:#fff,stroke:#ddd,stroke-width:1px
