<div align="center">

<h1 align="center">ANXETY COLAB</h1>

[English ](./README.md) | Русский

</div>

<p align="center">
  <a href="https://colab.research.google.com/drive/1wEa-tS10h4LlDykd87TF5zzpXIIQoCmq"><img src="https://img.shields.io/badge/NoCrypt's%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=orange"></a>
  <a href="https://colab.research.google.com/drive/1AH8z-p_ZSQvowZ-9pIVXBcqt_c3V4O9W"><img src="https://img.shields.io/badge/Мой Колаб%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=16acc9"></a>
  <a href="https://discordapp.com/users/565783561878372352"><img src="https://img.shields.io/badge/Мой Дискорд-blue?style=for-the-badge&logo=discord&logoColor=white&color=blue"></a>
  <a href="https://colab.research.google.com/drive/1P89RgBbmnVAqtu0kF9BWo7HdJsWCCNxc"><img src="https://img.shields.io/badge/BETA -- не работает%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=16acc9"></a>
</p>

---

## ❗ ВАЖНО:

_NoCrypt заявил, что Google Colab полностью прекратил поддержку работы A1111, и вы можете быть отключены от сессии в любое время..._

<div align="center">

### Небольшая предыстория работы...

| _Дата_   | _Описание результатов?_ |
|----------|-------------------------|
| 14.09.23 | - Я не могу гарантировать это или подтвердить его слова, так как я работал 1 час и не был отключен. Не знаю, связано ли это с удачей или с чем-то еще 😉 |
| 15.09.23 | - Мне очень жаль, что это перестало работать, в отличие от вчерашнего тестирования... грустно, конечно, но я не теряю надежду! 
|          | - Все же я думаю, что проблема в коде, так что будем ждать действий от _NoCrypt_ ;d |

</div>
<br>

-> Мне было лень открывать доступ в колабе, поэтому просто скопируйте приведенный ниже код и запустите в ячейке. В моем случае я не отключался от сессии... Возможно, в основном коде есть конфликты, я точно не знаю)

<details>
<summary><kbd>Разверни чтобы увидеть</kbd></summary>

```py
import time
from IPython.utils import capture

try:
  start_colab
except:
  start_colab = int(time.time())-5

#@title # | То, что здесь находится, не имеет значения, но это работает! | наверное)

model_url = "https://civitai.com/api/download/models/138754" # @param {type:"string"}
model_file_name = "CuteColor_V3.safetensors" # @param {type:"string"}
commandline_arguments = "--enable-insecure-extension-access --multiple --disable-safe-unpickle --theme dark --no-hashing --opt-sdp-attention" #@param{type:"string"}

if "safetensors" or ".safetensors" not in model_file_name:
  model_file_name += ".safetensors"

print("Пожалуйста, подождите, пока это дерьмо загрузится, чтобы запустить его. В течение примерно 1 минуты ~", end='')
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
print("\rГотово!")

%cd /content/sdw
!COMMANDLINE_ARGS="{commandline_arguments}" REQS_FILE="requirements_versions.txt" python launch.py
```

</details>

---

## 👉 Начало

#### Большая часть идей и кода взята у [*NoCrypt*](https://github.com/NoCrypt).
В основном я просто убрал то, что считал ненужным и малоиспользуемым, а также сделал свою собственную систему загрузки и т.д. | Некоторые расширения были удалены, некоторые ***конфигурационные*** файлы были изменены, чтобы интерфейс не был слишком загроможден, некоторые вещи, конечно, были взяты из его колаба - например, его скрипт `ColabTimer` - действительно полезная вещь, ну и всякие мелочи в целом.

Думаю, нет смысла говорить что-то еще, и так понятно, что делает этот колаб.

**Я думаю, что буду продолжать делать какие-то обновления и тому подобное, пока не надоест, наверное).**

---

<div align="center">
  
  <small>-- Повторюсь, все, что было сделано мной, является лишь моей простой адаптацией --</small>
  
</div>


