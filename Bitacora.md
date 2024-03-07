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


