# OpenRGB-Setup

> **Objetivo:**  
> 1️⃣ Instalar o OpenRGB e garantir que ele rode sempre como Administrador.  
> 2️⃣ Instalar o driver *PawnIO* para obter controle total dos LEDs da placa‑mãe.  
> 3️⃣ Integração com scripts e automações(opcional).

---

## 📋 Pré‑requisitos

| Item | Descrição | Como garantir |
|------|-----------|---------------|
| Sistema Operacional | Windows 10/11 (64‑bit) | Certifique‑se de ter privilégios de administrador. |
| Conexão com a Internet | Para baixar os instaladores |  |
| Permissão de UAC | O OpenRGB precisa de acesso elevado | Quando solicitado, clique em **Sim** ou configure o “Run as Administrator” na tarefa do Scheduler. |

---

## 🛠️ Passo 1 – Instalar o OpenRGB

1. **Baixe a última release**  
   ```text
   https://github.com/CalcProgrammer1/OpenRGB/releases/latest
   ```
2. Extraia o arquivo ZIP em `C:\OpenRGB` (ou use o instalador padrão).  
3. **Verifique** que o executável está presente:  
   ```text
   C:\OpenRGB\OpenRGB.exe
   ```

> ⚠️ Se você usar a versão “Portable”, basta descompactar e usar o `OpenRGB.exe`.  
> ✅ *Para uso futuro, copie a pasta completa para `C:\Program Files\OpenRGB`.*

---

## 🔧 Passo 2 – Instalar o driver PawnIO

1. **Baixe** o driver no repositório oficial (ou em outro local confiável).  
   ```text
   https://github.com/paulradu/PawnIO/releases/latest  (exemplo)
   ```
2. Extraia para `C:\PawnIO`.  
3. Abra um Prompt de Comando **como Administrador** e execute o script de instalação:  

   ```cmd
   cd C:\PawnIO
   install.bat     REM ou: pnputil /add-driver PawnIO.inf /install
   ```

4. **Reinicie** a máquina para que o driver seja carregado corretamente.

> 💡 *Depois da reinicialização, abra o Gerenciador de Dispositivos → “Drivers de LED” (ou similar) e verifique se aparece “PawnIO Driver”.*  

---

## 🚀 Passo 3 – Configurar OpenRGB para iniciar como Administrador

### Opção 1: Task Scheduler (recomendado)

| Etapa | Instruções |
|-------|------------|
| Crie uma nova tarefa | `Task Scheduler → Create Basic Task…` |
| Nome da Tarefa | `OpenRGB - Logon Admin` |
| Trigger | **On log on** → *All users* |
| Action | **Start a program** →  
  Path: `C:\Program Files\OpenRGB\OpenRGB.exe` (ou o caminho completo que você extraiu) |
| Configurações avançadas | Marque **Run with highest privileges** e ajuste “Configure for” → Windows 10/11 |
| Salve | Clique em **Finish** |

> ✅ *A tarefa vai abrir automaticamente a cada logon com privilégios de Administrador.*

### Opção 2: Startup Folder + Shortcut

1. Copie `OpenRGB.exe` para a pasta de inicialização:  
   ```text
   %APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup
   ```
2. Clique com o botão direito → **Propriedades** → aba **Compatibilidade** → marque **Executar este programa como administrador**.  
3. Salve e reinicie para testar.

> ⚠️ *Esta segunda opção pode gerar prompts UAC repetidos; Task Scheduler evita isso.*

---

## ✅ Passo 4 – Verificar o funcionamento

1. **Inicie a máquina** (ela deve abrir automaticamente, se você configurou o Scheduler).  
2. Abra o OpenRGB → verifique se todas as LEDs da placa‑mãe aparecem e são controláveis.  
3. Se quiser testar um perfil automático:  

   ```cmd
   "C:\Program Files\OpenRGB\OpenRGB.exe" --profile "%APPDATA%\OpenRGB\<perfil>.orp"
   ```

4. **Logs** – Caso algo não apareça, abra o arquivo de log em `%APPDATA%\OpenRGB\OpenRGB.log` e procure por mensagens como “PawnIO not loaded” ou “Access denied”.

---

## 🛠️ Dicas de Troubleshooting

| Problema | Solução rápida |
|----------|----------------|
| LEDs da placa‑mãe não aparecem no OpenRGB | 1️⃣ Confirme que o driver PawnIO está instalado e carregado (Gerenciador de Dispositivos). <br>2️⃣ Certifique‑se de ter iniciado o OpenRGB como Administrador. |
| UAC sempre pergunta “Esta aplicação quer fazer alterações no seu computador?” | Use a tarefa do Scheduler com “Run with highest privileges”. |
| Driver PawnIO não instala | Execute `pnputil /add-driver PawnIO.inf /install` manualmente em um CMD elevado. |
| Problemas de compatibilidade com BIOS | Verifique se o recurso *RGB control* está habilitado no BIOS (geralmente em “Onboard Devices” → “LED Control”). |

---

## 📜 Estrutura do Documento

```
# Guia de Instalação e Configuração do OpenRGB com PawnIO
- Visão geral
- Pré‑requisitos
- Passo 1 – Instalar o OpenRGB
- Passo 2 – Instalar o driver PawnIO
- Passo 3 – Configurar para iniciar como Administrador
- Verificação final
- Troubleshooting rápido
```

---

### Próximos passos

- **Automação de perfis**: crie um script `.bat` ou use PowerShell para chamar `OpenRGB.exe --profile "<caminho_para_o_perfil>"`.
- **Integração com Task Scheduler**: se quiser que o OpenRGB abra automaticamente ao logar, basta usar a tarefa criada no passo 3.
