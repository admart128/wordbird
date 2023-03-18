# whisper-sandbox

This is just a sandbox for me to try out Whisper (https://openai.com/research/whisper).

Select an MP3 file and the program will run Whisper to transcribe the audio as text in the window.

Sample shown below is from YouTube video converted to MP3, source: https://www.youtube.com/watch?v=cZSdU6yYIdk&t=239s

~Adam Martinez
March 18, 2023

![sample image](Screenshot_2023-03-18_13-40-53.png)

```python
import whisper
import tkinter as tk
from tkinter import filedialog

window = tk.Tk()
window.title("whisper-sandbox")
window.geometry("750x750")

filename = ""

def select_file():
    file_path = filedialog.askopenfilename(
        initialdir="/", title="Select A File", filetypes=(("mp3 files", "*.mp3"),))
    model = whisper.load_model("tiny")
    result = model.transcribe(file_path)
    text = result["text"]
    output_text.delete('1.0', tk.END)
    output_text.insert(tk.END, text)

button = tk.Button(window, text="Select MP3 File", command=select_file)
button.pack()

output_text = tk.Text(window, height=40, width=80)
output_text.pack()

window.mainloop()
```