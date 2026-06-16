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

Reference: Soma Chaudhuri and Joydeep Bhattacharya (2025). Poetry Assessment EEG Dataset 1. OpenNeuro. [Dataset] doi: doi:10.18112/openneuro.ds006648.v1.0.0

## EEG recording. 

Dataset Core Information: ds006648

## Experimental Overview: 

1. Topic: Neural mechanics of reading poetic language.
2. Participants: $47$ individuals (whose data passed EEG quality control standards).
3. EEG Setup: 64-channel, continuous data logging.



## Stimuli: 

Total of 210 textual stimuli divided across 7 blocks:

1. Haiku (70 items): Nature-themed poetry.

2. Senryu (70 items): Emotion-themed poetry.

3. Control (70 items): Non-poetic, standard prose.


## * Behavioural Evaluations (5 Subjective Dimensions, 7-Point Likert Scale)

1. Aesthetic Appeal

2. Vivid Imagery

3. Being Moved

4. Originality

5. Creativity


## File Architecture (Per Subject Directory)

* File Name : eeg.set - Actual processed EEG tracking records (EEGLAB Native format $\rightarrow$ opens instantly).

* File Name : eeg.json - Recording metadata and hardware specifications

* File Name : channels.tsv - Spatial electrode channel mapping profiles.

* File Name : events.tsv - Logged trial event marker timelines.

## Critical Trigger Event Codes

* 65285, 65286: Baseline baseline metrics (Pre-experiment Resting State).

* 65287, 65288: Fatigue control metrics (Post-experiment Resting State).

## Secondary Data Repositories (/derivatives/)

* Behavioural Records: Trial-by-trial evaluation metrics saved in individual ".csv" format logs.

* Psychometric Profiles: Standard clinical battery scores including "PANAS, Openness, Curiosity, VVIQ, AVIQ, MAAS, and AReA surveys".

# 1. Import data

<img width="454" height="938" alt="Screenshot 2026-05-31 at 2 22 49 pm" src="https://github.com/user-attachments/assets/6d094953-71d8-4c4e-8a14-aa678f54a9de" />

<img width="1430" height="1236" alt="Screenshot 2026-05-31 at 2 24 27 pm" src="https://github.com/user-attachments/assets/adfe074f-c5db-47e5-abe9-cd8025ee61f6" />

# 2. Plot the raw EEG signals to see what they look like visually + Scan the display to identify channels with severe artifact noise.


<img width="1586" height="1096" alt="Screenshot 2026-05-31 at 2 28 05 pm" src="https://github.com/user-attachments/assets/4d598ce6-48db-43ec-ad3a-e770ddff07fa" />

$\rightarrow$ Make the scale into 300 - 500, make it 400

<img width="1602" height="1112" alt="Screenshot 2026-05-31 at 2 30 07 pm" src="https://github.com/user-attachments/assets/50a7fc59-ee34-409b-a94d-cc17136a5970" />

# Why We Plot Raw Data First: 

* The main purpose of checking the raw data visually before running automated preprocessing pipelines is to determine if the dataset is viable.


EX: 

* Half of the channels are completely flat: This indicates a hardware recording failure, meaning this participant's session will likely be unusable.

* The signals are excessively noisy throughout: It might be difficult to recover clean signals even with advanced preprocessing.

* The data looks relatively clean: Your preprocessing strategy can remain straightforward and minimal.


# 3. Filtering 

* Tools $\rightarrow$ Filter the data $\rightarrow$ Basic FIR filter

* Filter settings:

  1. Lower edge frequency (High-pass filter): 1 (Removes slow baseline drifts below 1 Hz)
  
  2. Upper edge frequency (Low-pass filter): 40 (Removes high-frequency line noise above 40 Hz)
 
  3. All other parameters: Keep as default $\rightarrow$ Click OK
  
<img width="1614" height="1368" alt="Screenshot 2026-05-31 at 3 01 20 pm" src="https://github.com/user-attachments/assets/e4a964e3-a016-4b77-af9b-9debbbd86f29" />

