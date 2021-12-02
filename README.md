# Spike train datasets

### Introduction
The folder named Datasets contains 28 datasets of spike train activity recorded in areas V1 and V2 of anesthetized macaque monkey. The data files are MATLAB .mat files and are described below, in sections titled The Experiment, The Data Files and List of the Datasets.

The folder named Selection contains 28 data files containing a selection of the data, which is the starting point of the analysis in the manuscript  
A Guidolin, M Desroches, JD Victor, K Purpura, & S Rodrigues (2021) *Geometry of spiking activity in early visual cortex: a Topological Data Analytic approach.*  
The data files containing the selected data are described in last section of this document, Selection of Data.


### The Experiment
The BTC experiments that will be studied here present a series of “binary textures” (i.e., images consisting of an array of 16x16 black or white checks) at locations in visual space that extend over the receptive fields of several isolated single-units in the anesthetized monkey visual cortex (areas V1 and V2). The textures are drawn from a high-dimensional stimulus space that is described in detail in several publications including JD Victor, DJ Thengone, SM Rizvi, & MM Conte (2015) *A perceptual space of local image statistics.* Vision Research, 117, 117-135. The experimental runs use texture samples drawn from this space from particular coordinates along the 10 cardinal axes in the space (here labelled G, B, C, D, E, T, U, V, W, and A, see below). Each of these 10 axes has a characteristic spatial correlation structure defined on 2x2 neighborhoods of checks. Coordinates along the axes correspond to the ‘strength’ of the rendering of these characteristic local multipoint spatial correlations. The sign of the spatial correlation can be positive or negative, therefore the coordinates on each axis run from +1 to -1 (both fully correlated); a value of 0 corresponds to no correlation.  Thus, the origin of the space (0 on all axes) corresponds to textures without spatial correlation, in which each check is randomly and independently assigned to black or white, with probability 0.5. We refer to these images as Random textures. 
Details of the neurophysiological recordings and the animal preparation can be found in Y Yu, AM Schmid, & JD Victor (2015) *Visual processing of informative multipoint correlations arises primarily in V2.* eLife; 10:7554/eLife.06604.  

In the data files, the 10 axes in the stimulus space are designated with a letter for each ‘class’ of textures (each axis in the stimulus space):  
G: gamma, 	single-point correlation (i.e., the bias of white vs black checks)   
B: beta --, 	two-point correlation, horizontal    
C: beta |, 	 two-point correlation, vertical  
D: beta \,	 two-point correlation, diagonal 1  
E: beta /,	 two-point correlation, diagonal 2  
T: theta ┘,	 three-point correlation 1  
U: theta└,	 three-point correlation 2  
V: theta┌,	 three-point correlation 3  
W: theta ┐,	 three-point correlation 4  
A: alpha,	  four-point correlation  

We add ‘R’ to denote an additional stimulus ‘class’, the random textures.   
For each stimulus class (except R), two strengths of correlation, for both ‘+’ and ‘-‘ spatial correlations, were tested. The smaller the correlation strength the more de-correlated the texture.  

| Class       | Strengths (-)          | Strengths (+)  |
| ------------- |:-------------:| -----:|
| G     | -0.4 -0.2  | 0.2 0.4 |
| B, C, D, E, T, U, V, W, A    | -0.8 -0.4      | 	0.4 0.8   |

(The reason that we used a lower strength for G than the other axes is that G is perceptually more salient than the others.) Thus, textures from 41 coordinates in the stimulus space were used in these experiments: 4 for G, 4 for each of B, C, D, E, T, U, V, W, A, and 1 for the origin, R; there are 41 coordinate values:  4 on each of the 10 axes, and one at the origin.

64 examples of textures representing each of these 41 coordinate values were shown in an experimental run. Since there are 41 coordinate values, there are 41 * 64=2624 unique stimuli.
  Each of these stimuli were shown for 4 repeats. So, the total count of stimulus presentations for each experiment is as follows:
