# llama3-finetuning-unsloth

This project utilizes the unsloth framework for fine-tuning Llama3 and employs a custom fine-tuning dataset to enhance Llama3's ability to emulate the tone and personality traits of specific characters from novels, movies, or games, enabling it to interact with users.

### Try it Now

I have uploaded my trained model to GitHub. Download `Paimon-unsloth.Q4_K_M.gguf`, and you can use this fine-tuned Llama3 model locally with platforms like chat4All or Ollama. I used dialogues from the character Paimon from the game Genshin Impact as the training dataset. Additionally, I included some standardized AI Q&A and AI Q&A with Paimon's tone (referred to as mutation) to train a specialized Paimon AI model. After fine-tuning, this model can interact with users using Paimon's tone and personality traits. In the future, I hope to expand the dataset to enable more advanced interactions.

### Related Projects

- unsloth: https://github.com/unslothai/unsloth
- gpt4all: https://gpt4all.io/
- triton: https://github.com/openai/triton
- llama.cpp: https://github.com/ggerganov/llama.cpp

### Fine-tuning Llama3 using Google Colab

#### Installation

1. **Fine-tune the model using unsloth's framework**  
   Refer to this link for the specific code: https://colab.research.google.com/drive/1RwPqpLXfrt85QQ8dXl5cS5EJzycOwWDu?usp=sharing  
   The link is set to be accessible to anyone with the link.

2. **Prepare the Dataset**  
   You need to prepare your own dataset of character dialogues, tone-specific datasets, and standardized AI datasets, which can be directly downloaded from `standardConversation.json`.  
   If you prefer, you can use my integrated Paimon dataset for training. I have uploaded this dataset to Huggingface: https://huggingface.co/uITimeCia/Paimon  
   I have also posted the trained gguf file of Paimon from Genshin Impact on Huggingface: https://huggingface.co/uITimeCia/Paimon  

3. **Train the Model using unsloth's Framework**  
   Use the previous unsloth framework to fine-tune the model. I have customized the parameters in my code for reference.

### Local Fine-tuning of Llama3

#### Windows Local Deployment Requirements

1. Windows 10/Windows 11  
2. Nvidia GPU with 12GB VRAM, 16GB RAM, CUDA 12.1, cuDNN 8.9, 20GB free disk space, and 40GB space for unsloth installation  
3. Required software: CUDA 12.1 + cuDNN 8.9, Python 11.9, Git, Visual Studio 2022, LLVM (optional)  
4. HuggingFace account for uploading the training dataset  

#### Windows Deployment Steps

##### Download and Install Packages

1. Install CUDA 12.1 and configure cuDNN 8.9  
2. Install Visual Studio 2022  
3. Unzip unsloth  
4. Install Python 11  
5. Install Git  
6. Project Baidu Netdisk link: https://pan.baidu.com/s/1haVvMgo_ir7oFfWvU3kvVQ   
   Extraction code: rgs1   

##### Install unsloth

1. Install dependencies  
   ```sh
   pip install torch==2.2.2 --index-url https://download.pytorch.org/whl/cu121  
   pip install "unsloth[colab-new] @ git+https://github.com/unslothai/unsloth.git"  
   pip install --no-deps trl peft accelerate bitsandbytes  
   pip install deepspeed-0.13.1+unknown-py3-none-any.whl  
   pip install triton-2.1.0-cp311-cp311-win_amd64.whl  
   pip install xformers
2. Test the installation
   nvcc --version  
  python -m xformers.info  
  python -m bitsandbytes 
3.Run scripts
  test-unlora.py  # Test inference before fine-tuning  
  fine-tuning.py  # Fine-tune the model with the dataset  
  test-lora.py  # Test inference after fine-tuning  
  save-16bit.py  # Save the model in 16-bit format  
  save-gguf-4bit.py  # Quantize and save the model in 4-bit gguf format

### 4-bit Quantization with llama.cpp

1. Clone llama.cpp repository  
   ```sh
   git clone https://github.com/ggerganov/llama.cpp
2. Compile following the official documentation
   mkdir build  
   cd build  
   cmake .. -DLLAMA_CUBLAS=ON
3. Add CMake paths from Visual Studio 2022 to the system environment variable PATH
   C:\Program Files\Microsoft Visual Studio\2022\Professional\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin  
   C:\Program Files\Microsoft Visual Studio\2022\Professional
4.Compile llama.cpp
  cmake --build . --config Release  
