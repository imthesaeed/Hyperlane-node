# Hyperlane-node
اکه سرورتون خام هست این ها رو ابتدا نصب کنید:
~~~
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install docker.io -y
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
nvm install 20
~~~
فاندری و نصب میکنیم
~~~
curl -L https://foundry.paradigm.xyz | bash
source /root/.bashrc
foundryup
~~~
ولت جدید میسازیم 
~~~
cast wallet new
~~~
کلاینت هایپرلین و نصب میکنیم:
~~~
npm install -g @hyperlane-xyz/cli
~~~

