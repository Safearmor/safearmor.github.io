# Como Gerar uma Chave SSH

As chaves SSH permitem acessar servidores e serviços de forma segura, sem a necessidade de senha.  
Siga este guia para criar uma chave SSH no Linux, macOS ou Windows.

---

## 1. Verificar se já existe uma chave SSH

Antes de criar uma nova, veja se já existem chaves no seu computador:

```bash
ls ~/.ssh
```

Se aparecerem arquivos como:

* id_rsa e id_rsa.pub

* id_ed25519 e id_ed25519.pub

então você já possui chaves SSH.

Se não existir, prossiga para criar uma nova.

## 2. Criar uma nova chave SSH

```bash
ssh-keygen -t ed25519 -C "seu-email@exemplo.com"
```

Durante o processo, será perguntado:

1. Local do arquivo da chave

Aperte Enter para usar o padrão:

```bash
~/.ssh/id_ed25519
```

2. Criar uma senha (passphrase)
Recomendado inserir uma senha.
Se não quiser, apenas aperte Enter.

## 3. Verificando a chave gerada

Após gerar, confira os arquivos:

```bash
ls ~/.ssh/id_ed25519*
```

Você deverá ver:

* id_ed25519 → chave privada (NUNCA compartilhe)
* id_ed25519.pub → chave pública (pode ser enviada)


## 4. Copiar a chave pública

Para copiar a chave pública:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copie o conteúdo completo, algo como:

```bash
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI... seu-email@exemplo.com
```

## 5. Adicionar a chave no servidor

Edite o arquivo authorized_keys no servidor:

```bash
mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys
```

Cole a chave pública dentro do arquivo e salve.

Corrija as permissões (muito importante!):

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```


## 5.1 (ALTERNATIVA) Copiar a chave pública com `ssh-copy-id`

A forma mais prática e segura de enviar sua chave pública para um servidor Linux é usando o comando:

```bash
ssh-copy-id usuario@servidor
```

