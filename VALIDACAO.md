# Validação — GoodWe ChargeGrid Intelligence

## 1. Objetivo

Este documento registra os principais testes e critérios de validação utilizados para avaliar o protótipo da Sprint 3.

A validação considera separadamente:

- Dashboard Web;
- Eletroposto 3D;
- gerenciamento energético;
- fluxo da sessão de recarga;
- funcionalidades simuladas.

---

# 2. Critérios de interpretação

Os resultados são classificados como:

- **OK:** comportamento observado de acordo com o esperado;
- **OK — Simulação:** comportamento demonstrado localmente, sem integração física;
- **Planejado:** funcionalidade prevista para evolução futura;
- **Não aplicável:** não faz parte do escopo implementado nesta Sprint.

---

# 3. Validação do Dashboard Web

## 3.1 Painel Geral

**Objetivo:** verificar se a aplicação apresenta uma visão geral da operação.

**Procedimento:**
1. acessar o Dashboard;
2. abrir o Painel Geral;
3. verificar indicadores, sessões e informações operacionais.

**Resultado esperado:** indicadores e dados simulados são exibidos corretamente.

**Status:** OK — Simulação.

---

## 3.2 Balanceamento

**Objetivo:** verificar a representação da distribuição de potência.

**Procedimento:**
1. acessar a área de Balanceamento;
2. observar potência dos carregadores;
3. verificar o limite de rede utilizado pelo cenário;
4. acompanhar a distribuição apresentada.

**Resultado esperado:** o Dashboard apresenta a demanda e a potência distribuída de acordo com o cenário simulado.

**Status:** OK — Simulação.

---

## 3.3 Estações

**Objetivo:** verificar a visualização dos carregadores.

**Procedimento:**
1. acessar Estações;
2. selecionar uma estação;
3. verificar potência, status, veículo e informações da sessão.

**Resultado esperado:** os dados do carregador são apresentados.

**Status:** OK — Simulação.

---

## 3.4 Logs

**Objetivo:** verificar a geração e apresentação dos eventos operacionais.

**Eventos observados:**

- `BootNotification`;
- `Heartbeat`;
- `StartTransaction`;
- `StopTransaction`;
- `StatusNotification`;
- `MeterValues`;
- `Authorize`;
- Load Balancing.

**Resultado esperado:** os eventos aparecem no histórico do Dashboard.

**Status:** OK — Simulação.

**Limitação:** os eventos são locais e não correspondem a mensagens OCPP transmitidas por um carregador físico.

---

## 3.5 IA & Previsão

**Objetivo:** verificar a apresentação dos indicadores e insights de previsão.

**Resultado esperado:** gráficos e informações de previsão são apresentados.

**Status:** OK — Demonstração.

**Limitação:** não há modelo de Machine Learning treinado e validado conectado ao sistema.

---

## 3.6 Simulador "E Se...?"

**Objetivo:** verificar a alteração de parâmetros e comparação de cenários.

**Parâmetros avaliados:**

- quantidade de carregadores;
- consumo base;
- limite contratado;
- veículos simultâneos;
- geração solar.

**Resultado esperado:** os indicadores do cenário são recalculados de acordo com os parâmetros.

**Status:** OK — Simulação.

**Limitação:** economia, ROI e demais resultados são estimativas matemáticas.

---

## 3.7 Faturamento

**Objetivo:** verificar a apresentação de valores financeiros da operação.

**Resultado esperado:** informações de receita e faturamento são exibidas.

**Status:** OK — Simulação.

**Limitação:** não existe processamento financeiro real.

---

# 4. Validação do Eletroposto 3D

## 4.1 Carregamento do ambiente

**Objetivo:** verificar se o modelo 3D é carregado corretamente.

**Arquivos necessários:**

```text
index_V8_1_SPRINT3.html
ChargeGrid_Web.glb
```

**Procedimento:**
1. colocar os dois arquivos na mesma pasta;
2. iniciar servidor HTTP local;
3. acessar o arquivo HTML.

**Resultado esperado:** ambiente 3D e modelo do eletroposto são carregados.

**Status:** OK.

---

# 5. Validação do fluxo da sessão

O fluxo avaliado é:

```text
Identificação
→ Configuração
→ Pagamento
→ Liberação
→ Retirada
→ Conexão
→ Carregamento
→ Distribuição
→ Encerramento
→ Devolução
→ Travamento
```

## 5.1 Identificação

**Objetivo:** iniciar a sessão a partir da identificação do usuário.

**Resultado esperado:** o fluxo permite avançar para a configuração.

**Status:** OK — Simulação.

## 5.2 Configuração

**Objetivo:** selecionar/configurar a sessão de recarga.

**Resultado esperado:** a sessão é preparada para carregamento.

**Status:** OK — Simulação.

## 5.3 Pagamento

**Objetivo:** representar a etapa de pagamento antes da liberação.

**Resultado esperado:** a interface permite demonstrar a etapa de pagamento.

**Status:** OK — Simulação.

**Limitação:** não há transação PIX ou cartão real.

## 5.4 Liberação da trava

**Objetivo:** representar a liberação do conector.

**Resultado esperado:** o fluxo avança para a retirada.

**Status:** OK — Simulação.

## 5.5 Retirada e conexão

**Objetivo:** demonstrar a retirada do conector e conexão ao EV 03.

