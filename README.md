 <H3>PAVITHRAN S</H3>
<H3>212223240113</H3>
<H3>EX. NO.8</H3>
<H3>DATE:25.10.2025</H3>
<H1 ALIGN =CENTER>Implementation of Speech Recognition</H1>
<H3>Aim:</H3> 
 To implement the conversion of live speech to text.<BR>
<h3>Algorithm:</h3>
Step 1: Import the speech_recognition library<Br>
Step 2: Initialize the Recognizer<Br>
Step 3: Create an instance of the Recognizer class, which will be used for recognizing speech.<Br>
Step 4: Set the duration for audio capture<Br>
Step 5: Define a variable to specify the duration (in seconds) for which the program will capture audio from the microphone.<Br>
Step 6: Display a message in the console to prompt the user to speak.<Br>
Step 7: Capture audio from the default microphone<Br>
Step 9: Use the default microphone as the audio source.<Br>
Step 10: Record audio for the specified duration using the Recognizer instance.<Br>
Step 11: Perform speech recognition with exceptional handling:<Br>
•	Attempt to recognize speech from the captured audio using the Google Speech Recognition service.<Br>
•	If successful, print the recognized text.<Br>
•	Handle specific exceptions: If the recognition result is unknown or if there is an issue with the request to the Google Speech Recognition service, print corresponding error messages.<Br>
•	A generic exception block captures any other unexpected errors.<Br>
<H3>Program:</H3>

```
import sounddevice as sd
import numpy as np
import speech_recognition as sr

fs = 16000  # Sample rate
recognizer = sr.Recognizer()

def recognize_chunk(duration=1):
    """Record a short chunk and return recognized text."""
    print("Listening...")
    audio_data = sd.rec(int(duration * fs), samplerate=fs, channels=1, dtype='int16')
    sd.wait()
    audio = sr.AudioData(np.squeeze(audio_data).tobytes(), fs, 2)
    try:
        text = recognizer.recognize_google(audio)
        return text.lower()
    except sr.UnknownValueError:
        return ""
    except sr.RequestError as e:
        print("Google Speech Recognition error:", e)
        return ""

def main():
    print("🛠️ Speech Recognition ready! Say 'stop' to exit.\n")
    while True:
        text = recognize_chunk(duration=1)  # 1 second chunks
        if text:
            print("You said:", text)
            if "stop" in text or "close" in text or "exit" in text:
                print("Exiting program. Bye!")
                break

if __name__ == "__main__":
    main()
```

<H3> Output:</H3>
<img width="1916" height="1017" alt="image" src="https://github.com/user-attachments/assets/a799d036-61cc-4413-826a-c0d942d7ac29" />


<H3> Result:</H3>
Thus, speech recognition has been successfully executed
