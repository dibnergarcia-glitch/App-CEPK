# App CEPK

App web simples para o aluno registrar as notas dos bimestres/trimestres e descobrir **quanto precisa tirar nas próximas avaliações para passar de ano**, com alertas para matérias acumuladas.

> Status: 🚧 em desenvolvimento — estrutura inicial.

## Proposta

- **Público:** alunos do 9º ano do Fundamental ao 3º ano do Médio.
- **Dor:** o aluno só percebe que está em risco no fim do ano, quando não há mais prova para recuperar.
- **Solução:** média automática, nota necessária nas provas restantes e alerta das matérias em risco.

## Decisões do MVP

| Item | Decisão |
| --- | --- |
| Estrutura padrão | 4 bimestres (configurável para 3 trimestres ou 2 semestres) |
| Nota mínima | 6,0 (configurável) |
| Escala | 0 a 10, com pesos opcionais por avaliação |
| Conta de usuário | Sem login; dados no `localStorage` + exportar/importar JSON |
| Stack | HTML + CSS + JavaScript puro, sem build |
| Deploy | Netlify ou Vercel (estático) |

## Escopo do MVP

1. Onboarding: série, estrutura de notas, nota mínima e matérias.
2. Lançamento de notas por matéria e avaliação.
3. Média do período e média anual.
4. "Quanto preciso" na próxima prova e no restante do ano.
5. Alerta de matérias em risco/acumuladas.
6. Simulador "e se eu tirar X?".
7. Backup dos dados (exportar/importar).
8. Layout responsivo, prioridade celular.

Fora do MVP: login/nuvem, notificações, recuperação/final, leitura de boletim por IA, painel para escolas e pagamentos.

## Cálculo

```
Média do período:  M = Σ(nota × peso) / Σ(peso)

Nota necessária:   n = (meta × (P + F) − S) / F
  S = soma ponderada já obtida
  P = peso já lançado
  F = peso que ainda falta
```

- `n ≤ 0`: nota já garantida.
- `n > 10`: impossível apenas com as provas restantes.
- A nota necessária é arredondada **para cima** (6,34 → 6,4).

## Estrutura

```
.
├── index.html          # página inicial provisória
├── assets/styles.css   # estilos base
├── src/                # código do app (próxima etapa)
├── tests/              # testes do motor de cálculo
└── README.md
```

## Como rodar

Não há build. Abra o `index.html` no navegador ou sirva a pasta:

```bash
python3 -m http.server 8000
```

Depois acesse `http://localhost:8000`.

## Roadmap (8 semanas, ~5h/semana)

| Semana | Entrega |
| --- | --- |
| 1 | Validação, landing e estrutura do projeto |
| 2 | Motor de cálculo v1 + testes |
| 3 | Motor v2 (média anual, acumuladas, impossível) + testes |
| 4 | Onboarding e cadastro de matérias |
| 5 | Lançamento de notas + persistência local |
| 6 | Dashboard e alertas de risco |
| 7 | Simulador, responsivo e backup |
| 8 | Beta com alunos, correções e lançamento |

## Privacidade

No MVP os dados ficam apenas no dispositivo do usuário (`localStorage`). Nenhuma informação é enviada a servidores.
