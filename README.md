# GEN rbcL EN POLYLEPIS DE ECUADOR
Polylepis nativos.

Q1. ¿En qué organismo o grupo de organismos vas a trabajar?
Voy a trabajar con árboles del género Polylepis, nativos de los Andes y presentes en los ecosistemas de alta montaña del Ecuador, como páramos y bosques montanos. Estas especies son fundamentales para la provisión de servicios ecosistémicos, como la regulación hídrica y la conservación de biodiversidad, pero muchas están amenazadas por la deforestación, el cambio climático y la expansión agropecuaria.

Q2. Brevemente describe qué piensas hacer en tu proyecto
Mi proyecto consiste en analizar la disponibilidad y diversidad de secuencias del gen rbcL (gen cloroplastídico ampliamente usado en estudios filogenéticos) para las especies de Polylepis nativas del Ecuador, como P. incana, P. sericea, P. microphylla, P. pauta, entre otras.
Quiero evaluar si existen suficientes datos genéticos públicos para estas especies y, si no los hay, evidenciar esta falta como una limitación para la investigación y conservación. También quiero construir una filogenia preliminar con los datos disponibles para observar relaciones entre especies.

Q3. ¿Qué programas voy a usar en mi proyecto?

- Conexión con un supercomputador en este caso Hoffman2
- Muscle
- IQTREE
- FigTree (http://tree.bio.ed.ac.uk/software/figtree/)
- EDirect

Pregunta de investigación:
¿Existe suficiente información genética (secuencias del gen rbcL) para las especies de Polylepis nativas del Ecuador en bases de datos públicas, o hay una brecha importante que limita los esfuerzos de conservación, identificación y estudio de su diversidad genética?

¿Por qué es importante este trabajo?
La falta de información genética básica impide conocer con precisión la diversidad y relaciones evolutivas de estas especies. Esto es especialmente crítico en Ecuador, donde muchas especies de Polylepis son endémicas o están mal estudiadas. Mejorar la disponibilidad de datos podría fortalecer los planes de conservación, restauración ecológica y estrategias de protección frente al cambio climático.

Q4. Imagen https://phytokeys.pensoft.net/article/83529/zoom/fig/16/

Diseño de Proyecto:

Importar las secuencias de NCBI con EDirect
Alinear las secuencias importadas desde NCBI (MUSCLE)
Descargar el output del alineamiento
Ejecutar las filogenias posibles (IQTREE)
Finalmente visualizar las filogenias en un árbol (FIGTREE)

1. Conectarse al supercomputador Hoffman2
Accede al servidor mediante tu cuenta institucional para iniciar el análisis.

2. Instalar EDirect
Ejecuta este comando para instalar las herramientas de EDirect:

sh -c "$(curl -fsSL https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh)"

3. Verificar que la instalación fue exitosa
esearch -version

5. Buscar y guardar los IDs de las secuencias rbcL del género Polylepis
esearch -db nucleotide -query "Polylepis[Organism] AND rbcL[Gene] AND 500:3000[Sequence Length]" |
efetch -format uid > polylepis_rbcl_ids.txt

7. Descargar las secuencias en formato FASTA
efetch -db nucleotide -id $(cat polylepis_rbcl_ids.txt) -format fasta > polylepis_rbcl.fasta

9. Verificar que las secuencias se descargaron correctamente
grep ">" polylepis_rbcl.fasta

11. Alinear las secuencias con MUSCLE
Asegúrate de tener MUSCLE instalado y ejecuta:
./muscle3.8.31_i86linux64 -in polylepis_rbcl.fasta -out polylepis_rbcl.alineamiento.fasta -maxiters 1 -diags

13. Crear la filogenia con IQ-TREE
Primero carga el módulo de IQ-TREE:
module load iqtree/2.2.2.6
Luego ejecuta el análisis filogenético:
iqtree2 -s polylepis_rbcl.alineamiento.fasta
Esto generará varios archivos nuevos basados en tu alineamiento, incluyendo el importante archivo con extensión .treefile.

14. Visualizar la filogenia con FigTree
Descarga el programa desde: http://tree.bio.ed.ac.uk/software/figtree/

Copia el archivo .treefile a tu escritorio local con scp, usando la ruta que obtuviste con pwd.

Abre el archivo .treefile en FigTree.

Ahora puedes visualizar la filogenia de las secuencias del gen rbcL del género Polylepis.

RESULTADOS: 
![ÁRBOL](https://github.com/renatabarreracabezas/PROYECTO-FINAL-BIOINFORMATICA/blob/main/Polylepis_rbcl.fasta.treefile.png)
