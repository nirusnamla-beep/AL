Program dibuat untuk:

1. Menggunakan environment `Taxi-v3`.
2. Menampilkan rata-rata reward setiap 100 episode.
3. Membandingkan training 1000, 2000, dan 5000 episode.
4. Membuat grafik perbandingan.
5. Melakukan evaluasi tanpa exploration.
6. Menampilkan perjalanan agent sampai penumpang berhasil diantarkan.

## Konsep Reinforcement Learning

### State

State adalah kondisi lingkungan yang sedang diamati agent. Pada `Taxi-v3`, state tersusun dari posisi taksi, lokasi penumpang, dan lokasi tujuan.

### Action

Environment memiliki enam action:

| Nilai | Action |
|---:|---|
| 0 | South |
| 1 | North |
| 2 | East |
| 3 | West |
| 4 | Pickup |
| 5 | Dropoff |

### Reward

Reward yang umum diterima agent:

- `-1` untuk setiap langkah.
- `+20` ketika penumpang berhasil diantarkan.
- `-10` untuk `Pickup` atau `Dropoff` ilegal.

### Learning Rate dan Discount Factor

Rumus pembaruan Q-value:

```text
Q(s,a) = Q(s,a) + α [r + γ max Q(s',a') - Q(s,a)]
```

- Learning Rate `α` menentukan seberapa besar informasi baru mengubah Q-value lama.
- Discount Factor `γ` menentukan seberapa penting reward masa depan.

### Exploration dan Exploitation

- **Exploration** dilakukan dengan memilih action secara acak.
- **Exploitation** dilakukan dengan memilih action yang memiliki Q-value tertinggi.
- Program menggunakan strategi epsilon-greedy selama training.
- Evaluasi dilakukan tanpa exploration.

## Instalasi

```bash
pip install -r requirements.txt
```

Atau:

```bash
pip install gymnasium==1.2.3 numpy pandas matplotlib jupyter
```

## Kode Utama

### Fungsi Training

```python
def train_taxi(
    num_episodes,
    alpha=0.1,
    gamma=0.95,
    epsilon_start=1.0,
    epsilon_decay=0.995,
    min_epsilon=0.01,
    max_steps=200,
    seed=42,
):
    env = gym.make("Taxi-v3")
    state_size = env.observation_space.n
    action_size = env.action_space.n
    q_table = np.zeros((state_size, action_size))

    rewards = []
    average_rewards = []
    epsilon = epsilon_start
    rng = np.random.default_rng(seed)

    for episode in range(num_episodes):
        state, _ = env.reset(seed=seed + episode)
        total_reward = 0

        for step in range(max_steps):
            if rng.random() < epsilon:
                action = int(rng.integers(action_size))
            else:
                action = int(np.argmax(q_table[state]))

            next_state, reward, terminated, truncated, _ = env.step(action)

            if terminated:
                target = reward
            else:
                target = reward + gamma * np.max(q_table[next_state])

            q_table[state, action] += alpha * (
                target - q_table[state, action]
            )

            state = next_state
            total_reward += reward

            if terminated or truncated:
                break

        rewards.append(total_reward)
        epsilon = max(min_epsilon, epsilon * epsilon_decay)

        if (episode + 1) % 100 == 0:
            avg_reward = float(np.mean(rewards[-100:]))
            average_rewards.append(avg_reward)
            print(
                f"Training {num_episodes} | "
                f"Episode {episode + 1} | "
                f"Rata-rata reward = {avg_reward:.2f}"
            )

    env.close()
    return q_table, rewards, average_rewards
```

### Fungsi Evaluasi Tanpa Exploration

```python
def evaluate_taxi(q_table, evaluation_episodes=100, seed=9999):
    env = gym.make("Taxi-v3")
    evaluation_rewards = []
    successful_episodes = 0
    total_steps = []

    for episode in range(evaluation_episodes):
        state, _ = env.reset(seed=seed + episode)
        total_reward = 0

        for step in range(200):
            action = int(np.argmax(q_table[state]))

            state, reward, terminated, truncated, _ = env.step(action)
            total_reward += reward

            if terminated or truncated:
                if terminated and reward == 20:
                    successful_episodes += 1
                total_steps.append(step + 1)
                break

        evaluation_rewards.append(total_reward)

    env.close()

    return {
        "rata_rata_reward_evaluasi": np.mean(evaluation_rewards),
        "tingkat_keberhasilan": successful_episodes / evaluation_episodes,
        "rata_rata_langkah": np.mean(total_steps),
    }
```

## Hasil Eksperimen

### Rata-Rata Reward Setiap 100 Episode
<img width="2141" height="1778" alt="01_rata_rata_reward" src="https://github.com/user-attachments/assets/a9d331a8-88d5-4574-b1c5-32c691a11bd9" />
### Grafik Perbandingan
<img width="1961" height="1057" alt="02_grafik_perbandingan" src="https://github.com/user-attachments/assets/663b831f-38d4-47ba-a4da-dc11fa4897e7" />

### Evaluasi Tanpa Exploration
<img width="2141" height="737" alt="03_evaluasi_tanpa_exploration" src="https://github.com/user-attachments/assets/b962d92e-164d-4262-a5b8-8137bb183906" />

Ringkasan hasil:

| Episode Training | Reward 100 Episode Terakhir | Reward Evaluasi | Keberhasilan | Rata-rata Langkah |
|---:|---:|---:|---:|---:|
| 1000 | -5.51 | -120.15 | 38.0% | 128.13 |
| 2000 | 5.84 | -29.01 | 82.0% | 46.23 |
| 5000 | 7.20 | 8.04 | 100.0% | 12.96 |

### Perjalanan Agent
<img width="1520" height="1180" alt="04_perjalanan_agent" src="https://github.com/user-attachments/assets/7c29518f-0fc0-4289-877c-f585ec3232ce" />
Urutan action agent:

```text
West -> North -> North -> West -> North -> Pickup -> South -> East -> South -> East -> North -> East -> East -> North -> Dropoff
```

Hasil perjalanan:

```text
Jumlah langkah : 15
Total reward   : 6
Status         : Berhasil mengantarkan penumpang
```

## Analisis

Training 1000 episode masih menghasilkan reward evaluasi negatif dan tingkat keberhasilan yang rendah. Setelah 2000 episode, agent mulai memahami strategi yang lebih baik. Training 5000 episode memberikan hasil terbaik karena agent mencapai tingkat keberhasilan 100% serta membutuhkan langkah yang lebih sedikit.

Reward awal bernilai sangat negatif karena agent masih sering bergerak secara acak dan melakukan tindakan yang tidak efisien. Seiring proses training, exploration berkurang, exploitation meningkat, dan Q-table semakin baik.

## Kesimpulan

1. Q-Learning dapat digunakan untuk melatih agent pada environment `Taxi-v3`.
2. Rata-rata reward meningkat seiring bertambahnya episode.
3. Training 5000 episode menghasilkan performa terbaik.
4. Evaluasi tanpa exploration menunjukkan kemampuan agent berdasarkan hasil pembelajaran, bukan tindakan acak.
5. Agent berhasil mengambil penumpang dan mengantarkannya ke lokasi tujuan.

## Menjalankan Notebook

```bash
jupyter notebook Tugas_KC_Week12_Final.ipynb
```

Kemudian pilih **Run All Cells**.
