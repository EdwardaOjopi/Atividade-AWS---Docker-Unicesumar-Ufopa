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
<br>

<h1 align="center"> Prática da Atividade <br> </h1>
<br>No início, vai ser necessário que realiza alguns passos para configurar a Network, conseguindo acessar de forma segura as instâncias e o Docker.<br>

<ul>
<li style="list-style-type: ⚙️" ><h3>VPC </h3>   </li>
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
<li style="list-style-type: ⚙️" ><h3>Security Groups</h3></li>   
- Agora, será preciso criar os <b>Security Groups</b>, para liberar acesso aos serviços.<br>
1. Pelo console AWS, acesse o painel para entrar no serviço de <b>EC2</b>; <br>
2. Depois, procure a opção  <b>Rede e Segurança</b> e clique em <b>Security groups</b>; <br>
3. Após isso, clique na opção de <b>Criar security group</b>; <br>
4. Configure cada security group dessa forma:<br>
</ul>

> [!NOTE]
> Para facilitar, você pode criar sem nenhuma regras, tanto de entrada como saída, para mais tarde associar à origem certa.
  
  <br>
  <b>Regras de Entrada</b> - Load Balancer<br>
<div>
<br>
  
![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/ff4cc816-087c-40e6-a028-58b1ed3d6e11)
</div>
<br>

  <b>Regras de Entrada</b> - Servidor Web EC2<br>
<div>
<br>
  
![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/8b0da9aa-c4ca-4223-a17e-b1d0ab8bf9b2)
</div>
<br>

  <b>Regras de Entrada</b> - RDS<br>
  <div>
  <br>

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/670a66ef-5a06-4df9-9864-703e471a6f13)
  </div>
<br>
 
 <b>Regras de Saída</b> - Conexão via Endpoint <br>
 <div>
<br>

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/83dbc0a6-47b4-48d1-afe1-a077371c40a8)
 </div>
<br>

 <b>Regras de Saída</b> - EFS<br>
 <div>
<br>
   
   ![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/2466c93c-44c1-4230-84b3-f31d0931dd57)
 </div> 
<br>

<ul>
<li style="list-style-type: ⚙️" ><h3>EFS</h3></li>   
- Agora, será preciso utilizar o serviço <b>Elastic File System(EFS)</b>, para criar e configurar sistemas de arquivos compartilhados aos serviços de computação da AWS.<br>
1. Pelo console AWS, acesse o painel para entrar no serviço de <b>EFS</b>; <br>
2. Ao acessar a tela, procure a opção  <b>Criar sistema de arquivos</b>; <br>
3. Após isso, clique na opção de <b>Personalizar</b>; <br>
4. Agora, você somente irá mudar o nome do EFS, depois clique em <b>Próximo</b>;<br>
5. Selecione a VPC criada para a atividade, além de escolher as subnets privadas e escolher o Security group do EFS, criado na etapa passada, depois clique em <b>Próximo</b>; <br>
6. Apenas aperta próximo;<br>
7. Revise se está de acordo e clique em Criar.<br>
</ul>

<ul>
<li style="list-style-type: ⚙️" ><h3>RDS</h3></li>   
- Agora, será preciso utilizar o serviço <b>Relational Database Service(RDS)</b>, para ter um serviço de banco de dados relacional fácil de gerenciar os dados do Wordpress. <br>
1. Pelo console AWS, acesse o painel para entrar no serviço de <b>RDS</b>; <br>
2. Depois, procure a opção <b>Banco de Dados</b> e clique em <b>Criar bando de dados</b>; <br>
3. Na tela para configuração, em <b>Opções do mecanismo</b>, selecione o tipo <b>MySql</b>; <br>
4. Em <b>Modelos</b>, selecione a opção de <b>Nível Gratuito</b>; <br>
5. Abaixo, em <b>Configurações de credenciais</b>, é recomendado que coloque uma senha principal para mais segurança;<br>
6. Em <b>Conectividade</b>, na parte de Nuvem privada virtual(VPC), selecione a VPC criada anteriormente;<br>
7. Na parte de <b>Grupo de segurança da VPC existentes</b>, selecione o security group do RDS;<br>
9. Antes de finalizar, vá para <b>Configuração adicional</b> e coloque um nome para o BD;<br>
10. Revise e clique em <b>Criar banco de dados</b>.<br>
</ul>

