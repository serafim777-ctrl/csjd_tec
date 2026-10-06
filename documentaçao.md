# CSJD - Documentação do Projeto
# Equipe senai fc : Alisson, Gustavo, Diego ,kaio
## 1. Informações do Projeto

**Nome do projeto:** Breakable

**Engine:** Godot

**Linguagem:** GDScript

**Tipo:** Jogo 2D de plataforma

---

## 2. Integrantes

- Wagner Xavier P
- [Adicionar nome dos outros integrantes]

---

## 3. Repositório

O código-fonte do projeto está armazenado no GitHub.

**Repositório:**

https://github.com/[SEU_USUARIO]/breakable

---

## 4. Jogabilidade

O projeto consiste em um jogo 2D de plataforma no qual o jogador controla um personagem.

O personagem possui movimentação horizontal e capacidade de pular.

### 4.1. Controles

| Tecla | Ação |
|---|---|
| ← | Movimentar para a esquerda |
| → | Movimentar para a direita |
| Espaço | Pular |

### 4.2. Movimentação

O personagem pode se movimentar para os lados utilizando as teclas direcionais.

A velocidade utilizada no projeto é definida pela constante:

```gdscript
## 4.2. Movimentação

O personagem pode se movimentar para a esquerda e para a direita utilizando as teclas direcionais.

A velocidade utilizada no projeto é definida pela constante:

```gdscript
const SPEED = 300.0
```

**Quando o jogador não está pressionando nenhuma direção, o personagem desacelera gradualmente até parar.**

---

## 4.3. Pulo

**O personagem pode pular utilizando a tecla Espaço.**

A força do pulo é definida pela constante:

```gdscript
const JUMP_VELOCITY = -400.0
```

**O pulo só pode ser realizado quando o personagem está no chão.**

---

## 4.4. Gravidade

Quando o personagem não está no chão, a gravidade é aplicada automaticamente:

```gdscript
if not is_on_floor():
    velocity += get_gravity() * delta
```

**Isso faz com que o personagem caia naturalmente depois de realizar um pulo.**

---

# 5. Código Principal

O personagem utiliza o sistema **CharacterBody2D** da Godot.

O código responsável pela movimentação é:

```gdscript
extends CharacterBody2D

const SPEED = 300.0
const JUMP_VELOCITY = -400.0

func _physics_process(delta: float) -> void:
    # Add the gravity.
    if not is_on_floor():
        velocity += get_gravity() * delta

    # Handle jump.
    if Input.is_action_just_pressed("ui_accept") and is_on_floor():
        velocity.y = JUMP_VELOCITY

    # Get the input direction and handle the movement/deceleration.
    var direction := Input.get_axis("ui_left", "ui_right")

    if direction:
        velocity.x = direction * SPEED
    else:
        velocity.x = move_toward(velocity.x, 0, SPEED)

    move_and_slide()
