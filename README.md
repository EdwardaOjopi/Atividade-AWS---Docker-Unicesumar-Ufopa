<h1 align="center"> Projeto AWS :page_facing_up: <br>
Atividade - DevSecOps - Docker - UNICESUMAR UFOPA <br> </h1>
<br>

# Descrição
A atividade tem como finalidade praticar os conceitos que foram abordados na Sprint 5. Foram explorados conceitos gerais sobre Contêineres, a partir de Docker, além de outras aplicações presentes nesse processo de conhecimento. Também houveram práticas no console da Amazon AWS, utilizando seus serviços que eram necessários para agregar ao estudo. Resumidamente, a atividade proposta terá que seguir uma topologia, ou seja, concretizá-la. A seguir, é demonstrado a imagem fornecida para realizar a atividade:
<br>

<div align="center">

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/c57f6bb5-1377-44dc-a82e-53180d0598c0)
</div>


# Pré-requisitos da Atividade<br>
Antes de iniciar, é preciso observar quais requisitos foram apresentados para realizar da forma correta:<br>
1. Instalar e configurar o DOCKER ou CONTAINERD no host EC2;
2. Efetuar Deploy de uma aplicação Wordpress com um contâiner de aplicação RDS Database MySQL;
3. Configurar o uso do serviço EFS AWS para estáticos do contâiner de aplicação Wordpress;
4. Configurar o serviço de Load Balancer AWS para a aplicação Wordpress.<br>

# Pontos de Atenção
Para essa atividade, será necessário atentar para algumas exceções fornecidas para executar de maneira correta:
1. Não utilizar IP Público para saída do serviços Wordpress;
2. As pastas públicas e estáticos do Wordpress é sugerido usar o serviço EFS AWS;
3. É preciso demonstrar a aplicação do Wordpress funcionando;
4. A aplicação Wordpress precisa estar rodando na porta 80 ou 8080.
