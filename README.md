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
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```
```bash
brew update
```

<br>

### Git
```bash
brew install gh install git
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

  > clique "New SSH key / Add SSH key"
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
sudo ln -sfn /usr/local/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
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
brew install pyspark
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

### p
