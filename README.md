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

لانچ کردن داکر و خود نود:
~~~
docker pull --platform linux/amd64 gcr.io/abacus-labs-dev/hyperlane-agent:agents-v1.0.0
~~~
ساخت پوشه و دیرکتوری:
~~~
mkdir -p /root/hyperlane_db_base && chmod -R 777 /root/hyperlane_db_base
~~~
تو این مرحله ها اگه سرور خام بود که اوکیه اگه داک قبلی و زدید و به مشکل خوردید فایل و پوشه های قبلی و پاک کنید و این کد و بزنید:
~~~
docker stop /hyperlane && docker rm /hyperlane
~~~
در مرحله ی آخر حواستون باشه چندبار چک کنید به جای <chain> هر چینی که رو مین نتش میخواید ران کنید و برنید اینجا برای مثال ما بیس و میزنیم
☑️نکته که تو مرحله ی ساخت پوشه و دیرکتوری خودم ادیت زدم و بیس و گذاشتم یعنی برای هرچین ای که میخواید ران کنید باید یک پوشه ی جدا درنظربگیرید تو بخش داکر و کانتینرها خودتون مدیریت کنید...
💬یادتون باشه که RPC رو حتما از آلکمی بگیرید که کوییک نود کار نمیکنه و پلنه پرو میخواد که پولیه...
https://dashboard.alchemy.com/
یه ۵ ،۶ دلار بزنید به مینمیت بیس برای فی


ران کردن نود
~~~
docker run -d \
  -it \
  --name hyperlane \
  --mount type=bind,source=/root/hyperlane_db_<CHAIN>,target=/hyperlane_db_<CHAIN> \
  gcr.io/abacus-labs-dev/hyperlane-agent:agents-v1.0.0 \
  ./validator \
  --db /hyperlane_db_<CHAIN> \
  --originChainName <CHAIN> \
  --reorgPeriod 1 \
  --validator.id <NAME> \
  --checkpointSyncer.type localStorage \
  --checkpointSyncer.folder <CHAIN> \
  --checkpointSyncer.path /hyperlane_db_<CHAIN>/<CHAIN>_checkpoints \
  --validator.key <PRIVATE_KEY> \
  --chains.<CHAIN>.signer.key <PRIVATE_KEY> \
  --chains.<CHAIN>.customRpcUrls <RPC_CHAIN>
~~~
جایگذاری <privatekey> و <rpc-chain> و <name> که اسم ولیدیتورتون هست...
و در آخر چک کردن لاگ و تمام 📈
~~~
docker logs -f hyperlane
~~~


