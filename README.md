## validate.py
This Python module includes features to be implemented in future [Olivar](https://github.com/treangenlab/Olivar) updates. It can visualize a Multiple Sequence Alignment (MSA) along with attached primers/probes, and validate their alignment and sensitivity. Ambiguous bases are supported. 
![](Figure.png)

## Dependencies
```
python >=3.8
biopython >=1.8
numpy
plotly >=5
tqdm
```

## Installation
1. Install Miniconda if not installed already ([quick command line install](https://docs.conda.io/projects/miniconda/en/latest/#quick-command-line-install))

2. Create a Conda environment called "myenv" and install required packages
```bash
conda create -n myenv biopython plotly tqdm --channel conda-forge
```
3. Add `validate.py` to your PATH, or copy it to your working directory. 

4. Run `validate.py -h` if added to PATH, or `./validate.py -h` if copied to your working directory. 

## Usage
Using example input files
```bash
./validate.py example/H1N1-2024-04-25-HA-MSA.fasta --oligos example/primers.csv
```
Outputs are `example/primers.csv.html` and `example/primers.csv.out`. For more details, run `./validate.py -h`

### Features to be added to `olivar validate`
1. Input unaligned sequences in FASTA format, and output an MSA with MAFFT. Ideally, we want to automatically detect if a file is aligned or not. **[PENDING]**
```python
with open('MSA.fasta', 'w') as mafft_out:
    cmd_out = run_cmd('mafft', '--auto', '--thread', str(n_cpu), 'sequences.fasta')
    mafft_out.write(cmd_out.stdout)
```
2. Input an MSA file (or use the file generated in step 1), and a list of primers (names and sequences, in CSV format)
   - a. output validation info for each primer (GC, dG, alignment, sensitivity, etc.). **[DONE]**
   - b. plot the MSA along with the primers, and save the plot as HTML using Plotly. **[DONE]**

### Features to be added to `olivar build`
1. Same as `olivar validate` step 1. 
2. Input an MSA file (or use the file generated in step 1), and output location and frequencies of variations using the consensus sequence as reference. **[DONE]**
