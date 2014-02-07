SUMMARY

**AssembleIrys.pl -** Adjusts stretch by scan. Merges BNXs and initiate assemblies with a range of parameters.
    
USAGE
    
    perl AssembleIrys.pl -g [genome size in Mb] -r [reference CMAP] -b [directory with BNX files] -p [project name]
    
DEPENDENCIES

    Perl module Statistics::LineFit. This can be installed using CPAN http://search.cpan.org/dist/Statistics-LineFit/lib/Statistics/LineFit.pm.
    Perl module XML::Simple. This can be installed using CPAN http://search.cpan.org/~grantm/XML-Simple-2.20/lib/XML/Simple.pm;
    Perl module Data::Dumper. This can be installed using CPAN http://search.cpan.org/~smueller/Data-Dumper-2.145/Dumper.pm;

SCRIPT DETAILS

**AssembleIrys.pl -** a package of scripts that adjust the bases per pixel (bpp) by scan for each flowcell BNX file and then merge each flowcell into a single BNX file. Quality by flowcell is poltted in a CSV file "flowcell_summary.csv." Potential issues are reported in the output (e.g if the bpp does not return to ~500 after adjustment). The script creates optArgument.xml files and commands to run assemblies with strict, relaxed, and default p-value thresholds. The best of these along with the best p-value threshold (-T) should be used to run strict and relaxed assemblies with varing minimum lengths using the script "RefineAssembleIrys.pl."

USAGE

       perl script.pl [options]

        Documentation options:
          -help    brief help message
          -man     full documentation
        Required options:
           -b       directory with all BNX's meant for assembly (any BNX in this directory will be used in assembly)
           -g       genome size in Mb
           -r       reference CMAP
           -p       project name for all assemblies

OPTIONS

       -help   Print a brief help message and exits.

       -man    Prints the more detailed manual page with output details and
               exits.

       -b, --bnx_dir
               The directory with all BNX's meant for assembly (any BNX in
               this directory will be used in assembly. Do not use a trailing
               / for this directory.

       -g, --genome
               The estimated size of the genome in Mb.

       -r, --ref
               The full path to the reference genome CMAP.

       -p, --project
               The project id. This will be used to name all assemblies

OUTPUT DESCRIPTION

       strict_t - This directory holds the output for the strictest assembly
       (where the p-value threshold is divided by 10).

       relaxed_t - This directory holds the output for the laxest assembly
       (where the p-value threshold is multiplied by 10).

       default_t - This directory holds the output for the default assembly
       (where the p-value threshold is used as-is).

       bestref_effect_summary.csv - this shows the difference between running
       a molecule quality report with and without - BestRef. If the values
       change substantially than your p-value threshold may be too lax.

       assembly_commands.sh - These are the commands to start the first pass
       of assemblies. In these strict, relaxed, and default p-value thresholds
       will be used.

       flowcell_summary.csv - This file can be evaluated to check quality
       (ability to align to reference for each flowcell.

**Test with sample datasets:**

```
git clone https://github.com/i5K-KINBRE-script-share/Irys-scaffolding

# no test dataset is available yet but here is an example of a command

perl Irys-scaffolding/KSU_bioinfo_lab/assemble/AssembleIrys.pl -g  -b -r  -p Test_project_name > testing_log.txt

bash assembly_commands.sh
```
    
    