(41 coordinate values * 64 examples) * 4 repeats = 10496. 
Each of these 2624 textures was presented for 320 ms, in a sequence without interruption, in a random order.  There was a brief pause between the 4 repeat cycles.  Repeats used the same 2624 unique stimuli, but in a different random order.
 A typical BTC experimental run took about 1 hour to complete (10496 * 320 ms=approx. 3358 sec).  
 
 Note: in the datasets whose name starts with ‘L73’ or ‘L76’, the number of examples of textures for each of the 41 coordinate values is 128 instead of 64. In these cases, the number of spike trains responses is the double of what we described in the previous paragraph. In the description of the data below we consider as a reference a dataset with 64 textures for each of the 41 coordinate values.
 
### The Data Files

Example data file: L8501_TT4_btc_SPKTs.mat.

The name of the file includes the animal id (L85), the recording session/sites (01), and the tetrode number (TT4). The spike times in the file are from the single-units that were recorded from TT4. The recording session/site represents an experimental run through the stimulus space described above with from 4 to 6 tetrodes positioned at various depths and retinotopic locations across V1 and V2. 

The animal id, session number, and tetrode numbers also provide the information necessary for querying the histology database to determine the likely anatomical location of a single or multiunit recording, in terms of cortical area (V1/V2) and depth (supragranular, granular, and infragranular) within the cortex, and we will describe that separately with the full database.
 
A ‘single unit’ or ‘multiunit’ are the spike times included in a distinct cluster of spike waveshapes extracted from the neural activity recorded from a single tetrode by spike-sorting software (which includes a K-means clustering step). A multiunit cluster is a collection of waveshapes that could not be further segregated into independent clusters yet are distinct from the other isolated single units in a tetrode recording. Multiunit clusters represent local population activity in the neighborhood of the tetrode.

Load the data files in MATLAB:

```dash
>>load(‘L8501_TT4_btc_SPKTs.mat’);
>>who
```

Your variables are:

```dash
>> SPKTs

SPKTs = 

  struct with fields:

    EXPV: [1×1 struct]
       R: [1×4 struct]
       G: [1×4 struct]
       B: [1×4 struct]
       C: [1×4 struct]
       D: [1×4 struct]
       E: [1×4 struct]
       T: [1×4 struct]
       U: [1×4 struct]
       V: [1×4 struct]
       W: [1×4 struct]
       A: [1×4 struct]
```

There are twelve structures now in the workspace. EXPV contains information about the recording session and the stimuli used. R, G, B, C, D, E, T, U, V, W, A are structured arrays that contain the spike time data for each repetition cycle through the texture sequence and additional information about the texture stimuli.  For example, SPKTs.R{1} contains the data generated by the random class and the maps for those stimuli that are used in the first cycle. T{3} contains the data generated by the T class of textures in the third repeat cycle. 

```dash
>> SPKTs.EXPV

ans = 

  struct with fields:

         Clusters: {'m1'  '2'  '3'  '4'  '5'  '6'}      : clusters of spiking activity (units) available for analysis
                                                                    m1 signifies a multiunit cluster.			
           animid: 'L85'				
           oglsuf: 'btc'
           cheeid: '01'                        : session, experimental run
          tetrode: 'TT4'
          oglname: 'L8501_btc'
         savename: 'L8501_TT4_btc_SPKTs' : name of this mat file
           NExper: 1                          : number of times the sequence is shown in the session
         Nrepeats: 4                         : number of repeats of each texture example in session
     presentOrder: 'Randomized'
          xCenter: 160                      : horiz.. position of the center of texture patch in pixels 
          yCenter: 0                          : vertical position of the center of texture patch
           radius: 0.1250
           orient: 45                           : orientation of the texture patch
              dom: 100                        : contrast (depth of modulation) of the textures
         pixWidth: 1280                    : display screen width (in pixels)
        pixHeight: 1024                    : display screen height (in pixels)
           pixDeg: 68.0300                : number of pixels in a degree of visual angle
          cm2eyes: 114                     : distance of the display from the animal’s eye
          mapSize: 64 				  
          mapStdv: 4
         sequence: [10496×1 double]: the sequence in which the stimuli are shown
    coordSequence: {2624×8 cell}: the organization of the texture stimuli for the BTC 		
                                                      experiments. The master memory list of textures.
```

