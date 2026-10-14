# Riff Store: Merch & Vinis de Rock

Protótipo de uma loja virtual fictícia desenvolvido para **Programação para Web I** — FACOM/UFU, campus Monte Carmelo, **2026/2**, Prof. Adriano Mendonça Rocha.

**Integrantes:** Gabriel Fernandes, Rafael Lemos e Nicolas Bernardes.

**[Acessar a loja online](https://gabrielfmck.github.io/riff-store-web/)**

A Riff Store utiliza **HTML, CSS e JavaScript no navegador**, com 31 produtos de exemplo e dados simulados. O catálogo, o carrinho, o cadastro, o login, os pedidos, as avaliações e o painel administrativo funcionam com armazenamento local.

## Executar o projeto

1. Abra a pasta do projeto no VS Code.
2. Abra [public/index.html](public/index.html).
3. Inicie a página pela extensão **Live Server**.

Também é possível servir a pasta `public/` com outro servidor estático. As imagens, as fontes, o jQuery e o Bootstrap já estão incluídos no projeto. Não é necessário instalar dependências com npm, configurar variáveis de ambiente ou iniciar um banco de dados.

A consulta automática de CEP e os vídeos externos precisam de conexão com a internet. As páginas, as imagens locais e as operações com dados simulados funcionam com os arquivos incluídos.

## Contas de demonstração

| Perfil | E-mail | Senha |
| --- | --- | --- |
| Administrador | `admin@riffstore.com` | `admin123` |
| Cliente | `cliente@riffstore.com` | `cliente123` |

Essas contas e senhas são públicas e servem somente para testar o protótipo. Utilize informações fictícias nos formulários e não reutilize senhas pessoais.

## Dados no navegador

Na primeira visita, [dados.js](public/js/demo/dados.js) fornece os registros iniciais. [api-local.js](public/js/demo/api-local.js) simula as operações e salva as alterações no **localStorage**. A sessão e o carrinho também ficam no navegador.

Cada navegador e endereço mantém seus próprios dados. Uma compra feita no site não altera a cópia aberta pelo Live Server nem os dados de outra pessoa. Limpar os dados do navegador remove o que foi salvo localmente.

Para restaurar os registros iniciais, entre como administrador e abra **Configurações → Restaurar dados de demonstração**. Essa ação substitui as alterações locais em produtos, contas, pedidos e demais registros daquele navegador.

## Organização do projeto

```text
riff-store-web/
├── public/
│   ├── *.html                    # Páginas da loja
│   ├── css/                      # Estilos e declaração das fontes
│   ├── js/
│   │   ├── compartilhado/
│   │   │   ├── app.js            # Navegação, carrinho, utilitários e RS.api()
│   │   │   └── fotos.js          # Referências das fotos da interface
│   │   ├── paginas/              # Controladores das páginas interativas
│   │   └── demo/
│   │       ├── dados.js          # Dados iniciais de exemplo
│   │       └── api-local.js      # Operações simuladas e persistência local
│   ├── img/                      # Fotos, logos e ícones
│   └── vendor/                   # Bibliotecas e fontes locais, com suas licenças
├── .github/workflows/pages.yml   # Publicação da pasta public/
├── .gitignore
└── README.md
```

## Como o código funciona

O fluxo de uma interação é **HTML → controlador da página → RS.api() → api-local.js → dados locais → atualização da página**. `RS.api()` é uma função compartilhada que encaminha as operações para a simulação no navegador; ela não depende de um servidor de aplicação.

Comece por [index.html](public/index.html) e [style.css](public/css/style.css) para entender a estrutura e a aparência. [home.js](public/js/paginas/home.js) controla a página inicial. [app.js](public/js/compartilhado/app.js) monta o cabeçalho e o rodapé, organiza o carrinho e oferece funções usadas pelas outras páginas.

Os comentários em português explicam os eventos, a validação dos formulários, as operações assíncronas e a persistência local. O código próprio da loja fica em `public/js/`; `public/vendor/` contém as bibliotecas prontas.

## Páginas

| Página | Arquivo | Controlador específico |
| --- | --- | --- |
| Início | `index.html` | `home.js` |
| Catálogo e filtros | `produtos.html` | `produtos.js` |
| Produto, galeria, tamanhos e faixas | `produto.html` | `produto.js` |
| Carrinho | `carrinho.html` | `carrinho.js` |
| Finalização do pedido | `checkout.html` | `checkout.js` |
| Login e cadastro | `login.html` | `login.js` |
| Minha conta | `conta.html` | `conta.js` |
| Contato e perguntas frequentes | `contato.html` | `contato.js` |
| Painel administrativo | `admin.html` | `admin.js` |
| Recuperação de senha | `recuperar-senha.html` | Código no próprio HTML |
| Sobre | `sobre.html` | Código compartilhado |
| Página não encontrada | `404.html` | Código compartilhado |

Os arquivos HTML ficam em `public/`, e os controladores ficam em `public/js/paginas/`. O menu de bandas e o link de promoções abrem o catálogo com filtros na URL. O checkout e a conta pedem login; o painel pede o perfil de administrador. Essas verificações são demonstrativas e ocorrem no navegador.

## Funcionamento da loja

- Frete de **R$ 19,90**, gratuito a partir de **R$ 299,00** em produtos, antes do desconto.
- Cupom **ROCK10**: desconto de 10% nos produtos, para e-mails inscritos na newsletter, com uso único por conta.
- Camisetas nos tamanhos **P, M, G e GG**, com quantidade limitada ao estoque simulado.
- Pix, cartão e boleto são opções simuladas; nenhuma cobrança ou entrega é realizada.
- A recuperação de senha apresenta um link simulado válido por uma hora; nenhum e-mail é enviado.
- Mensagens de contato, inscrições e pedidos ficam salvos apenas no navegador em uso.

## Alterar os exemplos

Edite [dados.js](public/js/demo/dados.js) para mudar os registros iniciais. Se o navegador já tiver dados salvos, restaure a demonstração pelo painel para carregar os novos exemplos.

Para acrescentar imagens, coloque os arquivos em `public/img/` e ajuste os caminhos dos produtos. Alterações feitas pelo painel administrativo afetam somente os dados locais, sem modificar os arquivos do repositório.

## Publicação

O workflow [pages.yml](.github/workflows/pages.yml) publica a pasta `public/` no GitHub Pages após um push na `main`. A origem do Pages deve estar configurada como **GitHub Actions** nas configurações do repositório.
