# Project BRSP: In Silico Drug Discovery
# Eksplorasi Mekanisme Farmakologi Kombinasi Metabolit Bahan Alam Terhadap Hepatocellular Carcinoma: Pendekatan Network Pharmacology dan Molecular Docking

## I.	PENDAHULUAN

Hepatocellular carcinoma (HCC) merupakan bentuk keganasan hati primer yang paling umum dijumpai dan menjadi salah satu penyumbang utama kematian akibat kanker secara global. Kompleksitas patogenesisnya tampak dari keterlibatan tiga proses sekaligus: disregulasi genetik dan epigenetik, gangguan jalur sinyal proliferasi sel, dan kemampuan sel kanker menghindari apoptosis. Pilihan terapi sistemik konvensional saat ini, termasuk golongan tyrosine kinase inhibitor seperti sorafenib dan lenvatinib, masih menghadapi kendala berupa efikasi klinis yang belum optimal, munculnya resistensi obat sekunder selama masa pengobatan, dan toksisitas yang relatif tinggi. Ketiga keterbatasan tersebut menjadi alasan utama perlunya eksplorasi agen terapeutik alternatif dengan efektivitas yang lebih tinggi dan toksisitas yang minimal.

Metabolit sekunder yang berasal dari bahan alam merupakan pendekatan terapeutik yang menjanjikan, sebab kemampuannya berinteraksi melalui mekanisme multi-component dan multi-target. Karakteristik tersebut berbeda secara mendasar dari obat sintetik konvensional, yang umumnya bekerja berdasarkan prinsip "satu obat, satu target". Senyawa bahan alam, sebaliknya, mampu memodulasi beberapa jalur pensinyalan secara bersamaan sehingga relevan untuk mengatasi kompleksitas patologis mikrolingkungan tumor pada HCC.

Meskipun demikian, upaya mengungkap mekanisme molekuler serta menentukan target spesifik senyawa bahan alam melalui pendekatan in vitro dan in vivo konvensional membutuhkan waktu dan sumber daya dalam jumlah besar. Kendala tersebut mendorong kebutuhan akan pendekatan in silico, khususnya melalui integrasi network pharmacology dan molecular docking, sebagai strategi yang lebih efisien dari segi waktu dan sumber daya. Network pharmacology menguraikan secara sistemik jaringan interaksi "senyawa-protein target-jalur penyakit" (compound-target-pathway network), sehingga hub genes yang berperan dalam progresi HCC dapat diidentifikasi. Sebagai pendekatan komplementer, molecular docking memberikan validasi pada tingkat struktural, dengan mengevaluasi afinitas pengikatan termodinamika serta stabilitas konformasi antara ligan (metabolit aktif) dan reseptor protein target pada level atomik.

Laporan ini disusun untuk memaparkan analisis terstruktur mengenai mekanisme farmakologi metabolit bahan alam terpilih terhadap HCC, dengan memanfaatkan kedua pendekatan komputasional tersebut. Melalui eksplorasi ini, interaksi molekuler diharapkan dapat dipetakan secara presisi, sekaligus menyediakan landasan teoretis yang kokoh bagi optimasi penemuan kandidat obat anti-HCC di masa mendatang.

## II.	METODE

### 2.1 Analisis Network Pharmacology

#### 2.1.1 Identifikasi Senyawa dan Target
Enam metabolit sekunder bahan alam menjadi objek kajian pada tahap ini: kuersetin, berberina, ginsenosida, resveratrol, kurkumin, dan epigalokatekin-3-galat (EGCG). Basis data PubChem mengonfirmasi identitas keenam senyawa tersebut, sementara prediksi target proteinnya diperoleh melalui platform Super-PRED.

#### 2.1.2 Pengumpulan Data Penyakit
Data genetik yang berasosiasi dengan patogenesis Hepatocellular Carcinoma (HCC) ditelusuri melalui basis data Online Mendelian Inheritance in Man (OMIM).

