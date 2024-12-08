
---

# **Tutorial Laravel 11 - Configuração e Personalização**  

## **Parte 1: Requisitos Iniciais**  

### **Certifique-se de que esses programas estão instalados no computador:**  
- Git versão 2.4 ou superior  
- PHP versão 8.2 ou 8.3  
- Composer versão 2.7 ou superior  
- Node.js versão 20.1 ou superior  

### **Verificar versão:**
```bash 
$ git -v
git version 2.43.0
```
```bash 
$ composer --version
Composer version 2.8.3
PHP version 8.3.11
```
```bash 
$ node -v
v22.9.0
```
### **Configurações no arquivo `php.ini`**  

#### **Habilitar extensões PHP**  
Adicione ou descomente as seguintes extensões no arquivo `php.ini`:  
```ini  
extension=zip  
extension=fileinfo  
extension=curl  
extension=openssl  
extension=gd  
extension=mysqli  
extension=pdo_mysql  
extension=pdo_pgsql  
extension=pdo_sqlite  
extension=pgsql  
extension=sqlite3  
extension=mbstring  
```  

#### **Exibição de erros e registro de logs**  
```ini  
display_errors = On  
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT  
log_errors = On  
# Defina o caminho do arquivo:  
error_log = /caminho/para/php_errors.log  
```  

---
## **Anotação Importante**  
**Se necessário**, remova os valores `& ~E_DEPRECATED & ~E_STRICT` no arquivo de configuração `php.ini` para evitar avisos e erros de depreciação em ambientes de desenvolvimento.

--- 

#### **Limites de memória e tempo de execução**  
```ini  
memory_limit = 256M  
max_execution_time = 120  
```  

#### **Configuração de upload de arquivos**  
```ini  
session.gc_maxlifetime = 14000  
```  

---

## **Parte 2: Configuração Inicial do Projeto**  

