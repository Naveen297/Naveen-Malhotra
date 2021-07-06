# Naveen-Malhotra
<!-- Jack My Personal AI (Code for both Mac And Windows)
THIS PROGRAMMING IS DONE IN PYTHON LANGUAGE -->
import pyttsx3
import speech_recognition as sr
import datetime
import pyaudio
import webbrowser
import wikipedia
import os
import os.path
import selenium
import smtplib
import pyjokes
import json
import requests
import urlopen
import playsound
engine = pyttsx3.init()#this will takes the inbuilt voices of the system.
voices = engine.getProperty('voices')#same as above
engine.setProperty('voice',voices[0].id)
#print(voices[0].id)#com.apple.speech.synthesis.voice.Alex.(ladke ki voice hai [0].id pe

def speak(audio):#this is the speak fuunction
    engine.say(audio)
    engine.runAndWait()
def wishme():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning!")
    elif hour>=12 and hour<18:
        speak("Good afternoon!")
    else:
        speak("Good Evening!")

    assname = ("Jack")
    speak("I am your Assistant Jack")
    speak("how may I help You?")

def takecommand():
    #it takes microfone input fron the user and returns string output
    r = sr.Recognizer()
    mic = sr.Microphone()
    with mic as source:
        r.adjust_for_ambient_noise(source)
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        print("Recognizing....")
        query = r.recognize_google(audio,language='en-in')
        print("user said:", query)
    except Exception as e:
        # print(e)
        print("Say that again please...")
        return "None"
    return query
def sendemail(to,content):
     server = smtplib.SMTP('smtp.gmail.com',587)
     server.ehlo()
     server.starttls()
     server.login('naveenmalhotra176@gmail.com','nonu@1212')
     server.sendmail('naveenmalhotra176@gmail.com',to,content)
     server.close()

