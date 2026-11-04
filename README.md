# Conceitos e Arquitetura do Laravel

## 1. Evolução Arquitetural
O MVC artesanal ensinou o fluxo básico: `rota → Controller → Model → View`. Isso facilitou o entendimento do Laravel, pois o framework organiza essas mesmas responsabilidades, mas com ferramentas prontas como rotas, Eloquent, Blade e validação.

## 2. Nova Arquitetura do Laravel 11
O Laravel 11 trouxe uma estrutura mais enxuta, com menos arquivos, providers e configurações padrão. O novo centro de configuração é o `bootstrap/app.php`, onde se definem rotas, middleware e exceções; os providers ficam em `bootstrap/providers.php`.

## 3. `.env` e Segurança
Senhas não devem ficar em `config/database.php` porque esse arquivo pode ser versionado no Git e exposto. O correto é colocar credenciais no `.env` e acessá-las com `env('DB_PASSWORD')`, mantendo configurações sensíveis fora do repositório.

## 4. APP_KEY
A `APP_KEY` é usada para criptografia e assinatura de dados, como sessões e cookies. Alterá-la em produção pode invalidar dados criptografados, deslogar usuários e corromper informações dependentes da chave.

## 5. Pasta `public/`
O servidor deve apontar apenas para `public/`, pois é a única pasta que deve ser acessível pela web. Apontar para a raiz exporia arquivos sensíveis como `.env`, configurações e código-fonte.

## 6. `php arquivo.php` vs. `php artisan`
`php arquivo.php` executa um script PHP isolado, sem o contexto do Laravel. Já `php artisan` roda comandos dentro do framework, com acesso a configurações, banco de dados, models e serviços.

## 7. `.env.example`
O `.env.example` é um modelo versionado no Git que mostra quais variáveis o projeto precisa. Ele evita erros de configuração e ajuda novos desenvolvedores a configurar o ambiente rapidamente, sem expor senhas reais.

## 8. Blade e XSS
`{{ $variavel }}` escapa o conteúdo e protege contra XSS. Já `{!! $variavel !!}` renderiza HTML bruto e deve ser usada somente com conteúdo confiável ou sanitizado.

## 9. Controller Enxuto
O Controller deve ser curto porque apenas coordena a requisição HTTP. Consultas e regras de negócio devem ficar em Models, Services ou Form Requests, deixando o código mais organizado, testável e reutilizável.

## 10. Tinker
O `php artisan tinker` abre um console interativo do Laravel. Ele é útil para testar models, consultas, relacionamentos e regras rapidamente, sem criar rotas ou arquivos temporários.