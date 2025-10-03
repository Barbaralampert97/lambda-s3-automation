# lambda-s3-automation
Este repositório contém minhas anotações e insights do projeto "Executando Tarefas Automatizadas com Lambda Function e S3", parte do bootcamp Code Girls 2025 | DIO. O objetivo é documentar os aprendizados adquiridos durante a prática (hands-on), servindo como material de apoio para estudos futuros e implementações em projetos reais.


<img width="863" height="643" alt="image" src="https://github.com/user-attachments/assets/fe748034-385f-4738-bcdf-487ed392b69b" />

## Explicação do Fluxo

1. O usuário faz o upload de um arquivo (nota fiscal em JSON).
2. O arquivo é armazenado no Amazon S3.
3. O S3 aciona uma função Lambda (Python), que valida o tipo de arquivo e os campos obrigatórios.
4. A Lambda grava os dados relevantes no banco de dados (DynamoDB).
5. O cliente pode consultar as notas fiscais por meio de um API Gateway.
6. O API Gateway aciona outra Lambda, que faz a consulta no DynamoDB e retorna a resposta ao cliente.

7. # 📦 Amazon S3 – Armazenamento de Objetos na Nuvem

O Amazon Simple Storage Service (Amazon S3) é um serviço de armazenamento de objetos altamente escalável, seguro e durável, projetado para armazenar e recuperar qualquer quantidade de dados a qualquer momento, de qualquer lugar na web.

## 🧠 O que é o Amazon S3?

- **Armazenamento de Objetos**: o S3 armazena dados como objetos, cada um contendo dados, metadados e um identificador único.
- **Buckets**: os objetos ficam armazenados dentro de containers chamados *buckets*, que possuem nome único e estão localizados em regiões específicas da AWS.
- **Objetos**: cada arquivo armazenado no S3 é chamado de objeto.

## ⚙️ Características Principais

- **Escalabilidade**: suporta trilhões de objetos e exabytes de dados.
- **Durabilidade**: projetado para fornecer 99,999999999% (11 noves) de durabilidade anual.
- **Disponibilidade**: oferece 99,99% de disponibilidade por padrão.
- **Segurança**: suporta criptografia de dados em repouso e em trânsito, controle de acesso detalhado e integração com o AWS Identity and Access Management (IAM).

## 🔐 Controle de Acesso

- **Políticas de IAM**: definem permissões granulares para usuários e grupos.
- **ACLs (Access Control Lists)**: oferecem controle de acesso por objeto.
- **Bloqueio de Objeto**: impede exclusão ou sobrescrição de objetos por período definido.
- **Bloqueio de Acesso Público**: evita que objetos sejam acessados publicamente, mesmo que ACLs permitam.

## 🔄 Ciclo de Vida (Lifecycle)

- **Regras de Ciclo de Vida**: permitem automatizar a transição de objetos entre diferentes estados ou a exclusão de objetos após um período específico.

## 🔗 Integração com Outros Serviços da AWS

- **AWS Lambda**: executa funções em resposta a eventos no S3, como upload de objetos.
- **Amazon CloudFront**: distribui conteúdo armazenado no S3 globalmente com baixa latência.
- **Amazon RDS e DynamoDB**: armazenam backups e dados de aplicações.
- **AWS Glue**: realiza transformações de dados armazenados no S3.
- **Amazon Rekognition e Amazon Transcribe**: analisam imagens e áudios armazenados no S3.

# ⚡ AWS Lambda 
O AWS Lambda é um serviço de computação sem servidor que permite executar código em resposta a eventos, sem necessidade de provisionar ou gerenciar servidores.

## 🔑 Características Principais

- **Execução Sob Demanda**: O código é executado automaticamente em resposta a eventos, como uploads no S3 ou chamadas de APIs.
- **Escalabilidade Automática**: O Lambda ajusta a capacidade de execução conforme a quantidade de eventos, sem intervenção manual.
- **Custo Eficiente**: Você paga apenas pelo tempo de execução e número de requisições, tornando-o uma opção econômica para muitas aplicações.
- **Suporte a Várias Linguagens**: Suporta linguagens como Node.js, Python, Java, Go, Ruby, C# e PowerShell.
- **Integração com Outros Serviços da AWS**: Pode ser acionado por serviços como S3, DynamoDB, SNS, API Gateway, entre outros.

