# CamillaDSP-Building-a-Config-1-Measure-Drivers-with-REW
1. Measure drivers with REW and useg REW EQ to flatten the SPL creating IIR (PEQ) filters for each driver, then import the PEQs into CamillaDSP and measure the results.

###REW SPL measuring.

First I set the SPL to about 90db. This is a K-Horn and needs to breathe. This level is also good to find various room rattles and stop them before they interfere with the measurements.

***** Screengrab of REW Bass bin measurement.

![alt text](<Images/Dec 1 2 UL5 Blank 92db 20-500Hz.jpg>)
 Dec 1 2 UL5 Blank Bass 20-500Hz 92db.jpg

The red trace is the SPL and the peaks at 32Hz and 43Hz are room resonances. The peak at 140Hz is a design quirk of the folded horn.

This procedure is repeated for the mid and hi, altering the frequency sweep to 200-5,000 Hz for mid and 2,000 to 20,000 Hz for hi and unmuting the appropriate "destination" channel in the Mixer. In my setup with the Motu Ultralight Mk5, bass is destination 2 & 3, mid 4 & 5 and hi 6 & 7, even numbers are the Left channel, odd numbers are the Right channel. After changing the unmuted destination, don't forget to "Apply to DSP".
 


This graph shows the three drivers raw measurement at the same volume setting. The SPL difference is due to differing driver sensitivity and  different amplifiers. Easy to flatten in a DSP, good luck in a passive XO.
![alt text](<Images/Dec 1 Bass Mid Hi Raw.jpg>)


###A note about naming REW files.

First off, there will be a lot of measurement files. The file name for the Bass measurement above is Dec 1 2 UL5 Blank 92db 20-500Hz RAW.mdat, a descriptor (rather than just an identifier) containing the measurement session date, measurement number in the session, CamillaDSP config identifier and measurement settings.  I keep an A4 note book where I write out what the measuring session is trying to achieve and the variables I am testing - new filters, different XO cut offs, rePhase Phase Fixes etc. and make a note of each measurement so that the file from REW can be related to a particular measurement session.
I have a folder called REW Measurements where I keep measurements etc filed and retrieveable.
 

###Calculate EQ and save EQ filters.

In REW with the Bass measurement displayed, click the EQ tab to display the EQ function screen, I usually click the "Fit to Data" box (top of screen, 4 arrows) and then work down the Target Settings to set the Target Level (I normally click "Calculate target level from response", then in the Filter Tasks set the range leaving the Boost at default, and set the Flatness Target.
Then click the "Calculate target level from response" to generate the filters. Review the calculated filters, then click "Save filter settings to YAML file" and fill in the dialog popup where you can set the filter name. Again, the label is a descriptor showing the Bass measurement label and the filter task settings (Target Level, frequency spread and Flatness target) so that in later testing I can see what I was trying to do. REW will then popup a standard save file dialog tol save the EQ Filters for CamillaDSP in the correct format for Biquad filters.
This screengrab shows the REW EQ screen with filters calculated for the Bass measurement and the popup input of filter labels.
 

Here is the screengrab of the save filters
 

Here is a partial listing of the filters generated by REW
 
and the pipeline generated by REW
 
It is these filters that are imported to the config file in the Filters section of CamillaDSP.
and the Pipeline for Bass is also imported.
In the CamillaDSP GUI I select the Config file that I want to import the filters to. I have a Config based on Michaels template for a Motu Ultralight Mk 5 (UL5) that I will use. The config is contains a gain filter and a mixer. 
Select the File tab, and click the Import Config box - the screengrab shows the popup dialog with the mouse in the Import Config box, the Configs section shows the operating config with a green box around the star and the green tick indicates the config in the GUI. 
This screengrab shows the popup info with the mouse pointer in the CamillaDSP Config box. Having clicked Import Config we have a choice, we can select an existing config file or by clicking the CamillaDSP Config box we get a file selection screen.
 
Having clicked the CamillaDSP Config box, I select the EQ file output by REW.
 
and the filters and pipeline is displayed, click the button to select. Note the pipeline shows "0" which is the channel the filters will be assigned to and an "i" in a circle, hovering the mouse over the "i" will display the pipeline steps. After saving, the channel number should be changed. As I want these filters for left and right channels I will import them by clicking the "Import" box and then assign the pipeline to the left channel , then import only the pipeline steps by clicking the "tick" next to "Filters" which will change the "tick" to "-" , then assign the pipeline steps to the right channel. The red triangle "!" is warning that these filters already exist and will be overwritten.
 
Here is the Pipeline plot after the first import showing all the EQ filters for Channel 2.
 
After importing the pipeline steps a second time.
 


This process is repeated for Mid and High.
Here is a rather busy All SPL showing RAW, EQd with XO measurements for each driver.
 
RAW and EQd for Bass Mid Hi.jpg

Here is the pipeline showing each biquad.
 
T28 Biquads pipeline expanded.jpg

This shows the pipeline with biquads collapsed.
 
T28 Biquads pipeline collapsed.jpg
