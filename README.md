# parcial_bioinformatica

## Anotaciones y funciones repetidas
### Para entrar al cluster
  Se usará siempre que se quiera ingresar al cluster el comando: ssh -i bio.pt.pem -p 53841 bio.pt@loginpub-hpc.urosario.edu.co, ya que se está fuera del campus.
  
  Para pasar archivos locales al cluster se usará siempre la función: scp -i bio.pt.pem -P 53841 <ruta_del_archivo> bio.pt@login01-hpc.urosario.edu.co:<ruta_de_donde_quiero_guardarlo>
  
  Para pasar archivos del cluster al local se usará siempre la función: scp -r -i bio.pt.pem -P 53841 bio.pt@login01-hpc.urosario.edu.co:<ruta_del_archivo> <ruta_de_donde_quiero_guardarlo>
  
  Para crear carpetas se usará el comando: mkdir <Nombre de la carpeta>
  
  Para copiar archivos de un lugar a otro desde el mismo servidor se usará: cp <Dirección y nombre del archivo> <Dirección de destino>
  
  Se usó el comando 'salloc' para correr los alineamientos y funciones que requerían procesamiento.

## Primer punto: BLAST
### Modificación por expresiones regulares
  Para reemplazar los nombres se usaron las siguientes expresiones: (\>\w+\.\w)(\s)(\w+)\s(\w+)(.*).
  
  Y se reemplazaron por: $1$2COI_$3_$4.
  
  El archivo quedó guardado como 'COI_s_exigua.fasta'.

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
   

## Tercer punto: Edición de archivos

## Cuarto punto: Subir archivos
