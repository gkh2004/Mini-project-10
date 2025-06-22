# Mini-project-10
PYTHON
!sudo apt install tesseract-ocr
!pip install pytesseract
!pip install gTTS
!pip install playsound
!pip install pygobject
from PIL import Image
import pytesseract
from gtts import gTTS
import os
from playsound import playsound

# -------- Step 1: Load and Extract Text from Image --------
image_path = "image.webp"  # Replace with your image path

# Optional: specify tesseract path if needed
# pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'

try:
    image = Image.open(image_path)
    extracted_text = pytesseract.image_to_string(image)
    print("Extracted Text:\n", extracted_text)

    if extracted_text.strip():
        # -------- Step 2: Convert Text to Speech --------
        tts = gTTS(text=extracted_text, lang='en')
        audio_path = "output_audio.mp3"
        tts.save(audio_path)

        # -------- Step 3: Play Audio --------
        print("Playing Audio...")
        playsound(audio_path)
    else:
        print("No readable text found in the image.")

except Exception as e:
    print("Error:", e)
