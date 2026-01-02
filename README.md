# Audio Compression: Handcrafted MP3 Codec

A comprehensive, low-level implementation of the **MP3 (ISO/IEC 11172-3 Layer III)** audio compression protocol. This project demonstrates a deep understanding of digital signal processing (DSP), psychoacoustic modeling, and entropy coding by building a functional encoder and decoder from the ground up.

## Project Overview
Developed for the **Multimedia Systems** course (9th Semester) at the Aristotle University of Thessaloniki. The project implements the complex pipeline required to reduce audio resolution without perceived quality loss, utilizing the human auditory system's limitations.

### Key Technical Components
* **Subband Filtering**: Analysis of the input signal into frequency subbands to isolate specific spectral components.
* **Modified Discrete Cosine Transform (MDCT)**: Implementation of `frameDCT` and `iframeDCT` routines for efficient time-frequency mapping.
* **Psychoacoustic Modeling**: Sophisticated analysis of the audio spectrum to identify "masked" frequencies. This allows for reduced quantization accuracy in areas where errors are imperceptible to the human ear.
* **Non-Uniform Quantization**: Controlled signal distortion based on the psychoacoustic threshold to optimize bit allocation.
* **Entropy Coding**: A two-stage lossless compression pipeline featuring:
    * **Run-Length Encoding (RLE)**: To compress sequences of zero-valued quantized coefficients.
    * **Huffman Coding**: For optimal bit-representation of the remaining signal data.

## Project Structure
* **`src/`**: The core engine of the codec.
    * `MP3_total_pipeline.py`: The final integrated `codec1`, `coder1`, and `decoder1`.
    * `psychoacousticUtils.py`: Implementation of the psychoacoustic model and masking thresholds.
    * `frameDCT.py`: Forward and inverse DCT transformations.
    * `huffman_utils.py` & `rle_utils.py`: Entropy encoding and decoding logic.
* **`scripts/`**: Demonstration scripts (`subband_filtering_demo.py`, `quantizer_demo.py`, etc.) that verify the mathematical correctness of each individual stage.
* **`data/`**: Storage for input `.wav` files.
* **`protocol_files/`**: Essential protocol coefficients and tables required for standard-compliant compression.
* **`report.pdf`**: Report of this project.

## How to Run
### Prerequisites
Install the required dependencies using the provided requirements file:
```bash
pip install -r requirements.txt
```
Running the Codec
The `MP3_codec_demo.py` script serves as the primary interface for the codec. It supports full loopback (codec), encoding only, or decoding only.

1. Full Codec (Encode then Decode):
```bash
python3 MP3_codec_demo.py --mode codec --sound_data ./data/myfile.wav --out_bitstream_path ./outputs/bitstream.bin --add_info_path ./outputs/add_info.npy --output_decoded_data ./outputs/final.wav
```
2. Encoder Only:
```bash
python3 MP3_codec_demo.py --mode encoder --sound_data ./data/myfile.wav --out_bitstream_path ./outputs/bitstream.bin --add_info_path ./outputs/add_info.npy
```
3. Decoder Only:
```bash
python3 MP3_codec_demo.py --mode decoder --sound_data ./data/myfile.wav --out_bitstream_path ./outputs/bitstream.bin --add_info_path ./outputs/add_info.npy --output_decoded_data ./outputs/final.wav
```
