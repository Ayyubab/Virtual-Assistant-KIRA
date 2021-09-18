# Virtual-Assistant-KIRA
#This is an prefunctioned virtual assistant. I made this in my school at the age of 16yrs. Have fun whit it and don't forget to do the necessary changes in code as given.
#dont forget to add double slash(//) when pasting file location.

#Code starts here.
#modules
import pyttsx3  # pip install pyttsx3
import speech_recognition as sr  # pip install speechRecognition
import datetime
import wikipedia  # pip install wikipedia
import webbrowser
import os
import pywhatkit
import subprocess
import random
import pyfirmata

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
# print(voices[1].id)
engine.setProperty('voice', voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour >= 0 and hour < 12:
        speak("Good Morning!")

    elif hour >= 12 and hour < 18:
        speak("Good Afternoon!")

    else:
        speak("Good Evening!")

    speak("I am Kira. How may I help you")


def takeCommand():
    # It takes microphone input from the user and returns string output

    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print(f"User said: {query}\n")

    except Exception as e:
        # print(e)
        speak("Say that again please...")
        print("Say that again please...")
        return "None"
    return query


if __name__ == "__main__":
    wishMe()
    while True:
        # if 1:
        query = takeCommand().lower()

        # Logic for executing tasks based on query
        if 'wikipedia' in query:
            speak('Searching Wikipedia...')
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=2)
            speak("According to Wikipedia")
            print(results)
            speak(results)

        elif 'open youtube' in query:
            speak('Opening YouTube...')
            webbrowser.open("youtube.com")

        elif 'open google' in query:
            speak('What should i search on google?')
            order = takeCommand()
            order = order.replace('search','')
            if "just" in order:
                speak('As you wish sir')
                webbrowser.open("google.com")
            else:
                pywhatkit.search(order)
                speak('This is what I found.')

        elif 'open rainy mood' in query:
            speak("Opening rainymood...")
            webbrowser.open("rainymood.com")


        elif 'play music' in query:
            music_dir = 'paste//your//music folder//location' #just paste your music folder location dont add song name. just folder.also dont forget to add double slash(//).
            songs = os.listdir(music_dir)
            test_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
            ran = random.choice(test_list)
            os.startfile(os.path.join(music_dir, songs[ran]))

        elif 'change the song' in query:
            new_ran = random.choice(test_list)
            os.startfile(os.path.join(music_dir, songs[new_ran])) #dont change this.

        elif 'time' in query:
            strTime = datetime.datetime.now().strftime("%I:%M %p") #dont change this.
            speak(f"Sir, the time is {strTime}")

        elif 'open code' in query:
            codePath = "paste//your//visual code//path here//Code.exe"
            os.startfile(codePath)

        elif 'mail to bhai' in query:
            speak("What should be the subject?")
            subject = takeCommand()
            if "just" in subject or "leave" in subject:
                subject = ""
            else:
                subject = subject
            speak("What should I say to bhai")
            content = takeCommand()
            pywhatkit.send_mail('Your gmail id', 'Your password', subject, content, 'receiver's mail id')
            speak("Email has been sent!")

        elif 'mail to papa' in query:
            speak("What should I say?")
            content = takeCommand()
            pywhatkit.send_mail('Your gmail id', 'Your password', '', content, 'receiver's mail id')
            speak("Email has been sent!")

        elif 'mail to TP' in query:
            speak("What should I say?")
            content = takeCommand()
            pywhatkit.send_mail('Your gmail id', 'Your password', '', content, 'receiver's mail id')
            speak("Email has been sent!")


        elif "play" in query:
            music = query.replace("Kira", "") #with this you can play videos and music on youtube.
            music = query.replace("play", "")
            speak("Playing" + music)
            pywhatkit.playonyt(music)

        elif "who are you" in query:
            speak("Hi I am _your name_ Assistant Kira. I am an A.I. I can do a lot of stuffs.")

        elif "what can you do" in query:
            speak(
                "I was programmed to Assist _Your name_ in his work. I can play videos and songs for you on youtube. Also much more thing which _Your name_ asks me to do. Better you ask _Your name_ what am i capable of.")

        elif "cmd" in query:
            speak('Opening cmd...')
            subprocess.call("cmd.exe") #dont change this.

        elif "calculator" in query:
            speak('Opening Calculator...') #dont change this.
            subprocess.run("calc.exe")

        elif "brave" in query:
            speak('Opening Brave browser...')
            subprocess.call("paste//your//software//destion//here//brave.exe")

        elif "telegram" in query:
            speak('Opening Telegram...')
            subprocess.call("paste//your//software//destion//here//Telegram.exe")

        elif "chrome" in query:
            speak('Opening Chrome...')
            subprocess.call("paste//your//software//destion//here//chrome.exe") #You can add more apps just like this and give the original file dir.

        elif "whatsapp message" in query:
            query = query.replace("kira", "")
            query = query.replace("send", "")
            query = query.replace("a", "")
            query = query.replace("whatsapp", "")
            query = query.replace("message", "")
            query = query.replace("to", "")
            name = query
            if "bhai" in name:
                speak(f"What's the message for {name}")
                m = takeCommand()
                pywhatkit.sendwhatmsg_instantly(phone_no='phone no. with country code', message=m, wait_time=10, tab_close=False,
                                                close_time=6) #Add your friends phone no. with country code where requested.

            elif "Hari Puttar" in name:
                speak(f"What's the message for {name}")
                m = takeCommand()
                pywhatkit.sendwhatmsg_instantly(phone_no='phone no. with country code', message=m, wait_time=10, tab_close=False,
                                                close_time=6) #Add your friends phone no. with country code where requested.

        elif "search" in query:
            query = query.replace("search", "")
            speak("searching" + query)
            pywhatkit.search(query)

        elif "mail" in query:
            speak("Whom should I send mail?")
            whom = takeCommand()
            whom = whom.replace("@gamil.com", "")
            whom = whom.replace(" ", "")
            speak("what should be the subject?")
            sub = takeCommand()
            if "just" in sub or "leave" in sub:
                sub = ""
            else:
                sub = sub
            speak("What should I say?")
            mess = takeCommand()
            pywhatkit.send_mail('Your mail id', 'your password', sub, mess, whom + "@gmail.com") #add your gmail id and password to send mail through your account.

        # basic functions

        # exit code

        elif "exit" in query: #whit this KIRA with go to sleep.
            speak("Ok sir")
            exit()

        elif "quit" in query:
            speak("Ok sir")
            exit()

        # shutdown code

        elif "shut down" in query:
            speak("Are u sure you want to shutdown?")
            shut = takeCommand()
            if "yes" in shut:
                os.system("shutdown /s /t 1")
            elif "no" in shut:
                exit()
