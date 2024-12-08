
---

# **Tutorial Laravel 11 - Configuração e Personalização**

Este repositório contém um projeto Laravel 11 configurado com autenticação e suporte ao idioma **português do Brasil** (pt-BR). Siga as etapas abaixo para configurar e executar o projeto em sua máquina.

## **1. Clonar o Repositório**

Baixe o projeto diretamente do GitHub:

```bash
git clone https://github.com/lucio-adriano/laravel-crud-1.git
```

Acesse a pasta do projeto:

```bash
cd laravel-crud-1
```

## **2. Configurar o Arquivo `.env`**

1. Faça uma cópia do arquivo `.env.example`:
   ```bash
   cp .env.example .env
   ```

2. Edite o arquivo `.env` e ajuste as informações necessárias, como o idioma da aplicação e as configurações de email. Exemplo:  
   ```env
   APP_LOCALE=pt_BR
   MAIL_MAILER=smtp
   MAIL_PORT=1025
   ```

## **3. Instalar Dependências**

Instale as dependências do projeto para o backend e frontend:

```bash
composer install && npm install && npm run build
```

## **4. Gerar a Chave do Projeto**

Crie a chave de segurança da aplicação:

```bash
php artisan key:generate
```

## **5. Configurar o Banco de Dados**

Execute as migrações para criar as tabelas no banco de dados:

```bash
php artisan migrate
```

---

Com essas etapas concluídas, o projeto estará configurado e pronto para uso. Caso tenha dúvidas ou problemas, sinta-se à vontade para abrir uma issue no repositório.

--- 

Se precisar de mais ajustes, é só avisar! 🚀