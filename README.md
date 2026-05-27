# EEG-Study

## How to start: 
<img width="990" height="970" alt="Screenshot 2026-04-21 at 4 01 03 pm" src="https://github.com/user-attachments/assets/e7814f4f-daa0-4660-a1c5-543496d616cb" />

Before started: 

Step 1. open the EEGLAB 

Step 2. click file -> load the exisiting dataset    

<span style="color:red"> this is just for prac (since using sample dataset from EEGLAB). In real experiemental setting, I need to import data in a right format </span>

Step 3. find and click the "eeglab_data.set"

After successful completion:

This screen will shows up-

<img width="1632" height="1190" alt="Screenshot 2026-05-05 at 5 28 49 pm" src="https://github.com/user-attachments/assets/1d77370c-50b9-4d4f-bd0d-a1b02f9a6862" />




# Terminology of EEGlab

## {EVENT DATA}

When analyzing EEG data, one of the most crucial elements is knowing: 'when and what happened' 
'Import event info' is the menu used to input that exact information

### EEG Event:
  Stimulus onset: "The moment a red square appeared on the screen"
  Response: "The moment the subject pressed a button"
  Error: "The moment the subject sneezed, introducing muscle noise"
  
Depending on the setup, the computer presenting the stimuli might save the event logs as a separate text file (e.g., .txt, .csv)
This menu is used to execute the command: "Import the separately saved event record file and align it perfectly with the time axis of the currently open EEG data.

Conditions for the Event Info File (Prerequisites)
For EEGLAB to read event information, it primarily requires a text-format file (such as .txt or .csv). This file should not be a complex document, but rather a very simple format much like an Excel spreadsheet.

It must contain the following two columns:

  1. Latency (Occurrence Time): A number indicating 'when' the event occurred after the start of the EEG measurement. (This is usually recorded in seconds or as the number of data frames/sample number).
  
  2. Type (Event Category): The 'name tag' of the event that occurred at that specific time. (e.g., 'StimulusA', 'ButtonClick', 'Error', etc.)

### EX:

If 'StimulusA' was presented at 1.5 seconds, and the subject pressed a 'Button' at 3.2 seconds, the text file would look roughly like this:

[Uploading Elatency, type
1.5, stimulusA
3.2, bottons
EGeventcode.txt…]()


### Option Settings (Crucial Step):
When a new window opens, you must inform EEGLAB how the data in the imported file is structured.

1. Input field (column) names: Specify the names according to the column order in the text file.
  
   EX: if the first column is the occurrence time and the second is the type, type latency type in this field, separated by a space.

2. Time unit: If the latency numbers in the file are recorded in 'seconds', adjust this setting to match.

3. Alignment: Choose the reference point for aligning the start of the existing data with the start of the event times. (The default is usually based on the first data sample).

4. Apply: Click Ok, and the newly imported event markers will be overlaid on top of your existing EEG data.

### After successful completion of these process, this screen will shows up:

<img width="1418" height="690" alt="Screenshot 2026-05-05 at 5 46 51 pm" src="https://github.com/user-attachments/assets/772d579d-30e6-4ef0-83ef-6f1617dd3f86" />



1. Append events (Whether to keep existing events)
  
  - Unchecked (overwrite): Erases all existing event markers in the EEG data and completely overwrites them with the contents of the file you are currently loading.
  
  - Checked: Keeps the existing event markers as they are and appends the contents of the new file.

Tip: If the data already has events (like the sample data) and you just want to layer new information on top, it might be safer to check this box.

2. Input field (column) names **(Most important!)**
This is where you specify what data each column in the imported text file represents, in order.

