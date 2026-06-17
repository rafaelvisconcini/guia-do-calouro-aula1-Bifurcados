# Como contribuir com o códex

Este guia explica como adicionar a sua dica sem quebrar nada nem atropelar os colegas no Git.
Leia uma vez com calma; depois vira rotina.

## Antes de tudo: o repositório do seu grupo (uma vez por grupo)

O trabalho do grupo acontece em um **fork** do repositório do professor.

1. **Um integrante** (o Mantenedor da Aula 1) abre o repositório do professor e clica em **Fork**
   (canto superior direito). O fork nasce na conta dele e passa a ser o repositório do grupo.
2. Ainda no fork, esse integrante vai em **Settings > Collaborators** e adiciona os **outros dois**
   colegas pelo @usuario. Eles recebem um convite e precisam **aceitar**.
3. Os outros dois **não forkam**. Eles trabalham no fork do grupo, clonando direto (abaixo).

Só o dono do fork pode mudar as configurações do repositório. Os colegas, como colaboradores, podem
clonar, criar branches, abrir PRs, revisar e mergear.

## As regras de ouro

1. Você nunca trabalha direto na `main`. Sempre crie uma branch.
2. Um verbete por arquivo, dentro de `/verbetes`.
3. Toda mudança entra por Pull Request (PR) e é revisada por um colega.
4. O guia só fala de coisa pública e verdadeira. Sem dados privados, sem ofensa. O repositório é público.

## Anatomia de um verbete

Cada verbete segue o [`verbetes/MODELO.md`](verbetes/MODELO.md): título, categoria, resumo, onde fica,
horário, custo, dica de ouro e cilada.

Nome do arquivo: minúsculas, sem acento, hífen no lugar de espaço.

- Certo: `cantina-ipolon-i.md`, `onibus-circular.md`
- Errado: `Cantina Ipolon I.md`, `ônibus.md`

## O fluxo, passo a passo

Na Aula 1 a base das branches é a `main`. A partir da Aula 2 passa a ser a `develop`.

```bash
# 1. Clone o fork do grupo (URL no botao verde "Code" do fork)
git clone git@github.com:DONO-DO-FORK/guia-do-calouro.git
cd guia-do-calouro

# 2. Garanta que sua main esta atualizada
git switch main
git pull origin main

# 3. Crie a sua branch
git switch -c feature/cantina-ipolon-i

# 4. Crie o verbete a partir do modelo e edite
cp verbetes/MODELO.md verbetes/cantina-ipolon-i.md
code verbetes/cantina-ipolon-i.md

# 5. NAO esqueca: adicione a linha do verbete no verbetes/INDEX.md,
#    logo abaixo da linha marcada (todos adicionam no MESMO ponto)

# 6. Veja, prepare e salve
git status
git add verbetes/cantina-ipolon-i.md verbetes/INDEX.md
git commit -m "Adiciona verbete da cantina do Ipolon I"

# 7. Envie a branch
git push -u origin feature/cantina-ipolon-i
```

Depois, **abra o Pull Request pela web**: logo após o push, o GitHub mostra o botão
**Compare & pull request**. Escolha a base `main`, descreva pelo template e crie. Peça revisão a um
colega; quando ele aprovar, o Mantenedor faz o merge.

## Mensagens de commit decentes

Escreva no imperativo, dizendo o que muda:

- Certo: `Adiciona verbete dos laboratórios da Sede`, `Corrige horário da cantina do Ipolon II`
- Errado: `att`, `mudei umas coisas`

## Padrão de branches

| Tipo | Nome | Exemplo |
| --- | --- | --- |
| Novo verbete | `feature/<slug>` | `feature/biblioteca-central` |
| Correção | `fix/<slug>` | `fix/horario-cantina` |
| Só índice/organização | `chore/<slug>` | `chore/ordena-indice` |

## Quando der conflito (vai dar, no INDEX.md)

Conflito não é erro: é o Git avisando que duas pessoas mexeram no mesmo lugar. Para resolver, traga a
`main` para dentro da sua branch e arrume no VS Code:

```bash
git switch feature/sua-branch
git fetch origin
git merge origin/main      # aqui aparece o conflito no INDEX.md
# No VS Code: Accept Current / Incoming / Both Changes.
# No INDEX.md, quase sempre e "Accept Both" (manter as duas linhas).
git add verbetes/INDEX.md
git commit                 # confirma a resolucao
git push
```

## Definição de "pronto"

Seu PR está pronto para mergear quando:

- [ ] O verbete segue o `MODELO.md`.
- [ ] A linha dele está no `INDEX.md`, na categoria certa.
- [ ] Você releu o próprio diff (aba **Files changed**).
- [ ] Um colega revisou e aprovou.
