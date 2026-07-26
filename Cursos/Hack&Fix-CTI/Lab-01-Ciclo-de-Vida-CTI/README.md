
# Laboratório 01: Ciclo de Vida da Inteligência de Ameaças (CTI)
## Visão Geral
Este laboratório tem como objetivo aplicar as 6 fases do Ciclo de Inteligência de Ameaças a um caso real de ataque de ransomware, demonstrando a transição de dados brutos para inteligência acionável.

* **Curso:** Certified Threat Intelligence Analyst (CTIA) - Hack & Fix Academy
* **Estudo de Caso:** Incidentes do Ransomware DragonForce (Scattered Spider)
* **Artefato Anexo:** `CTI.drawio.pdf`

---

## Mapeamento do Ciclo de Inteligência

### 1. Planning & Direction (Planejamento e Direção)
* **Objetivo:** Entender a cadeia de ataque do ransomware DragonForce (operado pelo grupo Scattered Spider) para mitigar e impedir sua propagação futura.
* **Marco Temporal:** Ataque de Abril de 2025.

### 2. Collection (Coleta)
Coleta de telemetria interna e inteligência de fontes abertas/fechadas:
* **Advisories:** CISA Advisory (Scattered Spider/DragonForce) e Trend Micro Research.
* **CVE:** Exploitation da vulnerabilidade CVE-2025-22224.
* **C2 Domains:** `mands-update-portal.com`, `staff-mands-auth.net`.
* **Network Infrastructure:** IPs `185.193.38.12` (exfiltração Mega.nz) e `45.227.253.114` (proxy/túnel SSH).
* **Artefatos:** Hashes SHA256 do payload (`dragon.exe`) e ferramenta de exfiltração (Rclone modificado).

### 3. Processing (Processamento)
Normalização e estruturação dos dados brutos:
* **Normalização Temporal:** Conversão e padronização de todos os timestamps para UTC.
* **Atributos Críticos:** Consolidação da CVE-2025-22224 e patch URLs em planilha técnica para priorização de correção.
* **Catalogação de IoCs:** Extração de hashes para arquivos CSV (`DragonForce-20250424-Hashes.csv`) para facilitação do bloqueio em soluções de EDR.
* **Mapeamento MITRE:** Mapeamento de TTPs para a matriz MITRE ATT&CK.

### 4. Analysis (Análise)
Correlação de eventos e contexto da ameaça:
* **Correlação:** Anomalias de autenticação em hosts ESXi correlacionadas com scripts de automação.
* **VirusTotal Pivoting:** Verificação de hashes no VT, confirmando a propagação do ransomware em múltiplos setores em menos de 48h.
* **Cyber Kill Chain Mapped:**
  * *Initial Access:* Engenharia social (vishing) e exploração da CVE-2025-22224.
  * *Execution:* Deploy do payload `dragon.exe`.
  * *Lateral Movement:* Ferramentas de tunelamento SSH e movimento lateral via Domain Controllers.
  * *Impact:* Criptografia de sistemas de estoque/logística e exfiltração para dupla extorsão.

### 5. Dissemination (Disseminação)
Entrega da inteligência aos stakeholders:
* **Tactical Report:** Relatório técnico enviado ao SOC via e-mail contendo links para patching, hashes SHA256 e assinaturas de rede.
* **Platform Sharing:** Evento criado e publicado na plataforma TIP (MISP) com IoCs e notas detalhadas de TTPs.

### 6. Feedback (Retroalimentação)
* **Problema Identificado:** Bloqueio amplo de conexões SSH gerou falsos positivos em tarefas legítimas de manutenção do SOC.
* **Melhoria para o Próximo Ciclo:** Inclusão de whitelist para IPs de origem conhecidos de nuvem e exigência de *Confidence Score* "Alto" para bloqueio automático de hashes com poucas ocorrências globais (<10x).

---

## Autoavaliação do Laboratório
* **Pontuação:** 10 / 10
* **Critérios Atendidos:** Mapeamento preciso de IoCs/TTPs, rigor técnico na normalização UTC/MITRE ATT&CK e ciclo de feedback acionável para o SOC.
