# qPCR-multiple_gene_analysis_calculator
This code works like a calculator to analyze the relative quantification of qPCR data including multiple genes. The gene expression of living cells varies depending on various factors such as environment. For example, environmental stress can induce various stress response genes that in turn may help an individual to cope with the stress. Similarly, the gene expression can vary depending on food consumed, medicine used, or pollution exposed which may determine an individual’s susceptibility to disease. Furthermore, microbes can alter their gene expression when exposed to human body enhancing their pathogenicity. Hence, the gene expression can be determined by an environment that may lead to a response which may be indicative of several characteristics (e.g. diseases, pathogenicity, etc.).

Environment (e.g. compound ingested) ----------> Gene expression ----------> Response (e.g. disease)

Hence, gene expression analysis is performed widely to study several diseases, microbial pathogenicity, etc. 

The changes in gene expression can be quantitated using qPCR. The relative quantitation method (ddct) is used to determine the gene expression of sample of interest in comparison to reference sample (Rao et al, 2013). In ddct method, dct is obtained by subtracting ct value of a reference gene from ct value of a target gene to obtain dct. The reference gene is a gene that is constitutively expressed. Then dct value of a reference sample is subtracted from the dct of sample of interest to obtain ddct. The foldchange in gene expression compared to control is then obtained by 2^(-ddct).

dct= ct (target gene) - ct (reference gene)

ddct = dct (sample of interest) – dct (reference sample)

fold change= 2^(-ddct)

The fold change greater than 1 represents upregulation whereas fold change in between 0 to 1 represent downregulation. While representing this fold change on graph, the downregulation will be squeezed between 0 to 1 hence difficult to study. Thus, the fold change can be expressed as regulation where fold change > 1 is upregulation and a reciprocal of negative fold change is taken for fold change between 0 to 1 to determine the downregulation (Dhungel et al, 2021).

Fold change > 1 (upregulation)

Fold change <1 (-1/fold change, downregulation)

In this code, I have used this ddct method to determine the relative gene quantitation of sample of interest. An example of qPCR plate design is shown below. 

<img width="524" alt="qPCR_plate" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/203b46fa-d19a-4c49-a139-0d5028cc4443">

Each well on qPCR plate is coated with primers that correlate with gene. These genes may be related to various categories such as diseases, functions, etc. If the gene is present in sample used for qPCR, then they amplify which can be quantitated by ct values. Lower the Ct values higher the amount of gene present in the sample. The qPCR data analysis using this code is not dependent on the type of qPCR plate and can be used to analyze the data if Ct values are provided. The csv file format for the qPCR data is shown below. 

<img width="525" alt="qPCR_csv_file" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/863ae543-2f2f-48cd-822b-21c501b301b3">

It is important for user to have columns for gene and gene category. However, the number of samples for control and treatment groups can vary. 

At first, users are asked to provide names of file, columns for genes and gene category, reference gene (should be in gene category), and control sample. It is important to note that the reference gene name should be in gene category as it is not referring to the name of a particular gene but may include single or multiple genes in that category. 


<img width="478" alt="file_name_input" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/a590ad54-d78d-4610-8ce3-242177dd72ed">


Then users will be asked to provide the higher and lower ct cutoff values. During qPCR cycle, the primer-dimer may form which may falsely give a positive ct values. Hence, it is important to exclude these from the analysis. Thus, users are asked to provide the higher ct cut off values above which the gene expression will be considered as absent. Similarly, sometimes a very low ct values are seen erroneously. Hence, users are provided with opportunity to adress these issue during analysis. If user do not have lower ct cut off value then 'n' can be typed representing none. The Ct values above the higher ct cut off and below the lower ct cut off are considered absent.


<img width="471" alt="ct_cut_off" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/a76c8fb2-42e9-426b-bea4-364ba09ce523">


A data clean up is done to adress the 'NaN' (or missing values) present originally on the data and those considered as absent being greater than higher ct cut off or below lower ct cut off. For data clean up, the values greater than higher ct cut off or below lower ct cut off are replaced by 'NaN'. Then, these "NaN' values are replaced by mean ct values of particular treatment group (for example if one of the control sample has 'NaN' value then it is replaced by mean ct value obtained from other control sample). The ddct method provides relative quantitation of gene expression compared to control. Hence, if the gene expression for control is 0 (or 'NaN') then there is no baseline for comparison of gene expression. Hence, the row for gene with no amplication for all the control sample is dropped. Then, data is separated into rows with and without 'NaN' values. The ddct method is applied to data without 'NaN' values. However, if the gene is not amplified for a treatment group despite being amplified for control then it indicates that the treatment shut down the expression of certain gene (this is an extremely important result). Therefore, user will be provided later the data with 'NaN" values for treatment group depsite being expressed in control.  

Then user will be provided with an option to save csv file on gene regulation. If typed 'yes' then file name to be saved need to be provided.


<img width="471" alt="csv_file_name_input" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/3d3bc286-e77a-4b08-ab91-3ab12a975d07">


Then user will be asked to provide input on title and labels for heat map. The heat map for gene regulation and mean gene regulation will be generated.


<img width="420" alt="Heat_map_input" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/6a7648e3-024b-474a-95f7-6fd665d24823">


![heat_map_regulation](https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/03b2149d-180d-4b09-8fcf-2f5bae83155c)


![heat_map_mean_regulation](https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/4bc91282-7816-41f8-b7ee-7fea2dafc36d)


Then user will be asked to provide input on title and labels for bar chart. 


<img width="442" alt="bar_chart_input" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/5a4d7dbb-79d8-42fa-9a96-ed416330f323">


![barchart](https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/3cb0dd72-1546-47f5-82f6-504494399931)


Then user will be provided with an option to generate separate barchart and heat map for each gene category. If typed 'yes', then separate heat map and barchart with statistical significance for each gene category will be generated.


<img width="446" alt="separate_chart_options" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/34b90622-394d-46ab-84ea-bd5dddc672bb">


![bar_chart_apoptosis](https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/79bec631-7e05-4211-baad-421e391316b8)


![bar_chart_cell_signalling](https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/319a44f2-5b2b-4104-a6bd-5543357414db)


![separate_heat_map_apoptosis](https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/9c160bf7-7f50-499d-b661-e9d0e968508e)


![separate_heat_map_cell_signalling](https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/d645dff6-8767-490f-af26-30c5fbd22031)


Further, information on genes that were present in control but absent in any of the treatment groups will be provided. Here, the reference gene with 'NaN' values are removed as these genes should be consitutively expressed irrespective of treatment. Hence, if there is a discrepancy in expression of reference gene based on treatment then it is not a suitable reference gene. 


<img width="457" alt="nan_genes" src="https://github.com/Laxmi-Dhungel/qPCR-multiple_gene_analysis_calculator/assets/154451345/ed910c2c-967e-4239-b570-bf927c63d678">


At the end, users will be provided with an option to analyze next set of data.


Honestly speaking manually doing this qPCR analysis (using ddct) on excel for multiple genes and generating the barchart with statitstical significane and heatmap for seperate gene categories can take a day or days. Again, I cannot thank python and its tool enough for making this days of work possible only in few minutes. 