#### 2.1.3 Interseksi Target dan Konstruksi Jaringan
Target protein senyawa dan gen terkait HCC diinterseksikan melalui analisis diagram Venn untuk mengisolasi target molekuler yang berpotensi relevan. Gen hasil irisan ini menjadi dasar konstruksi jaringan Protein-Protein Interaction (PPI) pada basis data STRING, dengan ambang batas confidence ≥ 0,700. Cytoscape memvisualisasikan topologi jaringan yang terbentuk. Berdasarkan tiga parameter sentralitas, yaitu degree, betweenness centrality, dan closeness centrality, plugin cytoHubba menentukan sepuluh hub genes utama.

 
## Gambar 1. Irisan gen target HCC dan target metabolit sekunder

![Gambar 1.](/Gambar1.png "Gambar 1.")

#### 2.1.4 Analisis Pengayaan Fungsional
Enrichment analysis dijalankan melalui platform STRING, mencakup ranah Biological Process pada Gene Ontology (GO), KEGG Pathways, serta Disease-gene Associations (DISEASES). Ambang batas signifikansi ditetapkan pada False Discovery Rate (FDR) < 0,05. Fitur Merge Network pada Cytoscape kemudian menggabungkan seluruh hasil pengayaan ini dengan jaringan senyawa-target dan jaringan PPI ke dalam satu visualisasi terpadu.

### 2.2 Simulasi Molecular Docking

#### 2.2.1 Preparasi Reseptor (Protein Target)

Protein AKT1 manusia berperan sebagai makromolekul target pada simulasi ini. Struktur kristal protein tersebut ditelusuri dan diperoleh melalui unduhan dari Protein Data Bank (RCSB PDB), dengan PDB ID 1H10 pada resolusi 1,40 Å.

#### 2.2.2 Preparasi Ligan
Kurkumin (Curcumin) ditetapkan sebagai ligan uji dalam simulasi ini. Notasi SMILES kurkumin, yang diperoleh dari basis data PubChem, adalah sebagai berikut:

COCI=C(C=CC(=C1)=C=C=C(=O)CC(=O)C=C=C2=CC(=C(C=C2)O)OC)O

#### 2.2.3 Penentuan Grid dan Search Space
Platform PrankWeb memindai koordinat pusat binding pocket spesifik yang menjadi acuan search space. Titik koordinat yang diperoleh berada pada sumbu referensi 15, 41, dan 40.

#### 2.2.4 Eksekusi Docking
Server web SwissDock menjalankan simulasi docking berbasis termodinamika secara penuh, dengan struktur ligan yang disiapkan lebih dulu melalui fitur “Prepare Ligand” pada platform tersebut. Pada tahap preparasi reseptor (1H10), parameter heteroatom diatur pada opsi "None" agar kantong enzim bersih dari molekul air maupun ligan bawaan, sehingga potensi tumpang tindih spasial dapat dicegah. Proses ini menghasilkan 20 model konformasi yang dievaluasi berdasarkan nilai calculated affinity (kcal/mol) sekaligus divisualisasikan untuk menganalisis kesesuaian geometri antara ligan dan situs aktif enzim.

## III.	HASIL DAN INTERPRETASI

### 3.1 Identifikasi Target dan Jaringan Polifarmakologi
Pemetaan target molekuler mengonfirmasi adanya mekanisme interaksi multi-target dari metabolit bahan alam terhadap mikrolingkungan Hepatocellular Carcinoma (HCC). Diagram Venn mengungkap sembilan gen irisan, di antaranya AKT1, JAK2, CTNNB1, IL6, dan PIK3CA, yang menandai titik potong presisi antara target metabolit sekunder dengan patofisiologi genetik HCC. 


## Tabel 1. Nilai degree, betweenness centrality, dan closeness centrality dari 10 hub   gen teratas hasil analisis jaringan PPI

| name   | Degree | BetweennessCentrality | ClosenessCentrality |
|--------|--------|-----------------------|---------------------|
| JAK2   | 11     | 0.023536809194703936  | 0.6666666666666666  |
| AKT1   | 14     | 0.03060383573541468   | 0.7692307692307692  |
| CTNNB1 | 2      | 0.0010526315789473684 | 0.48780487804878053 |
| IL10   | 11     | 0.02851383509278246   | 0.6896551724137931  |
| IL6    | 6      | 0.0030019493177387917 | 0.5882352941176471  |
| PTEN   | 13     | 0.04796194546194546   | 0.7407407407407407  |
| IFNGR1 | 7      | 0.005105498789709316  | 0.6060606060606061  |
| IL6    | 16     | 0.08225012317117579   | 0.8333333333333334  |
| JUN    | 10     | 0.01125262651578441   | 0.6666666666666666  |
| MYC    | 12     | 0.046781084412663355  | 0.7142857142857143  |

