## Гипотеза:
	- ID не несет никой семантики, может меняться во время разработки и от игры к игре.
		- Это делает практически невозможным использование RL "в бою".
- Какие варианты?
	- TODO [[2411.12173] SkillTree: Explainable Skill-Based Deep Reinforcement Learning for Long-Horizon Control Tasks](https://arxiv.org/abs/2411.12173)
	- TODO [[1906.09223] Disentangled Skill Embeddings for Reinforcement Learning](https://arxiv.org/abs/1906.09223)
	- TODO [[1806.01830] Relational Deep Reinforcement Learning](https://arxiv.org/abs/1806.01830)
- Какие есть примеры использования RL в реальных играх
	- [[Dota 2 with Large Scale Deep Reinforcement Learning]]
	  :LOGBOOK:
	  CLOCK: [2024-12-19 Thu 17:38:55]--[2024-12-19 Thu 17:38:55] =>  00:00:00
	  :END:
		- Categorical data processing немного не понятен {{embed ((6765586a-d7e4-463e-9221-49829ce007f8))}}
	- [AI Summit Building ML Bots at Ubisoft La Forge From Research to Production](https://disk.yandex.ru/d/cz6waY7qvJ3LHQ)
		- Rainbowsix Siege
			- [[Imitation Learning]]
			- Никаких подробностей о структуре состояния👎
		- For Honor
			- [[RL]]
			- Аналогично
		- Smart Proto
			- 35:30 Ray-cast Perception, speed up with RT
			- [[CMDP]]
		- Trends
			- Natural language
			- Show don't tell [[Offline RL]]
		- https://github.com/edbeeching/godot_rl_agents
	- [Machine Learning Summit Naruto Mobile Optimization for LargeScale Reinforcement Learning in Fighting Games](https://disk.yandex.ru/d/cz6waY7qvJ3LHQ)
		- Вместо ID предлагается использовать AABB ключевых объектов
	- [Machine Learning Summit Training HumanLike and HighPerformance Basketball AI Bot for Streetball Allstar With Introduction from Summit Advisor Julien Merceron](https://disk.yandex.ru/d/cz6waY7qvJ3LHQ)
		- [[Behaviour Cloning]]
		- Просто используют ID
	- TODO [Learning Agents | Unreal Fest 2024](https://www.youtube.com/watch?v=FYgJsN_fMr8)
		- TODO [Humanlike Behavior in a Third-Person Shooter with Imitation Learning | Alex Farhang](https://alexfarhang.github.io/humanlikebehavior) [Humanlike_Behavior.pdf](https://alexfarhang.github.io/assets/pdf/Humanlike_Behavior.pdf)
	- TODO find Minecraft refs