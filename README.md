# Data Engineer

  Cliente de logística 
  
     Solução de ETL e a criação de um data lake - AWS - para realizar a ingestão dos dados 

        Conjunto de frota de caminhões que gera 
            informações de GPS 
                a cada 5 minutos e dispara para uma fila, 
                    em torno de 3000 registros a cada envio.

        Os caminhões possuem um tagueamento para pagamento de 
                  pedágio e 
                  estacionamento, 
        no qual é possível obter as informações por API REST ou SOAP.
        
    - Arquivo bancário disponibilizado por JSON através de SFTP do fornecedor.

    - Disponibilizar algum tipo de acesso de visualização das informações por consultas 
      ANSI/SQL aos seus analistas de dados.

    - Desenho/fluxograma completo da arquitetura para esse data lake.

          O desenho deve utilizar os componentes das nuvens que o cliente tem disponíveis, 
          e pode-se utilizar também algum componente padrão de data pipeline ou Python / Pyspark.

          Desenho de arquitetura no draw.io (ou alguma outra ferramentas de desenho de componentes e fluxo) 
          enviado por email: dirlei.moreira@platformbuilders.io e rodrigo.diniz@platformbuilders.io

     - Breve texto explicando as decisões tomadas ao analisar os 
       componentes da arquitetura e os relacionamentos entre eles.
     

## Sintese :

          Conjunto de frota de caminhões, sendo que cada caminhão possui um aparelho de GPS e tageamentos 
          para a gestão de trafico e custos operacionais respectivamente.

          * Ingestão dos dados 
          
            - informações de GPS
                cada 5 minutos é disparado para uma fila em torno de 3000 registros
                 36.000 registros por hora
                864.000 resgistros por dia
               
            - tagueamento para pagamento de pedágio e estacionamento
                obter as informações por API REST ou SOAP.
                
            - Arquivo bancário disponibilizado por JSON através de SFTP do fornecedor.
              
           * acesso de visualização das informações por consultas ANSI/SQL    
          
           * desenho/fluxograma completo da arquitetura
          
  ## AWS - Serviços componentes
    
          Glue
              - Crawler para o obter o formato dos dados a serem disponibilizados no S3
              
          Athenas          
              - Catalog gerado pelo crawler do Glue - Presto para as consultas ANSI/SQL
              
          S3  
               - Buckets que vão compor o catalogo de dados
                  - Frotas
                  - GPS
                  - Tageamento
                  - Financeiro
               
          EC2 - Instancia com o Airflow - Docker-compose com a infra neccessária - Postregs, Redis , Works , Scheduler , Web Server , Flask
                Bibliotecas - DAGs
                Fluxos
                  
          Lambda - Estudar possibilidades
          API-Gateway - Analisar custo/beneficio 
          RDS - Postgres - Analisar custo/beneficio 
          
          Airflow   - Docker-Compose
          Terraform - Automação, Scaling
                   
## Modelo de dados :

            Frota - Caminhão - GPS - Tageamento - Estacionamento - Pedagio - Financeiro
            
            Frota       : modelo do caminhão, placa do caminhão
            Caminhão    : placa, nome do motorista , numero do aparelho GPS
            GPS         : numero do aparelho GPS, coordenadas de localização, dia e hora
            Tageamento  : Placa, estacionamento , pedagio
            Financeiros : Arquivo com dados bancários
            
 ## Airflow 
    * Biblioteca : criação de objetos para uso do S3,STFP,Alertas,Limpezas, outros
    * Dags para os fluxos
    
## Decisões

    A solução adotada contemplou a experiencia do autor, escolheu-se o Glue pois o mesmo 
    tem uma caracteristica que permite executar uma varredura no S3 identificando o modelo de dados 
    dos arquivos e buckets.
    
    O Athenas em conjunto com o Glue permite a criação de um catalago que pode ser consultado
    utilizando o painel do mesmo.
    
    O airflow foi escolhido por uma questão de alinhamento com a expertise solicitada pela oportunidade.
    Permite a construção de um pipeline utilizando todo um conjunto de caracteristicas, desenvolvido em python,
    um conjunto infinito de libs pode ser utilizadas, acesso ao S3, SFTP , personalização de acessos com o RBAC, 
    extensão usando o Flask.
    
    Segurança, adotou-se o Cognito para o controle de acesso e permissões dos usuarios aos serviços da AWS.
    
    IAM para as permissões dos recursos da AWS.
    
    CloudWatch para acompanhento dos logs gerados pelos recursos utilizados na solução.
    
    Alguns outros serviços foram cogitados a fazer parte da solução, mas um aprofudamento nos requisitos seria necessário.
    
    
 
 
 
 
 
 
 
 
 
 
            