<ul>
<li style="list-style-type: ⚙️" ><h3>Classic Load Balancer</h3></li>   
- Agora, será preciso utilizar o serviço <b>EC2</b>, para acessar o Load Balancer, usando sua versão Classic.<br>
1. No console AWS, acesse o painel para entrar no serviço de <b>EC2</b> e procure a opção <b>Balanceamento de carga</b>; <br>
2. Depois, vá para <b>Load balancers</b> e clique na opção <b>Criar load balancer</b>; <br>
3. Nos tipos de Load balancer, selecione a opção <b>Classic Load Balancer</b> (abaixo das três opções) e aperte em <b>Criar</b>; <br>
4. Em <b>Configuração básica</b>, coloque um nome para o Load balancer e selecione a opção de <b>Nível Gratuito</b>; <br>
5. Abaixo, em <b>Mapeamento de rede</b>, selecione a VPC criada;<br>
6. Em <b>Mapeamentos</b>, selecione as duas AZs, correspondendo-as para as <b>subnets privadas</b>;<br>
7. Na parte de <b>Grupos de segurança</b>, selecione o security group do Load Balancer;<br>
9. Antes de finalizar, vá para <b>Verificação de Integridade</b> e coloque no <b>Caminho de ping</b> "/wp-admin/install.php", para filtrar o acesso do Wordpress; <br>
10. Revise e clique em <b>Criar load balancer</b>.<br>
</ul>

<div>
<br>

