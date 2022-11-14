# PSYCH 403 - Assignment 6 exercises: MPacificar

## Dialog box exercises
Use the PsychoPy help page on guis to customize your "exp_info" dialog box: psychopy.gui
1. Edit the dictionary "exp_info" so you have a variable called "session", with "1" preset as the session number.
2. Edit the "gender" variable in "exp_info" so the subject can write in whatever they want into an empty box, instead of the drop-down list
```
# setup the dictionary for the gui
exp_info = {    'subject_nr':0, 
                'age':0, 
                'handedness':('right','left','ambi'), 
                'gender':'',
                'session': 1}
print(exp_info)
```
Using DlgFromDict:
1. Customize my_dlg so that you have a title for your dialog box: "subject info".
2. Set the variable "session" as fixed. What happens?

- **Answer: The session variable cannot be edited (non-editable) by the participant if it's set to fixed**

3. Set the order of the variables as session, subject_nr, age, gender, handedness.
4. Once you have done all of the above, don't show "my_dlg" right away. Tell your experiment to print "All variables have been created! Now ready to show the dialog box!". Then, show the dialog box.
```
print("All variables have been created! Now ready to show the dialog box!") 

my_dlg = gui.DlgFromDict(dictionary = exp_info,
                        title = 'subject info',
                        fixed = ['session'],
                        order = ['session','subject_nr','age','gender','handedness'])
```
Fill in the following pseudocode with the real code you have learned so far:
```
#=====================
#COLLECT PARTICIPANT INFO
#=====================
from psychopy import gui, core, 
from datetime import datetime
import os

#-create a dialogue box that will collect current participant number, age, gender, handedness
# setup the dictionary for the gui:
exp_info = {    'subject_nr':0, 
                'age':0, 
                'handedness':('right','left','ambi'), 
                'gender':'',
                'session': 1}
print(exp_info)

print("All variables have been created! Now ready to show the dialog box!")
# participant info dialog box customization:
my_dlg = gui.DlgFromDict(dictionary = exp_info,
                        title = 'subject info',
                        fixed = ['session'],
                        order = ['session','subject_nr','age','gender','handedness'])

# make sure subject data is entered correctly
if exp_info['subject_nr'] == 0: #nothing entered
    # error message dialog box:
    err_dlg = gui.Dlg(title='error message') #give the dlg a title
    err_dlg.addText('Enter a valid subject number!') #create an error message
    err_dlg.show() #show the dlg
    core.quit() #quit the experiment
    
# make sure subject can consent to taking part in the experiment
if exp_info['age'] < 18:
    # error message dialog box:
    err_dlg = gui.Dlg(title='error message')
    err_dlg.addText('%d year olds cannot give consent!' % (exp_info['age']))
    err_dlg.show()
    core.quit()
    
# get date and time
date = datetime.now()
print(date)
exp_info['date'] = str(date.hour) + '-' + str(date.day) + '-' + str(date.month) + '-' + str(date.year)
print(exp_info['date'])

#-create a unique filename for the data
filename =  str(exp_info['subject_nr']) + '_' + exp_info['date'] + '.csv'
print(filename)

main_dir = os.getcwd() 
sub_dir = os.path.join(main_dir,'sub_info',filename)
```

## Monitor and window exercises

Look at the psychopy help page on "window" to help solve the exercises:
1. How does changing "units" affect how you define your window size?
- **Answer:**
3. How does changing colorSpace affect how you define the color of your window? Can you define colors by name?
- **Answer:**

Fill in the following pseudocode with the real code you have learned so far:
```
#=====================
#CREATION OF WINDOW AND STIMULI
#=====================
from psychopy import visual, monitors

#-define the monitor settings using psychopy functions
mon = monitors.Monitor('myMonitor', width=38.3, distance=60) 
mon.setSizePix([1920,1080])
mon.save()

#-define the window (size, color, units, fullscreen mode) using psychopy functions
win = visual.Window(monitor=mon, size=(400,400), color=[-1,-1,-1], units='pix', fullscr=True)
```

## Stimulus exercises
Check the psychopy help page on "ImageStim" to help you solve these exercises:
1. Write a short script that shows different face images from the image directory at 400x400 pixels in size. What does this do to the images? How can you keep the proper image dimensions and still change the size?
2. Write a short script that makes one image appear at a time, each in a different quadrant of your screen (put the window in fullscreen mode). Think about how you can calculate window locations without using a trial-and-error method.
3. Create a fixation cross stimulus (hint:text stimulus).

Fill in the following pseudocode with the real code you have learned so far:
```
#=====================
#CREATION OF WINDOW AND STIMULI
#=====================
#-define experiment start text unsing psychopy functions
#-define block (start)/end text using psychopy functions
#-define stimuli using psychopy functions (images, fixation cross)

#=====================
#START EXPERIMENT
#=====================
#-present start message text
#-allow participant to begin experiment with button press

#=====================
#BLOCK SEQUENCE
#=====================
#-for loop for nBlocks
    #-present block start message
    #-randomize order of trials here
    
    #=====================
    #TRIAL SEQUENCE
    #=====================    
    #-for loop for nTrials
        #-set stimuli and stimulus properties for the current trial
        
        #=====================
        #START TRIAL
        #=====================  
        #-draw fixation
        #-flip window
        #-wait time (stimulus duration)
        
        #-draw image
        #-flip window
        #-wait time (stimulus duration)
        
        #-draw end trial text
        #-flip window
        #-wait time (stimulus duration)
        
#======================
# END OF EXPERIMENT
#======================        
#-close window
```