**Resultado esperado:** o conector é apresentado como conectado ao veículo.

**Status:** OK — Simulação.

## 5.6 Carregamento

**Objetivo:** iniciar a sessão de carregamento.

**Resultado esperado:** tempo, energia e informações da sessão são atualizados.

**Status:** OK — Simulação.

## 5.7 Distribuição energética

**Objetivo:** demonstrar o gerenciamento da potência entre os veículos.

**Resultado esperado:** a potência disponível é distribuída conforme as regras da simulação.

**Status:** OK — Simulação.

## 5.8 Encerramento

**Objetivo:** finalizar a sessão.

**Resultado esperado:** o carregamento é encerrado e o fluxo segue para devolução.

**Status:** OK — Simulação.

## 5.9 Devolução e travamento

**Objetivo:** concluir a operação física simulada.

**Resultado esperado:** o conector retorna à posição e o eletroposto é apresentado como travado.

**Status:** OK — Simulação.

---

# 6. Validação energética

## 6.1 Limite da rede

O protótipo 3D utiliza:

**35 kW**

como limite de rede do cenário.

O consumo base do prédio é:

**32 kW**

Isso deixa uma margem simulada de aproximadamente:

**3 kW**

antes de considerar outras fontes ou estratégias de gerenciamento.

O objetivo da demonstração é justamente mostrar como geração solar, Battery ESS e gerenciamento da potência dos veículos podem ser considerados para administrar esse cenário.

---

## 6.2 Battery ESS

Parâmetros utilizados:

- capacidade: **60 kWh**;
- SOC inicial: **72%**.

**Objetivo:** representar armazenamento como elemento do cenário energético.

**Status:** OK — Simulação.

---

## 6.3 Veículos

| Veículo | Potência máxima simulada |
|---|---:|
| EV 01 | 18 kW |
| EV 02 | 12 kW |
| EV 03 Econômico | 20 kW |
| EV 03 Rápido | 28 kW |

**Status:** OK — Simulação.

---

# 7. Validação do Peak Shaving

**Cenário:**

```text
Demanda elevada
      ↓
Detecção
      ↓
Peak Shaving
      ↓
Redução da potência
      ↓
Menor demanda
```

**Objetivo:** verificar se o Dashboard consegue demonstrar a redução temporária da potência de carregadores em modo econômico.

**Resultado esperado:** potência reduzida e evento registrado nos logs simulados.

**Status:** OK — Simulação.

---

# 8. Validação da atualização dinâmica

**Objetivo:** verificar se os dados do Dashboard são atualizados dinamicamente.

**Procedimento:**
1. manter o Dashboard aberto;
2. observar sessões, potência, carga e indicadores;
3. acompanhar as alterações ao longo do tempo.

**Resultado esperado:** os dados simulados são atualizados aproximadamente a cada 2 segundos.

**Status:** OK — Simulação.

---

# 9. Validação das tecnologias

## Dashboard

| Item | Validação |
|---|---|
| React | OK |
| TypeScript | OK |
| Vite | OK |
| Tailwind CSS | OK |
| Recharts | OK |
| React Router | OK |
| Leaflet | OK |
| Vitest | Disponível no projeto |

## Eletroposto 3D

| Item | Validação |
|---|---|
| HTML | OK |
| CSS | OK |
| JavaScript | OK |
| Three.js | OK |
| GLTFLoader | OK |
| PointerLockControls | OK |
| GLB | OK |

---

# 10. Limitações dos testes

Os testes da Sprint 3 validam principalmente o comportamento do protótipo.

Não foram validados como integração física:

- comunicação com carregador GoodWe;
- comunicação OCPP real;
- CSMS;
- Edge Gateway/Raspberry Pi;
- pagamentos reais;
- banco de dados persistente;
- telemetria física;
- modelo de Machine Learning treinado;
- validação energética em campo.

Portanto, os resultados devem ser interpretados como **validação funcional do protótipo e das simulações**, e não como homologação de uma instalação comercial real.

---

# 11. Critérios finais

| Critério | Resultado |
|---|---|
| Dashboard disponível | **OK** |
| Eletroposto 3D funcional | **OK** |
| Modelo GLB carregado | **OK** |
| Fluxo de recarga demonstrado | **OK — Simulação** |
| Distribuição energética | **OK — Simulação** |
| Geração solar | **OK — Simulação** |
| Battery ESS | **OK — Simulação** |
| EV 01 / EV 02 / EV 03 | **OK — Simulação** |
| Peak Shaving | **OK — Simulação** |
| Logs | **OK — Simulação** |
| IA/Previsão | **OK — Demonstração** |
| Pagamento real | **Planejado** |
| OCPP real | **Planejado** |
| Integração física | **Planejado** |

---

# 12. Conclusão

A Sprint 3 apresenta um protótipo funcional capaz de demonstrar a proposta central do GoodWe ChargeGrid Intelligence: **coordenar a recarga de veículos elétricos considerando a capacidade energética disponível e diferentes fontes e cargas do ambiente comercial**.

O Dashboard demonstra a camada de gestão e monitoramento, enquanto o Eletroposto 3D demonstra a operação física/simulada da sessão de recarga.

A validação confirma o funcionamento das principais demonstrações previstas para o protótipo, mantendo explícita a distinção entre funcionalidades implementadas em simulação e integrações que permanecem como evolução futura.