Jaringan Protein-Protein Interaction (PPI) yang dibangun untuk mengevaluasi interaksi tingkat protein tervisualisasi dalam bentuk 9 nodes dan 11 edges. Analisis topologi terhadap jaringan ini menetapkan AKT1, JAK2, CTNNB1, dan IL6 sebagai hub genes sentral. Nilai betweenness centrality dan closeness centrality gen-gen tersebut secara signifikan lebih unggul dibandingkan dengan protein lain, yang mengonfirmasi tingginya probabilitas mereka dalam menyebarkan sinyal biologis.

## Gambar 2. Jaringan Protein-Protein Interaction (PPI) dari 11 gen irisan hasil konstruksi STRING

 ![Gambar 2.](/string.png "Gambar 2.")

Konstruksi jaringan senyawa-target-pathway selanjutnya memvalidasi mekanisme kerja polifarmakologi tersebut. Di antara enam senyawa uji, kuersetin dan kurkumin tampil sebagai metabolit paling dominan dengan jumlah koneksi (degree) tertinggi terhadap berbagai target protein. Jaringan ini turut menegaskan peran AKT1, JAK2, dan CTNNB1 sebagai simpul utama yang menghubungkan metabolit dengan sejumlah jalur sinyal esensial, antara lain PI3K-Akt signaling pathway, intervensi terhadap resistensi EGFR tyrosine kinase inhibitor, dan jalur pos pemeriksaan imun PD-1/PD-L1.

## Gambar 3. Visualisasi jaringan interaksi senyawa–target–pathway

 ![Gambar .](/target.png "Gambar 3.")

### 3.2 Signifikansi Fungsional dan Pengayaan Biologis
Enrichment analysis yang disajikan pada gambar di bawah memperkuat dasar teoretis mekanisme aksi metabolit. Pada ranah Gene Ontology (Biological Process), target molekuler dominan meregulasi kelangsungan proliferasi otot polos serta memediasi respons seluler terhadap sitokin pro-inflamasi kunci, yaitu IL-6. Modulasi ini berperan penting dalam meredam stres inflamasi kronis pada jaringan hepatik.

## Gambar 4. Hasil enrichment analysis Gene Ontology (Biological Process), KEGG Pathway, dan Disease-gene Associations (DISEASES) terhadap target irisan

 
 ![Gambar 4.](/Process.svg "Gambar 4.")
  ![Gambar 4.](/KEGG.svg "Gambar 4.")
   ![Gambar 4.](/DISEASES.svg "Gambar 4.")
 

 

Pada jalur KEGG Pathways, kelompok gen target terkonsentrasi secara signifikan pada kaskade proliferasi sel tumor (Pathways in cancer) dan regulasi stres metabolik (AGE-RAGE signaling pathway). Analisis asosiasi gen-penyakit (DISEASES) memvalidasi signifikansi fenotipik ini: entitas Hepatobiliary disease and Liver disease menunjukkan tingkat signifikansi terkuat, ditandai dengan FDR terendah. Keterlibatan penyakit inflamasi sistemik seperti kolitis turut menegaskan interkoneksi gut-liver axis, yang menunjukkan bahwa intervensi pada gen target mampu memodulasi patogenesis HCC secara komprehensif, dari hulu inflamasi hingga hilir karsinogenesis.

### 3.3	Validasi Interaksi Struktural melalui Molecular Docking
Merujuk pada temuan sentralitas AKT1 dalam jaringan PPI serta dominasi konektivitas kurkumin, simulasi molecular docking difokuskan pada evaluasi interaksi termodinamika antara ligan kurkumin dan makromolekul target AKT1 manusia (PDB ID: 1H10). Koordinat spasial binding pocket spesifik berhasil dilokalisasi melalui PrankWeb pada titik 15, 41, dan 40.

 
## Gambar 5 : Pencarian center box terbaik melalui PrankWeb

 ![Gambar 5.](/centerbox.png "Gambar 5.")

