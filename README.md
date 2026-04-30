    import random
    import matplotlib.pyplot as plt

#
DATA PENGELUARAN

    items = [
    ("Makan", 20000, 80),
    ("Kopi", 15000, 60),
    ("Jajan", 10000, 50),
    ("Transport", 10000, 70),
    ("Internet", 5000, 40),
    ]

    BUDGET = 50000

    POP_SIZE = 30
    GENERATIONS = 100
    MUTATION_RATE = 0.2
Pada bagian ini, program mendefinisikan data utama berupa daftar item pengeluaran yang akan dipilih. Setiap item terdiri dari nama, biaya, dan nilai kepuasan. Selain itu, ditentukan juga batas budget dan parameter algoritma seperti ukuran populasi, jumlah generasi, dan tingkat mutasi.

Penjelasan source code:

- items = [...] → list berisi tuple (nama, biaya, kepuasan)
- BUDGET = 50000 → batas maksimal total biaya
- POP_SIZE → jumlah individu dalam satu populasi
- GENERATIONS → berapa kali proses evolusi dilakukan
- MUTATION_RATE → peluang perubahan gen (0–1)
#
INIT

    def create_individual():
        return [random.randint(0,1) for _ in items]
    
    def init_population():
        return [create_individual() for _ in range(POP_SIZE)]
Bagian ini membuat populasi awal yang berisi solusi acak. Setiap solusi direpresentasikan dalam bentuk biner (0 dan 1) untuk menentukan apakah suatu item dipilih atau tidak.

Penjelasan source code:

- create_individual() → membuat satu individu
  - random.randint(0,1) → menghasilkan angka 0 atau 1
  - for _ in items → jumlah gen sesuai jumlah item
- init_population() → membuat banyak individu
  - [create_individual() for _ in range(POP_SIZE)] → membuat list populasi
# 
FITNESS

    def fitness(ind):
        total_cost = 0
        total_value = 0

    for gene, (name, cost, value) in zip(ind, items):
        if gene == 1:
            total_cost += cost
            total_value += value

    if total_cost > BUDGET:
        return 0

    return total_value
Bagian ini mengevaluasi kualitas setiap solusi dengan menghitung total biaya dan kepuasan. Jika biaya melebihi budget, maka solusi dianggap tidak valid.

Penjelasan source code:

- for gene, (name, cost, value) in zip(ind, items)
  - menggabungkan gen dengan data item
- if gene == 1: → hanya item yang dipilih yang dihitung
- total_cost += cost → menambahkan biaya
- total_value += value → menambahkan kepuasan
- if total_cost > BUDGET: return 0 → penalti jika melebihi budget
- return total_value → nilai fitness adalah kepuasan
#
SELECTION

    def selection(pop):
        return max(random.sample(pop, 3), key=fitness)
Bagian ini memilih individu terbaik untuk dijadikan induk menggunakan metode tournament selection.

Penjelasan source code:
- random.sample(pop, 3) → ambil 3 individu secara acak
- max(..., key=fitness) → pilih yang fitness-nya paling tinggi
# 
CROSSOVER

    def crossover(p1, p2):
        point = random.randint(1, len(p1)-1)
        return p1[:point] + p2[point:]
Bagian ini menggabungkan dua individu untuk menghasilkan individu baru.

Penjelasan source code:
- point = random.randint(1, len(p1)-1)
  - menentukan titik potong
- p1[:point] → bagian awal dari parent 1
- p2[point:] → bagian akhir dari parent 2
- return p1[:point] + p2[point:] → gabungan jadi anak
# 
MUTATION

    def mutate(ind):
        for i in range(len(ind)):
            if random.random() < MUTATION_RATE:
                ind[i] = 1 - ind[i]
        return ind
Bagian ini mengubah gen secara acak untuk menjaga variasi solusi.

Penjelasan source code:
- for i in range(len(ind)) → iterasi setiap gen
- random.random() < MUTATION_RATE
  - menentukan apakah gen dimutasi
- ind[i] = 1 - ind[i]
  - membalik nilai (0 jadi 1, 1 jadi 0)
#
DECODE

    def decode(ind):
        chosen = []
        total_cost = 0
        total_value = 0

    for gene, (name, cost, value) in zip(ind, items):
        if gene == 1:
            chosen.append(name)
            total_cost += cost
            total_value += value

    return chosen, total_cost, total_value
Bagian ini mengubah solusi biner menjadi bentuk yang mudah dipahami manusia.

Penjelasan source code:

