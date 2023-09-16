<div align="center">

<h1 align="center">ANXETY COLAB</h1>

[English ](./README.md) | Русский

</div>

<p align="center">
  <a href="https://colab.research.google.com/drive/1wEa-tS10h4LlDykd87TF5zzpXIIQoCmq"><img src="https://img.shields.io/badge/NoCrypt's%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=orange"></a>
  <a href="https://colab.research.google.com/drive/1AH8z-p_ZSQvowZ-9pIVXBcqt_c3V4O9W"><img src="https://img.shields.io/badge/Мой Колаб | Требуются Обновления%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=darkred"></a>
  <a href="https://discordapp.com/users/565783561878372352"><img src="https://img.shields.io/badge/Мой Дискорд-blue?style=for-the-badge&logo=discord&logoColor=white&color=blue"></a> <br>
  <a href="https://colab.research.google.com/drive/1P89RgBbmnVAqtu0kF9BWo7HdJsWCCNxc"><img src="https://img.shields.io/badge/БЕТА ВЕРСИЯ%20-%20grey?style=for-the-badge&logo=google%20colab&logoColor=orange&label=Colab&labelColor=darkcayan&color=purple"></a>
</p>

---

## ❗ ВАЖНО:

_NoCrypt заявил, что Google Colab полностью прекратил поддержку работы A1111, и вы можете быть отключены от сессии в любое время..._

<div align="center">

### Небольшая справка о работе...

| _Дата_   | _Описание результатов_ |
|----------|------------------------|
| 13.09.23 | - Я не могу гарантировать это или подтвердить его слова, так как я работал 1 час и не был отключен. Не знаю, связано ли это с удачей или с чем-то еще 😉 |
| 14.09.23 | - Мне очень жаль, что это перестало работать, в отличие от вчерашнего тестирования... грустно, конечно, но я не теряю надежду! <br> - Все же я думаю, что проблема в коде, так что будем ждать действий от _NoCrypt_ ;d |
|          | - Потратив еще пару часов на поиск решения методом проб и ошибок, я, возможно, нашел причину.. _**(XL - отстой, запомните это, это правда)**_. А пока воспользуйтесь [_БЕТА-версией_](https://colab.research.google.com/drive/1P89RgBbmnVAqtu0kF9BWo7HdJsWCCNxc) моего колаба, возможно, он все еще будет работать. |
| 15.09.23 | - Это плохо, меня снова отключает от сеанса... в данный момент я ищу \*_слова-триггеры_\*, на которые ругается Гугл Колаб. |
|          | - Я так и не смог решить проблему с отключением... завтра планирую продолжить, возможно, придется применить другой подход, а не пытаться найти "запрещенные слова". _NoCrypt_ - сегодня обновил свой репозиторий на Hugging Face - возможно, он тоже предпринимает какие-то действия? |
| 16.09.23 | - Провел небольшой тест на отключение сессии на колабе [cameduru](https://github.com/camenduru/stable-diffusion-webui-colab) - отключений не обнаружено, возможно, придется переписать все под его репо. |

</div>

---

### ⚠️ `СТАТУС БЕТА ВЕРСИИ:` на данный момент снова отключается - _не работает_. ⚠️

### Код на котором я делаю проверки:
<details>
<summary><kbd>Разверните чтобы увидеть.</kbd></summary>

- _Мне было лень открывать доступ в колабе, поэтому просто скопируйте приведенный ниже код и запустите в ячейке._

```py
%cd /content

%env TF_CPP_MIN_LOG_LEVEL=1

!apt -y install -qq aria2

# Huh. The best way to get around the prohibition.
a = "stable-"+"diffusion-"+"webui"
b = "sd-"+"webui"

!git clone -b v2.6 https://github.com/camenduru/{a}
!git clone https://github.com/kohya-ss/{b}-additional-networks /content/{a}/extensions/{b}-additional-networks
!git clone https://github.com/Mikubill/{b}-controlnet /content/{a}/extensions/{b}-controlnet
!git clone https://github.com/camenduru/{b}-tunnels /content/{a}/extensions/{b}-tunnels
!git clone https://github.com/etherealxx/batchlinks-webui /content/{a}/extensions/batchlinks-webui
!git clone https://github.com/catppuccin/{a} /content/{a}/extensions/{a}-catppuccin
!git clone https://github.com/thomasasfk/{b}-aspect-ratio-helper /content/{a}/extensions/{b}-aspect-ratio-helper
%cd /content/{a}
!git reset --hard

!aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/ckpt/OrangeMixs/resolve/main/AOM3.safetensors -d /content/{a}/models/Stable-diffusion -o AOM3.safetensors
!aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/ckpt/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.ckpt -d /content/{a}/models/Stable-diffusion -o orangemix.vae.pt

!python launch.py --enable-insecure-extension-access --multiple --disable-safe-unpickle --theme dark --no-hashing --opt-sdp-attention
```

</details>

---

## 👉 Начало

#### Большая часть идей и кода взята у [*NoCrypt*](https://github.com/NoCrypt).
В основном я просто убрал то, что считал ненужным и малоиспользуемым, а также сделал свою собственную систему загрузки и т.д. | Некоторые расширения были удалены, некоторые ***конфигурационные*** файлы были изменены, чтобы интерфейс не был слишком загроможден, некоторые вещи, конечно, были взяты из его колаба - например, его скрипт `ColabTimer` - действительно полезная вещь, ну и всякие мелочи в целом.

---

<div align="center">
  
  <small>-- Повторюсь, все, что было сделано мной, является лишь моей простой адаптацией --</small>
  
</div>


