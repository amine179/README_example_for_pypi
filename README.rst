
MorEpiTool
----------

a RL based simulation environment for epidemic control

Installation
------------

Install using pip ``pip install MorEpiTool``

Requirements
------------

-  Python 3.6 or greater
-  numpy
-  networkX
-  matplotlib

Testing example
---------------

::

   from MorEpiTool import the_env
   import random
   import time
   import matplotlib.pyplot as plt

   #### initialize the env
   epidemic_data = [0.55, 0.76]
   demographic_data = [10000, 3, 0.44]
   env = the_env.MorEpiEnv(epidemic_data, demographic_data)

   num_ep = 100
   num_steps = 366


   step_reward_list = []
   reward_avrg_list = []

   try:
       for ep in range(num_ep):
           obs = env.reset()

           for step in range(num_steps):
               action = env.random_action()

               obs, reward, done, info = env.step(action, step)

               #env.render()

               #time.sleep(0.00001)

               step_reward_list.append(reward)

               if done:
                   print("episode finish at : ", step)
                   env.reset()
                   reward_avrg = sum(step_reward_list) / len(step_reward_list)

           reward_avrg_list.append(reward_avrg)
   except Exception as error:
       print ('oops')        

   plt.plot(reward_avrg_list)
   plt.show()
