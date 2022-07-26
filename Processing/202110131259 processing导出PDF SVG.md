相关链接：
[pdf Export](https://processing.org/reference/libraries/pdf/index.html)
[svg Export](https://processing.org/reference/libraries/svg/index.html)

# 简介
SVG Library和PDF Library都支持导出矢量文件。
对于P3D渲染的内容，它会压扁3D数据变成2D的文件。（如果想要3D data，使用DXF library）。
这个库可以使用size(), or createGraphics()来执行。

## 关于字体效果
SVG导出时，**不支持字体的效果**，但是会保留文本数据（可以在Ai里更改字体）。
而PDF导出可以支持字体效果，但是已经轮廓化。


# SVG Export


## ①不显示，直接导出
直接在size()里写SVG渲染器，并写上导出文件名。draw完直接exit()
```processing
import processing.svg.*;

void setup() {
  size(400, 400, SVG, "filename.svg");
}

void draw() {
  // Draw something good here
  line(0, 0, width/2, height);

  // Exit the program
  println("Finished.");
  exit();
}
```

## ②带屏幕显示，只渲染一帧。
svg的这个record模式，只会保留endRecord()前的最后一帧。
使用`beginRecord(SVG,"filename.svg")`，和`endRecord()`

```processing
import processing.svg.*;

void setup() {
  size(400, 400);
  noLoop();
  beginRecord(SVG, "filename.svg");
}

void draw() {
  // Draw something good here
  line(0, 0, width/2, height);

  endRecord();
}
```


## ③随心导出某些帧（加控制开关）
```processing
import processing.svg.*;

boolean record;

void setup() {
  size(400, 400);
}

void draw() {
  if (record) {
    // Note that #### will be replaced with the frame number. Fancy!
    beginRecord(SVG, "frame-####.svg");
  }

  // Draw something good here
  background(255);
  line(mouseX, mouseY, width/2, height/2);

  if (record) {
    endRecord();
    record = false;
  }
}

// Use a keypress so thousands of files aren't created
void mousePressed() {
  record = true;
}
```

## ④从P3D里导出SVG
使用beginRaw() endRaw().
写法和Record类似
这两个命令会压扁空间数据，使其在二维平面上展示。

![[src/img/iShot2021-10-13 13.38.55.png]]
![[src/img/Pasted image 20211013133916.png]]

```processing
import processing.svg.*;

boolean record;

void setup() {
  size(500, 500, P3D);
}

void draw() {
  if (record) {
    beginRaw(SVG, "output.svg");
  }

  // Do all your drawing here
  background(204);
  translate(width/2, height/2, -200);
  rotateZ(0.2);
  rotateY(mouseX/500.0);
  box(200);

  if (record) {
    endRaw();
    record = false;
  }
}

// Hit 'r' to record a single frame
void keyPressed() {
  if (key == 'r') {
    record = true;
  }
}
```


## ⑤局部导出：使用createGraphics()
这会只导出画在PGraphics上的内容。
```processing
import processing.svg.*;

PGraphics svg = createGraphics(300, 300, SVG, "output.svg");
svg.beginDraw();
svg.background(128, 0, 0);
svg.line(50, 50, 250, 250);
svg.dispose();
svg.endDraw();
```

## 其他注意事项
-   很多Method，尤其是基于像素处理的method在SVG Render里是无效的。包括loadPixels,updatePicels,get,set,mask,filter,copy,blend,save,image.
-   重要重申, exit() 非常重要 ，当你使用size()来导出svg时。

---


# PDF Export
[PDF Export官方说明](https://processing.org/reference/libraries/pdf/index.html)
pdf导出的特性和svg大体相似。都可以导出矢量图形。
在Ai里，需要对他进行解除蒙版的操作，会有一点点麻烦（也还好）。

调用这个export，通常是在size()里，配合beginRecord()和endRecor()、或者beginRaw(),endRaw(); 也可以使用createGraphics().

用法和SVG导出大体相同。只是把渲染器SVG换成PDF，文件名的后缀换成.pdf
下面只列举PDF特有的导出情况。

## ①导出多页文件（无屏幕显示）
关键是使用`.nextPage()`
```processing
import processing.pdf.*;

void setup() {
  size(400, 400, PDF, "filename.pdf");
}

void draw() {
  // Draw something good here
  line(0, 0, frameCount * 4, height);

  PGraphicsPDF pdf = (PGraphicsPDF) g;  // Get the renderer。虽然不懂这个g是什么意思，但总之就这么跟着写吧。或许是get。

  // 在此设定页数100，如果达成就退出。
  if (frameCount == 100) {
    exit();
  } else {
    pdf.nextPage();  // 告诉程序 go to the next page
  }
}
```

## ②所见即所得渲染, 只1帧（有显示）
```processing
import processing.pdf.*;

void setup() {
  size(400, 400);
  beginRecord(PDF, "everything.pdf");
}

void draw() {
  // Be sure not to call background, otherwise your file
  // will just accumulate lots of mess, only to become invisible

  // Draw something good here
  line(mouseX, mouseY, width/2, height/2);
}

void keyPressed() {
  if (key == 'q') {
    endRecord();
    exit();
  }
}
```


## ③仅取最后start~stop之间的内容。

![[src/img/Pasted image 20211013143000.png]]
![[src/img/Pasted image 20211013142945.png]]
```processing
import processing.pdf.*;

boolean recording;
PGraphicsPDF pdf;

void setup() {
  size(400, 400);
  pdf = (PGraphicsPDF) createGraphics(width, height, PDF, "pause-resume.pdf");
}

void draw() {
  // Be sure not to call background, otherwise your file
  // will just accumulate lots of mess, only to become invisible

  // Draw something good here
  if (mousePressed) {
    line(pmouseX, pmouseY, mouseX, mouseY);
  }
}

void keyPressed() {
  if (key == 'r') {
    if (recording) {
      endRecord();
      println("Recording stopped.");
      recording = false;
    } else {
      beginRecord(pdf);
      println("Recording started.");
      recording = true;
    }
  } else if (key == 'q') {
    if (recording) {
      endRecord();
    }
    exit();
  }
}
```


## ④使用createGraphics()
注意，这里有必要在画完之后使用dispose()，这等同于exit(),但是它不会退出程序。
```processing
import processing.pdf.*;

PGraphics pdf = createGraphics(300, 300, PDF, "output.pdf");
pdf.beginDraw();
pdf.background(128, 0, 0);
pdf.line(50, 50, 250, 250);
pdf.dispose();
pdf.endDraw();
```

## 其他注意事项
### 关于字体
据官方说明，从0120号更新开始，文本不再默认被当做一个形状数据了。这意味着必须安装字体才能在所创建的这个PDF里看到它。这可以让PDF渲染得更好。

具体的操作方法：
情况一：使用`size( ,PDF, )`来渲染的情况。
那么无所谓顺序，只要creatFont了就行。
如果还是不行，那就在size(width,height,PDF,"file.pdf")后使用textMode(SHAPE)

情况二：使用`beginRecord()`的情况。
要在这个命令之后，有配置字体的命令。写在setup里的不算数。
所以可以写一个`void fontOffset()`来方便调用。
```processing

void setup(){
size();
fontOffset();}

void draw(){
if(record){
beginRecord();
fontOffset();}
...//画你想画
if(record){
endRecord();
record = false;}
}}

void fontOffset(){
myFont = createFont(...);
textFont(myFont);
textAlign();

}
```
    
情况三：使用`PGraphics()`的情况。
要在画布里逐一配置上text相关的设置。例如
```
PGraphics pdf = createGraphics(600, 250, PDF, "output.pdf");

pdf.beginDraw();
    syyt = createFont("data/syyt.ttf", 30);
    pdf.textFont(syyt);
    pdf.imageMode(CENTER);
    pdf.textAlign(RIGHT, CENTER);
	
	...
pdf.dispose();
pdf.endDraw();
	
	
```

### 创建新的一页
使用`nextPage()`
    
    ```processing
    PGraphicsPDF pdf = (PGraphicsPDF) g;
    pdf.nextPage();
    ```
    
    (This example is also shown above)
    
### exit()很重要	
最后重申， exit() is really important when using PDF with size() 。