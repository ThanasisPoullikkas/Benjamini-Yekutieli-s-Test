# Benjamini-Yekutieli-s-Test
import numpy as np
from statsmodels.stats.multitest import multipletests

# File paths
input_file = "pvalues.txt"           # Input file with one p-value per line
output_file = "adjusted_pvalues.txt" # Output file with original + adjusted p-values

# Read p-values from file
with open(input_file, 'r') as f:
    p_values = [float(line.strip()) for line in f if line.strip()]

# Perform Benjamini–Yekutieli adjustment
adjusted_results = multipletests(p_values, alpha=0.05, method='fdr_by')
adjusted_pvals = adjusted_results[1]  # Second item is adjusted p-values

# Write original and adjusted p-values to output file
with open(output_file, 'w') as f:
    f.write("Original_P\tAdjusted_P_BY\n")
    for original, adjusted in zip(p_values, adjusted_pvals):
        f.write(f"{original:.6f}\t{adjusted:.6f}\n")

print(f"Original and BY-adjusted p-values written to '{output_file}'")
