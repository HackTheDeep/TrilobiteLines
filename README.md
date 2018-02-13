
American Museum of Natural History 'Hack the Deep' Hackathon
10-11 Feb-2018

Simple tool to experiment with 'ridge' detection along back of trilobite

1. read in image
2. convert to gray scale
3. apply some gamma correction (currently static value)
4. apply multiple adjacent line profiles along Y in center
5. average line profiles
6. look for trough (minima) peaks
7. draw output data onto lines in output image
8. write out output image
