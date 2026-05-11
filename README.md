# Classificadores - SVM e Bayesianos

Projeto educacional de Machine Learning para classificacao supervisionada de qualidade/aceitacao de carros, usando um notebook Jupyter com comparacao entre modelos bayesianos/discriminantes e SVM.

## Visao Geral

Este repositorio demonstra um fluxo completo de classificacao em dados tabulares:

- leitura e exploracao inicial do dataset;
- limpeza de dados (remocao de coluna de indice e linhas com nulos);
- codificacao de variaveis categoricas com one-hot encoding;
- separacao treino/teste;
- treinamento e comparacao de modelos;
- avaliacao com matriz de confusao e relatorio de classificacao.

O notebook conclui que, no cenario analisado, o modelo `SVC` apresentou melhor desempenho.

## Estrutura do Repositorio

- `Aula 06 - Classificadores (SVM e Bayesianos)_aluno.ipynb`: notebook principal com todo o pipeline.
- `car_dataset.csv`: dataset tabular com atributos de carros e classe alvo.

## Tecnologias Utilizadas

- Python 3
- Jupyter Notebook
- NumPy
- pandas
- scikit-learn
- matplotlib
- seaborn
- `google_drive_downloader` (usado no notebook original para baixar `dados.csv` de um link do Google Drive)

## Dataset

O dataset possui as colunas:

- `buying`: preco de compra
- `maint`: preco de manutencao
- `doors`: numero de portas
- `persons`: capacidade de pessoas
- `lug_boot`: tamanho do porta-malas
- `safety`: nivel de seguranca
- `category`: classe alvo (`unacc`, `acc`, `good`, `vgood`)

Observacoes importantes:

- existe uma coluna de indice sem nome (removida no notebook como `Unnamed: 0`);
- existem valores ausentes em diferentes colunas;
- ha registros com `category` vazia, que sao descartados no tratamento (`dropna`).

## Arquitetura do Pipeline no Notebook

1. **Importacao de bibliotecas**  
   Carrega ferramentas de manipulacao de dados, modelos e metricas.

2. **Carga dos dados**  
   O notebook original baixa um arquivo `dados.csv` do Google Drive e le com `pandas`.

3. **Analise exploratoria**  
   Usa `head`, `shape`, `info`, `isnull` e `describe` para entender o conjunto.

4. **Tratamento de dados**  
   - remove coluna sem valor preditivo (`Unnamed: 0`);  
   - remove linhas com nulos (`dropna`);  
   - aplica one-hot encoding em `doors` e `persons`;  
   - remove as colunas categoricas originais apos encoding.

5. **Separacao treino/teste**  
   Divide `X` e `y` e aplica `train_test_split` com `test_size=0.3` e `random_state=42`.

6. **Treinamento**  
   Treina e compara:
   - `GaussianNB`
   - `LinearDiscriminantAnalysis`
   - `QuadraticDiscriminantAnalysis`
   - `SVC(kernel='rbf')`

7. **Avaliacao**  
   Gera matrizes de confusao e `classification_report` para cada modelo.

## Como Executar Localmente

### 1) Pre-requisitos

- Python 3.10+ recomendado
- `pip` atualizado

### 2) Criar e ativar ambiente virtual

No PowerShell (Windows):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 3) Instalar dependencias

```powershell
pip install --upgrade pip
pip install numpy pandas scikit-learn matplotlib seaborn jupyter googledrivedownloader
```

### 4) Executar o notebook

```powershell
jupyter notebook
```

Depois, abra o arquivo:

- `Aula 06 - Classificadores (SVM e Bayesianos)_aluno.ipynb`

### 5) Usar o dataset local (opcional, recomendado)

Como o repositorio ja possui `car_dataset.csv`, voce pode editar a celula de carga para evitar download externo e ler diretamente o arquivo local, por exemplo:

```python
dados = pd.read_csv("car_dataset.csv", sep=",")
```

## Seguranca e Boas Praticas

- Nao versione credenciais, chaves de API, tokens ou arquivos `.env`.
- Se for adicionar configuracoes sensiveis, use variaveis de ambiente locais.
- Revise outputs do notebook antes de publicar (alguns outputs podem conter caminhos locais ou metadados de execucao).
- Prefira manter dependencias em um `requirements.txt` para reproducibilidade.

## Melhorias Sugeridas

- Criar `requirements.txt` com versoes fixadas.
- Adicionar validacao cruzada e tuning de hiperparametros.
- Incluir script Python modular (`src/`) para separar preprocessamento, treino e avaliacao.
- Adicionar testes para etapa de preprocessamento.

