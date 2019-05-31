---
title: Electron Microscopy in the Age of “Big Data”
separator: <!--s-->
verticalSeparator: <!--v-->
theme: nist.css
revealOptions:
  transition: 'slide'
  transitionSpeed: 'fast'
  controls: true
  math: {
    config: 'TeX-AMS_HTML-full'}
  slideNumber: 'c/t'
  center: false
  history: true	
	backgroundTransition: 'none'
---

<!-- .slide: data-state="title" -->

# Electron Microscopy in the Age of <br/> “*Big Data*”

&nbsp;

#### CCEM Summer School on Electron Microscopy <!-- .element: style="text-align: left;"-->

#### June 5, 2019 - Hamilton, ON <!-- .element: style="color: #a9a9a9; text-align: left;"-->

Joshua Taillon <!-- .element: class="author"-->

joshua.taillon@nist.gov <!-- .element: class="contact"-->

Note:

This talk could also be called "an introduction to computational microscopy"

<!--s-->

<!-- .slide: class="disclaimer" -->

## NIST Disclaimer

*Certain commercial equipment, instruments, materials, vendors, and software are
identified in this talk for example purposes and to foster understanding. Such
identification does not imply recommendation or endorsement by the National
Institute of Standards and Technology, nor does it imply that the materials or
equipment identified are necessarily the best available for the purpose.*

<!--s-->

## A Brief Introduction

- Materials scientist by training <!-- .element: class="fragment" data-fragment-index="1" -->

- Background in Materials characterization <!-- .element: class="fragment" data-fragment-index="2" -->
  - TEM, FIB/SEM, EDS/EELS, etc. <!-- .element: class="fragment" data-fragment-index="2" -->

- Stumbled into the world of "advanced" data analysis  <!-- .element: class="fragment" data-fragment-index="3" -->
  - Do not consider myself a software developer  <!-- .element: class="fragment" data-fragment-index="3" -->

- NIST Office of Data and Informatics <!-- .element: class="fragment" data-fragment-index="4" -->
  - <!-- .element: class="fragment" data-fragment-index="4" --> Not *actually* a microscopist any longer...

Note:

ODI contributes scientific value to research by providing guidance in best
practices and resources which optimize the discoverability, usability, and
interoperability of data products.  

ODI fosters collaboration and coordination among MML laboratory domain experts and other data specialists at NIST.

ODI supports development of research programs where advanced manipulation, visualization, and analysis of large data sets are needed to advance knowledge.

<!-- .slide: data-transition="none" -->
<!--v-->
<!-- .slide: data-transition="none" -->

## About NIST

<div class="two-cols">
<div class="col">
  <img width="480px" src="img/nist_gaithersburg.jpg"/>
  <div style="font-style: italic; color: #4a4a4a; font-size: x-large;">
    Gaithersburg, MD
  </div>
</div>
<div class="col">
  <img width="480px" src="img/nist_boulder.jpg"/>
  <div style="font-style: italic; color: #4a4a4a; font-size: x-large;">
    Boulder, CO
  </div>
</div>
</div>


<!-- .slide: data-transition="none" -->
<!--v-->
<!-- .slide: data-transition="none" -->

## Office of Data and Informatics
<!-- .slide: class="text_right_im_left" -->

![NIST ODI](img/nist_odi.png) <!-- .element: class="plain vertical-center" style="left:5%; width:30%" -->

<ul style="font-size:0.8em;">
  <li>Provides data expertise and resources to NIST researchers</li>
  <li>Develops best practices to optimize FAIR data products</li>
  <li>Supports research into advanced manipulation, visualization, and analysis of large data sets</li>
</ul>

<!--s-->

## High-level Outline

- <!-- .element: class="fragment" data-fragment-index="1" --> What is *computational microscopy*?

- <!-- .element: class="fragment" data-fragment-index="2" --> Real-world examples of "big data" analysis in EM

- The advent of open tools <!-- .element: class="fragment" data-fragment-index="3" -->
  - <!-- .element: class="fragment" data-fragment-index="3" --> *Now you can get the same result as your neighbor!*

- <!-- .element: class="fragment" data-fragment-index="4" --> Deeper dive into "signal separation"
  - <!-- .element: class="fragment" data-fragment-index="4" --> Methods, examples, *gotchas*, etc.

<!--s-->

<!-- .slide: class="section_header" data-background="#303c6b"-->
## What is *computational microscopy*?

<!--s-->

## What *is not* CM?

<!-- .slide: class="text_left_im_right" -->

- Digitization

![From film to CCD](img/digitization.svg) <!-- .element: class="plain vertical-center" -->
<div class="fig-caption" style="bottom: 25%">From film to CCD<br/>(Ted Pella; Gatan)</div>

<sticky>This is personal opinion! Feel free to disagree...</sticky><!-- .element: style="height:11.5%;" -->
<!-- .slide: data-transition="none" -->

<!--v-->
<!-- .slide: data-transition="none" -->

## What *is not* CM?

<!-- .slide: class="text_left_im_right" -->

- Digitization
- Image simulation

