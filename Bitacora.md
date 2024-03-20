# Ensamblaje de C. kefyr solo usando lecturas largas. 

Previo a esto, se realizó identificación de taxonomía utilizando Kaju y se determinó que las lecturas de PacBio están contaminadas (>75%), este no es el caso de las lecturas de Illumina.
Debido a esto, se procedió a solo ensamblar con las lecturas largas usando: 

 - Smartdenovo
 - Flye
 - wtdbg2

Se pulirá con lecturas cortas y se hará scaffold utilizando el genoma de referencia.

# Conversión de .bam a .fq.gz

Se utilizó bedtools. NO USAR SAMTOOLS. Samtools filtra las secuencias y al momento de ensamblar sale un ensamblaje de <10mbps.

```
$bedtools_dir/bedtools bamtofastq -i pacbio_fofn_files/Y1_m54222_200717_093742.subreads.lbl094--lbl094.bam -fq Ckefyr.fastq
gzip Ckefyr.fastq
```

De allí, se procedió al ensamblaje usando el script de LRSDAY

# Identificación de centromeros
Para la identificación de centromeros se usaron las secuencias de centromeros de Kluyveromyces marxianus utilizando como referencia el artículo: 

> Establishment of a Cre-loxP System Based on a Leaky LAC4 Promoter and an Unstable panARS Element in Kluyveromyces marxianus
by Haiyan Ren 1,2,Anqi Yin 1,2ORCID,Pingping Wu 1,2,Huanyu Zhou 1,2,Jungang Zhou 1,2ORCID,Yao Yu 1,2,3,* andHong Lu 1,2,3,4,* doi: 10.3390/microorganisms10061240

# NOTA
Para el ensamblaje de Flye, se tuvo que realizar la conversión con Samtools, debido a que el archivo de bedtools nombra a los contigs de una manera no acepta por el ensamblador. 
Se pule con las lecturas cortas y se procede a realizar scaffolding con RagTag utilizando el genoma de referencia. 

# Problema
Al momento de hacer las anotaciones de centrómeros, los centrómeros no se encuentran donde se espera según la información. En el caso de Canu-smartdenovo, el cromosoma mitocondrial tiene el centrómero del cromosoma 2. En el caso de Smartdenovo solo, el cromosoma 7 tiene dos centrómeros, el que le corresponde y el centrómero 2. 
Tambien se hizo canu-wtdbg2, y wtdbg2. 

# 19/03/2024
Se instaló whokaryote para poder diferenciar entre contigs de prokaryotes y eukaryotes. 
Después, se corrió este programa utilizando los ensamblajes de Flye, Canu-smartdenovo, smartdenovo, wtdbg2, y canu-wtdbg2. 


