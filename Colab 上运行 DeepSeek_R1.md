# Colab 上运行 DeepSeek_R1
https://colab.research.google.com/drive/1fLWACoAnOeD1aMY8S6z9K8HK_8RAyEAB#scrollTo=R__jZhLwg6Mh
https://myapollo.com.tw/blog/google-colab-ollama/
https://blog.csdn.net/gitblog_00117/article/details/142275832
## 用 colab-xterm 在 Google Colab 上安裝 Ollama
```
!pip install colab-xterm
```
## 啟用 colab-xterm
```
%load_ext colabxterm
```
## 在 Colab 打開終端機(terminal)
```
%xterm
```
## 在終端機輸入 Ollama 安裝指令
```
curl -fsSL https://ollama.com/install.sh | sh
```
## 執行 Ollama
```
ollama serve &
```
## 运行 DeepSeek
```
ollama run deepseek-r1:32b
```
