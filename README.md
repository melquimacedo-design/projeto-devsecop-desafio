# Desafio DevSecOps — Gerenciador de Tarefas

## Sobre o Projeto
Este repositório faz parte do desafio prático do módulo de DevSecOps da ADA Tech.
Você receberá este projeto com vulnerabilidades propositais e uma pipeline incompleta.
Seu objetivo é **implementar a pipeline de segurança** e **corrigir as vulnerabilidades**.

## Estado atual
A pipeline está **incompleta**. Os steps de segurança precisam ser implementados por você.

## Sua missão
1. Implementar os steps de segurança no `pipeline.yml`
2. Fazer a pipeline **quebrar** ao detectar os problemas
3. Corrigir as vulnerabilidades encontradas
4. Fazer a pipeline **passar** com tudo verde ✅
5. Documentar o funcionamento da pipeline neste README

## O que implementar
- [ ] Secrets Scanning com **Gitleaks**
- [ ] SAST com **Semgrep**
- [ ] SCA com **Grype**
- [ ] Assinatura do artefato com cosign
- [ ] Deploy com **GitHub Pages**

## Como a pipeline funciona
> Nossa pipeline é dividida em 3 etapas cruciais de validação automatizada:

### 1. 🔍 Secrets Scanning (Varredura de Segredos)
* **Ferramenta:** Gitleaks
* **O que faz:** Analisa todo o histórico de commits em busca de chaves de API, senhas, tokens ou credenciais que possam ter sido esquecidas e enviadas por engano no código fonte.
* **Por que é importante:** Credenciais expostas publicamente no GitHub podem ser detectadas por robôs maliciosos em poucos minutos, permitindo acessos indevidos e prejuízos financeiros ou vazamento de dados.

### 2. 🔬 SAST - Static Application Security Testing (Teste Estático de Segurança)
* **Ferramenta:** Semgrep
* **O que faz:** Analisa o código de forma estática (sem precisar executá-lo), procurando por padrões e linhas de código que sejam historicamente inseguras.
* **Por que é importante:** Ajuda a interceptar falhas clássicas de desenvolvimento de software logo no início do fluxo, como vulnerabilidades de injeção (SQL Injection, Command Injection), Cross-Site Scripting (XSS) ou o uso de funções consideradas perigosas/obsoletas pela comunidade.

### 3. 📦 SCA - Software Composition Analysis (Análise de Composição de Software)
* **Ferramenta:** Grype
* **O que faz:** Examina o arquivo de dependências (as bibliotecas de terceiros que o projeto importa para funcionar) e cruza as versões utilizadas com bancos de dados públicos de vulnerabilidades conhecidas (CVEs).
* **Por que é importante:** Muitas vezes o seu código próprio está totalmente seguro, mas uma biblioteca que você instalou possui uma falha grave. A pipeline foi configurada para travar o build caso encontre qualquer vulnerabilidade de severidade **Média ou Superior**.

**## 🐛 Vulnerabilidades Encontradas e Corrigidas**

Durante a execução inicial da esteira, foram detectados e corrigidos **5 problemas** críticos no código original:

1. **[Chave de API exposta]:** Detectada pelo Gitleaks nas linhas 1: API_KEY e 2: DB_PASSWORD, do arquivo src/script.js. **Correção:** As linhas foram removidas do código.
2. **[Função insegura]:** Detectada pelo Semgrep no uso de eval() na função addTask() em src/script.js. **Correção:** Substituída a função por uma alternativa segura recomendada pelas boas práticas, ou seja chamada direta sem uso de eval().
3. **[Vulnerabilidade XSS]:** Detectada pelo Semgrep no uso de innerHTML na função addTask() em src/script.js. **Correção:** Implementada a sanitização correta dos dados de entrada do usuário, criado via DOM no padrão já utilizado no código.
4. **[Dependências desatualizadas]:** Detectadas pelo Grype nas dependências: lodash, express e axios declaradas em package.json. **Correção:** Atualizadas as bibliotecas para as versões estáveis mais recente livre de CVEs.
5. **[Dependências desatualizadas]:** Atualizar o artefato indicado na linha 127 do código para a versão 4.1.3

Aprovadas todas as correções, a esteira passou a rodar com status **verde**, efetuando o deploy automático na infraestrutura.


## URL de Produção
> https://melquimacedo-design.github.io/projeto-devsecop-desafio/
