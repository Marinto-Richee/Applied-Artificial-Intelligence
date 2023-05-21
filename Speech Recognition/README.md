# Implementation of Speech Recognition

## Aim:
 Construct a python program to implement speech recognition.
## EQUIPMENTS REQUIRED:
Hardware – PCs
Anaconda – Python 3.7 Installation / Google Colab /Jupiter Notebook
## Algorithm:
Step 1:Import the speech_recognition module as sr.<br>
Step 2:Assign a string variable "file" with the name of the audio file that you want to transcribe.<br>
Step 3:Create an instance of the Recognizer class called "r".<br>
Step 4:Use the AudioFile() method of sr to create an AudioFile object with the audio file name passed as an argument.<br>
Step 5:Use the record() method of r to read the audio data from the AudioFile object and store it in the variable "audio".<br>
Step 6:Use the recognize_google() method of r to transcribe the audio data stored in the "audio" variable.<br>
Step 7:Print the transcribed text on the console if the transcribe process was successful.<br>
Step 8:Handle any potential errors during the transcribing process. If the audio is not clear, print "not clear". If there's an error while trying to retrieve the transcribed text from the Google speech recognizer, print "Couldnt get results from google speech recognizer".<br>

## Program:
```python3
import speech_recognition as sr

# Assign a string variable "file" with the name of the audio file that you want to transcribe.
file = "audio.wav"

# Create an instance of the Recognizer class called "r".
r = sr.Recognizer()

# Use the AudioFile() method of sr to create an AudioFile object with the audio file name passed as an argument.
with sr.AudioFile(file) as source:
    audio = r.record(source)

# Use the recognize_google() method of r to transcribe the audio data stored in the "audio" variable.
try:
    text = r.recognize_google(audio)
except sr.UnknownValueError:
    print("Not clear")
except sr.RequestError as e:
    print("Couldn't get results from Google Speech Recognition service; {0}".format(e))

# Print the text in the next lines.
for line in text.splitlines():
    print(line)

```

## Output:
``what if somebody decides to break it be careful that you keep adequate coverage but look for places to save money baby it's taking longer to get things squared away than the bankers expected during the wife for once company may win her tax hated retirement income as helpful as our cost on the two naked bone when the title of this type of song is in question there's no dying or waxing or gassing needed maybe personalized leather hard place work on a flat surface and smooth out the simplest kind of separate system uses a single self-contained unit the old shop at it still holds a good mechanic is usually a bad boss both figures would go higher in later years doll houses at set``
## Result:
Hence , we have implemented a program that will transcribe the audio file in the file variable and print the transcribed text on the console, one line at a time.
