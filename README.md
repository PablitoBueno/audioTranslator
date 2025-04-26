
# AudioTranslator

## Description
**AudioTranslator** is a Python script that converts English audio files into text and automatically translates the text into Portuguese using Meta's NLLB-200 model.

## Requirements
- Python 3.7+  
- Internet connection  
- Libraries: `SpeechRecognition`, `pydub`, `transformers`, `sentencepiece`, `torch`

## Installation
```bash
pip install SpeechRecognition pydub transformers sentencepiece torch
```

## Usage
1. **Upload an audio file (.mp3, .wav, etc.)**  
   The script will automatically convert it to `.wav` if needed.

2. **Transcription with Google Speech Recognition**
   ```python
   with sr.AudioFile(audio_wav) as source:
       audio_data = r.record(source)
   texto_en = r.recognize_google(audio_data, language="en-US")
   ```

3. **Translation with NLLB-200**
   ```python
   tokenizer = AutoTokenizer.from_pretrained("facebook/nllb-200-distilled-600M")
   model = AutoModelForSeq2SeqLM.from_pretrained("facebook/nllb-200-distilled-600M")
   inputs = tokenizer(texto_en, return_tensors="pt")
   inputs["forced_bos_token_id"] = tokenizer.convert_tokens_to_ids("por_Latn")
   translated = model.generate(**inputs)
   print(tokenizer.decode(translated[0], skip_special_tokens=True))
   ```

## Structure
- `convert_to_wav`: converts audio files to `.wav` if needed  
- `speech_recognition`: transcribes English audio  
- `transformers`: translates text into Portuguese via Meta’s model  

Designed for quick use on Google Colab or locally.