<img width="1598" height="1098" alt="Screenshot 2026-05-31 at 3 17 20 pm" src="https://github.com/user-attachments/assets/c72f744b-4aa8-4e6f-a844-141e83bcaf45" />

<img width="1596" height="1108" alt="Screenshot 2026-05-31 at 3 20 38 pm" src="https://github.com/user-attachments/assets/b0556d86-aa89-4fd7-a64e-a20dd6ee569f" />

<img width="968" height="870" alt="Screenshot 2026-05-31 at 3 12 04 pm" src="https://github.com/user-attachments/assets/983005bb-47ad-4a4d-9639-4d8ae381c69c" />

<img width="1644" height="1178" alt="Screenshot 2026-05-31 at 3 04 12 pm" src="https://github.com/user-attachments/assets/4ea045c8-7967-4c98-a3e0-77541ac00bde" />

$\rightarrow$ Make the scale into 300 - 500, make it 400

<img width="1490" height="900" alt="Screenshot 2026-05-31 at 3 12 33 pm" src="https://github.com/user-attachments/assets/a33f0866-435d-40f5-aee8-a0e89f07ed9e" />

# 4. Reject data using Clean Rawdata and ASR

<img width="1476" height="912" alt="Screenshot 2026-05-31 at 3 22 44 pm" src="https://github.com/user-attachments/assets/0f8c7cc7-8efd-4336-9cb5-5e697f7007d6" />

<img width="1014" height="1208" alt="Screenshot 2026-06-05 at 5 24 25 pm" src="https://github.com/user-attachments/assets/99bf94fc-ac51-46a3-b6da-634749cf639d" />


## Curiosity: Parameter Breakdown

### 1. Remove channel drift (Unchecked)

* "Removes slow tracking drift where a signal gradually floats upward or downward."
  
* Reality: If an electrode shifts slightly against the participant's scalp, the baseline signal will slowly drift up or down.

* Why we uncheck it: Since we already applied a 1 Hz high-pass filter in the previous step, that filter has already eliminated these slow baseline drifts. Running it twice is redundant, so we leave it unchecked.

### 2. Remove channel if flat for more than 5 seconds

* "Identifies and removes a channel as dead if its signal goes completely flat for 5 seconds or longer."

* Reality: A functional EEG channel must constantly fluctuate.

* Why we use it: If a signal shows zero variance for more than 5 seconds, the electrode has either completely disconnected from the scalp or suffered a hardware malfunction. This setting automatically drops that faulty channel from the dataset.

### 3. Min acceptable correlation: 0.85

* "A channel is considered normal only if its signal movement correlates at least 85% with its neighbouring channels."

* Reality: Because of volume conduction through the scalp, adjacent EEG electrodes should naturally record highly similar signal patterns. For instance, channel Fz should fluctuate similarly to F3 and F4.

* Why we use it: If the correlation coefficient drops below 0.85, it means the channel is behaving erratically compared to its neighbours. Python flags this as an anomaly and removes it. The higher you set this threshold, the more strictly it discards channels (0.85 is the standard baseline value).


# Curiosity: Do we need to set the channel location?

## Why Channel Locations Are Essential

* Without channel locations mapped, your analysis will immediately hit several walls:

  * Immediate Errors: You will experience re-referencing failures & you will be completely unable to run ICA to remove eye-blink artifacts.

  * Downstream Limitations: You won't be able to generate scalp topographies (the colour-mapped 2D head plots showing voltage distribution) or properly visualise your Event-Related Potential (ERP) spatial distributions.

## How to set the channel location:

Step 1. Edit $\rightarrow$ channel locations

<img width="1704" height="1260" alt="Screenshot 2026-05-31 at 4 16 31 pm" src="https://github.com/user-attachments/assets/29edbd2e-e0f1-4c42-ab35-5f1c1c7eb4eb" />


Step 2. When this screen pops up, click the cancel 

<img width="1122" height="730" alt="Screenshot 2026-05-31 at 4 15 01 pm" src="https://github.com/user-attachments/assets/2a01031e-9ba5-410e-a65a-18cf7643d077" />

