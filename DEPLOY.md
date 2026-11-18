# Deploy no Streamlit Community Cloud — passo a passo para a prova

## 0. Antes da prova (faça em casa!)
- [ ] Ter conta no **GitHub** e saber a senha
- [ ] Entrar em **share.streamlit.io** com "Continue with GitHub" e autorizar
- [ ] Fazer um deploy de teste com esta pasta, para não descobrir problema na hora

## 1. Conferir a pasta do projeto
A pasta precisa ter, **todos juntos no mesmo nível**:

```
prova-streamlit/
├── app.py             <- o código
├── requirements.txt   <- as bibliotecas
└── dados.csv          <- o arquivo de dados da prova (ou .xlsx)
```

`requirements.txt`:
```
streamlit
pandas
plotly
```
**Se o arquivo da prova for Excel (.xlsx), adicione uma linha `openpyxl`.**

## 2. Testar no computador
No terminal, dentro da pasta:
```
pip install -r requirements.txt
streamlit run app.py
```
Abriu no navegador e os gráficos aparecem? Feche com **Ctrl + C**.

## 3. Mandar para o GitHub

### Jeito A — pelo site (mais rápido, sem usar git)
1. github.com → botão **+** (canto superior direito) → **New repository**
2. Nome: ex. `prova-streamlit` → marque **Public** → **Create repository**
3. Clique em **uploading an existing file**
4. Arraste `app.py`, `requirements.txt` e o arquivo de dados → **Commit changes**

### Jeito B — pelo terminal (igual ao guia do professor)
```
git init
git add .
git commit -m "Commit inicial da aplicacao Streamlit"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git
git push -u origin main
```

## 4. Fazer o deploy
1. Entre em **share.streamlit.io** (login com GitHub)
2. **Create app** → **Deploy a public app from GitHub** (ou "Yup, I have an app")
3. Preencha:

| Campo          | O que colocar                     |
|----------------|-----------------------------------|
| Repository     | `SEU_USUARIO/prova-streamlit`     |
| Branch         | `main`                            |
| Main file path | `app.py`                          |
| App URL        | (opcional) um nome para o link    |

4. **Deploy!** → espere 1 a 3 minutos → copie o link `....streamlit.app` e entregue

## 5. Atualizar depois do deploy
Editou o código? Suba de novo no GitHub (pelo site: abra o arquivo → ícone de lápis →
**Commit changes**; ou `git add .` / `git commit -m "ajuste"` / `git push`).
O app atualiza sozinho em alguns segundos.

## 6. Erros comuns e como resolver
| Erro na tela do app | Causa | Solução |
|---|---|---|
| `ModuleNotFoundError: No module named 'plotly'` | faltou no requirements | adicione `plotly` no requirements.txt |
| `ImportError: Missing optional dependency 'openpyxl'` | arquivo é Excel | adicione `openpyxl` no requirements.txt |
| `FileNotFoundError: dados.csv` | arquivo não subiu ou nome diferente | suba o arquivo; confira o nome (maiúsculas, acento, extensão) |
| `KeyError: 'NOMEUP'` | nome de coluna errado | use as linhas de DIAGNÓSTICO do app.py e corrija as COL_ |
| Gráficos vazios | nome do bairro/filtro diferente do arquivo | confira `df[COL_GRUPO].unique()` e o VALOR_SERIE |
| `UnicodeDecodeError` | encoding do CSV | troque `encoding="utf-8"` por `encoding="latin-1"` |
| Tudo numa coluna só / números errados | separador ou decimal errado | ajuste `sep=` e `decimal=` no read_csv |
| "Main module does not exist" | caminho errado no deploy | Main file path = `app.py` (ou `pasta/app.py` se estiver numa subpasta) |

Para ver o erro completo no Streamlit Cloud: canto inferior direito do app → **Manage app** → logs.