- chosen.append(name) → menambahkan nama item yang dipilih
- total_cost += cost → menghitung total biaya
- total_value += value → menghitung total kepuasan
- return chosen, total_cost, total_value
  - mengembalikan hasil dalam bentuk lengkap
#
GA

    def GA():
        pop = init_population()
        best_hist = []

    print("\n===== OPTIMASI UANG JAJAN =====\n")

    for gen in range(GENERATIONS):

        pop = sorted(pop, key=fitness, reverse=True)

        best = pop[0]
        best_fit = fitness(best)

        best_hist.append(best_fit)

        if gen % 5 == 0:
            print(f"Gen {gen:3d} | Nilai kepuasan: {best_fit}")

        new_pop = pop[:2]

        while len(new_pop) < POP_SIZE:
            p1 = selection(pop)
            p2 = selection(pop)

            child = crossover(p1, p2)
            child = mutate(child)

            new_pop.append(child)

        pop = new_pop
Bagian utama yang menjalankan seluruh proses evolusi hingga menemukan solusi terbaik.

Penjelasan source code:
- pop = init_population() → membuat populasi awal
- for gen in range(GENERATIONS): → loop evolusi
- sorted(pop, key=fitness, reverse=True) → urutkan dari terbaik
- best = pop[0] → ambil individu terbaik
- best_hist.append(best_fit) → simpan untuk grafik
- new_pop = pop[:2] → elitism (simpan 2 terbaik)
- selection(pop) → pilih parent
- crossover(p1, p2) → buat anak
- mutate(child) → variasi gen
- pop = new_pop → update populasi
#
HASIL
    
    best = sorted(pop, key=fitness, reverse=True)[0]
    chosen, cost, value = decode(best)

    print("\n===== HASIL AKHIR =====")
    print("Pilihan:", chosen)
    print("Total biaya:", cost)
    print("Total kepuasan:", value)

    if cost <= BUDGET:
        print("Penjelasan: Pengeluaran optimal sesuai budget.")
    else:
        print("Penjelasan: Melebihi budget (tidak valid).")
Bagian ini menampilkan solusi terbaik yang ditemukan.

Penjelasan source code:
- sorted(pop, key=fitness, reverse=True)[0]
  - mengambil individu terbaik
- decode(best) → mengubah ke bentuk manusia
- print(...) → menampilkan:
 - item yang dipilih
 - total biaya
 - total kepuasan
- if cost <= BUDGET: → validasi hasil
#
VISUAL

    plt.figure()
    plt.plot(best_hist)
    plt.title("Perkembangan Kepuasan")
    plt.xlabel("Generasi")
    plt.ylabel("Fitness")
    plt.grid()
    plt.show()
Bagian ini menampilkan grafik perkembangan fitness selama proses evolusi.

Penjelasan source code:
- plt.figure() → membuat canvas grafik
- plt.plot(best_hist) → menggambar grafik
- plt.xlabel() dan plt.ylabel() → memberi label
- plt.title() → judul grafik
- plt.grid() → menampilkan grid
- plt.show() → menampilkan grafik ke layar
  
# 
RUN
    
    GA()

Bagian ini menjalankan program secara keseluruhan.

Penjelasan source code:
- GA() → memanggil fungsi utama

 
OPTIMASI UANG JAJAN

Gen   0 | Nilai kepuasan: 250
Gen   5 | Nilai kepuasan: 250
Gen  10 | Nilai kepuasan: 250
Gen  15 | Nilai kepuasan: 250
Gen  20 | Nilai kepuasan: 250
Gen  25 | Nilai kepuasan: 250
Gen  30 | Nilai kepuasan: 250
Gen  35 | Nilai kepuasan: 250
Gen  40 | Nilai kepuasan: 250
Gen  45 | Nilai kepuasan: 250
Gen  50 | Nilai kepuasan: 250
Gen  55 | Nilai kepuasan: 250
Gen  60 | Nilai kepuasan: 250
Gen  65 | Nilai kepuasan: 250
Gen  70 | Nilai kepuasan: 250
Gen  75 | Nilai kepuasan: 250
Gen  80 | Nilai kepuasan: 250
Gen  85 | Nilai kepuasan: 250
Gen  90 | Nilai kepuasan: 250
Gen  95 | Nilai kepuasan: 250

HASIL AKHIR 
Pilihan: ['Makan', 'Kopi', 'Transport', 'Internet']
Total biaya: 50000
Total kepuasan: 250
Penjelasan: Pengeluaran optimal sesuai budget.
<img width="509" height="405" alt="image" src="https://github.com/user-attachments/assets/f44b57a9-a174-4c54-b44d-7ac0a1ddedf9" />
