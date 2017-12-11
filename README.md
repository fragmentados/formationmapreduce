# formationmapreduce

Ejemplo práctico de contador de palabras utilizando el modelo de programación de MapReduce.

Utilizamos docker y hadoop para ejecutarlo. Los comandos necesarios son los siguientes:

1) Testeamos nuestro código:

echo "foo foo quux labs foo bar quux" | python3 mapper.py

cat libros/4300-0.txt | python3 mapper.py

2) Arrancamos la imagen de docker:

sudo docker run --hostname=quickstart.cloudera --privileged=true -t -i -v /home/elias/MapReduce:/home/cloudera/practicas --publish-all=true -p 7180 cloudera/quickstart /usr/bin/docker-quickstart

3) Colocamos la carpeta con los libros en el sistema de ficheros distribuido:

hdfs dfs -put libros/

Podemos visualizarlo con:

hdfs dfs -ls

4) Arrancamos mapreduce a través de hadoop:

/usr/bin/hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming-2.6.0-cdh5.7.0.jar -input libros -output salida_libros -mapper mapper.py -reducer reducer.py -file mapper.py -file reducer.py

5) Comprobamos el resultado:

hdfs dfs -ls salida_libros

hdfs dfs -cat salida_libros/part-00000

Podemos obtener esta carpeta mediante:

hdfs dfs -get salida_libros

6) Eliminamos la imagen de docker mediante los comandos:

sudo docker ps -a

docker rm id_image