There are 2624 unique stimuli in the experimental run. Each has a position in the master list. For example, the first 41 entries in the list are as follows:

```dash
>> SPKTs.EXPV.coordSequence(1:41,:)

ans =

  41×8 cell array

    {[ 1]}    {4×1 double}    {[ 0]}    {[0]}    {[ 1]}    {[1]}    {'g'}    {[      0]}
    {[ 2]}    {4×1 double}    {[ 1]}    {[0]}    {[ 2]}    {[1]}    {'g'}    {[ 0.2000]}
    {[ 3]}    {4×1 double}    {[ 2]}    {[0]}    {[ 3]}    {[1]}    {'g'}    {[ 0.4000]}
    {[ 4]}    {4×1 double}    {[ 3]}    {[0]}    {[ 4]}    {[1]}    {'g'}    {[-0.2000]}
    {[ 5]}    {4×1 double}    {[ 4]}    {[0]}    {[ 5]}    {[1]}    {'g'}    {[-0.4000]}
    {[ 6]}    {4×1 double}    {[ 5]}    {[0]}    {[ 6]}    {[1]}    {'b'}    {[ 0.4000]}
    {[ 7]}    {4×1 double}    {[ 6]}    {[0]}    {[ 7]}    {[1]}    {'b'}    {[ 0.8000]}
    {[ 8]}    {4×1 double}    {[ 7]}    {[0]}    {[ 8]}    {[1]}    {'b'}    {[-0.4000]}
    {[ 9]}    {4×1 double}    {[ 8]}    {[0]}    {[ 9]}    {[1]}    {'b'}    {[-0.8000]}
    {[10]}    {4×1 double}    {[ 9]}    {[0]}    {[10]}    {[1]}    {'c'}    {[ 0.4000]}
    {[11]}    {4×1 double}    {[10]}    {[0]}    {[11]}    {[1]}    {'c'}    {[ 0.8000]}
    {[12]}    {4×1 double}    {[11]}    {[0]}    {[12]}    {[1]}    {'c'}    {[-0.4000]}
    {[13]}    {4×1 double}    {[12]}    {[0]}    {[13]}    {[1]}    {'c'}    {[-0.8000]}
    {[14]}    {4×1 double}    {[13]}    {[0]}    {[14]}    {[1]}    {'d'}    {[ 0.4000]}
    {[15]}    {4×1 double}    {[14]}    {[0]}    {[15]}    {[1]}    {'d'}    {[ 0.8000]}
    {[16]}    {4×1 double}    {[15]}    {[0]}    {[16]}    {[1]}    {'d'}    {[-0.4000]}
    {[17]}    {4×1 double}    {[16]}    {[0]}    {[17]}    {[1]}    {'d'}    {[-0.8000]}
    {[18]}    {4×1 double}    {[17]}    {[0]}    {[18]}    {[1]}    {'e'}    {[ 0.4000]}
    {[19]}    {4×1 double}    {[18]}    {[0]}    {[19]}    {[1]}    {'e'}    {[ 0.8000]}
    {[20]}    {4×1 double}    {[19]}    {[0]}    {[20]}    {[1]}    {'e'}    {[-0.4000]}
    {[21]}    {4×1 double}    {[20]}    {[0]}    {[21]}    {[1]}    {'e'}    {[-0.8000]}
    {[22]}    {4×1 double}    {[21]}    {[0]}    {[22]}    {[1]}    {'t'}    {[ 0.4000]}
    {[23]}    {4×1 double}    {[22]}    {[0]}    {[23]}    {[1]}    {'t'}    {[ 0.8000]}
    {[24]}    {4×1 double}    {[23]}    {[0]}    {[24]}    {[1]}    {'t'}    {[-0.4000]}
    {[25]}    {4×1 double}    {[24]}    {[0]}    {[25]}    {[1]}    {'t'}    {[-0.8000]}
    {[26]}    {4×1 double}    {[25]}    {[0]}    {[26]}    {[1]}    {'u'}    {[ 0.4000]}
    {[27]}    {4×1 double}    {[26]}    {[0]}    {[27]}    {[1]}    {'u'}    {[ 0.8000]}
    {[28]}    {4×1 double}    {[27]}    {[0]}    {[28]}    {[1]}    {'u'}    {[-0.4000]}
    {[29]}    {4×1 double}    {[28]}    {[0]}    {[29]}    {[1]}    {'u'}    {[-0.8000]}
    {[30]}    {4×1 double}    {[29]}    {[0]}    {[30]}    {[1]}    {'v'}    {[ 0.4000]}
    {[31]}    {4×1 double}    {[30]}    {[0]}    {[31]}    {[1]}    {'v'}    {[ 0.8000]}
    {[32]}    {4×1 double}    {[31]}    {[0]}    {[32]}    {[1]}    {'v'}    {[-0.4000]}
    {[33]}    {4×1 double}    {[32]}    {[0]}    {[33]}    {[1]}    {'v'}    {[-0.8000]}
    {[34]}    {4×1 double}    {[33]}    {[0]}    {[34]}    {[1]}    {'w'}    {[ 0.4000]}
    {[35]}    {4×1 double}    {[34]}    {[0]}    {[35]}    {[1]}    {'w'}    {[ 0.8000]}
    {[36]}    {4×1 double}    {[35]}    {[0]}    {[36]}    {[1]}    {'w'}    {[-0.4000]}
    {[37]}    {4×1 double}    {[36]}    {[0]}    {[37]}    {[1]}    {'w'}    {[-0.8000]}
    {[38]}    {4×1 double}    {[37]}    {[0]}    {[38]}    {[1]}    {'a'}    {[ 0.4000]}
    {[39]}    {4×1 double}    {[38]}    {[0]}    {[39]}    {[1]}    {'a'}    {[ 0.8000]}
    {[40]}    {4×1 double}    {[39]}    {[0]}    {[40]}    {[1]}    {'a'}    {[-0.4000]}
    {[41]}    {4×1 double}    {[40]}    {[0]}    {[41]}    {[1]}    {'a'}    {[-0.8000]}

```