### **Criando o projeto Laravel**  
```bash  
$ laravel new example-app
```  
```bash
   _                               _
  | |                             | |
  | |     __ _ _ __ __ ___   _____| |
  | |    / _` | '__/ _` \ \ / / _ \ |
  | |___| (_| | | | (_| |\ V /  __/ |
  |______\__,_|_|  \__,_| \_/ \___|_|


 ┌ Would you like to install a starter kit? ────────────────────┐
 │ Laravel Breeze                                               │
 └──────────────────────────────────────────────────────────────┘

 ┌ Which Breeze stack would you like to install? ───────────────┐
 │ Blade with Alpine                                            │
 └──────────────────────────────────────────────────────────────┘

 ┌ Would you like dark mode support? ───────────────────────────┐
 │ Yes                                                          │
 └──────────────────────────────────────────────────────────────┘

 ┌ Which testing framework do you prefer? ──────────────────────┐
 │ Pest                                                         │
 └──────────────────────────────────────────────────────────────┘
```
```bash
 ┌ Which database will your application use? ───────────────────┐
 │ SQLite                                                       │
 └──────────────────────────────────────────────────────────────┘

 ┌ Would you like to run the default database migrations? ──────┐
 │ Yes                                                          │
 └──────────────────────────────────────────────────────────────┘
```

## Escolhendo um Starter Kit

Na etapa de configuração inicial, você será solicitado a escolher um **starter kit**. Aqui estão as opções:

- **No starter kit**: Instalação básica do Laravel, sem funcionalidades extras.
- **Laravel Breeze**: Um kit leve para autenticação, ideal para projetos simples.
- **Laravel Jetstream**: Um kit completo com autenticação, gestão de equipes e muito mais.

### Recomendação

- Se você está iniciando, escolha **Laravel Breeze** para um setup mais simples e fácil de entender:

- Para uma aplicação mais robusta, opte por **Laravel Jetstream** e siga as instruções do [site oficial](https://jetstream.laravel.com/).

---

```bash
$ cd example-app
$ npm install && npm run build  
$ composer run dev # ("php artisan serve")  
```  

### **Servidor embutido do Laravel**  
```bash  
$ php artisan serve  
```  
Acesse [http://127.0.0.1:8000](http://127.0.0.1:8000) ou [http://localhost:8000](http://localhost:8000). 

## Instalar e configurar o pacote de autenticação Laravel/UI

```plaintext
=============== VERIFICAR SE REALMENTE É NECESSÁRIO ESSA PARTE =================
```

Se você deseja utilizar o pacote Laravel/UI para autenticação, siga estas etapas:

```bash
$ composer require laravel/ui
$ php artisan ui vue --auth
$ npm install
$ npm run build # Ou, se usar Vite:
$ npm run build --watch
```

```plaintext
================================================================================
```

### Observação:
Se você já escolheu **Laravel Breeze** ou **Jetstream**, pode ignorar essa seção, pois eles oferecem soluções modernas para autenticação.

---

### **Criar repositório Git local**  
```bash  
$ git init
$ git branch -M main
$ git add .
$ git commit -m "Primeiro commit"
$ git config --global user.name "Seu Nome"
$ git config --global user.email "seuemail@dominio.com"
```  

---

## **Parte 3: Configuração e Tradução para o Português Brasileiro**  

### **Alterar idioma no `.env`**  
Modifique as variáveis de idioma:  
```ini  
APP_LOCALE=pt_BR
```  

### **Traduzir mensagens do Laravel**  
1. Faça o download do pacote de tradução.  

    [Módulo de linguagem pt-BR (português brasileiro) para Laravel](https://github.com/lucascudo/laravel-pt-BR-localization/tree/main)

2. Publique os arquivos de idioma:  
   ```bash  
   $ php artisan lang:publish  
   ```  
   Ou simplesmente crie uma pasta `lang` na raiz do sistema.
   
3. Copie a pasta `pt_BR` e o arquivo `pt_BR.json` para `lang`. 

4. Publique as traduções
    ```bash  
    $ php artisan vendor:publish --tag=laravel-pt-br-localization
    ```  
---
## **Parte 4: Personalização de Redefinição de Senha**  

### **Opção 1: Personalização Direta no Modelo Padrão**  

1. Abra o arquivo `vendor/laravel/framework/src/Illuminate/Auth/Notifications/ResetPassword.php`.  
2. Altere o método `buildMailMessage($url)` conforme abaixo:  

```php  
protected function buildMailMessage($url)  
{  
    return (new MailMessage)  
        ->subject(Lang::get('Notificação de redefinição de senha'))  
        ->line(Lang::get('Você está recebendo este e-mail porque recebemos uma solicitação de redefinição de senha para sua conta.'))  
        ->action(Lang::get('Redefinir senha'), $url)  
        ->line(Lang::get('Este link de redefinição de senha expirará em :count minutos.', ['count' => config('auth.passwords.'.config('auth.defaults.passwords').'.expire')]))  
        ->line(Lang::get('Se você não solicitou uma redefinição de senha, nenhuma outra ação é necessária.'));  
}
```  

3. Abra o arquivo `vendor/laravel/framework/src/Illuminate/Notifications/resources/views/email.blade.php` e altere:  

```php  
{{-- Greeting --}}
@if (! empty($greeting))
# {{ $greeting }}
@else
@if ($level === 'error')
# @lang('Whoops!')
@else
# @lang('Hello!')
@endif
@endif
```  
Para
```php  
{{-- Greeting --}}
@if (! empty($greeting))
# {{ $greeting }}
@else
@if ($level === 'error')
# @lang('Opá, algo deu errado!')
@else
# @lang('Olá!')
@endif
@endif
``` 
---  

```php  
{{-- Salutation --}}
@if (! empty($salutation))
{{ $salutation }}
@else
@lang('Regards,')<br>
{{ config('app.name') }}
@endif
```   
Para:  
```php  
{{-- Salutation --}}
@if (! empty($salutation))
{{ $salutation }}
@else
@lang('Atenciosamente,')<br>
{{ config('app.name') }}
@endif
```  
---  

```php  
@lang(  
    "If you're having trouble clicking the \":actionText\" button, copy and paste the URL below\n".  
    'into your web browser:',  
    [  
        'actionText' => $actionText,  
    ]  
)  
```  
Para:  
```php  
@lang(  
    "Se você estiver com problemas para clicar no botão \":actionText\", copie e cole a URL abaixo\n".  
    'no seu navegador da web:',  
    [  
        'actionText' => $actionText,  
    ]  
)  
```  
---
### **Opção 2: Criar um Modelo Personalizado de Notificação**  

1. **Gerar uma notificação personalizada**  

   ```bash  
   php artisan make:notification ResetPassword  
   ```
2. **Configurar a classe `ResetPassword`**

    Remova o arquivo `ResetPassword.php`:
    ```bash
    $ rm app/Notifications/ResetPassword.php
    ```  

    Copie o novo arquivo `ResetPassword.php` da pasta `vendo`:
    ```bash
    $ cp vendor/laravel/framework/src/Illuminate/Auth/Notifications/ResetPassword.php app/Notifications/ResetPassword.php
    ```
    Edite o arquivo `app/Notifications/ResetPassword.php`:

    ```php  
    protected function buildMailMessage($url)  
    {  
    return (new MailMessage)  
        ->subject(Lang::get('Notificação de redefinição de senha'))  
        ->line(Lang::get('Você está recebendo este e-mail porque recebemos uma solicitação de redefinição de senha para sua conta.'))  
        ->action(Lang::get('Redefinir senha'), $url)  
        ->line(Lang::get('Este link de redefinição de senha expirará em :count minutos.', ['count' => config('auth.passwords.'.config('auth.defaults.passwords').'.expire')]))  
        ->line(Lang::get('Se você não solicitou uma redefinição de senha, nenhuma outra ação é necessária.'));  
    }
    ```  
3. **Atualizar o modelo do usuário**  
   No arquivo `app/Models/User.php`, importe e adicione:  
   ```php  
   use App\Notifications\ResetPassword;  

   public function sendPasswordResetNotification($token)  
   {  
       $this->notify(new MyResetPassword($token));  
   }  
   ```  

4. **Editar o modelo de e-mail personalizado**  
   Publique os modelos de notificações:  
   ```bash  
   $ php artisan vendor:publish --tag=laravel-notifications  
   ```  
   Edite `resources/views/vendor/notifications/email.blade.php` com as mesmas mudanças descritas na **Opção 1**.  

---

Seguindo esses passos, o Laravel estará configurado com traduções e notificações personalizadas para redefinição de senha.


#### Configurar o DotEnv (.env) para utiizar o Mailhog

Faça as alterações nas variáveis de ambiente `MAIL_*` no arquivo .env conforme abaixo

```shell
MAIL_MAILER=smtp
MAIL_HOST=127.0.0.1
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"
```
## **Erro**  
```bash
[logs] ┌ 20:27:58 Symfony\Component\...\UnsupportedSchemeException ─── vendor/symfony/... ┐
[logs] │ The "" scheme is not supported; supported schemes for mailer "smtp" are: "s... │
[logs] └───────────────────────────────────── POST: /forgot-password • Auth ID: guest ┘
```

`OBS: adicionado 'scheme' => 'smtp' ao app/config/mail.php em mail.mailers.smtp`
