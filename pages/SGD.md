- **Стохастический градиентный спуск**— это метод оптимизации, который используется для минимизации функции ошибки в машинном обучении, особенно в нейронных сетях. Это одна из ключевых техник, позволяющих обучать модели, такие как глубокие нейронные сети. Давайте разберем, как он работает и в чем его особенности.
- **Что делает стохастический градиентный спуск?**
	- Стохастический градиентный спуск (SGD) ускоряет процесс, вычисляя градиент только на одном случайно выбранном примере из обучающей выборки. Это снижает вычислительные затраты, но делает процесс обучения более шумным.
	- Обновление весов в SGD
	  collapsed:: true
		- **Вместо усреднения градиентов по всей выборке (как в классическом методе), SGD делает обновления для каждого примера отдельно.**
- **Улучшенные варианты SGD**
	- [[Momentum]]: Добавляет "ускорение", чтобы быстрее сходиться к минимуму.
	- [[RMSProp]]: Адаптирует скорость обучения для разных параметров.
	- [[Adam]]: Комбинирует Momentum и RMSProp, чтобы сделать процесс обучения более стабильным и быстрым.