The last ten in the master list:

```dash
>> SPKTs.EXPV.coordSequence(end-9:end,:)

ans =

  10×8 cell array

    {[2615]}    {4×1 double}    {[318]}    {[7]}    {[32]}    {[64]}    {'v'}    {[-0.4000]}
    {[2616]}    {4×1 double}    {[319]}    {[7]}    {[33]}    {[64]}    {'v'}    {[-0.8000]}
    {[2617]}    {4×1 double}    {[320]}    {[7]}    {[34]}    {[64]}    {'w'}    {[ 0.4000]}
    {[2618]}    {4×1 double}    {[321]}    {[7]}    {[35]}    {[64]}    {'w'}    {[ 0.8000]}
    {[2619]}    {4×1 double}    {[322]}    {[7]}    {[36]}    {[64]}    {'w'}    {[-0.4000]}
    {[2620]}    {4×1 double}    {[323]}    {[7]}    {[37]}    {[64]}    {'w'}    {[-0.8000]}
    {[2621]}    {4×1 double}    {[324]}    {[7]}    {[38]}    {[64]}    {'a'}    {[ 0.4000]}
    {[2622]}    {4×1 double}    {[325]}    {[7]}    {[39]}    {[64]}    {'a'}    {[ 0.8000]}
    {[2623]}    {4×1 double}    {[326]}    {[7]}    {[40]}    {[64]}    {'a'}    {[-0.4000]}
    {[2624]}    {4×1 double}    {[327]}    {[7]}    {[41]}    {[64]}    {'a'}    {[-0.8000]}
```

Column 1: position in the master list
Column 2: the positions in the experimental sequence where this unique texture appears. As an example:

```dash
>> SPKTs.EXPV.coordSequence{1:1,2}

ans =

        2073
        3705
        6137
        9348
```
Column 3: (NA) A number used for specifying the texture map on the disk (bookkeeping for us)
Column 4: (NB) An additional number used for specifying the texture map on the disk (bookkeeping)
Column 5: coordinate number (1-41 in these BTC experiments).
Column 6: sample from the texture ensemble associated with each coordinate.
Column 7: texture class
Column 8: correlation strength and sign for the coordinate   

Now we look inside the structured arrays for the texture classes. The R class has a different organization than the other classes due to the absence of any coordinates other than the origin.
For example, 
```dash
>> SPKTs.R(1)

ans = 

  struct with fields:

    mp0: [1×1 struct]
```
but
```dash
ans = 

  struct with fields:

    m2: [1×1 struct]
    p2: [1×1 struct]
    p1: [1×1 struct]
    m1: [1×1 struct]
```

We look within SPKTs.R(1) at the structure mp0. The field name mp0 signifies that these stimuli are from the origin in the stimulus space, a position that has neither or positive or negative coordinate value.
```dash
ans = 

  struct with fields:

    trialsInSequence: [1×64 double]
             HOCaxis: 'g'
        HOCaxisValue: 0
                Maps: [16×16×64 double]
            spkTimes: {1×6 cell}
```
Note that the **HOCaxis** is ‘g’ for gamma, even though these are random textures. Since all of the axes pass through the origin, we could have pulled the random textures from the origin of any of the 10 cardinal axes. The **HOCaxisValue** is zero, indicating that the stimuli used here are indeed random textures.
**Maps**: these are the 64, 16x16 element textures that were used in the experiment for the random texture class. The order in which they are stacked here corresponds to order of the unit responses in the field **spkTimes**. The position in the sequence in which each texture example appears is given in the field **trialsInSequence**. You can view these maps with, for example, 
figure,  imagesc(SPKTs.W(1).p2.Maps(:,:,1)). This will show the first 16x16 W ‘class’ texture for coordinate 0.8 used in the first repeat cycle.

For all the texture classes other than R, fields p1, p2, m1, m2 correspond to the ‘plus’ and ‘minus’ coordinates along the axes of these classes. 
```dash
>> SPKTs.B(3).m2

ans = 

  struct with fields:

    trialsInSequence: [1×64 double]
             HOCaxis: 'b'
        HOCaxisValue: -0.8000
            spkTimes: {1×6 cell}
```
Note the HOCaxisValue is -0.8, while for the p1 field,
```dash
>> SPKTs.B(3).p1

ans = 

  struct with fields:

    trialsInSequence: [1×64 double]
             HOCaxis: 'b'
        HOCaxisValue: 0.4000
            spkTimes: {1×6 cell}
```
the **HOCaxisValue** is 0.4. Note also that since these stimuli are delivered during the third repeat cycle of the stimulus sequence, the **trialsInSequence** field has higher numbers than the field has for SPKTs.B(1).trialsInSequence.

If we open the **spkTimes** field, we see the following:
```dash
>> SPKTs.U(2).m1.spkTimes

ans =

  1×6 cell array

    {1×64 cell}    {1×64 cell}    {1×64 cell}    {1×64 cell}    {1×64 cell}    {1×64 cell}
```
Each cell array is for one of the 6 clusters listed in SPKTs.EXPV.Clusters. These data were generated by the U class textures at the m1 coordinate (-0.4) during the second repeat cycle.
So, for each cluster, we have the spike times for each presentation of the texture examples from the coordinate along the U class axis. For the first presentation of one of these textures, we have the following spike times (in seconds with respect to the appearance of the texture) for Cluster 1 (here, ‘m1’):   
```dash
>> SPKTs.U(1).m1.spkTimes{1}{1}'

ans =

  Columns 1 through 9

    0.1177    0.1297    0.1392    0.1577    0.1605    0.1618    0.1663    0.1850    0.1891

  Columns 10 through 18

    0.2015    0.2093    0.2104    0.2227    0.2234    0.2253    0.2385    0.2403    0.2427

  Columns 19 through 26

    0.2447    0.2610    0.2954    0.2965    0.3022    0.3080    0.3134    0.3171
```

To summarize:

