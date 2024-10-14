# BDA

## Comandos

docker pull cassandra:latest  
docker-compose up  
docker cp postulaciones.csv nodo1:postulaciones.csv  

docker exec -it nodo1 bash *Para abrir la terminal del nodo1*  
Dentro de la terminal del nodo:  
cqlsh
CREATE KEYSPACE lab_cassandra WITH replication = {'class':'SimpleStrategy','replication_factor': 3 };  
use lab_cassandra;

## Queries
 Dentro del nodo y después de "use lab_cassandra;"  

###############################  
1° Query  
###############################  

CREATE TABLE carrera (  
 cedula text,  
 periodo int,  
 sexo text,  
 preferencia text, 
 carrera text,  
 matriculado text,  
 facultad text,  
 puntaje int,  
 grupo_depen text,  
 region text,  
 latitud text,  
 longitud text,   
 ptje_nem int,  
 psu_promlm int,  
 pace text,  
 gratuidad text,  
 Primary key ((carrera, matriculado), periodo, cedula)  
);  
  
COPY carrera (  
CEDULA, PERIODO, SEXO, PREFERENCIA, CARRERA, MATRICULADO, FACULTAD, PUNTAJE, GRUPO_DEPEN, REGION, LATITUD, LONGITUD, PTJE_NEM, PSU_PROMLM, PACE, GRATUIDAD  
) FROM 'postulaciones.csv'  
WITH DELIMITER=';'  
AND HEADER=true;  
  
SELECT * FROM carrera WHERE carrera='MEDICINA' AND matriculado='SI';  
  
###############################  
2° Query  
###############################  
  
CREATE TABLE region_carrera (  
 cedula text,  
 periodo int,  
 sexo text,  
 preferencia text,  
 carrera text,  
 matriculado text,  
 facultad text,  
 puntaje int,  
 grupo_depen text,  
 region text,  
 latitud text,  
 longitud text,  
 ptje_nem int,  
 psu_promlm int,  
 pace text,  
 gratuidad text,  
 Primary key ((region, carrera, matriculado), periodo, cedula)  
);  
  
COPY region_carrera (  
CEDULA, PERIODO, SEXO, PREFERENCIA, CARRERA, MATRICULADO, FACULTAD, PUNTAJE, GRUPO_DEPEN, REGION, LATITUD, LONGITUD, PTJE_NEM, PSU_PROMLM, PACE, GRATUIDAD  
) FROM 'postulaciones.csv'  
WITH DELIMITER=';'  
AND HEADER=true;  
  
SELECT * FROM region_carrera WHERE region='MAULE' AND carrera='INGENIERÍA CIVIL INFORMÁTICA' AND matriculado='SI';  
  
###############################  
3° Query  
###############################  
  
CREATE TABLE facultad (  
 cedula text,  
 periodo int,  
 sexo text,  
 preferencia text,  
 carrera text,  
 matriculado text,  
 facultad text,  
 puntaje int,  
 grupo_depen text,  
 region text,  
 latitud text,  
 longitud text,  
 ptje_nem int,  
 psu_promlm int,  
 pace text,   
 gratuidad text,  
 Primary key ((facultad, matriculado), puntaje, cedula)  
);  

COPY facultad (  
CEDULA, PERIODO, SEXO, PREFERENCIA, CARRERA, MATRICULADO, FACULTAD, PUNTAJE, GRUPO_DEPEN, REGION, LATITUD, LONGITUD, PTJE_NEM, PSU_PROMLM, PACE, GRATUIDAD  
) FROM 'postulaciones.csv'  
WITH DELIMITER=';'  
AND HEADER=true;  
  
SELECT * FROM facultad WHERE facultad='CIENCIAS DE LA SALUD' AND matriculado='SI';  
 