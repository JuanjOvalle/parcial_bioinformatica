# parcial_bioinformatica

## Anotaciones y funciones repetidas
### Para entrar al cluster
  Se usará siempre que se quiera ingresar al cluster el comando: ssh -i bio.pt.pem -p 53841 bio.pt@loginpub-hpc.urosario.edu.co, ya que se está fuera del campus.
  
  Para pasar archivos locales al cluster se usará siempre la función: scp -i bio.pt.pem -P 53841 <ruta_del_archivo> bio.pt@login01-hpc.urosario.edu.co:<ruta_de_donde_quiero_guardarlo>
  
  Para pasar archivos del cluster al local se usará siempre la función: scp -r -i bio.pt.pem -P 53841 bio.pt@login01-hpc.urosario.edu.co:<ruta_del_archivo> <ruta_de_donde_quiero_guardarlo>
  
  Para crear carpetas se usará el comando: mkdir <Nombre de la carpeta>
  
  Para copiar archivos de un lugar a otro desde el mismo servidor se usará: cp <Dirección y nombre del archivo> <Dirección de destino>
  
  Se usó el comando 'salloc' para correr los alineamientos y funciones que requerían procesamiento.

### Para usar github desde la terminal
  Crear el directorio para git: git init -b main.
  
  Dentro del directorio ingresar usuario: git config --global user.name "JuanjOvalle"
  
  Dentro del directorio ingresar correo: git config --global user.name "juanjovalle.bio@outlook.com"
  
  Ingresar URL del repertorio: git remote add origin 
## Primer punto: BLAST
### Modificación por expresiones regulares
  Para reemplazar los nombres se usaron las siguientes expresiones: (\>\w+\.\w)(\s)(\w+)\s(\w+)(.*).
  
  Y se reemplazaron por: $1$2COI_$3_$4.
  
  El archivo quedó guardado como 'COI_s_exigua.fasta'.
  
  En el cluster, en una carpeta llamda "blast" dentro de la carpeta "parcial1" dentro de "JuanOvalle", se pasaron tanto la secuencia de referencia como las obtenidas a partir del popset.
  
  Usando el comando: module load blast/2.7.1, se cargó el script para BLAST.
  
  Luego se usó el comando:  makeblastdb -in query_s_exigua_COI -dbtype nucl -parse_seqids -out trans_s_exigua -title "S. exigua BLAST" ára crear la base de datos de BLAST a partir de las secuencias.
  
  Por último se usó:  blastn -query sec_refe.fasta -task megablast -db trans_s_exigua -outfmt 7 -word_size 7 -out blast_s_exigua -num_threads 1, para hacer el BLAST entre las secuencias y mi secuencia de referencia.
### Resultado
  Dado a que los porcentajes de identidad son muy altos, y los e-value muy bajos, se puede concluir que la secuencia de referencia corresponde con el gen de interés tomado a partir de las secuencias.
## Segundo punto: Alineamientos y árboles
### Concatenar
   Se usó el comando: cat query.fasta COI_s_exigua.fasta > query_s_exigua_COI.fasta
### Alineamiento múltiple con muscle
   Se cargó el programa de muscle por medio del comando: module load muscle/3.8.31
   
   Para obtener el alineamiento se usó: muscle -in query_s_exigua_COI.fasta -out s_exigua_alin.fasta
  
  Se hizo una copia del archivo en una carpeta creada previamente llamada "fasconcat".
### Fasconcat y árbol
  Previamante copiada la función 'FASconCAT-G_v1.05.1.pl' y el alineamiento 's_exigua_alin.fasta', se ejecutó: 
   ./FASconCAT-G_v1.05.1.pl, y se seleccionaron el formato Nexus por bloques y el Phylip relaxed, y se ejecutó,
  dando como resultado varios archivos, de entre ellos 'FcC_supermatrix.phy' el cual se usará para hacer el arbol.
  
  En otra carpeta llamada 'arbol' se copió el archivo 'FcC_supermatrix.phy' y se cargó iqtree con: module load       iqtree. Luego para generar el arbol se usó el comando: iqtree -s FcC_supermatrix.phy -m TEST -bb 1000 -pre 
  s_exigua_muscle_tree. A partir de esto se obtuvieron varios archivos entre ellos uno llamado s_exigua_muscle_tree.treefile, el cual se visualizó con: cat s_exigua_muscle_tree.treefile, y se copió en el portapapeles para exportarlo a la página de [Phylo](https://phylo.io/). El resultado se puede visualizar como [Imágen](https://www.dropbox.com/s/3hpdyoj3ft3b9k6/arbol_parcial.png?dl=0)
### Análisis
  Se encuentran 10 secuencias de 4 especies distintas, más la secuencia de referencia usada para el BLAST, como se esperaba, las secuencias peternecientes a la misma especie se encuentran cerca en el árbol, y se ve que la secuencia de *Spodoptera cilium* se ubica cerca a las de *Spodoptera exigua*, y es la más cercana a la secuencia de referencia (Query), el grupo de *Spodoptera* es cercano al de *Peridoma saucia*, y el más lejano es el de *Mythimna loreyi*.

## Tercer punto: Edición de archivos
  Para guardar el archivo desde la terminal se usó el comando: wget 'https://raw.githubusercontent.com/paula-torres/bioinformatica_ur/main/files/archivo1.csv'.
  
  Para ver el número de filas se usó: wc archivo1.csv, el cual muestra 3 datos, siendo el segundo el número de filas, en este caso 49.
  
  Para ver el número de columnas se usó: awk -F "," '{print NF; exit}' archivo1.csv, el cual da como resultado 4 columnas
  
  Para modificar "chr" por "Cromosoma", se usa el comando: sed 's/chr/Cromosoma/g' archivo1.csv > archivo_cromo.csv.
  
  Para cambiar la separación de comas a espacios se usó: sed 's/,/\t/g' archivo_cromo.csv > result_file.csv.
  
  Por último, para hacer un archivo con sólo los datos que tuvieran 'coding', se usó: grep -v no_coding result_file.bed > result_file_coding.bed.
  

## Cuarto punto: Subir archivos
### Comprimir archivos
  Para comprimir el archivo se usó: zip parcial_JuanOvalle.zip parcial1.
### Subir el archivo al repositorio
  Una vez se tiene el archivo en el local, se usa el comando: git remote add origin https://github.com/JuanjOvalle/parcial_bioinformatica.git
  
  Se confirma que se tengan permisos con: git remote -v
  
  Luego, se hace una copia del comprimido .zip a la carpeta creada para el git del repositorio del parcial, y se hacen los pasos descritos anteriormente dentro de esa carpeta.
  
  Luego se añade con: git add parcial1_JuanOvalle.zip
  
  Se confirma que esté el archivo con: git status.
  
  Se comete el archivo con: git commit git commit -m "Comprimido del parcial"
  
  Finalmente se envia al github con: git push origin main.
  
  
  
  