![Image simulation](img/image_simulation.png) <!-- .element: class="plain vertical-center" -->
<div class="fig-caption" style="bottom: 20%">EJ Kirkland; Multislice TEM Simulation</div>
<sticky>This is personal opinion! Feel free to disagree...</sticky><!-- .element: style="height:11.5%;" -->

<!--v-->
<!-- .slide: data-transition="none" -->

## What *is not* CM?
<!-- .slide: class="text_left_im_right" -->

- Digitization
- Image simulation
- "Traditional" image analysis

![Image simulation](img/hrtem_fourier.png) <!-- .element: class="plain vertical-center" style="background:none; top:40%; height:73%; right:4%;" -->
<div class="fig-caption" style="width:49%; bottom: 14%">HRTEM Fourier analysis</div>
<sticky>This is personal opinion! Feel free to disagree...</sticky><!-- .element: style="height:11.5%;" -->

<!--s-->

## Attempting a definition

*Microscopy directed by or collected primarily for computational processes
(as opposed to by/for the user directly)*

<sticky>This is personal opinion! Feel free to disagree...</sticky> <!-- .element: style="height:11.5%;" -->

<!-- .slide: data-transition="none" -->
<!--v-->
<!-- .slide: data-transition="none" -->

## Attempting a definition

<sticky>This is personal opinion! Feel free to disagree...</sticky> <!-- .element: style="height:11.5%;" -->
<!-- .slide: class="two-columns" -->

- Relevant buzzwords:

<div class="two-cols">
  <div class="col">
    <ul>  
      <ul>
        <li>Machine learning</li>
        <li>Artificial intelligence</li>
        <li>Autonomous measurement</li>
      </ul>
    </ul>
  </div>

  <div class="col">
    <ul>  
      <ul>
        <li>Dynamic sampling</li>
        <li>Compressive sensing</li>
        <li>Sparse imaging</li>
      </ul>
    </ul>
  </div>
</div>
<!--s-->

## Why computational microscopy?

- Statistical power <!-- .element: class="fragment" data-fragment-index="1" -->
  - Is your image actually *representative*? <!-- .element: class="fragment" data-fragment-index="1" -->
- Reproducibility is the default <!-- .element: class="fragment" data-fragment-index="2" -->
  - Computers only do what you tell them too (*we hope*) <!-- .element: class="fragment" data-fragment-index="2" -->
- Leverages massive advances in computational power <!-- .element: class="fragment" data-fragment-index="3" -->

<!--s-->

<!-- .slide: class="section_header" data-background="#303c6b"-->
## Some real-world examples of computational microscopy and "big data"

<!--s-->

## (1/5) Electron Tomography

<!-- .slide: class="text_left_im_right tight_list" -->

