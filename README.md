<div align="center">

<h1 align="center">ANXETY COLAB</h1>

English | [Русский ](./README-ru_RU.md)

</div>

<p align="center">
  <a href="https://colab.research.google.com/drive/1wEa-tS10h4LlDykd87TF5zzpXIIQoCmq"><img src="https://img.shields.io/badge/NoCrypt's%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=orange"></a>
  <a href="https://colab.research.google.com/drive/1AH8z-p_ZSQvowZ-9pIVXBcqt_c3V4O9W"><img src="https://img.shields.io/badge/My Colab%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=16acc9"></a>
  <a href="https://discordapp.com/users/565783561878372352"><img src="https://img.shields.io/badge/MY%20DISCORD-blue?style=for-the-badge&logo=discord&logoColor=white&color=blue"></a> <br>
  <a href="https://colab.research.google.com/drive/1P89RgBbmnVAqtu0kF9BWo7HdJsWCCNxc"><img src="https://img.shields.io/badge/BETA -- it seems to be working%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=purple"></a>
</p>

---

## ❗ IMPORTANT:

_NoCrypt stated that Google Colab has completely stopped supporting the operability of A1111, and you can be disconnected from the session at any time..._

<div align="center">

### A little background check on the job...

| _Date_   | _Description of Performance_ |
|----------|------------------------------|
| 14.09.23 | - I can't guarantee this or confirm his words, as I worked for 1 hour and wasn't disconnected. I don't know if it was luck or if it's related to something else 😉 |
| 15.09.23 | - I'm really bummed that it stopped working, unlike yesterday's tryout... sad, of course, but I'm not giving up hope! <br> - Still I think the problem is in the code, so we will wait for action from _NoCrypt_ ;d |
|          | - After spending a couple more hours searching for a solution by trial and error, I may have found the reason.. _**(XL is shit, remember this, no kidding, it's true)**_. For now, use the `BETA version` of my colab, perhaps it will still work. **`Sorry but I didn't translate it into English(`** |

</div>


### Code to check for session disconnection:
<details>
<summary><kbd>Expand to see.</kbd></summary>
  
- _I wasn't too lazy to open access in the colaba, so just copy the code below and run it in the cell. In my case, I did not disconnect from the session... Maybe there are conflicts in the main code, I don't know for sure._
  
```py
import time
from IPython.utils import capture

try:
  start_colab
except:
  start_colab = int(time.time())-5

#@title # | What's here doesn't matter, but it works!

model_url = "https://civitai.com/api/download/models/138754" # @param {type:"string"}
model_file_name = "CuteColor_V3.safetensors" # @param {type:"string"}
commandline_arguments = "--enable-insecure-extension-access --multiple --disable-safe-unpickle --theme dark --no-hashing --opt-sdp-attention" #@param{type:"string"}

if "safetensors" or ".safetensors" not in model_file_name:
  model_file_name += ".safetensors"

print("Please wait for the shit to load for this to run. For about 1 minute~", end='')
with capture.capture_output() as cap:
  !wget https://huggingface.co/NoCrypt/fast-repo/resolve/main/ubuntu_deps.zip ; unzip ubuntu_deps.zip -d ./deps ; dpkg -i ./deps/* ; rm -rf ubuntu_deps.zip /content/deps/
  !echo -e "https://huggingface.co/NoCrypt/fast-repo/resolve/main/dep.tar.lz4\n\tout=dep.tar.lz4\nhttps://huggingface.co/NagisaNao/sd_webui_anxety_colab/resolve/main/anxety_repo.tar.lz4\n\tout=repo.tar.lz4\nhttps://huggingface.co/NoCrypt/fast-repo/resolve/main/cache.tar.lz4\n\tout=cache.tar.lz4\n" \
    | aria2c -i- -j5 -x16 -s16 -k1M -c

  !tar -xI lz4 -f dep.tar.lz4 --overwrite-dir --directory=/usr/local/lib/python3.10/dist-packages/ #(manual dir)
  !tar -xI lz4 -f repo.tar.lz4 --directory=/ #/content/sdw/ (auto dir)
  !tar -xI lz4 -f cache.tar.lz4 --directory=/ #/root/.cache/huggingface (auto dir)

  !rm -rf /content/dep.tar.lz4 /content/repo.tar.lz4 /content/cache.tar.lz4

  !aria2c --optimize-concurrent-downloads --console-log-level=error --summary-interval=10 -j5 -x16 -s16 -k1M -c -d /content/sdw/models/Stable-diffusion/ -o {model_file_name} {model_url}
  !aria2c --optimize-concurrent-downloads --console-log-level=error --summary-interval=10 -j5 -x16 -s16 -k1M -c -d /content/sdw/models/VAE/ -o Blessed2.vae.safetensors https://huggingface.co/NoCrypt/resources/resolve/main/VAE/blessed2.vae.safetensors
 
  !echo -n {start_colab} > /content/sdw/static/colabTimer.txt
del cap
print("\rDone!")

%cd /content/sdw
!COMMANDLINE_ARGS="{commandline_arguments}" REQS_FILE="requirements_versions.txt" python launch.py
```

</details>

---

## 👉 Beginnings

#### Most of the idea and code comes from [*NoCrypt*](https://github.com/NoCrypt).
I mostly just cut down what I considered unnecessary and little used, and also made my own system for downloading and so on. | Some extensions were removed, some ***config*** files were changed so that the interface was not too cluttered, some things of course were taken from his colab - for example his script `ColabTimer` - a really useful thing, and all the little things in general.

I don't think there's no point in saying anything else, it's clear what this colab does.

**I think I'll keep doing some updates and stuff like that until I get bored, I guess).**

---

<div align="center">
  
  <small>-- Again everything that has been done by me is just my simple adaptation --</small>
  
</div>
