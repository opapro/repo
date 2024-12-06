import streamlit as st
import pandas as pd
from io import StringIO
import whisper

# Initialize the Whisper model (make sure to load the model you need)
model = whisper.load_model("base")  # You can choose "small", "medium", "large", etc.

# File uploader widget
uploaded_file = st.file_uploader("Upload a CSV file or an audio file", type=['csv', 'mp3', 'wav', 'opus'])

if uploaded_file is not None:
    # Check the file type
    if uploaded_file.type == "text/csv":
        # Read the file as bytes
        bytes_data = uploaded_file.getvalue()
        st.write("File bytes:", bytes_data)

        # Convert to a string-based IO
        stringio = StringIO(uploaded_file.getvalue().decode("utf-8"))
        st.write("StringIO object:", stringio)

        # Read file as string
        string_data = stringio.read()
        st.write("String data:", string_data)

        # Read the CSV file into a DataFrame
        dataframe = pd.read_csv(uploaded_file)
        st.write("DataFrame:", dataframe)

    elif uploaded_file.type in ["audio/mpeg", "audio/wav"]:
        # If the uploaded file is an audio file, process it with Whisper
        audio_bytes = uploaded_file.read()
        st.audio(audio_bytes, format='audio/wav')  # Display audio player

        # Save the audio file temporarily
        with open("temp_audio.wav", "wb") as f:
            f.write(audio_bytes)

        # Transcribe the audio using Whisper
        transcription = model.transcribe("temp_audio.wav")
        st.write("Transcription:", transcription['text'])

        # Optionally, you can delete the temporary file after processing
        import os
        os.remove("temp_audio.wav")

