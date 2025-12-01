# Configurando uma chave SSH no Cloud Server

Este guia ensina como gerar e adicionar uma chave SSH para acessar seu Cloud Server com segurança.

## 1. Gerar uma chave SSH no seu computador

No seu terminal, execute:

```bash
ssh-keygen -t ed25519 -C "seu_email@exemplo.com"
```

* Pressione Enter para aceitar o local padrão (~/.ssh/id_ed25519).

* Defina uma senha segura (opcional, mas recomendado).

Isso gera duas chaves:

* Privada: id_ed25519 → nunca compartilhe.

* Pública: id_ed25519.pub → será adicionada no servidor.

## 1.2 Adicionar a chave pública no Cloud Server

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub usuario@ip-do-servidor
```

Alternativa: Manualmente

Conecte-se ao servidor:

```bash
ssh usuario@ip-do-servidor
```

Crie a pasta .ssh se não existir:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

Adicione a chave pública ao arquivo authorized_keys:

```bash
echo "COLE_SUA_CHAVE_PUBLICA_AQUI" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

## 1.3 Testar a conexão

```bash
ssh usuario@ip-do-servidor
```