![image](https://github.com/EdwardaOjopi/Atividade-AWS---Docker-Unicesumar-Ufopa/assets/114951492/8768a5a0-0f81-4319-9343-348a8a58cf6b)
</div>
<br>

<ul>
<li style="list-style-type: ⚙️" ><h3>Pares de chaves</h3></li>   
- Agora, será preciso utilizar o serviço <b>EC2</b>, para acessar o recurso chamado <b>Pares de Chaves</b>, o que limita ainda mais o acesso aos serviços. <br>
1. No console AWS, acesse o painel para entrar no serviço de <b>EC2</b> e procure a opção <b>Rede e Segurança</b>; <br>
2. Depois, clique em <b>Pares de chaves</b> e selecione a opção de <b>Criar par de chaves</b>; <br>
3. Escolha um nome para seu par de chaves; <br>
4. Selecione em <b>Tipo de par de chaves</b> a opção <b>RSA</b>;<br>
5. Em <b>Formato de arquivo de chave privada</b>, selecione a opção de <b>.pem</b>; <br>
6. Revise e clique em <b>Criar par de chaves</b>; <br>
</ul>

> [!NOTE]
> Ao finalizar, a chave será baixada. Guarde em um local seguro e de fácil recordação para utilizar mais a frente!
<br>

<ul>
<li style="list-style-type: ⚙️" ><h3>Modelos de Execução</h3></li>   
- Agora, será preciso utilizar o serviço <b>EC2</b>, para acessar o recurso chamado <b>Modelos de execução</b>, o que irá automatizar na execução das instâncias necessárias para essa atividade.<br>
1. No console AWS, acesse o painel para entrar no serviço de <b>EC2</b> e procure a opção <b>Instâncias</b>; <br>
2. Depois, clique em <b>Modelos de execução</b> e selecione a opção de <b>Início rápido</b>; <br>
3. Escolha a imagem <b>Amazon Linux</b> e selecione <b>Amazon Linux 2 AMI</b>; <br>
4. Em <b>Tipo de instância</b>, selecione a opção <b>t3.small</b>; <br>
5. Em <b>Par de chaves (login)</b>, selecione a opção o par de chaves criado no passo anterior; <br>
6. Em <b>Configurações de rede</b>, selecione o grupo de segurança do servidor web da EC2; <br>
7. Para as <b>Tags de recurso</b>, coloque as informações que foram fornecidas para executar as instâncias, com os nomes <b>Name, CostCenter e Project</b>, além de selecionar os tipos de recurso como <b>Instâncias e Volumes</b>; <br>
8. Antes de finalizar, clique em <b>Detalhes Avançados</b> e coloque no campo de <b>Dados do usuário</b> o script a seguir:
<br>
<pre><code>
#!/bin/bash

sudo yum update -y

sudo yum install docker -y 
sudo systemctl start docker
sudo systemctl enable docker

sudo usermod -aG docker ec2-user

sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose 
</pre></code>
<br>
9. Agora faça a revisão e clique em <b>Criar modelo de execução</b>.<br>
</ul>

> [!NOTE]
> A seguir, o passo será bem longo. Olhe com atenção para não realizar algum erro mais a frente!
<br>

<ul>
<li style="list-style-type: ⚙️" ><h3>Grupos Auto Scaling</h3></li>   
- Agora, será preciso utilizar o serviço <b>EC2</b>, para acessar o recurso chamado <b>Grupos Auto Scaling</b>, o que ajuda a habilitar recursos de escalabilidade automática e gerenciar frotas. <br>
1. No console AWS, acesse o painel para entrar no serviço de <b>EC2</b> e procure a opção <b>Auto Scaling</b>; <br>
2. Depois, clique em <b>Grupos Auto Scaling</b> e selecione a opção de <b>Criar grupo de Auto Scaling</b>; <br>
3. Escolha um nome para o grupo do Auto Scaling; <br>
4. Em <b>Modelo de execuçãos</b>, coloque o modelo que foi criado no passo anterior, depois clique em <b>Próximo</b>;<br>
5. Em <b>Rede</b>, selecione a VPC criada para essa atividade e as subnets privadas criadas, depois cliquem em <b>Próximo</b>; <br>
6. Em <b>Balanceamento de carga</b>, selecione a opção <b>Anexar a um balanceador de carga existente</b>. Abaixo, escolha a opção <b>Escolher entre Classic Load Balancers</b>, colocando o Load balancer criado; <br>
7. Em <b>Verificações de integridade</b>, marque a opção de <b>Ative as verificações de integridade do Elastic Load Balancing</b>, depois clique em <b>Próximo</b>;<br>
8. Em <b>Configurar tamanho do grpo e ajuste de escala</b>, insira o número 2 para a <b>Capacidade desejada</b>;<br>
9. Em <b>Escabilidade</b>, insira o número 2 para a <b>Capacidade mínima desejada</b> e número 4 para <b>Capacidade
máxima desejada</b>;
10. Em <b>Ajuste de escala automática</b>, selecione a opção <b>Política de dimensionamento com monitoramento do objetivo</b>, depois coloque o número 75 em <b>Valor de destino</b> e clique em <b>Próximo</b>;
11. Aperte em <b>Próximo</b> até chegar na revisão, depois clique em <b>Criar grupo do Auto Scaling</b>;
</ul>

<ul>
<li style="list-style-type: ⚙️" ><h3>Configuração EC2 - Conexão da Instância via Endpoint</h3></li>   
- Agora, será preciso utilizar o serviço <b>VPC</b>, para acessar o recurso chamado <b>Endpoints</b>, o que limita ainda mais o acesso aos serviços. <br>
1. No console AWS, acesse o painel para entrar no serviço de <b>EC2</b> e procure a opção <b>Rede e Segurança</b>; <br>
2. Depois, clique em <b>Pares de chaves</b> e selecione a opção de <b>Criar par de chaves</b>; <br>
3. Escolha um nome para seu par de chaves; <br>
4. Selecione em <b>Tipo de par de chaves</b> a opção <b>RSA</b>;<br>
5. Em <b>Formato de arquivo de chave privada</b>, selecione a opção de <b>.pem</b>; <br>
6. Revise e clique em <b>Criar par de chaves</b>; <br>
</ul>

