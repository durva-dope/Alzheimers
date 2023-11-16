import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset into a Pandas DataFrame
df = pd.read_excel('ADNI_Mitochondrial_Haplotypes.xlsx')

# Display the entire dataset to provide a comprehensive view
print("Complete dataset:")
pd.set_option('display.max_rows', None)
print(df)

# Define the column name ('HAPLOTYPE') for genetic haplotypes
haplotype_column = 'HAPLOTYPE'

# Calculate the frequency of each genetic haplotype
haplotype_frequencies = df[haplotype_column].value_counts()

# Present the genetic haplotype frequencies
print("Genetic Haplotype Frequencies:")
print(haplotype_frequencies)

#combined bar chart and line plot

with plt.style.context("seaborn"):
    
    fig, ax1 = plt.subplots(figsize=(12, 6))

    custom_blue = "#3498db"
    sns.barplot(x=haplotype_frequencies.index, y=haplotype_frequencies.values, color=custom_blue, ax=ax1)
    ax1.set_title("Genetic Haplotype Frequencies")
    ax1.set_xlabel("Haplotype")
    ax1.set_ylabel("Frequency")
    ax1.set_xticklabels(ax1.get_xticklabels(), rotation=45, horizontalalignment='right', fontsize=15)
    for p in ax1.patches:
        ax1.annotate(f'{int(p.get_height())}', (p.get_x() + p.get_width() / 2., p.get_height()), ha='center', va='baseline')
    ax2 = ax1.twinx()
    ax2.plot(range(len(haplotype_frequencies)), haplotype_frequencies.values, marker='o', linestyle='-', color='red', label='Line Plot')
    ax2.set_ylabel("Line Plot Values")
    ax2.legend(loc='upper right')

plt.show()
plt.savefig('chart.png')


haplotype_frequencies = df[haplotype_column].value_counts()

# Generate a bar chart to visualize haplotype frequencies
plt.figure(figsize=(10, 6))
haplotype_frequencies.plot(kind='bar')
plt.title("Genetic Haplotype Frequencies")
plt.xlabel("Haplotype")
plt.ylabel("Frequency")
plt.xticks(rotation=90) 
plt.show()
plt.savefig('chart.png')
