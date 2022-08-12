### Pygame的历史

﻿﻿![pygame_logo](https://eyehere.net/wp-content/uploads/2011/04/pygame_logo.gif)

Pygame是一个利用SDL库的写就的游戏库，SDL呢，全名Simple DirectMedia Layer，是一位叫做Sam Lantinga的大牛写的，据说他为了让Loki（致力于向Linux上移植Windows的游戏的一家大好人公司，可惜已经倒闭，唉好人不长命啊……）更有效的工作，创造了这个东东。

SDL是用C写的，不过它也可以使用C++进行开发，当然还有很多其它的语言，Pygame就是Python中使用它的一个库。Pygame已经存在很多时间了，许多优秀的程序员加入其中，把Pygame做得越来越好。

### 安装Pygame

你可以从[www.pygame.org](http://www.pygame.org/)下载Pygame，选择合适你的操作系统和合适的版本，然后安装就可以了（什么，你连Python都没有？您可能是不适合看这个系列了，不过如果执意要学，很好！快去[www.python.org](http://www.python.org/)下载吧！）。 一旦你安装好，你可以用下面的方法确认下有没有安装成功：

Python

| 123  | >>> import pygame>>> print pygame.ver1.9.1release |
| ---- | ---------------------------------------- |
|      |                                          |

你的版本可能和我不同，这没关系。我所翻译的这本书上的版本还是1.7.1的……所以如果有些过时的不合时宜的东西，千万不要客气请指出来！

若说为什么要介绍这么一个“过时”的东西，真正的知识是不会过时的，只有技术才会。这里主要是依靠Pygame来介绍的游戏开发的方方面面，并不是说咱就可以靠这个做出什么伟大的游戏了（当然也不是说不可以）！

另外说一下，就产品而言，Pygame更致力于2D游戏的开发，也就是说，你可以用Pygame写一个植物大战僵尸，但是写一个魔兽世界则相当困难……请不要做出鄙夷的目光，底层的东西永远是相通的，而且对于新手而言，从简单的2D入手才是正途。

### 使用Pygame

Pygame有很多的模块，下面是一张一览表：

| 模块名              | 功能             |
| ---------------- | -------------- |
| pygame.cdrom     | 访问光驱           |
| pygame.cursors   | 加载光标           |
| pygame.display   | 访问显示设备         |
| pygame.draw      | 绘制形状、线和点       |
| pygame.event     | 管理事件           |
| pygame.font      | 使用字体           |
| pygame.image     | 加载和存储图片        |
| pygame.joystick  | 使用游戏手柄或者 类似的东西 |
| pygame.key       | 读取键盘按键         |
| pygame.mixer     | 声音             |
| pygame.mouse     | 鼠标             |
| pygame.movie     | 播放视频           |
| pygame.music     | 播放音频           |
| pygame.overlay   | 访问高级视频叠加       |
| pygame           | 就是我们在学的这个东西了…… |
| pygame.rect      | 管理矩形区域         |
| pygame.sndarray  | 操作声音数据         |
| pygame.sprite    | 操作移动图像         |
| pygame.surface   | 管理图像和屏幕        |
| pygame.surfarray | 管理点阵图像数据       |
| pygame.time      | 管理时间和帧信息       |
| pygame.transform | 缩放和移动图像        |

有些模块可能在某些平台上不存在，你可以用None来测试一下。

Python

| 123  | if pygame.font is None:    print "The font module is not available!"    exit() |
| ---- | ---------------------------------------- |
|      |                                          |

### 新的Hello World

学程序一开始我们总会写一个Hello world程序，但那只是在屏幕上写了两个字，现在我们来点更帅的！写好以后会是这样的效果：

![pygame_hello_world](https://eyehere.net/wp-content/uploads/2011/04/pygame_hello_world.jpg)

Python

| 12345678910111213141516171819202122232425262728293031323334353637383940414243444546 | #!/usr/bin/env python background_image_filename = 'sushiplate.jpg'mouse_image_filename = 'fugu.png'#指定图像文件名称 import pygame#导入pygame库from pygame.locals import *#导入一些常用的函数和常量from sys import exit#向sys模块借一个exit函数用来退出程序 pygame.init()#初始化pygame,为使用硬件做准备 screen = pygame.display.set_mode((640, 480), 0, 32)#创建了一个窗口pygame.display.set_caption("Hello, World!")#设置窗口标题 background = pygame.image.load(background_image_filename).convert()mouse_cursor = pygame.image.load(mouse_image_filename).convert_alpha()#加载并转换图像 while True:#游戏主循环     for event in pygame.event.get():        if event.type == QUIT:            #接收到退出事件后退出程序            exit()     screen.blit(background, (0,0))    #将背景图画上去     x, y = pygame.mouse.get_pos()    #获得鼠标位置    x-= mouse_cursor.get_width() / 2    y-= mouse_cursor.get_height() / 2    #计算光标的左上角位置    screen.blit(mouse_cursor, (x, y))    #把光标画上去     pygame.display.update()    #刷新一下画面 |
| ---------------------------------------- | ---------------------------------------- |
|                                          |                                          |

*这个程序需要两张图片，你可以在这篇文章最后的地方找到下载地址，虽然你也可以随便找两张。为了达到最佳效果，背景的 sushiplate.jpg应要有640×480的分辨率，而光标的fugu.png大约应为80×80，而且要有Alpha通道（如果你不知道这是 什么，还是下载吧……）。*
**注意**：代码中的注释我使用的是中文，如果执行报错，可以直接删除。

**游戏中我已经为每一行写了注释，另外如果打算学习，强烈建议自己动手输入一遍而不是复制粘贴！

稍微讲解一下比较重要的几个部分：

**set_mode**会返回一个Surface对象，代表了在桌面上出现的那个窗口，三个参数第一个为元祖，代表分 辨率（必须）；第二个是一个标志位，具体意思见下表，如果不用什么特性，就指定0；第三个为色深。

| 标志位        | 功能                                  |
| ---------- | ----------------------------------- |
| FULLSCREEN | 创建一个全屏窗口                            |
| DOUBLEBUF  | 创建一个“双缓冲”窗口，建议在HWSURFACE或者OPENGL时使用 |
| HWSURFACE  | 创建一个硬件加速的窗口，必须和FULLSCREEN同时使用       |
| OPENGL     | 创建一个OPENGL渲染的窗口                     |
| RESIZABLE  | 创建一个可以改变大小的窗口                       |
| NOFRAME    | 创建一个没有边框的窗口                         |

**convert**函数是将图像数据都转化为Surface对象，每次加载完图像以后就应该做这件事件（事实上因为 它太常用了，如果你不写pygame也会帮你做）；**convert_alpha**相比convert，保留了Alpha 通道信息（可以简单理解为透明的部分），这样我们的光标才可以是不规则的形状。

游戏的主循环是一个无限循环，直到用户跳出。在这个主循环里做的事情就是不停地画背景和更新光标位置，虽然背景是不动的，我们还是需要每次都画它， 否则鼠标覆盖过的位置就不能恢复正常了。

**blit**是个重要函数，第一个参数为一个Surface对象，第二个为左上角位置。画完以后一定记得用**update**更新一下，否则画面一片漆黑。

这是一个最最大概的Pygame程序的印象，接下来我们会学习更多深层次的东西，并且把各条语句都真正读懂。



### 理解事件

事件是什么，其实从名称来看我们就能想到些什么，而且你所想到的基本就是事件的真正意思了。我们上一个程序，会一直运行下去，直到你关闭窗口而产生了一个QUIT事件，Pygame会接受用户的各种操作（比如按键盘，移动鼠标等）产生事件。事件随时可能发生，而且量也可能会很大，Pygame的做法是把一系列的事件存放一个队列里，逐个的处理。

### 事件检索

上个程序中，使用了**pygame.event.get()**来处理所有的事件，这好像打开大门让所有的人进入。如果我们使用**pygame.event.wait()**，Pygame就会等到发生一个事件才继续下去，就好像你在门的猫眼上盯着外面一样，来一个放一个……一般游戏中不太实用，因为游戏往往是需要动态运作的；而另外一个方法**pygame.event.poll()**就好一些，一旦调用，它会根据现在的情形返回一个真实的事件，或者一个“什么都没有”。下表是一个常用事件集：

| 事件              | 产生途径                    | 参数                |
| --------------- | ----------------------- | ----------------- |
| QUIT            | 用户按下关闭按钮                | none              |
| ATIVEEVENT      | Pygame被激活或者隐藏           | gain, state       |
| KEYDOWN         | 键盘被按下                   | unicode, key, mod |
| KEYUP           | 键盘被放开                   | key, mod          |
| MOUSEMOTION     | 鼠标移动                    | pos, rel, buttons |
| MOUSEBUTTONDOWN | 鼠标按下                    | pos, button       |
| MOUSEBUTTONUP   | 鼠标放开                    | pos, button       |
| JOYAXISMOTION   | 游戏手柄(Joystick or pad)移动 | joy, axis, value  |
| JOYBALLMOTION   | 游戏球(Joy ball)?移动        | joy, axis, value  |
| JOYHATMOTION    | 游戏手柄(Joystick)?移动       | joy, axis, value  |
| JOYBUTTONDOWN   | 游戏手柄按下                  | joy, button       |
| JOYBUTTONUP     | 游戏手柄放开                  | joy, button       |
| VIDEORESIZE     | Pygame窗口缩放              | size, w, h        |
| VIDEOEXPOSE     | Pygame窗口部分公开(expose)?   | none              |
| USEREVENT       | 触发了一个用户事件               | code              |

如果你想把这个表现在就背下来，当然我不会阻止你，但实在不是个好主意，在实际的使用中，自然而然的就会记住。我们先来写一个可以把所有方法输出的程序，它的结果是这样的。

![pygame_event](https://eyehere.net/wp-content/uploads/2011/04/pygame_event.jpg)

我们这里使用了wait()，因为这个程序在有事件发生的时候动弹就可以了。还用了*font*模块来显示文字（后面会讲的），下面是源代码：

Python

| 12345678910111213141516171819202122232425262728293031323334 | import pygamefrom pygame.locals import *from sys import exit pygame.init()SCREEN_SIZE = (640, 480)screen = pygame.display.set_mode(SCREEN_SIZE, 0, 32) font = pygame.font.SysFont("arial", 16);font_height = font.get_linesize()event_text = [] while True:     event = pygame.event.wait()    event_text.append(str(event))    #获得时间的名称    event_text = event_text[-SCREEN_SIZE[1]/font_height:]    #这个切片操作保证了event_text里面只保留一个屏幕的文字     if event.type == QUIT:        exit()     screen.fill((255, 255, 255))     y = SCREEN_SIZE[1]-font_height    #找一个合适的起笔位置，最下面开始但是要留一行的空    for text in reversed(event_text):        screen.blit( font.render(text, True, (0, 0, 0)), (0, y) )        #以后会讲        y-=font_height        #把笔提一行     pygame.display.update() |
| ---------------------------------------- | ---------------------------------------- |
|                                          |                                          |

*小贴士：*
书上说，如果你把填充色的(0, 0, 0)改为(0, 255, 0)，效果会想黑客帝国的字幕雨一样，我得说，实际试一下并不太像……不过以后你完全可以写一个以假乱真甚至更酷的！

这个程序在你移动鼠标的时候产生了海量的信息，让我们知道了Pygame是多么的繁忙……我们第一个程序那样是调用**pygame.mouse.get_pos()**来得到当前鼠标的位置，而现在利用事件可以直接获得！

### 处理鼠标事件

**MOUSEMOTION**事件会在鼠标动作的时候发生，它有三个参数：

- buttons – 一个含有三个数字的元组，三个值分别代表左键、中键和右键，1就是按下了。
- pos – 就是位置了……
- rel – 代表了现在距离上次产生鼠标事件时的距离

和MOUSEMOTION类似的，我们还有**MOUSEBUTTONDOWN**和**MOUSEBUTTONUP**两个事件，看名字就明白是什么意思了。很多时候，你只需要知道鼠标点下就可以了，那就可以不用上面那个比较强大（也比较复杂）的事件了。它们的参数为：

- button – 看清楚少了个s，这个值代表了哪个按键被操作
- pos – 和上面一样

### 处理键盘事件

键盘和游戏手柄的事件比较类似，为**KEYDOWN**和**KEYUP**，下面有一个例子来演示使用方向键移动一些东西。

Python

| 12345678910111213141516171819202122232425262728293031323334353637383940414243 | background_image_filename = 'sushiplate.jpg' import pygamefrom pygame.locals import *from sys import exit pygame.init()screen = pygame.display.set_mode((640, 480), 0, 32)background = pygame.image.load(background_image_filename).convert() x, y = 0, 0move_x, move_y = 0, 0 while True:    for event in pygame.event.get():        if event.type == QUIT:           exit()        if event.type == KEYDOWN:            #键盘有按下？            if event.key == K_LEFT:                #按下的是左方向键的话，把x坐标减一                move_x = -1            elif event.key == K_RIGHT:                #右方向键则加一                move_x = 1            elif event.key == K_UP:                #类似了                move_y = -1            elif event.key == K_DOWN:                move_y = 1        elif event.type == KEYUP:            #如果用户放开了键盘，图就不要动了            move_x = 0            move_y = 0         #计算出新的坐标        x+= move_x        y+= move_y         screen.fill((0,0,0))        screen.blit(background, (x,y))        #在新的位置上画图        pygame.display.update() |
| ---------------------------------------- | ---------------------------------------- |
|                                          |                                          |

当我们运行这个程序的时候，按下方向键就可以把背景图移动，但是等等！为什么我只能按一下动一下啊……太不好试了吧？！用脚掌考虑下就应该按着就一直动下去才是啊！？Pygame这么垃圾么……

哦，真是抱歉上面的代码有点小bug，但是真的很小，你都不需要更改代码本身，只要**改一下缩进**就可以了，你可以发现么？Python本身是缩进编排来表现层次，有些时候可能会出现一点小麻烦，要我们自己注意才可以。

KEYDOWN和KEYUP的参数描述如下：

- key – 按下或者放开的键值，是一个数字，估计地球上很少有人可以记住，所以Pygame中你可以使用**K_xxx**来表示，比如字母a就是K_a，还有**K_SPACE**和**K_RETURN**等。
- mod – 包含了组合键信息，如果mod & **KMOD_CTRL**是真的话，表示用户同时按下了Ctrl键。类似的还有**KMOD_SHIFT**，**KMOD_ALT**。
- unicode – 代表了按下键的Unicode值，这个有点不好理解，真正说清楚又太麻烦，游戏中也不太常用，说明暂时省略，什么时候需要再讲吧。

### 事件过滤

并不是所有的事件都需要处理的，就好像不是所有登门造访的人都是我们欢迎的一样。比如，俄罗斯方块就无视你的鼠标，而在游戏场景切换的时候，你按什么都是徒劳的。我们应该有一个方法来过滤掉一些我们不感兴趣的事件（当然我们可以不处理这些没兴趣的事件，但最好的方法还是让它们根本不进入我们的事件队列，就好像在门上贴着“XXX免进”一样），我们使用**pygame.event.set_blocked(事件名)**来完成。如果有好多事件需要过滤，可以传递一个列表，比如pygame.event.set_blocked([KEYDOWN, KEYUP])，如果你设置参数None，那么所有的事件有被打开了。与之相对的，我们使用**pygame.event.set_allowed()**来设定允许的事件。

### 产生事件

通常玩家做什么，Pygame就产生对应的事件就可以了，不过有的时候我们需要模拟出一些事件来，比如录像回放的时候，我们就要把用户的操作再现一遍。

为了产生事件，必须先造一个出来，然后再传递它：

Python

| 1234 | my_event = pygame.event.Event(KEYDOWN, key=K_SPACE, mod=0, unicode=u' ')#你也可以像下面这样写，看起来比较清晰（但字变多了……）my_event = pygame.event.Event(KEYDOWN, {"key":K_SPACE, "mod":0, "unicode":u' '})pygame.event.post(my_event) |
| ---- | ---------------------------------------- |
|      |                                          |

你甚至可以产生一个完全自定义的全新事件，有些高级的话题，暂时不详细说，仅用代码演示一下：

Python

| 12345678 | CATONKEYBOARD = USEREVENT+1my_event = pygame.event.Event(CATONKEYBOARD, message="Bad cat!")pgame.event.post(my_event) #然后获得它for event in pygame.event.get():    if event.type == CATONKEYBOARD:        print event.message |
| -------- | ---------------------------------------- |
|          |                                          |

这次的内容很多，又很重要，一遍看下来云里雾里或者看的时候明白看完了全忘了什么的估计很多，慢慢学习吧~~多看看动手写写，其实都很简单。



### 全屏显示

我们在第一个程序里使用了如下的语句

Python

| 1    | screen = pygame.display.set_mode((640, 480), 0, 32) |
| ---- | ---------------------------------------- |
|      |                                          |

也讲述了各个参数的意思，当我们把第二个参数设置为FULLSCREEN时，就能得到一个全屏窗口了

Python

| 1    | screen = pygame.display.set_mode((640, 480), FULLSCREEN, 32) |
| ---- | ---------------------------------------- |
|      |                                          |

*注意：如果你的程序有什么问题，很可能进入了全屏模式就不太容易退出来了，所以最好先用窗口模式调试好，再改为全屏模式。*

在全屏模式下，显卡可能就切换了一种模式，你可以用如下代码获得您的机器支持的显示模式：

Python

| 123  | >>> import pygame>>> pygame.init()>>> pygame.display.list_modes() |
| ---- | ---------------------------------------- |
|      |                                          |

看一下一个实例：

Python

| 123456789101112131415161718192021222324252627 | background_image_filename = 'sushiplate.jpg' import pygamefrom pygame.locals import *from sys import exit pygame.init()screen = pygame.display.set_mode((640, 480), 0, 32)background = pygame.image.load(background_image_filename).convert() Fullscreen = False while True:     for event in pygame.event.get():        if event.type == QUIT:            exit()    if event.type == KEYDOWN:        if event.key == K_f:            Fullscreen = not Fullscreen            if Fullscreen:                screen = pygame.display.set_mode((640, 480), FULLSCREEN, 32)            else:                screen = pygame.display.set_mode((640, 480), 0, 32)     screen.blit(background, (0,0))    pygame.display.update() |
| ---------------------------------------- | ---------------------------------------- |
|                                          |                                          |

运行这个程序，默认还是窗口的，按“f ”，显示模式会在窗口和全屏之间切换。程序也没有什么难度，应该都能看明白。

### 可变尺寸的显示

虽然一般的程序窗口都能拖边框来改变大小，pygame的默认显示窗口是不行的，而事实上，很多游戏确实也不能改变显示窗口的大小，我们可以使用一个参数来改变这个默认行为。

Python

| 123456789101112131415161718192021222324252627282930 | background_image_filename = 'sushiplate.jpg' import pygamefrom pygame.locals import *from sys import exit SCREEN_SIZE = (640, 480) pygame.init()screen = pygame.display.set_mode(SCREEN_SIZE, RESIZABLE, 32) background = pygame.image.load(background_image_filename).convert() while True:     event = pygame.event.wait()    if event.type == QUIT:        exit()    if event.type == VIDEORESIZE:        SCREEN_SIZE = event.size        screen = pygame.display.set_mode(SCREEN_SIZE, RESIZABLE, 32)        pygame.display.set_caption("Window resized to "+str(event.size))     screen_width, screen_height = SCREEN_SIZE    # 这里需要重新填满窗口    for y in range(0, screen_height, background.get_height()):        for x in range(0, screen_width, background.get_width()):            screen.blit(background, (x, y))     pygame.display.update() |
| ---------------------------------------- | ---------------------------------------- |
|                                          |                                          |

当你更改大小的时候，后端控制台会显示出新的尺寸，这里我们学习到一个新的事件**VIDEORESIZE**，它包含如下内容：

- size  —  一个二维元组，值为更改后的窗口尺寸，size[0]为宽，size[1]为高
- w  —  宽
- h  —  一目了然，高；之所以多出这两个，无非是为了方便

*注意:在我的Windows 7 64bit上运行的时候，一改变窗口大小就非法退出；在Linux机器上很正常，应该是系统的兼容性问题（Pygame还只支持32位），不过想来平时都不会更改游戏窗口大小，问题不大。*

至于无边框的窗口等，看一看[本教程的第一篇](https://eyehere.net/2011/python-pygame-novice-professional-1/)就能知道了，不再赘述。

### 其他、复合模式

我们还有一些其他的显示模式，但未必所有的操作系统都支持（放心windows、各种比较流行的Linux发行版都是没问题的），一般来说窗口就用0全屏就用FULLSCREEN，这两个总是OK的。

如果你想创建一个硬件显示（surface会存放在显存里，从而有着更高的速度），你必须和全屏一起使用：

Python

| 1    | screen = pygame.display.set_mode(SCREEN_SIZE, HWSURFACE \| FULLSCREEN, 32) |
| ---- | ---------------------------------------- |
|      |                                          |

当然你完全可以把双缓冲（更快）DOUBLEBUF也加上，这就是一个很棒的游戏显示了，不过记得你要使用**pygame.display.flip()**来刷新显示。pygame.display.update()是将数据画到前面显示，而这个是交替显示的意思。

稍微说一下双缓冲的意思，可以做一个比喻：我的任务就是出黑板报，如果只有一块黑板，那我得不停的写，全部写完了稍微Show一下就要擦掉重写，这样一来别人看的基本都是我在写黑板报的过程，看到的都是不完整的黑板报；如果我有两块黑板，那么可以挂一块给别人看，我自己在底下写另一块，写好了把原来的换下来换上新的，这样一来别人基本总是看到完整的内容了。双缓冲就是这样维护两个显示区域，快速的往屏幕上换内容，而不是每次都慢慢地重画。