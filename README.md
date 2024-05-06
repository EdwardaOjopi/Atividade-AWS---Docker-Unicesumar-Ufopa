<h1 align="center"> Projeto AWS :page_facing_up: <br>
Atividade - DevSecOps - Docker - UNICESUMAR UFOPA <br> </h1>
<br>

# Descrição
A atividade tem como finalidade praticar os conceitos que foram abordados na Sprint 5. Foram explorados conceitos gerais sobre Contêineres, a partir de Docker, além de outras aplicações presentes nesse processo de conhecimento. Também houveram práticas no console da Amazon AWS, utilizando seus serviços que eram necessários para agregar ao estudo. Resumidamente, a atividade proposta terá que seguir uma topologia, ou seja, concretizá-la. A seguir, é demonstrado a imagem fornecida para realizar a atividade:
<br>

<br>
<div align="center">

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/c57f6bb5-1377-44dc-a82e-53180d0598c0)
</div>
<br>

# Pré-requisitos da Atividade<br>
Antes de iniciar, é preciso observar quais são os requisitos apresentados para realizar a atividade:<br>
1. Instalar e configurar o DOCKER ou CONTAINERD no host EC2;
2. Efetuar Deploy de uma aplicação Wordpress com um contâiner de aplicação RDS Database MySQL;
3. Configurar o uso do serviço EFS AWS para estáticos do contâiner de aplicação Wordpress;
4. Configurar o serviço de Load Balancer AWS para a aplicação Wordpress.<br>

# Pontos de Atenção
Para essa atividade, será necessário atentar para algumas exceções:<br>
1. Não utilizar IP Público para saída do serviços Wordpress;
2. As pastas públicas e estáticos do Wordpress é sugerido usar o serviço EFS AWS;
3. É preciso demonstrar a aplicação do Wordpress funcionando;
4. A aplicação Wordpress precisa estar rodando na porta 80 ou 8080.<br>

<h1 align="center"> Prática da Atividade <br> </h1>
<br>No início, vai ser necessário que realiza alguns passos para configurar a Network, conseguindo acessar de forma segura as instâncias e o Docker.<br>

<ul>
<li style="list-style-type: 🔔" ><h3>Gerar uma VPC </h3>   </li>
- Para iniciar, iremos criar uma VPC, para uma rede virtual logicamente isolada. <br>
1. Pelo console AWS, acesse o painel para entrar no serviço de VPC <b>VPC</b>; <br>
2. Depois, procure a opção  <b>Nuvem Privada Virtual</b> e clique em <b>Suas VPCs</b>; <br>
3. Após isso, clique na opção de <b>Criar VPC</b>; <br>
4. Nos Recursos a serem criados, selecione <b>VPC e muito mais</b>; <br>
5. Na Geração automática da etiqueta de nome, insira o nome para identificação; <br>
6. No Número de zonas de disponibilidade (AZs), selecione o <b>número 2</b>;<br>
7. Em Gateways NAT (USD), é necessário selecionar o <b>número</b>;<br>
8. Por último, em Endpoints da VPC, selecione <b>Nenhuma</b>.<br>

</ul>

Depois, você obterá essa pré-visualização: 
<br>

<div>
  
![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/bef45d99-11a1-4f1f-ac71-596b8f242aa1)
</div>

<ul>
<li style="list-style-type: 🔔" ><h3>Gerar os Security Groups</h3></li>   
- Agora, será preciso criar os <b>Security Groups</b>, para liberar acesso aos serviços.<br>
1. Pelo console AWS, acesse o painel para entrar no serviço de <b>EC2</b>; <br>
2. Depois, procure a opção  <b>Rede e Segurança</b> e clique em <b>Security groups</b>; <br>
3. Após isso, clique na opção de <b>Criar security group</b>; <br>
4. Configure cada security group dessa forma:<br>
</ul>
  <b>Regras de Entrada</b> - Load Balancer<br>
<div>

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/23c6c79f-c046-496e-9e2e-1bfdbb3b9f34)
</div>
<br>

  <b>Regras de Entrada</b> - Servidor Web EC2<br>
<div>
<br>
  
  ![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/0cfc84d6-5291-47d6-a87f-32fea8fba219)
</div>
   
<br>

<ul>
<li style="list-style-type: 🔔" ><h3>Gerar o EFS</h3></li>   
- Agora, será preciso utilizar o serviço <b>Elastic File System(EFS)</b>, para criar e configurar sistemas de arquivos compartilhados aos serviços de computação da AWS.<br>
1. Pelo console AWS, acesse o painel para entrar no serviço de <b>EC2</b>; <br>
2. Depois, procure a opção  <b>Rede e Segurança</b> e clique em <b>Security groups</b>; <br>
3. Após isso, clique na opção de <b>Criar security group</b>; <br>
4. Crie e configure cada security group dessa forma:
</ul>

> [!NOTE]
> Para facilitar, você pode criar sem nenhuma regras, tanto de entrada como saída, para mais tarde associar à origem certa.
  
  <br>
  <b>Regras de Entrada</b> - Load Balancer<br>
<div>

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/ff4cc816-087c-40e6-a028-58b1ed3d6e11)
</div>
<br>

  <b>Regras de Entrada</b> - Servidor Web EC2<br>
<div>
<br>
  
![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/dbb16f55-49af-4693-b37e-fed1b3b96027)
</div>

   <b>Regras de Entrada</b> - Servidor Web EC2 <br>
  <div>
  <br>

  ![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/7280a53f-ae89-426d-bc0c-938c9b993a0f)
 </div>

  <b>Regras de Entrada</b> - RDS<br>
  <div>
  <br>

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/670a66ef-5a06-4df9-9864-703e471a6f13)
  </div>

 
 <b>Regras de Saída</b> - Conexão via Endpoint <br>
 <div>
<br>

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/83dbc0a6-47b4-48d1-afe1-a077371c40a8)
 </div>

 <b>Regras de Saída</b> - EFS<br>
 <div>
<br>
   
![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/df13dad1-391c-47c8-9ddb-f69979e2efbd)
 </div>
 