<ul style="bottom: 25%; position: absolute;">
<li style="color: #729fcf;">Y. Yang, J. Miao, *et al.*, *Nature*, **542**, 75-79, 2017 ([link](https://doi.org/10.1038/nature21042))</li> <br>

<li>68 ADF-STEM images of FePt nanoparticle</li>
<li>Located 6,569 Fe and 16,627 Pt atoms to 21.6 pm precision (correlated with multislice simulations)</li>
<li>Calculated SROP to distinguish individual grains</li>
<li>3D information at the atomic scale</li>
</ul>

![Tomography tilt series](img/yang_nature_tomo1_crop.png) <!-- .element: class="plain" style="max-width:35%; bottom:27%" -->
<div class="fig-caption" style="width:49%; bottom: 22%">Selection of nanoparticle tilt images</div>

<!-- .slide: data-transition="none" -->
<!--v-->
<!-- .slide: data-transition="none" -->

## (1/5) Electron Tomography

<video  class="center"
		style="width:65%;"
        data-autoplay
        src="vid/yang_nature_tomo.mp4"
        controls
        loop>
</video>

<!--s-->

## (2/5) ML for Factor Analysis

<!-- .slide: class="text_left_im_right tight_list" -->

<ul style="bottom: 25%; position: absolute;">
<li style="color: #729fcf;">O. Nicoletti, P. Midgley, *et al.*, *Nature*, **502**, 80-84, 2013 ([link](https://doi.org/10.1038/nature12469))</li> <br>
<li>Non-negative matrix factorization of EELS spectra</li>
<li>Identifying meaningful spectral components in a sea of overlapping signals</li>
<li>Combine with tilt-tomography for 3D information</li>
<li>Identified nanoparticle plasmon resonances</li>
</ul>

![Nicoletti fig1](img/nicoletti1.svg) <!-- .element: class="plain" style="max-width:50%; bottom:26%" -->

<!-- .slide: data-transition="none" -->
<!--v-->
<!-- .slide: data-transition="none" -->

## (2/5) ML for Factor Analysis

<!-- .slide: class="text_left_im_right tight_list" -->

<ul style="bottom: 25%; position: absolute;">
<li style="color: #729fcf;">O. Nicoletti, P. Midgley, *et al.*, *Nature*, **502**, 80-84, 2013 ([link](https://doi.org/10.1038/nature12469))</li> <br>
<li>Non-negative matrix factorization of EELS spectra</li>
<li>Identifying meaningful spectral components in a sea of overlapping signals</li>
<li>Combine with tilt-tomography for 3D information</li>
<li>Identified nanoparticle plasmon resonances</li>
</ul>

<video  style="width: 500px; bottom:30%"
        data-autoplay
        src="vid/nicoletti_nature_video.mp4"
        controls
        loop>
</video>

<!--s-->

## (3/5) Autonomous Metrology

<!-- .slide: class="text_left_im_right tight_list" -->

<ul style="bottom: 25%; position: absolute; font-size:0.8em; max-width:35%">
<li style="color: #729fcf;">A. Kusne, I. Takeuchi, *et al.*, *Nanotechnology*, **26**, 444002, 2015 ([link](https://doi.org/10.1088/0957-4484/26/44/444002))</li> <br>
<li>High-throughput XRD for combinatorial materials discovery</li>
<li>Autonomous phase diagram mapping of composition spread wafer</li>
<li>Phase diagram is estimated at each step based on collected data and physics-informed ML algorithms</li>
<li>Unsupervised AI determines new composition to measure to best estimate phase diagram</li>
</ul>

<video  style="width:65% ; bottom:30%; max-width:100% !important; right:-5px"
        data-autoplay
        src="vid/akusne.mp4"
        controls
        loop>
</video>

<!--s-->

## (4/5) Dynamic Sampling in SEM

<!-- .slide: class="text_left_im_right tight_list" -->

<ul style="bottom: 25%; position: absolute; font-size:0.8em; max-width:35%">
<li style="color: #729fcf;">G. Godaliyadda, C. Bouman, *et al.*,
*Electronic Imaging*, **19**, 1-8, 2016 ([link](https://engineering.purdue.edu/~bouman/software/SLADS/))</li> <br>
<li>Supervised Learning Approach to Dynamic Sampling (SLADS)</li>
<li>Sparse imaging and weighted inpainting reconstruction</li>
<li>Train algorithm offline to measure how much certain types of pixels reduce overall distortion</li>
<li>Online, pick new pixels to reduce expected distortion in reconstruction</li>
</ul>

![SLADS for EBSD](img/SLADS_EBSD.png) <!-- .element: class="plain vertical-center" style="max-width:100% !important; width:65%; right:-5%; top:45%;" -->
<div class="fig-caption" style="width:49%; bottom: 22%">Simulated EBSD patterns</div>

Note:

LS is low-discrepancy sequencing (grid + random jitter)

<!-- .slide: data-transition="none" -->
<!--v-->
<!-- .slide: data-transition="none" -->

## (4/5) Dynamic Sampling in SEM

<!-- .slide: class="text_left_im_right tight_list" -->

<ul style="bottom: 25%; position: absolute; font-size:0.8em; max-width:35%">
<li style="color: #729fcf;">G. Godaliyadda, C. Bouman, *et al.*,
*Electronic Imaging*, **19**, 1-8, 2016 ([link](https://engineering.purdue.edu/~bouman/software/SLADS/))</li> <br>
<li>Supervised Learning Approach to Dynamic Sampling (SLADS)</li>
<li>Sparse imaging and weighted inpainting reconstruction</li>
<li>Train algorithm offline to measure how much certain types of pixels reduce overall distortion</li>
<li>Online, pick new pixels to reduce expected distortion in reconstruction</li>
</ul>

![SLADS on experimental image](img/SLADS.png) <!-- .element: class="plain vertical-center" style="max-width:100% !important; width:65%; right:-5%; top:45%;" -->
<div class="fig-caption" style="width:49%; bottom: 22%">Experimental SEM images</div>

<!--s-->

## (5/5) STEM CS

<!-- .slide: class="text_left_im_right tight_list" -->

<ul style="bottom: 25%; position: absolute; font-size:0.9em; max-width:35%">
<li style="color: #729fcf;">A. Stevens, N. Browning, *et al.*,
*Microscopy*, **63**, 41-51, 2014. ([link](https://doi.org/10.1093/jmicro/dft042))</li> <br>
<li>Intentionally acquire image at severe undersampling conditions</li>
<li>Use $\ell_1$-norm convex optimization to fill in the missing details</li>
<li>An interesting means to get around the Nyquist-Shannon limit</li>
<li>Demonstrated with random sampling in both STEM and SEM</li>
</ul>

![CS reconstruction in STEM](img/stevens_CS.svg) <!-- .element: class="plain vertical-center" style="max-width:100% !important; width:55%; right:-5%; top:40%;" -->
<div class="fig-caption" style="width:55%; bottom: 15%">Compressed Sensing STEM reconstructions</div>

<!--s-->

<!-- .slide: class="section_header" data-background="#303c6b"-->
## Open tools for electron microscopy

<!--s-->

## Acknowledgments

- Collaborators:
  - Lourdes Salamanca-Riba - UMD
  - Leonard Feldman - Rutgers

<!--s-->

# Thank you! <!-- .element: style="text-align: center;" -->

Joshua Taillon

<a href="mailto:joshua.taillon@nist.gov">joshua.taillon@nist.gov</a>

<!--s-->

## References
<!-- .slide: class="reference" -->
