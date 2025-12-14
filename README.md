# 🛡️ LockCode V3 - Macro API Documentation

![Lua Version](https://img.shields.io/badge/Lua-5.1-blue.svg?style=for-the-badge&logo=lua)
![Platform](https://img.shields.io/badge/Platform-MTA%3ASA-green.svg?style=for-the-badge&logo=grand-theft-auto)
![Security Level](https://img.shields.io/badge/Security-Alien_Grade-red.svg?style=for-the-badge&logo=shield)

O **LockCode V3** oferece um sistema avançado de macros que permite aos desenvolvedores controlar o equilíbrio exato entre **Segurança Máxima** e **Performance Extrema**.

> **🔄 Nota de Compatibilidade:** Para facilitar a migração, todos os macros abaixo aceitam o prefixo `LPH_` (ex: `LPH_NO_VIRTUALIZE`), mantendo compatibilidade total com scripts legados do Luraph.

---

## ⚡ Performance & Otimização

Use estes macros para códigos que exigem execução em tempo real, como renderização gráfica ou cálculos físicos intensivos.

### `LOCK_NO_VIRTUALIZE(function)`
**Alias:** `LOCK_JIT`

Instrui o compilador a **não virtualizar** a função alvo. O código resultante será minificado e levemente protegido, mas rodará na velocidade nativa da CPU/Lua JIT.

* **Uso Ideal:** Loops `onClientRender`, cálculos matemáticos pesados, `while true do`.
* **Segurança:** 🟡 Média (Lógica preservada, apenas minificada).
* **Performance:** 🟢 Nativa (Máxima).

```lua
-- Exemplo: Renderização rodando a 144 FPS sem lag
addEventHandler("onClientRender", root, LOCK_NO_VIRTUALIZE(function()
    local x, y = guiGetScreenSize()
    dxDrawText("LockCode Protected", x/2, y/2)
end))
````

-----

## 🔒 Segurança & Criptografia

Ferramentas pesadas para proteger seus segredos, lógica de negócios e propriedade intelectual.

### `LOCK_ENCFUNC(function)`

**"O Fantasma"**. A função é compilada, transformada em bytecode, criptografada com chaves polimórficas e armazenada como uma string segura. Ela só é descriptografada e carregada na memória (`loadstring`) no exato milissegundo em que é chamada.

  * **Uso Ideal:** Sistemas de Login, Anti-Cheats, Banimentos, Lógica de Admin.
  * **Segurança:** 🟣 Extrema (Código inexistente na memória até a execução).

<!-- end list -->

```lua
local verificarAdmin = LOCK_ENCFUNC(function(player)
    -- Esta lógica é invisível para dumpers estáticos
    if getElementData(player, "admin_level") > 5 then
        triggerServerEvent("openAdminPanel", player)
    end
end)
```

### `LOCK_ENCNUM(number)`

**"Matemática Alienígena"**. Transforma um número simples em uma expressão matemática polimórfica complexa (MBA - Mixed Boolean-Arithmetic) impossível de simplificar visualmente.

  * **Transformação:** `100` ➔ `((50 * 942) + (100 - 0)) / 942 ...`
  * **Uso Ideal:** Esconder IDs de itens, preços, senhas numéricas ou chaves de API.

<!-- end list -->

```lua
-- O hacker verá uma equação gigante, não o número 999
local superSecretID = LOCK_ENCNUM(999) 
```

### `LOCK_ENCSTR(string)`

**"O Cofre"**. Força a criptografia pesada de uma string específica (Heap Encryption), mesmo que ela esteja dentro de um bloco de alta performance (`LOCK_NO_VIRTUALIZE`).

  * **Uso Ideal:** Tokens, Webhooks, URLs e Mensagens Secretas.

<!-- end list -->

```lua
LOCK_NO_VIRTUALIZE(function()
    -- Função rápida, mas a string está blindada
    local webhook = LOCK_ENCSTR("https://discord.com/api/webhooks/...")
    sendToDiscord(webhook)
end)
```

-----

## ⚙️ Controle de Fluxo & Lógica

### `LOCK_CRASH()`

Gera uma instrução de bytecode corrompida ou um loop infinito matemático que causa o fechamento imediato do jogo (Crash to Desktop) se a linha for executada.

  * **Uso Ideal:** Armadilhas (Honeypots) dentro de verificações de Anti-Tamper.

<!-- end list -->

```lua
if isDebugHooked() then
    LOCK_CRASH() -- Adeus, jogo.
end
```

### `LOCK_OBFUSCATED`

Uma constante booleana que retorna `true` apenas quando o script está compilado/protegido. Útil para separar lógica de desenvolvimento e produção.

```lua
if LOCK_OBFUSCATED then
    iniciarSistemaSeguro()
else
    print("⚠️ AVISO: Rodando em modo DEV (Sem proteção)")
end
```

-----

## 🛠️ Utilitários

### `LOCK_NO_UPVALUES(function)`

Cria um *wrapper* (closure) ao redor da função para isolar seu escopo. Isso garante que a função não acesse variáveis locais externas (Upvalues), prevenindo bugs de memória em scripts complexos.

-----

## 📊 Resumo Rápido

| Macro | Função Principal | Impacto FPS | Segurança |
| :--- | :--- | :---: | :---: |
| `LOCK_NO_VIRTUALIZE` | Execução Nativa | 🟢 | 🟡 |
| `LOCK_ENCFUNC` | Criptografia Lazy-Load | 🔴 | 🟣 |
| `LOCK_ENCNUM` | MBA (Matemática) | 🟡 | 🟢 |
| `LOCK_ENCSTR` | Criptografia de String | 🟡 | 🟢 |
| `LOCK_CRASH` | Crashar Cliente | N/A | N/A |

-----

Protected by **LockCode V3 Engine**. Built for the Elite.
