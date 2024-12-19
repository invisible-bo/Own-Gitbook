---
icon: forklift
---

# Usefull Pips & Modules

## Pygame

```python
pip install pygame
# 그래픽,사운드,이벤트 처리(키보드, 마우스 입력 감지),애니메이션 등을 지원

import pygame

pygame.init() # Pygame 초기화(반드시필요)
```

* sound part

<pre class="language-python"><code class="lang-python">{variable name} = pygame.mixer.Sound(sound file name)
# Importing sound file

<strong>{variable name}.play()
</strong><strong># play sound file
</strong>
{variable name}.play(-1)
# play sound file Infinite loop

{variable name}.stop()
# stop sound file

pygame.mixer.stop()
# stop playing all sound files

{variable name}.fadeout(num)
# (num)ms동안 fadeout   1000ms = 1second
</code></pre>



***

## Time Module

```python
import time 

time.sleep(n) 
# stop while n seconds 
```

