# parcial_bioinformatica

## Anotaciones y funciones repetidas
### Para entrar al cluster
  Se usará siempre que se quiera ingresar al cluster el comando: ssh -i bio.pt.pem -p 53841 bio.pt@loginpub-hpc.urosario.edu.co, ya que se está fuera del campus.
  
  *Para pasar archivos locales al cluster se usará siempre la función: scp -i bio.pt.pem -P 53841 <ruta_del_archivo> bio.pt@172.25.255.10:<ruta_de_donde_quiero_guardarlo>
  
  **Para pasar archivos del cluster al local se usará siempre la función: scp -r -i bio.pt.pem -P 53841 bio.pt@login01-hpc.urosario.edu.co:<ruta_del_archivo> <ruta_de_donde_quiero_guardarlo>

## Primer punto: BLAST
### Modificación por expresiones regulares
  Para reemplazar los nombres se usaron las siguientes expresiones: (\>\w+\.\w)(\s)(\w+)\s(\w+)(.*).
  
  Y se reemplazaron por: $1$2COI_$3_$4.
  
  El archivo quedó guardado como 'COI_s_exigua.fasta'.

## Segundo punto: Alineamientos y árboles

## Tercer punto: Edición de archivos

## Cuarto punto: Subir archivos
