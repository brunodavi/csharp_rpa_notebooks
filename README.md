# C# RPA Notebooks

## Demo 🔥

https://github.com/user-attachments/assets/07f76f14-5d61-4b65-83c8-ce49f61b4c2b

Este repositório contém notebooks interativos em C# (.NET Interactive / Polyglot Notebooks) focados em **RPA (Robotic Process Automation)** e **Testes Dinâmicos**.

O objetivo principal é fornecer um ambiente de "start rápido" onde o navegador permanece aberto e controlado em tempo real, permitindo desenvolver scripts de automação passo a passo, testar seletores e validar fluxos sem a necessidade de recompilar um projeto de console a cada alteração.

## 🚀 Funcionalidades

* **Setup Instantâneo:** As dependências do Selenium e WebDriverManager são baixadas e carregadas diretamente no notebook.
* **Browser Persistente:** O Chrome é iniciado com um diretório de perfil temporário (`user-data-dir`), mantendo logins, cookies e sessões ativos enquanto você desenvolve.
* **Métodos de Extensão:** Helpers incluídos para simplificar a extração de texto, atributos de imagens e serialização JSON.
* **Gerenciamento Automático de Driver:** Uso do `WebDriverManager` para garantir que a versão do ChromeDriver seja compatível com o seu navegador instalado.
* **Limpeza de Processos:** Utilitários para matar processos "zumbis" do Chrome/Chromedriver antes de iniciar.

## 🛠️ Pré-requisitos

Para rodar os notebooks deste projeto, você precisará de:

1. **[VS Code](https://code.visualstudio.com/)**
2. **[.NET SDK](https://dotnet.microsoft.com/download)** (Versão 6.0 ou superior recomendada)
3. **Extensão [Polyglot Notebooks](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode)** para VS Code.

## 📂 Estrutura e Fluxo de Trabalho

O projeto foi desenhado para ser um "template" para seus scripts pessoais.

### O Arquivo Base

* **`selenium_startup.ipynb`**: Este é o notebook mestre. Ele contém todo o código de inicialização, configuração de `ChromeOptions` e métodos auxiliares. Use-o como base para iniciar qualquer nova automação.

### Gitignore Estratégico

O arquivo `.gitignore` está configurado para permitir que você crie dezenas de notebooks de teste (ex: `teste_login_siteA.ipynb`, `extracao_dados_B.ipynb`) na mesma pasta, **sem que eles sejam comitados no repositório**, mantendo o ambiente limpo.

```gitignore
# Ignora todos os notebooks
*.ipynb
# Ignora executáveis gerados
*.exe

# EXCETO o notebook de inicialização/template
!selenium_startup.ipynb

# Outras possíveis bibliotecas de RPA
!<rpa_lib>_startup.ipynb
```

## ⚡ Como Usar

1. Clone este repositório.
2. Abra o arquivo `selenium_startup.ipynb` no VS Code.
3. Execute as células sequencialmente:
* **Instalação:** Baixa os pacotes NuGet.
* **Utils:** Carrega funções de limpeza e extensões.
* **Configuração:** Define opções do Chrome (Headless, GPU, SSL, etc).
* **Inicialização:** Abre o navegador.


4. **Desenvolva:** Adicione novas células de código abaixo para interagir com a página aberta (`driver.FindElement...`).

### Exemplo de Uso (Snippet)

```csharp
// Navegar
driver.Navigate().GoToUrl("https://www.saucedemo.com");

// Interagir
driver.FindElement(By.Id("user-name")).SendKeys("standard_user");
driver.FindElement(By.Id("login-button")).Click();

// Extrair Dados (usando as extensões inclusas)
var itens = driver.FindElements(By.ClassName("inventory_item"))
    .Select(e => new { 
        Nome = e.GetText(".inventory_item_name"), 
        Preco = e.GetText(".inventory_item_price") 
    });

Console.WriteLine(itens.ToJsonString());

```

## 🔮 Roadmap

A ideia é expandir este repositório conforme a necessidade surgir, adicionando templates para outras bibliotecas de automação modernas:

* [x] Template para **Puppeteer Sharp**
* [ ] Template para **Playwright for .NET**

## 🤝 Contribuição

Sinta-se à vontade para fazer um fork e adaptar os `ChromeOptions` ou métodos de extensão conforme sua necessidade.

---

**Nota:** Este projeto é focado em produtividade local e prototipagem rápida de automações.
