# Duelo AFK

**Um jogo de duelo para 2 jogadores no terminal, feito só com Python puro.** Sem Pygame, sem bibliotecas externas e sem IA: apenas a biblioteca padrão (`random`, `time` e `dataclasses`).

*English summary: a two-player auto-battler for the terminal, written in pure Python with only the standard library, no game engine or external packages. Players pick a weapon, fight automatic duels, earn coins and spend them in a shop with a forge and a rarity-based rune system. First to 10 wins.*

## Por que ele existe
Em 2024 já existiam o Pygame, outros motores de jogo e a IA para gerar código. Eu me desafiei a fazer tudo na mão: o laço do jogo, as regras, a loja, a economia e o balanceamento, do meu jeito e com o mínimo de ferramentas. O que mais me orgulha nele são as decisões de design.

## Como se joga
1. Cada jogador digita o nome e escolhe uma arma: **Adaga, Espada, Machado, Alabarda ou Clava**. O dano base é sorteado entre 5 e 10, e fica escondido até a luta.
2. Começa um **duelo automático**: vence quem tiver o maior dano total (arma + runa). Cada golpe é narrado ("um golpe *avassalador*…").
3. Os dois recebem **moedas**: 30 para quem venceu, 20 para quem perdeu, 20 para cada um no empate.
4. Na **loja**, cada jogador escolhe uma opção:

| Opção | Custo | Efeito |
|---|---|---|
| **Forja** | 40 moedas | Aprimora a arma: +20 a 30 de dano, garantido |
| **Runa** | 20 moedas | Sorteia uma runa de 5 a 35 de dano bônus |
| **Pular** | — | Guarda as moedas para a próxima rodada |

5. Os duelos continuam até alguém chegar a **10 vitórias** e "liderar o mundo".

### As runas

| Runa | Dano bônus |
|---|---|
| Arqueológica | 5 a 9 |
| Mágica | 10 a 19 |
| Sombria | 20 a 29 |
| Ancestral | 30 a 35 |

Se a runa sorteada for pior que a equipada, ela é descartada: a runa nunca piora a sua arma, mas você pode pagar e não melhorar.

## As decisões de design (o balanceamento)
- **Quem perde também ganha moedas (20 contra 30).** A diferença é pequena de propósito: quem está atrás consegue reagir na loja, e a partida não fica decidida cedo.
- **Forja × Runa é uma escolha de risco.** A Forja custa o dobro, mas o ganho é garantido. A Runa é barata e pode vir Ancestral, ou ser descartada.
- **O dano fica escondido** ("??? Lute para revelar") até o confronto. Você decide na loja sem saber exatamente quanto o adversário melhorou.
- **Compras consistentes.** Se o segundo jogador digita algo inválido na loja, a compra do primeiro é desfeita e os dois escolhem de novo. O estado do jogo nunca fica pela metade.

## Rodar
Precisa só do Python 3.

```bash
python dueloafk.py
```

No Windows, também dá para usar o executável em `Play Duelo AFK/dueloafk.exe`, gerado com PyInstaller.

## Estrutura do código

| Arquivo | O que faz |
|---|---|
| `dueloafk.py` | Ponto de entrada |
| `classes.py` | `Arma`, `Runas` e `Jogador` (dataclasses) |
| `funcoes.py` | O laço do jogo: nomes, armas, confronto, status e loja |
| `utilitarios.py` | Validação de entrada, regras, arsenal e loja |

A loja, as runas e as armas são separadas em classes e funções próprias, para dar para reaproveitar a lógica e acrescentar itens e regras sem reescrever o jogo.

## Próximos passos
Versão atual: alfa 1.0 (junho de 2024). Ideias para a próxima versão:
- trocar de arma na loja;
- armas com características próprias, além do dano;
- partidas mais longas.

Tudo continuando em Python puro.
