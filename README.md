# Morse_GUI_2

import tkinter as tk
import time
from gpiozero import LED
import RPi.GPIO

RPi.GPIO.setmode(RPi.GPIO.BCM)

led = LED(14)

morse_code = {' ': '_', 
	"'": '.----.', 
	'(': '-.--.-', 
	')': '-.--.-', 
	',': '--..--', 
	'-': '-....-', 
	'.': '.-.-.-', 
	'/': '-..-.', 
	'0': '-----', 
	'1': '.----', 
	'2': '..---', 
	'3': '...--', 
	'4': '....-', 
	'5': '.....', 
	'6': '-....', 
	'7': '--...', 
	'8': '---..', 
	'9': '----.', 
	':': '---...', 
	';': '-.-.-.', 
	'?': '..--..', 
	'A': '.-', 
	'B': '-...', 
	'C': '-.-.', 
	'D': '-..', 
	'E': '.', 
	'F': '..-.', 
	'G': '--.', 
	'H': '....', 
	'I': '..', 
	'J': '.---', 
	'K': '-.-', 
	'L': '.-..', 
	'M': '--', 
	'N': '-.', 
	'O': '---', 
	'P': '.--.', 
	'Q': '--.-', 
	'R': '.-.', 
	'S': '...', 
	'T': '-', 
	'U': '..-', 
	'V': '...-', 
	'W': '.--', 
	'X': '-..-', 
	'Y': '-.--', 
	'Z': '--..', 
	'_': '..--.-'}
 
def translateToMorse(word):
    word = word.upper()
    morse_code_word = ""
    for character in word:
        morse_code_word += morse_code[character] + " " 
    return morse_code_word

def clickMe():
    Name = name.get()
    wordLed = translateToMorse(Name)
    for char in wordLed:
        if char == '-':
            led.on()
            time.sleep(3)
            led.off()
            time.sleep(1)
        elif char == '.':
            led.on()
            time.sleep(1)
            led.off()
            time.sleep(1)
        elif char == ' ':
            led.off()
            time.sleep(3)
        else:
            break
    
def Exit():
    RPi.GPIO.cleanup()
    window.destroy()
    
 
window = tk.Tk()
window.title("GUI morse code")
window.minsize(600,400)

label = tk.Label(window, text = "Enter Your Name")
label.grid(column = 0, row = 0)

name = tk.StringVar()
nameEntered = tk.Entry(window, width = 15, textvariable = name)
nameEntered.grid(column = 0, row = 1)

goButton = tk.Button(window, text = "Blink Morse", command = clickMe)
goButton.grid(column= 0, row = 2)

exitButton = tk.Button(window, text = "Exit", command = Exit)
exitButton.grid(column= 0, row = 3)
window.mainloop()