### Why You Should Cancel

This prompt is offering to automatically find coordinates using EEGLAB's generic system template (standard_1005.elc). 

However, for this specific dataset, we want to load the exact BioSemi64.loc file provided by the authors. 

Using the dataset's native mapping file ensures that your channel coordinates are 100% accurate to how the actual experiment was recorded.


Step 3. Cancel $\rightarrow$ Read locations $\rightarrow$ Finder $\rightarrow$ Onedrive $\rightarrow$  ds006648 $\rightarrow$ BioSemi64.loc

<img width="1310" height="1478" alt="Screenshot 2026-05-31 at 4 16 49 pm" src="https://github.com/user-attachments/assets/690cbd58-93be-47bf-a3b5-c24498ca84e5" />

<img width="1310" height="1478" alt="Screenshot 2026-05-31 at 4 16 49 pm" src="https://github.com/user-attachments/assets/d944cb80-0ddf-4c58-8164-ae501c20bf85" />

<img width="508" height="706" alt="Screenshot 2026-05-31 at 4 18 08 pm" src="https://github.com/user-attachments/assets/0c2a57f9-c42d-4054-a73b-cff1edfa1fa1" />


### Error Occurred: Still indicated as channel locations: no (labels only)

### Figure out - The Cause

: EEGLAB rejected the file mapping because the channel dimensions did not match (64 spatial points in the file vs. 70 total tracks in the dataset).

### Solution: Remove the EXG Channels First, Then Add Locations

* Remove the EXG Channels First

* Go to the top menu and click Edit $\rightarrow$ Select data, then configure the following settings:

    * Check or highlight the "Channel(s) to remove" field.

    * In the input text block below it, type or paste the exact auxiliary labels: EXG1 EXG2 EXG3 EXG4 EXG5 EXG6 EXG7 EXG8
 
    * Ensure "Remove these" is active $\rightarrow$ Click OK.

 <img width="1720" height="1204" alt="Screenshot 2026-05-31 at 4 44 14 pm" src="https://github.com/user-attachments/assets/41860c7e-9676-450f-b79a-9cb36b7c5f42" />

 <img width="1018" height="712" alt="Screenshot 2026-05-31 at 4 44 30 pm" src="https://github.com/user-attachments/assets/1edff898-cd49-4eaa-bfb0-421afe8dd0b5" />

 <img width="996" height="694" alt="Screenshot 2026-05-31 at 4 44 51 pm" src="https://github.com/user-attachments/assets/112490a5-8573-4c96-9b16-5d3ef1d82425" />

$\rightarrow$ Click Ok

  * These steps were successful $\rightarrow$ Try the Channel location setting again.

# Re-referencing the data

* Tools $\rightarrow$ Re-referencing the data

<img width="862" height="770" alt="Screenshot 2026-05-31 at 4 47 39 pm" src="https://github.com/user-attachments/assets/1ab2956d-d60c-4520-a679-5cc2fe79c999" />
 
## Why are we doing this?

* The Original Baseline: The raw data was initially recorded using the EXG5 and EXG6 electrodes (placed on the mastoids behind the ears) as the physical reference points.

* The Problem: Because we just removed those auxiliary EXG channels from our dataset to fix our spatial dimensions, our data loop no longer has an active baseline link to track.

* The Solution: To fix this, we recalculate a new baseline reference by shifting our tracking index to the Average Reference (the mathematical average of all remaining scalp channels combined).

## Why Average Reference is great for ERPs

By computing the mean signal across all 64 scalp electrodes and subtracting it from each individual channel, you cancel out localised biases. 

This creates a neutral baseline that brings out the true geographical distribution of your neural activity, which is ideal for isolating components like the N400 or P300 when analysing text or poetry processing.


# Decompose data by ICA

* Tools $\rightarrow$ Decompose data by ICA

<img width="1236" height="602" alt="Screenshot 2026-05-31 at 4 52 16 pm" src="https://github.com/user-attachments/assets/c1474a89-9c97-4ba6-99d9-69fb25fb9a1e" />