if __name__ == "__main__" :

    wishme()
    while True:
        query = takecommand().lower()

        #logic for executing tasks based on query
        if 'wikipedia' in query:
            speak('Searching Wikipedia...')
            query = query.replace("wikipedia","")
            results = wikipedia.summary(query, sentences=2)
            print(results)
            speak(results)
        elif 'open youtube' in query:
            webbrowser.open('https://www.youtube.com/')
        elif 'open google' in query:
            webbrowser.open('https://www.google.in/')
        elif 'open spotify' in query:
            webbrowser.open('https://www.spotify.com/us/')
        elif 'open stackoverflow' in query:
            webbrowser.open('https://stackoverflow.com/')
        #play music ke liye abhi karna hai

        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"Hey the time is {strTime}")

        elif 'open Android Studio' in query:
            speak("opening Android studio please wait!")
            d = '/Applications'
            apps = list(map(lambda x: x.split('.app')[0], os.listdir(d)))
            app = 'Android Studio'
            os.system('open ' + d + '/%s.app' % app.replace(' ', '\ '))
        elif 'open Kindle' in query:
            speak("opening Kindle please wait!")
            d = '/Applications'
            apps = list(map(lambda x: x.split('.app')[0], os.listdir(d)))
            app = 'Kindle'
            os.system('open ' + d + '/%s.app' % app.replace(' ', '\ '))
        elif 'open telegram' in query:
            speak("opening telegram please wait!")
            d = '/Applications'
            apps = list(map(lambda x: x.split('.app')[0], os.listdir(d)))
            app = 'Telegram'
            os.system('open ' + d + '/%s.app' % app.replace(' ', '\ '))
        elif 'open pycharm' in query:
            speak("opening pycharm please wait!")
            d = '/Applications'
            apps = list(map(lambda x: x.split('.app')[0], os.listdir(d)))
            app = 'PyCharm CE'
            os.system('open ' + d + '/%s.app' % app.replace(' ', '\ '))
        elif 'open music' in query:
            speak("opening Music please wait!")
            d = '/Applications'
            apps = list(map(lambda x: x.split('.app')[0], os.listdir(d)))
            app = 'YT Music'
            os.system('open ' + d + '/%s.app' % app.replace(' ', '\ '))
        elif 'email to naveen' in query:
            try:
                speak("what should i say?")
                content=takecommand()
                to = "naveenmalhotra148@gmail.com"
                sendemail(to,content)
                speak("Email has been sent!")
            except Exception as e:
                print(e)
                speak("Sorry your email has not send!")
        elif 'send a mail' in query:
            try:
                speak("What should I say?")
                content = takecommand()
                speak("whome should i send")
                to = input("enter mail -> ")
                sendEmail(to, content)
                speak("Email has been sent !")
            except Exception as e:
                print(e)
                speak("I am not able to send this email")
        elif 'how are you' in query:
            speak("I am fine, Thank you")
            speak("How are you, Sir")

        elif 'fine' in query or "good" in query:
            speak("It's good to know that your fine")
        elif "I want to change your name" in query:
            speak("What would you like to call me, Sir ")
            assname = takecommand()
            speak("Thanks for naming me")
        elif "what's your name" in query or "What is your name" in query:
            print("My friends call me", assname)
            speak("My friends call me")
            speak(assname)

        elif "who made you" in query or "who created you" in query:
            speak("I have been created by Naveen.")
        elif 'joke' in query:
            speak(pyjokes.get_joke())
        elif 'play' in query:

            query = query.replace("search", "")
            query = query.replace("play", "")
            webbrowser.open(query)

        elif "who i am" in query:
            speak("If you talk then definitely you are a human.")

        elif "why you came to world" in query:
            speak("Thanks to Naveen. further It's a secret")
        elif 'is love' in query:
            speak("It is 7th sense that destroy all other senses")

        elif "who are you" in query:
            speak("I am your virtual assistant Jack created by Naveen")

        elif 'reason for you' in query:
            speak("I was created as a Minor project by Mister Naveen")
        elif 'search' in query:
            statement = query.replace("search", "")
            webbrowser.open(query)

        elif "where is" in query:
            query = query.replace("where is", "")
            location = query
            speak("User asked to Locate")
            speak(location)
            webbrowser.open("https://www.google.nl / maps / place/" + location + "")

        elif "write a note" in query:
            speak("What should i write, sir")
            note = takecommand()
            file = open('jack.txt', 'w')
            speak("Sir, Should i include date and time")
            snfm = takecommand()
            if 'yes' in snfm or 'sure' in snfm:
                strTime = datetime.datetime.now().strftime("% H:% M:% S")
                file.write(strTime)
                file.write(" :- ")
                file.write(note)
            else:
                file.write(note)
        elif "open note" in query:
            file = open('jack.txt')
            speak("the file contains")
            print(file.read)
        elif "read note " in query:
            file=open('jack.txt')
            speak("ok sir it says")
            print(file.read())
            speak(file.read())

        elif "will you be my gf" in query or "will you be my bf" in query:
            speak("I'm not sure about, may be you should give me some time")

        elif "how are you" in query:
            speak("I'm fine, glad you me that")

        elif "i love you" in query:
            speak("It's hard to understand")

        elif "jack" in query:
            wishme()
            speak("Jack is always there for you Sir!")
            speak("what should i do for you sir")
            speak(assname)
            # aritmatic operations are done by type castinbg the string into integers
        elif "please add" in query:
            speak("please say first number")
            a=takecommand()
            speak("please say second number")
            b=takecommand()
            print("The answere is ->",int(a)+int(b))
            speak("the answer is")
            c=str(int(a)+int(b))
            speak(c)
        elif "please suubtract" in query:
            speak("please say first number")
            a=takecommand()
            speak("please say second number")
            b=takecommand()
            print("The answere is ->",int(a)-int(b))
            speak("the answer is")
            c=str(int(a)-int(b))
            speak(c)
        elif "please multiply" in query:
            speak("please say first number")
            a=takecommand()
            speak("please say second number")
            b=takecommand()
            print("The answere is ->",int(a)*int(b))
            speak("the answer is")
            c=str(int(a)*int(b))
            speak(c)
        elif "please divide" in query:
            speak("please say first number")
            a=takecommand()
            speak("please say second number")
            b=takecommand()
            print("The answere is ->",int(a)/int(b))
            speak("the answer is")
            c=str(int(a)/int(b))
            speak(c)
        elif "who is" in query:
            speak('Searching Wikipedia...')
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=2)
            print(results)
            speak(results)
        elif 'news' in query:
            webbrowser.open('https://www.jagran.com/')
            speak("opening news")
        elif 'exit' in query:
            speak("Thanks for giving me your time")
            exit()
