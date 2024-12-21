repo:: [openai/gym: A toolkit for developing and comparing reinforcement learning algorithms.](https://github.com/openai/gym?ysclid=m4xxhs8liy706146817)

- Чем это является?
	- Это Python библиотека, которая предоставляет стандартизированный, унифицированный интерфейс (API) для различных окружений (environment) с их:
		- агентами (agent)
		- состояниями (observation/state space)
		- действиями (action)
		- вознаграждениями (reward)
	- Кроме предоставления API окружений, библиотека также предоставляет набор готовых окружений, наиболее популярные из которых:
		- [[Atari Games]] (около 200 игр)
			- Игры имеют одинаковый action space (соответствующий вводу геймпада)
			- Observation может быть как экран, так и дамп памяти
			- Reward разный для каждой игры
		- [[MuJuCo]]
			- Физический движок в основном для задач робототехники
- Чем это **Не** является?
	- Библиотекой для обучения агентов
		- Библиотека не предоставляет никаких RL алгоритмов для обучения агентов
- Как это выглядит?
	- ```python
	  env = gym.make("LunarLander-v2", render_mode="human") # создаем LunarLander-v2 env
	  observation, info = env.reset(seed=42) # устанавливаем начальное состояние
	  for _ in range(1000):
	     # env.action_space.sample берем рандомное действие 
	     # говорим env обработать полученное действие и вернуть нам 
	     # следующее состояние, observation, 
	     # полученную награду reward
	     # terminated нужно ли перезапустить игру?
	      observation, reward, terminated, truncated, info = env.step(env.action_space.sample())
	  
	      if terminated or truncated:
	          observation, info = env.reset()
	  
	  env.close()
	  ```
- Как это будет выглядеть с обучением?
	- Простейший вариант обучения алгоритм [[REINFORCE]] (псевдо py-like code)
	  
	  ```python
	  env = gym.make("CartPole-v1")
	  policy = PolicyNetwork(input_dim=<state_space_size>, output_dim=<action_dist_param_size>)
	  optimizer = optim.Adam(policy.parameters(), lr=1e-2)
	  gamma = 0.99  # Discount factor
	  
	  for episode in range(1000):
	      state = env.reset()
	      
	      log_probs = []
	      rewards = []
	      done = False
	      
	      while not done:
	          # Sample action from the policy
	          action_dist_parms = policy(state)
	          dist = <ActionDistribution>(action_dist_parms )
	          action = dist.sample()
	          log_probs.append(dist.log_prob(action))
	          
	          # Step in the environment
	          state, reward, done, _ = env.step(action.item())
	          rewards.append(reward)
	      
	      # rewards = [1,2,3,4]
	      # Compute discounted rewards
	      discounted_rewards = []
	      G = 0
	      for reward in reversed(rewards):
	          G = reward + gamma * G
	          discounted_rewards.insert(0, G)
	      
	      # discounted_rewards = [9.8, 8.8, 6.9, 4.0]
	      # Normalize rewards (optional for stability)
	      discounted_rewards = (discounted_rewards - discounted_rewards.mean()) / (discounted_rewards.std() + 1e-8)
	  
	      # Compute loss and update policy
	      # stimulate big log_prob for big reward 
	      loss = -torch.stack(log_probs) * discounted_rewards
	      loss = loss.sum()
	      optimizer.zero_grad()
	      loss.backward()
	      optimizer.step()
	  
	  env.close()
	  ```