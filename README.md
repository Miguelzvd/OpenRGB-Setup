# OpenRGB Setup Guide

> **Objetivo**
> Configurar o **OpenRGB** para:
>
> * controlar os LEDs do sistema
> * iniciar automaticamente com o Windows
> * carregar um perfil RGB automaticamente no boot

---

# 📋 Pré-requisitos

| Item                | Descrição                              |
| ------------------- | -------------------------------------- |
| Sistema Operacional | Windows 10 ou Windows 11 (64-bit)      |
| Permissões          | Conta com privilégios de administrador |
| Internet            | Necessária para baixar o OpenRGB       |

---

# 🛠️ Passo 1 – Instalar o OpenRGB

1. Baixe a versão mais recente:

```text
https://github.com/CalcProgrammer1/OpenRGB/releases/latest
```

2. Extraia o arquivo.

3. Coloque a pasta em:

```text
C:\Program Files\OpenRGB
```

4. Verifique se o executável existe:

```text
C:\Program Files\OpenRGB\OpenRGB.exe
```

---

# 🎨 Passo 2 – Criar ou carregar um perfil RGB

1. Abra o **OpenRGB**.
2. Configure as cores desejadas.
3. Vá em:

```
Profiles → Save Profile
```

4. Salve o perfil.

Exemplo:

```
Blue
```

O perfil será salvo automaticamente em:

```text
%APPDATA%\OpenRGB\Profiles
```

---

# 🚀 Passo 3 – Testar carregamento do perfil via comando

Antes de configurar a inicialização automática, teste o comando manualmente.

Abra **PowerShell** e execute:

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --noautoconnect -p Blue
```

### Parâmetros usados

| Parâmetro         | Função                                |
| ----------------- | ------------------------------------- |
| `--noautoconnect` | Evita tentar conectar ao servidor SDK |
| `-p Blue`         | Carrega o perfil chamado **Blue**     |

Se o RGB for aplicado corretamente, o comando está funcionando.

---

# ⚡ Passo 4 – Ativar inicialização automática

O próprio OpenRGB pode configurar o autostart.

Execute uma vez:

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --autostart-enable "--startminimized --noautoconnect -p Blue"
```

Isso fará o OpenRGB:

* iniciar automaticamente com o Windows
* iniciar **minimizado**
* carregar o perfil **Blue**

---

# 🔍 Verificar se o autostart está ativo

Execute:

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --autostart-check
```

Saída esperada:

```
Autostart enabled
```

---

# 🧪 Teste final

1. Reinicie o computador.
2. Aguarde o Windows iniciar.
3. Verifique se:

* o OpenRGB iniciou automaticamente
* o perfil **Blue** foi aplicado

---

# ⚠️ Observações

Alguns sistemas podem mostrar mensagens como:

```
Failed to load SmbusI801.bin
Failed to load SmbusNCT6793.bin
```

Isso significa apenas que o OpenRGB não conseguiu acessar alguns controladores SMBus da placa-mãe.

Na maioria dos casos:

✅ isso **não impede o funcionamento do RGB**

---

# 📂 Estrutura final

```
OpenRGB Setup
│
├─ Instalação do OpenRGB
├─ Criação de perfil RGB
├─ Teste do comando de carregamento
├─ Configuração de autostart
└─ Teste final
```

---

# 💡 Dica extra (opcional)

Para inicialização ainda mais rápida, é possível usar:

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --startminimized --noautoconnect --nodetect -p Blue
```

`--nodetect` reduz o tempo de inicialização do OpenRGB.

---

✅ **Seu setup agora está:**

* automático no boot
* carregando o perfil correto
* sem scripts externos
* usando apenas recursos nativos do OpenRGB

---

## 🧰 Comandos úteis do OpenRGB

### Mostrar ajuda

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --help
```

---

### Mostrar versão

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --version
```

---

### Listar dispositivos RGB

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --list-devices
```

---

### Carregar perfil

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --noautoconnect -p Blue
```

---

### Salvar perfil atual

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --save-profile MeuPerfil.orp
```

---

### Iniciar minimizado

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --startminimized
```

---

### Ativar inicialização automática

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --autostart-enable "--startminimized --noautoconnect -p Blue"
```

---

### Verificar autostart

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --autostart-check
```

---

### Desativar autostart

```powershell
& "C:\Program Files\OpenRGB\OpenRGB.exe" --autostart-disable
```

---

💡 **Dica:** use sempre `--noautoconnect` ao carregar perfis para evitar erros de conexão SDK.