```

---

# 6. Erros e Problemas Encontrados

Durante o desenvolvimento podem ocorrer alguns problemas relacionados à **movimentação, colisão e configuração do projeto**.

## 6.1. Personagem não se movimenta

Uma possível causa é a configuração incorreta das entradas do projeto.

É necessário verificar se as ações utilizadas pelo código estão configuradas em:

**Project > Project Settings > Input Map**

As ações utilizadas são:

- **`ui_left`** — movimentar para a esquerda;
- **`ui_right`** — movimentar para a direita;
- **`ui_accept`** — realizar o pulo.

---

## 6.2. Personagem não pula

O código verifica se o personagem está no chão através da função:

```gdscript
is_on_floor()
```

Por isso, é necessário que o personagem esteja configurado corretamente como **CharacterBody2D** e possua uma colisão adequada.

Também é necessário verificar se existe um **chão com colisão**.

---

## 6.3. Personagem atravessa o chão

Esse problema pode acontecer caso o personagem ou o chão não possua um **CollisionShape2D** configurado corretamente.

### Para corrigir:

1. **Adicionar um CollisionShape2D ao personagem.**
2. **Adicionar uma colisão ao chão.**
3. **Verificar se as formas de colisão estão posicionadas corretamente.**
4. **Verificar as camadas e máscaras de colisão.**

---

## 6.4. Movimento muito rápido ou muito lento

A velocidade do personagem pode ser alterada através da constante:

```gdscript
const SPEED = 300.0
```

### Para deixar o personagem mais lento:

```gdscript
const SPEED = 200.0
```

### Para deixar o personagem mais rápido:

```gdscript
const SPEED = 400.0
```

---

# 7. Incrementos e Melhorias

Como melhorias futuras para o projeto, podem ser adicionados **novos elementos de jogabilidade**.

## 7.1. Animações

Adicionar animações para diferentes estados do personagem:

- **Idle** — personagem parado;
- **Run** — personagem correndo;
- **Jump** — personagem pulando;
- **Fall** — personagem caindo.

---

## 7.2. Inimigos

Adicionar inimigos que possam se movimentar pelo mapa e causar dano ao jogador.

Os inimigos podem possuir **diferentes comportamentos e níveis de dificuldade**.

---

## 7.3. Sistema de Vida

Adicionar uma quantidade de vidas ou pontos de vida para o personagem.

### Exemplo:

**Vida do jogador:**

❤️ ❤️ ❤️

Quando o jogador sofrer dano, **uma quantidade de vida será perdida**.

---

## 7.4. Sistema de Pontuação

Adicionar um sistema de pontuação para recompensar o jogador por determinadas ações.

O jogador poderá ganhar pontos ao:

- **Coletar moedas;**
- **Derrotar inimigos;**
- **Completar fases;**
- **Encontrar itens;**
- **Superar determinados obstáculos.**

---

## 7.5. Novas Fases

Criar novas fases com **diferentes obstáculos, inimigos e desafios**.

Cada fase poderá apresentar um **nível de dificuldade diferente**.

---

## 7.6. Menu Inicial

Criar um menu inicial com opções como:

- **Jogar**
- **Configurações**
- **Créditos**
- **Sair**

---

## 7.7. Sons e Músicas

Adicionar efeitos sonoros para diferentes ações do jogo.

### Exemplos:

- **Som de pulo;**
- **Som de queda;**
- **Som de dano;**
- **Som de coleta de itens;**
- **Som de derrota de inimigos.**

Também poderá ser adicionada uma **música de fundo**.

---

# 8. Melhorias Futuras

| **Melhoria** | **Status** |
|---|---|
| Movimentação do personagem | ✅ **Concluído** |
| Sistema de pulo | ✅ **Concluído** |
| Gravidade | ✅ **Concluído** |
| Colisão com o chão | 🔄 **Em desenvolvimento** |
| Animação do personagem | ⏳ **Futuro** |
| Inimigos | ⏳ **Futuro** |
| Sistema de vida | ⏳ **Futuro** |
| Sistema de pontuação | ⏳ **Futuro** |
| Novas fases | ⏳ **Futuro** |
| Menu inicial | ⏳ **Futuro** |
| Sons e músicas | ⏳ **Futuro** |

---

# 9. Estrutura do Projeto

A estrutura do projeto poderá ser organizada da seguinte maneira:

```text
Breakable/
│
├── project.godot
├── README.md
├── documentacao.md
│
├── cenas/
│   └── fase1.tscn
│
├── scripts/
│   └── personagem.gd
│
├── sprites/
│
└── audio/
```

---

# 10. Tecnologias Utilizadas

O projeto utiliza as seguintes tecnologias:

| **Tecnologia** | **Utilização** |
|---|---|
| **Godot Engine** | Desenvolvimento do jogo |
| **GDScript** | Programação |
| **Git** | Controle de versão |
| **GitHub** | Armazenamento e compartilhamento do projeto |

---

# 11. Controle de Versão

O projeto será desenvolvido utilizando **Git** e **GitHub** para controlar as versões do código.

As alterações realizadas durante o desenvolvimento poderão ser registradas através de **commits**.

### Exemplos de commits:

```text
feat: adiciona movimentação do personagem
feat: adiciona sistema de pulo
fix: corrige colisão com o chão
fix: corrige movimentação do personagem
feat: adiciona inimigos
feat: adiciona sistema de vida
```


