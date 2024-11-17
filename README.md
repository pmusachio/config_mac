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
git config --global user.name "pmusachio"
git config --global user.email "paulomusachio@gmail.com"
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
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install
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
ssh-keygen -t rsa -b 4096 -C "paulomusachio@gmail.com"
ssh-add ~/.ssh/id_rsa  # Adicionar a chave ao agente SSH
cat ~/.ssh/id_rsa.pub  # Copiar a chave pública para adicionar ao GitHub
```

[GitHub SSH Settings](https://github.com/settings/keys)

> "New SSH key / Add SSH key"
> 
> cole a chave exibida no terminal
> 
> nomeie a chave

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
# sudo vim ~/.zshrc
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
pyenv install -l
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

## Criar Projetos
```bash
ls
```
```bash
cd repos
```
```bash
git clone "git@github.com:seu-usuario/novo-repositorio.git"
cd novo-repositorio
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

spark = SparkSession.builder.master("local[*]").appName("ProjetoCienciaDadosSpark").getOrCreate()

url = "https://raw.githubusercontent.com/jbrownlee/Datasets/master/iris.csv"
columns = ["sepal_length", "sepal_width", "petal_length", "petal_width", "class"]
df = spark.read.option("header", "false").csv(url)

df = df.toDF(*columns)

print("Primeiras linhas do DataFrame:")
df.show(5)

print("Resumo estatístico das colunas numéricas:")
df.describe().show()

print("Média das colunas numéricas por classe:")
df.groupBy("class").agg(
    avg("sepal_length").alias("avg_sepal_length"),
    avg("sepal_width").alias("avg_sepal_width"),
    avg("petal_length").alias("avg_petal_length"),
    avg("petal_width").alias("avg_petal_width")
).show()

print("Filtrar onde 'sepal_length' > 5:")
df.filter(col("sepal_length") > 5).show()

df.write.parquet("iris.parquet")

spark.stop()
```
<br/>

## Git PUSH
```bash
pip freeze > requirements.txt
```
```bash
git add .
git commit -m "Descrição das alterações"
git push origin main
```
```bash
deactivate
```
<br/>

## Git PULL
```bash
cd repos/nome-do-repositorio
```
```bash
source venv/bin/activate
```
```bash
git pull origin main
```
```bash
pip install -r requirements.txt
```
