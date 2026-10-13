# CIPA, part three: where on the protein does it break?

Part one asked whether a model could separate pathogenic NTRK1 variants from benign ones. Part two looked at the cells. This one asks where, physically, on the actual folded protein, the pathogenic variants land.

## What I did

I took the 706 labeled variants from part one and pulled their absolute amino acid positions from the raw CADD annotations, 558 variants had a usable position. I pulled NTRK1's real domain boundaries directly from UniProt (not guessed, the protein kinase domain is residues 510-781, confirmed via their REST API), mapped every variant onto AlphaFold's predicted structure for NTRK1, and tested whether pathogenic variants concentrate in the kinase domain more than benign ones.

## What I found

They do, and it's statistically real, not just a visual impression. **56.5% of pathogenic variants fall inside the kinase domain, versus 35.9% of benign variants** (Fisher's exact test, odds ratio 2.31, p = 0.0004).

The 3D structure makes this tangible: pathogenic variants (red) cluster densely in and around the kinase domain (gold), while benign variants (blue) scatter more evenly across the whole protein, including the extracellular domains that aren't doing the actual catalytic work.

This makes biological sense. The kinase domain is where NTRK1 phosphorylates itself and its downstream signaling partners, the part of the protein actually doing the job. A change there is simply more likely to break the whole mechanism than a change somewhere less functionally critical.

## A caveat worth stating

This AlphaFold structure has lower confidence in some flexible regions (about 15% of residues fall in the lowest pLDDT confidence band), so I'm not over-interpreting exact 3D positioning in those stretches. The kinase domain itself, fortunately, is typically one of the better-resolved regions in receptor tyrosine kinase structures, which is part of why this result holds up.

## Repo structurenotebooks/ # Colab notebook: position extraction, domain mapping, statistics, 3D visualization
data/ # AlphaFold structure (AF-P04629-F1-model_v6.pdb), raw variant data
results/ # Position histogram, 3D structure screenshot, variants-with-positions CSV
## Data sources

- Structure: [AlphaFold DB, P04629](https://alphafold.ebi.ac.uk/entry/P04629)
- Domain annotations: [UniProt, P04629](https://www.uniprot.org/uniprotkb/P04629)
- Variant data: [MyVariant.info](https://myvariant.info) (ClinVar, CADD)

## Series so far

1. [NTRK1 variant pathogenicity classifier](https://github.com/Bioinformatician0507/cipa-ntrk1-variants)
2. [DRG cell type analysis](https://github.com/Bioinformatician0507/cipa-drg-celltypes)
3. This project

---
Iqra Nadeem | [LinkedIn](https://linkedin.com/in/iqra-nadeem) | [GitHub](https://github.com/Bioinformatician0507)
