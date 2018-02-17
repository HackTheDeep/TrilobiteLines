
### American Museum of Natural History 'Hack the Deep' Hackathon
## 10-11 Feb-2018

# Simple tool to experiment with 'ridge' detection along back of trilobite

1) read in image
2) convert to grayscale
3) apply some gamma correction (currently static value)
4) apply multiple adjacent line profiles along Y in center
5) average line profiles
6) look for trough (minima) peaks
7) draw output data onto lines in output image
8) write out output image

The challenge suggested we used ImageJ; we actually just used imageJ to sample and test some very simple processing of images, then used some of those ideas via OpenCV, Numpy, et al inside of a python script. The general idea is: given a symmetrical trilobite image with long axis parallel and coincident with sampling axis, a 'strip sampled' profile along either side of the axis will give a (looking for) per segment (summed in dX) signal that will be noisy. Averaging the signal will give a cleaned, varying in dY sample of dark/light signal along this strip. Segments tend to be darker, so looking for lowest peaks will give initial rough set of 'crossings' constituting the candidates for segments. Finally, some dumb stats and cleaning up yields a set of candidate segments, and a count.

Obviously, this assumes a lot of stupid things, like, the trilobite is positioned up/down, long axis, centered on image. But /if/ the sampling approach generally correlates with the segments, then simply varying the affine of the image or the sampling axis should yield constant results. So this helps decouple the problem into two pieces: localization and detection. We kick the localization can down the road (given 24 hour constraint) and test the concept on a bunch of images that are PRETTY CLOSE to trilobite in center of page, up down, etc. And, it generally works (kind of) in these cases.

Again, in a perfect world, we could do two things. We could: do some localization and/or normalization of image (detection, localization, extract affine for translations, rotations, etc) then run sampling OR from a workflow perspective, let the operator queue up a bunch of images, let a human do the sampling strip placement, and run the sampler. Again, this decouples the parts of the problem in such a way that multiple and potentially synergistic solutions are possible.

The JSON output from the code is kind of what we discussed we'd want. It's the useful entropy coming back from the code, but we can add in whatever we want. The input image, the output image, the dimensions of the image, a vector of candidate offsets in Y for segments, a result string/descriptor (completion/result state of code run). It was never used by a 'consumer' process, but is in place so that a consumer (such as a web server) could invoke the code, get an easy result vector, then make use of it.
