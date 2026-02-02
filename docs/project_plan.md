# План разработки (Roadmap)

## Этап 1
- [Done] Выбрать, скомпилировать проект, с реализованной обратной трассировкой лучей (Path Tracer). Это может быть как версия для CPU, так и для GPU, например, https://github.com/knightcrawler25/GLSL-PathTracer.

---
Проект https://github.com/knightcrawler25/GLSL-PathTracer использует библиотеки:
- Кроссплатформенная мультимедийная библиотеку: [SDL 2](https://www.libsdl.org/)
- Программный интерфейс для написания приложений, использующих двумерную и трёхмерную компьютерную графику: [OpenGL 3.3]()
- библиотека графического пользовательского интерфейса (GUI): [imgui](https://github.com/ocornut/imgui?ysclid=ml5fpp4rai884204024)
- Библиотека ускорения пересечения лучей разработанная AMD: [Radeon Rays](https://gpuopen.com/radeon-rays/) 

```
Примечание

RadeonRays не ограничивается аппаратным оборудованием AMD, конкретной операционной системой или графической структурой. Библиотека помогает обеспечить совместимость и лучшую производительность на широком спектре аппаратных платформ.

В проекте используется версия Radeon Rays 2.0.0 (или 2.0.1)

В мае 2020 вышла версия Radeon Rays 4.0 и одним из изменений прекращение использования OpenCL что усложнило интеграцию библиотеки в проект.

Radeon Rays 4.0 работает только с API Vulkan 1.2 и DirectX 12
``` 
- Однофайловая реализация загрузчика формата Wavefront .obj: [tinyobjloader](https://github.com/tinyobjloader/tinyobjloader?ysclid=ml5gh7hrp765674338)
- Библиотека для загрузки моделей glTF, закодированных в JSON: [tinygltf](https://github.com/syoyo/tinygltf?ysclid=ml5giyo5s012060310)
- Используется библиотека для удаления шума для трассировки лучей (denoiser): [Intel® Open Image Denoise](https://www.openimagedenoise.org/)


---
![Пример сцены "hyperion_sphere_light.scene без использования denoiser"](screen_path_tracing/Пример%20сцены%20pt.png)
<center>Пример сцены "hyperion_sphere_light.scene без использования denoiser"</center>

---

![Пример сцены "hyperion_sphere_light.scene с использованием denoiser"](screen_path_tracing/Пример%20сцены%20pt%20с%20denoiser.png)
<center>Пример сцены "hyperion_sphere_light.scene с использованием denoiser"</center>

---

Сцена хранится в файле в формате *.scene

Структура:
- Настройка рендера сцены
```
renderer
{
	resolution 1280 720
	maxdepth 3
	tilewidth 256
	tileheight 144
}
```
- Настройка камеры
```
camera
{
	position -15.0 15.0 0.0
	lookat 0 0 0
	fov 60
}
```
- Настройка материалов
```
material glass
{
	color 1.0 1.0 1.0
	spectrans 1.0
	ior 1.45
	roughness 0.05
}
...
```
- Загрузка и настройка объектов (использование материала, изменение размера, положения и поворота)
```
mesh
{
	name Glass Ball
	file hyperion/glass.obj
	material glass
	position -0.57 1.87 6.55
}
...
```
- Настройка источника света
```
light
{
	emission 80 80 80
	position 0 39.0 -43.9
	radius 6.0
	type sphere
}
```
## Этап 2
- [ ] Выбрать или создать с помощью редактора (например, blender) 3D сцены (несколько штук, например, 2-3) для рендеринга.
## Этап 3
- [ ] Реализовать загрузку 3D сцены для проекта с Path Tracer, например, с помощью поддержки формата GLTF (для хранения сцены) и библиотеки Assimp (для загрузки).
## Этап 4
- [In-progress] Изучить PBR (2012) техники, связанные с построением модели освещения (https://learnopengl.com/PBR/Theory).
## Этап 5
- [In-progress] Изучить теорию и выбрать метод двунаправленной трассировки лучей (Bidirectional Path Tracing).
## Этап 6
- [ ] Реализовать Bidirectional Path Tracing.
## Этап 7
- [ ] Сравнить решения с PT и BD RT. Сравнить время рендеринга, качество финальной картинки.
## Этап 8.1
- [In-progress] Изучить готовые решения AI-based upscaler и denosier.
## Этап 8.2
- [ ] Добавить их в проект.
## Этап 9
- [ ] Сравнить решения с upscaler и denosier и без. Сравнить время рендеринга, качество финальной картинки. Сравнить с разными разрешениями.
## Этап 10
- [ ] Написать дипломную работу на основе полученной информации и результатов вычислительных экспериментов.
