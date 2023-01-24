""" Virtual-assistant
An easy Python code for a virtual assistant.

Import modules"""

import pyttsx3
import speech_recognition as sr
import os
import webbrowser
import wikipedia
import pyjokes
import randfacts
import random
import requests 

# Engine

engine=pyttsx3.init("sapi5")
voices=engine.getProperty("voices")
engine.setProperty("voices",voices[1].id)

def speak(audio):
    engine.say(audio)
    print(audio)
    engine.runAndWait()

def takecommand():
    r=sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening....")
        r.pause_threshold=1
        audio=r.listen(source)
    
    try:
        print("Recognizing....")
        query=r.recognize_google(audio, language="en-in")
        print("You said:", query)
    except Exception as e:
        speak("Say that again please...")
        return "None"
    return query

# main

if __name__ == "__main__":
    speak("Hello, my name is Edith how may i help you?")
    while True:
        query=takecommand().lower()     
        if "google" in query:
            speak("What do you wnat to search in Google")
            c=takecommand()
            url="https://google.com/search?q="+c
            speak("Opening Google")
            webbrowser.get().open(url)

        elif "youtube" in query:
            url="https://youtube.com"
            speak("Opening Youtube")
            webbrowser.get().open(url)

        elif "spotify" in query:
            url="https://spotify.com"
            speak("Opening Spotify")
            webbrowser.get().open(url)

        elif "wikipedia" in query:
            speak("What do you want to search for?")
            a=takecommand()
            speak("Here is what i found.")
            speak(wikipedia.summary(a))
                
        elif "whatsapp" in query:
            speak("Opeing WhatsApp")
            url="https://web.whatsapp.com"
            webbrowser.get().open(url)

        elif "download pictures" in query:
            speak("What picture do you want to search for?")
            b=takecommand()
            speak("I found this on the internet")
            url="https://unsplash.com/s/photos/"+b
            webbrowser.get().open(url)
                
        elif "electronics" in query:
            speak("Opening Expansys")
            url="https://www.expansys.com.sg/"
            webbrowser.get().open(url)

        elif "shopee" in query:
            speak("Opening Shopee")
            webbrowser.get.open("https://shopee.sg")

        elif "amazon" in query:
            speak("Opening Amazon")
            webbrowser.get().open("https://amazon.sg")
        
        elif "lazada" in query:
            speak("Opeining Lazada")
            webbrowser.get().open("https://lazada.sg")
        
        elif "qoo10" in query:
            speak("Opening Qoo10")
            webbrowser.get().open("https://qoo10.sg")
        
        elif "carousell" in query:
            speak("Opeining Carousell")
            webbrowser.get().open("https://carousell.sg")
               
        elif "python" in query:
            speak("Opening Visual Studio Code")
            path=<Enter the path of visual studio code of youe computer in double inverted commas>
            os.startfile(path)
        
        elif "word" in query:
            speak("Opening Microsoft Word")
            path=<Enter the path of Microsoft word of your computer in double inverted commas>
            os.startfile(path)
        
        elif "store" in query:
            speak("Opeining Microsoft Store")
            path=<Enter the path of microsoft store of your computer in double inverted commas>
            os.startfile(path)

        elif "settings" in query:
            speak("Opening settings")
            path=<Enter the path of settings of your computer in double inverted commas>
            os.startfile(path)
        
        elif "zoom" in query:
            speak("Opening zoom")
            path=<Enter the path of zoom of your computer in double inverted commas>
            os.startfile(path)
        
        elif "chess" in query:
            speak("Opening Chess.com")
            url="https://www.chess.com/home"
            webbrowser.get().open(url)
        
        elif "discord" in query:
            speak("Opening Discord")
            url="https://discord.com/channels/@me"
            webbrowser.get().open(url)
        
        elif "joke" in query:
            speak(pyjokes.get_joke())
        
        elif "fact" in query:
            x=randfacts.get_fact()
            speak(x)

        elif "international news" in query:
            url="https://abcnews.go.com/International"
            speak("Opening ABC News")
            webbrowser.get().open(url)
        
        elif "local news" or "singapore news" in query:
            url="https://straitstimes.com"
            speak("Opening Straits Times")
            webbrowser.get().open(url)
        
        elif "weather" in query:
            speak("Please tell the city you want  me show the forecast of.")
            c=takecommand()
            speak("Displaying the weather forecast of ", c)
            url="https://wttr.in/{}".format(c)
            res=requests.get(url)
            print(res.text)
