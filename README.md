# Configurando MAC M1 para Projetos de DataScience com BigData
<br>

### Atualizar o macOS
```bash
softwareupdate --install --all
```
<br>

### Ferramentas de Desenvolvimento
```bash
xcode-select --install
```
<br>

### Homebrew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```bash
export PATH="/opt/homebrew/bin:$PATH"
```
```bash
source ~/.zshrc
```
<br>

### Git
```bash
brew install gh
```
```bash
git config --global user.name "pmusachio"
```
```bash
git config --global user.email "paulomusachio@gmail.com"
```
```bash
git config --global init.defaultBranch main
```
<br>

### zsh
```bash
brew install zsh
chsh -s /bin/zsh
```
> oh my zsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
> zsh-fzf
```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install
```
> zsh-autosuggestions
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
> zsh-syntax-highlighting
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
sudo vim ~/.zshrc
```
> plugins
```bash
plugins=(
  git
  fzf
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```
<br>

### chaves SSH - CHECAR!!
```bash
ls ~/.ssh/
```
```bash
ssh-keygen -t rsa -b 4096 -C "paulomusachio@gmail.com"
```
```bash
ssh-add ~/.ssh/id_rsa
```
```bash
cat ~/.ssh/id_rsa.pub
```

[GitHub SSH Settings](https://github.com/settings/keys)

  > "New SSH key / Add SSH key"
  > cole a chave exibida no terminal
  > nomeie a chave

```bash
ssh -T git@github.com
```
<br>

### Java
```bash
brew install openjdk@11
```
> std version
```bash
export JAVA_HOME=$(/usr/libexec/java_home -v 11)
export PATH=$JAVA_HOME/bin:$PATH
```
<br>

### Pyenv
```bash
brew install pyenv
sudo vim ~/.zshrc
```
> config
```bash
export PATH="$(pyenv root)/shims:$PATH"
```
```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zprofile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zprofile
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
source ~/.zprofile
```
```bash
pyenv --version
```
<br>

### Python
```bash
pyenv install -l
pyenv install 3.12.3
pyenv global 3.12.3
```
<br>

### Apache Spark
```bash
brew install apache-spark
```
```bash
export PATH="/opt/homebrew/opt/apache-spark/bin:$PATH"
```
```bash
source ~/.zshrc
```
<br>

### PySpark
```bash
pip install pyspark
```

> Variáveis de Ambiente
```bash
export SPARK_HOME=/opt/homebrew/opt/apache-spark/libexec
export PATH=$SPARK_HOME/bin:$PATH
```
```bash
pyspark
```
<br>

### Instalar Hadoop e HDFS
```bash
brew install hadoop
```
> Configure o HDFS editando o arquivo de configuração no diretório de instalação e execute o serviço localmente.
<br>

### VSCode
```bash
brew install --cask visual-studio-code
```
<br>

## Let's Work!!
<br>

### Criando projeto
- `ls` lista de diretorios
- `cd repos` navegando ate diretorio de "repositorios local"
- criar repositorio no GitHub via navegador web
- `git clone "git@github.com:seu-usuario/seu-novo-repositorio.git"` clonando para diretorio local
- `cd seu-novo-repositorio` acessar diretorio criado
- criando e ativando o ambiente virtual

~~~
python3 -m venv venv
source venv/bin/activate
~~~

- `pip install jupyter` instalando IDE
- `jupyter notebook` iniciando IDE
- `pip install pandas numpy matplotlib findspark...` instalar as dependencias necessarias
<br>

### SPARK CODE

```
import findspark
findspark.init()

from pyspark.sql import SparkSession
from pyspark.sql.functions import col, avg

# Iniciar a sessão Spark
spark = SparkSession.builder.master("local[*]").appName("ProjetoCienciaDadosSpark").getOrCreate()

# Carregar um dataset de exemplo (CSV)
url = "https://raw.githubusercontent.com/jbrownlee/Datasets/master/iris.csv"
columns = ["sepal_length", "sepal_width", "petal_length", "petal_width", "class"]
df = spark.read.option("header", "false").csv(url)

# Renomear as colunas
df = df.toDF(*columns)

# Mostrar as primeiras linhas do DataFrame
print("Primeiras linhas do DataFrame:")
df.show(5)

# Realizar algumas operações básicas
print("Resumo estatístico das colunas numéricas:")
df.describe().show()

# Agrupar e calcular a média das colunas numéricas por classe
print("Média das colunas numéricas por classe:")
df.groupBy("class").agg(
    avg("sepal_length").alias("avg_sepal_length"),
    avg("sepal_width").alias("avg_sepal_width"),
    avg("petal_length").alias("avg_petal_length"),
    avg("petal_width").alias("avg_petal_width")
).show()

# Filtrar os dados (por exemplo, só as linhas onde sepal_length > 5)
print("Filtrar onde 'sepal_length' > 5:")
df.filter(col("sepal_length") > 5).show()

# Salvar o DataFrame como um arquivo Parquet
df.write.parquet("iris.parquet")

# Finalizar a sessão Spark
spark.stop()
```
<br>

### PUSH
- `pip freeze > requirements.txt` listar dependencias e versoes
- `git add .` adiciona as alteracoes
- `git commit -m "explicar atividades executadas"` comentario das alteracoes
- `git push origin main` enviar alteracoes para repositorio
- `deactivate` desativando ambiente
<br>

### PULL
- `cd repos/nome-do-repositorio` acessar diretorio do projeto
- `source venv/bin/activate` ativando o ambiente virtual
- `git pull origin main` atualizando branch local
- `pip install -r requirements.txt` atualizando dependencias
- `jupyter notebook` iniciando IDE


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Configurando Mac M1 para Data Science com Big Data
<br/>

## Atualizar o macOS
```bash
softwareupdate --install --all
```
<br/>

## Instalar Ferramentas de Desenvolvimento
```bash
xcode-select --install
```
<br/>

## Instalar e Configurar o Homebrew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```bash
export PATH="/opt/homebrew/bin:$PATH"
source ~/.zshrc
```
<br/>

## Instalar e Configurar o Git
```bash
brew install gh
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@example.com"
git config --global init.defaultBranch main
```
<br/>

## Instalar Zsh e Configurar o Oh My Zsh
```bash
brew install zsh
chsh -s /bin/zsh
```
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
```bash
# Instalar fzf para autocomplete interativo
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install

# Instalar zsh-autosuggestions e zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
```bash
sudo vim ~/.zshrc
```
```bash
plugins=(
  git
  fzf
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```
```bash
source ~/.zshrc
```
<br/>

## Gerenciar Chaves SSH
```bash
ls ~/.ssh/
```
```bash
ssh-keygen -t rsa -b 4096 -C "seu-email@example.com"
ssh-add ~/.ssh/id_rsa  # Adicionar a chave ao agente SSH
cat ~/.ssh/id_rsa.pub  # Copiar a chave pública para adicionar ao GitHub
```
Adicione a chave SSH ao seu GitHub
<br/>

## Instalar Java
```bash
brew install openjdk@11
```
```bash
export JAVA_HOME=$(/usr/libexec/java_home -v 11)
export PATH=$JAVA_HOME/bin:$PATH
```
<br/>

## Instalar e Configurar o Pyenv
```bash
brew install pyenv
```
```bash
export PATH="$(pyenv root)/shims:$PATH"
```
```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zprofile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zprofile
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
source ~/.zprofile
```
<br/>

## Instalar Python
```bash
pyenv install 3.12.3
pyenv global 3.12.3
```
<br/>

## Instalar e Configurar o Apache Spark
```bash
brew install apache-spark
```
```bash
export PATH="/opt/homebrew/opt/apache-spark/bin:$PATH"
source ~/.zshrc
```
<br/>

## Instalar o PySpark
```bash
pip install pyspark
```
```bash
export SPARK_HOME=/opt/homebrew/opt/apache-spark/libexec
export PATH=$SPARK_HOME/bin:$PATH
```
<br/>

## Instalar Hadoop e Configurar o HDFS
```bash
brew install hadoop
```
Edite o arquivo de configuração do HDFS e execute o serviço localmente.
<br/>

## Instalar o VSCode
```bash
brew install --cask visual-studio-code
```
<br/>

## Criar e Gerenciar Projetos
```bash
ls  # Verificar diretórios
cd repos  # Navegar até o diretório de repositórios
```
```bash
git clone "git@github.com:seu-usuario/seu-novo-repositorio.git"
cd seu-novo-repositorio
```
```bash
python3 -m venv venv
source venv/bin/activate
```
```bash
pip install pandas numpy matplotlib findspark
```
<br/>

## Código de Exemplo no Spark
```python
import findspark
findspark.init()

from pyspark.sql import SparkSession
from pyspark.sql.functions import col, avg

# Iniciar a sessão Spark
spark = SparkSession.builder.master("local[*]").appName("ProjetoCienciaDadosSpark").getOrCreate()

# Carregar um dataset de exemplo (CSV)
url = "https://raw.githubusercontent.com/jbrownlee/Datasets/master/iris.csv"
columns = ["sepal_length", "sepal_width", "petal_length", "petal_width", "class"]
df = spark.read.option("header", "false").csv(url)

# Renomear as colunas
df = df.toDF(*columns)

# Mostrar as primeiras linhas do DataFrame
print("Primeiras linhas do DataFrame:")
df.show(5)

# Realizar algumas operações básicas
print("Resumo estatístico das colunas numéricas:")
df.describe().show()

# Agrupar e calcular a média das colunas numéricas por classe
print("Média das colunas numéricas por classe:")
df.groupBy("class").agg(
    avg("sepal_length").alias("avg_sepal_length"),
    avg("sepal_width").alias("avg_sepal_width"),
    avg("petal_length").alias("avg_petal_length"),
    avg("petal_width").alias("avg_petal_width")
).show()

# Filtrar os dados (por exemplo, só as linhas onde sepal_length > 5)
print("Filtrar onde 'sepal_length' > 5:")
df.filter(col("sepal_length") > 5).show()

# Salvar o DataFrame como um arquivo Parquet
df.write.parquet("iris.parquet")

# Finalizar a sessão Spark
spark.stop()
```
<br/>

## Comandos Básicos de Git
```bash
pip freeze > requirements.txt  # Listar dependências e suas versões
```
```bash
git add .  # Adicionar alterações ao Git
git commit -m "Descrição das alterações"  # Commit com mensagem explicativa
git push origin main  # Enviar alterações para o repositório remoto.
```
```bash
git pull origin main  # Atualizar a branch local com mudanças do repositório remoto
```
<br/>

```bash
deactivate
```
