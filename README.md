# EEG-Study

## How to start: 
<img width="990" height="970" alt="Screenshot 2026-04-21 at 4 01 03 pm" src="https://github.com/user-attachments/assets/e7814f4f-daa0-4660-a1c5-543496d616cb" />

Before started: 

Step 1. open the EEGLAB 

Step 2. click file -> load the exisiting dataset    

<span style="color:red"> this is just for prac. In real experiemental setting, I need to import data in a right format</span>

Step 3. find and click the "eeglab_data.set"

After successful completion:

This screen will shows up-

<img width="1632" height="1190" alt="Screenshot 2026-05-05 at 5 28 49 pm" src="https://github.com/user-attachments/assets/1d77370c-50b9-4d4f-bd0d-a1b02f9a6862" />




Terminology of EEGlab

{EVENT DATA}

When analyzing EEG data, one of the most crucial elements is knowing: 'when and what happened' 
'Import event info' is the menu used to input that exact information

EEG Event:
  Stimulus onset: "The moment a red square appeared on the screen"
  Response: "The moment the subject pressed a button"
  Error: "The moment the subject sneezed, introducing muscle noise"
  
Depending on the setup, the computer presenting the stimuli might save the event logs as a separate text file (e.g., .txt, .csv)
This menu is used to execute the command: "Import the separately saved event record file and align it perfectly with the time axis of the currently open EEG data.

Conditions for the Event Info File (Prerequisites)
For EEGLAB to read event information, it primarily requires a text-format file (such as .txt or .csv). This file should not be a complex document, but rather a very simple format much like an Excel spreadsheet.

Fundamentally, it must contain the following two columns:

1. Latency (Occurrence Time): A number indicating 'when' the event occurred after the start of the EEG measurement. (This is usually recorded in seconds or as the number of data frames/sample number).

2. Type (Event Category): The 'name tag' of the event that occurred at that specific time. (e.g., 'StimulusA', 'ButtonClick', 'Error', etc.)

For example, if 'StimulusA' was presented at 1.5 seconds, and the subject pressed a 'Button' at 3.2 seconds, the text file would look roughly like this:

[Uploading Elatency, type
1.5, stimulusA
3.2, bottons
EGeventcode.txt…]()


Option Settings (Crucial Step):
When a new window opens, you must inform EEGLAB how the data in the imported file is structured.

Input field (column) names: Specify the names according to the column order in the text file. For instance, if the first column is the occurrence time and the second is the type, type latency type in this field, separated by a space.

Time unit: If the latency numbers in the file are recorded in 'seconds', adjust this setting to match.

Alignment: Choose the reference point for aligning the start of the existing data with the start of the event times. (The default is usually based on the first data sample).

Apply: Click Ok, and the newly imported event markers will be overlaid on top of your existing EEG data.

This screen will shows up:

<img width="1418" height="690" alt="Screenshot 2026-05-05 at 5 46 51 pm" src="https://github.com/user-attachments/assets/772d579d-30e6-4ef0-83ef-6f1617dd3f86" />




Besides browsing for the file (Browse), I will explain the four crucial settings among the blank fields and checkboxes that you must verify according to your situation, in order from top to bottom.

1. Append events? (Whether to keep existing events)
Unchecked (overwrite): Erases all existing event markers in the EEG data and completely overwrites them with the contents of the file you are currently loading.

Checked: Keeps the existing event markers as they are and appends the contents of the new file.

Tip: If the data already has events (like the sample data) and you just want to layer new information on top, it might be safer to check this box.

2. Input field (column) names (Most important!)
This is where you specify what data each column in the imported text file represents, in order.

As shown in the example on the right (Ex: type latency duration), simply write the names separated by spaces to match the data order in your file.

At this step, latency (occurrence time) must always be included for EEGLAB to grasp the timing.

3. Number of file header lines (Skipping header rows)
This field asks if the top row of the loaded text file contains a 'Header' (titles) rather than actual data.

If there is text like 'Time' or 'Event Type' in the top row (much like an Excel file), the machine might mistake it for numbers and throw an error.

In such cases, entering the number 1 commands the system to "skip the first row because it's a title." If the file is full of raw data without any headers, you can leave it at the default value of 0.

4. Time unit (sec)
This tells the system what time unit the latency numbers in the text file are using. You can get a hint from the blue text example on the right.



    1: When the unit is in Seconds (e.g., 1.5 seconds).
    
    1E-3: When the unit is in Milliseconds (e.g., 1500ms).
    
    NaN: When it is recorded not in time units, but as sequential 'Data points/Frames' of the EEG data.

Once I have adjusted these four settings to match the format of your prepared text file, click the Ok button at the bottom right of the window. <- this should be happen, however, there is error going on; Since I use the eeglab datasets, might be blocker regarding this.




<img width="1602" height="1094" alt="Screenshot 2026-05-05 at 5 43 42 pm" src="https://github.com/user-attachments/assets/b4676e4f-701f-4414-a828-da75cf68666d" />




The event types in this sample dataset are 

1. Square
2. RT




{Using EEG functions and plugin}


<img width="864" height="1024" alt="Screenshot 2026-05-05 at 5 26 21 pm" src="https://github.com/user-attachments/assets/7b788e4f-069d-4875-b15c-ef3601c8bee3" />


1. General Data & Basic Formats
  
   ASCII/float file or MATLAB array: Simple text file that can open in Excel file (e.g., .txt or .csv) containging sequences of numbers

   Biosemi BDF file (BIOSIG Plugin): standard medical/research formats, research EEG device called 'Biosemi'

   EDF/EDF+/GDF files: EDF (European Data Format), global standard format for pilysomnography and clinical EEGs. (most of the hospital equipment devices)

2. Specific Equipment Manufacturer Formats
The options below are proprietary formats created by individual EEG equipment manufacturers specifically for their machines.

    ANT EEProbe (.CNT / .AVR file): Files extracted from 'ANT Neuro' equipment.

    From BIDS(Brain Imaging Data Structure) folder structure: not a specific file, a folder organisation rule - international standard for naming folders and files to share research data. 

 This menu is used to load an entire folder organized according to these rules at once.

From Brain Vis. Rec. (.vhdr / .ahdr file) / Matlab file: The format for 'Brain Products (BrainVision)', a highly popular research EEG device. Typically, three files move together as a set: data (.eeg), header (.vhdr), and marker (.vmrk).

From Netstation (binary / Multiple seg. / Matlab): The format for the 'Net Station' program created by 'EGI (now Magstim)'. You will frequently see this when using high-density EEG caps (resembling hairnets) with 128 or 256 electrodes.

From Muse Direct / Monitor App .CSV file: Files extracted from 'Muse', a consumer-grade meditation and sleep EEG headband (available for general purchase), and its smartphone app.

From Neuroscan (.CNT / .EEG file): The format of 'Compumedics Neuroscan', a historic and highly renowned EEG equipment brand.

From Snapmaster .SMA file: The format for Snapmaster, one of the early PC-based EEG data collection programs.

From .XDF or .XDFZ file: A general-purpose Extensible Data Format. It is primarily used when synchronizing and recording data from multiple devices simultaneously during an experiment, such as EEG, eye-trackers, and mouse movements.

Import Magstim/EGI .mff file: A relatively modern format for the aforementioned EGI Net Station equipment.

