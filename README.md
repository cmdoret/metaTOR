# metaTOR

[![License: Artistic-2.0](https://img.shields.io/badge/License-GPL%203-0298c3.svg)](https://opensource.org/licenses/GPL-3.0)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/ambv/black)

Metagenomic Tridimensional Organisation-based Reassembly - A set of scripts that streamlines the processing and binning of metagenomic 3C datasets.

## Usage

    metator {align|partition|annotation|binning} [parameters]

A metaTOR command takes the form ```metator action --param1 arg1 --param2
arg2 #etc.```

There are four actions or steps in the meta3c pipeline. They must be run in this order:

* ```align``` : map paired-end reads on a preliminary assembly, then generate a network from
 detected contacts between DNA chunks.
* ```partition``` : perform the Louvain community detection algorithm many times to isolate
     chunks that consistently cluster together for binning purposes.
* ```annotation``` : run standard annotation software on the assembly (namely gene prediction
      and database comparison) to match with the bins
* ```binning``` : match annotations to bins, extract bin genomes and subnetworks, build bin-local
   and global contact maps

After the last step is completed, you should have at your disposal a set of bins, their relative
enrichments in various gene categories as well as the contact map of each bin.

In addition, there are a number of optional, miscellaneous actions:

* ```pipeline``` : check the environment is right, then run all four of the above sequentially.
    This can take a while.
* ```dependencies``` : download some third party dependencies (```louvain``` and HMM databases)
* ```deploy``` : set up the environment and dependencies (currently only Ubuntu
  14.04 and higher are supported)
* ```version``` : display current version number
* ```help``` : display this (hopefully useful) help message

Please refer to the [metaTOR manual](https://github.com/koszullab/metaTOR/meta3c_manual.pdf) for detailed explanations on the parameters.

## Installation

```sh
   sudo pip3 install -e git+https://github.com/koszullab/metator.git@master#egg=metator
```

## Requirements

* Python with ```numpy```, ```scipy```, ```matplotlib```, ```biopython``` and ```pysam``` libraries
* [bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)
* [samtools](http://www.htslib.org/)
* [hmmer](http://hmmer.org/) and some HMM databases (such as [these](http://dl.pasteur.fr/fop/5eHgTGww/modele_HMM.tar.gz))
* [prodigal](https://github.com/hyattpd/Prodigal)
* [louvain](https://sourceforge.net/projects/louvain/) (original implementation)

Most of these can usually be installed with your OS's package manager. The Python libraries can be installed with the ```requirements.txt``` file:

```sh
    pip install -Ur requirements.txt
```

A dockerfile is also available if you are into that sort of thing.

## References

* [Metagenomic chromosome conformation capture (meta3C) unveils the diversity of chromosome organization in microorganisms](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4381813/), Martial Marbouty, Axel Cournac, Jean-François Flot, Hervé Marie-Nelly, Julien Mozziconacci, and Romain Koszul, eLife, 2014
* [Scaffolding bacterial genomes and probing host-virus interactions in gut microbiome by proximity ligation (chromosome capture) assay](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5315449/), Martial Marbouty, Lyam Baudry, Axel Cournac, and Romain Koszul, Science Advances, 2017

## Contact

### Authors

* lyam.baudry@pasteur.fr
* thfoutel@pasteur.fr
* martial.marbouty@pasteur.fr
* romain.koszul@pasteur.fr

### Research lab

[Spatial Regulation of Genomes](https://research.pasteur.fr/en/team/spatial-regulation-of-genomes/) (Institut Pasteur, Paris)