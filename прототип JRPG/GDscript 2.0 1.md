## Движение
S = V x t
S - расстояние
V - скорость
t - время (delta(чем больше fps, тем меньше delta))

```python

# Текущее положение объекта
var current_position = global_transform.origin/global_position

# Рассчитывам расстояние, на которое переместимся в текущем кадре
var distance: float = SPEED * delta

# Рассчитывам точку перемещения на расстояние distance в направлении direction
var next_point: Vector3 = current_position + (direction.normalized() * distance)

# Перемещаем объект
global_transform.origin = next_point

```

## Анимация
```js
@onready var animatonPlayer = $AnimationPlayer 
@onready var animationTree = $AnimationTree
@onready var animState = animationTree.get("parameters/playback")

# Если в переменной направления (которая задаётся WASD) есть какое-то значение в Vector2, то идёт анимация
if input_dir:
	animationTree.set("parameters/Idle/blend_position", input_dir)
	animationTree.set("parameters/Walk/blend_position", input_dir)
	animState.travel("Walk")
else:
	animState.travel("Idle")
```

## Пауза

```js
func pause(s: bool = false):
	get_tree().paused = s
```


___

## Сигналы
Ноды в Godot общаются между собой сигналами и отправляют их вне зависимости от того, отправляет ли разработчик стандартные сигналы вручную из скрипта или нет

```python
# коннект сигнала выхода ноды из дерева
var x: Node

x.connect("tree_exited", _tree_exited) #<- это callable (_tree_exited)

func _tree_exited():
	pass
```

## EXTRA

*Ctrl + R*  - замена одинаковых строчек кода

```python
# если объект сильно отдалился от стартовой позиции
if transform.origin.distance_to(start_point) > 10:

# направление до какой-то цели
global_position.direction_to(target)

# если инстанс объекта не валиден и не вышел из дерева
if is_instance_valid(x)

# callable
func _ready():
	interaction_area.interact = Callable(self, "_on_interact")
	pass
	
#выход из игры
func _unhandled_input(event):
	
	if event is InputEventKey:
		if event.pressed and event.keycode == KEY_ESCAPE:
			get_tree().quit()


#закрепление 2d объекта за 3d объектом
var screenPos = cam.unproject_position(self.global_position)
current_dialog.control.set_position(Vector2(screenPos.x - 200, screenPos.y - 200))


```