SPKTs.U(*repeat cycle*).*coordinate*.spkTimes{*Cluster number*}{*texture example*}.

Repeat cycle: 1-4  
Coordinate: mp0 (R), p1, p2, m1, m2 (for all other texture classes).  
Cluster number: refer to SPKTs.EXPV.Clusters. For this BTC file, the number runs from 1-6.  
Texture example: 1-64.  

### List of the datasets

We list below the names of the datasets, indicating for each of them the area (V1 or V2) and the layer of the recordings in the visual cortex.

| Dataset  | Area | Layer  |
| ------------- |:-------------:| -----:|
| L7215_TT3 |   V1 |   4B or 4Cα  |
| L7301_TT1 |   V1 |   4Cβ  |
| L7301_TT2 |   V1 |   2/3 or 4A or 4B  |
| L7301_TT3 |   V1 |   NaN  |
| L7301_TT4 |   V2 |   4  |
| L7301_TT5 |   V2 |   5 or 6 |
| L7301_TT6 |   V2 |   5 |
| L7304_TT2 |   V1 |   4Cα or 4Cβ |
| L7304_TT5 |   V2 |   4 or 5 |
| L7304_TT6 |   V2 |   5 |
| L7305_TT4 |   V2 |   4 |
| L7305_TT5 |   V2 |   2/3 or 4 |
| L7305_TT6 |   V2 |   2/3 or 4 |
| L7306_TT4 |   V2 |   2/3 |
| L7306_TT5 |   V2 |   2/3 |
| L7306_TT6 |   V2 |   2/3 or 4 |
| L7603_TT2 |   NA |  NaN |
| L7603_TT3 |   V2 |   6 or WM |
| L7603_TT4 |   V2 |   NaN |
| L7604_TT2 |   V2 |   5 or 6 |
| L7604_TT3 |   V2 |   5 or 6 |
| L8501_TT1 |   V1 |   2/3 |
| L8501_TT2 |   V1 |  4 |
| L8501_TT4 |   V1 |  2/3 |
| L8501_TT5 |   V1 |   2/3 |
| L8603_TT3 |   V1 |   4 |
| L8603_TT5 |   V1 |   5 or 6 |
| L8605_TT3 |   V1 |  5 or 6 |

### Selection of the Data

We briefly describe the data files contained in the folder named Selection. Their names have the suffix “one0_SL”, e. g. L7215_TT3_one0_SL.mat. 
These files are a selection of the spike data from the previously described datasets. The selected data has been analyzed in the manuscript  
A Guidolin, M Desroches, JD Victor, K Purpura, & S Rodrigues (2021) *Geometry of spiking activity in early visual cortex: a Topological Data Analytic approach.*

Example data file: L7215_TT3_one0_SL.mat. 
L7215_TT3_one0_SL.selectedClusters  contains the identity (as numbered in the original dataset L7215_TT3_btc_SPKTs.mat) of the single-units (neurons) that were selected for the analysis from the original dataset.

L7215_TT3_one0_SL.summary80groups contain information on the selected 80 collection of neural responses within the original dataset. For each of the 80 collections (rows), the first four columns are:

Column 1: number of non-empty responses in the original dataset (computed considering all neurons of the original dataset, before restricting to considering four neurons)

Column 2: axis of correlation of the visual texture that elicited the response. The axes are numbered from 1 to 10, and correspond as follows to the letters denoting axes in the original dataset:
1 - G, &nbsp; 2 - B, &nbsp; 3 - C, &nbsp; 4 - D, &nbsp; 5 - E, &nbsp; 6 - T, &nbsp; 7 - U, &nbsp; 8 - V, &nbsp; 9 - W, &nbsp; 10 - A.

Column 3: number of repeat of the experiment in which the response was recorded (1-4).

Column 4: strength of correlation of the visual texture that elicited the response. The strength levels are numbered from 1 to 4, and correspond as follows to the abbreviations denoting strength levels in the original dataset:
1 - m2, &nbsp; 2 - m1, &nbsp; 3 - p1, &nbsp; 4 - p2.
