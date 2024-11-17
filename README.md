# Setup Mac Apple Silicon for DS projects W/ Big Data
<br/>

## OS Update
```bash
softwareupdate --install --all
```
<br/>

## XCode
```bash
xcode-select --install
```
<br/>

## Homebrew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
<br/>

## Git
```bash
brew install gh
git config --global user.name "pmusachio"
git config --global user.email "paulomusachio@gmail.com"
git config --global init.defaultBranch main
```
<br/>

## Oh My Zsh
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
<br/>

## SSH keys
```bash
ls ~/.ssh/
```
```bash
ssh-keygen -t rsa -b 4096 -C "paulomusachio@gmail.com"
```
```bash
ssh-add ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub
```

[SSH Set](https://github.com/settings/keys)

> Add SSH key
> 
> past key from terminal
> 
> rename key

<br/>

## Java
```bash
brew install openjdk@11
```
<br/>

## Pyenv
```bash
brew install pyenv
```
<br/>

## Python
```bash
pyenv install -l
```
```bash
pyenv install 3.12.3
pyenv global 3.12.3
```
<br/>

## Spark
```bash
brew install apache-spark
```
<br/>

## PySpark
```bash
pip install pyspark
```
<br/>

## Hadoop
```bash
brew install hadoop
```

> hdfs namenode -format
> 
> start-dfs.sh
> 
> hdfs dfsadmin -report
> 
> stop-dfs.sh
<br/>

## VSCode
```bash
brew install --cask visual-studio-code
```
<br/>

## Edit .zshrc
```bash
vim ~/.zshrc
```
```bash
# HOMEBREW
export PATH="/opt/homebrew/bin:$PATH"

# OH MY ZSH
plugins=(
  git
  fzf
  zsh-autosuggestions
  zsh-syntax-highlighting
)

# JAVA
export JAVA_HOME=$(/usr/libexec/java_home -v 11)
export PATH=$JAVA_HOME/bin:$PATH

# PYENV
export PATH="$(pyenv root)/shims:$PATH"

# SPARK
export PATH="/opt/homebrew/opt/apache-spark/bin:$PATH"

# PYSPARK
export SPARK_HOME=/opt/homebrew/opt/apache-spark/libexec
export PATH=$SPARK_HOME/bin:$PATH
```
```bash
source ~/.zshrc
```
<br/>

## Edit .zprofile
```bash
vim ~/.zprofile
```
```bash
# PYENV
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zprofile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zprofile
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
```
```bash
source ~/.zprofile
```
<br/>

## New Project
```bash
ls
```
```bash
cd repos
```
```bash
git clone "git@github.com:user/new-repo.git"
cd new-repo
```
```bash
python3 -m venv venv
source venv/bin/activate
```
```bash
pip install pandas numpy matplotlib findspark
```
<br/>

## Project Test
```python
import findspark
findspark.init()

from pyspark.sql import SparkSession
from pyspark.sql.functions import col, avg

spark = SparkSession.builder.master("local[*]").appName("ProjectoTest").getOrCreate()

url = "https://raw.githubusercontent.com/jbrownlee/Datasets/master/iris.csv"
columns = ["sepal_length", "sepal_width", "petal_length", "petal_width", "class"]
df = spark.read.option("header", "false").csv(url)

df = df.toDF(*columns)

df.show(5)

df.describe().show()

df.groupBy("class").agg(
    avg("sepal_length").alias("avg_sepal_length"),
    avg("sepal_width").alias("avg_sepal_width"),
    avg("petal_length").alias("avg_petal_length"),
    avg("petal_width").alias("avg_petal_width")
).show()

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
git commit -m "COMMIT CHANGES"
git push origin main
```
```bash
deactivate
```
<br/>

## Git PULL
```bash
cd repos/name-repo
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
