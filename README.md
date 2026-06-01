
<h1>👤 microsrvices-user</h1>

<p>
    Serviço responsável pelo gerenciamento de usuários e pela publicação de mensagens
    no RabbitMQ para processamento assíncrono de e-mails.
</p>

<h2> Responsabilidades</h2>

<ul>
    <li>Cadastro de usuários</li>
    <li>Publicação de mensagens no RabbitMQ</li>
    <li>Integração com o microsserviço de e-mail</li>
    <li>Gerenciamento dos dados dos usuários</li>
</ul>

<h2> Fluxo de Comunicação</h2>

<ol>
    <li>O cliente envia uma requisição para cadastro de usuário.</li>
    <li>O microsserviço <strong>microsrvices-user</strong> persiste os dados no PostgreSQL.</li>
    <li>Uma mensagem é publicada no RabbitMQ.</li>
    <li>O microsserviço <strong>microsrvices-email</strong> consome a mensagem.</li>
    <li>O e-mail é processado e enviado ao usuário.</li>
    <li>O status do envio é registrado no banco de dados.</li>
</ol>

<h2> Como Executar</h2>

<h3>1. Clone os repositórios</h3>

<pre>
git clone https://github.com/EnzoDiego/microsrvices-user.git
git clone https://github.com/EnzoDiego/microsrvices-email.git
</pre>

<h3>2. Execute os microsserviços</h3>

<h4> User Service</h4>

<pre>
cd microsrvices-user
mvn spring-boot:run
</pre>

<h4> Email Service</h4>

<pre>
cd microsrvices-email
mvn spring-boot:run
</pre>

<h2> Arquitetura do Sistema</h2>

<pre>
┌───────────────────┐
│      Cliente      │
└─────────┬─────────┘
          │
          ▼
┌──────────────────────────┐
│ microsrvices-user        │
│ User Management Service  │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│      RabbitMQ Broker     │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│ microsrvices-email       │
│ Email Processing Service │
└──────────────────────────┘
</pre>

<h2>🛠️ Tecnologias Utilizadas</h2>

<ul>
    <li>Java 21</li>
    <li>Spring Boot</li>
    <li>Spring Data JPA</li>
    <li>PostgreSQL</li>
    <li>RabbitMQ</li>
    <li>Maven</li>
</ul>

