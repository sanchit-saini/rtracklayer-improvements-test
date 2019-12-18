# rtracklayer-improvements-test

## Solutions


- ### Identify some of the functions in the [Kent library](https://github.com/ucscGenomeBrowser/kent/tree/master/src/lib) that would need to be called to read and write BigBed files.

    | Function |task       | Return  |
    | ------------- |:-------------:| -----:|
    | [bigBedFileOpen](https://github.com/ucscGenomeBrowser/kent/blob/981a56e061a1e3e9a54904f09eb17832151d20be/src/lib/bigBed.c#L23)|Open bigBed/bigWig File|struct bbiFile*|
    |[bigBedIntervalQuery](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/bigBed.c#L35)|Get data for interval|struct bigBedInterval*|
    |[bbiChromList](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/bbiRead.c#L219)|Return list of chromosomes|struct bbiChromInfo*|
    |[mustOpen](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/common.c#L2587)|Open a file or squawk and die|FILE*|
    |[repeatCharOut](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/common.c#L2347)|Write character to file repeatedly|void|
    |[mustWrite](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/common.c#L2613)|Write to a file or squawk and die|void|
    |[bbiWriteDummyHeader](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/bbiWrite.c#L18)|Write out all-zero header, just to reserve space for it|void|
    |[bbiWriteDummyZooms](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/bbiWrite.c#L24)|Write out zeroes to reserve space for ten zoom levels|void|
    |[bbiSummaryElementWrite](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/bbiWrite.c#L30)|Write out summary element to file|void|
    |[bbiWriteChromInfo](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/bbiWrite.c#L50)|Write out information on chromosomes to file|void|
    |[bbiWriteZoomLevels](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/lib/bbiWrite.c#L283)|Write out all the zoom levels and return the number of levels written|int|
    |[bigBedFileClose](https://github.com/ucscGenomeBrowser/kent/blob/0ca4edff9bd7aefe16d3af95d137f61576539929/src/inc/bigBed.h#L62)|Close down a big wig/big bed file|void|




- ### Use the restfulr package to retrieve the list of available UCSC genomes from their REST API.
    ```R
    # Checking requirements are installed if not, then install the required packages
    if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

    if(!require(S4Vectors))
    BiocManager::install("S4Vectors")
    
    if(!require(restfulr))
    install.packages("restfulr")
    
    # Solution: Fetch list of available UCSC genomes 
    library(restfulr)
    genome <- RestUri("http://api.genome.ucsc.edu/list")
    response <- read(genome$ucscGenomes)
    print(response)
    ```
