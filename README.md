This repository contains data published in Artzi et al, 2021. Please read below for a description of the enclosed files.

data/:

GERAB
data/GERAB/GERAB_BACSU_full_b03.a2m: The final alignment file in .a2m format for the GERAB_BACSU sequence. This file is used to calculate evolutionary couplings (ECs). Lowercase columns indicate columns with too many gaps that did not meet the minimum column coverage threshold, which means they were excluded from the EC calculation. Lowercase columns have a '.' for gap character by convention. Additionally, sequences which did not fulfill the the minimum sequence coverage threshold (i.e. fragments with too many gaps) have been removed from this alignment.

data/GERAB_BACSU_full_b03.sto: This is the alignment in Stockholm format as output from Jackhmmer, which will show where there are insertions relative to the query sequence. Note that there might be more sequences in the Stockholm file than in the .a2m file, because we filter out fragments with > 50% gaps.

data/GERAB_BACSU_full_b03_CouplingScores.csv: For GerAB, the complete list of EVcouplings scores for all possible pairs of positions. Contains the evolutionary couplings sorted according to score, and the probability that a pair represents significant coupling rather than background noise (probability of belonging to the lognormal component of a lognormal (signal) - skew normal (noise) mixture model).

Note: this file contains couplings between positions that are close on the chain, which are known to be high due to short-range contacts in the molecule. You may want to filter these before further analysis.

Columns:

i: position i, numbered according to target sequence
A_i: character in position i in target sequence
Segment_i: (complexes only) specifies whether position i originates from the first monomer (A_1) or the second monomer (B_1). Position i is numbered according to its position within the monomer sequence, not its overall position in the concatenated alignment.
j: position j, numbered according to target sequence
A_j: character in position j in target sequence
Segment_j: (complexes only) specifies whether position j originates from the first monomer (A_1) or the second monomer (B_1). Position j is numbered according to its position within the monomer sequence, not its overall position in the concatenated alignment.
fn: placeholder column (formerly fn score)
cn: Evolutionary couplings score (cn score)
probability: Probability that this coupling is significant (i.e. in the lognormal signal tail)

data/GERAB_BACSU_full_b03_CouplingScores_longrange.csv: This is equivalent to the CouplingScores.csv file above, but has been pre-filtered to remove positions that are within 5 residues of each other on the sequence.

data/GERAB_BACSU_full_b03_alignment_statistics.csv: An output file that gives information about this particular alignment, including number of sequences. A description of the columns is below:

Columns:

prefix: run prefix
minimum_column_coverage: user input, fraction of non-gap characters required per column
num_seqs: number of sequences in final alignment
seqlen: length of target sequence (interchangeably called the query sequence)
num_cov: number of uppercase columns in final alignment (columns that satisfied minimumum_column_coverage)
num_lc: number of lowercase columns in final alignment (columns that did not satisfy minimum_column_coverage)
perc_cov: fraction of columns that are uppercase (num_cov / seqlen)
1st_uc: index of first uppercase column, numbered according to target sequence
last_uc: index of last uppercase column, numbered according to target sequence
len_cov: last_uc - 1st_uc
num_lc_cov: number of lowercase columns between 1st_uc and last_uc (i.e. num_cov = len_cov - num_lc_cov)
N_eff: effective number of non-redundant sequences after clustering based on theta parameter(similar neighborhood = 1 sequence)
domain_threshold: sequence search inclusion threshold
average_identity: average percent identity of sequences in the alignments to the target sequence


data/GERAB_BACSU_full_b03_annotation.csv: A file that contains the species identifier for each sequence in the Stockholm format alignment.

GERAA
Descriptions are equivalent to the files in GERAB, but running GERAA_BACSU instead.

GERAA_GERAB_complex
GerAA_b01_GerAB_b03_gd_CouplingScoresCompared_all.csv: A list of EVcouplings scores for all available pairs of residues, both within either GerAA or GerAB (intra-ECs) or between GerAA and GerAB (inter-ECs).
GerAA_b01_GerAB_b03_gd_CouplingScoresCompared_longrange.csv: A list of both intra- and inter-EC scores, but omitting any intra-ECs for residues that are within 5 amino acids of each other
GerAA_b01_GerAB_b03_gd_CouplingScoresCompared_inter.csv: The list of EVcouplings scores for just the inter-ECs (in other words, only includes scores for all possible pairs between GerAA and GerAB)
GerAA_b01_GerAB_b03_gd_first_distance_map_monomer.npy and GerAA_b01_GerAB_b03_gd_first_distance_map_monomer.csv: Two files that contain distance information from the known monomer structures of GerAA; used to calculate the blue dots in contact maps featuring GerAA.
GerAA_b01_GerAB_b03_gd_first_distance_map_multimer.npy and GerAA_b01_GerAB_b03_gd_first_distance_map_multimer.csv: Two files that contain distance information from the known possible homomultimer structures of GerAA (specifically taken from PDB structures where multiple chains corresponded to GerAA); used to calculate the orange dots in monomer contact maps featuring GerAA.
GerAA_b01_GerAB_b03_gd_first_structure_hits.csv: The list of PDB structures used to create monomeric and homomultimeric contacts for GerAA.


structures
data/structures/gerab_bacsu_5oqt_A.pir: The alignment file used by Modeller to build the homology model of the GerAB sequence against 5oqt
data/structures/gerab_bacsu_5oqt_A_modeller_3041349.pdb: the structure generated by Modeller, after using HHPRED to align GERAB_BACSU to the 5oqt sequence (alignment shown in the .pir file)

notebooks/:
notebooks/recreating_contact_map_figures.ipynb: A jupyter notebook that uses the files in this repo to recreate paper figures Fig. 1a, Supp. Fig. 1a, and Supp. Fig. 12a.
notebooks/recreating_contact_map_figures.html: An export of the above notebook to allow for easier viewing.

Additional notes:
The zipped datasets for running the complex pipeline (the ENA tables etc) can be found at doi:10.6084/m9.figshare.16873912
