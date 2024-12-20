Link:: [[1912.06680] Dota 2 with Large Scale Deep Reinforcement Learning](https://arxiv.org/abs/1912.06680)

- OpenAI Five observes 16000 total values (mostly floats and **categorical** values with hundreds of possibilities) each time step
- Because visible information and _fog of war_ are shared across a team in Dota 2, the observations are nearly identical for each hero.
	- Ну это чистой воды читерство, не спортивно!
- Continual Transfer via Surgery. Или: что делать, когда в игре что-то меняется
	- Проблема:
		- When these changes occur, most aspects of the old model are likely relevant in the new environment. But cherry-picking parts of the parameter vector to carry over is challenging and limits reproducibility. For these reasons training from scratch is the safe and common response to such changes.
	- Решение:
		- Если коротко: входные веса рандомим, выходные зануляем
		- ==Странно==, но они рассказали, только про случай увеличения Obs space.
			- Очевидно, только потому, что то что они описали работает только в этом случае, может я что-то упустил
			- Потому что при уменьшении, нужно выбрать веса, которые выкинуть, т.е. нужно вводить некоторую unitity function, как мы видели это у Sutton [[Streaming Deep Reinforcement Learning Finally Works]]
- Reward Function:
	- In practice, we maximize a reward function which includes additional signals such
	   as characters dying, collecting resources, etc.
	- we symmetrize rewards by subtracting the reward earned by the opposing team
- Limitations:
	- Subset of 17 heroes — in the normal game players select before the game one from a pool of
	   117 heroes to play; we support 17 of them.
	- No support for items which allow a player to temporarily control multiple units at the same
	   time
	- While we were careful to ensure that all the information available to the model is also available to a human, the model does get to see all the information available simultaneously every time step, **whereas a human needs to click into various menus and options to get that data**. Although these discrepancies are a **limitation**, we do not believe they meaningfully detract from our ability to benchmark against human players.
		- Именно поэтому сравнение с человеком не имеет смысла он SuperHuman, потому что имеет non human capabilities.
			- Для бота нормально, для спорта нет.
- Observation Space:
	- Instead of using the pixels on the screen, we approximate the information available to a human
	   player in a set of data arrays.
	- This approximation is **imperfect**; there are small pieces of information which humans can gain access to which we have not encoded in the observations.
	- Why not screen image?
		- OpenAI Five uses a more semantic observation space than this for two reasons: First, because our goal is to study strategic planning and gameplay rather than focus on visual processing. Second, it is infeasible for us to render each frame to pixels in all training games; this would multiply the computation resources required for the project manyfold.
	- Категориальные переменные
		- Такие вещи как:
			- unit type
			- current animation
			- scripted build id (они говорили, что покупка заскриптована), next item to purchase
			- area of effect spells in effect
			- modifier name
			- item name
			- ability name
			- pickup name
		- На картинке 17(а) говорится, что они "Embed" processing, в таблице 4 говорится, что размер 1 float, наверное это означает, либо то что они переводят имена и т.д. в embedding размера 1, либо передают это как ID, **тут не понятно, подробностей особо нет**
		  id:: 6765586a-d7e4-463e-9221-49829ce007f8
	- TODO У них есть интересный вход **Unit Embedding**, я пока не раскусил его смысл, похоже на некоторое сжатое представление состояния