<img width="774" height="684" alt="Screenshot 2026-05-31 at 4 52 56 pm" src="https://github.com/user-attachments/assets/2511ea73-c73a-4cee-b16a-a148d00279f9" />

Takes quite of the time.

## When this screen pops up, don't press anything. Leave it.

<img width="650" height="324" alt="Screenshot 2026-05-31 at 4 54 48 pm" src="https://github.com/user-attachments/assets/e073077a-7e73-4c40-b52e-7d57a7bb55e5" />

### When it's done, it changes into 'yes' (Look up the section called ICA weights)

<img width="1102" height="716" alt="Screenshot 2026-06-05 at 6 31 22 pm" src="https://github.com/user-attachments/assets/82a77fd7-3d98-4212-8460-2768028d9b6d" />


# Classify components using ICLabel

* Tools → Classify components using ICLabel

<img width="1674" height="960" alt="Screenshot 2026-06-05 at 6 33 43 pm" src="https://github.com/user-attachments/assets/7f1d422d-b237-484f-9b9a-50c155559f5b" />

<img width="524" height="390" alt="Screenshot 2026-06-05 at 6 34 02 pm" src="https://github.com/user-attachments/assets/e1e7b8b7-7d5a-4f22-ad6f-ae32aaec427a" />

$\rightarrow$ Click the Default

<img width="802" height="546" alt="Screenshot 2026-06-05 at 6 34 27 pm" src="https://github.com/user-attachments/assets/96d052fb-81f6-4989-8579-9a99c2b7b5db" />

# Understanding the ICLabel Grid

<img width="1596" height="1166" alt="Screenshot 2026-06-05 at 6 36 23 pm" src="https://github.com/user-attachments/assets/a44563ac-c31f-44d3-8e9f-c455634c535e" />

<img width="1582" height="1498" alt="Screenshot 2026-06-05 at 6 36 18 pm" src="https://github.com/user-attachments/assets/8e153e0b-5136-4351-a3c9-3fba7b1bb3fe" />

* Each circular plot (scalp topography) represents an individual ICA component. The algorithm has successfully decomposed your continuous 64-channel EEG data into 62 independent, non-overlapping signal sources.

* Brian : Genuine neural activity - KEEP

* Eye : Ocular artifacts (Blinks, vertical/horizontal eye movements) - Remove

* Muscle : electormyographic noise (Jaw clenching, neck muscle tension) - Remove

* Channel noise : Isolated bad electrode connection jitter - Remove

* Other : Ambigous or mixed source signals - Review / Keep

## Components identified for rejection in this Data:

* Components 1 & 2: Classified as Eye (99.9%) $\rightarrow$ Classic vertical eye-blink profiles. Definite removal.
  
* Component 35: Classified as Eye (67.8%) $\rightarrow$ Likely a residual eye movement. Definite removal.
  
* Component 23: Classified as Channel Noise (95.6%) $\rightarrow$ High variance limited to a single sensor. Definite removal.

* Component 42: Classified as Muscle (84.6%) $\rightarrow$ High-frequency bursts typical of localized tension. Definite removal.

* Component 31: Classified as Muscle (42.0%) $\rightarrow$ Ambiguous distribution under the 80% threshold; safely kept for now.

# Automating the Cleanup

* Tools $\rightarrow$ Classify components using ICLabel $\rightarrow$ Flag components as artifacts

<img width="1784" height="914" alt="Screenshot 2026-06-07 at 11 23 31 am" src="https://github.com/user-attachments/assets/f1b561c7-4e9d-4b9d-aa11-d484ff888ebe" />

<img width="748" height="788" alt="Screenshot 2026-06-07 at 11 25 28 am" src="https://github.com/user-attachments/assets/2ccd571e-b8c9-4fb8-8bc5-3bca29acc1ed" />

<img width="1090" height="882" alt="Screenshot 2026-06-07 at 11 34 02 am" src="https://github.com/user-attachments/assets/2c2e9620-8b73-4e28-b817-7daa59a435ff" />

