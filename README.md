# llama3-finetuning-unsloth
本项目采用了unsloth的Llama3微调框架，并使用自制的微调用数据集，对Llama3进行微调。通过这些微调，使得Llama3能够模拟特定小说、电影或游戏中的某个角色的语气和性格特点，与使用者进行交流。

## Try it now
我已将我训练出来的模型upload到github上了，下载Paimon-unsloth.Q4_K_M.gguf，并使用类似于chat4All或者Ollama的platform便能在local直接使用此微调的llama3模型。我使用了原神里的派蒙文本作为此模型的训练集，并且加入了一些规范化的AI问答和一些使用派蒙语气的AI问答（称之为mutation）来训练特化的派蒙AI模型，此模型在微调之后可以使用派蒙的语气和性格特点来和使用者做出一些简单的交互，在未来，希望能够通过拓展数据集来做出更多高级的交互。

## 相关项目
unsloth：https://github.com/unslothai/unsloth  
gpt4all：https://gpt4all.io/  
triton：https://github.com/openai/triton  
llama.cpp：https://github.com/ggerganov/llama.cpp  

## 使用Google Colab微调Llama3
## Installation
1、使用unsloth的fine tuning框架微调模型  
具体code参考这个链接：https://colab.research.google.com/drive/1RwPqpLXfrt85QQ8dXl5cS5EJzycOwWDu?usp=sharing  
我已将权限设为有link就能访问  

2、准备数据集  
需要自己自备想训练的人物对话数据集，人物语气特化数据集，规范化的AI数据集可以直接下载standardConversation.json。  
如果嫌麻烦，可以直接用我整合好的派蒙数据集进行训练，我已将这个数据集upload到了Huggingface上：https://huggingface.co/uITimeCia/Paimon  
我已经训练好的《原神》派蒙的gguf file也已经post到Huggingface上了:https://huggingface.co/uITimeCia/Paimon  

3、使用之前的unsloth框架来训练微调模型，具体的code我已经将customized parameter cooment了，请直接参考我的code来进行训练。  

## 本地微调Llama3
## Windows本地部署条件
1、Windows10/Windows11  
2、英伟达卡8G显存、16G内存，安装CUDA12.1、cuDNN8.9，C盘剩余空间20GB、unsloth安装盘S40GB  
3、依赖软件：CUDA12.1+cuDNN8.9、Python11.9、Git、Visual Studio 2022、llvm(可选）  
4、HuggingFace账号，上传训练数据集  

## Windows部署步骤
一、下载安装包  
1、安装cuda12.1，配置cuDNN8.9  
2、安装Visual Studio 2022  
3、解压unsloth  
4、安装python11  
5、安装git  

二、安装unsloth  
1、安装依赖包  
pip install torch==2.2.2 --index-url https://download.pytorch.org/whl/cu121  
pip install "unsloth[colab-new] @ git+https://github.com/unslothai/unsloth.git"  
pip install --no-deps trl peft accelerate bitsandbytes  
pip install deepspeed-0.13.1+unknown-py3-none-any.whl  
pip install  triton-2.1.0-cp311-cp311-win_amd64.whl  
pip install xformers

2、测试安装是否成功  
nvcc  --version  
python -m xformers.info  
python -m bitsandbytes

3、运行脚本  
test-unlora.py   测试微调之前推理  
fine-tuning.py   用数据集微调  
test-lora.py   测试微调之后推理  
save-16bit.py  合并保存模型16位  
save-gguf-4bit.py  4位量化gguf格式  

三、4位量化需要安装llama.cpp，步骤如下：  
1、git clone https://github.com/ggerganov/llama.cpp  

2、按官方文档编译  
mkdir build  
cd build  
cmake .. -DLLAMA_CUBLAS=ON  

3、设置Visual Studio 2022中cmake路径到系统环境变量path里  
C:\Program Files\Microsoft Visual Studio\2022\Professional\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin  
C:\Program Files\Microsoft Visual Studio\2022\Professional  

4、编译llama.cpp  
cmake --build . --config Release  

5、如果上面这句编译命令无法执行，需要做以下操作：  
复制这个路径下的  
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.1\extras\visual_studio_integration\MSBuildExtensions  
4个文件，粘贴到以下目录里  
C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\MSBuild\Microsoft\VC\v170\BuildCustomizations  

6、编译好以后，把llama.cpp\build\bing\release目录下的所有文件复制到llama.cpp目录下  

7、重新运行fine-tuning.py微调并保存  