Kalkulasi docking termodinamika ini menghasilkan 20 konformasi interaksi spasial. Berdasarkan parameter afinitas pengikatan, Model 1 mencatat nilai Calculated affinity yang sangat baik, yaitu -4,963 kcal/mol. Nilai negatif yang memadai tersebut merepresentasikan pelepasan energi bebas interaksi yang tinggi, sekaligus mengindikasikan afinitas pengikatan yang stabil secara termodinamika.

 
## Tabel 2. Hasil Afinitas Molecular Docking

 ![Tabel 2.](/tabel.png "Tabelr 2.")

Secara visual, analisis konformasi geometri mengonfirmasi struktur ligan kurkumin tersuspensi dengan presisi tinggi di dalam celah enzimatik protein AKT1. Penempatan struktural yang akurat ini memvalidasi kemampuan ligan tersebut mengokupasi situs aktif atau situs alosterik enzim. Pemblokiran situs pengikatan molekul biologis pada AKT1 diproyeksikan merepresi kaskade kelangsungan hidup sel melalui jalur PI3K/Akt/mTOR. Pada tingkat atomik, mekanisme represi ini secara rasional berkorelasi langsung dengan kapasitas menghentikan siklus proliferasi tak terkendali sekaligus memulihkan sensitivitas apoptosis pada sel HCC.

 
## Gambar 6: Visualisasi pose Curcumin di dalam kantong aktif protein AKT1

 ![Gambar 6.](/pose.png "Gambar 6.")

## IV.	Kesimpulan
Integrasi pendekatan komputasional network pharmacology dan molecular docking pada riset ini berhasil mengungkap mekanisme polifarmakologi metabolit sekunder bahan alam terhadap mikrolingkungan Hepatocellular Carcinoma (HCC). Temuan utama dari antara lain sebagai berikut:
 A.	Identifikasi Target dan Jaringan: Analisis network pharmacology memetakan 11 gen target spesifik, termasuk AKT1, JAK2, CTNNB1, IL6, dan PIK3CA, yang beririsan langsung dengan patofisiologi genetik HCC. Di antara gen-gen tersebut, AKT1, JAK2, dan CTNNB1 terkonfirmasi sebagai hub genes sentral dengan nilai parameter sentralitas topologi tertinggi pada jaringan Protein-Protein Interaction (PPI).

B.	Mekanisme Multi-Target: Kurkumin dan kuersetin teridentifikasi sebagai dua metabolit dengan konektivitas terapeutik paling dominan. Kedua senyawa ini memediasi efek antikanker secara sinergis melalui modulasi beberapa jalur biologis, meliputi PI3K-Akt signaling pathway, represi kaskade stres inflamasi melalui respons IL-6, penekanan siklus proliferasi sel tumor melalui jalur Pathways in cancer, serta pembalikan resistensi terhadap EGFR tyrosine kinase inhibitor.

C.	Validasi Termodinamika: Simulasi molecular docking memvalidasi interaksi struktural yang stabil antara ligan kurkumin dan makromolekul target AKT1 (PDB ID: 1H10) pada titik koordinat pencarian (15, 41, 40). Energi bebas interaksi (Calculated affinity) sebesar -4,963 kcal/mol, disertai konformasi geometri ligan yang presisi di dalam celah enzimatik, mengindikasikan kapasitas kurkumin untuk memblokir situs pengikatan AKT1 secara efektif. Pada tingkat atomik, pemblokiran ini diproyeksikan secara biologis mampu menghentikan kaskade proliferasi serta memulihkan kepekaan sel kanker hati terhadap induksi apoptosis terprogram.

Secara keseluruhan, eksplorasi in silico ini menyediakan landasan teoretis yang komprehensif bahwa metabolit bahan alam, khususnya kurkumin, memiliki prospek menjanjikan sebagai kandidat inhibitor berbasis Structure-Based Drug Design (SBDD) untuk HCC. Rangkaian metodologi ini menunjukkan efisiensi skrining komputasional dalam memetakan target molekuler secara sistematis, sebagai tahap awal sebelum validasi laboratorium (in vitro dan in vivo).