<img width="854" height="540" alt="Screenshot 2026-06-07 at 11 31 40 am" src="https://github.com/user-attachments/assets/7f71d8b1-fd43-4c53-a94b-aeb4a1193564" />

$\rightarrow$ Click Yes

<img width="1280" height="348" alt="Screenshot 2026-06-07 at 11 32 48 am" src="https://github.com/user-attachments/assets/bf89abd1-c007-441a-a2ca-0e66d34eb1aa" />

$\rightarrow$ Click Accept

## After cleaning: 

<img width="1598" height="1094" alt="Screenshot 2026-06-07 at 11 35 42 am" src="https://github.com/user-attachments/assets/87755419-1ed4-4ab0-8b62-9f723ac1b14a" />


### Before cleaning, channel data looks like this: 
<img width="2034" height="1390" alt="Screenshot 2026-06-07 at 11 36 33 am" src="https://github.com/user-attachments/assets/5ad21906-4ba4-4d7d-bc20-4bdb1bd59bb2" />


# ERP Analysis 

## Verify the Event Markers

Before performing Epoching (slicing the continuous data into trial-by-trial segments), you must identify the exact trigger codes used to mark the stimulus presentation times in the dataset

* Edit $\rightarrow$ Event value

<img width="992" height="674" alt="Screenshot 2026-06-07 at 11 39 29 am" src="https://github.com/user-attachments/assets/b6504ee8-cc81-4e9a-b5e4-d8d882d01c32" />

* 213 events recorded
  
* The first one is labelled 65284

## Check More Event Codes

* Please click the > (next) button a few times in that window to see what other numeric trigger codes appear throughout the recording.

* According to the ds006648 dataset documentation:

  - 65285, 65286: Baseline metrics (Pre-experiment Resting State)
  
  - 65287, 65288: Fatigue control metrics (Post-experiment Resting State)
 
<img width="1292" height="836" alt="Screenshot 2026-06-07 at 1 56 46 pm" src="https://github.com/user-attachments/assets/afcd4ebf-93fb-40ff-83e9-85d0f8d85f76" />

$\rightarrow$ Check the green part

### Curiosity: Do I have to check all 213 events one by one? Or is there a search option?

A: 

The Easier Method: Open the events.tsv file with Excel


<img width="1800" height="808" alt="Screenshot 2026-06-07 at 2 11 55 pm" src="https://github.com/user-attachments/assets/7718e783-c976-45fe-8313-b7f12ecf905e" />
<img width="2272" height="1488" alt="Screenshot 2026-06-07 at 2 11 31 pm" src="https://github.com/user-attachments/assets/640001c9-ad1e-4ea2-aec3-eae801c8c79a" />

* Once opened, look at the value or trial_type columns. You will be able to instantly identify which specific codes correspond to the Haiku, Senryu, and Control conditions

$\rightarrow$

* Since there is no trial_type column available in this specific spreadsheet, you need to look at the dataset's README file or the eeg.json file to find the decoding legend provided by the authors **Turns out** Preprocessing.m file contains such data (More specific details on finding the trigger's event code are available in the Branch: openNeuro_dataset_prac)


<img width="1574" height="854" alt="Screenshot 2026-06-07 at 3 58 24 pm" src="https://github.com/user-attachments/assets/f6b498a6-4b8c-4970-a720-f1f5d6d2b51c" />

<img width="1290" height="830" alt="Screenshot 2026-06-07 at 3 58 12 pm" src="https://github.com/user-attachments/assets/d3498780-ea0e-42a0-b913-ee59a703161d" />

* eventCode = 65282
* epochDuration = 15  % 4 seconds before, 11 seconds after
* epochOffset = 4

  - eventCode = 65282: The target trigger code used to slice the continuous data. EEGLAB will locate every instance where this specific marker occurs.
  
  - epochDuration = 15: The total time window (duration) for each sliced segment, which spans exactly 15 seconds in total.
  
  - epochOffset = 4: The pre-stimulus baseline window, set to 4 seconds before the trigger onset.

# Step 1. Epoching

