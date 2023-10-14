<img src="https://www.projetoacbr.com.br/forum/uploads/monthly_2019_12/acbrliblogo1000.png.ec2a316e66a0f321329b6eba77ed84eb.png" />

## acbr-demo-linux

Repo para teste da falha Segmentation Fault ao utilizar a lib ACBR com nodejs no Ubuntu.

## Passos iniciais

Clone o repositório.

```sh
gh repo clone git@github.com:Maurelima/acbr-demo-linux.git
```

`cd` no diretório criado para acessa-lo.

```sh
cd acbr-demo-linux
```

Instale as dependências do projeto:

```sh
npm install
```

Certificado.pfx:

```sh
Cole seu certificado digital na pasta tmp/certificado com o nome certificado.pfx
```

Senha do certificado:

```sh
Na linha 154 do arquivo lib_test_teste-acbrlibnfe.js, altere o texto 'senha_certificado' pela senha do seu certificado.
```

Instale as dependências do sistema:

```sh
echo "deb http://archive.ubuntu.com/ubuntu/ focal main universe" | tee -a /etc/apt/sources.list && \
echo "deb http://security.ubuntu.com/ubuntu/ focal-security main universe" | tee -a /etc/apt/sources.list && \
apt-get update && apt-get install -y --no-install-recommends \
xvfb \
xauth \
libxml2 \
libgtk2.0-0 \
ttf-mscorefonts-installer && \

# Download e instalação do OpenSSL 1.1.1q
wget --no-check-certificate https://www.openssl.org/source/openssl-1.1.1q.tar.gz && \
tar -zxf openssl-1.1.1q.tar.gz && \
cd openssl-1.1.1q && \
./config && \
make && \
make install && \

# Criação de links simbólicos para as bibliotecas do OpenSSL
ln -s /usr/local/lib/libssl.so.1.1 /usr/lib/libssl.so.1.1 && \
ln -s /usr/local/lib/libcrypto.so.1.1 /usr/lib/libcrypto.so.1.1 && \

# Criação de um link simbólico para a biblioteca libxml2.so
ln -s /usr/lib/x86_64-linux-gnu/libxml2.so.2 /usr/lib/x86_64-linux-gnu/libxml2.so
```

Teste a execução localmente:

```sh
node lib_test_teste-acbrlibnfe.js
```

Agora você deve conseguir ver os resultados no console 🚀.

## Ferramentas 🧰

- [x] ACBR
- [x] NODEJS
- [x] FFI-NAPI
- [x] REF-NAPI

## Estrutura do Projeto 🏗

No projeto temos:

- `lib_test_teste-acbrlibnfe.js`: Arquivo a ser executado pelo node para efetuar o teste
- `assets/` : Pasta com as bibliotecas do ACBR
- `tmp/` :  Pasta onde se encontra o acbrlib.ini carregado no arquivo lib_test_teste-acbrlibnfe.js
- `tmp/certificado` :  Pasta onde deve ser colocado o certificado com nome "certificado.pfx"
- `tmp/acbr/logs` :  Pasta onde os logs gerados serão gravados
- `tmp/acbr/reports` :  Pasta onde os reports gerados serão gravados