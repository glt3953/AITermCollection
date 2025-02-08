# Colab 上运行 DeepSeek_R1
https://colab.research.google.com/drive/1fLWACoAnOeD1aMY8S6z9K8HK_8RAyEAB#scrollTo=cgMuhmNZVsLU
https://blog.csdn.net/m0_47426354/article/details/144961256
## 注册 Colab 和 ngrok
https://dashboard.ngrok.com/
## 安装Ollama
```
!curl -fsSL https://ollama.com/install.sh | sh
```
## 安装python库和导入库
```
!pip install aiohttp pyngrok

import os
import asyncio

# 设置 GPU 库，让Ollma能够使用GPU进行推理
os.environ.update({'LD_LIBRARY_PATH':'/usr/lib64-nvidia'})

async def run_process(cmd):
  print('>>> starting', *cmd)
  p = await asyncio.subprocess.create_subprocess_exec(
      *cmd,
      stdout=asyncio.subprocess.PIPE,
      stderr=asyncio.subprocess.PIPE,
  )

  async def pipe(lines):
    async for line in lines:
      print(line.strip().decode('utf-8'))

  await asyncio.gather(
      pipe(p.stdout),
      pipe(p.stderr),
  )

#注册一个 ngrok 账户，获取Authtoken，替换下面的 ngrok-authtoken
await asyncio.gather(
    run_process(['ngrok', 'config', 'add-authtoken','<ngrok-authtoken>'])
)

await asyncio.gather(
    run_process(['ollama', 'serve']),
    run_process(['ngrok', 'http', '11434', '--host-header', 'localhost:11434'])
)
```
看到 starting ngrok http 11434 --host-header localhost:11434 等日志，表示部署成功，在 ngrok 官网 endpoints 查看公网URL，点击 URL->view site，显示 Ollama is running，表示代理成功
## 在本地修改 OLLAMA_HOST 环境变量为刚才的公网URL
```
export OLLAMA_HOST="https://1906-34-16-181-192.ngrok-free.app"
```
## 在本地客户端输入 ollama 的命令会在 colab 上执行
```
ollama run deepseek-r1:14b
```

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
