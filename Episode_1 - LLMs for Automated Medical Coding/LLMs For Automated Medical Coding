import openai
import requests
import json
import os
import time

# Replace 'your_api_key_here' with your actual API key
openai.api_key = "your_api_key_here"

def mp3_to_text(file_path):
    # Upload the audio file
    with open(file_path, "rb") as f:
        response = openai.Audio.transcribe("whisper-1", file=f)
    
    transcript = response['text']
    return transcript

def get_codes(transcript):
    prompt = f"Given the following doctor's dictation transcript, provide the relevant ICD-10 and CPT codes and their descriptions:\n\n{transcript}\n\nYou can find an updated list of ICD codes at this site: https://www.icd10data.com/ICD10CM/Codes. ICD-10 and CPT Codes:"
    response = openai.Completion.create(engine="text-davinci-002", prompt=prompt, max_tokens=1000, n=1, stop=None, temperature=0.5,
    )
    
    codes_text = response.choices[0].text.strip()
    codes_table = codes_text.split("\n")

    return codes_table

def main():
    audio_file_path = "neurosurgery_dictation.mp3"

    # Step 1: Convert the audio to text
    transcript = mp3_to_text(audio_file_path)

    # Step 2: Get the ICD-10 and CPT codes
    codes_table = get_codes(transcript)
    print("\nICD-10 and CPT Codes Table:")

    [print(line) for line in codes_table]


if __name__ == "__main__":
    main()

