# 🎨Алгоритм создания лабиринта🎨

![maze1](https://github.com/user-attachments/assets/66ccaed5-0fd4-4301-b7c5-69763c232bb1)

1. создаем HTML, CSS, JS документ

![2024-12-05_20-28-36](https://github.com/user-attachments/assets/e58db691-642d-4436-b12a-6f6c7efcc2b2)


2. объявляем Canvas
	- в файле index.html

```html
<canvas id="Canvas"></canvas>
```

![2024-12-05_20-35-34](https://github.com/user-attachments/assets/2f5cae01-4961-4756-bf2a-bf2b1218c309)

3. пишем стиль для Canvas в виде рамочки в файле Maze_CSS.css

```css
canvas{  
    border: 6px double black;  
    background: white;  
}
```

![2024-12-05_20-32-43](https://github.com/user-attachments/assets/6817f953-d2a6-4b15-8ef7-5a1b2986a4c2)

4. загружаем героя 

- в файле index.html

```html
<img id="face" src="face.png">
```

![2024-12-05_20-36-59](https://github.com/user-attachments/assets/24ab20a2-4ef5-47e5-b687-4a74e76e1bf4)


- в файле Maze_CSS.css

```css
img{  
    display: none;  
}
```

![2024-12-05_20-39-32](https://github.com/user-attachments/assets/86340ffa-07e1-4f10-a15f-be8c56c5ce9c)


5. определяем глобальные переменные для холста и контекста в файле Maze_JS.js

```JavaScript
var canvas;  
var context;
```

![2024-12-05_20-41-02](https://github.com/user-attachments/assets/efbf5da1-b12a-4950-90e0-307b74816906)

6. готовим холст
7. загружаем сам лабиринт - генерация лабиринта (https://mazegenerator.net/)
	- создаем функцию, которая будет рисовать наш лабиринт
	
	```JavaScript
	var x = 0;  
	var y = 0;  
	
	window.onload = function() {  
	    canvas = document.getElementById("Canvas");  
	    context = canvas.getContext("2d");  
	    drawMaze("maze1.jpg", 265, 5)  
		  
	};  
	  
	function drawMaze(mazeFile, startingX, startingY) {  
	
	}
	```
		
	- загружаем изображение лабиринта и изменяем размер холста в соответствии с размером изображения лабиринта
	
	```JavaScript
    dx = 0;  
    dy = 0;  
	  
    var imgMaze = new Image();  
    imgMaze.onload = function() {  
        canvas.width = imgMaze.width;  
        canvas.height = imgMaze.height;  
		  
        context.drawImage(imgMaze, 0, 0);  
		  
        x = startingX;  
        y = startingY;  
	
    };  
    
	```
	
	- рисуем лабиринт и значок
	
	```JavaScript
	var imgFace = document.getElementById("face");  
	        context.drawImage(imgFace, x, y);  
	        context.stroke();  
	imgMaze.src = mazeFile;  
	```
	
	- рисуем следующий кадр через 10 миллисекунд
	
	```JavaScript
	var timer; 
	clearTimeout(timer);  
	timer = setTimeout("drawMaze()", 10);  
	```

![2024-12-05_20-57-17](https://github.com/user-attachments/assets/0ae5950c-9c50-4ca8-a0df-ad8e26a660a6)


8. делаем анимацию значка
	- задаем начальную скорость перемещения значка
	- если значок при запуске находится в движении, останавливаем его
	- если нажата стрелка вверх, начинаем двигаться вверх
9. отображаем изменения на холсте
	- обновляем кадр только если значок движется
	- закрашиваем перемещение значка желтым цветом
	- обновляем координаты значка, создавая перемещение
	- проверка столкновения со стенками лабиринта
		- создаем отдельную функцию
		- перебираем все пикселы и "узнаем" их цвет
		- получаем данные для одного пиксела
		- смотрим на наличие черного цвета стены, что указывает на столкновение
