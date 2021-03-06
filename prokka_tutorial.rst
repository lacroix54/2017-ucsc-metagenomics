======================
Annotation with Prokka
======================

Prokka is a tool that facilitates the fast annotation of prokaryotic genomes.

The goals of this tutorial are to:

*  Install Prokka
*  Use Prokka to annotate our genomes

Installing Prokka
=================

Download and extract the latest version of prokka:
::
   
    cd ~/
    wget http://www.vicbioinformatics.com/prokka-1.11.tar.gz
    tar -xvzf prokka-1.11.tar.gz

We also will need some dependencies such as bioperl:
::
   
    sudo apt-get -y install bioperl libdatetime-perl libxml-simple-perl libdigest-md5-perl

and we need an XML package from perl
::

    sudo bash
    export PERL_MM_USE_DEFAULT=1
    export PERL_EXTUTILS_AUTOINSTALL="--defaultdeps"
    perl -MCPAN -e 'install "XML::Simple"'
    exit

Now, you should be able to add Prokka to your ``$PATH`` and set up the index for the sequence database:
::
   
    export PATH=$PATH:$HOME/prokka-1.11/bin
    prokka --setupdb

Prokka should be good to go now-- you can check to make sure that all is well by typing ``prokka``. This should print the help screen with all available options. You can find out more about Prokka databases `here <https://github.com/tseemann/prokka#Databases>`__.

Running Prokka
==============

Make a new directory for the annotation:
::
   
    cd ~/
    mkdir annotation
    cd annotation

Link the metagenome assembly file into this directory:
::

    ln -fs ~/mapping/subset_assembly.fa .

Now it is time to run Prokka! There are tons of different ways to specialize the running of Prokka. We are going to keep it simple for now, though. It will take a little bit to run.
::

    prokka subset_assembly.fa --outdir prokka_annotation --prefix metagG --metagenome

This will generate a new folder called ``prokka_annotation`` in which will be a series of files, which are detailed `here <https://github.com/tseemann/prokka/blob/master/README.md#output-files>`__.

In particular, we will be using the ``*.ffn`` file to assess the relative read coverage within our metagenomes across the predicted genomic regions.

Questions? 
=========

* What can I annotate with prokka?
* Alternatives?
* How do I submit my annotated files to `Genbank? EBI? <https://github.com/tseemann/prokka/blob/master/README.md#NCBI Genbank submitter>`__?
* Why is it called Prokka?


References
===========

* http://www.vicbioinformatics.com/software.prokka.shtml
* https://www.ncbi.nlm.nih.gov/pubmed/24642063
* https://github.com/tseemann/prokka/blob/master/README.md
