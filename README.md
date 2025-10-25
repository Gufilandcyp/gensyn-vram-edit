# gensyn-vram-edit
Balanced lowering of settings for bottlenecks and system glitches
---
* Important statement
## This guide only applies to GPU users. If you're using a CPU, you can still try these settings, but you may not get the full performance.
## If you are renting ready nodes like octaspace or similar, you should know that these settings will not work there because their ready systems are different.
## These settings are only prepared for those who have the ability to make manual settings on Vast.ai and similar GPU rental sites.

![Image Alt](https://github.com/Gufilandcyp/gensyn-vram-edit/blob/b28833bbc939a96d7d72fb386d61a71f9adb2afd/2025-10-25%2022_56_54-Gensyn%20_%20Testnet%20-%20Opera.png)


---

* **What do these settings do?**
* `Vram usage decreases`: VRAM usage increases after Qwen/Qwen 3-0.6B. This is necessary to reduce potential usage.
*  `Prevents node crashes`: It provides a permanent solution to crashes that require frequent resets. (At least the feedback received is in this direction.)

## 1.How to start?

* First, if you have a running node, you must stop it. If you are just installing, you can skip to step (4)
## Step 1:
`To do this, first stop the node with`

* `ctrl+c`
  
## Step 2: 
`paste this into the terminal`
```bash
nano rgym_exp/config/rg-swarm.yaml
```
* Now you'll see this page
![Image Alt](https://github.com/Gufilandcyp/gensyn-vram-edit/blob/75a2359e73bfdd96800edd636c1ae6ded729932f/2025-10-02_13_25_42-.png)
* dttype: downgrade float32 to bfloat16
* Save and exit with

`ctrl x+y enter`

* Restart node
```bash
./run_rl_swarm.sh
```

---

## Step 3: 
* If after a while your node still stops and crashes except for a general problem explained by gensyn, then add these settings as well.

`Stop node`

```bash
nano rgym_exp/config/rg-swarm.yaml
```
* change the settings as follows:
`num_generations 2`
`num_train_samples 1`
`num_transplant_trees 1`
`data type: bfloat16` 
`beam_size: 30`

`ctrl+x +y enter, and re run`
```bash
./run_rl_swarm.sh
```

---

# Step 4:
* If you are installing for the first time
* `git clone https://github.com/gensyn-ai/rl-swarm` After this code you entered when setting up node (dont forget to upload ur swarm pem after git clone)
`try this`
```bash
cd rl-swarm
```
`Then`
```bash
sed -i -E "s/(dtype:\s*)'float32'/\1'bfloat16'/" rgym_exp/config/rg-swarm.yaml && grep -nE "dtype:" rgym_exp/config/rg-swarm.yaml
```
# Now your VRAM settings will change before the node starts and the VRAM load will be reduced.

## Good luck in Swarm! :honeybee:

  