## 💡 Casos de Uso Comuns

- **Processamento de Arquivos**: Automatizar tarefas como compressão ou conversão de arquivos.
- **Automação de Tarefas**: Executar rotinas agendadas ou em resposta a eventos específicos.
- **Construção de APIs Serverless**: Criar APIs escaláveis sem gerenciar servidores.

# 📂 Upload de Arquivos com Processamento e Registro no DynamoDB

## 🔄 Fluxo de Execução

1. **Usuário envia um arquivo** (por exemplo, JSON com informações de uma nota fiscal) para o **Amazon S3**.
2. O **S3 aciona uma trigger** para o **AWS Lambda**.
3. O **Lambda processa o arquivo**, valida os dados e extrai os campos relevantes.
4. Os dados processados são gravados no **Amazon DynamoDB**.
5. Os dados podem ser consultados via **API Gateway**, permitindo acesso controlado às informações.

**Representação simplificada:**  
`S3 → Lambda → DynamoDB → API Gateway`

---

## 🛠 Serviços Utilizados

### Amazon S3
- Armazena arquivos enviados pelos usuários.
- Gatilho (*trigger*) que dispara a execução do Lambda.
- Permite persistência inicial dos arquivos.

### AWS Lambda
- Executa código em resposta a eventos (upload no S3).
- Processa e valida os dados do arquivo.
- Desacopla o processamento do armazenamento e da consulta.

### Amazon DynamoDB
- Banco de dados **NoSQL totalmente gerenciado**.
- Alta performance, escalável e com baixa latência.
- Armazena informações processadas pelo Lambda de forma persistente.
- Automatiza o pipeline de dados, permitindo que o processamento seja contínuo sem intervenção manual.

---

## 💡 Conceitos Importantes

- **Automatização do pipeline de dados**: fluxo de dados do upload até a persistência e consulta totalmente automatizado.
- **Persistência das informações processadas**: os dados validados e processados ficam armazenados de forma durável no DynamoDB.
- **Desacoplamento de componentes**: cada serviço (S3, Lambda, DynamoDB) atua independentemente, garantindo flexibilidade e escalabilidade.

---

# 🖥️ AWS Local com LocalStack

O **LocalStack** é um projeto **open source** que simula serviços da AWS localmente, permitindo que desenvolvedores construam, testem e integrem soluções sem precisar usar a nuvem real.

## 🔑 Para que é utilizado?

- **Desenvolvimento e testes locais** sem custos na AWS real.
- **Validação de soluções** antes de publicar na nuvem, evitando custos inesperados.
- Suporta a maioria dos serviços populares da AWS, como S3, Lambda, DynamoDB, API Gateway, entre outros.
- Possui **versão gratuita** e **versão paga** com recursos adicionais.

## ⚙️ Requisitos e Preparação do Ambiente

- **Python** instalado no sistema.
- Preparação do ambiente local para execução do LocalStack.
- Configuração do **AWS CLI** para apontar para o endpoint do LocalStack.

## 📝 Passos Básicos de Uso

1. Instalar o LocalStack.
2. Configurar o AWS CLI para usar o endpoint do LocalStack.
3. Criar recursos locais, como:
   - Buckets no S3  
   - Tabelas no DynamoDB  
   - Funções Lambda  
   - Outros serviços conforme necessidade
4. Testar e validar a aplicação localmente antes de subir para a AWS real.

## 🌟 Benefícios

- **Desenvolvimento rápido** sem depender da nuvem real.
- **Testes locais confiáveis** antes de deploy em produção.
- **Integração em pipelines de CI/CD**, permitindo automação completa do fluxo de desenvolvimento.
- **Economia de custos**, já que não é necessário criar recursos na AWS real durante a fase de desenvolvimento.