Ex) on the right, (type latency duration) - no comma needed to spacing these 3 data. (Latency; occurrence time MUST included for EEGLAB to grasp the timing

3. Number of file header lines (Skipping header rows)
This field asks if the top row of the loaded text file contains a 'Header' (titles) rather than actual data.

If there is text like 'Time' or 'Event Type' in the top row (much like an Excel file), the machine might mistake it for numbers and throw an error.

In such cases, entering the number 1 commands the system to "skip the first row because it's a title." If the file is full of raw data without any headers, you can leave it at the default value of 0.

4. Time unit (sec)

This tells the system what time unit the latency numbers in the text file are using. 

    1: When the unit is in Seconds (e.g., 1.5 seconds).
    
    1E-3: When the unit is in Milliseconds (e.g., 1500ms).
    
    NaN: When it is recorded not in time units, but as sequential 'Data points/Frames' of the EEG data.

Once I have adjusted these four settings to match the format of prepared text file, click the Ok button at the bottom right of the window. <- this should be happen, however, there is error going on; Since I use the eeglab datasets, might be blocker regarding this.


<img width="1602" height="1094" alt="Screenshot 2026-05-05 at 5 43 42 pm" src="https://github.com/user-attachments/assets/b4676e4f-701f-4414-a828-da75cf68666d" />



The event types in this sample dataset are 

1. Square
2. RT




## {Using EEG functions and plugin}


<img width="864" height="1024" alt="Screenshot 2026-05-05 at 5 26 21 pm" src="https://github.com/user-attachments/assets/7b788e4f-069d-4875-b15c-ef3601c8bee3" />


### 1. General Data & Basic Formats
  
   ASCII/float file or MATLAB array: Simple text file that can open in Excel file (e.g., .txt or .csv) containging sequences of numbers

   Biosemi BDF file (BIOSIG Plugin): standard medical/research formats, research EEG device called 'Biosemi'

   EDF/EDF+/GDF files: EDF (European Data Format), global standard format for pilysomnography and clinical EEGs. (most of the hospital equipment devices)

### 2. Specific Equipment Manufacturer Formats
The options below are proprietary formats created by individual EEG equipment manufacturers specifically for their machines.

    ANT EEProbe (.CNT / .AVR file): Files extracted from 'ANT Neuro' equipment.

    BIDS(Brain Imaging Data Structure) folder structure: not a specific file, a folder organisation rule - international standard for naming folders and files to share research data; load an entire folder organsied according to these rules at once.

    Brain Vis. Rec. (.vhdr / .ahdr file) / Matlab file: 'Brain Products (BrainVision : research EEG device), 3 files as a set; data (.eeg), header (.vhdr), and marker (.vmrk).

   Netstation (binary / Multiple seg. / Matlab): 'EGI (/Magstim)' created. When using high-density EEG caps (resembloing hairnets) with 128 or 256 electrodes.

   Muse Direct / Monitor App .CSV file: Files extracted from 'Muse', a consumer-grade meditation and sleep EEG headband (available for general purchase), and its smartphone app -> could be used for remote participants study

  Neuroscan (.CNT / .EEG file): The format of 'Compumedics Neuroscan'; EEG equipment brand.

  Snapmaster .SMA file: The format for Snapmaster, PC-based EEG data collection programs.

  From .XDF or .XDFZ file: A general-purpose Extensible Data Format. Primarily used for synchronising and recording data from multiple devices simultaneously during an experiments (i.e., EEG, eye-trackers, and mouse movements)

  Import Magstim/EGI .mff file: A relatively modern format for the aforementioned EGI Net Station equipment.

# Managing datasets in EEGLAB

  ## Modify and store the dataset
  
  <img width="1418" height="1374" alt="Screenshot 2026-05-07 at 1 53 01 pm" src="https://github.com/user-attachments/assets/68e7a9e9-0f4b-4a2c-903b-b3fac8a1d14f" />


# Filter the data

## 1. FIR (Finite Impulse Response) Filters: most widely used methid in EEG research.

   Advantage of use this funtion:

   maintaining the exact occurence time of EEG waveforms - doesn't cause 'phase distortion (:pushes or twists the time axis of the data)'

  ### FIR filter types: 
  1. Basic FIR filter (new, default):

     Standard filter, most recommened in EEGLAB. Stable with minimal signal distortion.

     {using this default value is considered the general standard}

  2. Windowed sinc FIR filter:

    Traditional method in signal processing. Applies mathematical window function to reduce the waveform distortion that occurs when cutting off frequencies. <- Basic FIR filter adopts a specific form of this sinc method that is already optimised to the most stable values (rarely used)

  3. Parks-McClellan (equiripple) FIR filter:

     Specialised in cutting out the desired frequency band in a shape and accurate manner.

     Risk: this filter creating artificial wave shapes (Ringing artifacts) around sharp waveforms (e.g., epileptic spikes)

  4. Moving average FIR filter:

     Smoothing the signal by averaging adjacent data points. Rarely used for precise frequency band separation.

### IIR (Infinite Impulse Response) Filters type: 
    Short IIR filter:

    Calculation speed is faster, cuts frequencies sharply (compated to FIR). It can cause 'Phase Distortion'. Used when computational resources are lacking / real-time processing is required 

    Not Recommened cases: 
    
    time accuracy is crucial (e.g., Event-Related Potentials (ERP)


After Clicked Basic FIR filter (new, default):

<img width="968" height="864" alt="Screenshot 2026-05-07 at 1 53 28 pm" src="https://github.com/user-attachments/assets/94d08f92-53ba-41fe-9311-7e9c9e1e2d20" />


I've set the Lower edge of the frequency pass band (Hz) as in 1, Just for prac. 



### 3 Main categories based on objects:

  1. General Screening and Clinical Reading (The Basics): Setting - 1 Hz to 70 Hz (plus 60Hz Notch filter turned on)
  
      EEGLAB Input: Lower = 1, Higher = 70

     Reason: "Spike" wave forms (During the epilepsy diagnosis) are fast and acute - the frequency pathway **MUST** kept open up to a high limit (70Hz).

  2. **Cognitive Science Research (ERP, Event-Related Potentials)**: Setting- 0.1 Hz to 30 Hz

      EEGLAB Input: Lower = 0.1, Higher = 30

      Reason: EEG showing the visual or auditory stimuli (ERPs); rapid waves above 30Hz (: muscle movements) needed to cut off to smooth out.

      Using 0.1Hz (rather than 1Hz) prevents the slow lingering effects of the brainwaves from being removed.

     !! In most cases of cognitive/neuro- psychology research will use this. In my research, I would be use this methods as well, since it will contains visual stimuli (Various types of facial expressions).


  3. Cleaning the Data (Preprocessing for ICA Application): Setting- 1 Hz to 40 Hz (or 45 Hz)

    EEGLAB Input: Lower = 1, Higher = 40

    Reason: To automatically filter out major artifacts (e.g., eye blinks, sweats) using Independent component Analysis (ICA). Use this when data needed to be highly stable. Blocking the too slow waveforms (1Hz) and capping the top at 40Hz to preventing power line noise (In Europe; 50Hz)


=> 

### Curiosity 1. Lower limit settings in cognitive science (ERP) research

0.1Hz is mostly adopted as the standards in cogntive science reseach

Reason: If the Lower edge is raised to 1Hz (rather than 0.1Hz), the waveforms of cognition-related brain waves that slowly appear 100m/s after the stimulus presentation (e.g., late event-related potnetials: P300, N400) can be distorted. 

(Note: Recent analysis trends - To improve the accuracy of ICA, cross-application technique is actively used; Training the ICA algorithm only on a 'copy with a 1Hz filter applied' and then overlaying the resulting noise removal fomular onto the 'original data filtered at 0.1Hz'.)

### Curiosity 2. The identity of movements below 1Hz and the reason for the 40Hz upper limit

  *The nature of frequencies below 1Hz*: 
  
  primarily mechanical and physiological noise (: galvanic skin response (GSR) caused by sweat, slow drifts resulting from chemical changes between the electrodes and the scalp, and the patient's slow breathing).
  
+) Although delta waves (0.5–4Hz) are treated as significant in sleep EEGs (not with awake subjects)

  *A reason for the 40Hz upper limit*
  
  Muscle noise (EMG)—generated when a subject frowns or tenses their neck or jaw—spreads widely across higher frequency bands (especially above 20Hz). -> When setting the upper limit into 40Hz: Reduce interference from a substantial amount of muscle noise.


## After completion of setting the lower/higher limits: 

  
<img width="1436" height="320" alt="Screenshot 2026-05-07 at 1 54 25 pm" src="https://github.com/user-attachments/assets/06b6309a-a5e0-40f6-8497-bf5c27da1dbc" />


<img width="1438" height="1292" alt="Screenshot 2026-05-07 at 1 55 06 pm" src="https://github.com/user-attachments/assets/37bc391f-8d35-4218-a01b-4f2e8d3f2351" />


## How to deleting the dataset: 

<img width="1378" height="734" alt="Screenshot 2026-05-07 at 1 56 36 pm" src="https://github.com/user-attachments/assets/a8852023-e1db-4402-888e-f748f2ba8b72" />


# Continous data_ EEGLAB

## [Preparation]

### Manual: First, if you have a raw EEG data file, determine the file format...

### Meaning: First, check the label (file extension, e.g., .cnt, .edf) of your raw EEG file to identify which equipment was used to record it.


# EEG Equipment & File Formats Frequently Used in Psychology

## 1. Brain Products — .vhdr / .eeg / .vmrk

: Currently the most widely used equipment in psychology research laboratories.

* Product Lines: BrainAmp, actiCHamp, etc.

* Data Structure: Files are saved as a 3-file set:

  * vhdr: Header file (contains metadata like channel count, sampling frequency, etc.)
  
  * eeg: The actual raw EEG data.
  
  * vmrk: Marker file (contains event markers, such as stimulus onset times).

* EEGLAB Import: Requires the BVA-io plugin to read.

## 2. Biosemi — .bdf 

: Frequently used in sleep research and cognitive experiments

* Flagship Product: ActiveTwo system.

* EEGLAB Import: Supported natively (Default / No extra plugin required).

* Strengths: Highly optimised for high-density setups (64-channel, 128-channel).

## 3. EDF / EDF+ — .edf

: The most standard format used within clinical hospital environments

* Primary Uses: Polysomnography (PSG / Sleep studies), epilepsy diagnosis, etc.

* Characteristics: A universal format that can be exported by many different hardware systems.

* EEGLAB Import: Supported natively (Default).

## 4. Neuroscan — .cnt / .avg

: A legacy system that has a long history of use in psychology labs.

File Types:

  * .cnt: Continuous raw data.

  * .avg: Averaged Event-Related Potential (ERP) data.

## 5. EGI (Electrical Geodesics) — .mff / .raw

: Specialised for ultra-high-density electrode arrays (128 to 256 channels)

  * Primary Uses: Widely utilised in developmental psychology and child research.
  
  * Design: Distinctive net-like, hydrocel geodesic sensor cap.
  
  * EEGLAB Import: Requires the MFF-matlab-io plugin.

## 6. Common/Standard Format — .set

: not a hardware-specific file, but rather EEGLAB's native storage format.

  * Workflow: Import data via any external format $\rightarrow$ Save it within EEGLAB $\rightarrow$ Outputs as a .set file.
    
  * Advantage: Convenient because it can be opened directly in subsequent sessions without re-importing.

## 7. Modern Standard — BIDS Format

: An international standard has been actively pushed in recent research to enhance data sharing and reproducibility

  * Focus: Rather than a specific file extension, it dictates a standardised folder architecture and metadata formatting method.
  
  * Primary Uses: Highly recommended when publishing open-access dataset repositories for journals.
  
  * EEGLAB Import: Fully supports both BIDS import and export functionalities.



<img width="858" height="1032" alt="Screenshot 2026-05-25 at 2 25 14 pm" src="https://github.com/user-attachments/assets/4c1d1b67-9166-426d-b2cb-584e85dc944b" />

$\rightarrow$ 

* Multi-modal synchronisation (.XDF, .XDFD) : An integrated multi-stream container format used when recording EEG, eye-trackiing, and behavioural logs simultaneously in real-time via Lab streaming Layer (LSL)

* Open Data standard (BIDS folder structure) : The international organisational data standard increasingly mandated by top-tier neuroimaging journals to ensure computational reproducibility and open science sharing

* Consumer Grade/Alternative (.CSV - Muse) : Raw metrics exported from commerical, consumer-grad meditation bands

* Consumer Grade/Alternative (Netstation) : A dedicated analysis software forma

* Consumer Grade/Alternative (.SMA) : A legacy format utilised by specific niche analog data acquisition hardware nodes


## [Step 1: Check the Default Menu]: " .edf (EDF/EDF +), .bdf (Biosemi), .cnt (Neuroscan) "

### Manual: Look if a menu item is available in File $\rightarrow$ Using EEGLAB functions and plugins.
### Meaning: Look for your specific file extension in the standard EEGLAB menu. If it's there, simply click it. This is the most straightforward, standard route.


<img width="1932" height="1284" alt="Screenshot 2026-05-24 at 5 46 22 pm" src="https://github.com/user-attachments/assets/efcd8fe2-493f-4fbb-8814-1d5e5180f15e" />

<img width="1024" height="872" alt="Screenshot 2026-05-24 at 5 46 06 pm" src="https://github.com/user-attachments/assets/35c42c68-a3de-4891-9a3b-49738136711b" />

<img width="640" height="356" alt="Screenshot 2026-05-24 at 5 50 29 pm" src="https://github.com/user-attachments/assets/520349a3-67f8-4667-900d-2297cf63c2ed" />


## [Step 2: Use the Universal Translator]: Target Formats are rare, proprietary, or highly legacy data configurations, not listed above.

### Manual: Use menu item File $\rightarrow$ Using the File-IO interface.

<img width="1256" height="1068" alt="Screenshot 2026-05-25 at 11 32 50 am" src="https://github.com/user-attachments/assets/b5e7e39f-08d6-491a-9e71-7e4adde49517" />
<img width="524" height="346" alt="Screenshot 2026-05-25 at 11 33 07 am" src="https://github.com/user-attachments/assets/eb7053db-0caa-425e-8309-8ff988169386" />

## [Step 3: Use the Medical-Grade Translator]: " .edf (EDF/EDF +), .bdf (Biosemi), .cnt (Neuroscan) $\rightarrow$ Steps 1 & 3 Merged" 

## Manual: Use menu item File $\rightarrow$ Using the BIOSIG interface.
## Meaning: This is a highly specialised translator tailored specifically for medical and laboratory data structures used in clinics and research facilities.

<img width="1258" height="1070" alt="Screenshot 2026-05-25 at 11 36 47 am" src="https://github.com/user-attachments/assets/0f181230-4469-497b-9f99-8e836d70b114" />

## [Step 4: Download a Dedicated Add-on]: " .vhdr (Brain Products), .mff (EGI), BIDS structures" 

$\rightarrow$ These importers might already be visible in Step 1. However, if they are missing, this is your classic Step 4 scenario

# Importing a MATLAB array _ Practising: https://eeglab.org/tutorials/04_Import/Importing_Continuous_and_Epoched_Data.html

 ## % build a matrix of random test data (32 channels, 100 seconds at 256 Hz)

 $\rightarrow$ Used ocatave: first attempt, error occured

 
<img width="2880" height="1800" alt="Screenshot 2026-05-25 at 3 30 40 pm" src="https://github.com/user-attachments/assets/cd3afc50-c061-4fa1-a9d8-26ac25151963" />

<img width="210" height="230" alt="Screenshot 2026-05-25 at 3 48 57 pm" src="https://github.com/user-attachments/assets/8a7bbda5-fffa-4301-8d7d-570670adc19d" />
 
<img width="1978" height="1106" alt="Screenshot 2026-05-25 at 3 43 28 pm" src="https://github.com/user-attachments/assets/8a46610f-5f22-4d5a-a8f5-e9ccaf75ddea" />


 
 $\rightarrow$  troubleshooting for the EEGLAB .mat file import error:

You need to re-save the data in the Octave Online console by explicitly passing the -mat or -v6 version flags

Used code- 

eegdata = rand(32, 256*100);

save('-mat', 'fake_eeg.mat', 'eegdata');


<img width="236" height="210" alt="Screenshot 2026-05-25 at 3 51 37 pm" src="https://github.com/user-attachments/assets/6b003605-4a1c-4d05-a380-ac56434049b2" />

<img width="1238" height="1074" alt="Screenshot 2026-05-25 at 3 51 47 pm" src="https://github.com/user-attachments/assets/b80b872a-e612-4d39-8a46-65afb896714c" />



# Sample practice challenge

Reference: Sex modulation of faces prediction error in the autistic brain

## EEG recording. 

* EEG recordings were performed at the IRMaGeneurophysiology facility (Grenoble, France). **BrainAmp amplifiers and EasyCaps (Brain Products GmbH, Germany) with 96 active electrodes following the 10–5 standard system were used for EEG recording**, with impedance kept below 25 kΩ. A sampling rate of 1000 Hz was used for signal recording, with an anti-aliasing filter at 500 Hz. 
* The ground electrode for the EEG was FPz, while the reference electrode was FCz. Two electrodes on the left and right outer canthi of the eyes and two others above and below the left
eye were used to record the horizontal and vertical electrooculographic (EOG) activity (hEOG and vEOG), respectively.
The ground electrode for EOG was positioned on the left base of the neck.


* EEGLAB Data import file selection: 

<img width="1908" height="1164" alt="Screenshot 2026-05-27 at 2 57 38 pm" src="https://github.com/user-attachments/assets/8e320296-d8c6-44ad-9d3c-f7950432fe48" />




## EEG preprocessing.

* Brainstorm software105 and MATLAB (The
MathWorks Inc.) scripts were used for EEG preprocessing.
Muscular artifacts were manually discarded for each participant.
The signal was then re-referenced using the average reference.
Eye movements were corrected using signal space projection
(SSP). Finally, a band-pass filter of 0.1–40 Hz was applied to the
cleaned signal and trials were epoched from 100 ms pre-stimulus
to 600 ms post-stimulus, except for the first three trials of the sequences and trials presented after the deviant or target, which
were excluded. In the end, 1% of the trials from NA participants
and 2.3% of the trials from autistic participants were discarded
during preprocessing. Next, bad channels were interpolated based
on neighboring channels. An average of 4 channels were inter-
polated per participant. For six participants, the signal was
recorded on only 64 electrodes and missing electrodes (dis-
tributed on the scalp) were also interpolated for statistical
analyses.
Event-related potentials. For each subject and each condition of
interest in the oddball sequence (standard, dHSF, dLSF) and in
the equiprobable sequence, all trials were averaged. MMRs were
computed for HSF and LSF conditions by calculating the arith-
metic difference between the ERPs to the deviant in the oddball
sequence, and the ERPs to the same stimulus presented in the
equiprobable sequence. Finally, grand average waveforms were
computed across participants for each ERP and deviant
condition.
Source reconstruction. The anatomical location of the activity was
estimated by source reconstruction using Brainstorm. A realistic
forward model based on the ICBM152 template and a standard
co-registered set of electrode positions was used. Noise covariance
matrices were computed for each participant using the baseline
activity of each condition. The source space was restricted to the
cortical surface with 2500 dipoles and the inversion kernel was
computed using sLoreta106 assuming SNR 3 and unconstrained
orientation. Source reconstruction was performed for each par-
ticipant in each condition, except for one autistic participant who
had an atypical signal in frontal areas. Then, the difference in
sources between deviant and equiprobable conditions (for HSF and LSF) was performed for each participant as well as the difference between HSF MMR and LSF MMR. Finally, the signal was
average for each group and subgroup (autistic males, autistic
females, NA males and NA females) in each condition.

FYI, autistic individuals would rely on High Spatial Frequencies of the images (HSF, conveying local information) / Low Spatial Frequencies (LSF)
