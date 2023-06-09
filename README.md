# deepG predictions

These are Python script that runs containerized versions of the deepG for prediction.

## Installation

1. Clone this repository to your local machine.

2. Navigate to the cloned repository in a terminal window.

3. Run the installation script to install the necessary dependencies. Run the following command:

```
./install.py
```

This script will install the following dependencies:

* argparse
* pathlib2

It will also check if Podman is installed and install it if it is not present.

4. (Optional) Run the following command to check if Podman is installed:

```
podman --version
```

If Podman is installed, the command will return the version number. If it is not installed, the command will return an error.

## sORF models

1. Navigate to the cloned repository in a terminal window.

2. Pull the image

```
podman pull docker.io/genomenet/sorf
```

3. Run the Python script using the following command:

```
./sorf.py --input example.fasta --output sorf_prediction --batch_size 5000
```

An example output is in the `sorf_prediction` folder 

**Note:** Replace `example.fasta` with the path to your input file. The script will run the sorf tool on your input file and save the output files in the specified output directory. If you don't specify an output directory, it will create a folder like deepG_sorf_20230329_1 with the current date. 

## Virus models

1. Navigate to the cloned repository in a terminal window.

2. Pull the image

```
podman pull docker.io/genomenet/virus
```

3. Run the Python script using the following command:

```
./virus.py --input example.fasta --output virus_prediction_genus --batch_size 5000 --level genus
```

and to output one prediction per FASTA entry (will evaluate all subsamples per entry)

```
./virus.py --input example.fasta --output virus_prediction_genus_by_entry --batch_size 5000 --level binary --by_entry
```

and to output one prediction per FASTA entry (fast mode, only one sample per entry)

```
./virus.py --input example.fasta --output virus_prediction_genus_by_entry_fast --batch_size 5000 --level binary --by_entry --fast
```

and for the binary level

```
./virus.py --input example.fasta --output virus_prediction_binary --batch_size 5000 --level binary
```

for the binary level, it is possible to output the mean prediction per FASTA entry. This will evaluate all subsamples per entry.

```
./virus.py --input example.fasta --output virus_prediction_binary --batch_size 5000 --level binary --by_entry
```

With the `--fast` parameter, only one subsample per entry will be evaluated
```
./virus.py --input example.fasta --output virus_prediction_binary_fast --batch_size 5000 --level binary --by_entry --fast
```


Here are the options you can use with the `virus.py` script:

* `--input` (**required**): Path to the input file.
* `--output` (**optional**): Path to the output directory (default: `deepG_virus_<date>_1`, where `<date>` is the current date in the format `YYYYMMDD`).
* `--gpu` (**optional**): Use GPU mode (untested).
* `--batch_size` (**optional**): Batch size for processing (default: `3000`).
* `--level` (**optional**): Prediction level (`binary` or `genus`; default: `binary`).
* `--verbose` (**optional**): Enable verbose mode for more information during execution.

3. Wait for the script to finish running. The output files will be saved in the specified output directory.
