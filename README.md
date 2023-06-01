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

    - Disponibilizar algum tipo de acesso de visualização das informações por consultas 
      ANSI/SQL aos seus analistas de dados.

    - Desenho/fluxograma completo da arquitetura para esse data lake.

          O desenho deve utilizar os componentes das nuvens que o cliente tem disponíveis, 
          e pode-se utilizar também algum componente padrão de data pipeline ou Python / Pyspark.

          Desenho de arquitetura no draw.io (ou alguma outra ferramentas de desenho de componentes e fluxo) 
          enviado por email: dirlei.moreira@platformbuilders.io e rodrigo.diniz@platformbuilders.io

     - Breve texto explicando as decisões tomadas ao analisar os 
       componentes da arquitetura e os relacionamentos entre eles.
     

## Resumo :

          Conjunto de frota de caminhões, sendo que cada caminhão possui um aparelho de GPS e tageamentos 
          para a gestão de trafico e custos operacionais respectivamente.

          * Ingestão dos dados 
          
            - informações de GPS
                cada 5 minutos é disparado para uma fila em torno de 3000 registros
                36.000 registros por hora
                
              
            - tagueamento para pagamento de pedágio e estacionamento
                obter as informações por API REST ou SOAP.
              
           * acesso de visualização das informações por consultas ANSI/SQL    
          
           * desenho/fluxograma completo da arquitetura
          
    AWS - Serviços componentes
    
          Glue
              - Crawler para o obter o formato dos arquivos
              
          Athenas          
              - Catalog - Presto para as consultas ANSI/SQL
              
          S3  
               - Tageamento
               - GPS
               
          EC2 - Instancia com o Airflow - Docker-compose com a infra neccessária
                Dags
                
          Lambda - 
          API-Gateway -
          RDS - Postgres -
          
          Airflow - Docker-Compose
          Terraform
          
## Modelo de dados :

            Frota - Caminhão - GPS - Tageamento - Estacionamento - Pedagio
            
            Frota      : modelo do caminhão, placa do caminhão
            Caminhão   : placa, nome do motorista , numero do aparelho GPS
            GPS        : numero do aparelho GPS, coordenadas de localização, dia e hora
            Tageamento : Placa, estacionamento , peda
